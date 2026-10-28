---
title: "Crear Informe"
modulo_id: "reports-create"
nombre_funcionalidad: "Generación de Informes Pecuarios Personalizados"
tipo_documento: "guia-app"
categoria: "sincronizacion-reportes"
submodulo: "reportes"
especies_aplicables: ["todas"]
version_minima_app: "2025.07.17"
confianza_reglas: "verificada-con-tests"
fecha_actualizacion: "2026-10-19"
intenciones_y_sinonimos:
  - "como generar un informe o reporte de mi ganado"
  - "donde descargo o creo reportes personalizados para mis animales"
  - "como sacar un informe de pesaje o leche por fechas"
  - "no puedo crear un informe sin conexion a internet"
  - "el informe se esta generando y cuando puedo verlo"
  - "por que no se activa el boton para crear el informe"
---

# Generación de Informes Pecuarios Personalizados

### Resumen y Alcance Funcional
Asistente interactivo guiado paso a paso para la configuración y solicitud de informes zootécnicos y productivos a la medida de la finca ganadera activa. Permite al productor estructurar consultas analíticas dinámicas según la especie pecuaria de trabajo (bovinos, bufalinos, equinos, ovinos, caprinos o porcinos), seleccionando variables zootécnicas, rangos cronológicos específicos y parámetros de datos requeridos.

El catálogo ofrece diferentes modalidades de informes según el tipo de información deseada: desde informes directos basados en fechas o eventos específicos que no requieren elegir columnas de datos, hasta consultas zootécnicas avanzadas donde el usuario personaliza las columnas visualizadas eligiendo desde un mínimo de dos parámetros hasta un máximo de cinco.

Una vez completadas las preguntas del asistente, la orden de generación se envía al servidor para procesar los cálculos consolidados y disponibilizar el resultado final en el historial de informes de la explotación ganadera.

- **Especies a las que aplica:** Aplica para todas las especies pecuarias configuradas en la finca (bovinos, bufalinos, equinos, ovinos, caprinos y porcinos). El árbol de preguntas y opciones se adapta dinámicamente a la especie seleccionada (por ejemplo, las opciones de leche y ordeño son exclusivas para especies con aptitud lechera: bovinos, caprinos y bufalinos).
- **¿Funciona sin conexión a internet (Modo Offline)?:** No. Este módulo requiere conexión a internet activa obligatoria tanto para consultar el catálogo de opciones analíticas disponibles como para enviar la solicitud de procesamiento del informe. Si el dispositivo no detecta red, el sistema restringe el acceso a la pantalla o despliega un aviso de bloqueo por requerimiento de conectividad.
- **Comportamiento de sincronización:** La generación de informes es una operación centralizada en los servicios en la nube de la plataforma. Al presionar el botón de creación final, la solicitud viaja al servidor; la aplicación confirma de inmediato el encolado con el aviso "El informe se está generando y podrá acceder a él cuando termine." y retorna a la lista de informes de la finca, donde se actualizará el estado de la tarea una vez concluido el cómputo de los datos.

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
    - *Etapa de desarrollo:* Permite consultar hembras por categoría etaria (ternera, destetada, novilla, vaca adulta o vaca vieja en bovinos; adaptado a cada especie) con selección de 2 a 5 parámetros.
    - *Todas las hembras:* Listado general del inventario femenino de la finca sin filtros preliminares; avanza de inmediato a la selección de 2 a 5 parámetros.
    - *Raza:* Agrupa a las hembras según la raza zootécnica asignada, solicitando posteriormente elegir de 2 a 5 parámetros.
    - *Por lote:* Filtra las hembras pertenecientes a un potrero o lote determinado y solicita entre 2 y 5 parámetros de datos.
    - *Por peso:* Permite seleccionar un rango numérico de peso corporal y configurar de 2 a 5 columnas informativas.
    - *En venta:* Relaciona las hembras marcadas para comercialización, con selección directa de 2 a 5 parámetros.
    - *Hembras vendidas:* Historial de hembras comercializadas con sus datos asociados (2 a 5 parámetros).
    - *Hembras fallecidas:* Reporte de bajas y mortalidad en hembras con selección de 2 a 5 parámetros.
    - *Animales con mastitis:* Reporte sanitario de hembras con registro activo de mastitis clínica o subclínica (especies lecheras), requiriendo entre 2 y 5 parámetros.
