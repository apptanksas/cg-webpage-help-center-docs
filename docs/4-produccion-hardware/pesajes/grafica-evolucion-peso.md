---
title: "Gráfica de Peso"
modulo_id: "pesajes-grafica-evolucion-peso"
nombre_funcionalidad: "Gráfica de Evolución de Peso Corporal"
tipo_documento: "guia-app"
categoria: "produccion-hardware"
submodulo: "pesajes"
especies_aplicables: ["todas"]
version_minima_app: "2025.05.1"
confianza_reglas: "verificada-con-tests"
fecha_actualizacion: "2026-10-19"
intenciones_y_sinonimos:
  - "como ver la curva de crecimiento y peso del ganado"
  - "grafica de evolucion de peso individual del animal"
  - "donde veo la ganancia diaria de peso y el peso actual"
  - "por que no me aparece el boton de ver grafica en peso"
  - "grafico de peso corporal y tipo de dieta"
  - "curva de ganancia de peso del animal"
---

# Gráfica de Evolución de Peso Corporal

### Resumen y Alcance Funcional
Herramienta visual que grafica la curva de crecimiento y evolución de peso corporal de un animal a lo largo del tiempo, facilitando la evaluación del desarrollo ponderal, la efectividad del plan de alimentación y la respuesta a los manejos de la finca ganadera. En el encabezado superior se consolidan los indicadores de desempeño clave (último peso registrado rotulado como "Actual", promedio de "Ganancia diaria" y régimen alimenticio rotulado como "Dieta"). En el área principal se dibuja una curva continua con estilo de termómetro que conecta cronológicamente los pesajes registrados e incluye una proyección estimada que extiende la tendencia hasta la fecha actual.

- **Especies a las que aplica:** Aplica por igual a todas las especies manejadas en la finca ganadera (bovinos, bufalinos, equinos, caprinos, ovinos y porcinos).
- **¿Funciona sin conexión a internet (Modo Offline)?:** Sí. El trazado de la curva y el cálculo de indicadores operan de forma completamente autónoma sin conexión a internet, procesando los registros de pesaje almacenados localmente en la base de datos del teléfono móvil.
- **Comportamiento de sincronización:** Las estadísticas y la curva se actualizan al instante al registrar, editar o eliminar pesajes en el dispositivo. Al sincronizar en segundo plano con el servidor de la finca ganadera mediante Horus, cualquier nueva medición remota se incorpora automáticamente al gráfico.
- **Plataformas:** Funciona con idéntica interfaz y comportamiento tanto en dispositivos Android como en iOS.

### Reglas de Negocio y Restricciones
- **Mínimo estricto de pesajes requeridos (Verificado con tests):**
    - Se requiere un mínimo de **2 registros de pesaje corporal** en el historial del animal para poder generar y trazar la curva de evolución.
    - Si el animal tiene menos de 2 pesajes registrados, el botón "Vista gráfica" no se muestra en la sección "Evolución de peso" del resumen de producción.
    - Si por alguna eventualidad se intenta abrir la pantalla con menos de 2 pesajes (por ejemplo, tras eliminar registros), el sistema interrumpe la carga y redirige automáticamente hacia la pantalla anterior para resguardar la experiencia visual.
- **Indicadores del encabezado superior:**
    - **Peso actual ("Actual %1$s"):** Muestra el valor del último pesaje corporal registrado para el animal junto a su unidad de medida (kilogramos o libras). Si no hay datos, muestra el símbolo "---".
    - **Ganancia diaria de peso ("Ganancia diaria"):** Promedio ponderado de ganancia diaria calculado a partir del histórico de pesajes y el lapso entre mediciones.
    - **Régimen nutricional ("Dieta"):** Muestra el tipo de alimentación asignado en la última medición ("Pastoreo", "Pastoreo + Concentrado", "Heno", "Ensilage", "Concentrado", "Suplementos", "Forraje", "Raciones mezcladas", "Estabulación" u "Otros"). Si la última pesada no tiene dieta especificada, se exhibe el indicador de ausencia de datos "---".
- **Comportamiento y escala del gráfico:**
    - Curva de líneas continuas que proyecta visualmente la tendencia del peso del animal hasta la fecha actual.
    - El eje vertical (eje Y) y los valores de los puntos se adaptan automáticamente a la unidad de medida oficial de peso configurada en la finca ganadera activa (kilogramos o libras).
    - La leyenda y los valores de cada pesaje se presentan formateados a un decimal.
- **Botón de acción rápida para registrar peso:**
    - Si el ejemplar se encuentra activo y no bloqueado en la finca (no figura como vendido, fallecido ni trasladado), se exhibe en la esquina inferior derecha un botón flotante con el icono de báscula para registrar rápidamente un nuevo pesaje individual.
    - Si el animal está bloqueado o dado de baja, el botón flotante se oculta automáticamente.

### Flujo Paso a Paso para el Usuario
- **Ruta de acceso en la aplicación:**
    - **Ruta principal:** Menú inferior "Animales" > Seleccionar el animal de la lista > Tarjeta "Producción" > Sección "Evolución de peso" > Presionar el botón "Vista gráfica".

#### 1. Acceso y Verificación de Requisitos
1. Ingrese a la ficha del animal desde el listado general en "Animales".
2. Ubique la tarjeta "Producción" y desplace la vista hasta la sección "Evolución de peso".
3. Confirme que el animal cuente con al menos dos pesajes registrados.
4. Presione el botón "Vista gráfica" (ubicado junto a la métrica de ganancia diaria).

