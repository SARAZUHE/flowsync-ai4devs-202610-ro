# Spec viva: Cuentas y acceso

## Purpose
Permitir que una persona cree una cuenta en FlowSync, inicie y cierre sesión, mantenga la sesión entre recargas del navegador y consulte su perfil, de modo que solo quien tiene una sesión válida accede a las pantallas y a la API privadas.

## Requirements

### Requirement: Registro de cuenta por API
El sistema SHALL permitir crear una cuenta mediante `POST /api/v1/auth/signup` con los campos `fullName` (texto o `null`), `email`, `password` y `passwordConfirmation`, y SHALL responder con los datos públicos del usuario creado y un token de acceso, envueltos en `{ "data": { "user": {...}, "token": "..." } }`, dejando a la persona con sesión iniciada sin necesidad de un inicio de sesión aparte.

#### Scenario: Alta con nombre completo
- **WHEN** se envía una petición de registro con `fullName` "Ada Lovelace", un email que no está registrado, una contraseña de entre 8 y 32 caracteres y la misma contraseña en `passwordConfirmation`
- **THEN** la respuesta es correcta (2xx) y contiene `data.user` con `id`, `fullName` ("Ada Lovelace"), `email`, `createdAt`, `updatedAt` e `initials`, y `data.token` con un token de acceso; la respuesta no incluye la contraseña

#### Scenario: Alta sin nombre
- **WHEN** se envía una petición de registro válida con `fullName` igual a `null`
- **THEN** la cuenta se crea y `data.user.fullName` vale `null`

#### Scenario: El token del registro sirve para acceder
- **WHEN** tras registrarse se usa el `data.token` recibido como `Authorization: Bearer <token>` en `GET /api/v1/account/profile`
- **THEN** la API devuelve el perfil de la cuenta recién creada

### Requirement: Validación de los datos de registro
El sistema SHALL rechazar las peticiones de registro con datos no válidos con un estado 422 y un cuerpo `{ "errors": [ ... ] }` en el que cada error indica `message`, `rule` y `field`, sin crear la cuenta.

#### Scenario: Email ya registrado
- **WHEN** se envía una petición de registro con un email que ya pertenece a una cuenta existente
- **THEN** la respuesta es 422 con un error de `field` "email" y `rule` "database.unique"

#### Scenario: Email con formato no válido
- **WHEN** se envía una petición de registro cuyo `email` no tiene formato de dirección de correo
- **THEN** la respuesta es 422 con un error de `field` "email" y `rule` "email"

#### Scenario: Contraseña demasiado corta o demasiado larga
- **WHEN** se envía una petición de registro con una `password` de menos de 8 caracteres o de más de 32
- **THEN** la respuesta es 422 con un error de `field` "password" y `rule` "minLength" o "maxLength" respectivamente

#### Scenario: La confirmación no coincide
- **WHEN** se envía una petición de registro en la que `passwordConfirmation` es distinta de `password`
- **THEN** la respuesta es 422 con un error de `field` "passwordConfirmation" y `rule` "sameAs"

#### Scenario: Campo obligatorio vacío
- **WHEN** se envía una petición de registro en la que `email`, `password` o `passwordConfirmation` falta o es una cadena vacía
- **THEN** la respuesta es 422 con un error de `rule` "required" para ese campo

### Requirement: Inicio de sesión por API
El sistema SHALL permitir iniciar sesión mediante `POST /api/v1/auth/login` con `email` y `password`, y SHALL responder, cuando las credenciales son correctas, con los datos públicos del usuario y un token de acceso nuevo en `{ "data": { "user": {...}, "token": "..." } }`.

#### Scenario: Credenciales correctas
- **WHEN** se envía una petición de inicio de sesión con el email y la contraseña de una cuenta existente
- **THEN** la respuesta es correcta (2xx) y contiene `data.user` con los datos públicos de esa cuenta y `data.token` con un token de acceso

#### Scenario: Contraseña incorrecta o email desconocido
- **WHEN** se envía una petición de inicio de sesión con un email válido que no está registrado, o con la contraseña equivocada de una cuenta existente
- **THEN** la respuesta es 400 con el cuerpo `{ "errors": [{ "message": "Invalid user credentials" }] }`, idéntica en ambos casos

#### Scenario: Datos de inicio de sesión no válidos
- **WHEN** se envía una petición de inicio de sesión sin email, con un email sin formato de dirección de correo o sin contraseña
- **THEN** la respuesta es 422 con un error de validación para el campo correspondiente

### Requirement: Consulta del perfil por API
El sistema SHALL devolver los datos públicos de la persona autenticada en `GET /api/v1/account/profile` cuando la petición incluye un token de acceso válido en la cabecera `Authorization: Bearer <token>`, y SHALL responder 401 en cualquier otro caso.

