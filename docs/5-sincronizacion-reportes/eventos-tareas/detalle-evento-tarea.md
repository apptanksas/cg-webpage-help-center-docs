---
title: "Detalle de Evento o Tarea"
modulo_id: "eventask-detalle-informacion"
nombre_funcionalidad: "Consulta y Gestión de Eventos y Tareas Ganaderas"
categoria: "sincronizacion-reportes"
submodulo: "eventos-tareas"
version_minima_app: "2026.10.1"
fecha_actualizacion: "2026-10-09"
intenciones_y_sinonimos:
  - "como marcar una tarea como completada en la app"
  - "donde veo los detalles de un evento o tarea en el calendario"
  - "como cambiar el estado de una tarea a en progreso o pendiente"
  - "por que no me aparece el boton de editar en un evento proyectado"
  - "como ver a que animal o trabajador esta asignada una actividad"
  - "que significa el aviso de actividad proyectada en el futuro"
---

# Consulta y Gestión de Eventos y Tareas Ganaderas

### Resumen y Alcance Funcional
Pantalla de detalle que centraliza la visualización técnica y operativa tanto de **Eventos informativos** como de **Tareas de manejo** programadas en la finca ganadera. Permite a administradores y operarios consultar las instrucciones de trabajo, fechas de ejecución, frecuencia de repetición, animales vinculados o colaboradores asignados, y registrar observaciones de campo.

La experiencia visual y operativa se adapta automáticamente según el tipo de actividad consultada:
- **En Eventos informativos:** Funciona como una ficha de consulta de hitos o recordatorios clave de la finca (como aniversarios, visitas técnicas o fechas límite), manteniendo una visualización limpia sin requerir cumplimiento ni avances de estados.
- **En Tareas operativas:** Funciona como un centro de gestión de labores de campo, permitiendo avanzar o retroceder el ciclo de vida de la actividad (marcar como pendiente, en progreso o completada), registrar notas de cumplimiento y auditar quién culminó la labor y en qué fecha.

- **¿Funciona sin conexión a internet (Modo Offline)?:** Sí.
- **Comportamiento de sincronización:** Toda la información de eventos y tareas se almacena y consulta en la base de datos local del dispositivo móvil. Los cambios de estado de una tarea y las observaciones ingresadas se guardan de manera inmediata en el teléfono y quedan registrados para sincronizarse automáticamente con el servidor y los demás dispositivos de la finca en cuanto se disponga de conexión a internet.

### Reglas de Negocio y Restricciones
- **Diferenciación estructural entre Eventos y Tareas:**
    - **Evento:** Representa un recordatorio o suceso informativo de fecha fija. No cuenta con un estado operativo (**Pendiente**, **En progreso** o **Completada**), no muestra la fila de estado en la ficha de detalles, no incluye sección de culminación y no dispone de botones de acción para completar o cambiar estado en la parte inferior.
    - **Tarea:** Representa una labor de manejo que exige ejecución en campo. Dispone de un ciclo de vida con tres estados posibles (**Pendiente**, **En progreso** y **Completada**) y permite registrar notas y auditoría de finalización.
- **Código visual de la cabecera:**
    - En un **Evento**, la cabecera superior y la barra de navegación utilizan el color principal institucional de la aplicación.
    - En una **Tarea**, el fondo de la cabecera adopta dinámicamente el color asociado a su estado operativo actual: azul oscuro para **Pendiente**, naranja para **En progreso** y verde oscuro para **Completada**.
- **Permisos de usuario para completar tareas:** La actualización del estado de una labor (marcar como pendiente, en progreso o completada) exige que el usuario disponga del permiso de gestión y cumplimiento de tareas en la finca ganadera.
- **Restricción de tareas pasadas (Fecha vencida):** Los botones de acción para cambiar el estado de una tarea no se muestran si la fecha programada de la labor es anterior al día actual.
- **Comportamiento ante Proyecciones Futuras:**
    - Si la actividad visualizada corresponde a una ocurrencia proyectada por recurrencia en el futuro (y no a una entrada creada o editada individualmente), se muestra un mensaje informativo de advertencia contextual:
      - Para eventos: *"Este es un evento proyectado en el futuro..."*.
      - Para tareas: *"Esta es una tarea proyectada en el futuro..."*.
      - Las ocurrencias proyectadas (sean eventos o tareas) no presentan el botón circular de edición con ícono de lápiz en la cabecera para preservar la integridad de la serie recurrente original.
      - En tareas proyectadas a futuro, los botones de acción de cambio de estado se ocultan por completo hasta que llegue la fecha o se individualice la labor.
