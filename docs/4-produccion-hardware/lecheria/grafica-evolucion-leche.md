---
title: "Gráfica de Producción de Leche"
modulo_id: "lecheria-grafica-produccion-leche"
nombre_funcionalidad: "Gráfica de Evolución de Producción de Leche"
tipo_documento: "guia-app"
categoria: "produccion-hardware"
submodulo: "lecheria"
especies_aplicables: ["bovinos", "bufalinos", "caprinos"]
version_minima_app: "2025.05.1"
confianza_reglas: "verificada-con-tests"
fecha_actualizacion: "2026-10-19"
intenciones_y_sinonimos:
  - "como ver la curva de lactancia de una vaca"
  - "grafica de produccion de leche individual"
  - "ver la evolucion lechera de un animal"
  - "donde veo el promedio diario y pico de leche"
  - "por que no me aparece el boton de vista grafica en leche"
  - "grafico de leche por periodos de lactancia"
---

# Gráfica de Evolución de Producción de Leche

### Resumen y Alcance Funcional
Módulo visual de análisis lechero individual que permite consultar de forma gráfica la curva de producción de leche de una hembra a lo largo del tiempo, facilitando el seguimiento zootécnico del comportamiento productivo, la persistencia láctea y los períodos de secado y lactancia en la finca ganadera. En el encabezado superior se consolidan los tres indicadores globales de rendimiento ("Promedio diario", "Producción máxima" y "Producción total"), mientras que en el cuerpo de la pantalla se despliega la curva continua de mediciones o se desglosan gráficos independientes para cada ciclo de lactancia cuando el animal registra múltiples partos y eventos de secado.

- **Especies a las que aplica:** Exclusivamente a hembras de especies con aptitud lechera registradas en la finca: bovinos, bufalinos y caprinos. Las especies sin control lechero (equinos, porcinos y ovinos) no disponen de esta visualización.
- **¿Funciona sin conexión a internet (Modo Offline)?:** Sí. El cálculo estadístico, la segmentación de ciclos de lactancia y el trazado de las curvas en pantalla operan completamente sin cobertura celular ni conexión Wi-Fi a partir de las mediciones almacenadas localmente.
- **Comportamiento de sincronización:** Las gráficas y valores estadísticos se generan de forma instantánea a partir de las mediciones de pesaje guardadas en la base de datos local del dispositivo móvil. Al recibir nuevos pesajes o sincronizar cambios en segundo plano con el servidor de la finca ganadera, los gráficos se recalculan y actualizan automáticamente.
- **Plataformas:** Interfaz idéntica y paridad total de funciones en Android y en iOS.

### Reglas de Negocio y Restricciones
- **Mínimo de registros requeridos para graficar:**
  - Se requiere un mínimo de 2 registros de pesaje de leche en fechas distintas para trazar la curva en el gráfico.
  - Si el animal cuenta con menos de 2 fechas de pesajes (0 o 1 medición), el botón "Vista gráfica" no se muestra en la pantalla de evolución del animal.
  - Si se intenta ingresar directamente a la pantalla con menos de 2 pesajes registrados, la aplicación protege la interfaz y regresa de inmediato a la vista previa sin mostrar un gráfico vacío.
- **Consolidación diaria de pesajes:**
  - Si en una misma fecha existen pesajes en turnos divididos (por ejemplo, mañana y tarde), el sistema suma automáticamente las cantidades de ambos turnos para presentar la producción total correspondiente a ese día como un único punto en la gráfica.
- **Segmentación por períodos de lactancia:**
  - El sistema calcula los períodos de lactancia considerando las fechas de parto de las crías de la hembra y los tratamientos de secado registrados en su historial sanitario.
  - Cuando la hembra registra más de un ciclo de lactancia, la pantalla presenta gráficos independientes identificados con el encabezado de cada período (por ejemplo, "Lactancia 1", "Lactancia 2", etc.).
  - Si la hembra tiene un único ciclo productivo o no registra eventos de secado ni nuevos partos, se despliega una sola gráfica general.
- **Indicadores estadísticos del encabezado:**
  - **"Promedio diario":** Media aritmética de la cantidad de leche producida por día con registro en el animal.
  - **"Producción máxima":** Medición diaria más alta alcanzada por el animal en todo su historial lechero registrado.
  - **"Producción total":** Suma acumulada total de toda la leche registrada para el animal en la finca.
- **Unidad de medida:**
  - Las cantidades en el eje vertical (eje Y) y en las estadísticas se muestran de forma automática con la unidad oficial configurada para la leche en la finca ganadera (litros, galones o kilogramos).
- **Acceso rápido al registro de pesaje:**
  - Si el animal se encuentra activo en la finca (no dado de baja, ni vendido, ni fallecido), la pantalla exhibe un botón flotante con el icono de recipiente de leche para acceder directamente al formulario de registro individual de pesaje.

### Flujo Paso a Paso para el Usuario
- **Ruta de acceso en la aplicación:**
  - **Ruta principal (Desde el resumen del animal):** Menú inferior "Animales" > Seleccionar la hembra > Pestaña o sección "Producción" > Presionar "Ver detalles de producción" (o la tarjeta de producción) > En el bloque "Producción de leche", ubicar la sección del promedio y presionar el botón "Vista gráfica".

