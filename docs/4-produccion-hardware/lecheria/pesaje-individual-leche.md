---
title: "Registro Individual de Pesaje de Leche"
modulo_id: "lecheria-registro-pesaje-leche"
nombre_funcionalidad: "Registro Individual de Producción y Pesaje de Leche"
tipo_documento: "guia-app"
categoria: "produccion-hardware"
submodulo: "lecheria"
especies_aplicables: ["bovinos", "bufalinos", "caprinos"]
version_minima_app: "2025.05.1"
confianza_reglas: "verificada-con-tests"
fecha_actualizacion: "2026-10-19"
intenciones_y_sinonimos:
  - "como registrar el pesaje de leche de una vaca"
  - "formulario de produccion de leche por animal"
  - "editar pesaje de leche individual"
  - "ingresar litros de leche de una vaca o cabra"
  - "anotar pesaje de manana y tarde de leche"
  - "registrar concentrado y leche de un animal"
---

# Registro Individual de Producción y Pesaje de Leche

### Resumen y Alcance Funcional
Módulo de captura individual que permite asentar, actualizar o eliminar las mediciones de rendimiento lechero y consumo de suplemento concentrado para un animal hembra en una fecha específica. El formulario admite el registro desglosado por turnos u horarios de ordeño ("Mañana", "Tarde", o ambos simultáneamente en una sola operación), vinculando opcionalmente el lote o "Hato de ordeño" y el "Potrero" donde pastoreaba el ejemplar. Los datos alimentan automáticamente la curva de lactancia individual, la producción acumulada de la campaña y las estadísticas generales de la lechería en la finca ganadera.

- **Especies a las que aplica:** Hembras lecheras o de doble propósito de las especies bovina, bufalina y caprina.
- **¿Funciona sin conexión a internet (Modo Offline)?:** Sí. El diligenciamiento del formulario, la selección de fechas, turnos, hatos, potreros y las operaciones de guardado, actualización y borrado operan con total normalidad sin cobertura celular ni conexión Wi-Fi.
- **Comportamiento de sincronización:** Las mediciones se almacenan de inmediato en la base de datos local del dispositivo móvil. En cuanto el teléfono detecta señal o conexión a internet, los registros se transmiten automáticamente en segundo plano al servidor de la finca ganadera.
- **Plataformas:** Interfaz idéntica y paridad de funciones en Android y en iOS.

### Reglas de Negocio y Restricciones
- **Permisos requeridos por rol en la finca:**
    - Registro de nuevo pesaje: Requiere el permiso de creación de registros de ordeño en la finca ganadera activa.
    - Modificación de pesaje existente: Requiere el permiso de edición de registros de ordeño.
    - Eliminación de pesaje: Requiere el permiso de eliminación de registros de ordeño.
    - Si el usuario carece del permiso correspondiente, el sistema detiene el proceso y muestra la notificación: "Con tu perfil de %1$s, NO tienes permisos para realizar esta acción."
- **Restricción estricta por estado del animal:**
    - El animal debe encontrarse activo y presente en la finca ganadera. Si el ejemplar está registrado como muerto, vendido o trasladado fuera del predio, la pantalla deniega el acceso y regresa automáticamente a la vista previa.
- **Validaciones de fecha:**
    - El selector "Fecha" restringe la selección según la vida productiva del ejemplar: no es posible elegir fechas futuras posteriores al día de hoy ni fechas anteriores al nacimiento o fecha de ingreso del animal a la finca.
- **Turnos y períodos del día:**
    - Selector "Periodo del día" con tres opciones oficiales: "Mañana", "Tarde", y "Mañana y Tarde".
    - Al seleccionar "Mañana y Tarde", el formulario despliega de forma dinámica dos secciones independientes bajo "Datos de producción", permitiendo ingresar las cantidades de cada jornada por separado.
    - **Bloqueo del período en modo edición:** Al consultar un pesaje existente para modificarlo ("Editar Leche"), el selector "Periodo del día" permanece deshabilitado para resguardar la consistencia cronológica del turno originalmente evaluado.
- **Prevención de registros duplicados:**
    - No se permite asentar más de una medición para un mismo animal en la misma fecha y turno. Si ya existe un registro previo para el período seleccionado, el sistema bloquea el guardado y emite la alerta: "Ya existe un registro de producción de leche para este animal en la fecha seleccionada con el periodo del día seleccionado."
- **Validación de cantidades numéricas y unidades de medida:**
    - Los campos "Concentrado" y "Leche" requieren números decimales positivos válidos.
    - La unidad de medida de volumen o peso para "Leche" (litros, kilogramos o galones) y de masa para "Concentrado" (kilogramos o libras) se toma automáticamente de la configuración oficial de la finca ganadera activa y se exhibe en el sufijo del campo.