- **Registro de auditoría al completar:** Al marcar una tarea como completada, el sistema captura automáticamente la fecha exacta del día y asocia el nombre del usuario que realizó la acción, mostrando además el título con formato tachado para denotar visualmente su culminación.
- **Enlace directo al animal:** Si el evento o la tarea está asociado a un bovino específico de la finca, su código o nombre se presenta como un enlace interactivo para navegar de inmediato a su ficha individual.
- **Independencia del Centro de Notificaciones:** Los eventos y tareas creados en el calendario de la finca no generan registros locales automáticos en la pestaña de notificaciones de la aplicación. Su consulta y seguimiento se efectúan directamente a través de las rutas oficiales de acceso.

### Flujo Paso a Paso para el Usuario
- **Ruta de acceso en la aplicación:**
    - *Ruta 1 (Desde el Menú Lateral):* Menú lateral principal > Opción **Eventos y Tareas** > Seleccionar una actividad del calendario o lista.
    - *Ruta 2 (Desde el Panel Principal de la Finca):* Pantalla de inicio de la finca > Bloque de calendario de eventos y tareas > Pulsar sobre la actividad deseada.
    - *Ruta 3 (Desde Datos veterinarios del animal):* Menu inferior animal > **Datos veterinarios** > Tabla de eventos y tareas > Pulsar sobre el registro de interés.

1. Al ingresar a la pantalla, identifique el tipo de actividad y su estado en la cabecera superior:
    - **Color de cabecera:** Si consulta un evento, el fondo es del color corporativo principal de la aplicación. Si consulta una tarea, el color cambia según el estado (azul para pendiente, naranja para en progreso, verde para completada).
     - **Título de la actividad:** Muestra el nombre asignado al evento o la tarea. Si se trata de una tarea completada, el título se mostrará con una línea tachada.
     - **Fecha y tiempo relativo:** Se visualiza el ícono de calendario junto a la fecha completa en formato legible (día de la semana, día del mes, mes y año) y el cálculo de tiempo relativo (por ejemplo, *"hoy"*, *"en 3 días"* o *"hace 2 días"*).

#### 1. Modificación de la Actividad
- Si la actividad no es una proyección recurrente futura, en la esquina inferior de la cabecera se ubica el botón circular de edición con el ícono de lápiz.
- Al presionar este botón, la aplicación redirige al formulario de edición correspondiente (sea de evento o de tarea), donde podrá modificar el nombre, la descripción, la fecha, el animal vinculado, la frecuencia de repetición o los responsables.

#### 2. Ficha de Detalles de la Actividad

En el cuerpo central de la pantalla se despliegan los parámetros configurados según el tipo de actividad:

- **Aviso de proyección futura (si aplica):** Si la actividad es proyectada por recurrencia, en la parte superior del contenido aparece un mensaje de advertencia específico: *"Este es un evento proyectado en el futuro..."* o *"Esta es una tarea proyectada en el futuro..."*.
- **Descripción:** Detalle explicativo de las instrucciones o propósito de la actividad. Si no tiene texto adicional, se indica que no posee valor registrado.
- **Repetir:** Frecuencia de repetición configurada (por ejemplo, diaria, semanal, mensual o ninguna).
- **Repetir hasta:** Fecha límite de vigencia de la recurrencia (visible únicamente si la actividad tiene repetición programada).
- **Estado (Solo en Tareas):** Muestra la situación operativa actual de la labor (**Pendiente**, **En progreso** o **Completada**). En eventos informativos, esta fila se omite por completo.
- **Visibilidad:** Perfiles de usuario de la finca que pueden ver la actividad (o la indicación de visible para todos).
- **Usuario asignado:** Nombre del colaborador responsable de atender la actividad, o la indicación personal cuando está asignada al propio usuario en sesión.
- **Animal asignado:** Si la actividad corresponde al manejo de un ejemplar específico, se muestra su código o nombre. Al presionar sobre el dato, la aplicación abre automáticamente el resumen y ficha del animal.
- **Notas / Observación:** Comentarios complementarios o anotaciones de campo guardadas previamente.

#### 3. Información de Culminación (Exclusiva para Tareas Completadas)

Si la actividad es una tarea y ya ha sido finalizada, se incorpora una sección adicional delimitada por una línea divisoria:

- **Completada por:** Nombre del colaborador que registró la finalización de la labor.
- **Completada el:** Fecha en la que se llevó a cabo el registro de cumplimiento.
*(Esta sección no se muestra en tareas pendientes o en progreso, ni en ningún evento informativo).*

#### 4. Gestión del Estado de la Tarea (Exclusiva para Tareas Activas)

En eventos informativos o en tareas proyectadas a futuro, esta sección no está presente. En tareas activas individuales cuya fecha programada sea igual o posterior al día actual, se habilitan los botones de acción operativa en la parte inferior:

