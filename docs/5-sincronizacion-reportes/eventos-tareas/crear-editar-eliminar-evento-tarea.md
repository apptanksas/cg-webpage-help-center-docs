---
title: "Crear, Editar o Eliminar Evento y Tarea"
modulo_id: "eventask-crear-editar-eliminar"
nombre_funcionalidad: "Creación, Modificación y Eliminación de Eventos y Tareas Ganaderas"
categoria: "sincronizacion-reportes"
submodulo: "eventos-tareas"
version_minima_app: "2026.10.1"
fecha_actualizacion: "2026-10-09"
intenciones_y_sinonimos:
  - "como programar una nueva tarea en la finca"
  - "como crear un evento de recordatorio"
  - "como configurar repeticiones en una tarea"
  - "como asignar un evento a un trabajador o a un animal"
  - "como eliminar una actividad o toda la serie repetitiva"
  - "como borrar o quitar un evento o tarea"
  - "por que no puedo cambiar el tipo de actividad al editar"
---

# Creación, Modificación y Eliminación de Eventos y Tareas Ganaderas

### Resumen y Alcance Funcional
Formulario integral para la planificación y programación de actividades ganaderas dentro de la finca. Permite a los administradores y operarios registrar **Eventos informativos** (recordatorios de fechas clave, vacunaciones generales, pesajes grupales, visitas técnicas) o **Tareas de manejo** (labores con ciclo de cumplimiento obligatorio en campo).

Desde este módulo es posible definir nombres, descripciones detalladas, programar fechas de ejecución hasta con diez años de proyección a futuro, configurar reglas de repetición periódica automática (diaria, semanal, mensual o anual con fecha límite opcional), restringir la visibilidad por perfiles de usuario y asignar la labor a un colaborador específico de la finca o vincularla a un animal individual de la vacada. En modo de edición, la pantalla permite actualizar los datos o suprimir la actividad de forma individual o eliminando toda la serie periódica vinculada.

- **¿Funciona sin conexión a internet (Modo Offline)?:** Sí.
- **Comportamiento de sincronización:** Las actividades y sus reglas de configuración se guardan de forma instantánea en la base de datos local del teléfono. Al recuperar conectividad a internet, los eventos y tareas creados se transmiten automáticamente a la nube y se distribuyen al resto de los integrantes de la finca que tengan permisos de consulta.

### Reglas de Negocio y Restricciones
- **Permisos requeridos:**
    - Para registrar nuevas actividades se requiere el permiso de creación de eventos y tareas en la finca.
    - Para modificar una actividad existente se requiere el permiso de actualización de eventos y tareas.
    - Para suprimir una actividad o serie se requiere el permiso de eliminación de eventos y tareas.
    - Si el usuario carece del permiso correspondiente, el sistema no permitirá guardar, actualizar ni eliminar la información.
- **Diferenciación entre Evento y Tarea al crear:**
    - **Evento:** Suceso o hito informativo de fecha fija. No exige marcarse como completado en el sistema y no posee estados operativos.
    - **Tarea:** Compromiso de campo que debe ejecutarse y marcarse formalmente como completada en la aplicación una vez concluida la labor.
    - El interruptor para alternar entre evento y tarea **solo está disponible durante la creación**. Una vez que la actividad ha sido guardada en la base de datos, su naturaleza (evento o tarea) queda bloqueada de forma permanente y no puede ser modificada en el formulario de edición.
- **Restricciones de fecha de ejecución:**
    - La fecha programada no puede ser anterior al día de hoy; solo se admiten fechas desde el día actual hasta un máximo de diez años en el futuro.
- **Validación del nombre de la actividad:**
    - El campo de nombre es de carácter obligatorio. No es posible guardar el formulario sin asignar un título a la labor.
- **Descripción de la actividad:**
    - El campo de descripción es opcional y admite texto multilínea para detallar instrucciones específicas, productos requeridos o dosis de campo.
- **Reglas de periodicidad y repetición:**
    - La actividad puede configurarse sin repetición o con frecuencia periódica según la fecha base programada (repetición diaria, semanal, mensual o anual).
    - Al activar una frecuencia de repetición, se habilita la opción de definir una fecha límite de finalización de la serie (con un horizonte de hasta diez años). Si se deja vacía la fecha de culminación, la periodicidad se proyectará indefinidamente según el calendario.
- **Filtro de visibilidad por perfiles:**
    - Permite limitar qué tipos de colaboradores pueden consultar la actividad en su calendario (por ejemplo, restringir para administradores, veterinarios o vaqueros). Por defecto se encuentra seleccionada la opción para todos los miembros de la finca. Los perfiles con rol de visitante quedan automáticamente excluidos de la lista de asignación.
