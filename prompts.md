# Prompts

Aquí van **todos los prompts que lanzaste** para hacer el ejercicio, en el orden en que los
lanzaste, con el modelo y la herramienta de cada uno.

Esto no es papeleo. Lo que se revisa es **cómo pediste las cosas**, no solo lo que salió: un
resultado flojo con un prompt bueno y un resultado flojo con un prompt vago necesitan feedback
distinto, y sin este archivo no se distinguen.

## Cómo rellenarlo

- Un apartado `## Prompt N` por cada prompt.
- **Pega el prompt tal cual lo lanzaste**, dentro del bloque de código, aunque ocupe diez líneas
  y aunque tenga faltas. No lo reescribas para que quede bien: el que arreglaste mentalmente
  después no es el que lanzaste.
- Incluye también los que **no funcionaron**. Suelen ser los más útiles de leer.
- `Modelo` y `Herramienta` en todos. Si cambiaste de una a otra a mitad, se nota aquí.

Borra el ejemplo de abajo cuando escribas el primero.

---

## Prompt 1

**Modelo:** Opus 5.5 · Claude Pro
**Herramienta:** Claude Code v2.1.303


```
Antes de nada, léete el repo y devuélveme el estado real del proyecto: qué capabilities
  ya existen (auth…) y un diagrama rápido del modelo de datos actual (entidades y
  relaciones, en Mermaid). No propongas cambios todavía; solo quiero el mapa de lo que
  hay.
```

**Qué salió:** digrama de la implementación acutal, tablas de bd y servicios que se consumen acutualmente. 



## Prompt 2

**Modelo:** Opus 5.5 · Claude Pro
**Herramienta:** Claude Code v2.1.303


```
lee esto como parte del contexto y no hagas nada más **
  - Qué duele hoy: la daily de sincronización y el "¿en qué estás?" constante por
  Slack/chat. Nadie ve el estado del equipo sin interrumpir a alguien.
  - Quién cobra el valor: los pares, no un lead. No hay reporte hacia arriba y a un
  manager le daría igual. Duele a los dos devs que descubren tarde que iban a lo mismo, y
  al que interrumpe a otro para preguntar.
  - Episodio concreto: dos personas del equipo tocaron el mismo módulo la misma semana
  porque una empezó sin que la otra lo supiera. Dos días perdidos.
  - Qué reunión desaparece (respuesta honesta, no la vendas de más): la daily NO
  desaparece entera. Desaparece la ronda de "¿en qué estás?", que hoy se come la mitad de
  los 15 minutos. La parte de bloqueos sigue, y este MVP no la resuelve.
  - Usuarios / equipo: equipos remotos pequeños, 3–25 personas. Roles planos: en el MVP
  todos ven y editan lo mismo, sin jerarquía de permisos.
  - Primer usuario concreto: equipo de 6 personas de producto SaaS, en 3 husos horarios,
  que hoy usa un gestor de tareas pesado y una daily de 15 minutos por videollamada. Es un
  CASO DE ESTUDIO, no un cliente real: dilo en voz alta en vez de fingir lo contrario.
  - Fronteras: un espacio único compartido, sin entidad "equipo". Varios equipos
  separados, o gente en más de uno, queda FUERA del MVP: se anota como supuesto en el PRD,
  no se construye.
  - "Tiempo real" = ver los cambios de estado de las tareas sin refrescar ni preguntar. NO
  es chat, NO es videollamada, NO es colaboración simultánea sobre el mismo documento.
  - Es frescura, no presencia: el estado es de la TAREA, no de la persona. Nada de "quién
  está conectado ahora" ni indicadores de actividad; eso es vigilancia y lo rechazamos a
  propósito.
  - Forma de la señal: resumen que espera, no aviso que interrumpe. El caso es "llego por
  la mañana o vuelvo de una reunión y veo qué se ha movido". Sin notificaciones push.
  - Qué decisión cambia: no empezar algo que otra persona ya está tocando, y elegir lo
  siguiente sabiendo qué está libre. Si la única respuesta fuera "sentirse informado", el
  tiempo real no valdría lo que cuesta.
  - De dónde sale el estado: lo teclea la persona que hace la tarea, en segundos.
  Derivarlo de señales externas (Git/PRs, CI, calendario) está FUERA del MVP: es otro
  producto, con integraciones y OAuth de terceros.
  - Por qué se sostiene: no porque sea más agradable, sino porque son dos clics sobre una
  lista ya abierta, sin campos obligatorios, sin decidir sprint ni estimación. Y quien lo
  escribe cobra en el momento: esa misma lista es su cola de trabajo, la mira para decidir
  qué coge, y de paso deja de recibir interrupciones preguntándole cómo va. Si el
  beneficio fuera solo para los demás, no lo escribiría.
  - Si la información se queda vieja: el producto pierde el sentido, y lo asumo. Es el
  riesgo #1 a validar, no un detalle. La mitigación es que actualizar cueste dos clics, no
  obligar a nadie.
  - Es donde se hace el trabajo, no donde se cuenta: sustituye al gestor de tareas, no
  convive con él. FlowSync crea las tareas, no lee las de otro sitio. Convivir exigiría
  doble actualización, que es como muere esta categoría.
  - Renuncia explícita a sprints, estimaciones, épicas, backlog priorizado e informes. Un
  equipo que necesite eso no es nuestro usuario.
  - "Menos rollo que Jira" = crear una tarea y cambiarle el estado en segundos, sin flujos
  de configuración ni campos obligatorios. Lo mínimo para saber quién está en qué.
  - Qué necesita una tarea en el MVP: título, responsable, estado y fecha de vencimiento.
  La fecha, para ver de un vistazo qué se ha pasado de plazo.
  - Cómo se consume la lista: filtrando por estado, para centrarse en lo pendiente.
  - Éxito para el usuario: dejar de hacer la ronda de "¿en qué estás?" de la daily porque
  el estado del equipo se ve de un vistazo.
  - Criterio a una semana de uso real: que el equipo cancele esa ronda y nadie pida que
  vuelva. Si la siguen haciendo igual, no funcionó.
  - Cuánto construir: una vertical fina y usable de punta a punta, no el andamiaje amplio
  de un producto. Prefiero una capability terminada a tres a medias.
  **
```

