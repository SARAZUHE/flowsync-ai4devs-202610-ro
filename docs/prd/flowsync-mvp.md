# PRD del MVP de FlowSync

> **Fuente:** `docs/prd/alcance-mvp.md` (alcance consensuado).
>
> **El primer usuario es un caso de estudio, no un cliente real.** Ninguna cifra de este documento sale de un estudio de mercado. Lo que no está validado lleva la etiqueta **[SUPUESTO]**.

---

## 1. Problema y contexto

En los equipos remotos pequeños, saber en qué está cada persona exige preguntarlo.

- **La daily se dedica a sincronizar.** En una daily de 15 minutos, la ronda de "¿en qué estás?" se come la mitad del tiempo.
- **Interrupciones constantes.** Fuera de la daily, la gente pregunta por Slack o chat "¿cómo va X?" y corta el trabajo de otra persona.
- **El trabajo se duplica sin que nadie lo sepa.** En el caso de estudio, dos personas tocaron el mismo módulo la misma semana porque una empezó sin saber que la otra ya estaba en ello. Se perdieron dos días.

El gestor de tareas que usa hoy el equipo es pesado: sprints, estimaciones y campos obligatorios. Actualizarlo cuesta tanto que nadie lo mantiene al día. Por eso la información de verdad viaja por la daily y por el chat.

**Qué resuelve el MVP y qué no.** Elimina la ronda de "¿en qué estás?". La daily no desaparece: la parte de bloqueos sigue y este MVP no la aborda.

**Decisión que el producto debe cambiar.** No empezar algo que otra persona ya está tocando, y elegir lo siguiente sabiendo qué está libre.

## 2. Usuarios y jobs-to-be-done

### Segmento
- Equipos remotos pequeños, de 3 a 25 personas, repartidos en varios husos horarios.
- Roles planos: todos ven y editan lo mismo, sin jerarquía de permisos.
- El valor lo reciben los compañeros del equipo, no un lead ni un manager. No hay reporte hacia arriba.

### Primer usuario (caso de estudio)
Un equipo de producto SaaS de 6 personas en 3 husos horarios. Hoy usa un gestor de tareas pesado y una daily de 15 minutos por videollamada.

### Quién no es nuestro usuario
Un equipo que necesite sprints, estimaciones, épicas, backlog priorizado o informes.

### Jobs-to-be-done
| # | Cuando… | quiero… | para… |
|---|---|---|---|
| JTBD-1 | llego por la mañana o vuelvo de una reunión | ver de un vistazo en qué está cada persona y qué ha cambiado de estado | no tener que preguntar ni esperar a la daily |
| JTBD-2 | voy a empezar algo | comprobar si alguien ya lo tiene en curso | no duplicar trabajo |
| JTBD-3 | termino una tarea y busco la siguiente | ver qué tareas están libres y cogerme una | elegir sabiendo qué no está tocando nadie |
| JTBD-4 | empiezo o termino una tarea | actualizar su estado en segundos | que nadie tenga que interrumpirme para preguntar cómo va |
| JTBD-5 | se me ocurre algo que hay que hacer | apuntarlo solo con un título | que no se pierda, sin rellenar formularios |

## 3. Propuesta de valor

**Una lista compartida donde cada persona mantiene el estado de sus tareas con dos clics. Así el estado del equipo se ve de un vistazo y deja de hacer falta preguntar.**

- **Es donde se hace el trabajo, no donde se cuenta.** FlowSync sustituye al gestor de tareas, no convive con él. Las tareas se crean aquí. Convivir con otra herramienta obligaría a actualizar dos veces, y así es como mueren los productos de esta categoría.
- **Quien escribe también gana.** La lista es la cola de trabajo de cada persona: la consulta para decidir qué coge, y además deja de recibir interrupciones. Si el beneficio fuera solo para los demás, nadie la mantendría.
- **Coste mínimo de actualizar.** Solo el título es obligatorio. No hay sprints, estimaciones ni flujos que configurar.
- **Frescura, no presencia.** Los cambios de estado de las tareas se ven sin recargar la página. El estado es de la tarea, nunca de la persona: no hay "quién está conectado" ni indicadores de actividad.
- **Una señal que espera, no que interrumpe.** No hay notificaciones push. La información está ahí cuando alguien abre la lista.

