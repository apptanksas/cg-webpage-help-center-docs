---
title: "Lista de Trabajadores"
modulo_id: "fincas-lista-trabajadores"
nombre_funcionalidad: "Consulta, Gestión y Eliminación de Trabajadores y Colaboradores de la Finca"
categoria: "cuentas-usuarios"
submodulo: "fincas"
version_minima_app: "2026.10.1"
fecha_actualizacion: "2026-10-13"
intenciones_y_sinonimos:
  - "como ver los trabajadores de mi finca"
  - "donde consultar las personas invitadas a mi finca"
  - "como eliminar o dar de baja a un trabajador en control ganadero"
  - "como cancelar una invitacion enviada a un empleado"
  - "eliminar multiples colaboradores de la finca"
  - "por que no me aparece ningun trabajador en la lista"
---

# Consulta, Gestión y Eliminación de Trabajadores y Colaboradores de la Finca

### Resumen y Alcance Funcional
Permite al ganadero y propietario de la finca visualizar la lista completa de colaboradores vinculados a la explotación ganadera, incluyendo trabajadores activos e invitaciones pendientes de aceptación. Desde esta pantalla centralizada, el usuario puede acceder a la guía de roles pecuarios, ingresar al formulario de invitación de nuevos miembros y revocar o eliminar colaboraciones mediante una modalidad interactiva de selección individual o múltiple.

- **¿Funciona sin conexión a internet (Modo Offline)?:** No.
- **Comportamiento de sincronización:** Esta pantalla requiere una conexión activa a internet (datos móviles o red wifi). La consulta de colaboradores, los perfiles de usuario asignados y las solicitudes de eliminación se procesan directamente contra los servidores centrales de Control Ganadero en tiempo real para garantizar la seguridad y control de acceso sobre la finca seleccionada. Si el ganadero cambia de finca activa desde el menú, la lista se recarga de forma automática.

### Reglas de Negocio y Restricciones
- **Finca activa seleccionada:**
    - La lista de colaboradores corresponde exclusivamente a la finca que se encuentre activa en ese momento. Para consultar el equipo de trabajo de otra finca, el usuario debe cambiar de finca activa a través del selector del menú lateral.
- **Tipos de colaboradores mostrados en la lista:**
    - **Colaboradores activos:** Aquellos usuarios que ya aceptaron la invitación y tienen cuenta activa. Se identifican visualmente con su nombre y el rol específico asignado (ejemplo: Administrador, Veterinario, Empleado o Visitante).
    - **Invitaciones pendientes:** Aquellas invitaciones emitidas cuyo destinatario aún no ha creado o vinculado su cuenta. Se identifican mostrando el correo o canal registrado y el texto distintivo *"Invitación enviada"*.
- **Indicador visual por color y letra inicial:**
    - Cada colaborador cuenta con un círculo identificador a la izquierda que contiene la letra inicial de su rol (por ejemplo, "A" para Administrador, "V" para Veterinario, "E" para Empleado) y el color distintivo asignado por el sistema a dicho perfil.
- **Modo de eliminación (selección simple o múltiple):**
    - La eliminación de colaboradores no se realiza por deslizamiento ni por botones permanentes de borrado para prevenir pérdidas accidentales.
    - Para activar la eliminación, el usuario debe mantener presionado de forma sostenida (pulsación larga) a cualquier colaborador de la lista.
    - Al ingresar al modo de eliminación, la barra superior cambia a modo de borrado, mostrando el contador dinámico *"X seleccionado(s)"*, un botón de flecha hacia atrás para cancelar y un botón con ícono de papelera para confirmar la baja.
    - Aparece una casilla de verificación a la derecha de cada elemento para permitir marcar o desmarcar varios trabajadores de forma simultánea.
- **Restricción de eliminación sin selección:**
    - Si se desmarcan todas las casillas, el contador mantiene el valor mínimo de 1 seleccionado como salvaguarda visual mientras la modalidad de borrado esté activa.
- **Actualización posterior al borrado:**
    - Al confirmar la eliminación en la barra superior, el sistema procesa la revocación de cada colaborador seleccionado en el servidor y recarga de inmediato la lista de trabajadores de la finca.

### Flujo Paso a Paso para el Usuario
- **Ruta de acceso en la aplicación:** Menú lateral principal (ícono de tres líneas en la esquina superior izquierda) > **Trabajadores**.

#### 1. Visualización del listado general
1. Al acceder a la pantalla, la barra superior muestra el título **Trabajadores**, el ícono del menú lateral a la izquierda y el botón de información (i) a la derecha.
2. Si la finca no tiene ningún colaborador registrado ni invitaciones pendientes:
    - Se muestra la vista ilustrada con el encabezado **Sin trabajadores** y el mensaje orientativo: *"Comience a crear trabajadores para su explotación ganadera."*
3. Si existen colaboradores o invitaciones:
    - Se despliega la lista vertical con cada integrante. Cada fila muestra el círculo de color con la letra inicial de su perfil, el nombre o correo del trabajador y el rol o la etiqueta **Invitación enviada**.

