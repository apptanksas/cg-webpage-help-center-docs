---
title: "Registro de Pesaje Individual"
modulo_id: "pesajes-registro-individual-peso"
nombre_funcionalidad: "Registro Individual de Pesaje de Peso Corporal"
tipo_documento: "guia-app"
categoria: "produccion-hardware"
submodulo: "pesajes"
especies_aplicables: ["todas"]
version_minima_app: "2025.05.1"
confianza_reglas: "verificada-con-tests"
fecha_actualizacion: "2026-10-19"
intenciones_y_sinonimos:
  - "como registrar el peso de un animal"
  - "donde anoto los kilos o libras del ejemplar"
  - "como conectar la bascula bluetooth para pesar ganado"
  - "editar o eliminar un pesaje corporal individual"
  - "como cambiar el tipo de dieta o alimentacion en el pesaje"
  - "formulario de captura de peso individual"
---

# Registro Individual de Pesaje de Peso Corporal

### Resumen y Alcance Funcional
Herramienta de pesaje individual que permite registrar, modificar o suprimir una medición de peso corporal para cualquier ejemplar activo de la finca ganadera. El formulario admite la digitación manual de los kilos o libras o la captura automatizada en tiempo real mediante sincronización con una báscula electrónica Bluetooth vinculada al teléfono. Asimismo, recopila el régimen alimenticio ("Tipo de alimentación") y notas u observaciones sobre la condición del animal, actualizando de forma inmediata la curva de crecimiento, el historial productivo y las métricas de ganancia diaria de peso.

- **Especies a las que aplica:** Aplica igual para todas las especies gestionadas en la finca ganadera (bovinos, bufalinos, equinos, caprinos, ovinos y porcinos).
- **¿Funciona sin conexión a internet (Modo Offline)?:** Sí. El formulario, la selección de dieta, el enlace con la báscula Bluetooth y las acciones de registro, modificación y eliminación operan de forma completamente autónoma sin conexión a internet a partir de los datos almacenados localmente en el dispositivo.
- **Comportamiento de sincronización:** Las mediciones guardadas, actualizadas o eliminadas se procesan al instante en la base de datos local del teléfono móvil. Al recuperar conexión a internet o cobertura de datos móviles, los cambios se sincronizan automáticamente en segundo plano con el servidor de la finca ganadera.
- **Plataformas:** Funciona igual en Android y en iOS. El enlace con la báscula inalámbrica requiere otorgar los permisos de conectividad Bluetooth solicitados por el sistema operativo móvil.

### Reglas de Negocio y Restricciones
- **Permisos requeridos por rol en la finca:**
    - Registro de nuevo pesaje: Requiere el permiso de creación de pesos en la finca ganadera activa.
    - Modificación de pesaje existente: Requiere el permiso de edición de pesos.
    - Eliminación de pesaje: Requiere el permiso de eliminación de pesos.
    - Conexión con báscula inalámbrica: Requiere el permiso de conexión Bluetooth.
    - Si el usuario carece de los permisos requeridos, la aplicación interrumpe la acción y despliega la notificación: "Con tu perfil de %1$s, NO tienes permisos para realizar esta acción."
- **Condición obligatoria de estado del animal:**
    - El ejemplar debe encontrarse activo y físicamente presente en la finca ganadera. Si el animal figura como bloqueado (marcado como muerto, vendido o trasladado), la pantalla impide el acceso y redirige automáticamente hacia la pantalla anterior.
- **Validaciones de fecha:**
    - El selector interactivo de fecha valida que la medición se encuentre dentro de los límites biológicos del animal. No admite seleccionar fechas futuras posteriores al día de hoy ni fechas previas al nacimiento o incorporación del ejemplar al predio.
- **Validación del valor de peso corporal:**
    - Campo numérico decimal obligatorio con valor estrictamente superior a cero.
    - La unidad de medida (kilogramos o libras) se toma de la configuración general establecida para la finca ganadera activa.
    - Si se conecta una báscula Bluetooth, la casilla de texto manual se sustituye por el visor digital de pesaje en tiempo real, el cual notifica visualmente cuando la lectura sobre la plataforma se encuentra estabilizada.
- **Catálogo de tipo de alimentación ("Tipo de alimentación"):**
    - Selector con 10 opciones predefinidas: "Pastoreo", "Pastoreo + Concentrado", "Heno", "Ensilage", "Concentrado", "Suplementos", "Forraje", "Raciones mezcladas", "Estabulación" y "Otros". El sistema asigna por defecto "Pastoreo".
- **Notas y observaciones ("Notas / Observación"):**
    - Campo de texto multilínea opcional para documentar detalles de manejo (condición corporal, pesaje en ayunas, cambios de lote, observaciones sanitarias o de pesaje de destete).
