---
title: "Invitar Trabajador"
modulo_id: "fincas-invitar-trabajador"
nombre_funcionalidad: "Añadir e Invitar Usuarios y Trabajadores a la Finca"
categoria: "cuentas-usuarios"
submodulo: "fincas"
version_minima_app: "2026.10.1"
fecha_actualizacion: "2026-10-13"
intenciones_y_sinonimos:
  - "como invitar un trabajador o colaborador a mi finca"
  - "como agregar un administrador o veterinario a la finca"
  - "donde registrar un nuevo usuario o empleado en control ganadero"
  - "como dar acceso a mi mayordomo a la app"
  - "que roles y permisos puedo asignarle a un colaborador"
  - "que hacer si no le llega la invitacion al trabajador"
---

# Añadir e Invitar Usuarios y Trabajadores a la Finca

### Resumen y Alcance Funcional
Permite al propietario de la finca ganadera (o usuarios autorizados) enviar invitaciones formales por correo electrónico a mayordomos, administradores, veterinarios, empleados y visitantes para colaborar en la gestión operativa de la explotación pecuaria. Al invitar a un usuario, el propietario define su nivel de responsabilidad asignándole un perfil predeterminado con permisos específicos de consulta, registro, edición o supervisión sobre los datos de la finca activa.

- **¿Funciona sin conexión a internet (Modo Offline)?:** No.
- **Comportamiento de sincronización:** Esta funcionalidad requiere una conexión activa a internet (datos móviles o red wifi). El envío de la invitación y la asignación del rol sobre la finca se procesan en tiempo real mediante los servidores centrales de Control Ganadero. Una vez enviada con éxito, la invitación queda registrada en la lista de invitaciones pendientes de la finca hasta que el usuario invitado acceda con su cuenta a la plataforma.

### Reglas de Negocio y Restricciones
- **Permisos requeridos en la plataforma:**
  - El usuario debe contar con el permiso de creación e invitación de colaboradores en la finca activa. Si un usuario sin este permiso intenta acceder o enviar el formulario, el sistema bloquea la operación y presenta el aviso: *"No tienes permisos para realizar esta acción."*
- **Campos obligatorios del formulario:**
  - **Nombre:** Obligatorio. Debe corresponder al nombre personal o identificador del colaborador.
  - **Correo electrónico:** Obligatorio. Debe cumplir con un formato válido de dirección de correo electrónico (ejemplo: `nombre@correo.com`).
  - **Tipo de perfil:** Selección obligatoria entre los perfiles disponibles en el sistema.
- **Perfiles predeterminados y niveles de acceso:**
  - **Empleado (seleccionado por defecto):** Responsable del registro diario de actividades pecuarias de campo (pesajes, tareas, eventos). Cuenta con permisos para leer registros autorizados y registrar eventos, pero no puede editar ni eliminar configuraciones generales de la finca.
  - **Administrador:** Encargado de supervisar y administrar la finca. Cuenta con permisos completos para leer, crear, editar y eliminar registros de la explotación ganadera, pero no puede administrar ni invitar a otros colaboradores.
  - **Veterinario:** Responsable del seguimiento sanitario y reproductivo del hato. Puede leer registros de la finca y gestionar planes de vacunación, tratamientos, partos, celos e inseminaciones, pero no puede eliminar registros generales de la finca.
  - **Visitante:** Usuario con acceso de solo consulta y lectura. No puede crear, editar ni eliminar información en la finca.
- **Tarjeta explicativa dinámica del rol:**
  - Al cambiar la selección en el campo **Tipo de perfil**, la parte inferior del formulario actualiza de inmediato una tarjeta explicativa que detalla el título del perfil seleccionado, su descripción funcional y el desglose literal de permisos y restricciones.
- **Reinicio del formulario tras el envío:**
  - Al completar con éxito la invitación, el sistema muestra el aviso *"Invitación enviada"* y restablece automáticamente los campos a sus valores iniciales (formulario limpio y perfil en **Empleado**), permitiendo invitar a otro usuario consecutivamente si se requiere.

### Flujo Paso a Paso para el Usuario
- **Ruta de acceso en la aplicación:** Menú lateral principal (ícono de tres líneas en la esquina superior izquierda) > **Trabajadores** > Presione el botón flotante con el ícono de agregar persona (+).