- **Asignación personalizada y a animales:**
    - **Asignación a colaborador:** Permite delegar la actividad a un miembro registrado de la finca o autoasignársela directamente.
    - **Asignación a animal:** Permite vincular la actividad a un ejemplar específico de la finca ganadera. El selector filtra y presenta únicamente animales vivos que se encuentren registrados físicamente en la finca en ese momento. Al asignar un ejemplar, su cinta identificadora se exhibe en la parte superior del formulario.
- **Reglas de eliminación de actividades periódicas:**
    - Si una actividad no tiene repeticiones (es única), se elimina directamente tras presionar el botón de supresión.
    - Si la actividad forma parte de una serie recurrente con más de una ocurrencia registrada, el sistema despliega un diálogo de confirmación que permite al usuario elegir entre:
      1. **Solo este evento / Solo esta tarea:** Suprime únicamente la fecha seleccionada, manteniendo intactas las demás actividades de la serie.
      2. **Todos los eventos de la serie / Todas las tareas de la serie:** Elimina de manera definitiva la actividad actual y todas las demás ocurrencias vinculadas a la misma configuración.

### Flujo Paso a Paso para el Usuario
- **Ruta de acceso en la aplicación:**
  - *Ruta para Crear (Desde el Calendario de Actividades):* Menú lateral principal > **Eventos y Tareas** > Pulsar el botón flotante circular con ícono de calendario en la esquina inferior derecha.
  - *Ruta para Crear (Desde el Panel Principal de la Finca):* Pantalla de inicio de la finca > Bloque superior de calendario interactivo de tareas > Pulsar sobre el día deseado > Pulsar el botón flotante circular con ícono de calendario en la esquina inferior derecha.
  - *Ruta para Crear (Desde el Menú Rápido Central):* Barra de navegación inferior de inicio > Botón flotante central con ícono de suma (**+**) > Opción **Crear Evento/Tarea**.
  - *Ruta para Modificar o Eliminar (Desde el Calendario o Inicio):* Menú lateral principal > **Eventos y Tareas** (o desde el bloque de calendario en Inicio) > Pulsar sobre la actividad para abrir su pantalla de detalle > Tocar el botón de edición con ícono de lápiz en la esquina superior derecha.
  - *Ruta para Modificar o Eliminar (Desde la Ficha del Animal):* Menú inferior de la pantalla principal > **Animales** > Seleccionar ejemplar > Tarjeta de **Datos veterinarios** > Opción eventos y tareas > Pulsar sobre la actividad deseada > En la pantalla de detalle tocar el botón de edición con ícono de lápiz en la esquina superior derecha.

#### 1. Configuración del Tipo de Actividad (Solo al Crear)
- Al ingresar en modo de creación, la pantalla presenta en la parte superior el interruptor **Crear como tarea**.
- Por defecto, el formulario inicia configurado como **Evento**.
- Si desea que la labor requiera cumplimiento obligatorio en campo y seguimiento de estados (pendiente, en progreso, completada), active el interruptor. El texto informativo confirmará: *"Una tarea se debe marcar como completada"*.

#### 2. Definición de Fechas y Datos Básicos
- **Fecha:** Pulse sobre el selector de fecha para abrir el calendario y elegir el día en que iniciará la labor. Por defecto viene preseleccionado el día de hoy.
- **Nombre:** Escriba el título representativo de la actividad (por ejemplo, *"Vacunación contra fiebre aftosa"* o *"Revisión de cerca en potrero 3"*). Este dato es obligatorio.
- **Descripción:** Escriba de forma voluntaria detalles adicionales, observaciones o instrucciones para el personal de campo.
- **Visibilidad:** Si desea que la actividad solo sea visible para ciertos roles de trabajo, despliegue el menú y elija el perfil deseado, o mantenga la opción para que todos los usuarios de la finca puedan verla.

#### 3. Configuración de Repetición (Frecuencia)
- En el bloque de frecuencia, toque la opción **Repetir** para desplegar el menú inferior de periodicidades disponibles calculadas para esa fecha (sin repetición, cada día, cada semana, cada mes o cada año).
- Si selecciona una periodicidad distinta a ninguna, se desplegará el campo **Repetir hasta**:
    - Pulse el selector de fecha si desea definir un día exacto de culminación de la serie.
    - Deje el campo vacío si desea que la actividad se repita de manera continua sin límite de tiempo.

#### 4. Designación a Usuarios y Animales
- **Asignar a un usuario específico:** Despliegue el listado para seleccionar al miembro de la finca que se hará responsable de la labor. Si desea asignársela a sí mismo, elija la opción correspondiente a su nombre de cuenta. Si no desea asignarla a nadie en particular, conserve la opción en blanco.
- **Asignar a un animal:** Toque el selector de animal para buscar por número de arete, chapeta, nombre o código electrónico al ejemplar de la finca vinculado a la actividad. Al seleccionarlo, sus datos distintivos aparecerán en la cinta superior de la pantalla.