## 4. Alcance / Fuera de alcance

### Alcance
Una sola vertical, fina y usable de punta a punta: **la vista del equipo**, más lo mínimo para alimentarla.

1. Acceso con cuenta a un único espacio compartido.
2. Lista compartida de tareas. Cada tarea tiene título, responsable (o "libre"), estado y fecha de vencimiento.
3. Crear una tarea en la que solo el título es obligatorio.
4. Cambiar el estado en dos clics como máximo. Hay tres estados fijos: *Pendiente*, *En curso* y *Hecha*.
5. Coger una tarea libre con un clic.
6. Filtrar la lista por estado.
7. Distinguir a simple vista las tareas vencidas.
8. Actualización de la lista sin recargar la página.
9. Bloque «Qué se ha movido» encima de la lista, con los cambios que han hecho otras personas desde tu última visita.

**Si el tiempo no da, se recorta en este orden.** Los puntos 1–5 y 9 no se recortan.
1. La actualización en vivo (8) pasa a "al día cada vez que se abre o recarga la lista".
2. El resaltado de vencidas (7).
3. El filtro por estado (6).

### Fuera de alcance
- **Gestión pesada:** sprints, estimaciones, épicas de producto, backlog priorizado e informes.
- **Bloqueos:** no hay estado "Bloqueada" ni nada para gestionarlos.
- **Más allá de «Qué se ha movido»:** ni historial completo de una tarea, ni marcas de "nuevo" dentro de la propia lista, ni cambios de título, fecha o eliminaciones en el resumen.
- **Comunicación:** notificaciones push, email, chat, videollamada, comentarios y edición simultánea de un mismo documento.
- **Presencia y actividad de personas:** nada de "quién está conectado", "visto por última vez" ni indicadores de actividad. Se rechaza a propósito porque es vigilancia. La última visita que usa «Qué se ha movido» es privada de cada persona y nadie más la ve.
- **Estado derivado de fuera:** Git, PRs, CI, calendario, integraciones u OAuth de terceros.
- **Importar o sincronizar tareas de otras herramientas.**
- **Varios equipos:** ni espacios separados, ni personas en varios equipos, ni invitaciones.
- **Roles y permisos:** sin jerarquía.
- **Campos obligatorios más allá del título.**

## 5. Épicas del MVP

- **E1 «Cuentas y acceso»:** registro, inicio y cierre de sesión, y pertenencia de cada persona con cuenta al único espacio compartido.
- **E2 «Gestión de tareas»:** crear, editar, eliminar, asignar o coger y cambiar de estado las tareas de la lista compartida.
- **E3 «Actividad del equipo»:** la vista del estado del equipo (lista, filtro por estado, vencidas, cambios visibles sin recargar y bloque «Qué se ha movido» desde tu última visita). Se centra en la actividad de las **tareas**, nunca en la de las personas.

## 6. Requisitos funcionales

Las marcas de cada requisito significan:
- **(existe):** ya implementado en el repo.
- **(adaptar):** existe pero hay que ajustarlo.
- Sin marca: requisito nuevo.