- **Marcar como pendiente:** Disponible si la tarea se encuentra en progreso o completada, para retornar la labor a la cola de pendientes.
- **Marcar como en progreso:** Disponible si la tarea no se encuentra en curso (está pendiente o completada), para indicar que los trabajos de campo han iniciado.
- **Marcar como completada:** Disponible si la tarea está pendiente o en progreso:
    - Al pulsar este botón, se despliega una ventana modal titulada **Marcar como completada**.
    - En el campo de texto multilínea **Notas / Observación**, el operario puede redactar opcionalmente cualquier apunte sobre el trabajo realizado (por ejemplo, dosis aplicada, novedad en el potrero o condición del animal).
    - Para confirmar, presione el botón **Completar**. Si desea desistir, presione **Cancelar**.

**Pantalla de llegada tras guardar o actualizar:** La pantalla se recarga de forma inmediata mostrando la tarea con el nuevo estado, los nuevos colores correspondientes y los datos de cumplimiento actualizados. Si se presiona el botón de regreso en la barra superior, el usuario vuelve a la pantalla de origen (calendario o ficha del animal).

### Matriz de Errores y Soluciones
| Mensaje en la App / Síntoma | Causa Real | Respuesta Sugerida por el Agente | Criterio de Escalamiento Humano |
| :--- | :--- | :--- | :--- |
| "La tarea ya no existe." o "El evento ya no existe." | La actividad fue eliminada desde otro dispositivo de la finca o ya no se encuentra en la base de datos local | "La actividad seleccionada ya no se encuentra registrada en la finca, posiblemente porque fue eliminada o reasignada. La aplicación regresará a la pantalla anterior para actualizar la lista." | Si el usuario afirma que no eliminó la actividad y desapareció involuntariamente, verificar posibles conflictos de sincronización en su cuenta. |
| "No aparecen los botones para marcar como completada o en progreso, ni la fila de estado" | La actividad consultada corresponde a un Evento informativo (hito de calendario) y no a una Tarea operativa de manejo | "La actividad que está visualizando es un Evento informativo del calendario. Los eventos sirven como recordatorios de fecha fija y no requieren gestión de estados ni botones de cumplimiento. Si requiere seguimiento operativo, cree la actividad como Tarea." | Si el usuario afirma haberla creado como tarea pero aparece como evento, verificar en el formulario de edición el tipo seleccionado. |
| "No aparecen los botones de acción en una tarea activa" | La fecha programada para la labor ya pasó (es anterior al día actual), o la tarea es una proyección futura no individualizada | "Verifique la fecha de la labor. Por regla del sistema, las tareas cuya fecha programada ya venció no permiten cambiar de estado desde esta vista. Asimismo, si es una proyección futura recurrente, los botones se habilitarán al llegar su fecha." | Si la fecha es de hoy o futura y el usuario no puede cambiar el estado, revisar si su rol en la finca cuenta con el permiso para completar tareas. |
| "No aparece el botón de edición con el lápiz en la cabecera" | Se está visualizando una ocurrencia proyectada a futuro derivada de una serie recurrente (evento o tarea) | "Esta actividad corresponde a una proyección futura de una serie recurrente. Para editar las condiciones o la fecha de la serie, debe ingresar a la actividad original configurada en el calendario." | Si el usuario requiere ayuda para modificar o reprogramar series recurrentes, guiarlo paso a paso en el calendario de eventos. |
| "Aparece un mensaje de advertencia sobre actividad proyectada en el futuro" | La actividad consultada fue generada automáticamente por la frecuencia de repetición y aún no es una entrada individualizada | "El mensaje le recuerda que esta actividad es una proyección calculada automáticamente por la frecuencia de repetición programada. Estará disponible para su gestión habitual a medida que llegue la fecha señalada." | No requiere escalamiento; es un comportamiento informativo previsto del sistema. |
| "No permite completar la tarea y muestra mensaje de permiso insuficiente" | El perfil o rol del usuario en la finca no tiene habilitado el permiso para completar eventos y tareas | "Su cuenta en la finca no tiene asignado el permiso para completar o modificar el estado de tareas. Solicite al propietario o administrador de la finca que actualice sus permisos de usuario." | Si el usuario es el propietario registrado de la finca y experimenta este bloqueo, transferir a soporte técnico. |

### Directivas de Seguridad y Guardrails
- Las notas de observación de las tareas y eventos son registros operacionales compartidos con el equipo de la finca; no ingrese información financiera confidencial, contraseñas ni datos sensibles en este campo.
- Los cambios de estado realizados sin conexión a internet son definitivos en el dispositivo local y prevalecerán al sincronizar con el servidor; asegúrese de registrar las notas de campo con precisión antes de confirmar.
- El personal de soporte nunca solicitará al usuario eliminar tareas o eventos de la base de datos de forma manual mediante desinstalación de la app sin previo respaldo de sincronización.
