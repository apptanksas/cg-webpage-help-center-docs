---
title: "Calendario de Eventos y Tareas"
modulo_id: "eventask-calendario"
nombre_funcionalidad: "Calendario Mensual de Eventos y Tareas Ganaderas"
categoria: "sincronizacion-reportes"
submodulo: "eventos-tareas"
version_minima_app: "2026.10.1"
fecha_actualizacion: "2026-10-09"
intenciones_y_sinonimos:
  - "como ver el calendario de actividades de la finca"
  - "donde consultar los eventos y tareas del mes"
  - "como saltar a una fecha especifica en el calendario"
  - "por que algunas tareas del calendario se ven mas claras o atenuadas"
  - "que significa la linea roja en la lista de actividades"
  - "como crear un nuevo evento desde el calendario"
---

# Calendario Mensual de Eventos y Tareas Ganaderas

### Resumen y Alcance Funcional
Pantalla principal de planificación y seguimiento temporal que consolida en una sola vista cronológica todos los **Eventos informativos** y **Tareas de manejo** programados en la finca ganadera. Permite a administradores y colaboradores visualizar las labores diarias y mensuales, consultar el volumen de actividades por día en un calendario desplegable interactivo, navegar de forma rápida entre meses y acceder al detalle operativo de cualquier labor.

El calendario integra un cálculo automático de proyecciones futuras para aquellas actividades configuradas con frecuencia de repetición (diaria, semanal, mensual o anual), garantizando que el usuario tenga visibilidad de sus próximos compromisos sanitarios, reproductivos o de manejo antes de que se creen de forma individual en la base de datos.

- **¿Funciona sin conexión a internet (Modo Offline)?:** Sí.
- **Comportamiento de sincronización:** Todas las actividades registradas se consultan directamente desde el almacenamiento local del teléfono móvil. Las proyecciones recurrentes se computan en tiempo real en la memoria del dispositivo sin requerir internet. Al registrar nuevos eventos o sincronizar con la nube, las actividades creadas o actualizadas por otros miembros de la finca se incorporan de forma automática a la vista del calendario al reconectar.

### Reglas de Negocio y Restricciones
- **Permisos requeridos para acceder:** El ingreso a la pantalla del calendario de eventos y tareas exige que el colaborador cuente con el permiso de gestión y cumplimiento de tareas en la finca ganadera. Si el usuario no tiene asignado este permiso, la opción no estará visible en el menú lateral ni en el panel de inicio.
- **Diferenciación visual y estructural de actividades en la lista:**
  - **Tareas:** Se presentan como tarjetas con fondo coloreado según su estado operativo: azul oscuro para **Pendiente**, naranja para **En progreso** y verde oscuro para **Completada**. Incluyen un ícono circular de verificación y, cuando la tarea ha sido completada, el título se muestra con formato tachado.
  - **Eventos:** Se presentan como tarjetas con bordes redondeados y fondo verde claro (o gris si corresponde a una proyección recurrente). Muestran el título en texto oscuro y no incluyen indicadores de estado ni formato tachado.
- **Agrupamiento cronológico de fechas en la lista (Columna Lateral):**
  - En la lista cronológica de actividades, las labores se organizan y agrupan por día.
  - **Presentación de la fecha:** La fecha (número del día y abreviatura del día de la semana) solo se muestra en la primera actividad registrada para ese día. Si para una misma fecha existen múltiples actividades programadas (por ejemplo, un evento y varias tareas, o múltiples tareas consecutivas), las labores siguientes pertenecientes al mismo día se alinean inmediatamente debajo sin repetir el bloque de fecha a la izquierda.
  - **Diferenciación aparente entre eventos y tareas:** Tanto eventos como tareas tienen fecha asignada; sin embargo, al estar agrupadas cronológicamente, si un evento aparece de primero en el día mostrará el número y día de la semana, mientras que las tareas que le siguen en esa misma fecha no repiten la etiqueta de fecha lateral, dando un aspecto limpio y continuo por jornada.
