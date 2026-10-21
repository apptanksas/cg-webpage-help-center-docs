---
title: "Historial de Informes"
modulo_id: "reports-history"
nombre_funcionalidad: "Historial y Seguimiento de Informes Pecuarios"
categoria: "sincronizacion-reportes"
submodulo: "reportes"
version_minima_app: "2026.10.1"
fecha_actualizacion: "2026-10-09"
intenciones_y_sinonimos:
  - "donde veo los informes que he solicitado o generado"
  - "como consultar el historial de reportes de mi finca"
  - "por que mi informe dice generando y cuando estara listo"
  - "que significa cuando un informe aparece con estado de error"
  - "como cambiar de especie pecuaria en los informes"
  - "por que no me deja iniciar o generar un nuevo informe"
---

# Historial y Seguimiento de Informes Pecuarios

### Resumen y Alcance Funcional
Pantalla central de consulta, supervisión y administración cronológica de todos los informes zootécnicos y productivos solicitados en la finca activa. Permite al ganadero explorar el catálogo de reportes procesados, revisar la fecha de solicitud, verificar los filtros aplicados, monitorear el estado de generación en tiempo real y acceder directamente a los resultados consolidados de aquellos que culminaron exitosamente.

Asimismo, la pantalla sirve como punto de partida para solicitar nuevos reportes personalizados y cuenta con un selector de especie pecuaria que permite segmentar el historial según los animales de trabajo configurados en la explotación (bovinos, bufalinos, equinos, ovinos, caprinos o porcinos).

- **¿Funciona sin conexión a internet (Modo Offline)?:** Parcialmente. Los informes previamente descargados y consultados en la memoria del dispositivo pueden visualizarse en el listado sin cobertura. Sin embargo, para cargar páginas anteriores del historial, solicitar un nuevo informe o verificar la finalización de reportes que se encuentren en proceso de cómputo en la nube, se requiere conexión a internet activa obligatoria.
- **Comportamiento de sincronización:** La pantalla sincroniza de forma paginada los registros históricos almacenados en el servidor central. Cuando el usuario tiene informes con estado de procesamiento activo ("Generando..."), la aplicación ejecuta comprobaciones automáticas periódicas en segundo plano cada 10 segundos para actualizar el estado; en el momento en que el servidor completa exitosamente el reporte, el sistema abre de manera automática la pantalla de detalle del resultado.

### Reglas de Negocio y Restricciones
- **Filtrado por especie pecuaria:**
  - Si la finca cuenta con más de una especie animal registrada y configurada, la aplicación habilita un selector en la barra superior identificado con la silueta de la especie activa.
  - Al presionar dicho icono, se despliega el menú de selección con las especies disponibles. Al cambiar de especie, el historial se reinicia y muestra exclusivamente los reportes vinculados a ese tipo de animal.
  - Si la explotación solo gestiona una especie, el sistema la selecciona de manera predeterminada y oculta el selector para simplificar la vista.
- **Acceso a la creación de nuevos informes:**
  - En la parte superior de la vista se ubica la tarjeta permanente **Generar nuevo informe**, la cual muestra la fecha del último informe solicitado en la finca.
  - El botón **Iniciar** y el toque sobre la tarjeta requieren conexión a internet activa. Si el dispositivo no tiene red, el botón se muestra en gris deshabilitado y restringe el ingreso al asistente de creación.
- **Estados de procesamiento de un informe:**
  - **Generando... (Azul oscuro / En proceso):** El servidor central se encuentra procesando los algoritmos y compilando los datos zootécnicos solicitados. El icono de estado realiza una animación vertical continua. Mientras la pantalla permanezca abierta con conexión a internet, la aplicación verifica el avance cada 10 segundos. Si el reporte finaliza mientras el usuario observa la lista, se abre automáticamente la pantalla de resultados.
  - **Completado (Verde oscuro / Exitoso):** El informe culminó su procesamiento y sus datos están consolidados. Se muestra el botón **Ver** habilitado en verde. Al pulsar la tarjeta o el botón **Ver**, el usuario accede a la pantalla de detalle, gráficos y exportación.
  - **Error (Rojo / Fallido):** Ocurrió una interrupción durante el cómputo en el servidor o los parámetros generaron un conflicto irrecuperable. El botón **Ver** aparece deshabilitado en gris claro y no es posible abrir el reporte, requiriendo generar una nueva solicitud.