**Qué salió:** nada, me confirmó que leyó la información como contexto y no hizo nada más. 


## Prompt 3

**Modelo:** Opus 5.5 · Claude Pro
**Herramienta:** Claude Code v2.1.303


```
❯ necesito proponer el alcance para el MVP por lo tanto necesito que me hagas las cinco preguntas que más reducirían la incertidumbre sobre el problema, los usuarios y el alcance. Acota a una sola ronda, está prohído bajar al modelo de datos o a los endpoints, quedate a nivel de producto con mis respuestas continua sin abrir otra rodan de preguntas.
```

**Qué salió:** Lista de preguntas: 
```
1. Si solo cupiera una vertical terminada, ¿cuál?
- a) Mi cola de trabajo: crear tareas y cambiarles el estado en dos clics. Es lo que hace que la gente escriba.
- b) La vista del equipo: ver qué está haciendo cada uno y qué ha cambiado. Es lo que elimina la ronda de "¿en qué estás?".

Las dos se necesitan, pero el orden decide qué se recorta si el tiempo no da.

2. ¿Qué significa que una tarea esté "libre", y qué campos son obligatorios de verdad?
Pides título, responsable, estado y fecha, pero también "sin campos obligatorios". ¿Se puede crear una tarea sin responsable (libre para quien la coja) y sin fecha? ¿O libre quiere decir "tiene responsable pero aún no ha empezado"?

3. ¿Qué estados hay, y son fijos o los configura el equipo?
Mi propuesta es un conjunto cerrado de tres: Pendiente · En curso · Hecha. ¿Hace falta un "Bloqueada", aunque los bloqueos no los resuelva este MVP? ¿O ese estado invitaría a esperar algo que el producto no da?

4. ¿Qué mínimo resuelve "llego por la mañana y veo qué se ha movido"?
- a) Basta con que la lista esté al día sin refrescar.
- b) Hace falta distinguir lo que ha cambiado desde mi última visita: marcar los cambios o un resumen del tipo "desde ayer: X pasó a En curso".

La b añade bastante alcance. ¿Entra en el MVP o es la segunda vertical?

5. ¿Basta con ver título, responsable y estado para evitar el choque del episodio?
En ese episodio, dos personas tocaron el mismo módulo con tareas que seguramente tenían nombres distintos. Para evitar el choque, ¿basta con ver de un vistazo quién tiene qué tarea en curso? ¿O hace falta alguna forma ligera de agrupar por área o módulo? Si hace falta, está muy cerca de las "épicas" que has descartado.

RESPUESTAS: ❯ 1. b), 2. libre para quien la coja, 3. acepto tu propuesta, 4.a), 5. NA 

PROPUESTA DE MVP (no usé otro promt en automático después de responder las preguntas me dio la propuesta)

```

## Prompt 4

**Modelo:** Opus 5.5 · Claude Pro
**Herramienta:** Claude Code v2.1.303


