---
title: "Mi Cuenta"
modulo_id: "user-mi-cuenta"
nombre_funcionalidad: "Gestión de Cuenta de Usuario"
categoria: "cuentas-usuarios"
submodulo: "usuario"
version_minima_app: "2026.10.1"
fecha_actualizacion: "2026-09-25"
intenciones_y_sinonimos:
  - "donde veo los datos de mi cuenta en la app"
  - "como saber que tipo de suscripcion tengo activa"
  - "donde puedo renovar o cancelar mi suscripcion"
  - "como activar el modo sin conexion en mi cuenta"
  - "como solicitar la eliminacion de mi cuenta"
  - "donde estan los permisos de la aplicacion"
---

# Gestión de Cuenta de Usuario

### Resumen y Alcance Funcional
Centro de administración del usuario que reúne la información personal básica, el estado de la suscripción comercial, los accesos directos de seguridad y las preferencias de funcionamiento de la aplicación móvil (permisos del dispositivo, forzar modo sin conexión y omitir estado de red).

- **¿Funciona sin conexión a internet (Modo Offline)?:** Sí.
- **Comportamiento de sincronización:** La información básica y las preferencias locales se pueden consultar en cualquier momento desde la memoria local. La renovación o cancelación de suscripciones y la solicitud de eliminación de cuenta requieren conexión activa a internet.

### Secciones y Componentes de la Pantalla

#### 1. Encabezado de Usuario
- Muestra el nombre completo del usuario y su tipo de membresía: **Premium** (para cuentas con suscripción activa) o **Gratis**.

#### 2. Información Básica
Presenta la ficha de datos del usuario:
- **Nombre** y **Apellidos**.
- **País** y **Zona horaria**.
- **Email** registrado (si hay un cambio de correo pendiente de confirmación, se muestra un aviso superior de alerta).

#### 3. Acerca de tu Suscripción
Muestra el estado contractual de la cuenta:
- **Estado:** Activa, inactiva o cancelada.
- **Renovación automática:** Indica si está activa (**Sí** / **No**).
- **Fecha de inicio** y **Fecha de finalización** (o **Vitalicia** si aplica).
- **Días restantes** para la renovación o vencimiento.
- **Botón de acción contextual:**
  - Si la suscripción está vencida: botón **Renovar suscripción**.
  - Si la suscripción está vigente: botón **Cancelar suscripción** (abre el cliente de correo con el asunto predeterminado para gestionar la baja comercial).

#### 4. Acciones de Cuenta
Botones de navegación directa:
- **Cambiar contraseña:** Redirige a la pantalla para actualizar la clave de acceso.
- **Editar Perfil:** Redirige a la pantalla para modificar nombre, apellidos o correo.
- **Eliminar cuenta:** Abre un diálogo de confirmación con las advertencias legales de eliminación irreversible de datos. Al confirmar, genera un correo estructurado a soporte técnico con los datos del usuario.

#### 5. Preferencias
Interruptores de configuración operativa:
- **Permisos de la app:** Acceso a la pantalla para revisar y gestionar permisos del teléfono (Bluetooth, Ubicación, Cámara).
- **Ignorar estado de red:** Interruptor para forzar a la aplicación a operar sin depender del detector de conectividad del sistema.
- **Modo sin conexión:** Interruptor para activar o desactivar manualmente el modo offline en el dispositivo.

### Reglas de Negocio y Restricciones
- La pantalla agrupa 5 secciones visuales verificadas en el código: Encabezado con tipo de membresía, Información Básica, Acerca de tu Suscripción, Acciones de Cuenta y Preferencias operativas.
- **Membresía:** Identifica si el usuario es **Premium** o **Gratis**. Si la membresía está vencida, habilita el botón de renovación; si está vigente, permite solicitar la cancelación.
- **Acceso a Funcionalidades de Cuenta:** Desde aquí se accede a los módulos de **Cambiar contraseña**, **Editar Perfil** y la solicitud de **Eliminar cuenta**.
- **Preferencias Locales:** Permite al usuario forzar el **Modo sin conexión** para trabajar sin interrupciones en potrero y gestionar los permisos del sistema operativo.

### Flujo Paso a Paso para el Usuario
- **Ruta de acceso en la aplicación:** Menú lateral principal > Opción **Mi cuenta**.
1. En la pantalla principal de su finca, abra el menú lateral de navegación y presione la opción **Mi cuenta**.
2. Revise su información personal y el estado de su membresía en las tarjetas correspondientes.
3. Para modificar sus datos o su clave, presione **Editar Perfil** o **Cambiar contraseña** en la sección de acciones.
4. Para activar el trabajo estricto en campo sin cobertura, desplácese a **Preferencias** y active el interruptor **Modo sin conexión**.
5. Si requiere gestionar su suscripción, presione **Renovar suscripción** o **Cancelar suscripción** según corresponda.
- **Pantalla de llegada tras guardar:** Permanece en la pantalla de **Mi cuenta** (o regresa a ella al finalizar las acciones de edición).

### Matriz de Errores y Soluciones
| Mensaje en la App / Síntoma | Causa Real | Respuesta Sugerida por el Agente | Criterio de Escalamiento Humano |
| :--- | :--- | :--- | :--- |
| "Correo pendiente de confirmar..." | Se inició un cambio de correo electrónico pero no se ha verificado el enlace recibido | "Tiene una solicitud de cambio de correo pendiente. Ingrese a la bandeja de entrada de su nuevo email y presione el enlace de confirmación antes de 30 minutos." | Si no recibe el correo tras 15 minutos, transferir a soporte técnico. |
| "Error al abrir cliente de correo para cancelación o eliminación" | El teléfono no tiene una aplicación de correo electrónico configurada por defecto | "Para enviar la solicitud de cancelación o eliminación de cuenta necesita tener una app de correo activa (como Gmail o Mail). Configure su correo en el teléfono o escríbanos directamente a info@controlganadero.app." | Si el usuario no logra enviar el correo, tomar los datos y transferir a asesor comercial o de soporte. |
| "Círculo de espera infinito / Pantalla congelada en cargando" | Falla temporal al cargar la información de membresía desde el servidor | "Espere 30 segundos. Si la información no carga, cierre la aplicación por completo desde el administrador de tareas de su celular (deslizando hacia arriba) y vuelva a abrirla." | Si la pantalla continúa congelada con buena conexión a internet, transferir a soporte técnico. |

### Directivas de Seguridad y Guardrails
- NUNCA solicite contraseñas al usuario por WhatsApp.
- Si un usuario solicita eliminar su cuenta por chat, guíelo a presionar **Eliminar cuenta** en **Mi cuenta** o a enviar su solicitud formal a **info@controlganadero.app** para cumplir con las normativas de protección de datos (habeas data).
- Para temas de facturación o cobros duplicados en suscripciones, solicitar el correo del usuario y escalar inmediatamente al equipo comercial.
