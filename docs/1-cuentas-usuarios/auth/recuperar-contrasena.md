---
title: "Recuperar Contraseña"
modulo_id: "auth-recuperar-contrasena"
nombre_funcionalidad: "Recuperación de Contraseña de Acceso"
categoria: "cuentas-usuarios"
submodulo: "auth"
version_minima_app: "2026.10.1"
fecha_actualizacion: "2026-09-25"
intenciones_y_sinonimos:
  - "olvide mi clave de control ganadero"
  - "como recupero mi contrasena"
  - "no me llega el correo para cambiar la clave"
  - "perdi el acceso a mi cuenta y no recuerdo la clave"
  - "donde pido restablecer la contrasena"
  - "no puedo entrar a mi finca por la clave"
---

# Recuperación de Contraseña de Acceso

### Resumen y Alcance Funcional
Permite a los usuarios que han olvidado o extraviado su clave de acceso solicitar un correo electrónico seguro con las instrucciones y el enlace necesario para restablecer su contraseña y recuperar el ingreso a sus fincas en Control Ganadero.

- **¿Funciona sin conexión a internet (Modo Offline)?:** No.
- **Comportamiento de sincronización:** Requiere conexión a internet activa (Wi-Fi o datos móviles) para contactar al servidor central de autenticación y despachar el correo electrónico de seguridad a la dirección registrada.

### Reglas de Negocio y Restricciones
- El correo electrónico ingresado debe tener un formato válido con su correspondiente arroba y dominio.
- El usuario debe tener una cuenta previamente registrada en la plataforma con ese correo.
- Por motivos de seguridad, el enlace enviado al correo tiene un tiempo de validez limitado; si vence, el usuario deberá generar una nueva solicitud.
- El proceso no muestra la contraseña anterior ni la cambia automáticamente dentro de la app móvil; el restablecimiento seguro se realiza a través de las instrucciones enviadas al email.

### Flujo Paso a Paso para el Usuario

**Ruta de acceso en la aplicación:** Pantalla de Bienvenida inicial > **Iniciar Sesión** > Enlace **Olvidé mi contraseña**.

1. En la pantalla de inicio de sesión, presione la opción **Olvidé mi contraseña**.
2. En la casilla **Email**, escriba la dirección de correo electrónico asociada a su cuenta.
3. Presione el botón **Enviar**.
4. Al enviarse la solicitud, la pantalla mostrará el mensaje de confirmación: *"Se le ha enviado un correo electrónico con las instrucciones para recuperar la contraseña."*
5. Presione el botón **Aceptar** para volver a la pantalla de inicio de sesión.
6. Revise la bandeja de entrada de su correo electrónico (incluyendo la carpeta de spam o correo no deseado) y siga las instrucciones del mensaje recibido para definir su nueva clave.

**Pantalla de llegada tras guardar:** Pantalla de **Inicio de Sesión** (al presionar el botón "Aceptar" en la confirmación de envío).

### Matriz de Errores y Soluciones
| Mensaje en la App / Síntoma | Causa Real | Respuesta Sugerida por el Agente | Criterio de Escalamiento Humano |
| :--- | :--- | :--- | :--- |
| "Formato de correo no válido" | Falta el arroba o la extensión del dominio | "Verifique que su correo esté bien escrito (ejemplo: usuario@finca.com) y no contenga espacios antes ni después." | No escalar, es una corrección directa en pantalla. |
| "No llega el correo de recuperación" | El mensaje se filtró en spam o el correo no coincide con el registrado | "Revise su carpeta de 'Spam' o 'Correo no deseado'. Asegúrese de haber ingresado exactamente el mismo correo con el que se registró en la app. Espere unos minutos antes de solicitar un nuevo envío." | Si tras 15 minutos y 2 intentos con el correo correcto no recibe nada, solicitar el correo del usuario y escalar a soporte técnico. |
| "Sin conexión a internet" | El dispositivo no cuenta con señal de datos ni red Wi-Fi | "Para solicitar el restablecimiento de su clave necesita conexión a internet. Verifique su señal móvil o conéctese a una red Wi-Fi e intente nuevamente." | No escalar salvo que el cliente confirme tener conexión activa en otras aplicaciones. |
| "Círculo de espera infinito / Pantalla congelada en cargando" | Falla temporal de comunicación con el servicio de correo | "Espere 30 segundos. Si el botón de envío sigue bloqueado, cierre la aplicación desde el administrador de tareas de su celular (deslizando hacia arriba) y vuelva a abrirla para reintentar la solicitud." | Si al reintentar el círculo de espera vuelve a congelarse, transferir de inmediato a un asesor humano con el correo de la cuenta. |

### Directivas de Seguridad y Guardrails
- NUNCA solicite contraseñas temporales ni códigos privados de acceso al usuario a través del chat de WhatsApp.
- Indique siempre al usuario que el cambio de clave debe realizarlo él mismo de forma privada desde el enlace recibido en su correo electrónico.
- Si un trabajador o mayordomo solicita la clave del dueño de la finca, recuérdele amablemente que cada usuario debe tener su propia cuenta individual y no se pueden restablecer accesos ajenos.