- **Informes de Machos:**
    - *Etapa de desarrollo:* Agrupa machos por categoría (ternero, destetado, novillo, toro o toro viejo en bovinos; adaptado a cada especie) y solicita entre 2 y 5 parámetros.
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
- **Parámetros Exclusivos de Hembras:** Estado reproductivo, fecha de último parto, fecha de próximo parto estimado, intervalo de días entre partos, fecha de última inseminación, promedio de leche por día y días de lactancia (en especies lecheras).

### Reglas de Negocio y Restricciones
- **Requisitos de conectividad y finca activa:**
    - Es indispensable contar con acceso a internet. La pantalla no puede iniciar su asistente si no hay conectividad verificada con el servidor central, ya que opera bajo control estricto de requerimiento de red.
    - Si el dispositivo pierde la señal de internet durante el uso de la pantalla, el sistema activa un bloqueo de seguridad con el mensaje "Esta funcionalidad requiere una conexión activa a internet para poder funcionar correctamente. Por favor, verifica tu conexión e intenta de nuevo."
    - La solicitud se asocia estrictamente a la finca ganadera activa seleccionada en el dispositivo y a la especie pecuaria sobre la cual se originó la petición.
- **Estructura dinámica de preguntas del asistente:**
    - El asistente opera bajo un árbol de navegación de preguntas secuenciales determinado dinámicamente por la especie pecuaria y provisto por el servidor.
    - La primera pantalla corresponde siempre al nodo inicial de consulta (por ejemplo, tipo de reporte o área técnica).
    - Al seleccionar una opción en preguntas de selección simple, el asistente registra la opción y avanza de forma automática al siguiente paso lógico.
    - Si una categoría o criterio de consulta no devuelve opciones disponibles, la pantalla despliega el estado informativo con el texto "No hay nada para mostrar".
    - El usuario puede retroceder en cualquier momento utilizando la flecha de regreso en la barra superior; al retroceder desde un paso avanzado (paso 2 o superior), el sistema desapila el último nodo y conserva las selecciones previas permitiendo corregir o cambiar opciones anteriores. Si se retrocede desde el primer paso, el asistente se cancela y regresa al historial de informes.
- **Reglas de selección múltiple (Parámetros y columnas del informe):**
    - En los pasos de selección múltiple (donde se eligen los campos que integrarán el informe), el usuario debe seleccionar un mínimo de 2 opciones para habilitar el botón "Crear informe".
    - Existe un límite máximo de selección determinado por la configuración del sistema para evitar tablas sobrecargadas. Una vez alcanzado el tope permitido, las demás casillas quedan temporalmente atenuadas e inhabilitadas hasta que se desmarque alguna opción previa.
    - El identificador o código del animal se incluye de manera interna y obligatoria en todo informe para garantizar la trazabilidad individual, sin restar cupos de selección al usuario.
- **Reglas de selección por rango de fechas:**
    - Cuando el reporte solicita un período de tiempo, la fecha inicial ("Desde") debe ser menor o igual a la fecha final ("Hasta").
    - Si la fecha inicial es posterior a la fecha final, el botón "Crear informe" se mantendrá deshabilitado hasta corregir la coherencia cronológica.
    - El usuario dispone de atajos rápidos para establecer rangos estándar con un solo toque: "Hoy", "Última semana", "Este mes" y "Último mes".

### Flujo Paso a Paso para el Usuario
- **Ruta de acceso en la aplicación:**
    - *Ruta 1 (Desde la pantalla de inicio de la finca):* Menú inferior (**Inicio**) > Sección **Informes** > Presionar sobre la tarjeta > En la pantalla de historial (**Informes**), presionar el botón **Empezar** dentro de la tarjeta superior **Generar nuevo informe**.
    - *Ruta 2 (Desde el Selector de Especie en Informes):* Si la finca cuenta con múltiples especies pecuarias configuradas, en la barra superior de la pantalla de historial (**Informes**), pulsar el ícono de especie para filtrar por la especie deseada (bovinos, bufalinos, equinos, caprinos, ovinos o porcinos) > En la tarjeta **Generar nuevo informe**, presionar **Comenzar**.

#### 1. Encabezado del Asistente y Navegación
- En la barra superior se visualiza el título "Nuevo informe" y el botón de flecha hacia la izquierda.
- Si se encuentra en el primer paso del asistente, presionar la flecha cancela el proceso y regresa al historial de informes.
- Si se encuentra en pasos avanzados (paso 2 o superior), presionar la flecha retrocede al paso inmediatamente anterior conservando las opciones previas para su ajuste.