#### 1. Verificación de Encabezado y Datos del Animal
1. En la barra superior confirme la identificación del animal (arete y nombre) en la tarjeta informativa derecha.
2. En la parte superior visualice el encabezado "Producción de leche" con los tres indicadores globales de la hembra:
   - **"Promedio diario":** Rendimiento medio por día de ordeño registrado.
   - **"Producción máxima":** Pico máximo diario de leche alcanzado.
   - **"Producción total":** Volumen acumulado total en la historia del animal.

#### 2. Interpretación de la Curva de Producción
1. Deslice verticalmente para visualizar la evolución temporal:
   - **Eje horizontal (eje X):** Cronología con las fechas de los pesajes.
   - **Eje vertical (eje Y):** Volumen de producción rotulado con la unidad de medida oficial de la finca.
2. **Si el animal cuenta con múltiples lactancias:** Cada período se presenta con su título respectivo ("Lactancia 1", "Lactancia 2", etc.) y su gráfico delimitado entre el parto y la fecha de secado.
3. **Si el animal tiene un solo período:** Se muestra una sola gráfica que abarca el historial completo de pesajes disponibles.

#### 3. Registro Rápido de Nuevo Pesaje (Opcional)
1. Para asentar una nueva medición de ordeño para este animal, presione el botón flotante circular con el icono de recipiente de leche ubicado en la esquina inferior.
2. El sistema abrirá de inmediato la pantalla para registrar el pesaje de leche de la hembra.
- **Pantalla de llegada tras salir:** Al presionar la flecha de regreso en la barra superior, la aplicación retorna a la pantalla de evolución y resumen de producción del animal.

#### Variaciones por especie
- **Especies lecheras:** La funcionalidad está habilitada para hembras de bovinos (vacas), bufalinos (búfalas) y caprinos (cabras).
- **Límites de lactancia:** La duración teórica del ciclo lechero predeterminado se ajusta según los parámetros biológicos de la especie si no media un tratamiento de secado previo.
- **Especies no compatibles:** En équidos, cerdas y ovejas (salvo configuraciones lecheras específicas), la tarjeta de producción lechera y el acceso a la gráfica no están disponibles.

#### Etiquetas de la interfaz en otros idiomas
| Español | Inglés | Portugués |
| :--- | :--- | :--- |
| "Producción de leche" | "Milk production" | "Produção de leite" |
| "Vista gráfica" | "Graph View" | "Visualização gráfica" |
| "Promedio diario" | "Daily Average" | "Média Diária" |
| "Producción máxima" | "Maximum Production" | "Produção Máxima" |
| "Producción total" | "Total Production" | "Produção Total" |
| "Lactancia %1$d" | "Lactation %1$d" | "Lactação %1$d" |

### Matriz de Errores y Soluciones
| Mensaje en la App / Síntoma | Causa Real | Respuesta Sugerida por el Agente | Criterio de Escalamiento Humano |
| :--- | :--- | :--- | :--- |
| El botón "Vista gráfica" no aparece en la pantalla de evolución de leche | La hembra cuenta con menos de 2 pesajes de leche registrados en fechas distintas | "Para generar la gráfica de producción se requieren al menos 2 pesajes en fechas diferentes. Registre un nuevo pesaje para que el botón 'Vista gráfica' aparezca automáticamente." | No escalar, regla de validación de puntos mínimos para trazar la gráfica. |
| La pantalla se abre y regresa de inmediato a la vista anterior | El historial local tiene menos de 2 fechas de pesajes válidas al procesar los datos | "La gráfica de leche necesita como mínimo 2 días con mediciones para dibujar la línea temporal. Si recientemente eliminó pesajes, registre nuevas mediciones para consultar la curva." | Si el usuario comprueba que en la tabla de pesajes hay 2 o más fechas registradas y la pantalla continúa cerrándose, escalar a soporte técnico indicando el arete del animal. |
| No aparece el botón flotante con el icono de leche para agregar pesajes | El animal se encuentra inactivo o bloqueado en la finca (registrado como fallecido, vendido o trasladado) | "El botón de registro rápido no se muestra porque el animal figura como inactivo en la finca. Verifique el estado del animal en su hoja de vida si requiere reactivarlo." | Si el ganadero confirma que el ejemplar continúa activo en ordeño en la finca pero la aplicación lo detecta inactivo, escalar a soporte técnico. |
| La unidad de medida en el eje vertical no coincide con la esperada | La finca ganadera tiene configurada una unidad de volumen o masa lechera distinta en sus ajustes de predio | "El gráfico adopta de forma automática la unidad de leche configurada en los ajustes generales de la finca. Solicite al administrador de la finca verificar la unidad de producción desde la configuración del predio." | No escalar, configuración de unidades de medida del predio. |

### Directivas de Seguridad y Guardrails
- Nunca solicites contraseñas, códigos SMS, pines ni datos bancarios por los canales de atención.
- Los agentes de soporte no deben interpretar caídas en la curva de lactancia como diagnósticos veterinarios ni recetar promotores de leche o raciones alimenticias; orienta siempre al productor a consultar con su médico veterinario o zootecnista.
- No alteres ni elimines registros históricos de pesajes de leche directamente en las bases de datos sin la autorización previa y documentada del propietario de la finca ganadera.
- Recuerda al usuario que todos los pesajes y gráficos se mantienen respaldados localmente en su teléfono y se sincronizan de forma automática con la nube al disponer de conexión a internet.
