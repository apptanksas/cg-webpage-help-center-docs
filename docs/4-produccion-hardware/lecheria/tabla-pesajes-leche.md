---
title: "Tabla de Producción de Leche"
modulo_id: "lecheria-tabla-produccion-leche"
nombre_funcionalidad: "Tabla de Historial de Pesajes de Leche"
tipo_documento: "guia-app"
categoria: "produccion-hardware"
submodulo: "lecheria"
especies_aplicables: ["bovinos", "bufalinos", "caprinos"]
version_minima_app: "2025.05.1"
confianza_reglas: "verificada-con-tests"
fecha_actualizacion: "2026-10-19"
intenciones_y_sinonimos:
  - "como ver la tabla de pesajes de leche de una hembra"
  - "historial de litros de leche por fecha y turno"
  - "consultar mediciones de leche por lactancia"
  - "como modificar o corregir un pesaje de leche anterior"
  - "donde veo los dias de lactancia y totales por ciclo lechero"
  - "tabla de produccion lechera individual"
---

# Tabla de Historial de Pesajes de Leche

### Resumen y Alcance Funcional
Módulo de consulta detallada que presenta el registro cronológico de todas las mediciones de pesaje de leche capturadas para una hembra en la finca ganadera. En el encabezado superior se consolidan los indicadores globales de rendimiento lechero ("Promedio diario", "Producción máxima", "Producción total" y "Días de lactancia"), mientras que en el cuerpo de la pantalla se despliega una tabla interactiva organizada por columnas ("Fecha", "Concentrado", "Mañana", "Tarde" y "Total leche"). Cuando el animal registra secados o partos que delimitan más de una lactancia, la información se organiza automáticamente en pestañas independientes por ciclo lechero, permitiendo además seleccionar cualquier fecha para consultar o corregir los pesajes realizados.

- **Especies a las que aplica:** Exclusivamente a hembras de especies con aptitud lechera registradas en la finca: bovinos, bufalinos y caprinos. Las especies sin control lechero (equinos, porcinos y ovinos) no disponen de esta visualización.
- **¿Funciona sin conexión a internet (Modo Offline)?:** Sí. El cálculo estadístico, la organización cronológica de las tablas y la segmentación por períodos operan de manera autónoma sin conexión a internet a partir de los datos almacenados en el dispositivo.
- **Comportamiento de sincronización:** Las tablas y métricas se generan de forma instantánea con los registros guardados localmente. Al registrar, editar o recibir pesajes sincronizados en segundo plano con el servidor de la finca ganadera, los datos de la tabla y los totales se actualizan automáticamente.
- **Plataformas:** Interfaz idéntica y paridad total de funciones en Android y en iOS.

### Reglas de Negocio y Restricciones
- **Indicadores estadísticos del encabezado:**
    - **"Promedio diario":** Media aritmética de la cantidad de leche obtenida por día con registro en todo el historial del animal.
    - **"Producción máxima":** Medición diaria más alta registrada para el animal en la finca.
    - **"Producción total":** Suma acumulada de todos los pesajes de leche registrados en la historia del ejemplar.
    - **"Días de lactancia":** Número total de jornadas en las que el animal registra mediciones de pesaje.
    - **Métricas comparativas para múltiples lactancias:** Si el animal registra más de un ciclo productivo, el encabezado incorpora el total en "Periodo de lactancia" (conteo de ciclos registrados) y el "Promedio por lactancia" (volumen medio de leche obtenido por período).
- **Segmentación por períodos de lactancia:**
    - El sistema calcula los períodos de lactancia considerando las fechas de parto y los tratamientos de secado registrados en el historial de la hembra.
    - Si el animal registra dos o más ciclos de lactancia, se habilitan pestañas superiores rotuladas como "Lactancia 1", "Lactancia 2", etc., permitiendo alternar entre períodos tocando la pestaña o deslizando horizontalmente.
    - Al pie de la tabla de cada período se despliega un bloque de resumen con el "Total" de leche del ciclo, los "Días de lactancia" acumulados, el "Promedio diario" y la "Producción máxima" propios de esa lactancia.
    - Si la hembra no registra secados o cuenta con un único ciclo lechero, los datos se despliegan en una única tabla continua sin pestañas divisoras.
