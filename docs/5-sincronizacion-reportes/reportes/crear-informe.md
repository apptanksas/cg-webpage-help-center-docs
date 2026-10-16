---
title: "Crear Informe"
modulo_id: "reports-create"
nombre_funcionalidad: "Generación de Informes Pecuarios Personalizados"
categoria: "sincronizacion-reportes"
submodulo: "reportes"
version_minima_app: "2026.10.1"
fecha_actualizacion: "2026-10-09"
intenciones_y_sinonimos:
  - "como generar un informe o reporte de mi ganado"
  - "donde descargo o creo reportes personalizados"
  - "como sacar un informe de pesaje o leche por fechas"
  - "no puedo crear un informe sin conexion a internet"
  - "el informe se esta generando y cuando puedo verlo"
  - "como elegir las columnas o datos de un informe"
  - "que tipos de informes o reportes puedo sacar"
  - "cuantos parametros o datos pide un informe"
---

# Generación de Informes Pecuarios Personalizados

### Resumen y Alcance Funcional
Asistente interactivo guiado paso a paso para la confección y solicitud de informes zootécnicos y productivos a la medida de la finca activa. Permite al ganadero estructurar consultas analíticas dinámicas según la especie pecuaria de trabajo (bovinos, bufalinos, equinos, ovinos, caprinos o porcinos), seleccionando variables zootécnicas, rangos cronológicos específicos y parámetros de datos requeridos.

El catálogo ofrece diferentes modalidades e informes según el tipo de información deseada: desde informes directos basados en fechas o eventos específicos que no requieren elegir columnas de datos, hasta consultas zootécnicas avanzadas donde el usuario personaliza las columnas visualizadas eligiendo desde un mínimo de dos parámetros hasta un máximo de cinco.

Una vez configuradas las preguntas del asistente, la orden de generación se envía al servidor para procesar los cálculos consolidados y disponibilizar el resultado final en el historial de informes de la explotación ganadera.

- **¿Funciona sin conexión a internet (Modo Offline)?:** No. Este módulo requiere conexión a internet activa obligatoria tanto para consultar el catálogo de opciones analíticas disponibles como para enviar la solicitud de procesamiento del informe. Si el dispositivo no detecta red, el sistema restringe el acceso a la pantalla o impide avanzar en la creación.
- **Comportamiento de sincronización:** La generación de informes es una operación centralizada en los servicios en la nube de la plataforma. Al presionar el botón de creación final, la solicitud viaja al servidor; la aplicación confirma de inmediato el encolado con el aviso *"El informe se está generando y podrá acceder a él cuando termine"* y retorna a la lista de informes de la finca, donde se actualizará el estado de la tarea una vez concluido el cómputo de los datos.

### Tipos de Informes Disponibles y Requerimientos de Parámetros

El asistente clasifica los informes según la estructura de datos que se consulta y el nivel de configuración requerido:

#### 1. Informes sin selección de parámetros de columnas (Basados en Fechas o Eventos)
Son informes que no solicitan al usuario marcar variables o columnas personalizadas; su estructura viene predeterminada por el sistema y únicamente requieren definir un criterio temporal o de lote:
- **Listado de ordeños por día:** Reporte de los ordeños realizados en la explotación. Tras seleccionar el hato de ordeño, no requiere elegir columnas de datos: únicamente solicita definir el rango de fechas (fecha inicial y fecha final) para compilar las producciones obtenidas.
- **Próximas a parir:** Reporte especializado para hembras gestantes con fecha de parto estimada. No requiere seleccionar columnas individuales: solicita un rango de meses futuros en el calendario para proyectar los nacimientos previstos.