#### 2. Selección de Criterios y Categorías (Pasos de Opción Única)
- En la parte superior de la pantalla se muestra el título de la pregunta o categoría a definir.
- En la lista central, pulse directamente sobre la alternativa deseada.
- Al tocar la opción, la aplicación la registra y avanza de manera inmediata a la siguiente etapa del asistente.
- Si la lista no contiene opciones disponibles, se muestra el estado "No hay nada para mostrar".

#### 3. Configuración de Parámetros del Informe (Pasos de Selección Múltiple)
- Cuando el paso presente casillas de verificación, active los datos o variables zootécnicas que desea incluir en las columnas del reporte.
- Verifique que al menos 2 casillas estén marcadas; de lo contrario, el botón "Crear informe" permanecerá deshabilitado.
- Si intenta marcar más opciones que el límite máximo permitido por el sistema, las casillas restantes aparecerán en tono gris atenuado y no responderán al toque hasta que deseleccione otra opción activa.
- Una vez seleccionadas las variables requeridas, pulse el botón "Crear informe" ubicado en la parte inferior.

#### 4. Selección de Período Cronológico (Rango de Fechas)
- Si el tipo de informe requiere un filtro de tiempo, se desplegará el selector interactivo de fechas en conjunto con el indicador "hasta".
- Puede utilizar los botones de acceso rápido situados debajo del selector para aplicar de inmediato un período predefinido:
    - "Hoy": Establece la jornada actual como inicio y fin.
    - "Última semana": Aplica los últimos 7 días transcurridos.
    - "Este mes": Fija desde el primer día del mes en curso hasta el día de hoy.
    - "Último mes": Selecciona el mes calendario inmediatamente anterior completo.
- Asegúrese de que la fecha inicial sea anterior o igual a la fecha final.
- Pulse el botón "Crear informe" en la parte inferior para formalizar la petición.
- **Pantalla de llegada tras guardar:** El sistema muestra una notificación de éxito con el mensaje "El informe se está generando y podrá acceder a él cuando termine." y redirige automáticamente al historial de informes de la finca (**Informes**).

#### Variaciones por especie
- **Especies con aptitud lechera (Bovinos, Bufalinos y Caprinos):** Cuentan con informes y parámetros especializados de lechería, tales como "Listado de ordeños por día", hato de ordeño, promedio de leche por día y días de lactancia.
- **Especies sin aptitud lechera (Equinos, Ovinos y Porcinos):** El árbol analítico no muestra categorías ni parámetros relacionados con ordeño ni producción láctea.
- **Terminología de etapas zootécnicas:** Las opciones de filtrado por etapa de desarrollo se adaptan automáticamente a la especie seleccionada (por ejemplo: ternero/vaca en bovinos; potrillo/yegua en equinos; lechón/cerda en porcinos; cordero/oveja en ovinos; cabrito/cabra en caprinos; bubillo/búfala en bufalinos).

#### Etiquetas de la interfaz en otros idiomas
- "Nuevo informe" → Inglés: "New Report" → Portugués: "Novo Relatório"
- "Crear informe" → Inglés: "Create Report" → Portugués: "Criar Relatório"
- "Generar nuevo informe" → Inglés: "Generate new report" → Portugués: "Gerar novo relatório"
- "Comenzar" → Inglés: "Start" → Portugués: "Começar"
- "Hoy" → Inglés: "Today" → Portugués: "Hoje"
- "Última semana" → Inglés: "Last week" → Portugués: "Última semana"
- "Este mes" → Inglés: "This month" → Portugués: "Este mês"
- "Último mes" → Inglés: "Last month" → Portugués: "Último mês"
- "hasta" → Inglés: "until" → Portugués: "até"
- "No hay nada para mostrar" → Inglés: "There is nothing to display" → Portugués: "Não há nada para exibir"
- "El informe se está generando y podrá acceder a él cuando termine." → Inglés: "The report is being generated and will be available once it is finished." → Portugués: "O relatório está sendo gerado e estará disponível quando for concluído."
- "Esta funcionalidad requiere una conexión activa a internet para poder funcionar correctamente. Por favor, verifica tu conexión e intenta de nuevo." → Inglés: "This feature requires an active internet connection to function properly. Please check your connection and try again." → Portugués: "Este recurso requer uma conexão ativa à internet para funcionar corretamente. Por favor, verifique sua conexão e tente novamente."