### E1 · Cuentas y acceso
- **RF-1 (existe).** Una persona puede registrarse con email y contraseña; el nombre es opcional. Al terminar el registro queda dentro, sin otro paso de login.
- **RF-2 (existe).** Una persona registrada puede iniciar sesión con su email y su contraseña. Si se equivoca, ve un mensaje en castellano que no revela cuál de los dos datos falla.
- **RF-3 (existe).** Una persona puede cerrar sesión. Después de hacerlo no puede ver ni modificar tareas hasta que vuelva a entrar.
- **RF-4 (existe).** Al recargar el navegador, la sesión se mantiene y no hay que volver a entrar.
- **RF-5 (adaptar).** Sin sesión no se puede ver, crear ni modificar ninguna tarea. Quien intente acceder sin sesión acaba en la pantalla de inicio de sesión.
- **RF-6 (adaptar).** Tras iniciar sesión o registrarse, la pantalla de inicio es la lista de tareas del equipo, no el perfil.
- **RF-7.** Toda persona con cuenta pertenece al único espacio compartido y aparece como posible responsable de cualquier tarea. Se identifica por su nombre o, si no lo tiene, por su email.

### E2 · Gestión de tareas
- **RF-8.** Cualquier persona con sesión puede crear una tarea escribiendo solo el título. Responsable y fecha de vencimiento son opcionales al crearla.
- **RF-9.** El título no puede estar vacío ni contener solo espacios. Si lo está, la tarea no se crea y se muestra un mensaje en castellano junto al campo. Su longitud máxima es de 200 caracteres **[SUPUESTO]**.
- **RF-10.** Toda tarea nueva empieza en estado *Pendiente*. Si no se indica responsable, queda **libre**. Si no se indica fecha, no vence.
- **RF-11.** Los únicos estados posibles son *Pendiente*, *En curso* y *Hecha*. Ningún usuario puede añadir, renombrar ni eliminar estados.
- **RF-12.** Desde la propia lista se puede cambiar el estado de cualquier tarea con dos clics como máximo, sin salir de la lista. Se permite cualquier transición entre los tres estados, incluido volver atrás para corregir un error **[SUPUESTO]**.
- **RF-13.** Una tarea libre muestra una acción para cogerla. Con un solo clic, la persona que la coge pasa a ser su responsable. El estado no cambia automáticamente **[SUPUESTO]**.
- **RF-14.** Si dos personas intentan coger la misma tarea libre casi a la vez, solo una queda como responsable. La otra ve un aviso de que la tarea ya la ha cogido alguien, con su nombre, y su intento no sobrescribe el de la primera.
- **RF-15.** Cualquier persona puede cambiar el responsable de cualquier tarea a otra persona del espacio, o dejarla libre.
- **RF-16.** Cualquier persona puede editar el título de cualquier tarea (con las reglas de RF-9) y poner, cambiar o quitar su fecha de vencimiento.
- **RF-17.** Cualquier persona puede eliminar una tarea tras confirmarlo **[SUPUESTO: no se discutió en el alcance; se incluye para que la lista sea usable si alguien crea una tarea por error]**.
- **RF-18.** Si un cambio no se puede guardar, la persona ve un aviso en castellano y la lista no muestra el cambio como hecho.

