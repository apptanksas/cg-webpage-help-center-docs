---
title: "Mi Cuenta"
modulo_id: "user-mi-cuenta"
nombre_funcionalidad: "Gestión de Cuenta de Usuario"
tipo_documento: "guia-app"
categoria: "cuentas-usuarios"
submodulo: "usuario"
version_minima_app: "2026.10.1"
confianza_reglas: "verificada-con-tests"
fecha_actualizacion: "2026-11-04"
intenciones_y_sinonimos:
  - "donde veo los datos de mi cuenta en la app"
  - "como saber que tipo de suscripcion tengo activa"
  - "donde puedo renovar o cancelar mi suscripcion"
  - "donde ver mi cuota de trazabilidad animal y cupos disponibles"
  - "como aumentar el cupo de identificacion electronica de animales"
  - "como generar un volcado de datos locales o aplicar un parche"
---

# Gestión de Cuenta de Usuario

### Resumen y Alcance Funcional
Centro de administración del usuario que reúne la información personal básica, el estado de la suscripción comercial, el control de la cuota de trazabilidad animal, los accesos directos de seguridad, las herramientas de diagnóstico técnico y las preferencias de funcionamiento de la aplicación móvil (permisos del dispositivo, forzar modo sin conexión y herramientas de volcado de datos).

- **Especies a las que aplica:** Aplica igual para todas las especies.
- **¿Funciona sin conexión a internet (Modo Offline)?:** Sí.
- **Comportamiento de sincronización:** La información básica, el resumen de cuotas locales y las preferencias se pueden consultar en cualquier momento desde la memoria local. La renovación o cancelación de suscripciones, la compra de cupos de trazabilidad, la subida de volcados de datos locales y la solicitud de eliminación de cuenta requieren conexión activa a internet.

### Secciones y Componentes de la Pantalla

#### 1. Encabezado de Usuario
- Muestra el nombre completo del usuario y su tipo de membresía: "Premium" (para cuentas con suscripción activa) o "Gratis".

#### 2. Información Básica
Presenta la ficha de datos del usuario:
- "Nombre" y "Apellidos".
- "País" y "Zona horaria".
- "Email" registrado (si hay un cambio de correo pendiente de confirmación, se muestra un aviso superior de alerta).

#### 3. Acerca de tu Suscripción
Muestra el estado contractual de la cuenta:
- "Estado": Activa, inactiva o cancelada.
- "Renovación automática": Indica si está activa ("Sí" / "No").
- "Fecha de inicio" y "Fecha de finalización" (o "Vitalicia" si aplica).
- "Días restantes" para la renovación o vencimiento.
- Botón de acción contextual:
    - Si la suscripción está vencida: botón "Renovar suscripción".
    - Si la suscripción está vigente: botón "Cancelar suscripción" (abre el cliente de correo con el asunto predeterminado para gestionar la baja comercial).

#### 4. Cuota de Trazabilidad Animal
Panel informativo que supervisa la disponibilidad de cupos de identificación electrónica (aretes RFID, microchips y códigos QR) asignados a la cuenta del usuario:
- "Capacidad utilizada": Barra porcentual y gráfica de uso de cupos de trazabilidad.
- "Disponibilidad" / "Agotado": Indicador del estado de cupos libres.
- "Con trazabilidad": Cantidad de animales con identificación electrónica vinculada actualmente.
- "Cupos": Número total de cupos contratados o disponibles en la cuenta.
- Botón "Aumentar cupo": Redirige a la pantalla de adquisición y compra de paquetes de trazabilidad animal.

#### 5. Acciones de Cuenta
Botones de navegación directa:
- "Cambiar contraseña": Redirige a la pantalla para actualizar la clave de acceso.
- "Editar Perfil": Redirige a la pantalla para modificar nombre, apellidos o correo.
- "Eliminar cuenta": Abre un diálogo de confirmación con las advertencias legales de eliminación irreversible de datos. Al confirmar, genera un correo estructurado a soporte técnico con los datos del usuario.

#### 6. Preferencias y Diagnóstico
Interruptores de configuración operativa y utilidades de soporte:
- "Permisos de la app": Acceso a la pantalla para revisar y gestionar permisos del teléfono (Bluetooth, Ubicación, Cámara).
- "Ignorar estado de red": Interruptor para forzar a la aplicación a operar sin depender del detector de conectividad del sistema.
- "Modo sin conexión": Interruptor para activar o desactivar manualmente el modo offline en el dispositivo.
- "Herramientas de diagnóstico": Diálogo técnico para soporte avanzado que permite:
    - "Volcado de datos locales": Genera y sube una copia de la base de datos local a los servidores de soporte técnico para resolver incidencias de sincronización. Permite incluir datos sensibles mediante confirmación de contraseña.
    - "Descargar y aplicar parche": Permite descargar y aplicar correcciones remotas de datos enviadas por el equipo de ingeniería.

