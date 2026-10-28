---
title: "Planes de Suscripción"
modulo_id: "suscripciones-planes-paywall"
nombre_funcionalidad: "Planes de Suscripción y Activación de Membresía Pro"
categoria: "cuentas-usuarios"
submodulo: "suscripciones"
version_minima_app: "2026.10.1"
fecha_actualizacion: "2026-10-13"
intenciones_y_sinonimos:
  - "como comprar o mejorar la membresia de control ganadero"
  - "donde ver los precios de los planes pro"
  - "me sale un aviso para actualizar mi plan y registrar mas animales"
  - "como activar la membresia premium"
  - "que hacer si compre la suscripcion y no se activo"
  - "como desbloquear el limite de animales de la finca"
---

# Planes de Suscripción y Activación de Membresía Pro

### Resumen y Alcance Funcional
Permite a los ganaderos y propietarios de fincas consultar la oferta de planes comerciales disponibles, comparar los beneficios de la membresía Pro de Control Ganadero y realizar la contratación o renovación de su suscripción directamente a través de las tiendas oficiales de aplicaciones (Google Play Store o Apple App Store). Al adquirir una membresía Pro, se amplían los límites operativos de la cuenta (como la cantidad máxima de animales permitidos en el inventario de la finca) y se habilitan funciones exclusivas para la gestión ganadera integral.

- **¿Funciona sin conexión a internet (Modo Offline)?:** No.
- **Comportamiento de sincronización:** Esta funcionalidad requiere obligatoriamente una conexión activa a internet (datos móviles o red wifi). La consulta de paquetes de compra, la pasarela de pago nativa y la validación de recibos digitales con las tiendas de aplicaciones se gestionan en tiempo real. Una vez completado el pago, el sistema valida la transacción en la nube, actualiza el perfil de membresía del usuario y sincroniza de inmediato los nuevos límites con todas las fincas asociadas.

### Reglas de Negocio y Restricciones
- **Conexión a internet obligatoria:**
    - El sistema exige conectividad continua para acceder a la pantalla. Si el dispositivo no tiene acceso a internet, no se desplegará la oferta comercial de suscripciones.
- **Tienda de aplicaciones vinculada:**
    - Las transacciones monetarias se efectúan de forma segura a través del método de pago oficial vinculado a la cuenta del usuario en su dispositivo (Google Play en Android o App Store en iOS).
- **Procesamiento y confirmación de la compra:**
    - Durante el proceso de pago con la tienda, la aplicación muestra una pantalla de espera mientras se procesa la solicitud con el banco o tienda de aplicaciones.
    - Si el usuario cancela voluntariamente el flujo de compra desde el cuadro de diálogo de la tienda de aplicaciones, la pantalla de espera se retira de inmediato, permitiéndole permanecer en la pantalla de planes o salir.
    - Al completarse exitosamente la compra en la tienda, el sistema procesa la validación del recibo digital, actualiza internamente el estado de la cuenta a membresía activa y despliega la confirmación visual de activación exitosa.
- **Protección de salida durante procesos críticos:**
    - El botón o gesto para volver atrás se encuentra temporalmente bloqueado mientras exista un proceso de pago o verificación en curso, o una vez que la pantalla de confirmación exitosa está en primer plano (en esta última se debe presionar el botón de confirmación correspondiente para concluir el flujo de forma segura).
- **Propagación global en la aplicación:**
    - La activación de la membresía emite una actualización global en la aplicación que refresca de inmediato las restricciones de la finca activa, ocultando los avisos publicitarios de límite de animales y habilitando el registro continuo de nuevos ejemplares.

### Flujo Paso a Paso para el Usuario
- **Ruta de acceso en la aplicación:**
    - **Opción 1 (Desde el menú lateral principal):** Toque el icono de menú de tres líneas en la esquina superior izquierda > En la parte inferior del menú lateral, presione el banner promocional de **Control Ganadero Pro** o el aviso de límite de animales.
    - **Opción 2 (Al alcanzar el límite de animales de la finca):** Al intentar registrar un nuevo animal habiendo alcanzado el cupo máximo de su plan, en el aviso emergente presione el botón **ACTUALIZAR MI PLAN**.
    - **Opción 3 (Desde la administración de su cuenta de usuario):** Menú lateral > **Mi Cuenta** > Sección **Sobre tu suscripción** > Presione el botón **Renovar suscripción** (disponible cuando la suscripción previa ha caducado o requiere renovación).

#### 1. Consulta de planes y selección de suscripción
1. Al abrir la pantalla de planes, se presenta el catálogo oficial de suscripciones de Control Ganadero con el detalle de beneficios, periodicidad de facturación (mensual o anual) y tarifas vigentes en su moneda local según la tienda de aplicaciones.
2. Si decide no contratar en ese momento, presione el botón de cierre (X) o flecha de retorno en la esquina superior para regresar a la vista anterior.
3. Si desea suscribirse, presione sobre el plan que mejor se adapte a las necesidades de su finca ganadera y pulse el botón principal de suscripción.