### E3 · Actividad del equipo
- **RF-19.** La lista muestra todas las tareas del espacio. De cada una se ve el título, el responsable (o la etiqueta "Libre"), el estado y la fecha de vencimiento, si la tiene.
- **RF-20.** La lista se ordena primero por estado, en el orden *En curso*, *Pendiente*, *Hecha*. Dentro de cada estado, por fecha de vencimiento ascendente, con las tareas sin fecha al final **[SUPUESTO]**.
- **RF-21.** La lista se puede filtrar por estado: *Todas*, *Pendiente*, *En curso* o *Hecha*. Al abrir la lista se muestran todas **[SUPUESTO]**.
- **RF-22.** Una tarea está **vencida** cuando su fecha de vencimiento es anterior al día actual de quien mira y su estado no es *Hecha*. Las tareas vencidas se distinguen a simple vista y no solo por el color. Una tarea que vence hoy todavía no está vencida.
- **RF-23.** Cuando alguien crea, edita, elimina, coge, reasigna o cambia de estado una tarea, cualquier otra persona que tenga la lista abierta ve el cambio sin recargar la página.
- **RF-24.** Si la lista deja de poder actualizarse sola (por ejemplo, porque se perdió la conexión), se indica de forma visible que puede no estar al día. Al recuperarse, la lista se pone al día sin que haya que recargar.
- **RF-25.** El producto no muestra quién está conectado, quién está mirando la lista, cuándo se vio a alguien por última vez ni ningún otro indicador de actividad de las personas. La única excepción es el momento en que cada persona dio por vistos los cambios (RF-28). Ese dato es privado, solo sirve para su propio bloque «Qué se ha movido» y nunca se muestra a otra persona.
- **RF-26.** El producto no envía notificaciones push, emails ni avisos sonoros por cambios en las tareas.
- **RF-27.** Encima de la lista hay un bloque «Qué se ha movido». Muestra los cambios que han hecho **otras personas** desde la última visita de quien mira; los cambios propios no aparecen. Solo cuentan tres tipos de cambio:
  - una tarea nueva;
  - un cambio de estado;
  - un cambio de responsable: alguien coge, reasigna o libera una tarea.
- **RF-28.** "Última visita" es el momento en que la persona marcó por última vez el bloque como visto, con una acción explícita del propio bloque. Recargar la página o cerrar sesión no vacía el bloque: los cambios se acumulan hasta que la persona los marca como vistos **[SUPUESTO]**.
- **RF-29.** Cada línea del bloque corresponde a un cambio y muestra:
  - el título de la tarea;
  - qué pasó: "creada", "Pendiente → En curso" o "cogida", "reasignada a X", "liberada";
  - quién lo hizo;
  - cuándo, con la hora local de quien mira.

  Las líneas van de la más reciente a la más antigua **[SUPUESTO]**.
- **RF-30.** Si no hay cambios de otras personas desde la última visita, el bloque lo dice expresamente ("Nada se ha movido desde tu última visita") en lugar de desaparecer. En la primera visita de una persona, el bloque empieza vacío **[SUPUESTO]**.
- **RF-31.** Si una tarea con cambios pendientes de ver se elimina, sus líneas desaparecen del bloque.
- **RF-32.** Mientras el bloque está abierto, los cambios nuevos de otras personas se añaden sin recargar, con la misma frescura que la lista (RF-23 y RNF-1). Si la actualización en vivo se recorta, el bloque se pone al día cada vez que se abre o recarga la lista.

## 7. Requisitos no funcionales

- **RNF-1 · Frescura.** Un cambio hecho por una persona aparece en la lista abierta de las demás en 5 segundos como máximo, en condiciones normales de red **[SUPUESTO]**.
- **RNF-2 · Coste de actualizar.** Cambiar el estado de una tarea cuesta 2 clics como máximo desde la lista. Coger una tarea libre cuesta 1 clic. Crear una tarea solo con título lleva 10 segundos como máximo a una persona que ya conoce el producto **[SUPUESTO]**.
- **RNF-3 · Respuesta de la interfaz.** Tras crear, editar o cambiar el estado de una tarea, la propia persona ve el resultado en menos de 1 segundo **[SUPUESTO]**.
- **RNF-4 · Volumen.** El producto funciona sin degradación apreciable con 25 personas usándolo a la vez y 800 tareas en el espacio **[SUPUESTO: dimensionado al techo del segmento]**.
- **RNF-5 · Idioma.** Toda la interfaz y todos los mensajes de error están en castellano.
- **RNF-6 · Husos horarios.** Las fechas de vencimiento son días, sin hora. "Vencida" y "hoy" se calculan con la fecha local de quien mira, para que funcione en un equipo repartido en 3 husos.
- **RNF-7 · Plataforma.** Funciona en las últimas versiones de Chrome, Firefox y Safari de escritorio **[SUPUESTO]**. El uso desde el móvil no es objetivo del MVP **[SUPUESTO]**.
- **RNF-8 · Accesibilidad.** Ninguna información depende solo del color (estado, vencida, libre). Las acciones principales (crear, cambiar de estado y coger) se pueden hacer con el teclado.
- **RNF-9 · Seguridad.** Las contraseñas nunca se guardan ni se muestran en claro. Ningún dato de tareas o personas es accesible sin sesión iniciada.
- **RNF-10 · Privacidad.** No se recogen datos de actividad de las personas (conexión, tiempo en pantalla, clics) ni para mostrarlos ni para medir. La única excepción es la última visita privada de RF-28, que no se usa para nada más. Las métricas de la sección 9 se obtienen por observación del equipo o del estado de las tareas.
- **RNF-11 · Integridad.** Ningún cambio confirmado se pierde. Si dos personas editan a la vez el mismo dato de una tarea, prevalece el último cambio guardado y ambas acaban viendo el mismo valor final.

