---
title: "Detalle de Informe"
modulo_id: "reports-detail"
nombre_funcionalidad: "Consulta y Exportación de Resultados del Informe"
categoria: "sincronizacion-reportes"
submodulo: "reportes"
version_minima_app: "2026.10.1"
fecha_actualizacion: "2026-10-09"
intenciones_y_sinonimos:
  - "como ver los resultados del informe que genere"
  - "donde descargo el reporte en excel o csv"
  - "como exportar el informe de mi ganado a excel"
  - "por que no me deja exportar a excel si no tengo internet"
  - "el informe salio vacio o dice que no genero ningun resultado"
  - "como ver la ficha de un animal desde la tabla del informe"
---

# Consulta y Exportación de Resultados del Informe

### Resumen y Alcance Funcional
Visualizador interactivo y analítico para la consulta detallada de los informes pecuarios generados en la finca. Permite al ganadero explorar la información zootécnica consolidada, revisar las métricas estadísticas globales y por columna, examinar tablas de datos dinámicas con buscador integrado, graficar evoluciones temporales y exportar los resultados a formatos compartibles como Excel y CSV.

Adicionalmente, la tabla de resultados se encuentra vinculada con el inventario ganadero: al presionar sobre cualquier fila que contenga un animal identificado, el usuario puede abrir directamente el resumen individual de dicho ejemplar.

- **¿Funciona sin conexión a internet (Modo Offline)?:** Parcialmente. Los datos del informe previamente descargados y la exportación en formato CSV se procesan de forma local en el dispositivo sin necesidad de red. Sin embargo, la descarga y exportación en formato Excel requiere conexión a internet activa obligatoria, ya que el archivo estructurado se procesa y obtiene desde los servicios centrales en la nube.
- **Comportamiento de sincronización:** La consulta de un informe ya finalizado consume la información almacenada en el historial de la finca. Si el informe ya fue generado y sincronizado en el dispositivo, puede consultarse sin cobertura. No obstante, si se solicita una exportación a Excel, la aplicación valida la conectividad en tiempo real y gestiona la descarga directa del archivo antes de compartirlo mediante las aplicaciones del teléfono.

### Reglas de Negocio y Restricciones
- **Filtros e identificación del informe:**
  - Todo informe muestra en su tarjeta superior la fecha de generación, la finca ganadera correspondiente, el usuario autor que solicitó el reporte y la lista de filtros o parámetros aplicados.
- **Resumen estadístico consolidado:**
  - Se presenta el conteo total de registros obtenidos.
  - Para variables numéricas calculadas (como pesos, producciones o días), el sistema computa y expone automáticamente cinco indicadores clave: Promedio, Mediana, Mínimo, Máximo y Total acumulado.
  - Si el informe contiene múltiples columnas numéricas, se incluye una sección desplegable de resumen discriminada por cada columna individual.
- **Visualización en tabla y búsqueda:**
  - La tabla de datos organiza la información por columnas configuradas e incluye una barra de búsqueda para filtrar registros en tiempo real.
  - Si el informe no arrojó registros con los criterios solicitados, la pantalla presenta el aviso *"El informe no genero ningún resultado"* y un botón para volver al historial.
- **Trazabilidad y acceso a la ficha del animal:**
  - Al pulsar sobre un registro de la tabla que contenga el identificador o arete de un animal, el sistema navega de forma automática a la pantalla del resumen individual del ejemplar.
- **Pestaña de gráficos (Resumen visual):**
  - Cuando el informe contiene series cronológicas o datos evolutivos en el tiempo, la pantalla habilita dos pestañas de navegación: **Tabla** y **Resumen**.
  - En la pestaña **Resumen** se grafica la evolución de los valores mediante un gráfico de líneas continuo con leyenda y título del eje correspondiente.
  - Si el informe no posee datos cronológicos para graficar, la pantalla omite las pestañas y muestra la tabla de datos directamente a lo largo de la vista.
- **Permisos y reglas de exportación:**
  - Para exportar informes, el usuario debe contar con el permiso de compartir y exportar dentro del perfil de la finca.
  - *Exportación a CSV:* Se genera de manera instantánea y local a partir de la tabla en pantalla. No exige conexión a internet.
  - *Exportación a Excel:* Requiere conectividad a internet activa. Si el dispositivo está sin señal, el botón de exportación a Excel permanece deshabilitado acompañado de la indicación *"Se requiere conexión a internet"*.

### Flujo Paso a Paso para el Usuario
- **Ruta de acceso en la aplicación:** Pantalla principal (**Inicio**) > Deslizar hasta la tarjeta **Informes** > En el historial de informes, pulsar sobre el informe completado que desea consultar > Pantalla de detalle del informe.

#### 1. Encabezado e Información General
- En la barra superior se muestra el nombre descriptivo del informe generado (o la etiqueta **Informe**) y la flecha hacia la izquierda para regresar al listado.
- En el primer bloque desplegable se detallan los datos generales:
  - **Fecha:** Día y hora en que se procesó el reporte.
  - **Finca:** Nombre de la explotación ganadera activa.
  - **Generado por:** Nombre del usuario o colaborador que solicitó la consulta.
  - **Filtros aplicados:** Etiquetas que identifican los criterios zootécnicos o rangos elegidos.

