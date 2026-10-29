# Alcance del MVP de FlowSync

> Alcance consensuado, base para el PRD. Todavía no es el PRD.
>
> **El primer usuario es un caso de estudio, no un cliente real.**

## 1. Problema

- **Qué duele hoy.** La mitad de los 15 minutos de la daily se va en la ronda de "¿en qué estás?". Durante el día, la gente se interrumpe por Slack o chat para preguntar cómo va algo. Nadie ve el estado del equipo sin interrumpir a alguien.
- **Episodio concreto.** Dos personas del equipo tocaron el mismo módulo la misma semana porque una empezó sin que la otra lo supiera. Se perdieron dos días.
- **Qué desaparece y qué no.** Desaparece la ronda de "¿en qué estás?". La daily **no** desaparece entera: la parte de bloqueos sigue y este MVP no la resuelve.
- **Qué decisión cambia.** No empezar algo que otra persona ya está tocando, y elegir lo siguiente sabiendo qué está libre. Si la única ganancia fuera "sentirse informado", el tiempo real no valdría lo que cuesta.

## 2. Usuarios

- **Segmento.** Equipos remotos pequeños, de 3 a 25 personas, con roles planos: todos ven y editan lo mismo, sin jerarquía de permisos.
- **Primer usuario (caso de estudio).** Equipo de producto SaaS de 6 personas en 3 husos horarios. Hoy usa un gestor de tareas pesado y una daily de 15 minutos por videollamada.
- **Quién se beneficia.** Los compañeros del equipo, no un lead: no hay reporte hacia arriba y a un manager le daría igual. Se benefician los devs que hoy descubren tarde que iban a lo mismo y quien tiene que interrumpir a otro para preguntar.
- **Quién no es nuestro usuario.** Un equipo que necesite sprints, estimaciones, épicas, backlog priorizado o informes.

## 3. Propuesta de valor

Una lista compartida donde cada persona mantiene el estado de sus tareas con dos clics. Así el estado del equipo se ve de un vistazo y deja de hacer falta preguntar.

- **Es donde se hace el trabajo, no donde se cuenta.** Sustituye al gestor de tareas en vez de convivir con él: las tareas se crean en FlowSync y no se leen de otro sitio. Convivir obligaría a actualizar en dos sitios, y así es como mueren los productos de esta categoría.
- **Por qué se mantiene al día.** Cambiar un estado son dos clics sobre una lista que ya está abierta, sin campos obligatorios ni decisiones de sprint o estimación. Quien la escribe se beneficia en el momento: la lista es su cola de trabajo y deja de recibir interrupciones.
- **"Tiempo real" significa frescura, no presencia.** Los cambios de estado de las tareas se ven sin refrescar ni preguntar. El estado es de la tarea, no de la persona.
- **Una señal que espera, no que interrumpe.** El caso de uso es "llego por la mañana o vuelvo de una reunión y miro qué se ha movido". Sin notificaciones push.
- **"Menos rollo que Jira".** Crear una tarea y cambiarle el estado en segundos, sin flujos de configuración. Lo mínimo para saber quién está en qué.

### Criterio de éxito
Tras una semana de uso real, el equipo cancela la ronda de "¿en qué estás?" y nadie pide que vuelva. Si la siguen haciendo igual, el MVP no funcionó.

### Riesgo principal a validar
**La información se queda vieja.** Si nadie la actualiza, el producto pierde el sentido. Se asume como el riesgo número 1, no como un detalle. La mitigación es que actualizar cueste dos clics, sin obligar a nadie.

## 4. Alcance

Es una sola vertical, fina y usable de punta a punta: **la vista del equipo**, más lo mínimo para alimentarla. Mejor una capability terminada que tres a medias.

1. **Lista compartida por todo el equipo.** Un solo espacio en el que todos ven y editan lo mismo. En cada tarea se ve el título, el responsable (o que está libre), el estado y la fecha de vencimiento.
2. **Crear una tarea en segundos.** Solo el título es obligatorio. Una tarea sin responsable está **libre** para quien la coja; sin fecha, no vence. El estado inicial es *Pendiente*.
3. **Cambiar el estado en dos clics.** Hay tres estados fijos que nadie configura: *Pendiente → En curso → Hecha*.
4. **Coger una tarea libre con un clic.** Quien la coge pasa a ser su responsable.
5. **Filtrar por estado,** para centrarse en lo pendiente o en lo que está en curso.
6. **Ver lo vencido sin buscarlo.** Las tareas con la fecha pasada que no están hechas se distinguen a simple vista.
7. **La lista se actualiza sola, sin refrescar.** Si alguien cambia un estado, los demás lo ven en su lista abierta.
8. **«Qué se ha movido» desde tu última visita.** Encima de la lista, un bloque resume lo que han hecho otras personas desde la última vez que la miraste: cambios de estado, tareas cogidas, reasignadas o liberadas, y tareas nuevas. Es el escenario principal: "llego por la mañana o vuelvo de una reunión y veo qué se ha movido".

### Si el tiempo no da, se recorta en este orden
1. La actualización en vivo (7) pasa a "al día cada vez que abres la lista".
2. El resaltado de lo vencido (6).
3. El filtro por estado (5).

El núcleo (1–4 y 8) no se recorta: sin él, la vertical no sirve para su propósito.

### Supuestos
- Todas las personas con cuenta entran en el mismo espacio único. No hay entidad "equipo".
- Ver título, responsable y estado basta para evitar choques como el del episodio. No hace falta agrupar por área o módulo.
- Todos pueden editar cualquier tarea, también reasignarla.
- Para saber qué es "desde tu última visita", el producto guarda en privado, para cada persona, el momento en que dio por vistos los cambios. Ese dato solo sirve para su propio bloque «Qué se ha movido» y nunca se muestra a nadie.

## 5. NO-alcance

Queda fuera a propósito; no se construye en el MVP:

- **Gestión pesada:** sprints, estimaciones, épicas, backlog priorizado e informes.
- **Bloqueos:** no hay estado "Bloqueada". Los bloqueos se siguen tratando en la daily.
- **Más allá de «Qué se ha movido»:** ni historial completo de una tarea, ni marcas de "nuevo" dentro de la propia lista, ni cambios de título, fecha o eliminaciones en el resumen.
- **Comunicación:** notificaciones push, chat, videollamada y edición simultánea del mismo documento.
- **Presencia o actividad de personas:** nada de "quién está conectado" ni indicadores de actividad. Se rechaza a propósito porque es vigilancia. Tu última visita es privada y nadie más la ve.
- **Estado derivado de fuera:** Git, PRs, CI, calendario, integraciones u OAuth de terceros. Sería otro producto.
- **Convivir con otro gestor:** no se importan ni se sincronizan tareas de otras herramientas.
- **Varios equipos:** ni espacios separados ni gente en más de un equipo. Se anota como supuesto, no se construye.
- **Roles y permisos:** sin jerarquía; todos ven y editan lo mismo.
- **Campos obligatorios más allá del título.**