```

modifica el RNF-4 quiero que el limite suba a 25 personas y suba a 800 tareas, identifica en que otros archivos o lugares es necesario actualizar esta información, en los archivos que identificaste haz las modificaciones para que todo este homologado con este ajuste
```

**Qué salió:** Se modificaron todas las partes para cambiar el alacance


## Prompt 5

**Modelo:** Opus 5.5 · Claude Pro
**Herramienta:** Claude Code v2.1.303


```
Ahora cambia de sombrero: sé un revisor de producto adversarial. Lee el PRD que acabas
  de escribir y atácalo. ¿Qué requisitos son ambiguos o no testables? ¿Qué supuesto, si es
  falso, tumba el MVP entero? ¿Dónde hay scope creep escondido? ¿Qué métrica de éxito no
  se puede medir de verdad? Prioriza por riesgo.
```

**Qué salió:** Me levanta varios escenarios, unicamente acepto el que indica que con un vistazo no puedo ver que cambios hubo en las tareas 

Revisión adversarial del PRD de FlowSync

Ordenada por riesgo, de mayor a menor. No he tocado los archivos.

🔴 Crítico: puede tumbar el MVP

1. El escenario principal no lo resuelve ninguna funcionalidad, y la más cara apunta a otro.
JTBD-1 dice: "llego por la mañana y veo qué ha cambiado". Pero el resumen de cambios está fuera de alcance, y RF-23 (actualización en vivo) solo ayuda a quien ya tiene la lista abierta. Quien llega por la mañana ve lo mismo que vería recargando la página: el estado actual, no lo que se ha movido. Así que el tiempo real, que es lo más costoso de construir, sirve a un escenario secundario, y el principal queda cubierto solo a medias.
→ Hay que elegir: o el escenario de verdad es "mirar el estado actual" y JTBD-1 se reescribe, o falta algo mínimo que muestre los cambios.

2. Que "estado de la tarea" equivalga a "¿en qué estás?" es un supuesto no declarado.
La ronda de la daily no solo dice qué: también dice cómo va ("me queda la parte de pagos, mañana lo cierro"). Una tarea "En curso" durante 8 días no aporta nada nuevo cada mañana. Sin notas ni comentarios (fuera de alcance), el equipo puede mantener la ronda para ese "cómo va", y entonces M1 falla aunque todo lo demás funcione.
→ Hay que declararlo como [SUPUESTO] y validarlo antes de construir.

3. El supuesto del episodio está mal planteado.
"Ver título, responsable y estado basta para evitar choques" solo es cierto si todo trabajo empieza con una tarea creada. En el episodio original, quien empezó sin avisar probablemente tampoco habría creado una tarea. Además, dos tareas con títulos distintos pueden tocar el mismo módulo y nada lo detecta.
→ La regla de equipo "si no está en FlowSync, no lo empiezas" es un supuesto del que depende todo, y no aparece en ninguna parte.

4. "Sustituye al gestor, no convive" choca con una prueba de una semana.
Ningún equipo migra su backlog a una herramienta en prueba, y no hay importación (está fuera de alcance). En la práctica convivirán ambas herramientas y habrá doble actualización, que es justo lo que el propio PRD dice que mata esta categoría. La validación, tal como está planteada, provoca el fallo que quiere evitar.

5. Al ampliar el segmento a 25 personas, se rompen otros supuestos.
- Una sola lista plana: con 25 personas y hasta 800 tareas, "de un vistazo" deja de ser cierto.
- Sin filtro de "mis tareas": el producto se justifica porque la lista es la cola de trabajo de cada persona, y no hay forma de ver solo la propia.
- Sin entidad "equipo": con 25 personas casi siempre hay subequipos, así que esa decisión pasa de simplificación a carencia.
- Las tareas hechas se acumulan: como no se archivan, con el tiempo la mayor parte de la lista son Hecha.

🟠 Requisitos contradictorios o no testables

