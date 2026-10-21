---
title: "Tabla de Evolución de Peso"
modulo_id: "pesajes-tabla-evolucion-peso"
nombre_funcionalidad: "Tabla de Historial de Pesajes de Peso Corporal"
categoria: "produccion-hardware"
submodulo: "pesajes"
version_minima_app: "2026.10.1"
fecha_actualizacion: "2026-10-08"
intenciones_y_sinonimos:
  - "donde veo la tabla completa de pesajes de una vaca"
  - "como ver el historial de peso corporal de un animal"
  - "consultar ganancia diaria y ultima ganancia de peso"
  - "como editar o modificar un pesaje corporal anterior"
  - "tabla de pesajes de carne y kilos ganados"
  - "historial cronologico de pesadas de ganado"
---

# Tabla de Historial de Pesajes de Peso Corporal

### Resumen y Alcance Funcional
Permite consultar el historial cronológico y detallado de todas las mediciones de pesaje corporal registradas para un animal en la finca ganadera. La pantalla consolida los indicadores clave del desempeño cárnico en el encabezado superior (peso actual, última ganancia registrada, ganancia diaria promedio acumulada y tipo de dieta suministrada), despliega una tabla interactiva con el detalle de cada medición y permite seleccionar cualquier registro para modificar o corregir sus datos.

- **¿Funciona sin conexión a internet (Modo Offline)?:** Sí.
- **Comportamiento de sincronización:** Las tablas y los cálculos estadísticos se generan al instante con los datos guardados en la memoria local del dispositivo. Cualquier pesaje registrado, corregido o sincronizado en segundo plano mediante Horus actualiza inmediatamente las filas y las métricas del animal.

### Reglas de Negocio y Restricciones
- **Indicadores generales del encabezado superior:**
  - **Actual:** Muestra el valor en kilos o libras del pesaje más reciente registrado para el animal. Si aún no cuenta con pesajes, muestra la ausencia de datos (-).
  - **Última ganancia:** Calcula la diferencia de peso entre las dos mediciones más recientes (peso actual menos el pesaje inmediatamente anterior). Requiere al menos dos pesajes para calcularse; en caso contrario, se muestra sin valor (-).
  - **Ganancia diaria:** Calcula el promedio diario general de ganancia o pérdida de peso del animal a lo largo de su historial registrado. Requiere un mínimo de mediciones para calcular la tasa de crecimiento diario.
  - **Dieta:** Refleja el tipo de alimentación asignado en el pesaje más reciente (por ejemplo: Pastoreo, Estabulado, Semiestabulado, Suplementado u Otro). Si no se seleccionó dieta, muestra el símbolo sin información (-).
- **Columnas de la tabla de pesajes:**
  - **Fecha:** Muestra la fecha en la que se tomó el pesaje, adaptada a la zona horaria del usuario.
  - **Peso:** Refleja la cantidad numérica del peso registrado junto a su unidad de medida (kg o lb).
  - **Ganancia:** Muestra el incremento o decremento de peso obtenido respecto al pesaje cronológicamente anterior. Para el pesaje inicial o más antiguo, al no existir una medición previa de comparación, se muestra sin valor (-).
  - **G. diaria (Ganancia diaria):** Muestra el promedio diario de ganancia de peso acumulado hasta esa fecha específica. En el primer registro del animal no se calcula valor (-).
  - **Dieta:** Presenta el tipo de régimen alimenticio documentado en esa fecha.
- **Interacción y edición de pesajes:**
  - Al presionar cualquier fila de la tabla, la aplicación abre directamente el formulario de registro y edición de pesaje con los datos cargados para su consulta o modificación.
- **Botón flotante para nuevo pesaje:**
  - Si el animal se encuentra activo en la finca y no está bloqueado (no vendido, ni fallecido, ni trasladado), se presenta un botón flotante circular con el ícono de balanza y **(+)** para registrar un nuevo pesaje corporal.
  - Si el animal está bloqueado o dado de baja, el botón flotante permanece oculto.