### Reglas de Negocio y Restricciones
- La pantalla agrupa las secciones visuales verificadas en el código: Encabezado con tipo de membresía, Información Básica, Acerca de tu Suscripción, Cuota de Trazabilidad Animal, Acciones de Cuenta, Preferencias y Herramientas de Diagnóstico.
- **Membresía:** Identifica si el usuario es "Premium" o "Gratis". Si la membresía está vencida, habilita el botón de renovación; si está vigente, permite solicitar la cancelación.
- **Cuotas de trazabilidad:** El panel calcula el porcentaje de cupos consumidos. Si la cuota llega a su límite máximo, el estado cambia a "Agotado" y bloquea nuevas vinculaciones de identificadores electrónicos en los formularios de animales hasta presionar "Aumentar cupo" y adquirir nuevos paquetes.
- **Herramientas de diagnóstico:** Para subir volcados que incluyan datos sensibles, el sistema solicita la contraseña del usuario mediante un diálogo de seguridad ("Contraseña requerida") antes de autorizar la carga al servidor de soporte.

### Flujo Paso a Paso para el Usuario
- **Ruta de acceso en la aplicación:** Menú lateral principal > Opción "Mi cuenta".

1. En la pantalla principal de su finca, abra el menú lateral de navegación y presione la opción "Mi cuenta".
2. Revise su información personal, el estado de su membresía y el consumo en "Cuota de trazabilidad animal".
3. Para ampliar su cupo de identificación electrónica, presione el botón "Aumentar cupo".
4. Para modificar sus datos o su clave, presione "Editar Perfil" o "Cambiar contraseña" en la sección de acciones.
5. Para activar el trabajo estricto en campo sin cobertura, desplácese a "Preferencias" y active el interruptor "Modo sin conexión".
6. Si un asesor de soporte técnico le solicita un diagnóstico, presione "Herramientas de diagnóstico", elija "Volcado de datos locales", confirme con su contraseña si se requieren datos sensibles y presione "Subir datos".
7. Si requiere gestionar su suscripción, presione "Renovar suscripción" o "Cancelar suscripción" según corresponda.
- **Pantalla de llegada tras guardar:** Permanece en la pantalla de "Mi cuenta" (o regresa a ella al finalizar las acciones de edición o diagnóstico).

### Matriz de Errores y Soluciones
| Mensaje en la App / Síntoma | Causa Real | Respuesta Sugerida por el Agente | Criterio de Escalamiento Humano |
| :--- | :--- | :--- | :--- |
| "Correo pendiente de confirmar..." | Se inició un cambio de correo electrónico pero no se ha verificado el enlace recibido | "Tiene una solicitud de cambio de correo pendiente. Ingrese a la bandeja de entrada de su nuevo email y presione el enlace de confirmación antes de 30 minutos." | Si no recibe el correo tras 15 minutos, transferir a soporte técnico. |
| "Error al abrir cliente de correo para cancelación o eliminación" | El teléfono no tiene una aplicación de correo electrónico configurada por defecto | "Para enviar la solicitud de cancelación o eliminación de cuenta necesita tener una app de correo activa (como Gmail o Mail). Configure su correo en el teléfono o escríbanos directamente a info@controlganadero.app." | Si el usuario no logra enviar el correo, tomar los datos y transferir a asesor comercial o de soporte. |
| "Contraseña incorrecta" en herramientas de diagnóstico | Se ingresó una clave errónea al autorizar la subida del volcado con datos sensibles | "La contraseña ingresada no coincide con la de su cuenta. Por favor escriba su clave actual para autorizar la subida segura del diagnóstico a soporte técnico." | No escalar, validación de autenticación de seguridad. |
| "Agotado" en Cuota de trazabilidad animal | Se han utilizado todos los cupos de identificación electrónica contratados en la cuenta | "Ha utilizado el total de cupos de trazabilidad disponibles en su cuenta. Presione el botón 'Aumentar cupo' para adquirir paquetes adicionales de trazabilidad electrónica." | Si el usuario ya realizó el pago de cupos y no se reflejan, solicitar el comprobante y transferir a facturación. |

### Directivas de Seguridad y Guardrails
- NUNCA solicite contraseñas al usuario por WhatsApp ni canales de soporte.
- La confirmación de contraseña en las herramientas de diagnóstico se realiza exclusivamente dentro de la aplicación móvil y nunca debe ser compartida al asesor.
- Si un usuario solicita eliminar su cuenta por chat, guíelo a presionar "Eliminar cuenta" en "Mi cuenta" o a enviar su solicitud formal a "info@controlganadero.app" para cumplir con las normativas de protección de datos (habeas data).
- Para temas de facturación o cobros duplicados en suscripciones o paquetes de trazabilidad, solicitar el correo del usuario y escalar inmediatamente al equipo comercial.