- **Indicadores visuales del día actual ("Hoy"):**
  - **En el calendario mensual superior:** El día actual se resalta por defecto con un círculo de color rojo. Cuando un día tiene eventos o tareas programadas en el mes, se dibuja una línea horizontal debajo del número de la fecha (la cual es proporcional al volumen de actividades del día). Si el día con actividades está seleccionado, muestra un borde exterior blanco.
  - **En la lista cronológica inferior:** Si una fecha coincide con el día de hoy, el número del día y las siglas del día de la semana se muestran resaltados en color rojo vivo (en los días normales se muestran en negro y gris). Además, la primera actividad del día de hoy se distingue con una línea horizontal divisoria de color rojo en la parte superior.
- **Identificación de animales asignados:** Si una tarea o evento está vinculado a un bovino específico de la finca, la tarjeta exhibe en su esquina superior derecha un ícono miniatura distintivo que representa la especie o tipo de animal.
- **Atenuación visual de actividades pasadas:** Las labores cuya fecha programada sea anterior al día de hoy se muestran con un 80% de opacidad (apariencia atenuada) y sin sombra o elevación sobre la superficie, indicando que corresponden al historial de días transcurridos.
- **Comportamiento de Proyecciones Futuras recurrentes:**
  - Las ocurrencias proyectadas automáticamente por repetición se visualizan con un 80% de opacidad para distinguirlas de las actividades creadas individualmente.
  - En el caso de los eventos informativos proyectados, el fondo de la tarjeta cambia a color gris en lugar del verde claro habitual.
- **Comportamiento interactivo del Calendario Desplegable:**
  - Al pulsar sobre cualquier día en la cuadrícula mensual del calendario, la lista inferior realiza un desplazamiento animado automático hasta ubicar las actividades de esa fecha en pantalla.
  - La tarjeta seleccionada se resalta temporalmente con un destello suave de color verde claro para confirmar visualmente la fecha elegida.
- **Acceso rápido a creación:** La pantalla dispone de un botón de acción flotante con ícono de calendario que permite iniciar de inmediato el registro de un nuevo evento en la finca.

### Flujo Paso a Paso para el Usuario
- **Ruta de acceso en la aplicación:**
  - *Ruta 1 (Desde el Menú Lateral):* Menú lateral principal > Opción **Eventos y Tareas**.
  - *Ruta 2 (Desde el Panel Principal de la Finca):* Pantalla de inicio de la finca > Bloque superior de calendario interactivo de tareas > Seleccionar el día deseado en la barra horizontal.

1. Al acceder a la pantalla, la barra superior muestra el mes y año consultados (por ejemplo, *"Octubre - 2026"*).
2. Si la lista contiene actividades, la aplicación se desplaza automáticamente hasta posicionarse en las labores correspondientes al día de hoy (o a la fecha solicitada).

#### 1. Uso del Calendario Desplegable Mensual
En la parte superior de la pantalla se ubica el calendario interactivo:
- **Ocultar o mostrar el calendario:** Presione sobre la barra de título superior que indica el mes y el año. Al pulsarla, el calendario se despliega o se repliega con una animación vertical, permitiendo liberar espacio para visualizar más actividades en la lista.
- **Navegación entre meses:** Deslice el calendario horizontalmente hacia la izquierda o hacia la derecha para avanzar o retroceder de mes.
- **Indicador de carga de actividades:** Cada número de día en el calendario que tenga eventos o tareas programadas muestra debajo una barra blanca proporcional a la cantidad de actividades del día.
- **Selección de día:** Al tocar cualquier fecha del calendario, el número queda resaltado con un círculo de color rojo (y con borde blanco si tiene actividades asociadas). De forma automática, la lista inferior se desplaza hasta el primer compromiso de esa fecha y aplica un destello visual verde sobre la tarjeta.

#### 2. Consulta y Exploración de la Lista de Actividades
Debajo del calendario se despliega la lista cronológica organizada por días:
- **Columna de fecha (lado izquierdo):** Agrupa las actividades mostrando en texto grande el número del día y debajo las tres primeras letras del día de la semana (por ejemplo, *"09 VIE"*).
  - Si coincide con la fecha de hoy, tanto el número como las siglas del día de la semana se destacan en color rojo vivo.
  - Para evitar repeticiones visuales innecesarias, la fecha solo se imprime una vez al inicio del grupo de actividades de ese día. Si tras un evento o tarea existen más labores en esa misma jornada, se listan debajo compartiendo la misma fecha sin duplicar el texto a la izquierda.