- **Paginación y carga continua:**
  - El historial expone en su encabezado la cantidad total de informes registrados entre corchetes (por ejemplo: `[15]`).
  - La lista carga los reportes de manera progresiva a medida que el usuario se desplaza hacia abajo en la pantalla (scroll infinito). La paginación hacia bloques antiguos se suspende si el teléfono pierde la conexión a internet.
- **Pantalla vacía sin registros:**
  - Si la finca no tiene ningún informe generado para la especie seleccionada, la pantalla presenta la ilustración representativa y el mensaje *"No hay informes generados"*.
- **Indicadores de carga y progreso:**
  - *Carga inicial:* Al ingresar a la pantalla, mientras se consulta por primera vez la lista de informes al servidor, se presenta un indicador de carga a pantalla completa.
  - *Carga durante paginación (scroll infinito):* Al desplazarse hacia el final del listado para obtener reportes más antiguos, aparece un indicador de carga en la parte inferior de la lista mientras se reciben los nuevos registros.

### Flujo Paso a Paso para el Usuario
- **Ruta de acceso en la aplicación:** Pantalla principal (**Inicio**) > Deslizar hasta la sección de accesos directos > Pulsar sobre la tarjeta **Informes** > Pantalla de historial de informes.

#### 1. Consulta del Historial y Especie Activa
1. Al ingresar a la pantalla, verifique en la barra superior el título **Informes**.
2. Si su finca gestiona múltiples especies (por ejemplo, vacas y caballos), observe el icono ubicado en la esquina superior derecha:
   - Presione el icono para abrir la ventana modal **Seleccionar tipo de animal**.
   - Pulse sobre la especie que desea consultar (bovinos, bufalinos, equinos, etc.). La pantalla se actualizará de inmediato para mostrar los reportes asociados a dicha especie.

#### 2. Generación de un Nuevo Reporte
1. En la tarjeta superior con el título **Generar nuevo informe**, revise la etiqueta **Último informe** para conocer cuándo se procesó la consulta más reciente.
2. Asegúrese de contar con conexión a internet (Wi-Fi o datos móviles activos).
3. Presione el botón **Iniciar** o pulse en cualquier zona de la tarjeta para ingresar al asistente paso a paso de confección de reportes.

#### 3. Monitoreo y Apertura de Informes en el Listado
1. Desplácese verticalmente por la lista bajo el encabezado **Historial de informes**, donde podrá observar el número total de registros disponibles.
2. Cada tarjeta de informe presenta:
   - **Fecha:** Día y hora en que se solicitó el reporte.
   - **Nombre:** Nombre descriptivo del informe generado (ejemplo: *Hembras - Estado reproductivo* o *Listado de ordeños por día*).
   - **Filtros:** Resumen de las condiciones y variables zootécnicas configuradas.
   - **Estado:** Indicador que señala si el informe está **Generando...**, **Completado** o en **Error**.
3. **Acciones según el estado del informe:**
   - Si el informe está **Completado**, presione el botón **Ver** o toque la tarjeta para ingresar a la tabla de resultados, métricas estadísticas y opciones de exportación en Excel o CSV.
   - Si el informe dice **Generando...**, espere unos instantes en la pantalla. La aplicación consultará automáticamente al servidor y lo redirigirá a los resultados tan pronto esté listo.
   - Si el informe muestra **Error**, la información no pudo procesarse en el servidor; deslice a la parte superior y pulse **Iniciar** para volver a solicitarlo.

