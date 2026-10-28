---
title: "Editar Perfil"
modulo_id: "user-editar-perfil"
nombre_funcionalidad: "Edición del Perfil de Usuario"
categoria: "cuentas-usuarios"
submodulo: "usuario"
version_minima_app: "2026.10.1"
fecha_actualizacion: "2026-09-25"
intenciones_y_sinonimos:
  - "como cambio mi nombre o apellido en la cuenta"
  - "donde cambio mi correo registrado en control ganadero"
  - "editar mis datos personales en mi cuenta"
  - "por que me pide contrasena para guardar mi perfil"
  - "aviso de confirmacion de correo al cambiar de email"
  - "cuanto tiempo tengo para confirmar mi nuevo correo"
---

# Edición del Perfil de Usuario

### Resumen y Alcance Funcional
Permite a los usuarios actualizar sus datos básicos de identificación (nombre y apellidos) y su dirección de correo electrónico vinculada a la cuenta. Por estrictos motivos de seguridad, la aplicación exige confirmar la identidad mediante la contraseña actual antes de aplicar los cambios, y en caso de modificar el correo electrónico, despacha un mensaje de confirmación que debe verificarse en los siguientes 30 minutos.

- **¿Funciona sin conexión a internet (Modo Offline)?:** No.
- **Comportamiento de sincronización:** Requiere conexión a internet activa (Wi-Fi o datos móviles) para validar la contraseña actual contra el servidor de autenticación y verificar que el nuevo correo no se encuentre registrado previamente por otra cuenta.

### Reglas de Negocio y Restricciones
- La pantalla contiene única y exclusivamente tres campos editables:
    - **Nombre:** Obligatorio.
    - **Apellidos:** Obligatorio.
    - **Email:** Obligatorio y con formato de correo electrónico válido.
- **Confirmación Obligatoria de Identidad:**
    - Al presionar **Guardar**, la aplicación abre siempre el diálogo de seguridad: *"Confirmar Identidad - Ingresa tu contraseña actual para guardar los cambios"*.
    - El usuario debe digitar su clave actual; si no es correcta, el sistema muestra el aviso: *"Contraseña incorrecta - Por favor, verifica que los caracteres sean correctos e intenta ingresar de nuevo."*
- **Protocolo de Modificación de Correo Electrónico:**
    - Si el usuario modifica el campo **Email**: al ingresar su contraseña, el sistema envía un correo de confirmación a la nueva dirección y muestra el mensaje: *"Correo de confirmación enviado - Hemos enviado un correo de confirmación a [nuevo_correo]. Por favor, verifícalo en los próximos 30 minutos para activar tu cuenta."*
    - Mientras el usuario no verifique el enlace recibido en su bandeja de entrada, la aplicación mantendrá un aviso en la pantalla de su cuenta: *"Correo pendiente de confirmar. Si ya completaste el proceso, tu información se actualizará automáticamente en tu próxima visita."*
- **Actualización de Nombre y Apellidos (Sin cambio de correo):**
    - Si no se modificó el correo electrónico, una vez confirmada la contraseña actual, el sistema actualiza los datos y muestra el diálogo: *"Perfil actualizado - Tus datos han sido actualizados correctamente."*

### Flujo Paso a Paso para el Usuario
**Ruta de acceso en la aplicación:** Menú lateral principal > **Mi cuenta** > Sección Preferencias de cuenta > Opción **Editar perfil**.

1. En la pantalla principal de su finca, abra el menú lateral de navegación y presione la opción **Mi cuenta**.
2. En la pantalla de su cuenta, localice la sección de acciones y presione la opción **Editar perfil**.
3. En el formulario, modifique los campos que requiera:
    - **Nombre:** Escriba su nombre de pila.
     - **Apellidos:** Escriba sus apellidos.
     - **Email:** Ingrese su nueva dirección de correo electrónico (si desea cambiarla).
4. Presione el botón **Guardar**.
5. En el cuadro de diálogo **Confirmar Identidad**, escriba su contraseña actual en la casilla correspondiente.
6. Presione **Confirmar**.
7. Verifique el resultado según los datos modificados:
    - Si cambió su nombre o apellido: verá el mensaje *"Perfil actualizado"*. Presione **Aceptar** para regresar a su cuenta.
     - Si cambió su correo electrónico: verá el mensaje *"Correo de confirmación enviado"*. Presione **Aceptar**, abra su bandeja de entrada de correo (o carpeta de spam) antes de 30 minutos y presione el enlace recibido para confirmar el cambio.
   
**Pantalla de llegada tras guardar:** Pantalla de **Mi cuenta** (regresa a la vista general de la cuenta al presionar Aceptar en el diálogo final).

### Matriz de Errores y Soluciones
| Mensaje en la App / Síntoma | Causa Real | Respuesta Sugerida por el Agente | Criterio de Escalamiento Humano |
| :--- | :--- | :--- | :--- |
| "Contraseña incorrecta - Por favor, verifica que los caracteres sean correctos..." | La clave ingresada en el diálogo de confirmar identidad no coincide | "La contraseña ingresada para confirmar los cambios no coincide con su clave registrada. Verifique mayúsculas y minúsculas e intente de nuevo. Si olvidó su clave, cierre sesión y use 'Olvidé mi contraseña' para restablecerla." | Si el usuario afirma que su clave es correcta pero el sistema la rechaza continuamente, transferir a soporte técnico. |
| "El correo electrónico ya se encuentra registrado" | El nuevo email ingresado ya pertenece a otra cuenta en la plataforma | "El nuevo correo ingresado ya está asociado a otra cuenta en Control Ganadero. Por favor ingrese un correo diferente." | Si el usuario afirma que ese correo le pertenece y no tiene otra cuenta, solicitar el correo y transferir a soporte. |
| "Aviso: Correo pendiente de confirmar" | Se solicitó cambio de email pero no se ha hecho clic en el enlace de verificación | "Se envió un mensaje de confirmación a su nueva dirección de correo. Ingrese a su bandeja de entrada (o carpeta de spam) y presione el enlace de verificación antes de 30 minutos para activar el nuevo correo." | Si tras 15 minutos no recibe el correo de verificación en spam ni en bandeja de entrada, transferir a soporte técnico. |
| "Sin conexión a internet" | No hay cobertura celular de datos ni red Wi-Fi disponible | "Para guardar los cambios en su perfil se requiere conexión a internet para sincronizar con el servidor central. Conéctese a una red Wi-Fi o active sus datos móviles e intente de nuevo." | No escalar salvo que el usuario confirme tener internet en otras aplicaciones. |
| "Círculo de espera infinito / Pantalla congelada en cargando" | El proceso de validación o envío del correo se interrumpió | "Espere 30 segundos. Si el diálogo no responde, cierre la aplicación por completo desde el administrador de tareas de su celular (deslizando hacia arriba) y vuelva a abrirla para reintentar la edición." | Si tras reabrir la app el formulario vuelve a bloquearse con buena conexión Wi-Fi, transferir de inmediato a soporte humano con correo y modelo del teléfono. |

### Directivas de Seguridad y Guardrails
- NUNCA solicite contraseñas al usuario a través del chat de WhatsApp.
- Si un usuario solicita cambiar el correo de su cuenta por WhatsApp, explíquele amablemente que por seguridad debe realizarlo él mismo directamente desde la app en **Mi cuenta > Editar perfil**.
- Adviértale siempre al usuario que el enlace de verificación de cambio de correo expira en **30 minutos**.