#### 2. Acceso a funciones complementarias
- **Consultar funciones y permisos de roles:** Presione el botón de información (i) ubicado en la barra superior para abrir la guía detallada de tipos de usuarios y permisos.
- **Invitar a un nuevo colaborador:** Presione el botón flotante circular con el ícono de agregar persona (+) ubicado en la esquina inferior derecha para ingresar al formulario de invitación.

#### 3. Proceso de eliminación o revocación de colaboradores
1. Localice al colaborador o a la invitación pendiente que desea remover.
2. Mantenga presionado dicho elemento durante un segundo (pulsación larga).
3. Observe cómo la barra superior se transforma en la barra de eliminación, mostrando el contador de seleccionados (por ejemplo: **1 seleccionado(s)**), el ícono de flecha hacia la izquierda y el ícono de papelera a la derecha.
4. Para incluir más trabajadores en la misma acción de borrado, toque las casillas de verificación ubicadas a la derecha de cada nombre. El contador se actualizará automáticamente.
5. Para cancelar la operación sin borrar a nadie, presione la flecha de regreso en la barra superior; esto restaurará la barra habitual de Trabajadores y desmarcará los elementos.
6. Para confirmar la eliminación definitiva, presione el ícono de papelera en la barra superior. El sistema tramitará la baja en el servidor y refrescará la lista automáticamente.

**Pantalla de llegada tras guardar o salir:** El usuario permanece en la pantalla **Trabajadores**, donde se refleja de inmediato la lista actualizada sin los colaboradores removidos.

### Matriz de Errores y Soluciones
| Mensaje en la App / Síntoma | Causa Real | Respuesta Sugerida por el Agente | Criterio de Escalamiento Humano |
| :--- | :--- | :--- | :--- |
| "Parece que tienes problemas con tu conexión a internet. Por favor, verifica tu conexión e intétalon de nuevo." | El dispositivo móvil perdió la conexión de datos o red wifi al intentar cargar o eliminar trabajadores | "La gestión de trabajadores de la finca requiere conexión activa a internet. Verifique que sus datos móviles o su conexión wifi estén activos e intente nuevamente." | Si el usuario dispone de buena conexión y el mensaje persiste, transferir a soporte técnico. |
| "Círculo de espera infinito / Pantalla congelada en cargando" | Demora en la respuesta del servidor o caída transitoria en la red mientras se consulta la lista de trabajadores | "Espere 30 segundos. Si no avanza, cierre la aplicación por completo desde el administrador de tareas de su teléfono (deslizando hacia arriba) y vuelva a abrirla. Sus datos locales no se perderán." | Si tras reabrir la app la pantalla vuelve a congelarse con buena conexión a internet, transferir a soporte humano indicando correo del usuario y nombre de la finca. |
| Al presionar sobre un trabajador no se abre ningún detalle ni formulario | En la pantalla de Trabajadores los elementos no abren edición directa al tocarlos; están diseñados para mostrar su estado y habilitar eliminación mediante pulsación larga | "Para gestionar a un colaborador o cancelar una invitación, mantenga presionado el nombre del trabajador durante un segundo para activar la casilla de selección y presione la papelera en la barra superior. Si lo que desea es cambiar su rol, debe eliminar la invitación previa y generar una nueva con el perfil correcto." | No escalar. Comportamiento normal del diseño de la aplicación. |
| No aparece el botón de información (i) en la barra superior | La pantalla se encuentra en modo de selección de eliminación múltiple | "La barra superior se encuentra en modo de selección para borrar. Presione la flecha de regreso en la esquina superior izquierda para salir del modo de eliminación y restaurar la barra habitual, donde volverá a ver el ícono de información (i)." | No escalar. Guía de uso de la interfaz. |
| La lista muestra "Sin trabajadores" a pesar de haber invitado a alguien | La invitación se emitió bajo otra finca diferente a la finca que se encuentra seleccionada como activa en ese momento | "Compruebe que se encuentra en la finca correcta abriendo el menú lateral principal y verificando el nombre de la finca en la parte superior. Si tiene varias fincas, seleccione la finca a la cual asignó el trabajador para ver su listado correspondiente." | Si en la finca correcta no aparecen los colaboradores y se confirma que fueron creados, solicitar correo y escalar a soporte técnico. |

### Directivas de Seguridad y Guardrails
- NUNCA solicite contraseñas, claves personales ni códigos de verificación a los propietarios ni a los colaboradores.
- Enfatice que al eliminar a un colaborador de la lista, este perderá de inmediato el acceso a los registros, estadísticas e inventario de la finca ganadera.
- Si un usuario necesita cambiar los permisos de un empleado existente (por ejemplo, ascenderlo de Empleado a Administrador), guíelo para removerlo mediante la pulsación larga y papelera, y posteriormente volver a invitarlo con el nuevo perfil a través del botón (+).