#### 1. Diligenciamiento de datos del colaborador
1. En la barra superior observará el encabezado **Añadir usuarios**, junto con el botón de flecha para regresar.
2. En el campo **Nombre**, escriba el nombre completo del colaborador o empleado que desea vincular.
3. En el campo **Correo electrónico**, ingrese la cuenta de correo electrónico exacta con la que el trabajador se registrará o iniciará sesión en la aplicación.
4. En el campo desplegable **Tipo de perfil**, pulse para abrir la lista de roles y seleccione el que corresponda a las funciones del usuario:
   - **Administrador**
   - **Veterinario**
   - **Empleado**
   - **Visitante**

#### 2. Revisión de permisos asignados
1. Debajo del botón de envío, consulte la tarjeta descriptiva de color gris claro.
2. Verifique las atribuciones del rol seleccionado (por ejemplo, qué actividades de campo puede registrar o si su acceso es estrictamente de consulta).

#### 3. Envío de la invitación
1. Presione el botón **Invitar**.
2. El sistema validará los campos y tramitará la invitación en el servidor.
3. Al finalizar, la aplicación presentará en la parte inferior una notificación emergente con el mensaje **Invitación enviada** y limpiará los campos del formulario.
- **Pantalla de llegada tras guardar o salir:** El usuario permanece en la pantalla **Añadir usuarios** con el formulario limpio para poder agregar más colaboradores si lo desea. Para regresar al listado general de miembros de la finca, presione el botón de flecha hacia atrás en la barra superior, retornando a la pantalla **Trabajadores** donde figurará la invitación recién enviada.

### Matriz de Errores y Soluciones
| Mensaje en la App / Síntoma | Causa Real | Respuesta Sugerida por el Agente | Criterio de Escalamiento Humano |
| :--- | :--- | :--- | :--- |
| "No tienes permisos para realizar esta acción." | El usuario con sesión iniciada no cuenta con el permiso para crear e invitar colaboradores en la finca activa | "Solo el propietario registrado o usuarios con permisos de administración pueden invitar nuevos colaboradores a la finca. Si necesita agregar personal, solicite al dueño de la finca que le otorgue los permisos requeridos o que envíe la invitación desde su cuenta." | No escalar. Corresponde al esquema de seguridad y permisos de la finca. |
| "El campo es requerido" | Se intentó presionar el botón de invitación dejando el nombre o el correo electrónico en blanco | "Por favor, complete tanto el nombre como el correo electrónico del trabajador antes de presionar el botón Invitar." | No escalar. Error de validación en pantalla. |
| "El correo electrónico es invalido" | El formato del correo electrónico ingresado no tiene la estructura estándar (ejemplo: falta el arroba @ o el dominio .com) | "El correo ingresado no es válido. Compruebe que esté escrito correctamente, sin espacios al inicio o al final y con un formato válido como ejemplo@correo.com." | No escalar. Guiar al ganadero para corregir el formato. |
| "Parece que tienes problemas con tu conexión a internet. Por favor, verifica tu conexión e inténtalo de nuevo." | El teléfono móvil perdió la conexión de datos móviles o señal wifi durante el envío de la invitación | "Para enviar la invitación al trabajador es necesario contar con conexión a internet. Verifique que sus datos móviles o su red wifi estén activos e intente presionar Invitar nuevamente." | Si el usuario cuenta con buena conexión y el mensaje persiste tras varios intentos, transferir a soporte técnico. |
| El trabajador invitado indica que no puede ver la finca tras registrarse | El trabajador se registró con un correo electrónico diferente al ingresado en la invitación, o aún no ha completado el proceso de registro | "Verifique que el trabajador se haya registrado en Control Ganadero con el mismo correo electrónico exacto al que usted envió la invitación. Si el correo coincide y aún no aparece la finca, pídale que cierre la aplicación y vuelva a iniciar sesión." | Si tras verificar la coincidencia exacta de correos el colaborador sigue sin acceso a la finca, solicitar correos de ambas cuentas y derivar a soporte técnico. |

### Directivas de Seguridad y Guardrails
- NUNCA solicite contraseñas, claves personales ni códigos de acceso a los propietarios ni a los trabajadores invitados.
- Las invitaciones se envían de forma segura al buzón de correo del destinatario y no requieren que el propietario comparta sus propias credenciales de acceso.
- Si un usuario reporta que invitó a un correo erróneo, explíquele cómo acceder a la lista general de **Trabajadores**, seleccionar la invitación pendiente y eliminarla para revocar el acceso de inmediato antes de generar una nueva invitación.
