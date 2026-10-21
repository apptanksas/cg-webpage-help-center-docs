---
title: "Venta de Ganado"
modulo_id: "animales-venta-ganado"
nombre_funcionalidad: "Registro y Administración de Venta de Ganado"
categoria: "inventario-trazabilidad"
submodulo: "animales"
version_minima_app: "2026.10.1"
fecha_actualizacion: "2026-10-09"
intenciones_y_sinonimos:
  - "como registrar la venta de animales en la app"
  - "donde vendo vacas o novillos de mi finca"
  - "como transferir animales vendidos a otro usuario de control ganadero"
  - "por que no me deja vender animales a mi propia finca"
  - "como poner un precio personalizado a un animal en una venta"
  - "error debes agregar al menos un animal al registrar venta"
---

# Registro y Administración de Venta de Ganado

### Resumen y Alcance Funcional
Asistente especializado en dos pasos para asentar la salida comercial de animales del inventario ganadero de la finca activa. Permite ingresar las condiciones comerciales de la negociación, vincular información logística de despacho, comprador y transporte, seleccionar los ejemplares comercializados y calcular el importe total en función del último peso registrado de cada cabeza o mediante precios asignados de forma personalizada.

Adicionalmente, si el comprador también es usuario de Control Ganadero, la pantalla permite activar una solicitud automática de traslado digital para transferir los animales vendidos de manera directa a la finca destino del comprador sin que este tenga que digitarlos nuevamente.

- **¿Funciona sin conexión a internet (Modo Offline)?:** No. El registro y la modificación de ventas pecuarias requieren conexión a internet activa obligatoria, debido a que el sistema debe validar en tiempo real los permisos del usuario, consultar las fincas receptoras en caso de traslado y forzar la sincronización con el servidor central para actualizar el inventario ganadero.
- **Comportamiento de sincronización:** La operación se procesa de forma directa con los servidores de Control Ganadero. Si se habilita la opción de traslado entre usuarios, el sistema ejecuta una sincronización forzada previa de los datos de la finca y genera la solicitud formal de traslado que el nuevo propietario deberá aceptar en su cuenta.

### Reglas de Negocio y Restricciones
- **Estructura en dos pasos (Asistente guiado):**
  - **Paso 1 (Datos de la venta):** Recopila la fecha del acuerdo, fecha estimada de despacho, datos del comprador, ubicación de entrega, empresa y guía de transporte, chofer, especie de animal comercializado, moneda, precio base por unidad de peso (según la unidad configurada en la finca: kilogramos o libras) y observaciones generales. Asimismo, alberga la opción de traslado a otra cuenta.
  - **Paso 2 (Animales vendidos):** Requiere la selección obligatoria de al menos un animal del inventario (`Debes agregar al menos un animal`).
- **Restricción de especie por venta:**
  - Cada venta se efectúa para una única especie pecuaria (bovinos, bufalinos, equinos, etc.).
  - En el selector de animales del paso 2, solo se muestran los animales que pertenezcan a la especie seleccionada en el paso 1, que se encuentren físicamente en la finca activa y cuyo estado no sea fallecido.
- **Cálculo de importes y precios personalizados:**
  - Por defecto, la aplicación toma el último peso registrado para cada ejemplar y multiplica dicho peso por el precio unitario por unidad de medida definido en el paso 1.
  - Si un animal no posee un pesaje previo en su historial, su peso inicial se toma como cero en la tabla.
  - El ganadero puede mantener presionado cualquier animal en la tabla para abrir la ventana modal **Precio personalizado** y fijar un monto manual directo, el cual sustituye el cálculo automático por peso.
- **Traslado de animales a otro usuario de Control Ganadero:**
  - El usuario puede activar la casilla de verificación con interruptor titulada *¿Quieres trasladar los animales a otro usuario de Control Ganadero?* (disponible si su rol cuenta con permisos para crear traslados).
  - Al ingresar el correo electrónico del comprador, debe presionar el botón **Validar**. El sistema busca en el servidor las fincas asociadas a dicho usuario y las despliega en un menú de selección.
  - **Restricción de auto-traslado:** Si el usuario intenta seleccionar una finca que pertenezca a su propia cuenta, el sistema bloquea la acción y emite el mensaje: *"Lo sentimos, no puedes vender animales a una finca vinculada a tu propia cuenta. Utiliza la opción de 'Trasladar animales' para hacer el traslado entre tus propias fincas."*