#### Scenario: Token válido
- **WHEN** se consulta el perfil con un token de acceso válido
- **THEN** la respuesta es correcta (2xx) con `{ "data": { "id", "fullName", "email", "createdAt", "updatedAt", "initials" } }` de la persona dueña del token

#### Scenario: Sin token o con token no válido
- **WHEN** se consulta el perfil sin cabecera `Authorization`, con un token inventado o con un token ya revocado
- **THEN** la respuesta es 401 con el cuerpo `{ "errors": [{ "message": "Unauthorized access" }] }`

### Requirement: Cierre de sesión por API
El sistema SHALL invalidar el token de acceso usado en la petición cuando se llama a `POST /api/v1/account/logout` con un token válido, y SHALL responder `{ "message": "Logged out successfully" }` sin el envoltorio `data`.

#### Scenario: Cierre de sesión con token válido
- **WHEN** se llama al cierre de sesión con un token de acceso válido
- **THEN** la respuesta es correcta (2xx) con `{ "message": "Logged out successfully" }`, y a partir de ese momento ese mismo token recibe 401 en las rutas protegidas

#### Scenario: Cierre de sesión sin token válido
- **WHEN** se llama al cierre de sesión sin token o con un token no válido
- **THEN** la respuesta es 401 con `{ "errors": [{ "message": "Unauthorized access" }] }`

### Requirement: Iniciales del usuario
El sistema SHALL incluir en los datos públicos del usuario un campo `initials`, en mayúsculas, calculado a partir del nombre completo o, si no lo hay, del email.

#### Scenario: Nombre con dos o más palabras
- **WHEN** el usuario tiene como nombre completo "Ada Lovelace"
- **THEN** `initials` vale "AL" (primera letra de la primera y de la segunda palabra)

#### Scenario: Nombre de una sola palabra
- **WHEN** el usuario tiene como nombre completo "Ada"
- **THEN** `initials` vale "AD" (las dos primeras letras del nombre)

#### Scenario: Sin nombre
- **WHEN** el usuario no tiene nombre completo y su email es "ada@example.com"
- **THEN** `initials` vale "AE" (primera letra de lo que hay antes y de lo que hay después de la "@")

### Requirement: Pantalla de registro
El sistema SHALL ofrecer en `/register` un formulario "Crea tu cuenta" con los campos "Nombre completo (opcional)", "Email", "Contraseña" y "Repite la contraseña", que crea la cuenta, inicia la sesión y lleva a la persona a su perfil.

#### Scenario: Registro correcto
- **WHEN** una persona sin sesión rellena el formulario con datos válidos y pulsa "Crear cuenta"
- **THEN** el botón muestra "Creando cuenta…" y queda deshabilitado mientras se procesa, y al terminar la persona llega a `/profile` con su sesión iniciada

#### Scenario: Nombre en blanco
- **WHEN** una persona deja "Nombre completo" vacío o solo con espacios y completa el registro
- **THEN** la cuenta se crea sin nombre y el perfil muestra "Sin nombre"

#### Scenario: Contraseñas distintas
- **WHEN** una persona escribe en "Repite la contraseña" algo distinto de "Contraseña" y pulsa "Crear cuenta"
- **THEN** aparece "Las contraseñas no coinciden." bajo "Repite la contraseña" sin que se envíe nada al servidor

#### Scenario: Errores de validación del servidor
- **WHEN** el servidor rechaza el registro por validación
- **THEN** cada mensaje aparece en castellano bajo su campo; por ejemplo, "Ese email ya está registrado. Inicia sesión en su lugar." bajo "Email", "Introduce una dirección de email válida." o "la contraseña debe tener al menos 8 caracteres." bajo "Contraseña"

#### Scenario: Servidor inaccesible o con error
- **WHEN** al pulsar "Crear cuenta" no se puede conectar con el servidor o este responde con un error interno
- **THEN** aparece un aviso sobre el formulario con "No se pudo conectar con el servidor. Comprueba que el backend está arrancado." o "Algo ha ido mal en el servidor. Inténtalo de nuevo en un momento.", respectivamente

#### Scenario: Pista y enlace
- **WHEN** una persona abre la pantalla de registro
- **THEN** ve bajo "Contraseña" la indicación "Entre 8 y 32 caracteres." y, al pie, "¿Ya tienes cuenta? Inicia sesión" con un enlace a `/login`

### Requirement: Pantalla de inicio de sesión
El sistema SHALL ofrecer en `/login` un formulario "Inicia sesión" con los campos "Email" y "Contraseña" que inicia la sesión y lleva a la persona a su perfil.