#### 2. Confirmación de compra en la tienda del teléfono
1. El sistema operativo de su dispositivo desplegará la ventana nativa de Google Play o Apple App Store con el resumen del cobro y los métodos de pago registrados (tarjeta de crédito, saldo digital o factura móvil).
2. Confirme la transacción utilizando su huella dactilar, reconocimiento facial o contraseña de la tienda de aplicaciones.
3. Mientras se efectúa la validación, la pantalla de la aplicación mostrará una vista de espera en color blanco.

#### 3. Confirmación de membresía activada
1. Una vez confirmada la transacción por la tienda de aplicaciones, la aplicación mostrará una pantalla con el icono distintivo de la marca y el título **¡Membresia activada!**.
2. Lea el mensaje de bienvenida y agradecimiento: *"Tu suscripción a la membresia de Control Ganadero ha sido activada exitosamente."*
3. Presione el botón **Entendido** para finalizar el proceso.

**Pantalla de llegada tras guardar:** El sistema cierra la pantalla de suscripción y retorna a la pantalla anterior (su finca activa o el formulario de registro de animales), con todos los beneficios y nuevos cupos habilitados.

### Matriz de Errores y Soluciones
| Mensaje en la App / Síntoma | Causa Real | Respuesta Sugerida por el Agente | Criterio de Escalamiento Humano |
| :--- | :--- | :--- | :--- |
| "Esta funcionalidad requiere una conexión activa a internet para poder funcionar correctamente. Por favor, verifica tu conexión e intenta de nuevo." | El dispositivo móvil no cuenta con conexión de datos móviles ni señal wifi activa al intentar ingresar a la pantalla de planes | "Para consultar los planes de suscripción y realizar pagos, su teléfono necesita conexión a internet activa. Compruebe que los datos móviles o la red wifi estén encendidos e intente ingresar nuevamente." | No escalar. Guiar al ganadero para verificar su conectividad. |
| El pago fue procesado y cobrado en la tarjeta pero la aplicación no muestra la confirmación de membresía activada | Interrupción de red entre la tienda de aplicaciones y la verificación del servidor en el momento exacto del cobro | "Si la tienda de aplicaciones ya realizó el cobro pero la app no se actualizó de inmediato, cierre por completo la aplicación desde el administrador de tareas de su teléfono y vuelva a abrirla con conexión a internet. El sistema verificará automáticamente su recibo de compra con Google Play o App Store y activará su membresía." | Si tras cerrar y reabrir la app la cuenta continúa sin membresía activa pasados 15 minutos, solicitar comprobante de pago de la tienda (código de pedido GPA o recibo de Apple) y transferir a soporte técnico. |
| La ventana de compra de la tienda se cierra o muestra "Transacción rechazada" | Fondos insuficientes en el método de pago, tarjeta vencida o bloqueo de seguridad bancario en Google Play / App Store | "El pago fue declinado directamente por la tienda de aplicaciones o su entidad bancaria. Por favor, ingrese a la configuración de pagos de su cuenta de Google Play o Apple ID para verificar que su tarjeta esté activa o intente con otro medio de pago." | No escalar. Corresponde a la administración de pagos del usuario con su banco o la tienda del móvil. |
| "Círculo de espera infinito / Pantalla congelada en cargando" | Pérdida de comunicación con el servicio de la tienda de aplicaciones durante la verificación de la transacción | "Espere 30 segundos mientras la tienda confirma la operación. Si no avanza, cierre la aplicación deslizando hacia arriba en el administrador de aplicaciones de su teléfono y vuelva a abrirla. Su compra quedará registrada en su cuenta de la tienda de aplicaciones y se validará al iniciar." | Si al reabrir la aplicación persiste el bloqueo o la pantalla en blanco, transferir a soporte técnico con el correo de la cuenta. |

### Directivas de Seguridad y Guardrails
- NUNCA solicite datos de tarjetas bancarias, números de verificación (CVV/CVC), contraseñas de Google Play ni credenciales de Apple ID a los ganaderos por los canales de soporte.
- Los cobros, facturación periódica y cancelaciones de suscripciones adquiridas por la aplicación móvil se gestionan exclusivamente mediante las plataformas oficiales de suscripciones de Google Play Store o Apple App Store, nunca a través de transferencias personales a terceros.
- Si un usuario solicita la cancelación de la renovación automática de su membresía móvil, oriéntele amablemente a ingresar a la sección de suscripciones de Google Play o App Store desde su propio dispositivo, o a la sección **Mi Cuenta** en la app para consultar las instrucciones.