### Matriz de Errores y Soluciones
| Mensaje en la App / Síntoma | Causa Real | Respuesta Sugerida por el Agente | Criterio de Escalamiento Humano |
| :--- | :--- | :--- | :--- |
| "El informe se está generando y podrá acceder a él cuando termine." | Notificación informativa de confirmación exitosa: los parámetros fueron recibidos y el servidor comenzó a consolidar los registros zootécnicos. | "Su informe ha sido encolado y se está procesando en nuestros servidores. En unos instantes aparecerá disponible en su historial de informes para su consulta o exportación." | No requiere escalamiento; comportamiento esperado del sistema. |
| El botón "Comenzar" en la tarjeta "Generar nuevo informe" aparece deshabilitado en color gris claro y no responde | El dispositivo no detecta conexión a internet activa en ese instante | "Para generar un nuevo informe es necesario contar con conexión a internet activa, ya que el cálculo se procesa en línea. Por favor verifique que su red Wi-Fi o datos móviles estén encendidos e intente nuevamente." | Si el usuario dispone de navegación en otras aplicaciones y la función continúa deshabilitada, reportar a soporte técnico. |
| "Esta funcionalidad requiere una conexión activa a internet para poder funcionar correctamente. Por favor, verifica tu conexión e intenta de nuevo." | Pantalla de bloqueo activada por pérdida o ausencia de conexión a internet durante el uso del asistente | "Para estructurar y generar un informe se requiere conexión activa a internet. Por favor compruebe su conexión Wi-Fi o datos móviles y vuelva a ingresar al asistente una vez restablecida la señal." | Si la conexión es estable y el bloqueo persiste tras reiniciar la app, transferir a soporte técnico. |
| El botón "Crear informe" permanece deshabilitado en pasos con casillas de verificación | Se han seleccionado menos de 2 opciones obligatorias para configurar las columnas del reporte | "Para poder crear el informe debe marcar al menos dos opciones o parámetros de datos en la lista. Por favor seleccione una segunda casilla para habilitar el botón de generación." | No requiere escalamiento; regla de validación de formulario. |
| El botón "Crear informe" permanece deshabilitado en la pantalla de rango de fechas | La fecha inicial seleccionada es posterior a la fecha final ("hasta") | "La fecha de inicio del informe no puede ser posterior a la fecha de finalización. Por favor revise el selector y asegúrese de que el rango sea coherente o utilice uno de los atajos predeterminados como 'Este mes'." | No requiere escalamiento; validación cronológica. |
| Pantalla con mensaje "No hay nada para mostrar" | El nodo o categoría analítica consultada no devolvió opciones disponibles en el catálogo del servidor | "En este momento no hay opciones disponibles para este tipo de consulta en la finca. Por favor presione la flecha de regreso en la esquina superior para elegir otra categoría o consultar otra especie pecuaria." | Si la categoría debería contener opciones según el plan de la finca y aparece vacía reiteradamente, transferir a soporte técnico. |
| Espera prolongada en pantalla con indicador de carga | Demora o interrupción en la comunicación con el servidor central durante la carga del catálogo o el envío de la orden del informe | "La aplicación está comunicándose con el servidor para procesar su solicitud. Por favor espere un momento. Si la pantalla no avanza tras unos instantes, verifique la estabilidad de su señal de internet o cierre la aplicación por completo y vuelva a abrirla para intentar de nuevo." | Si la pantalla permanece congelada en el indicador de carga en múltiples intentos con conexión estable, transferir a soporte técnico. |
| Cuadro de diálogo de error de red o fallo al procesar la solicitud del informe | Interrupción momentánea en la comunicación con el servidor central durante la transferencia de los parámetros | "Ocurrió una interrupción al enviar su solicitud de informe. Por favor verifique su conexión a internet y pulse nuevamente el botón 'Crear informe'. Si la interrupción persiste, aguarde un minuto y reintente." | Si tras verificar estabilidad de red persiste el fallo en múltiples intentos, transferir a soporte técnico indicando el tipo de informe y especie pecuaria. |

### Directivas de Seguridad y Guardrails
- Recuerde al usuario que los informes consolidados reflejan los datos zootécnicos y sanitarios sincronizados en la finca activa; si recientemente registró pesajes, palpaciones o servicios en modo sin conexión, debe sincronizarlos antes de generar el informe para que aparezcan en los resultados.
- La información contenida en los informes (inventarios, producciones y valores comerciales) es de estricta confidencialidad del propietario y administradores autorizados de la finca.
- Jamás solicite contraseñas, pines de acceso, códigos SMS ni datos de pago del usuario por el canal de soporte para gestionar o reenviar un informe.
- No prometa tiempos exactos de cálculo ni resultados zootécnicos fuera de las variables soportadas por el sistema.
- Verifique siempre que el usuario esté ubicado en la finca correcta y consultando la especie correspondiente antes de orientarlo sobre la ausencia de datos en un informe.