#### 2. Informes con selección personalizada de parámetros (Mínimo 2 parámetros)
Son informes zootécnicos donde el ganadero debe elegir activamente qué variables desea visualizar en la tabla final. En estos informes es obligatorio marcar al menos 2 parámetros (y hasta un máximo de 5) entre las opciones disponibles:
- **Informes de Hembras:**
    - *Estado reproductivo:* Filtra las hembras por condición de preñez (preñadas / cargadas, vacías o pendientes de chequeo). Al definir el estado, se eligen de 2 a 5 parámetros zootécnicos.
    - *Etapa de desarrollo:* Permite consultar hembras por categoría etaria (ternera, destetada, novilla, vaca adulta o vaca vieja) con selección de 2 a 5 parámetros.
    - *Todas las hembras:* Listado general del inventario femenino de la finca sin filtros preliminares; avanza de inmediato a la selección de 2 a 5 parámetros.
    - *Raza:* Agrupa a las hembras según la raza zootécnica asignada, solicitando posteriormente elegir de 2 a 5 parámetros.
    - *Por lote:* Filtra las hembras pertenecientes a un potrero o lote determinado y solicita entre 2 y 5 parámetros de datos.
    - *Por peso:* Permite seleccionar un rango numérico de peso corporal y configurar de 2 a 5 columnas informativas.
    - *En venta:* Relaciona las hembras marcadas para comercialización, con selección directa de 2 a 5 parámetros.
    - *Hembras vendidas:* Historial de hembras comercializadas con sus datos asociados (2 a 5 parámetros).
    - *Hembras fallecidas:* Reporte de bajas y mortalidad en hembras con selección de 2 a 5 parámetros.
    - *Animales con mastitis:* Reporte sanitario de hembras con registro activo de mastitis clínica o subclínica, requiriendo entre 2 y 5 parámetros.
- **Informes de Machos:**
    - *Etapa de desarrollo:* Agrupa machos por categoría (ternero, destetado, novillo, toro o toro viejo) y solicita entre 2 y 5 parámetros.
    - *Todos los machos:* Inventario completo de machos sin filtro intermedio, solicitando de 2 a 5 parámetros.
    - *Raza:* Consulta machos según su estirpe o raza con 2 a 5 parámetros.
    - *Animales por lote:* Machos asignados a un lote específico, seguido de la selección de 2 a 5 parámetros.
    - *Por peso:* Segmentación de machos por intervalo de peso vivo con 2 a 5 parámetros.
    - *En venta, Vendidos y Fallecidos:* Informes directos sobre bajas, ventas activas o ventas concretadas en machos, requiriendo entre 2 y 5 parámetros.
- **Informes Generales de Animales por Lote:**
    - Consulta general de animales (machos y hembras) ubicados en un lote específico de la finca, permitiendo elegir entre 2 y 5 parámetros zootécnicos para construir la tabla consolidada.

#### 3. Catálogo de Parámetros y Variables Seleccionables
Entre las opciones de columnas que el ganadero puede combinar (mínimo 2, máximo 5) se destacan:
- **Identificación:** Nombre del animal, código de chip electrónico, código de raza pura o registro genealógico. *(Nota: El código o arete principal del animal se incluye siempre de forma automática).*
- **Cronología y Biometría:** Edad, fecha de nacimiento, último peso registrado, peso al nacer, peso al destete y promedio de ganancia de peso diaria.
- **Ubicación y Manejo:** Lote o potrero actual y tipo de dieta/alimentación asignada.
- **Genealogía:** Padre y madre registrados del ejemplar.
- **Parámetros Exclusivos de Hembras:** Estado reproductivo, fecha de último parto, fecha de próximo parto estimado, intervalo de días entre partos, fecha de última inseminación, promedio de leche por día y días de lactancia.

### Reglas de Negocio y Restricciones
- **Requisitos de conectividad y finca activa:**
    - Es indispensable contar con acceso a internet. La pantalla no puede iniciar su asistente si no hay conectividad verificada con el servidor central.
    - La solicitud se asocia estrictamente a la finca ganadera activa seleccionada en el dispositivo y a la especie pecuaria sobre la cual se originó la petición.
