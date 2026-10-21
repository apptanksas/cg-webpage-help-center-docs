---
title: "Seleccionar Finca"
modulo_id: "farm-select"
nombre_funcionalidad: "Selección y Cambio de Finca Ganadera Activa"
categoria: "cuentas-usuarios"
submodulo: "fincas"
version_minima_app: "2026.10.1"
fecha_actualizacion: "2026-10-09"
intenciones_y_sinonimos:
  - "como cambiar de finca en la aplicacion"
  - "donde veo todas mis fincas registradas"
  - "como alternar entre dos fincas ganaderas"
  - "no puedo entrar a una finca porque sale un icono de bloqueo"
  - "que significa el contador de fincas en la parte superior"
  - "como crear una nueva finca desde el selector"
---

# Selección y Cambio de Finca Ganadera Activa

### Resumen y Alcance Funcional
Módulo central para la conmutación y administración visual de las fincas ganaderas asociadas a la cuenta del usuario. Permite alternar de manera instantánea la finca de trabajo activa en el dispositivo, visualizar el balance de predios propios frente al cupo máximo contratado en la suscripción, y acceder al alta de nuevas explotaciones pecuarias.

Al seleccionar una finca, todo el contexto operativo de la aplicación (inventario de animales, eventos de calendario, pesajes, tareas y registros lecheros) se actualiza de inmediato para reflejar exclusivamente la información del predio elegido.

- **¿Funciona sin conexión a internet (Modo Offline)?:** Sí. La lista de fincas y la selección de la finca activa se gestionan de forma 100% local en la base de datos y memoria del teléfono, permitiendo cambiar de predio en cualquier momento sin requerir conexión a internet.
- **Comportamiento de sincronización:** Al pulsar sobre una finca habilitada, el identificador se almacena de inmediato en la configuración local y se emite una notificación interna en el sistema que actualiza los filtros y permisos. La aplicación conmuta las restricciones correspondientes (sea que el usuario actúe como propietario o como colaborador autorizado con acceso concedido) y reanuda el ciclo de sincronización en segundo plano con el servidor central para mantener los datos de la finca al día.

### Reglas de Negocio y Restricciones
- **Permisos de visualización y acceso:**
  - Cualquier usuario registrado con una o más fincas asignadas puede abrir la pantalla de selección para alternar entre sus predios.
  - Para iniciar la creación de un nuevo predio desde esta pantalla (tarjeta con ícono de suma), el usuario debe poseer el permiso de creación de fincas. Si su perfil o rol actual no lo permite, el sistema bloqueará el avance mostrando la advertencia de permisos insuficientes.
- **Comportamiento en el menú lateral según el número de fincas registradas:**
  - *Caso 1: Usuario con una sola finca registrada:* En la parte superior del menú lateral se muestra la tarjeta de la finca actual junto a un botón directo para registrar una nueva explotación pecuaria (**Nueva finca**). En este caso, **no aparece el botón con la flecha desplegable**, ya que no existen predios adicionales para alternar en el dispositivo. Si el usuario desea conmutar entre fincas, primero debe registrar una segunda finca mediante dicho botón de alta.
  - *Caso 2: Usuario con 2 o más fincas registradas:* En la parte superior del menú lateral se muestran hasta 2 tarjetas de fincas en acceso rápido y, a la derecha de las mismas, aparece un botón circular con una **flecha desplegable hacia abajo**. Al presionar este botón, se abre la pantalla completa del selector general de fincas.
  - *Caso 3: Usuario sin finca seleccionada o activa:* El menú lateral muestra un botón prominente titulado **Seleccionar finca** para acceder directamente a la pantalla de selección y definir el predio de trabajo.
- **Contador y balance de fincas en cabecera:**
  - En la barra superior, a la derecha del título, se despliega una fracción numérica que indica el estado de la cuota: el primer número representa la cantidad de fincas propias registradas por el usuario, y el segundo número el límite máximo de fincas permitidas según el plan o complementos contratados (por ejemplo, 1/1, 2/3).
  - Las fincas en las que el usuario colabora como invitado o empleado no descuentan de su cuota de fincas propias de suscripción, pero sí se muestran en la cuadrícula para su consulta y gestión.
- **Ordenamiento y distintivos en la cuadrícula:**
  - Las fincas se presentan en una cuadrícula adaptable (3 columnas en teléfonos y 5 columnas en tabletas).
  - La primera posición de la cuadrícula siempre está reservada para la opción de registrar un nuevo predio.
  - Las fincas en las que el usuario es propietario se ordenan con prioridad al inicio de la lista y exhiben una insignia distintiva en la esquina superior de su tarjeta con el texto **Propietario**.
  - Si la finca cuenta con fotografía registrada, se despliega en su tarjeta; de lo contrario, se presenta la ilustración estándar de la plataforma.
- **Restricción por suscripción o fincas deshabilitadas:**
  - Si una finca se encuentra deshabilitada debido al vencimiento de la suscripción o por exceder el número de fincas adicionales activas en la cuenta, su imagen se muestra atenuada en escala de grises y con un ícono de bloqueo en el centro.
  - Al presionar una finca deshabilitada, el sistema impide el acceso a sus registros y despliega un cuadro de diálogo informativo indicando que se debe renovar o actualizar la suscripción para reactivarla.