- **Bloqueos en edición y eliminación:**
  - Si una venta ya tiene un traslado relacionado hacia otro usuario de la plataforma, el sistema bloquea la eliminación o modificación de los animales de la lista en el paso 2.
  - Del mismo modo, no se permite eliminar el registro de la venta completa si ya existe una transferencia vinculada en curso o aceptada, mostrando el mensaje: *"No se puede eliminar este registro de venta porque tiene una transferencia a otro usuario de Control Ganadero relacionada."*

### Flujo Paso a Paso para el Usuario
- **Ruta de acceso en la aplicación:**
  - *Opción 1 (Menú central de acciones rápidas):* En la pantalla principal de finca > Pulsar el botón flotante con el icono de casa con el signo **(+)** > Pulsar sobre **Venta de ganado**.
  - *Opción 2 (Desde estadísticas de carne):* Menú inferior de la pantalla presione producción > Producción de carne > Tabla de ventas de animales > Pulsar el botón flotante de **+** de nueva venta o seleccionar una venta existente para editar.

#### Paso 1: Diligenciamiento de Datos Comerciales y Logísticos
1. En la barra superior, verifique el título **Venta de ganado** (o **Editar venta** si está modificando un registro previo).
2. Configure las fechas iniciales:
   - **Fecha de venta:** Día en que se pactó la transacción comercial.
   - **Fecha de despacho:** Día programado para la entrega o salida física de los animales del predio.
3. Despliegue las secciones colapsables opcionales según requiera registrar información detallada:
   - **Comprador:** Ingrese el **Nombre/Empresa** y el **Teléfono** de contacto.
   - **Información de destino:** Seleccione el **País**, **Región / Departamento** y **Ciudad**, e ingrese la **Nombre finca/Dirección** de entrega.
   - **Información de transporte:** Ingrese la **Empresa transportadora**, el **Número de transporte** (guía con un máximo de 50 caracteres), la **Placa del vehículo**, el **Nombre del chofer** y el **Teléfono del chofer**.
4. En el bloque **Datos generales**:
   - **Tipo de animal:** Seleccione la especie ganadera que comercializa (bovinos, equinos, etc.). Si está editando una venta previamente guardada, este campo no puede alterarse.
   - **Moneda:** Elija el tipo de divisa en que se liquida la venta.
   - **Precio por unidad:** Digite el precio unitario por cada kilogramo o libra de peso según la unidad configurada en su predio.
   - **Notas y observaciones:** Escriba notas adicionales o acuerdos comerciales relevantes.
5. *(Opcional)* Si el comprador utilizará Control Ganadero para recibir el ganado:
   - Active el interruptor **¿Quieres trasladar los animales a otro usuario de Control Ganadero?**.
   - En el campo **Correo electrónico**, digite la dirección de correo con la que el comprador está registrado en la app.
   - Presione el botón **Validar**. Una vez confirmado el usuario, elija la finca destino en el campo desplegable **Seleccionar finca**.
6. Deslice hacia el segundo paso del asistente o presione avanzar.

#### Paso 2: Selección de Animales y Asignación de Precios
1. La pantalla presenta el bloque de advertencia: *"Mantén seleccionado un animal de la tabla si quieres asignarle un precio de venta personalizado."*
2. Presione el botón **Seleccionar animales**.
3. En la ventana modal de selección múltiple, marque las casillas de los animales que integran el lote vendido y confirme la selección.
4. Revise el resumen superior:
   - **Cantidad de animales:** Muestra el número total de cabezas seleccionadas.
   - **Total:** Monto económico consolidado en la moneda elegida.
5. En la tabla de animales vendidos, revise las columnas:
   - **Código:** Arete o código identificador del animal.
   - **Peso:** Último pesaje oficial del ejemplar en la finca.
   - **Precio:** Valor monetario computado para dicho animal.
6. **Ajuste de precio individual (opcional):**
   - Si acordó un precio fijo para un ejemplar en particular (independiente de su peso), mantenga presionado el registro del animal en la tabla.
   - En la ventana modal **Precio personalizado**, digite el valor acordado y presione confirmar. El total general de la venta se actualizará al instante.