#### Scenario: Inicio de sesión correcto
- **WHEN** una persona sin sesión introduce el email y la contraseña de su cuenta y pulsa "Entrar"
- **THEN** el botón muestra "Entrando…" y queda deshabilitado mientras se procesa, y al terminar la persona llega a `/profile`

#### Scenario: Credenciales incorrectas
- **WHEN** una persona introduce un email o una contraseña que no corresponden a ninguna cuenta y pulsa "Entrar"
- **THEN** aparece sobre el formulario el aviso "El email o la contraseña no son correctos." y sigue en `/login`

#### Scenario: Campos vacíos o email mal formado
- **WHEN** una persona pulsa "Entrar" con el email vacío, con un email sin formato válido o con la contraseña vacía
- **THEN** aparece bajo el campo afectado un mensaje como "Falta rellenar el email.", "Introduce una dirección de email válida." o "Falta rellenar la contraseña."

#### Scenario: Enlace al registro
- **WHEN** una persona abre la pantalla de inicio de sesión
- **THEN** ve al pie "¿Aún no tienes cuenta? Crea una" con un enlace a `/register`

### Requirement: Persistencia y restauración de la sesión
El sistema SHALL conservar el token de acceso en el navegador tras registrarse o iniciar sesión y SHALL comprobarlo contra el servidor cada vez que se carga la aplicación, mostrando un indicador de carga mientras lo hace.

#### Scenario: Recarga con sesión válida
- **WHEN** una persona con sesión iniciada recarga la página o vuelve a abrir la aplicación en el mismo navegador
- **THEN** ve un indicador de carga y después entra en su perfil sin volver a introducir credenciales

#### Scenario: Token rechazado por el servidor
- **WHEN** se carga la aplicación con un token guardado que el servidor ya no acepta (por ejemplo, revocado)
- **THEN** el token se elimina del navegador y la persona llega a `/login` con el aviso "Tu sesión ha caducado. Vuelve a iniciar sesión."

#### Scenario: Servidor inaccesible al cargar
- **WHEN** se carga la aplicación con un token guardado y no se puede conectar con el servidor
- **THEN** la persona llega a `/login` con el aviso "No se pudo conectar con el servidor. Comprueba que el backend está arrancado.", el token se conserva en el navegador y, si recarga cuando el servidor vuelve a estar disponible, recupera la sesión

#### Scenario: El aviso desaparece al iniciar sesión
- **WHEN** en `/login` se muestra el aviso de sesión perdida y la persona inicia sesión correctamente
- **THEN** llega a su perfil y el aviso ya no se muestra

### Requirement: Protección de rutas en pantalla
El sistema SHALL mostrar el perfil solo a personas con sesión válida y las pantallas de inicio de sesión y registro solo a personas sin sesión, redirigiendo en cada caso a la pantalla que corresponde.

#### Scenario: Acceso al perfil sin sesión
- **WHEN** una persona sin sesión abre `/profile`
- **THEN** se le lleva a `/login`

#### Scenario: Acceso a login o registro con sesión
- **WHEN** una persona con sesión válida abre `/login` o `/register`
- **THEN** se le lleva a `/profile`

#### Scenario: Ruta desconocida
- **WHEN** una persona abre cualquier otra dirección de la aplicación (incluida la raíz `/`)
- **THEN** se le lleva a `/profile` si tiene sesión, o a `/login` si no la tiene

### Requirement: Pantalla de perfil
El sistema SHALL mostrar en `/profile` los datos de la persona con sesión iniciada: sus iniciales, su nombre completo, su email y la fecha en que creó la cuenta.

#### Scenario: Perfil con nombre
- **WHEN** una persona con nombre completo "Ada Lovelace" abre su perfil
- **THEN** ve un círculo con "AL", el nombre "Ada Lovelace", su email y la línea "Miembro desde" con la fecha de alta en formato largo en castellano (por ejemplo, "10 de noviembre de 2026")

#### Scenario: Perfil sin nombre
- **WHEN** una persona que se registró sin nombre abre su perfil
- **THEN** ve "Sin nombre" en lugar del nombre y las iniciales calculadas a partir de su email

### Requirement: Cierre de sesión en pantalla
El sistema SHALL ofrecer en el perfil un botón "Cerrar sesión" que termina la sesión en el navegador y lleva a la persona a la pantalla de inicio de sesión.

#### Scenario: Cerrar sesión
- **WHEN** una persona con sesión pulsa "Cerrar sesión" en su perfil
- **THEN** el token se borra del navegador, se pide al servidor que lo invalide y la persona llega a `/login` sin ningún aviso de error

#### Scenario: Cierre de sesión con el servidor caído
- **WHEN** una persona pulsa "Cerrar sesión" y la petición al servidor falla
- **THEN** la sesión se cierra igualmente en el navegador y la persona llega a `/login` sin ningún aviso