### Flujo Paso a Paso para el Usuario
- **Ruta de acceso en la aplicación:**
  - Menú inferior **Animales** > Seleccionar el animal > Tarjeta **Producción** > En el apartado **Evolución de peso**, presionar la flecha situada a la derecha del título o el acceso a la tabla.

1. **Lectura de los datos generales del animal (Barra superior):**
   - En la parte superior de la pantalla, verifique el nombre y el sexo del animal en consulta.
2. **Lectura de indicadores de evolución (Encabezado superior):**
   - Revise las métricas consolidadas del animal:
     - **Actual:** Peso corporal registrado en la última medición.
     - **Última ganancia:** Kilos o libras ganados o perdidos frente a la pesada anterior.
     - **Ganancia diaria:** Tasa promedio diaria de ganancia de peso.
     - **Dieta:** Tipo de régimen alimenticio activo en el último pesaje.
3. **Consulta de registros en la tabla:**
   - Explore las filas de la tabla ordenadas de forma cronológica descendente (los pesajes más recientes arriba).
   - Revise las columnas de **Fecha**, **Peso**, **Ganancia**, **G. diaria** y **Dieta**.
4. **Edición o corrección de un pesaje:**
   - Presione directamente sobre la fila del pesaje que requiere corregir.
   - El sistema abrirá el formulario de edición de pesaje con los datos de esa medición.
   - Modifique el peso, la fecha, la dieta o las observaciones pertinentes y presione **Actualizar** para guardar los cambios.
5. **Registro de un nuevo pesaje:**
   - Si desea ingresar una nueva medición sin salir de la consulta, presione el botón flotante circular con el ícono de balanza y **(+)**.
- **Pantalla de llegada tras salir:** Al presionar la flecha de regreso en la barra superior, la app retorna a la pantalla de resumen de **Producción** del animal.

### Matriz de Errores y Soluciones
| Mensaje en la App / Síntoma | Causa Real | Respuesta Sugerida por el Agente | Criterio de Escalamiento Humano |
| :--- | :--- | :--- | :--- |
| La tabla aparece completamente vacía sin registros de peso | El animal fue registrado recientemente y aún no se le han ingresado pesajes de báscula en la finca | "El animal no cuenta con pesajes registrados todavía. Presione el botón circular (+) ubicado abajo para ingresar su primera medición de peso." | No escalar. Guiar al usuario para registrar el primer pesaje. |
| Los campos "Última ganancia" o "Ganancia diaria" muestran una raya (-)" | El animal solo tiene una medición de peso registrada, por lo que no es posible calcular diferencias ni tasas de crecimiento | "Para calcular la ganancia diaria y el incremento de peso se requieren al menos dos pesajes en fechas distintas. Al registrar la segunda pesada, el sistema calculará estos valores automáticamente." | No escalar. Explicar el requerimiento de dos mediciones para el cálculo. |
| No aparece el botón flotante (+) para registrar peso | El animal figura en la finca como inactivo o bloqueado (registrado como vendido, fallecido o transferido) | "El botón para registrar pesajes no se muestra porque el animal se encuentra marcado como inactivo o dado de baja en la finca. Revise el estado del animal en su hoja de vida." | Si el usuario confirma que el animal continúa físicamente en la finca pero la aplicación lo muestra bloqueado, transferir a soporte técnico. |
| La unidad de medida de peso no coincide con la esperada (por ejemplo, muestra libras en vez de kilos) | La finca tiene configurada una unidad de peso distinta en sus parámetros generales | "La unidad de peso (kilos o libras) se toma de la configuración general establecida para su finca. Puede solicitar al administrador cambiar la unidad desde los ajustes de la finca." | No escalar. Orientar al usuario sobre los ajustes de unidades de la finca. |

### Directivas de Seguridad y Guardrails
- NUNCA solicite contraseñas, claves personales o códigos de verificación por WhatsApp ni por ningún canal de atención.
- No emita diagnósticos clínicos veterinarios ni recomendaciones sobre dietas comerciales basadas en los kilos ganados o perdidos por el animal.
- No modifique ni elimine pesajes en la base de datos sin autorización explícita de los administradores de la finca ganadera.
