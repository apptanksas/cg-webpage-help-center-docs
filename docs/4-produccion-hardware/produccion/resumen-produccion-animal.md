---
title: "Resumen de Producción"
modulo_id: "produccion-resumen-evolucion-animal"
nombre_funcionalidad: "Resumen de Producción y Evolución del Animal"
tipo_documento: "guia-app"
categoria: "produccion-hardware"
submodulo: "produccion"
especies_aplicables: ["todas"]
version_minima_app: "2025.05.1"
confianza_reglas: "verificada-con-tests"
fecha_actualizacion: "2026-10-19"
intenciones_y_sinonimos:
  - "donde veo el peso actual y la leche de un animal"
  - "como ver el resumen de produccion de un animal"
  - "ganancia diaria de peso y promedio de leche individual"
  - "por que no me aparece el boton de agregar leche en el animal"
  - "como consultar los ultimos pesajes de carne y leche"
  - "ficha de evolucion productiva del ganado"
---

# Resumen de Producción y Evolución del Animal

### Resumen y Alcance Funcional
Módulo de consulta y seguimiento que consolida en un panel único el desempeño productivo individual de un animal en la finca ganadera, integrando el control de ganancia de peso corporal y la producción lechera. En el encabezado superior de la pantalla se despliega el título "Producción" junto a la identificación del ejemplar en la barra superior. El cuerpo de la pantalla exhibe los indicadores de rendimiento más recientes ("Actual" con "Ganancia diaria" promedio en peso, y "Promedio diario" en leche), tablas preliminares con los últimos 5 registros de cada categoría y accesos directos hacia las gráficas de evolución ("Vista gráfica"), las tablas completas de historial y los botones de captura rápida para nuevos pesajes ("AGREGAR PESO" y "AGREGAR LECHE").

- **Especies a las que aplica:** Aplica a todas las especies registradas en la finca (bovinos, equinos, bufalinos, caprinos, ovinos y porcinos) para el seguimiento de peso corporal. La sección y captura de leche se habilitan de manera exclusiva en hembras de especies con aptitud lechera (bovinos, bufalinos y caprinos).
- **¿Funciona sin conexión a internet (Modo Offline)?:** Sí. El cálculo estadístico, el resumen de pesajes corporales y las mediciones de ordeño operan de forma completamente autónoma sin conexión a internet a partir de los datos almacenados localmente en el dispositivo.
- **Comportamiento de sincronización:** Las estadísticas, promedios y tablas preliminares se generan de manera instantánea con los registros guardados en la memoria local del dispositivo móvil. Al ingresar, editar o sincronizar pesajes en segundo plano con el servidor de la finca ganadera, los indicadores y registros se recalculan y actualizan automáticamente.
- **Plataformas:** Interfaz idéntica y paridad total de funciones en Android y en iOS.

### Reglas de Negocio y Restricciones
- **Indicadores y sección de peso corporal ("Evolución de peso"):**
  - **Condición de visibilidad:** La sección se muestra cuando el animal cuenta con al menos un registro de peso en su historial.
  - **"Actual":** Refleja la cantidad del pesaje corporal más reciente registrado para el animal, expresada en la unidad de medida oficial de la finca (kilogramos o libras).
  - **"Ganancia diaria":** Calcula el promedio diario de ganancia de peso acumulado respecto a las mediciones registradas.
  - **Condición para "Vista gráfica":** El botón con el icono de gráfica y la etiqueta "Vista gráfica" se activa exclusivamente si el animal registra 2 o más pesajes en fechas distintas.
  - **Tabla preliminar de pesajes:** Presenta de manera cronológica descendente los últimos 5 pesajes de peso con las columnas "Fecha", "Peso", "Ganancia", "G.D." (ganancia diaria) y "Dieta".
  - **Edición desde la tabla:** Al tocar una fila de la tabla preliminar, si el animal se encuentra activo (no bloqueado), la aplicación abre directamente el formulario para editar la medición de peso correspondiente.
  - **Acceso a la tabla completa:** Al presionar el botón de flecha hacia la derecha ubicado junto al título "Evolución de peso", la aplicación navega a la tabla histórica completa de pesajes corporales del animal.