#### 5. Guardado, Actualización o Eliminación
- **Crear actividad:** En un registro nuevo, presione el botón **Crear** al final de la pantalla. La aplicación validará que el nombre esté completo, almacenará la actividad en el teléfono y regresará automáticamente al calendario o pantalla previa mostrando un mensaje de confirmación (*"El evento ha sido creado exitosamente"* o *"La tarea ha sido creada exitosamente"*).
- **Actualizar actividad:** En modo edición, tras modificar los campos deseados, presione el botón de guardado. Los cambios se actualizarán de inmediato mostrando el aviso de confirmación.
- **Eliminar actividad (Paso a paso para suprimir un evento o tarea):**
    1. Localice la actividad en el calendario o panel de inicio y púlsela para abrir su pantalla de **Detalle**.
     2. En la barra superior del detalle, presione el botón de edición (ícono de lápiz) para ingresar a este formulario en modo de edición.
     3. Deslícese hasta el final del formulario y presione el botón rojo **Eliminar**.
     4. Si la actividad es única (sin repeticiones), se suprimirá de inmediato.
     5. Si la actividad forma parte de una serie recurrente con múltiples fechas, el sistema desplegará una ventana de confirmación:
        - Presione **Solo este evento** / **Solo esta tarea** para borrar únicamente la fecha seleccionada.
        - Presione **Todos los eventos de la serie** / **Todas las tareas de la serie** para eliminar toda la secuencia programada.
        - Presione **Cancelar** si prefiere conservar la actividad sin cambios.

- **Pantalla de llegada tras guardar o eliminar:** La aplicación cierra el formulario y redirige al usuario a la pantalla anterior (habitualmente el calendario mensual o el panel de inicio de la finca), actualizando al instante el listado de actividades programadas.

### Matriz de Errores y Soluciones
| Mensaje en la App / Síntoma | Causa Real | Respuesta Sugerida por el Agente | Criterio de Escalamiento Humano |
| :--- | :--- | :--- | :--- |
| "El campo Nombre no puede estar vacío" / El botón no avanza | No se ingresó ningún texto en el campo obligatorio de nombre de la actividad | "Por favor ingrese un nombre o título para la actividad antes de guardar. Este dato es obligatorio para poder identificar la labor en el calendario." | No requiere escalamiento; validación visual directa de formulario. |
| "No tiene permisos para crear o modificar eventos y tareas" | La cuenta del usuario en la finca actual no tiene habilitados los permisos de administración de actividades | "Su cuenta de colaborador en la finca actual no cuenta con permisos para crear, editar o eliminar eventos y tareas. Solicite al propietario o administrador de la finca que actualice sus permisos de acceso." | Si el usuario es el propietario registrado de la finca y se le niega el permiso, transferir a soporte técnico. |
| "No es posible cambiar entre Evento y Tarea al editar" | La actividad ya fue guardada previamente y el sistema bloquea el cambio de tipo para preservar la integridad de los datos | "Una vez que una actividad ha sido creada como evento o como tarea, su tipo no puede ser modificado. Si necesita cambiar su naturaleza, le sugerimos eliminar la actividad actual y crear una nueva seleccionando el tipo correcto." | No requiere escalamiento; regla de negocio intencional del sistema. |
| "El animal no aparece en el listado para asignar" | El ejemplar buscado se encuentra marcado como fallecido, vendido o asignado a otra finca en el sistema | "El buscador solo muestra animales vivos registrados en la finca actual. Verifique que el ejemplar se encuentre activo en su inventario general de animales." | Si el animal está activo en el inventario de la finca pero no aparece en el selector, escalar a soporte técnico. |
| "Ocurrió un error al guardar la actividad" | Fallo temporal al escribir los datos en el almacenamiento local del dispositivo | "Ocurrió un inconveniente al guardar la información en su teléfono. Verifique que cuente con espacio disponible en su dispositivo, cierre la aplicación por completo y vuelva a intentarlo." | Si el fallo persiste de forma continua al intentar guardar, escalar a soporte técnico indicando modelo del teléfono y versión instalada. |

### Directivas de Seguridad y Guardrails
- Al configurar actividades y descripciones, recuerde al usuario no ingresar datos sensibles, contraseñas ni información financiera en los campos de notas abiertas.
- Advierta siempre las consecuencias de la opción de supresión: elegir eliminar todas las actividades de una serie borrará permanentemente las proyecciones y ocurrencias asociadas a esa configuración en la finca.
- Si un usuario reporta que no visualiza actividades creadas por otros colaboradores, asegúrese de verificar que el teléfono cuente con conexión a internet para sincronizar las novedades de la finca antes de considerar un error de sistema.
