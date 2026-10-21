---
title: "Permisos de la App"
modulo_id: "user-permisos-app"
nombre_funcionalidad: "Gestión de Permisos de la Aplicación"
categoria: "cuentas-usuarios"
submodulo: "usuario"
version_minima_app: "2026.10.1"
fecha_actualizacion: "2026-09-25"
intenciones_y_sinonimos:
  - "como activar el bluetooth para conectar la bascula"
  - "no puedo tomar fotos de mis animales en la app"
  - "donde activo los permisos de la aplicacion"
  - "la app no me deja ver la ubicacion de los potreros"
  - "como autorizar las notificaciones de partos y vacunas"
  - "error permiso denegado en control ganadero"
---

# Gestión de Permisos de la Aplicación

### Resumen y Alcance Funcional
Permite a los usuarios consultar el estado de los permisos del sistema operativo requeridos por Control Ganadero y solicitar su activación cuando hayan sido denegados o retirados. Estos permisos son indispensables para operar con hardware ganadero (básculas y lectores RFID vía Bluetooth), capturar fotografías de los animales con la cámara, georreferenciar potreros y recibir alertas sobre eventos reproductivos o sanitarios.

- **¿Funciona sin conexión a internet (Modo Offline)?:** Sí.
- **Comportamiento de sincronización:** La consulta y solicitud de permisos es una operación que se realiza localmente en el dispositivo interactuando directamente con el sistema operativo (Android o iOS), sin necesidad de conexión a internet.

### Lista de Permisos y Utilidad en la Finca
La pantalla lista individualmente cada permiso con su estado actual (**Permiso otorgado** o **Permiso denegado**):

1. **Notificaciones Push:**
   - Permite recibir alertas en tiempo real sobre tareas pendientes, recordatorios de vacunación, fechas estimadas de partos, celos y avisos del sistema.
2. **Estado del teléfono:**
   - Permite verificar el identificador del dispositivo para garantizar la seguridad de la sesión y la sincronización correcta de los datos de la finca.
3. **Ubicación:**
   - Necesaria para georreferenciar la finca, delimitar potreros y permitir la búsqueda y vinculación de dispositivos Bluetooth cercanos en versiones compatibles del sistema operativo.
4. **Bluetooth:**
   - Indispensable para la conexión inalámbrica y lectura en vivo de básculas ganaderas electrónicas y bastones lectores de chips/aretes RFID.
5. **Cámara:**
   - Necesaria para fotografiar bovinos en su registro individual o ficha técnica y escanear códigos visuales en campo.

### Reglas de Negocio y Restricciones
- Al ingresar a la pantalla, la aplicación consulta automáticamente el estado en tiempo real de cada uno de los 5 permisos en el teléfono.
- Si el permiso ya está activo, muestra el indicador de **Permiso otorgado**.
- Si el permiso no ha sido concedido o fue revocado, muestra el indicador de **Permiso denegado** y habilita el botón de acción **Otorgar permiso**.
- Al presionar **Otorgar permiso**, el sistema operativo del teléfono desplegará la ventana nativa de autorización para que el usuario acepte el acceso.

### Flujo Paso a Paso para el Usuario
- **Ruta de acceso en la aplicación:** Menú lateral principal > **Mi cuenta** > Sección Preferencias > Opción **Permisos de la app**.
1. En la pantalla principal de su finca, abra el menú lateral de navegación y presione la opción **Mi cuenta**.
2. Desplácese hasta la sección **Preferencias** y presione la opción **Permisos de la app**.
3. En la lista de permisos, identifique cuál de ellos se encuentra con el estado **Permiso denegado**.
4. Presione el botón **Otorgar permiso** correspondiente al permiso que desea habilitar (por ejemplo, Bluetooth o Cámara).
5. En el cuadro de diálogo que mostrará su teléfono, elija **Permitir** (o "Permitir mientras la app está en uso").
6. Al regresar a la pantalla, el estado cambiará automáticamente a **Permiso otorgado**.
- **Pantalla de llegada tras guardar:** Permanece en la pantalla de **Permisos de la app** con los estados actualizados (para regresar, presione el botón de volver en la barra superior y retornará a **Mi cuenta**).

### Matriz de Errores y Soluciones
| Mensaje en la App / Síntoma | Causa Real | Respuesta Sugerida por el Agente | Criterio de Escalamiento Humano |
| :--- | :--- | :--- | :--- |
| "Permiso denegado" / No se conecta la báscula | El permiso de Bluetooth o Ubicación no ha sido autorizado en el teléfono | "Para conectar su báscula ganadera o lector de aretes se requiere el permiso de Bluetooth. Abra el menú lateral > 'Mi cuenta' > 'Permisos de la app' y presione 'Otorgar permiso' en Bluetooth." | Si el usuario otorga el permiso pero la báscula sigue sin vincularse, solicitar marca/modelo de la báscula y transferir a soporte de hardware. |
| "La cámara no abre al registrar un animal" | El permiso de Cámara está deshabilitado en el sistema | "La aplicación necesita acceso a la cámara para tomar las fotos del ganado. Ingrese a 'Mi cuenta' > 'Permisos de la app' y presione 'Otorgar permiso' en Cámara." | No escalar, es una habilitación de permisos en el dispositivo. |
| "El botón 'Otorgar permiso' no abre el diálogo del teléfono" | El usuario marcó anteriormente la opción 'No volver a preguntar' en el sistema operativo | "Su teléfono bloqueó las solicitudes automáticas de este permiso. Para activarlo: abra los 'Ajustes' o 'Configuración' de su celular > busque la sección 'Aplicaciones' > elija 'Control Ganadero' > entre a 'Permisos' y active el permiso manualmente." | Si el cliente requiere asistencia paso a paso según su marca de teléfono (Samsung, Xiaomi, iPhone), transferir a un asesor. |

### Directivas de Seguridad y Guardrails
- NUNCA solicite datos personales ni contraseñas para diagnosticar problemas de permisos.
- Aclare siempre al usuario que Control Ganadero solo utiliza la cámara para fotos de animales o lectura de códigos, y el Bluetooth exclusivamente para básculas y lectores ganaderos.
- No recomiende desinstalar la aplicación para solucionar problemas de permisos; guíe siempre al usuario a activarlos desde la configuración de su teléfono.