- **Estructura de la tabla y detalle por turnos:**
    - Las columnas desplegadas corresponden a "Fecha", "Concentrado", "Mañana", "Tarde" y "Total leche".
    - Si en una misma fecha existen pesajes en turnos divididos (mañana y tarde), el sistema consolida el volumen total en la fila diaria.
    - Al presionar una fila con un único pesaje en la fecha, la aplicación abre de forma directa el formulario de edición.
    - Si la fecha contiene registros en más de un turno, la aplicación despliega una ventana emergente para que el usuario elija el turno específico que desea revisar o modificar.
- **Unidad de medida:**
    - Las cantidades de leche y alimento concentrado se presentan automáticamente en la unidad de medida oficial configurada para la producción en la finca ganadera (litros, galones o kilogramos).
- **Acceso rápido al registro de pesaje:**
    - Si el animal se encuentra activo en la finca (no bloqueado por venta, muerte o traslado), se muestra un botón flotante con el icono de recipiente de leche para abrir el formulario de captura individual.

### Flujo Paso a Paso para el Usuario
- **Ruta de acceso en la aplicación:**
    - Menú inferior "Animales" > Seleccionar la hembra > Presionar la tarjeta "Producción" > En el bloque "Producción de leche", presionar el icono de flecha hacia la derecha.

#### 1. Lectura del Encabezado e Indicadores Globales
1. En la barra superior confirme la identificación del animal (arete y nombre).
2. En el encabezado "Producción de leche", revise los indicadores consolidados de la hembra:
    - **"Promedio diario":** Rendimiento medio por día de pesaje.
     - **"Producción máxima":** Volumen máximo obtenido en un día.
     - **"Producción total":** Acumulado global de leche del animal.
     - **"Días de lactancia":** Total de días registrados con pesaje.
     - *(Si registra múltiples ciclos)* Revise el conteo en "Periodo de lactancia" y el "Promedio por lactancia".

#### 2. Consulta y Navegación por Períodos de Lactancia
1. **Si el animal cuenta con más de una lactancia:**
    - Toque la pestaña correspondiente ("Lactancia 1", "Lactancia 2", etc.) en la barra superior o deslice la pantalla horizontalmente para cambiar de período.
     - Deslice verticalmente para explorar las mediciones del ciclo seleccionado.
     - Al final de la tabla, consulte el resumen exclusivo de ese ciclo con el "Total", los "Días de lactancia", el "Promedio diario" y la "Producción máxima".
2. **Si el animal cuenta con una sola lactancia:**
    - La tabla se presenta en una vista continua con la totalidad de fechas y mediciones registradas.

#### 3. Consulta y Edición de un Pesaje Registrado
1. En la tabla, ubique la fecha correspondiente y presione sobre la fila:
   - Si el día registra un único turno de pesaje, la aplicación abrirá directamente el formulario de edición.
   - Si el día contiene mediciones en turnos divididos (por ejemplo, mañana y tarde), se desplegará una ventana emergente con la lista de turnos; presione el turno que desea corregir.
2. En el formulario de edición, modifique la cantidad de leche o el concentrado suministrado y guarde los cambios.
3. Al guardar, el sistema actualizará de inmediato la fila y los totales en la tabla.

#### 4. Registro Rápido de Nuevo Pesaje (Opcional)
1. Para ingresar una nueva medición sin abandonar la consulta, presione el botón flotante circular con el icono de recipiente de leche ubicado en la esquina inferior.
2. Complete los datos en el formulario de pesaje individual y guarde el registro.
    - **Pantalla de llegada tras salir:** Al pulsar la flecha de regreso en la barra superior, la aplicación retorna a la pantalla de resumen de "Producción" del animal.