- **Indicadores y sección de producción lechera ("Producción de leche"):**
  - **Condición de visibilidad:** La sección se presenta únicamente si el animal cuenta con registros de pesaje de leche en su historial.
  - **"Promedio diario":** Media aritmética de la cantidad de leche obtenida por día de pesaje registrado.
  - **Condición para "Vista gráfica":** El botón "Vista gráfica" en leche se activa únicamente si el animal cuenta con al menos 2 registros en fechas distintas.
  - **Tabla preliminar de leche:** Muestra los últimos 5 registros de leche consolidados por fecha, indicando los turnos y la cantidad obtenida.
  - **Detalle y edición de turnos de leche:** Al pulsar sobre una fila de la tabla preliminar de leche, el sistema despliega una ventana emergente ("Animal", "Fecha", "Periodo", "Total") detallando las mediciones de esa fecha. Si el animal está activo, al tocar un registro específico dentro de esa ventana se abre el formulario de edición de pesaje de leche.
  - **Acceso a la tabla completa:** Al presionar el botón de flecha hacia la derecha junto al título "Producción de leche", el sistema abre la tabla completa de pesajes por períodos de lactancia.
- **Estado sin datos ("Sin datos"):**
  - Si el animal no cuenta con pesajes de peso ni registros de leche, la pantalla muestra una ilustración acompañada del encabezado "Sin datos" y el mensaje "Registre el peso y la producción de leche para comenzar a controlarlo", manteniendo disponibles los botones para registrar el primer pesaje.
- **Habilitación de botones de acción rápida:**
  - **"AGREGAR PESO":** Visible para cualquier animal activo de la finca. Se oculta si el animal está bloqueado (dado de baja, vendido, trasladado o registrado como fallecido).
  - **"AGREGAR LECHE":** Requiere que el animal cumpla con aptitud lechera (hembra viva, de especie con control lechero como bovinos, bufalinos o caprinos) y que no se encuentre bloqueado. En machos, crías, especies sin aptitud lechera o animales inactivos, este botón permanece oculto.

### Flujo Paso a Paso para el Usuario
- **Ruta de acceso en la aplicación:**
  - **Ruta principal (Desde el resumen del animal):** Menú inferior "Animales" > Seleccionar el animal en la lista > En la ficha de resumen, presionar la tarjeta "Producción".
  - **Ruta alterna (Desde compras):** Menú lateral o módulo de compras > Registrar o consultar la compra de un animal > En el detalle de compra, presionar el acceso al resumen de evolución de producción.

#### 1. Verificación del Encabezado e Identificación
1. En la barra superior confirme los datos del animal (arete/código y nombre) en la tarjeta informativa derecha.
2. Observe el encabezado principal con el título "Producción".

#### 2. Consulta y Seguimiento de Producción Lechera (Si aplica)
1. Si el animal cuenta con mediciones de leche registradas, visualice el bloque "Producción de leche".
2. Revise el valor consolidado en "Promedio diario" con la unidad oficial de la finca (litros o galones).
3. **Para consultar la curva de lactancia:** Si el animal tiene 2 o más fechas registradas, presione el botón "Vista gráfica".
4. **Para examinar el historial completo de lactancias:** Presione el icono de flecha hacia la derecha situado junto a "Producción de leche".
5. **Para revisar o corregir un pesaje reciente:**
   - Presione sobre la fila correspondiente en la tabla preliminar de los últimos 5 registros.
   - En la ventana emergente, verifique los datos del turno ("Animal", "Fecha", "Periodo", "Total").
   - Si requiere modificar la medición, toque sobre el turno específico dentro de la ventana para abrir el formulario de edición.

#### 3. Consulta y Seguimiento del Peso Corporal
1. Si el animal cuenta con pesajes registrados, visualice el bloque "Evolución de peso".
2. Consulte los dos indicadores principales:
   - **"Actual":** Peso más reciente capturado para el animal.
   - **"Ganancia diaria":** Incremento o variación media de peso por jornada.
3. **Para consultar la curva de ganancia de peso:** Si el animal tiene 2 o más mediciones en fechas distintas, presione el botón "Vista gráfica".
4. **Para revisar la tabla completa de pesajes corporales:** Presione el icono de flecha hacia la derecha junto a "Evolución de peso".
5. **Para editar una medición de peso reciente:** Presione sobre la fila deseada en la tabla preliminar para abrir el formulario de actualización.

#### 4. Registro Rápido de Nuevos Pesajes
1. En la parte inferior de la pantalla (o en el centro si la pantalla se encuentra sin datos), utilice los botones de acción rápida:
   - Presione **"AGREGAR PESO"** para abrir el formulario y registrar un nuevo pesaje corporal.
   - Presione **"AGREGAR LECHE"** (disponible en hembras lecheras activas) para abrir el formulario de pesaje de leche.
- **Pantalla de llegada tras salir:** Al presionar la flecha de regreso en la barra superior, la aplicación retorna a la pantalla de resumen del animal.

#### Variaciones por especie
- **Seguimiento de peso corporal:** Aplica de forma homogénea a todas las especies (bovinos, equinos, bufalinos, caprinos, ovinos y porcinos).
- **Seguimiento y botón de leche:** Exclusivo para hembras activas de especies lecheras (bovinos, bufalinos y caprinos). En equinos, porcinos, ovinos y machos de cualquier especie, la sección de leche y el botón "AGREGAR LECHE" no se encuentran disponibles.