### Matriz de Errores y Soluciones
| Mensaje en la App / Síntoma | Causa Real | Respuesta Sugerida por el Agente | Criterio de Escalamiento Humano |
| :--- | :--- | :--- | :--- |
| "No hay informes generados" | La finca no ha solicitado ningún reporte zootécnico bajo la especie pecuaria seleccionada actualmente | "Actualmente no existen reportes registrados para esta especie de animal en la finca. Puede presionar el botón 'Iniciar' en la parte superior para crear su primer informe personalizado, o bien cambiar la especie desde el icono superior si tiene bovinos u otros animales." | No requiere escalamiento; comportamiento esperado en hatos nuevos o sin consultas previas. |
| El botón "Iniciar" en la tarjeta de generar informe aparece en gris y no responde al toque | El teléfono móvil se encuentra sin conexión a internet activa | "Para generar un nuevo informe se necesita conexión a internet, ya que las opciones y el procesamiento se gestionan en nuestros servidores centrales. Por favor active su conexión Wi-Fi o sus datos móviles e intente nuevamente." | Si el usuario dispone de conectividad estable y el botón continúa inactivo tras reiniciar la app, remitir a soporte técnico. |
| El informe permanece indefinidamente con el estado "Generando..." y no avanza a completado | Pérdida de cobertura prolongada en el móvil o demora extraordinaria en el procesamiento de un volumen masivo de datos en el servidor | "El reporte se encuentra en cola de cómputo en el servidor. Si estuvo sin señal de internet, vuelva a conectar su dispositivo a una red estable y mantenga abierta la pantalla de informes durante unos segundos para que se actualice el estado automáticamente. Si transcurren más de 10 minutos sin cambio, le sugerimos solicitar el informe nuevamente." | Si múltiples informes continúan congelados en 'Generando...' con internet estable por más de 30 minutos, reportar al equipo de infraestructura para revisar colas de reportes. |
| El informe muestra el estado "Error" en color rojo y el botón "Ver" está apagado | Se presentó un fallo inesperado al computar los registros zootécnicos solicitados o se configuraron filtros mutuamente excluyentes | "El servidor no pudo compilar los datos para este reporte en específico. Este intento no puede visualizarse, por lo que le recomendamos pulsar 'Iniciar' y generar una nueva solicitud. Si estaba filtrando por rangos de fechas muy extensos o parámetros combinados complejos, intente acotar el criterio." | Si solicitudes sucesivas del mismo tipo continúan finalizando en estado 'Error', escalar a ingeniería con el nombre y parámetros del reporte. |
| Al hacer scroll hacia abajo no cargan informes más antiguos | El dispositivo se quedó sin conexión a internet tras haber cargado la primera pantalla de registros | "Para consultar páginas anteriores del historial de informes se requiere conexión a internet activa. Compruebe la señal de sus datos móviles o Wi-Fi y deslice nuevamente hacia abajo para continuar cargando los reportes." | Si con conexión verificada el scroll infinito no solicita más registros y el total indicado entre corchetes es mayor al visible, escalar a soporte técnico. |
| Círculo de espera infinito / Pantalla congelada en cargando | Proceso de consulta bloqueado o fallo de conexión al solicitar los informes del servidor | "Espere 30 segundos. Si no avanza, cierre la aplicación por completo desde el administrador de tareas de su teléfono (deslizando hacia arriba) y vuelva a abrirla. Sus datos locales no se perderán." | Si tras reabrir la app con conexión a internet estable la pantalla vuelve a congelarse en el círculo de carga, transferir de inmediato a soporte técnico con correo y modelo del teléfono. |

### Directivas de Seguridad y Guardrails
- Recuerde al usuario que cada informe generado refleja la fotografía de los datos zootécnicos de la finca en el momento exacto de su solicitud; si se ingresaron nuevos partos, pesos o palpaciones posteriormente, debe solicitar un nuevo informe para reflejar las novedades más recientes.
- Los reportes de la finca contienen información estratégica del inventario pecuario; el agente de soporte jamás solicitará contraseñas ni códigos de autenticación para consultar o destrabar informes.
- El agente no debe prometer tiempos exactos de respuesta para la generación de reportes masivos, ya que estos dependen del volumen de cabezas de ganado de la finca y la estabilidad de la conexión del usuario.