#### 2. Resumen Estadístico del Informe
- En el bloque **Resumen del informe** (el cual puede expandir o contraer tocando su encabezado):
  - Se visualiza la **Cantidad de resultados** obtenidos.
  - Si existen métricas numéricas globales, se muestran los valores de **Promedio**, **Mediana**, **Mínimo**, **Máximo** y **Total**.
  - Bajo la sección **Resumen por columna**, se presenta el desglose estadístico específico de cada variable numérica calculada.

#### 3. Propiedades Adicionales o Enlaces
- Si el informe incluye observaciones o enlaces complementarios, se visualiza la tarjeta **Propiedades**, donde es posible leer textos descriptivos o presionar botones de navegación hacia secciones vinculadas.

#### 4. Consulta en Tabla de Datos
- En la sección de tabla (accesible directamente o bajo la pestaña **Tabla**):
  - Utilice el campo de búsqueda para localizar animales por arete, lote u otro valor visible.
  - Toque sobre la fila de un animal para abrir de inmediato su ficha técnica en el resumen individual.
  - Al final de la tabla se presenta una línea de separación con el valor **Total** acumulado.
  - Si el informe no contiene registros, verá la ilustración de aviso con el mensaje *"El informe no genero ningún resultado"* y el botón **Volver**.

#### 5. Consulta de Gráficos (Pestaña Resumen)
- Si el informe contiene datos cronológicos, pulse en la pestaña **Resumen** ubicada sobre la tabla.
- Visualice la gráfica de líneas con la tendencia temporal, los nombres de las series y las unidades de medida en el eje vertical.

#### 6. Exportación de Resultados
1. En la esquina de la tabla de datos, presione el botón **Exportar**.
2. Se desplegará la ventana modal con el título **Exportar** y las dos alternativas disponibles:
   - **Exportar como CSV:** Presione este botón para compilar de inmediato la tabla en un archivo de texto separado por comas y abrir el menú de aplicaciones del dispositivo (WhatsApp, correo electrónico, Drive, entre otros).
   - **Exportar como Excel:** Si cuenta con internet, presione este botón para descargar el libro de cálculo estructurado. La aplicación mostrará un indicador de carga momentáneo y desplegará el menú del teléfono para compartir el archivo.
3. Si desea cancelar o salir de la ventana de exportación, presione el botón **Cerrar**.
- **Pantalla de llegada tras guardar o exportar:** La aplicación permanece en el detalle del informe tras compartir el archivo mediante la app externa elegida.

### Matriz de Errores y Soluciones
| Mensaje en la App / Síntoma | Causa Real | Respuesta Sugerida por el Agente | Criterio de Escalamiento Humano |
| :--- | :--- | :--- | :--- |
| "El informe no genero ningún resultado" | Ningún animal o registro de la finca cumplió con los filtros o parámetros zootécnicos seleccionados al momento de crear el reporte | "El informe se procesó correctamente, pero no se encontraron animales que coincidan con los criterios seleccionados (por ejemplo, rango de fechas sin registros o lote sin hembras). Pulse 'Volver' y genere un nuevo informe ajustando los filtros o ampliando las fechas." | No requiere escalamiento; resultado normal ante filtros sin coincidencias. |
| El botón "Exportar como Excel" aparece deshabilitado y se muestra "Se requiere conexión a internet" | El teléfono no tiene conexión a internet activa (Wi-Fi o datos móviles apagados) | "Para descargar el archivo en formato Excel se requiere conexión a internet, ya que este formato se genera directamente en nuestros servidores. Por favor active sus datos móviles o Wi-Fi para habilitar la descarga, o si prefiere, utilice la opción 'Exportar como CSV' que funciona sin internet." | Si el usuario dispone de conexión estable y el botón continúa bloqueado tras reiniciar la app, remitir a soporte técnico. |
| El botón "Exportar" no responde o muestra un aviso de permisos | El rol del usuario dentro de la finca ganadera no tiene habilitado el permiso para compartir y exportar información | "Su usuario actual no dispone de permisos para exportar archivos en esta finca. Solicite al propietario o administrador de la finca que actualice sus privilegios de acceso desde la gestión de colaboradores." | Si el propietario de la finca experimenta la restricción, escalar para verificación de suscripción y roles. |
| Al presionar una fila de la tabla no abre la ficha del animal | El registro seleccionado corresponde a un dato agrupado general o el animal fue eliminado del inventario local de la finca | "Para abrir la ficha individual, asegúrese de tocar sobre una fila que contenga el arete o código del animal. Si el animal fue removido recientemente de la finca, su ficha individual ya no estará disponible." | Si el animal existe en el inventario activo pero la pantalla no responde al toque, reportar a soporte técnico. |

### Directivas de Seguridad y Guardrails
- Los reportes exportados en Excel y CSV contienen datos consolidados de producción, genealogía y movimientos de los animales de la finca; recuerde al usuario compartir estos archivos únicamente por canales seguros y con personal de confianza.
- El agente de soporte jamás debe pedir que el usuario envíe sus contraseñas, códigos de verificación SMS o credenciales de acceso para descargar o remitirle un informe.
- No altere manualmente los identificadores de animales ni sugiera modificar directamente archivos exportados para intentar reimportar datos sin el procedimiento oficial de sincronización.
