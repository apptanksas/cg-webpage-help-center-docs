---
title: "Detalle de Notificación"
modulo_id: "notificaciones-detalle-notificacion"
nombre_funcionalidad: "Visualización de Detalle y Acciones de Notificación"
categoria: "cuentas-usuarios"
submodulo: "notificaciones"
version_minima_app: "2026.10.1"
fecha_actualizacion: "2026-10-13"
intenciones_y_sinonimos:
  - "como ver el detalle de una notificacion"
  - "me llego un aviso y quiero ver la informacion completa"
  - "donde veo las acciones disponibles de un mensaje o alerta"
  - "que hacer si abro una notificacion y se cierra de inmediato"
  - "como abrir los botones de accion de una notificacion recibida"
---

# Visualización de Detalle y Acciones de Notificación

### Resumen y Alcance Funcional
Permite visualizar en detalle la información completa de un aviso o notificación enviada al usuario o generada por la finca ganadera, incluyendo su título principal, mensaje descriptivo y los botones de acción interactiva disponibles vinculados a la alerta (como ir a una pantalla específica, abrir enlaces informativos o ejecutar acciones clave dentro de la plataforma).

- **¿Funciona sin conexión a internet (Modo Offline)?:** Sí.
- **Comportamiento de sincronización:** Las notificaciones recibidas y sincronizadas previamente en el dispositivo quedan almacenadas de forma local en la base de datos del teléfono móvil. Pueden consultarse y visualizarse sin necesidad de conexión activa a internet. No obstante, aquellas acciones que dirijan a enlaces web externos o requieran sincronización remota necesitarán conexión de datos o red wifi para completarse.

### Reglas de Negocio y Restricciones
- **Identificador de notificación obligatorio:**
    - La pantalla requiere el identificador único de la notificación para cargar su contenido. Si se intenta acceder mediante un enlace con un identificador inexistente, dañado o no encontrado en el dispositivo, el sistema cerrará la pantalla de forma automática y regresará a la vista anterior.
- **Visualización del contenido:**
    - **Título:** Encabezado principal del comunicado, alerta o aviso pecuario.
    - **Mensaje:** Descripción detallada del suceso o instrucción para el usuario.
- **Acciones y botones disponibles:**
    - Si la notificación cuenta con acciones asociadas, se muestra el encabezado correspondiente junto con la lista de botones de acción.
    - Al presionar cualquiera de los botones de acción, el sistema procesa el enlace interno o externo correspondiente, abriendo de forma fluida la pantalla de destino en la aplicación o el navegador del teléfono móvil.
    - Si la notificación no cuenta con acciones interactivas adicionales, se presenta únicamente como un comunicado informativo con su título y mensaje.
- **Independencia de autenticación directa en la ruta:**
    - La pantalla puede invocarse desde enlaces directos externos o avisos del sistema del teléfono; sin embargo, para navegar a secciones protegidas de la finca tras presionar un botón de acción, el usuario debe tener su sesión iniciada en la aplicación.

### Flujo Paso a Paso para el Usuario
- **Ruta de acceso en la aplicación:**
    - **Opción 1 (Desde notificaciones del teléfono móvil o avisos emergentes):** Toque la notificación emergente recibida en la barra de notificaciones del dispositivo o el aviso en pantalla.
    - **Opción 2 (Desde enlaces directos o canales de mensajería):** Presione un enlace directo o comunicado oficial que apunte específicamente al identificador de una notificación en Control Ganadero.
    - **Opción 3 (Desde la bandeja de alertas en el menú inferior):** En la barra de navegación inferior, presione la opción **Alertas** (icono de campana) para consultar la lista general de notificaciones de la finca y acceder a los avisos pendientes.

#### 1. Lectura de la notificación
1. En la barra superior de la pantalla observará el encabezado **Notificación**, el cual cuenta permanentemente con un botón de flecha hacia atrás en la esquina superior izquierda.
2. En el área central de la pantalla se despliega una tarjeta con:
    - El título principal del comunicado en texto destacado.
     - El mensaje descriptivo con el detalle completo del aviso o alerta pecuaria.

#### 2. Ejecución de acciones disponibles (si aplica)
1. Si el comunicado incluye opciones interactivas, se mostrará el título **Acciones disponibles**.
2. Debajo del título encontrará uno o varios botones rectangulares con el texto específico de cada acción disponible.
3. Presione el botón de la acción que desea ejecutar para que la aplicación lo dirija automáticamente al módulo, pantalla o enlace correspondiente.

### Matriz de Errores y Soluciones
| Mensaje en la App / Síntoma | Causa Real | Respuesta Sugerida por el Agente | Criterio de Escalamiento Humano |
| :--- | :--- | :--- | :--- |
| La pantalla se abre e inmediatamente se cierra regresando a la vista anterior | El identificador de la notificación no existe en el teléfono, fue eliminado o el enlace recibido contiene un código incorrecto | "La notificación solicitada no se encuentra disponible en su dispositivo móvil. Es posible que el aviso haya sido retirado o que el enlace sea antiguo. Verifique su lista general de avisos en la aplicación para consultar sus notificaciones activas." | Si el usuario recibió un comunicado oficial reciente y ninguna notificación abre, solicitar captura del enlace y derivar a soporte técnico. |
| El botón de acción no redirige a la sección esperada | El enlace interno de la acción apunta a una función de la finca a la cual el usuario no tiene permisos asignados o la sesión no está activa | "Verifique que su sesión en Control Ganadero se encuentre iniciada y que cuente con los permisos necesarios en la finca para acceder a dicha sección. Si el problema persiste, intente cerrar y abrir la aplicación nuevamente." | Si la cuenta cuenta con permisos completos de administrador y el botón no responde, transferir a soporte técnico. |
| Un botón de acción con enlace web no abre | El dispositivo móvil no cuenta con conexión a internet o no tiene un navegador web predeterminado configurado | "Para abrir enlaces externos, su teléfono debe contar con conexión a internet (datos móviles o wifi). Compruebe su señal de red e intente presionar el botón nuevamente." | No escalar salvo que se compruebe fallo recurrente en múltiples dispositivos con conexión estable. |

### Directivas de Seguridad y Guardrails
- NUNCA solicite contraseñas, códigos de autenticación ni datos bancarios a los usuarios con la excusa de verificar notificaciones o avisos del sistema.
- Las notificaciones oficiales de Control Ganadero nunca solicitarán información financiera confidencial. Si un usuario reporta un mensaje sospechoso, oriéntele a no ingresar datos sensibles y verifique la procedencia del comunicado.