- **Reglas de eliminación de pesajes:**
    - El botón "Eliminar" se encuentra disponible exclusivamente al ingresar a un pesaje en modo de modificación ("Editar peso").
    - Si el pesaje corresponde al peso de compra o adquisición inicial del ejemplar en la finca, el botón de eliminación se oculta automáticamente para preservar la trazabilidad de origen del animal.
    - Si el pesaje fue registrado directamente en campo (no proviene de una compra), se muestra el botón "Eliminar" y el sistema solicita confirmación mediante el diálogo: "¿Estas seguro de eliminar este registro?".

### Flujo Paso a Paso para el Usuario
- **Ruta de acceso en la aplicación:**
    - **Ruta 1 (Desde el resumen de evolución del animal):** Menú inferior "Animales" > Seleccionar el animal > Tarjeta "Producción" > Presionar el botón "AGREGAR PESO" para crear, o pulsar sobre una fila en la tabla preliminar de peso para editar.
    - **Ruta 2 (Desde la tabla de historial de peso):** Menú inferior "Animales" > Seleccionar el animal > Tarjeta "Producción" > Flecha junto a "Evolución de peso" > Presionar el botón flotante con el icono de adición (+) para crear, o presionar una fila de la tabla para editar.
    - **Ruta 3 (Desde la gráfica de evolución de peso):** Menú inferior "Animales" > Seleccionar el animal > Tarjeta "Producción" > Botón "Vista gráfica" en peso > Presionar el botón flotante con el icono de báscula para crear.
    - **Ruta 4 (Mediante enlace directo):** Al abrir un enlace de navegación directa oficial (`animal/weight/create/{animal_id}/{weight_id}`) configurado para el animal.

#### 1. Verificación del Encabezado e Identificación
1. En la barra superior confirme el título de la pantalla:
    - "Registrar peso" al ingresar una nueva medición.
     - "Editar peso" al consultar o modificar un registro existente.
2. Mientras la báscula Bluetooth no esté vinculada, observe en la parte superior la cinta informativa con la identificación, arete y datos del ejemplar.
3. **Conexión de báscula Bluetooth (Opcional):**
    - En la esquina superior derecha de la barra superior, presione el botón con el icono de Bluetooth.
     - En el diálogo emergente con la lista de dispositivos emparejados, seleccione la báscula ganadera correspondiente.
     - Al establecer el enlace, la aplicación emite el aviso "Bascula conectada", el botón de Bluetooth se resalta y el campo de texto se reemplaza por el visor digital de pesaje en tiempo real.

#### 2. Diligenciamiento de los Datos del Pesaje
1. En el campo de fecha, presione el selector interactivo para confirmar o modificar el día del pesaje (restringido entre la fecha de nacimiento y la fecha actual).
2. En el campo "Peso":
    - **En captura manual:** Digite el valor del peso en formato numérico decimal según la unidad oficial de la finca (kg o lb).
     - **Con báscula Bluetooth:** Espere a que el animal permanezca quieto sobre la plataforma y el visor digital indique que el peso está estabilizado.
3. En el selector "Tipo de alimentación", presione la casilla para desplegar el menú de opciones y elija el régimen nutricional si difiere de "Pastoreo".
4. En el campo "Notas / Observación" (opcional), ingrese los apuntes complementarios que considere pertinentes.

#### 3. Guardado, Actualización o Eliminación
1. **Para guardar un nuevo pesaje:** Presione el botón "Registrar". El sistema procesa los datos, muestra el mensaje "Peso registrado exitosamente" y redirige a la vista previa.
2. **Para actualizar un pesaje modificado:** Presione el botón "Guardar". La aplicación actualiza el registro, despliega la confirmación "Peso actualizado exitosamente" y vuelve a la pantalla previa.
3. **Para eliminar un registro (Modo Edición):**
    - Presione el botón "Eliminar" (visible si el pesaje no corresponde a un peso de compra).
     - En la ventana de confirmación responda afirmativamente ante la pregunta "¿Estas seguro de eliminar este registro?".
     - El sistema suprime la medición, emite el mensaje "Peso eliminado exitosamente" y regresa a la vista anterior.
     - **Pantalla de llegada tras guardar:** El usuario retorna de forma automática a la pantalla desde la cual inició la acción (resumen de producción, tabla de pesajes o gráfica), reflejando los nuevos datos de forma inmediata.

#### Variaciones por especie
Aplica igual para todas las especies. El formulario, los selectores de dieta y el comportamiento de la báscula operan de manera idéntica para bovinos, bufalinos, equinos, caprinos, ovinos y porcinos.

