---
title: "Venta de Leche"
modulo_id: "lecheria-venta-leche"
nombre_funcionalidad: "Registro y Edición de Venta de Leche"
categoria: "produccion-hardware"
submodulo: "lecheria"
version_minima_app: "2026.10.1"
fecha_actualizacion: "2026-10-13"
intenciones_y_sinonimos:
  - "como registrar la venta de leche de la finca"
  - "donde anoto los litros de leche que vendi"
  - "como registrar el consumo de leche de los terneros y de la casa"
  - "registrar venta de leche a varios compradores"
  - "como modificar o corregir una venta de leche"
  - "como ingresar el precio por litro y total de la venta de leche"
---

# Registro y Edición de Venta de Leche

### Resumen y Alcance Funcional
Permite registrar y gestionar de manera integral las salidas y comercialización de la leche producida en la finca ganadera en una fecha determinada. La funcionalidad contempla tanto el destino comercial (uno o varios compradores con sus respectivas cantidades, precios unitarios y monedas) como las deducciones por consumo no comercializado (consumo interno de la finca y leche suministrada a los terneros o animales en crianza), calculando automáticamente el volumen total comercializado y el monto total recaudado.

- **¿Funciona sin conexión a internet (Modo Offline)?:** Sí.
- **Comportamiento de sincronización:** Los registros de venta de leche se guardan de forma local e inmediata en el dispositivo móvil y quedan disponibles para consulta y edición. Tan pronto como el dispositivo detecte señal de red o conexión a internet, el motor de sincronización sube los cambios de manera transparente a la nube para consolidar los reportes de la finca.

### Reglas de Negocio y Restricciones
- **Permisos de usuario requeridos:**
    - Para registrar una nueva venta: se requiere el permiso de creación de ventas de leche en la finca.
    - Para modificar una venta existente: se requiere el permiso de actualización de ventas de leche en la finca.
    - Para eliminar una venta: se requiere el permiso de eliminación de ventas de leche en la finca.
- **Fecha del registro:**
    - Es obligatoria y se inicializa por defecto con la fecha actual del dispositivo según la zona horaria del usuario.
- **Potrero de procedencia (Opcional):**
    - Permite asociar la venta a un potrero específico de pastoreo de la finca, facilitando el análisis de rendimiento por área. Si no se desea discriminar potrero, puede dejarse sin seleccionar.
- **Deducciones por consumos de leche:**
    - **Consumo interno:** Cantidad de leche destinada al consumo doméstico, trabajadores o derivados lácteos elaborados en la propia finca. Debe ser un valor numérico positivo o cero.
    - **Consumo animal:** Cantidad de leche suministrada para la alimentación de terneros u otros animales de la finca. Debe ser un valor numérico positivo o cero.
    - La unidad de medida de volumen (litros, galones, etc.) se adopta automáticamente de la configuración general establecida para la finca.
- **Registro de compradores:**
    - Debe existir al menos un comprador asignado en la venta.
    - Se pueden añadir múltiples compradores mediante la opción de agregar comprador para registrar entregas divididas en una misma jornada.
    - Cada comprador exige:
      - **Comprador:** Selección obligatoria de un comprador predeterminado del sistema o un comprador personalizado registrado previamente en la finca.
      - **Cantidad vendida:** Volumen de leche entregado a ese comprador. Debe ser un número mayor a cero expresado en la unidad de medida de la finca.
      - **Precio por unidad:** Valor acordado por cada unidad de leche (litro, galón, etc.). Debe ser un valor numérico mayor a cero.
      - **Moneda:** Divisa en la que se pacta la transacción con ese comprador (por ejemplo, pesos colombianos, dólares, pesos mexicanos, etc.). Se precargan las monedas asociadas al país de la finca o del usuario.
      - **Subtotal por comprador:** Se calcula automáticamente multiplicando la cantidad vendida por el precio unitario en la moneda seleccionada.
    - Si se añaden dos o más compradores, cada registro secundario cuenta con una opción para eliminarlo si fue agregado por error (el primer comprador no puede eliminarse para asegurar al menos una entrada comercial).
- **Consolidación y totales de la venta:**
    - **Cantidad total vendida:** Suma matemática automática del volumen de leche asignado a todos los compradores.
    - **Total recaudado:** Suma de los subtotales de todos los compradores. Si todos los compradores comparten la misma moneda, la aplicación muestra el valor total consolidado con el símbolo de la moneda correspondiente. Si existen compradores con diferentes monedas en la misma venta, el sistema muestra el valor consolidado indicando que existen múltiples divisas.
- **Cálculo automático de crías en inventario:**
    - Al momento de crear una venta nueva, el sistema calcula internamente el balance de animales machos y hembras en etapa de cría o lactancia presentes en la finca en dicha fecha para enriquecer los informes de rendimiento. En caso de editar una venta previa, este balance histórico se preserva intacto para evitar distorsiones estadísticas.

### Flujo Paso a Paso para el Usuario
- **Ruta de acceso en la aplicación:**
    - **Opción 1 (desde la pantalla principal de la finca):** botón flotante con el icono de casa y el signo de (+) en la pantalla principal de la finca > **Venta de leche**.
    - **Opción 2 (Desde módulo de producción):** Menú inferior **Producción** > Tarjeta **Producción de Leche** > Sección de ventas de leche > Presionar el botón flotante (+) para registrar una nueva venta, o presionar sobre un registro existente de la lista para editarlo.