- **Estructura dinámica de preguntas del asistente:**
    - El asistente opera bajo un árbol de navegación de preguntas secuenciales determinado dinámicamente por la especie pecuaria.
    - La primera pantalla corresponde siempre al nodo inicial de consulta (por ejemplo, tipo de reporte o área técnica).
    - Al seleccionar una opción en preguntas de selección simple, el asistente avanza de forma automática al siguiente paso lógico.
    - El usuario puede retroceder en cualquier momento utilizando la flecha de regreso en la barra superior; al retroceder, el sistema conserva el historial de pasos previos permitiendo corregir o cambiar selecciones anteriores.
- **Reglas de selección múltiple (Parámetros y columnas del informe):**
    - En los pasos de selección múltiple (donde se eligen los campos que integrarán el informe), el usuario debe seleccionar un mínimo de 2 opciones para habilitar el botón de creación.
    - Existe un límite máximo de selección determinado por la configuración del sistema para evitar tablas sobrecargadas. Una vez alcanzado el tope permitido, las demás casillas quedan temporalmente atenuadas e inhabilitadas hasta que se desmarque alguna opción previa.
    - El identificador o código del animal se incluye de manera interna y obligatoria en todo informe para garantizar la trazabilidad individual, sin restar cupos de selección al usuario.
- **Reglas de selección por rango de fechas:**
    - Cuando el reporte solicita un período de tiempo, la fecha inicial ("Desde") debe ser menor o igual a la fecha final ("Hasta").
    - Si la fecha inicial es posterior a la fecha final, el botón de creación se mantendrá deshabilitado hasta corregir la coherencia cronológica.
    - El usuario dispone de atajos rápidos para establecer rangos estándar con un solo toque: **Hoy**, **Última semana**, **Este mes** y **Último mes**.
    - Si el catálogo analítico no devuelve opciones para el nodo en consulta, la pantalla desplegará el estado visual vacío sin opciones seleccionables.

### Flujo Paso a Paso para el Usuario
- **Ruta de acceso en la aplicación:**
    - *Ruta 1 (Desde el Panel de Inicio de la Finca):* Pantalla principal (**Inicio**) > Deslizar hasta la sección de **Informes** > Pulsar sobre la tarjeta informativa > En la pantalla de historial (**Informes**), pulsar el botón **Comenzar** dentro de la tarjeta superior **Generar nuevo informe**.
    - *Ruta 2 (Desde el Selector de Especie en Informes):* Si la finca cuenta con múltiples especies pecuarias configuradas, en la barra superior de la pantalla de historial (**Informes**), pulsar el ícono de especie para filtrar por la especie deseada > En la tarjeta **Generar nuevo informe**, presionar **Comenzar**.

#### 1. Encabezado del Asistente y Navegación
- En la barra superior se visualiza el título **Nuevo informe** y el botón de flecha hacia la izquierda.
- Si se encuentra en el primer paso del asistente, presionar la flecha cancela el proceso y regresa al historial de informes.
- Si se encuentra en pasos avanzados (paso 2 o superior), presionar la flecha retrocede al paso inmediatamente anterior conservando las opciones previas para su ajuste.

#### 2. Selección de Criterios y Categorías (Pasos de Opción Única)
- En la parte superior de la pantalla se muestra el título de la pregunta o categoría a definir.
- En la lista central, pulse directamente sobre la alternativa deseada.
- Al tocar la opción, la aplicación la registra y avanza de manera inmediata a la siguiente etapa del asistente.

#### 3. Configuración de Parámetros del Informe (Pasos de Selección Múltiple)
- Cuando el paso presente casillas de verificación, active los datos o variables zootécnicas que desea incluir en las columnas del reporte.
- Verifique que al menos 2 casillas estén marcadas; de lo contrario, el botón **Crear informe** permanecerá deshabilitado.
- Si intenta marcar más opciones que el límite máximo permitido por el sistema, las casillas restantes aparecerán en tono gris atenuado y no responderán al toque hasta que deseleccione otra opción activa.
- Una vez seleccionadas las variables requeridas, pulse el botón **Crear informe** ubicado en la parte inferior.