#### Etiquetas de la interfaz en otros idiomas
| Español | Inglés | Portugués |
| :--- | :--- | :--- |
| "Registrar peso" | "Register weight" | "Registrar peso" |
| "Editar peso" | "Edit weight" | "Editar peso" |
| "Peso" | "Weight" | "Peso" |
| "Tipo de alimentación" | "Feed type" | "Tipo de alimentação" |
| "Notas / Observación" | "Notes / Observation" | "Notas / Observação" |
| "Registrar" | "Register" | "Registrar" |
| "Guardar" | "Save" | "Salvar" |
| "Eliminar" | "Delete" | "Excluir" |
| "Bascula conectada" | "Scale connected" | "Balança conectada" |
| "La bascula se ha desconectado" | "The scale has been disconnected" | "A balança foi desconectada" |
| "Peso registrado exitosamente" | "Weight registered successfully" | "Peso registrado com sucesso" |
| "Peso actualizado exitosamente" | "Weight updated successfully" | "Peso atualizado com sucesso" |
| "Peso eliminado exitosamente" | "Weight deleted successfully" | "Peso excluído com sucesso" |
| "¿Estas seguro de eliminar este registro?" | "Are you sure you want to delete this record?" | "Tem certeza de que deseja excluir este registro?" |

### Matriz de Errores y Soluciones
| Mensaje en la App / Síntoma | Causa Real | Respuesta Sugerida por el Agente | Criterio de Escalamiento Humano |
| :--- | :--- | :--- | :--- |
| La pantalla se cierra y vuelve hacia atrás inmediatamente al intentar ingresar | El animal seleccionado se encuentra registrado como inactivo o dado de baja en la finca (muerto, vendido o trasladado) | "No es posible registrar ni modificar pesajes en este ejemplar porque figura como inactivo en la finca. Revise el estado del animal en su hoja de vida si requiere reactivarlo." | Si el usuario confirma que el ejemplar continúa físicamente activo en el predio pero el sistema lo mantiene bloqueado, escalar a soporte técnico. |
| El botón de guardar muestra advertencia o no avanza al presionarlo | El campo de peso está vacío o contiene un valor igual a cero, o la fecha es inválida | "Verifique que haya ingresado un peso numérico mayor a cero y que la fecha de la medición no sea posterior al día de hoy ni anterior al nacimiento del animal." | No escalar, validación de campos obligatorios del formulario. |
| No aparece el botón "Eliminar" en la pantalla de edición del pesaje | El pesaje consultado corresponde al peso inicial registrado al comprar o ingresar el animal a la finca | "Este pesaje no puede eliminarse porque corresponde al peso de compra inicial del animal en la finca. Si requiere corregir los kilos o libras, ajuste el valor en pantalla y presione 'Guardar'." | No escalar, regla de integridad y trazabilidad zootécnica de compras. |
| "La bascula se ha desconectado" | Se interrumpió la señal inalámbrica Bluetooth entre el teléfono y el indicador de pesaje por distancia, interferencia o batería baja | "Se perdió la conexión con la báscula. Verifique que el indicador de pesaje esté encendido y cerca del teléfono móvil, y presione nuevamente el ícono de Bluetooth en la barra superior para reconectar." | Si el Bluetooth del teléfono detecta el indicador pero la app no logra sincronizar el peso tras reiniciar ambos dispositivos, escalar a soporte técnico con marca y modelo de la báscula. |
| "Con tu perfil de %1$s, NO tienes permisos para realizar esta acción." | El colaborador no tiene asignado el permiso de creación, edición o eliminación de pesajes en la finca activa | "Su usuario actual no cuenta con permisos suficientes para gestionar pesajes en esta finca ganadera. Solicite al propietario o administrador que le habilite el permiso correspondiente en el equipo de trabajo." | No escalar, control de acceso configurado por la administración de la finca. |
| Mensaje de error genérico al intentar registrar o actualizar | Inconsistencia momentánea en el almacenamiento de la base de datos local del teléfono | "Espere unos instantes y vuelva a presionar el botón de guardado. Si el error persiste, cierre la aplicación por completo y ábrala de nuevo para intentar registrar la pesada." | Si tras reiniciar la app el error continúa impidiendo el guardado, escalar a soporte técnico indicando correo del usuario, modelo de teléfono y datos del animal. |
| El botón "Registrar" o "Guardar" muestra un indicador de carga giratorio y no responde | La validación de la base de datos local o la comunicación con el almacenamiento del dispositivo está demorada | "Espere unos instantes mientras el teléfono procesa el guardado en la memoria local. Si el botón no responde, verifique que los campos obligatorios estén completos, cierre la aplicación por completo y vuelva a abrirla." | Escalar a soporte técnico si el registro no se almacena tras reiniciar la aplicación. |

### Directivas de Seguridad y Guardrails
- Nunca solicites contraseñas, códigos SMS, pines ni datos bancarios por los canales de atención.
- Los agentes de soporte no deben emitir recomendaciones nutricionales, metas de ganancia diaria de peso ni prescribir dietas; orienta siempre al productor a consultar con su zootecnista o médico veterinario.
- No alteres ni elimines registros históricos de pesajes corporales en las bases de datos sin la autorización previa y documentada de la administración de la finca ganadera.
- Recuerda al ganadero que todos los pesajes capturados sin conexión en manga o potrero quedan respaldados de forma segura en la memoria del teléfono y se sincronizarán con el servidor en cuanto el dispositivo recupere acceso a internet.