7. **Eliminar animales del lote:** Si agregó un animal por error, presione el icono de eliminar (papelera roja) al final de su fila en la tabla.
8. Presione el botón **Registrar** al pie de la pantalla para guardar la venta.

- **Pantalla de llegada tras guardar:** El sistema registra la venta y regresa a la pantalla anterior del historial o estadísticas.

### Matriz de Errores y Soluciones
| Mensaje en la App / Síntoma | Causa Real | Respuesta Sugerida por el Agente | Criterio de Escalamiento Humano |
| :--- | :--- | :--- | :--- |
| "Debes agregar al menos un animal" | Se intentó presionar el botón de registro en el paso 2 sin haber seleccionado ningún ejemplar del inventario | "Para registrar una venta de ganado es obligatorio incluir al menos un animal. Por favor presione el botón 'Seleccionar animales' en el paso 2, marque los ejemplares vendidos y vuelva a presionar 'Registrar'." | No requiere escalamiento; validación funcional del formulario. |
| "No se encontró ningún usuario con ese correo electrónico." | El correo ingresado en la sección de traslado a otra finca no coincide con ninguna cuenta activa en Control Ganadero | "Verifique con el comprador cuál es la dirección exacta de correo electrónico con la que inició sesión en Control Ganadero. Asegúrese de que no contenga espacios ni errores ortográficos antes de volver a presionar 'Validar'." | Si el comprador confirma que tiene cuenta activa y el correo no valida, verificar en soporte si el usuario está registrado en otro entorno o con número telefónico. |
| "Lo sentimos, no puedes vender animales a una finca vinculada a tu propia cuenta. Utiliza la opción de 'Trasladar animales' para hacer el traslado entre tus propias fincas." | El usuario seleccionó en la lista desplegable de traslado una finca donde él mismo figura como propietario | "No es posible utilizar el módulo de ventas para mover ganado entre fincas de su misma propiedad. Para reubicar sus animales entre sus propios predios, ingrese al menú de acciones rápidas (+) y elija la opción 'Trasladar animales'." | No requiere escalamiento; regla de negocio estricta para evitar inconsistencias contables y de inventario. |
| "No se puede eliminar este registro de venta porque tiene una transferencia a otro usuario de Control Ganadero relacionada." | Se intentó borrar una venta histórica que generó una solicitud de traslado digital a otro ganadero | "Esta venta cuenta con un traslado de animales asociado a otra cuenta de Control Ganadero, por lo que no puede eliminarse para preservar la trazabilidad del inventario entre ambas fincas." | Si el usuario requiere anular una transferencia por error involuntario y la finca receptora no ha aceptado el lote, remitir a soporte técnico para cancelar la solicitud de traslado. |
| El botón "Validar" en el correo de traslado muestra un indicador de carga y no responde | Pérdida puntual de conexión a internet durante la consulta de cuentas o lentitud de respuesta del servidor | "Espere unos segundos mientras se completa la verificación. Si el botón no reacciona, verifique su conexión a internet (Wi-Fi o datos móviles) e intente pulsar nuevamente sobre 'Validar'." | Si tras reintentar con buena señal el botón no valida el usuario por más de 2 minutos, reportar a soporte técnico. |
| Al presionar "Seleccionar animales" no aparece el animal deseado en la lista | El animal tiene una especie distinta a la configurada en el paso 1, no está asignado a la finca activa o figura con estado de baja/fallecido | "El selector solo muestra los animales de la misma especie elegida en el paso 1 que se encuentren vivos y activos en la finca. Verifique que la especie seleccionada coincida con la del animal y revise en el módulo de inventario que el ejemplar no haya sido dado de baja previamente." | Si el animal está activo y con la especie correcta en la finca pero no aparece en el selector, solicitar arete y correo para revisión de base de datos. |

### Directivas de Seguridad y Guardrails
- Advierta siempre al ganadero que al vincular un traslado digital a otro usuario, los animales seleccionados saldrán de su inventario activo una vez que la otra parte acepte la recepción.
- Los agentes de soporte jamás solicitarán contraseñas, datos bancarios ni información confidencial sobre el valor de las transacciones comerciales negociadas entre ganaderos.
- Si una venta fue completada sin traslado digital, recuerde al usuario que los animales vendidos quedan marcados en el sistema con su registro de salida, manteniéndose su trazabilidad histórica en la finca.
