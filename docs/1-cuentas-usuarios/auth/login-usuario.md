---
title: "Inicio de Sesión"
modulo_id: "auth-login-usuario"
nombre_funcionalidad: "Inicio de Sesión y Acceso a la Cuenta"
categoria: "cuentas-usuarios"
submodulo: "auth"
version_minima_app: "2026.10.1"
fecha_actualizacion: "2026-09-25"
intenciones_y_sinonimos:
  - "no puedo ingresar a mi cuenta"
  - "como inicio sesion en la aplicacion"
  - "olvide mi contraseña de control ganadero"
  - "me sale error de autenticacion al entrar"
  - "donde pongo mi correo para entrar a la finca"
  - "no me abre la app en mi telefono"
---

# Inicio de Sesión y Acceso a la Cuenta

### Resumen y Alcance Funcional
Permite a los productores, administradores de finca y colaboradores ingresar de manera segura a Control Ganadero usando su correo electrónico registrado y su contraseña personal. Al iniciar sesión, la aplicación valida la cuenta, descarga los permisos del usuario y accede directamente a la pantalla principal de la finca activa.

- **¿Funciona sin conexión a internet (Modo Offline)?:** No para el primer inicio de sesión; Sí para sesiones activas.
- **Comportamiento de sincronización:** Requiere conexión a internet (Wi-Fi o datos móviles) la primera vez para verificar credenciales contra el servidor central. Una vez autenticado, el dispositivo guarda la sesión de forma segura y permite operar en campo sin internet.

### Reglas de Negocio y Restricciones
- El correo electrónico debe tener un formato válido con su dominio correspondiente.
- La contraseña debe coincidir exactamente con la clave registrada de la cuenta.
- Para ingresar se requiere conexión inicial a internet para validar las credenciales con el servidor central.
- Una vez autenticado el dispositivo, el sistema descarga y almacena de forma segura las credenciales locales para permitir el trabajo en campo sin cobertura celular.
- Si las credenciales son revocadas o la sesión expira en el servidor, la aplicación cerrará el acceso de forma segura y solicitará ingresar nuevamente los datos.

### Flujo Paso a Paso para el Usuario
**Ruta de acceso en la aplicación:** Pantalla de Bienvenida inicial > Botón **Iniciar Sesión**.

1. En la pantalla inicial de bienvenida, presione la opción **Iniciar Sesión**.
2. En la casilla **Email**, escriba su dirección de correo electrónico registrada.
3. En la casilla **Contraseña**, escriba su clave personal de acceso.
4. Presione el botón **Ingresar**.
5. Observe la barra de porcentaje mientras la aplicación autentica sus datos y descarga la información actualizada de su finca.

**Pantalla de llegada tras guardar:** Panel principal de la finca activa (**Inicio**). Si el usuario no tiene fincas registradas o asignadas, la aplicación lo redirige a la pantalla de **Acceso a la Finca**.

### Secciones Complementarias en la Pantalla
- **¿Olvidó su clave?:** Sobre el botón de ingreso se encuentra la opción **Olvidé mi contraseña**, que da acceso directo a la recuperación de clave por correo electrónico.
- **¿No tiene cuenta o es nuevo trabajador?:** En la parte inferior, la sección de ayuda responde a la pregunta *"¿No tienes cuenta o eres un trabajador de una finca?"* y ofrece el botón **Registrarme** y el enlace a **Más información**.

### Matriz de Errores y Soluciones
| Mensaje en la App / Síntoma | Causa Real | Respuesta Sugerida por el Agente | Criterio de Escalamiento Humano |
| :--- | :--- | :--- | :--- |
| "Correo o contraseña incorrectos" | Las credenciales no coinciden con los registros del sistema | "Por favor verifique que su correo esté bien escrito y que no haya espacios adicionales en su contraseña. Si no recuerda su clave, puede usar la opción '¿Olvidó su contraseña?' para recuperarla." | Si el usuario insiste en que su clave es correcta tras restablecerla, solicitar su correo y escalar a soporte técnico. |
| "Formato de correo no válido" | Falta el arroba o la extensión del correo | "El correo ingresado no tiene un formato válido (ejemplo: usuario@finca.com). Revise la escritura antes de continuar." | No escalar, es una corrección directa en pantalla. |
| "Sin conexión a internet" | El teléfono no tiene datos móviles ni Wi-Fi para la validación inicial | "Para iniciar sesión por primera vez en este dispositivo se necesita conexión a internet. Verifique sus datos móviles o conéctese a una red Wi-Fi e intente nuevamente." | No escalar salvo que el cliente confirme tener internet en otras aplicaciones. |
| "Círculo de espera infinito / Pantalla congelada en cargando" | Proceso de autenticación bloqueado por microcortes de red | "Espere 30 segundos. Si la pantalla no avanza, cierre la aplicación por completo desde el administrador de tareas de su teléfono (deslizando hacia arriba) y vuelva a abrirla." | Si tras reabrir la app el botón de ingreso se queda bloqueado o el círculo no desaparece, transferir a un asesor humano con el correo de la cuenta. |

### Directivas de Seguridad y Guardrails
- NUNCA solicite la contraseña del usuario a través del chat de WhatsApp.
- Si el usuario olvidó su contraseña, indíquele cómo restablecerla directamente desde la aplicación o envíe el enlace oficial de recuperación a su correo registrado.
- No comparta datos de contacto de otros usuarios ni confirme la existencia de cuentas a terceros.