#### 2. Interpretación de la Información en Pantalla
1. **Identificación del animal:** En la barra superior confirme los datos del ejemplar (nombre, código o arete y fotografía si está disponible).
2. **Encabezado con métricas clave:**
   - En la parte superior de color destacado, observe:
     - El peso más reciente bajo la etiqueta "Actual %1$s" (por ejemplo: "Actual 420.5 kg").
     - El incremento promedio diario bajo la etiqueta "Ganancia diaria" (por ejemplo: "0.65 kg/día").
     - El régimen nutricional asignado bajo la etiqueta "Dieta" (por ejemplo: "Pastoreo + Concentrado" o "---" si no se registró).
3. **Curva gráfica de peso:**
   - En el cuerpo de la pantalla, explore el gráfico lineal de evolución.
   - El eje horizontal refleja la cronología de fechas y el eje vertical la escala de peso según la unidad configurada en la finca.
   - Cada punto representa una pesada real, y la línea punteada o extendida proyecta la tendencia esperada hacia el día de hoy.

#### 3. Registro de Nuevo Pesaje desde la Gráfica (Opcional)
1. Si el animal está activo y desea incorporar una nueva medición, presione el botón flotante circular con el icono de báscula en la esquina inferior derecha.
2. La aplicación abrirá inmediatamente la pantalla "Registrar peso" vinculada al ejemplar.
3. Al completar el formulario y presionar "Registrar", el sistema regresa a la gráfica reflejando la nueva medición de inmediato.
- **Pantalla de llegada tras salir:** Al pulsar el botón de flecha hacia atrás en la barra superior, el usuario regresa a la tarjeta "Producción" en la hoja del animal.

#### Variaciones por especie
Aplica de forma universal e idéntica a todas las especies zootécnicas de la finca ganadera (bovinos, bufalinos, equinos, caprinos, ovinos y porcinos). La curva de crecimiento, las unidades de medida configuradas y los cálculos de ganancia diaria operan bajo el mismo estándar biológico.

#### Etiquetas de la interfaz en otros idiomas
| Español | Inglés | Portugués |
| :--- | :--- | :--- |
| "Vista gráfica" | "Graphic view" | "Vista gráfica" |
| "Actual %1$s" | "Current %1$s" | "Atual %1$s" |
| "Ganancia diaria" | "Daily Gain" | "Ganho Diário" |
| "Dieta" | "Diet" | "Dieta" |
| "Evolución de peso" | "Weight evolution" | "Evolução do peso" |
| "Sin datos" / "---" | "No data" / "---" | "Sem dados" / "---" |
| "Registrar peso" | "Register weight" | "Registrar peso" |

### Matriz de Errores y Soluciones
| Mensaje en la App / Síntoma | Causa Real | Respuesta Sugerida por el Agente | Criterio de Escalamiento Humano |
| :--- | :--- | :--- | :--- |
| El botón "Vista gráfica" no aparece en la sección "Evolución de peso" | El animal tiene menos de 2 registros de pesaje en su historial | "Para generar la gráfica de evolución se requieren al menos 2 pesajes registrados en diferentes momentos. Agregue un nuevo pesaje mediante el botón 'AGREGAR PESO' para que la gráfica se habilite." | No escalar, comportamiento esperado del sistema para garantizar consistencia gráfica. |
| Al presionar "Vista gráfica", la pantalla se cierra y vuelve de inmediato al resumen del animal | La base de datos local confirmó que el ejemplar tiene menos de 2 pesajes válidos (por ejemplo, si se eliminó una pesada recientemente) | "La curva requiere un mínimo de 2 mediciones para poder trazarse. Registre los pesajes faltantes para volver a consultar la gráfica." | Si en la tabla de pesajes se aprecian 2 o más registros pero la pantalla sigue saliendo automáticamente, escalar a soporte técnico indicando la identificación del animal. |
| No aparece el botón flotante con el icono de báscula en la parte inferior | El animal se encuentra inactivo o bloqueado en la finca ganadera (marcado como muerto, vendido o trasladado) | "El botón para registrar nuevos pesajes no se muestra porque el ejemplar figura como inactivo en la finca. Si requiere registrar mediciones, verifique el estado del animal en su hoja de vida para reactivarlo." | Si el usuario confirma que el ejemplar continúa activo en el predio pero figura bloqueado, escalar a soporte técnico. |
| La unidad de medida en el gráfico no es la deseada (por ejemplo, libras en lugar de kilos) | La finca ganadera tiene establecida otra unidad de medida en sus parámetros generales | "La unidad de peso (kilogramos o libras) se toma de la configuración global de su finca ganadera. Solicite al administrador o propietario verificar la unidad de medida en los ajustes de la finca." | No escalar, configuración de parámetros generales de la finca. |
| Indicador de carga en pantalla se mantiene activo de forma prolongada | Demora momentánea al procesar y calcular los promedios de peso en la memoria del teléfono | "Espere unos instantes mientras el dispositivo procesa el historial del ejemplar. Si la pantalla no carga, cierre la aplicación por completo y ábrala de nuevo." | Si la aplicación continúa bloqueada tras reiniciar el teléfono y seleccionar al animal, escalar a soporte técnico detallando modelo del teléfono y versión del sistema operativo. |

### Directivas de Seguridad y Guardrails
- Nunca solicites contraseñas, códigos SMS, pines ni datos bancarios por los canales de atención.
- Los agentes de soporte no deben emitir diagnósticos zootécnicos sobre desnutrición, recomendaciones nutricionales ni prescribir dietas; orienta siempre al productor a consultar con su zootecnista o médico veterinario.
- No alteres ni elimines registros históricos de pesajes corporales en las bases de datos sin la autorización previa y documentada de la administración de la finca ganadera.
- Recuerda al ganadero que todas las curvas y cálculos estadísticos se generan de forma local en el teléfono sin requerir conexión a internet, sincronizándose con la nube cuando el dispositivo cuente con conectividad.