#### 4. Selección de Período Cronológico (Rango de Fechas)
- Si el tipo de informe requiere un filtro de tiempo, se desplegará el selector interactivo de fechas en conjunto con el indicador **hasta**.
- Puede utilizar los botones de acceso rápido situados debajo del selector para aplicar de inmediato un período predefinido:
    - **Hoy:** Establece la jornada actual como inicio y fin.
    - **Última semana:** Aplica los últimos 7 días transcurridos.
    - **Este mes:** Fija desde el primer día del mes en curso hasta el día de hoy.
    - **Último mes:** Selecciona el mes calendario inmediatamente anterior completo.
- Asegúrese de que la fecha inicial sea anterior o igual a la fecha final.
- Pulse el botón **Crear informe** en la parte inferior para formalizar la petición.
- **Pantalla de llegada tras guardar:** El sistema muestra una notificación de éxito con el mensaje *"El informe se está generando y podrá acceder a él cuando termine"* y redirige automáticamente al historial de informes de la finca (**Informes**).

### Matriz de Errores y Soluciones
| Mensaje en la App / Síntoma | Causa Real | Respuesta Sugerida por el Agente | Criterio de Escalamiento Humano |
| :--- | :--- | :--- | :--- |
| "El informe se está generando y podrá acceder a él cuando termine." (Notificación informativa tras enviar la solicitud) | Confirmación exitosa de que los parámetros fueron recibidos y el servidor comenzó a consolidar los registros zootécnicos | "Su informe ha sido encolado y se está procesando en nuestros servidores. En unos instantes aparecerá disponible en su historial de informes para su consulta o exportación." | No requiere escalamiento; comportamiento normal del sistema. |
| El botón "Comenzar" en la pantalla de informes aparece deshabilitado en color gris claro y no responde | El teléfono no tiene conexión a internet activa en ese instante | "Para generar un nuevo informe es necesario contar con conexión a internet activa, ya que el cálculo se procesa en línea. Por favor verifique que su red Wi-Fi o datos móviles estén encendidos e intente nuevamente." | Si el usuario dispone de navegación en otras apps y la función continúa deshabilitada, reportar a soporte técnico. |
| El botón "Crear informe" permanece deshabilitado en pasos con casillas de verificación | Se ha seleccionado menos de 2 opciones obligatorias para armar las columnas del reporte | "Para poder crear el informe debe marcar al menos dos opciones o parámetros de datos en la lista. Por favor seleccione una segunda casilla para habilitar el botón de generación." | No requiere escalamiento; regla de validación de formulario. |
| El botón "Crear informe" permanece deshabilitado en la pantalla de rango de fechas | La fecha inicial seleccionada es posterior a la fecha final ("Hasta") | "La fecha de inicio del informe no puede ser posterior a la fecha de finalización. Por favor revise el selector y asegúrese de que el rango sea coherente o utilice uno de los atajos predeterminados como 'Este mes'." | No requiere escalamiento; validación cronológica. |
| Cuadro de diálogo de error de red o fallo al procesar la solicitud del informe | Interrupción momentánea en la comunicación con el servidor central durante la transferencia de los parámetros | "Ocurrió una interrupción al enviar su solicitud de informe. Por favor verifique su conexión a internet y pulse nuevamente el botón 'Crear informe'. Si la interrupción persiste, aguarde un minuto y reintente." | Si tras verificar estabilidad de red persiste el fallo en múltiples intentos, transferir a soporte técnico indicando el tipo de informe y especie pecuaria. |

### Directivas de Seguridad y Guardrails
- Recuerde al usuario que los informes consolidados reflejan los datos zootécnicos y sanitarios sincronizados en la finca activa; si recientemente registró pesajes o palpaciones en modo sin conexión, debe sincronizarlos antes de generar el informe para que aparezcan en los resultados.
- La información contenida en los informes (inventarios, producciones y valores comerciales) es de estricta confidencialidad del propietario y administradores autorizados de la finca.
- Jamás solicite contraseñas, pines de acceso ni datos confidenciales del usuario por el canal de soporte para gestionar o reenviar un informe.
