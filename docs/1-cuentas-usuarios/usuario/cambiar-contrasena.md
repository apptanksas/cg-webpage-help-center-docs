---
title: "Cambiar Contraseña"
modulo_id: "user-cambiar-contrasena"
nombre_funcionalidad: "Cambio de Contraseña de Usuario"
categoria: "cuentas-usuarios"
submodulo: "usuario"
version_minima_app: "2026.10.1"
fecha_actualizacion: "2026-09-25"
intenciones_y_sinonimos:
  - "como cambio mi clave desde la aplicacion"
  - "donde actualizo mi contrasena de control ganadero"
  - "quiero cambiar la clave por seguridad"
  - "error al cambiar mi contrasena la clave actual no coincide"
  - "requisitos para la nueva clave de acceso"
  - "no me deja guardar la nueva contrasena"
---

# Cambio de Contraseña de Usuario

### Resumen y Alcance Funcional
Permite a los usuarios con sesión activa actualizar su clave de acceso de manera segura desde la configuración de su perfil. Por motivos de seguridad y verificación de identidad, el sistema exige comprobar la contraseña actual antes de registrar y encriptar la nueva clave en los servidores centrales.

- **¿Funciona sin conexión a internet (Modo Offline)?:** No.
- **Comportamiento de sincronización:** Requiere conexión a internet activa (Wi-Fi o datos móviles) para validar la contraseña actual contra el servidor de autenticación y registrar la nueva clave de forma segura e inmediata en la nube.

### Reglas de Negocio y Restricciones
- La **Contraseña actual** ingresada debe coincidir exactamente con la clave vigente de la cuenta.
- La **Nueva contraseña** debe ser distinta a la anterior y cumplir con los criterios de seguridad del sistema (longitud mínima requerida).
- La **Confirmación de contraseña** debe coincidir carácter por carácter con la nueva contraseña digitada.
- Si los datos son correctos, el sistema actualiza las credenciales en la nube y actualiza la sesión local sin desloguear al usuario de su finca.
- Si la contraseña actual no coincide, la solicitud es rechazada para prevenir cambios no autorizados en caso de préstamo del dispositivo.

### Flujo Paso a Paso para el Usuario
- **Ruta de acceso en la aplicación:** Menú lateral principal > **Mi cuenta** > Sección Preferencias de cuenta > Opción **Cambiar contraseña**.
1. En la pantalla principal de su finca, abra el menú lateral de navegación y presione la opción **Mi cuenta**.
2. En la pantalla de información de su cuenta, desplácese hasta la sección de acciones de cuenta.
3. Presione la opción **Cambiar contraseña**.
4. En el formulario de actualización, complete los tres campos requeridos:
      - **Contraseña actual:** Escriba la clave vigente con la que accede a la aplicación.
     - **Nueva contraseña:** Escriba su nueva clave de seguridad (mínimo 8 caracteres).
     - **Confirmar nueva contraseña:** Vuelva a escribir la nueva clave para verificar que coincida exactamente.
5. Presione el botón **Actualizar contraseña**.
6. La aplicación guardará los cambios y mostrará la confirmación de contraseña actualizada.

**Pantalla de llegada tras guardar:** Pantalla de **Mi cuenta** (regresa a la vista general de la cuenta de usuario).

### Matriz de Errores y Soluciones
| Mensaje en la App / Síntoma | Causa Real | Respuesta Sugerida por el Agente | Criterio de Escalamiento Humano |
| :--- | :--- | :--- | :--- |
| "La contraseña actual no es correcta" | La clave anterior digitada no coincide con los registros del sistema | "La contraseña actual ingresada no coincide con su clave registrada. Verifique que no haya espacios adicionales ni mayúsculas no deseadas. Si olvidó su clave actual, cierre sesión y utilice la opción 'Olvidé mi contraseña' para restablecerla por correo." | Si el usuario afirma que su clave actual es correcta pero el sistema la rechaza, transferir a soporte técnico con su correo. |
| "Las contraseñas no coinciden" | La confirmación de contraseña no es idéntica a la nueva contraseña | "La confirmación no coincide exactamente con la nueva clave escrita. Revise ambos campos con atención antes de presionar guardar." | No escalar, es una corrección directa en pantalla. |
| "La contraseña debe tener al menos 8 caracteres" | La nueva contraseña no cumple con la longitud mínima de seguridad | "Por seguridad de la información de su finca, su nueva contraseña debe tener un mínimo de 8 caracteres. Intente con una combinación más larga y segura." | No escalar, cumplimiento de directiva de seguridad. |
| "Sin conexión a internet" | No hay cobertura celular de datos ni red Wi-Fi disponible | "Para actualizar su clave de acceso se requiere conexión a internet para sincronizar con el servidor central. Conéctese a una red Wi-Fi o active sus datos móviles e intente nuevamente." | No escalar salvo que el usuario confirme tener internet en otras aplicaciones. |
| "Círculo de espera infinito / Pantalla congelada en cargando" | Microcorte de red durante el proceso de encriptación y envío a la nube | "Espere 30 segundos. Si el botón de guardado sigue bloqueado, cierre la aplicación por completo desde el administrador de tareas de su celular (deslizando hacia arriba) y vuelva a abrirla para reintentar la actualización." | Si tras reabrir la app el formulario vuelve a bloquearse con buena conexión Wi-Fi, transferir de inmediato a soporte humano con correo y modelo del teléfono. |

### Directivas de Seguridad y Guardrails
- NUNCA solicite la contraseña actual ni la nueva contraseña del usuario por el chat de WhatsApp.
- Indique siempre al usuario que el cambio de clave es un procedimiento estrictamente personal que debe realizar él mismo dentro de la aplicación móvil.
- Si un trabajador o colaborador solicita cambiar la contraseña de la finca, recuérdele que cada usuario debe tener su propia cuenta individual y no debe compartir claves maestras.