- **Datos complementarios (Opcionales):**
    - "Hato de ordeño" y "Potrero" son selectores opcionales para asociar la ubicación zootécnica de la vaca durante el ordeño.
- **Reglas de eliminación de registros:**
    - La opción de borrado solo está habilitada al acceder en modo de edición ("Editar Leche").
    - Al presionar eliminar, el sistema solicita confirmación del usuario para proceder.

### Flujo Paso a Paso para el Usuario
- **Ruta de acceso en la aplicación:**
    - **Ruta 1 (Desde el módulo de animales):** Menú inferior "Animales" > Seleccionar la hembra > Pestaña o sección "Producción" > "Evolución de leche" > Presionar el botón "AGREGAR LECHE".
    - **Ruta 2 (Desde la pantalla de producción):** selecciona la flecha en la sección "Producción de leche" > Presionar el botón flotante de adición (+) para crear, o tocar una fila específica para editarla.
    - **Ruta 3 (Desde la gráfica de evolución de leche):** Pantalla de "producción" > "Vista gráfica" > Presionar el botón flotante con ícono de recipiente de leche.
    - **Ruta 4 (Desde las estadísticas generales de leche de la finca):** Menú inferior > "Producción" > Pestaña "Producción de leche" > ve al boton flotante con el icono de botella de leche y icono "+" selecciona la hembra.

#### 1. Verificación del Encabezado e Identificación
1. En la barra superior confirme el título:
    - "Registrar Leche" si va a ingresar una nueva medición.
    - "Editar Leche" si va a modificar un registro previo.
2. En la parte superior de la pantalla se exhibe la tarjeta con los datos y el código identificador de la hembra.

#### 2. Selección de Fecha y Turno
1. En el campo "Fecha", presione el selector para verificar o indicar el día del pesaje (no admite fechas futuras ni previas al nacimiento).
2. En el selector "Periodo del día", presione para elegir entre "Mañana", "Tarde", o "Mañana y Tarde" (disponible únicamente al registrar un nuevo ordeño).

#### 3. Ingreso de Datos de Producción
1. Bajo el encabezado "Datos de producción", para el turno o turnos seleccionados:
    - En el campo "Concentrado", digite la cantidad de suplemento consumido en la unidad configurada para la finca.
    - En el campo "Leche", digite el volumen o peso de leche obtenido en el ordeño.

#### 4. Datos Complementarios (Opcionales)
1. Bajo el encabezado "Datos complementarios":
    - En "Hato de ordeño", seleccione el grupo o lote correspondiente si aplica.
    - En "Potrero", seleccione el potrero en el que se encontraba la hembra.

#### 5. Guardado, Modificación o Eliminación
1. **Para guardar un nuevo pesaje:** Presione el botón "Registrar". El sistema valida los datos, emite la confirmación "Ordeño registrado exitosamente" y regresa a la pantalla previa.
2. **Para actualizar un pesaje existente:** Presione el botón "Actualizar". La aplicación guarda los cambios, emite la notificación "Ordeño actualizado exitosamente" y vuelve a la vista anterior.
3. **Para eliminar un pesaje (Modo Edición):** Presione el botón de eliminación, confirme la acción y el sistema emite la notificación "Ordeño eliminado exitosamente", regresando a la vista previa.
- **Pantalla de llegada tras procesar:** El usuario regresa de forma automática a la pantalla anterior, observando los valores reflejados de inmediato en la tabla de pesajes y en la gráfica de producción de leche.

#### Variaciones por especie
- **Bovinos, Bufalinos y Caprinos:** La funcionalidad aplica a las hembras reproductoras o en lactancia de estas especies.
- **Parámetros zootécnicos:** Las unidades de medida (litros, kilos, libras o galones) se configuran a nivel de la finca ganadera y se aplican consistentemente en todas las especies evaluadas.
- **Especies no productoras de leche:** La pantalla no está disponible para animales machos ni para especies no lecheras como equinos o porcinos.