#### Variaciones por especie
- **Especies lecheras:** La tabla y las métricas de lactancia aplican a hembras de bovinos (vacas), bufalinos (búfalas) y caprinos (cabras).
- **Especies no compatibles:** En équidos, cerdas y ovejas (salvo configuraciones zootécnicas especializadas), la tarjeta de producción lechera y el acceso a la tabla no se encuentran disponibles en la hoja de vida del animal.

#### Etiquetas de la interfaz en otros idiomas
| Español | Inglés | Portugués |
| :--- | :--- | :--- |
| "Producción de leche" | "Milk production" | "Produção de leite" |
| "Promedio diario" | "Daily average" | "Média diária" |
| "Producción máxima" | "Max production" | "Produção máxima" |
| "Producción total" | "Total production" | "Produção total" |
| "Días de lactancia" | "Lactation days" | "Dias de lactação" |
| "Periodo de lactancia" | "Lactation period" | "Período de lactação" |
| "Promedio por lactancia" | "Average per lactation" | "Média por lactação" |
| "Lactancia %1$d" | "Lactation %1$d" | "Lactação %1$d" |
| "Total" | "Total" | "Total" |
| "Fecha" | "Date" | "Data" |
| "Concentrado" | "Concentrate" | "Concentrado" |
| "Mañana" | "Morning" | "Manhã" |
| "Tarde" | "Afternoon" | "Tarde" |
| "Total leche" | "Total milk" | "Leite total" |

### Matriz de Errores y Soluciones
| Mensaje en la App / Síntoma | Causa Real | Respuesta Sugerida por el Agente | Criterio de Escalamiento Humano |
| :--- | :--- | :--- | :--- |
| La tabla aparece completamente vacía sin registros | El animal no tiene pesajes de leche registrados en su historial o los datos no han terminado de descargarse en el dispositivo | "La hembra aún no registra pesajes de leche en su historial. Presione el botón flotante con el icono de leche para registrar la primera medición del animal." | Si el usuario comprueba haber registrado pesajes previamente en este animal y no aparecen tras sincronizar, escalar a soporte técnico indicando el arete del animal. |
| No aparece el botón flotante con el icono de leche para agregar pesajes | El animal se encuentra inactivo o bloqueado en la finca (registrado como vendido, fallecido o trasladado) | "El botón de registro rápido no se muestra porque el animal figura como inactivo en la finca. Verifique el estado del animal en su hoja de vida si requiere reactivarlo." | Si el ganadero confirma que el ejemplar continúa activo en ordeño en la finca pero la aplicación lo detecta inactivo, transferir a soporte técnico. |
| Al presionar una fecha en la tabla, se abre una ventana preguntando por el turno | En esa fecha se registraron dos o más turnos de ordeño (por ejemplo, mañana y tarde) | "En esa fecha se realizaron pesajes en más de un turno. Seleccione en la ventana emergente el turno específico que desea revisar o modificar." | No escalar, comportamiento esperado de selección de turno múltiple. |
| La unidad de medida de la tabla no coincide con la esperada | La finca ganadera tiene configurada una unidad de leche o peso diferente en sus ajustes de predio | "La tabla y los resúmenes muestran la unidad de medida establecida para la leche en la configuración general de su finca. Solicite al administrador del predio verificar la unidad de medida desde los ajustes de la finca." | No escalar, ajuste de parámetros de predio. |

### Directivas de Seguridad y Guardrails
- Nunca solicites contraseñas, códigos SMS, pines ni datos bancarios por los canales de atención.
- Los agentes de soporte no deben emitir recomendaciones zootécnicas, nutricionales ni diagnósticos clínicos veterinarios a partir de las variaciones observadas en los pesajes de la tabla.
- No alteres ni elimines registros históricos de pesajes de leche directamente en las bases de datos sin la autorización previa y documentada del propietario de la finca ganadera.
- Recuerda al usuario que todos los registros de pesaje se conservan en la base de datos local del teléfono y se sincronizan de forma segura con la nube al disponer de conexión a internet.