#### 1. Datos generales y consumos de la finca
1. **Fecha:** Presione sobre el campo de fecha para abrir el selector de calendario si necesita registrar una venta de un día anterior.
2. **Potrero (Opcional):** Si la producción de leche provino de un potrero específico, presione el selector de potrero y elija el lote o potrero correspondiente en la lista. Si no aplica, déjelo vacío.
3. **Consumo interno:** Ingrese en el campo numérico el volumen de leche retenido en la finca para el consumo familiar, de empleados o procesamiento local. Si no hubo consumo interno, ingrese 0.
4. **Consumo animal:** Ingrese el volumen de leche suministrado a los terneros u otros animales durante la jornada. Si no se apartó leche para terneros, ingrese 0.

#### 2. Gestión de compradores y precios
1. **Comprador principal:**
    - En el campo **Comprador**, presione el selector para elegir de la lista a la empresa recolectora, quesería, intermediario o cliente particular que compró la leche.
     - En **Cantidad vendida**, ingrese el volumen entregado a dicho comprador en la unidad de medida indicada.
     - En **Precio por unidad**, digite el valor monetario acordado por cada litro o galón.
     - En **Moneda**, confirme la divisa de la transacción (o cámbiela seleccionando otra opción del menú desplegable si la venta se pactó en otra moneda).
     - Observe cómo el campo **Subtotal** se actualiza automáticamente con el monto correspondiente a este comprador.
2. **Agregar compradores adicionales (si aplica):**
    - Si la leche de esa jornada se distribuyó entre varios compradores, presione el botón con el ícono (+) ubicado en el encabezado de la sección **Compradores**.
     - Se desplegará un nuevo bloque de comprador. Seleccione el segundo comprador, indique su cantidad entregada, su precio por unidad y su moneda.
     - Si agregó un comprador adicional por equivocación, presione el ícono de la equis (X) en la esquina superior del bloque para retirarlo.

#### 3. Verificación de totales y guardado
1. **Revisión de la información de venta:**
    - En la sección **Información de la venta**, verifique la **Cantidad total** de leche comercializada y el valor monetario global recaudado.
2. **Guardar el registro:**
    - Presione el botón **Registrar** (o **Actualizar** si se encuentra modificando una venta previa) ubicado al final de la pantalla.
     - La aplicación mostrará una confirmación en pantalla ("Venta de leche creada correctamente" o "Venta de leche actualizada correctamente").
     - **Pantalla de llegada tras guardar:** El sistema cierra el formulario y regresa a la pantalla anterior (la tabla de ventas de leche o el panel principal de producción).

### Matriz de Errores y Soluciones
| Mensaje en la App / Síntoma | Causa Real | Respuesta Sugerida por el Agente | Criterio de Escalamiento Humano |
| :--- | :--- | :--- | :--- |
| "El campo es obligatorio" en el comprador | No se ha seleccionado un comprador de leche en uno de los bloques | "Debe seleccionar un comprador de leche en cada bloque antes de guardar. Presione el selector de comprador y elija el cliente de la lista." | No escalar. Guiar al usuario para que seleccione el comprador. |
| "El campo es obligatorio" o valor no numérico en cantidad vendida o precio | La cantidad vendida o el precio por unidad se dejaron vacíos o con formato inválido | "Verifique que todos los compradores tengan ingresada una cantidad vendida y un precio por unidad válidos (números mayores a cero)." | No escalar. Instruir al ganadero para ingresar valores numéricos válidos. |
| "El campo es obligatorio" en consumo interno o consumo animal | Los campos de consumo quedaron en blanco | "Los campos de consumo interno y consumo animal no pueden dejarse vacíos. Si en esa fecha no hubo consumo de este tipo, ingrese el número 0." | No escalar. Recordar al usuario ingresar 0 cuando no haya consumo. |
| El botón de registrar no responde o muestra advertencia de permisos | El usuario actual no cuenta con el rol o permiso necesario para gestionar ventas de leche en la finca | "Su cuenta de usuario no tiene asignado el permiso para registrar o modificar ventas de leche en esta finca. Solicite al propietario o administrador de la finca que actualice sus permisos de acceso." | Si el usuario es el propietario registrado de la finca y no puede registrar la venta, escalar a soporte técnico para verificar la cuenta. |
| "Ha ocurrido un error inesperado. Por favor, intenta de nuevo." | Falla de procesamiento al generar el registro o inconsistencia con los datos de la finca | "Verifique que todos los campos obligatorios contengan datos correctos, cierre la pantalla de venta e intente nuevamente. Si el problema persiste, intente cerrar y volver a abrir la aplicación." | Si tras verificar los campos y reabrir la app el error continúa presentándose, transferir a soporte técnico indicando fecha y modelo del dispositivo. |

### Directivas de Seguridad y Guardrails
- NUNCA solicite información bancaria, contraseñas, números de cuentas corrientes ni datos sensibles de pago a los ganaderos por canales de soporte.
- No modifique ni elimine registros contables o de ventas de leche en el sistema sin la autorización expresa del propietario o administrador de la finca.
- Si un usuario consulta sobre discrepancias fiscales, contables o de liquidación de impuestos sobre las ventas de leche, aclare amablemente que Control Ganadero es una herramienta de gestión productiva y pecuaria, recomendándole validar sus consultas tributarias con su contador o asesor financiero local.