#### Etiquetas de la interfaz en otros idiomas
| Español | Inglés | Portugués |
| :--- | :--- | :--- |
| "Registrar Leche" | "Register Milk" | "Registrar Leite" |
| "Editar Leche" | "Edit Milk" | "Editar Leite" |
| "Periodo del día" | "Period of the day" | "Período do dia" |
| "Datos de producción" | "Production data" | "Dados de produção" |
| "Concentrado" | "Concentrate" | "Concentrado" |
| "Leche" | "Milk" | "Leite" |
| "Datos complementarios" | "Additional data" | "Dados adicionais" |
| "Hato de ordeño" | "Herd" | "Rebanho de Ordenha" |
| "Potrero" | "Pasture" | "Pasto" |
| "Mañana" | "Morning" | "Manhã" |
| "Tarde" | "Afternoon" | "Tarde" |
| "Mañana y Tarde" | "Morning and Afternoon" | "Manhã e Tarde" |
| "Registrar" | "Register" | "Registrar" |
| "Actualizar" | "Update" | "Atualizar" |
| "Ordeño registrado exitosamente" | "Milking recorded successfully" | "Ordenha registrada com sucesso" |
| "Ordeño actualizado exitosamente" | "Milking updated successfully" | "Ordenha atualizada com sucesso" |
| "Ordeño eliminado exitosamente" | "Milking deleted successfully" | "Ordenha excluída com sucesso" |
| "Ya existe un registro de producción de leche para este animal en la fecha seleccionada con el periodo del día seleccionado." | "A milk production record already exists for this animal on the selected date with the selected period of the day." | "Já existe um registro de produção de leite para este animal na data selecionada com o período do dia selecionado." |

### Matriz de Errores y Soluciones
| Mensaje en la App / Síntoma | Causa Real | Respuesta Sugerida por el Agente | Criterio de Escalamiento Humano |
| :--- | :--- | :--- | :--- |
| "Ya existe un registro de producción de leche para este animal en la fecha seleccionada con el periodo del día seleccionado." | Ya se encuentra registrado un pesaje de leche para ese ejemplar en la misma fecha y turno (mañana o tarde) | "Este animal ya cuenta con una medición registrada para esa fecha y turno. Si necesita corregir los valores de leche o concentrado, ingrese a la tabla de pesajes de la hembra y seleccione el registro para editarlo." | No escalar, validación de prevención de duplicados zootécnicos. |
| La pantalla se cierra y vuelve hacia atrás inmediatamente al intentar ingresar | La hembra seleccionada se encuentra registrada como inactiva o dada de baja en la finca (muerta, vendida o trasladada) | "No es posible registrar ni modificar mediciones de leche en este ejemplar porque figura como inactivo o dado de baja en la finca. Revise el estado del animal en su hoja de vida." | Si el usuario confirma que el animal continúa activo y produciendo en el rebaño pero la app lo bloquea, escalar a soporte técnico indicando la identificación del animal. |
| El botón de guardar muestra advertencia o no avanza al presionarlo | Los campos de cantidad de leche o concentrado están vacíos o contienen valores no numéricos | "Asegúrese de ingresar valores numéricos válidos en los campos de concentrado y leche para cada turno seleccionado antes de presionar el botón de registro." | No escalar, validación de campos obligatorios del formulario. |
| El selector "Periodo del día" aparece bloqueado en color gris y no permite cambiar el turno | Comportamiento por diseño en modo de edición: no se permite alterar el turno original del registro para preservar la trazabilidad | "Cuando se edita un pesaje de leche ya existente, el turno del día permanece bloqueado para proteger la coherencia de los datos históricos. Si registró el pesaje en el turno equivocado, elimine el registro y créelo nuevamente con el turno correcto." | No escalar, comportamiento esperado de integridad histórica. |
| "Con tu perfil de %1$s, NO tienes permisos para realizar esta acción." | El colaborador no tiene asignado el permiso de creación, edición o eliminación de registros de ordeño en la finca ganadera | "Su usuario actual no cuenta con permisos suficientes para gestionar pesajes de leche en esta finca. Solicite al propietario o administrador de la finca que le habilite los permisos correspondientes desde la administración de colaboradores." | No escalar, directiva de control de acceso configurada por el propietario del predio. |
| Mensaje de error genérico al intentar registrar o actualizar | Inconsistencia momentánea en el almacenamiento de la base de datos local del teléfono | "Espere unos instantes y vuelva a presionar el botón de guardado. Si el inconveniente persiste, cierre la aplicación por completo y ábrala de nuevo para registrar el ordeño." | Si tras reiniciar la aplicación el error continúa impidiendo el guardado, escalar a soporte técnico indicando correo del usuario, modelo de teléfono y datos del animal. |

### Directivas de Seguridad y Guardrails
- NUNCA solicites contraseñas, claves personales, códigos de verificación por SMS ni datos bancarios por los canales de soporte.
- Los agentes de soporte no deben emitir recomendaciones zootécnicas o nutricionales sobre raciones de concentrado, promotores de lactancia ni medicamentos para el ordeño; orienta siempre al productor a consultar con su médico veterinario o zootecnista.
- No alteres ni elimines registros históricos de pesajes de leche directamente en bases de datos sin la autorización expresa y documentada del propietario de la finca ganadera.
- Recuerda al ganadero que todos los pesajes capturados sin conexión en sala de ordeño quedan respaldados en la base de datos local del teléfono móvil y se sincronizarán automáticamente con la nube en cuanto el dispositivo recupere conexión a internet.