┌──────────────┬────────────────────────────────────────────────────────────────────────────────┐
│     Ref.     │                                    Problema                                    │
├──────────────┼────────────────────────────────────────────────────────────────────────────────┤
│ RF-14 frente │ RF-14 dice que gana el primero que coge la tarea. RNF-11 dice que gana el      │
│  a RF-15 y   │ último cambio guardado, y RF-15 deja que cualquiera se reasigne la tarea a sí  │
│ RNF-11       │ mismo. La protección de RF-14 es decorativa y además contradice a RNF-11.      │
│              │ "Casi a la vez" no es testable.                                                │
├──────────────┼────────────────────────────────────────────────────────────────────────────────┤
│ RF-13 frente │ Coger una tarea la deja en Pendiente. Una tarea pendiente con responsable no   │
│  a JTBD-2    │ deja claro si alguien la está tocando, y JTBD-2 consiste justo en saber eso.   │
├──────────────┼────────────────────────────────────────────────────────────────────────────────┤
│ RF-22 /      │ Como se calcula con la fecha local de quien mira, la misma tarea sale vencida  │
│ RNF-6        │ para unas personas y no para otras en el mismo equipo. Es testable, pero       │
│              │ confunde, y nadie lo ha decidido a propósito.                                  │
├──────────────┼────────────────────────────────────────────────────────────────────────────────┤
│ RF-24        │ "Deja de poder actualizarse sola" no fija a partir de cuánto tiempo sin datos  │
│              │ se muestra el aviso. Así no se puede probar.                                   │
├──────────────┼────────────────────────────────────────────────────────────────────────────────┤
│ RNF-1        │ "Condiciones normales de red" no está definido.                                │
├──────────────┼────────────────────────────────────────────────────────────────────────────────┤
│ RNF-2        │ "Una persona que ya conoce el producto" no define a quién se mide ni cómo.     │
├──────────────┼────────────────────────────────────────────────────────────────────────────────┤
│ RNF-4        │ "Degradación apreciable" no es medible; falta un umbral de tiempo con esa      │
│              │ carga.                                                                         │
├──────────────┼────────────────────────────────────────────────────────────────────────────────┤
│ RF-7         │ Dos personas con el mismo nombre no se distinguen.                             │
├──────────────┼────────────────────────────────────────────────────────────────────────────────┤
│ RF-12        │ "Dos clics" no dice desde dónde se cuentan ni si vale el teclado (RNF-8).      │
└──────────────┴────────────────────────────────────────────────────────────────────────────────┘

🟡 Scope creep escondido

- RF-24 (avisar de que la lista no está al día y ponerse al día al reconectar). Es lo primero que se recorta (la actualización en vivo) y, aun así, el PRD le añade la gestión de la reconexión.
- RF-23 en una sola línea. Debajo hay infraestructura nueva de tiempo real que el stack actual no tiene, y eso no se refleja en el PRD.
- RF-14 (concurrencia al coger una tarea). Además de contradictorio, es lógica extra.
- RF-17 (eliminar tareas). Lo añadí yo; no estaba en el alcance.
- RNF-4 con 25 personas y 800 tareas. Obliga a hacer pruebas de carga que antes no hacían falta.
- RNF-8 (accesibilidad con teclado) y RNF-6 (lógica de husos horarios). Son razonables, pero cada uno es trabajo que no aparece en las épicas.

🟠 Métricas que no se pueden medir de verdad

- M1 (principal): no hay ningún equipo real (es un caso de estudio), así que en el contexto del curso es imposible de medir. Además pide dos semanas, cuando el criterio acordado era una.
- M2: que cada persona confirme cada día si sus tareas En curso son correctas es la ronda de "¿en qué estás?" con otro nombre. Medirla reintroduce el problema.
- M3: el problema solo ha pasado una vez en el pasado. Cero choques en una semana es lo esperable con o sin FlowSync, así que no demuestra nada.
- M4: necesita una semana de referencia previa que no existe. Contar mensajes es autodeclarado, y RNF-10 prohíbe recoger esos datos de forma automática.
- M5: saber qué tareas cambiaron de estado durante la semana exige un historial, que está fuera de alcance. Tampoco dice quién hizo el cambio, porque cualquiera puede editar cualquier tarea.

Qué atacaría primero

1. Resolver el punto 1, porque decide si el tiempo real se queda en el MVP o se aparca.
2. Declarar como [SUPUESTO] los puntos 2 y 3 y añadir una forma barata de validarlos.
3. Decidir si el segmento de 3–25 personas se queda. Si se queda, el filtro "mis tareas" o por responsable deja de ser opcional.
4. Rehacer M1, M2, M4 y M5 con métodos que se puedan ejecutar sin historial y sin un equipo real.



## Prompt 6

**Modelo:** Opus 5.5 · Claude Pro
**Herramienta:** Claude Code v2.1.303


```

 De tus hayazgos acepto el numero 1. si quiero que se muestren los cambios como dentro del alcance, arregla este cambio para incluirlo en documentación tanto en alcance-mvp.md como en flowsync-mvp.md hazme un maximo de 3 preguntas para resolver dudas y dejar bien acotado el alcance, no reescribas secciones que no estén relacionadas con este hallazgo y nuevo alcance
```

**Qué salió:** realiza los ajustes del cambio que solicite en todos los documentos incluido el readme, el alcance del mvp y el propio mvp. 