- **Tarjeta de Tarea (lado derecho):**
  - Muestra el ícono de verificación, el título de la tarea y el color característico de su estado operativo actual.
  - Si la tarea fue completada, el texto del título se muestra tachado.
  - Si tiene un animal asociado, observe el ícono del ejemplar en la esquina superior derecha.
- **Tarjeta de Evento (lado derecho):**
  - Muestra el título del evento sobre una tarjeta de borde redondeado en color verde claro (o gris si es una proyección futura).
- **Apertura del detalle:** Toque sobre cualquier tarjeta (evento o tarea) para abrir la pantalla de **Detalle de Evento o Tarea**, donde podrá revisar la descripción completa, cambiar el estado de cumplimiento, editar la actividad o consultar notas de campo.

#### 3. Registro de un Nuevo Evento
- En la esquina inferior derecha de la pantalla se ubica un botón de acción flotante circular con el ícono de un calendario.
- Al pulsarlo, la aplicación abre directamente el formulario de creación de eventos para programar una nueva labor informativa o técnica en la finca.

- **Pantalla de llegada tras guardar o volver:** Al crear una nueva actividad o guardar cambios desde la pantalla de detalle, la aplicación regresa al calendario recargando de inmediato la lista de actividades del mes con los datos actualizados.

### Matriz de Errores y Soluciones
| Mensaje en la App / Síntoma | Causa Real | Respuesta Sugerida por el Agente | Criterio de Escalamiento Humano |
| :--- | :--- | :--- | :--- |
| "No hay eventos o tareas programadas" | No existen actividades registradas ni proyectadas en la finca para el mes que se está consultando | "En este mes no hay actividades programadas. Puede cambiar de mes deslizando el calendario superior o pulsar el botón circular con ícono de calendario en la parte inferior para programar un nuevo evento." | No requiere escalamiento; es el estado informativo normal ante ausencia de registros en el periodo. |
| "La opción Eventos y Tareas no aparece en el menú lateral ni en el panel de inicio" | La cuenta del usuario no cuenta con el permiso para completar y consultar tareas en la finca actual | "Su perfil en la finca actual no tiene habilitado el permiso de eventos y tareas. Solicite al propietario o administrador de la finca que actualice los permisos de su cuenta de usuario." | Si el usuario es el propietario registrado de la finca y no visualiza la sección, escalar a soporte técnico. |
| "Al tocar una fecha del calendario la lista no se mueve" | No hay ninguna actividad programada exactamente para el día seleccionado en el mes | "El día que seleccionó en el calendario no tiene eventos ni tareas programadas en la lista inferior. Los días con actividades muestran una pequeña barra blanca debajo del número en el calendario." | No requiere escalamiento; comportamiento previsto de la interfaz. |
| "Algunas actividades se muestran con colores apagados u opacos" | Las actividades corresponden a fechas ya pasadas o son proyecciones automáticas de repeticiones futuras | "Las actividades con apariencia atenuada corresponden a labores pasadas de días anteriores o a compromisos futuros calculados automáticamente por la repetición de una serie. Al ingresar a cualquiera de ellas podrá consultar sus detalles." | No requiere escalamiento; es una regla visual intencional del sistema. |
| "Círculo de espera en el centro de la pantalla sin mostrar actividades" | La aplicación está consultando y calculando las actividades y proyecciones del mes desde la base de datos local | "Espere unos instantes mientras el teléfono procesa y agrupa los compromisos del mes. Si el círculo de espera no desaparece tras varios segundos, cierre la aplicación por completo deslizando hacia arriba en su administrador de tareas y vuelva a ingresar." | Si tras reiniciar la aplicación el calendario queda bloqueado de forma recurrente, transferir a soporte técnico indicando modelo del teléfono y versión instalada. |

### Directivas de Seguridad y Guardrails
- Las actividades del calendario contienen información de manejo y programación interna de la finca; no solicite capturas de pantalla si estas contienen datos sensibles o notas privadas no relacionadas con la incidencia.
- El cálculo de proyecciones futuras se realiza de manera local en el teléfono y no modifica la base de datos hasta que se individualice o edite la actividad; el personal de soporte nunca debe indicar al usuario reinstalar la app sin antes verificar si tiene cambios pendientes de sincronizar.
- En caso de dudas sobre actividades no visibles de otros compañeros, recuerde al usuario verificar si su teléfono tiene conexión activa para recibir las últimas sincronizaciones de la finca.