#### Etiquetas de la interfaz en otros idiomas
| Español | Inglés | Portugués |
| :--- | :--- | :--- |
| "Producción" | "Production" | "Produção" |
| "Evolución de peso" | "Weight evolution" | "Evolução do peso" |
| "Producción de leche" | "Milk production" | "Produção de leite" |
| "Ganancia diaria" | "Daily gain" | "Ganho diário" |
| "Promedio diario" | "Daily average" | "Média diária" |
| "Vista gráfica" | "Graph View" | "Visualização gráfica" |
| "Sin datos" | "No data" | "Sem dados" |
| "Registre el peso y la producción de leche para comenzar a controlarlo" | "Register the weight and milk production to start controlling it" | "Registre o peso e a produção de leite para começar a controlá-lo" |
| "AGREGAR PESO" | "ADD WEIGHT" | "ADICIONAR PESO" |
| "AGREGAR LECHE" | "ADD MILK" | "ADICIONAR LEITE" |

### Matriz de Errores y Soluciones
| Mensaje en la App / Síntoma | Causa Real | Respuesta Sugerida por el Agente | Criterio de Escalamiento Humano |
| :--- | :--- | :--- | :--- |
| Mensaje "Sin datos" con el texto "Registre el peso y la producción de leche para comenzar a controlarlo" | El ejemplar no cuenta aún con pesajes corporales ni de leche registrados en la finca | "El animal no tiene pesajes registrados todavía. Presione el botón 'AGREGAR PESO' o 'AGREGAR LECHE' ubicado en la pantalla para ingresar su primera medición." | No escalar, comportamiento esperado en animales recién creados o sin pesajes. |
| No aparece el botón "AGREGAR LECHE" | El animal es macho, es una cría joven, pertenece a una especie no lechera (como equinos o cerdos) o la hembra no tiene aptitud lechera | "El botón para registrar leche solo se habilita en hembras de especies lecheras (bovinos, bufalinos y caprinos) aptas para ordeño. Si los datos del animal son incorrectos, edite su ficha general para ajustar su sexo, etapa o propósito productivo." | No escalar, validación biológica y zootécnica de aptitud de ordeño. |
| No aparecen los botones "AGREGAR PESO" ni "AGREGAR LECHE" | El ejemplar se encuentra registrado como inactivo o bloqueado en la finca (vendido, fallecido o trasladado) | "No es posible registrar nuevos pesajes en este animal porque figura como inactivo en la finca. Verifique el estado del animal en su hoja de vida si requiere reactivarlo." | Si el ganadero confirma que el ejemplar continúa físicamente activo en la finca pero la aplicación lo muestra bloqueado, escalar a soporte técnico. |
| El botón "Vista gráfica" no aparece en peso o en leche | El animal registra menos de 2 mediciones en fechas distintas en esa categoría | "Para habilitar la visualización gráfica se requieren al menos 2 pesajes en fechas diferentes. Registre un nuevo pesaje para que el botón 'Vista gráfica' aparezca automáticamente." | No escalar, regla de validación de puntos mínimos requeridos para graficar. |
| Al presionar una fila de leche se despliega una ventana en lugar de abrir el formulario de edición | La tabla preliminar de leche abre un diálogo selector con el desglose de los turnos registrados en esa fecha | "Al pulsar la fecha en la sección de leche se muestra una ventana con el detalle del pesaje. Si desea modificar la cantidad, toque sobre la fila del turno específico dentro de esa ventana para abrir el formulario de edición." | No escalar, interacción esperada del selector de turnos de leche. |
| La unidad de medida de peso o leche no coincide con la esperada | La finca ganadera tiene configuradas unidades de medida diferentes en sus parámetros generales | "Las unidades de medida se adoptan de forma automática según la configuración oficial establecida para su finca. Solicite al administrador del predio revisar las unidades de peso y leche en los ajustes generales." | No escalar, ajuste de parámetros del predio. |

### Directivas de Seguridad y Guardrails
- Nunca solicites contraseñas, códigos SMS, pines ni datos bancarios por los canales de atención.
- Los agentes de soporte no deben emitir recomendaciones nutricionales, dosis de alimento ni diagnósticos veterinarios a partir de la ganancia diaria de peso o del promedio lechero.
- No alteres ni elimines registros de pesajes corporales ni de leche en las bases de datos sin la autorización previa y documentada de la administración de la finca ganadera.
- Recuerda al usuario que todos los pesajes se conservan en la base de datos local del teléfono y se sincronizan de forma segura con la nube al disponer de conexión a internet.