## 8. Restricciones

- **Stack existente.** El backend es AdonisJS 7 con SQLite y el frontend, React 19 con Vite. El MVP se construye sobre ese stack, sin cambiar de framework.
- **La autenticación ya existe.** Registro, login, logout y perfil están implementados y se reutilizan. Solo se adaptan RF-5 y RF-6; no se rehace la autenticación.
- **Espacio único.** No existe la entidad "equipo". Todo el que tiene cuenta comparte el mismo espacio.
- **Sin dependencias de terceros.** No hay integraciones, OAuth externo ni servicios externos de notificaciones o tiempo real.
- **Una vertical terminada.** Se prefiere una capability completa de punta a punta antes que varias a medias. Si el tiempo aprieta, se aplica el orden de recorte de la sección 4.
- **Contexto.** Es un proyecto de práctica del curso, validado contra un caso de estudio y no contra un cliente real.

## 9. Métricas de éxito

La validación es una prueba de una semana de uso real con el equipo del caso de estudio **[SUPUESTO: en el curso se simula; los umbrales no están validados con datos reales]**.

| # | Métrica | Cómo se mide | Umbral de éxito |
|---|---|---|---|
| M1 · **Principal** | La ronda de "¿en qué estás?" deja de hacerse | Al final de la semana 1, el equipo decide si cancela la ronda; en la semana 2 se comprueba si alguien pide recuperarla | Ronda cancelada al día 7 y nadie pide que vuelva durante la semana 2. Si se sigue haciendo igual, **el MVP no funcionó** |
| M2 · Frescura (riesgo #1) | Las tareas *En curso* reflejan lo que cada persona está haciendo de verdad | Comprobación diaria: cada persona confirma si sus tareas *En curso* son correctas | ≥ 90 % de las tareas *En curso* son correctas en cada comprobación **[SUPUESTO]** |
| M3 · Choques | Dos personas trabajan en lo mismo sin saberlo | Cada persona lo declara al final de la semana | 0 casos durante la prueba |
| M4 · Interrupciones | Mensajes del tipo "¿en qué estás?" o "¿cómo va X?" | Recuento autodeclarado, comparado con una semana anterior al MVP | Baja respecto a la semana anterior. El porcentaje exacto **[SUPUESTO]** queda pendiente de medir primero la línea base |
| M5 · Adopción | Personas del equipo que crean o actualizan tareas | Recuento de personas distintas que figuran como responsables de tareas que cambiaron de estado durante la semana (dato de la tarea, no de la persona) | 6 de 6 personas |
| M6 · Coste de actualizar | Se cumple RNF-2 | Prueba guiada con cada persona del equipo | 100 % de los cambios de estado en ≤ 2 clics. Crear una tarea lleva ≤ 10 s |

**Señal de alarma.** Si al día 3 M2 está por debajo del umbral, la información se está quedando vieja (riesgo #1). Hay que revisar por qué antes de seguir con la prueba, sin obligar a nadie a actualizar.