### Flujo Paso a Paso para el Usuario
- **Ruta de acceso en la aplicación:**
  - *Ruta 1 (Desde el Menú Lateral con 2 o más fincas):* Menú lateral principal (ícono de tres líneas horizontales en la esquina superior izquierda) > En la sección superior donde se visualizan las tarjetas de fincas, pulsar el botón circular con la flecha desplegable hacia abajo situado a la derecha.
  - *Ruta 2 (Desde el Menú Lateral si no hay finca seleccionada):* Menú lateral principal > Pulsar el botón central **Seleccionar finca**.
  - *Nota sobre cuentas con una sola finca:* Si el usuario tiene una única finca registrada, la flecha desplegable no se muestra en el menú lateral; en su lugar, se visualiza la tarjeta de la finca activa junto al botón **Nueva finca** para permitirle registrar un segundo predio.

#### 1. Exploración de Predios y Estado de la Cuenta
- En la barra superior se visualiza el título **Fincas**, el botón de cierre para volver a la pantalla anterior sin cambiar de predio, y el contador de fincas propias frente al cupo máximo contratado.
- En la cuadrícula principal se observan las opciones de alta y las tarjetas de cada finca con su nombre respectivo, fotografía o ilustración, e insignia de propiedad si aplica.

#### 2. Cambio de Finca Activa de Trabajo
- Localice la finca que desea gestionar y pulse sobre su tarjeta.
- Si la finca está habilitada, la aplicación la establecerá como la finca activa y redirigirá automáticamente a la pantalla de **Inicio** (panel principal de la finca), cargando de inmediato sus métricas zootécnicas, alertas y calendario.

#### 3. Registro de una Nueva Finca
- En la primera casilla de la cuadrícula, identifique la tarjeta con el ícono de suma y la etiqueta **Nuevo**.
- Pulse sobre la tarjeta para iniciar el asistente de registro.
- Si cuenta con los permisos correspondientes y cupo disponible, la aplicación abrirá el formulario para configurar los datos básicos, ubicación y especies del nuevo predio.

### Matriz de Errores y Soluciones
| Mensaje en la App / Síntoma | Causa Real | Respuesta Sugerida por el Agente | Criterio de Escalamiento Humano |
| :--- | :--- | :--- | :--- |
| "No tienes fincas adicionales suficientes para acceder a esta finca. Te invitamos a renovar o actualizar tu suscripción para que puedas acceder a todas tus fincas." (acompañado de ícono de bloqueo en la tarjeta) | La finca seleccionada ha sido inhabilitada porque la suscripción del propietario venció o porque se superó la cuota de fincas contratadas | "Esta finca se encuentra deshabilitada temporalmente debido al estado de la suscripción o límite de fincas contratadas. Para recuperar el acceso completo a los datos y animales de este predio, es necesario renovar o actualizar su membresía en la plataforma." | Si el usuario ya realizó el pago y la finca continúa bloqueada tras sincronizar, solicitar comprobante de pago y transferir a facturación/soporte administrativo. |
| "No tienes permisos para realizar esta acción." / "Con tu perfil de [perfil], NO tienes permisos para realizar esta acción." | El usuario intentó presionar la tarjeta de creación de nueva finca sin contar con el permiso requerido en su rol | "Su rol o perfil actual dentro de la plataforma no tiene asignado el permiso para crear nuevas fincas ganaderas. Debe solicitar al propietario de la cuenta o administrador que ajuste sus facultades si requiere habilitar nuevos predios." | No requiere escalamiento; regla de control de acceso y seguridad por roles. |
| La pantalla muestra un indicador de carga central de forma persistente | Retardo en la lectura de la base de datos local o en el cálculo de cuentas al inicializar la pantalla | "Por favor espere unos segundos mientras la aplicación organiza sus fincas. Si no responde tras 30 segundos, cierre la aplicación por completo desde el administrador de tareas de su teléfono y vuelva a abrirla." | Si tras reiniciar la aplicación el indicador continúa sin mostrar las fincas, verificar si la sesión expiró y derivar a soporte técnico. |
| No aparece el botón de flecha desplegable para cambiar de finca en el menú lateral | La cuenta tiene registrada una sola finca ganadera activa; la interfaz sustituye la flecha por el botón directo "Nueva finca" | "Si solo tiene una finca registrada, la aplicación no despliega el selector desplegable múltiple en el menú lateral, ya que no existen otros predios a los cuales alternar. En su lugar, encontrará el botón 'Nueva finca' para registrar otro predio. Una vez que disponga de dos o más fincas, aparecerá automáticamente la flecha desplegable para alternar entre ellas." | No requiere escalamiento; comportamiento de interfaz adaptativo. |

### Directivas de Seguridad y Guardrails
- Recuerde siempre al usuario que al cambiar de finca activa no se pierden ni se sobreescriben datos del predio anterior: cada finca mantiene su propio historial zootécnico y registros independientes.
- Si el usuario reporta que una finca compartida está bloqueada, aclare que la habilitación depende de la suscripción del propietario legítimo de esa finca y no de la cuenta del colaborador invitado.
- Jamás solicite contraseñas, pines de acceso ni datos de tarjetas de crédito para solucionar bloqueos de suscripción; oriente siempre hacia los canales oficiales de renovación dentro de la aplicación o portal web.
