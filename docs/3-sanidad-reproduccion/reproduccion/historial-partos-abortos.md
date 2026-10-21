---
title: "Partos y Abortos"
modulo_id: "animal-partos-abortos-tabla"
nombre_funcionalidad: "Historial de Partos y Abortos"
categoria: "sanidad-reproduccion"
submodulo: "reproduccion"
version_minima_app: "2026.10.1"
fecha_actualizacion: "2026-10-05"
intenciones_y_sinonimos:
  - "como ver todos los partos y abortos de una vaca"
  - "tabla de crias y perdidas de prenez de una hembra"
  - "registrar nuevo ternero desde la lista de partos"
  - "ver la ficha de la cria desde los partos de la madre"
  - "editar un aborto desde el historial de eventos reproductivos"
  - "por que no aparecen los datos de una cria en la tabla de partos"
---

# Historial de Partos y Abortos

### Resumen y Alcance Funcional
Pantalla de consulta zootécnica que consolida en formato de tabla el historial completo de partos culminados y abortos ocurridos en una hembra de la finca ganadera. Permite al productor y al equipo de campo auditar la trayectoria de maternidad del ejemplar, identificar el tipo de evento, conocer el sexo de la cría o del feto, acceder directamente a la hoja de vida de las crías nacidas vivas y abrir la edición de cualquier registro de aborto. Asimismo, cuenta con un acceso rápido para registrar el nacimiento de un nuevo animal asignando a la hembra automáticamente como madre.

- **¿Funciona sin conexión a internet (Modo Offline)?:** Sí, la pantalla consulta la información consolidada de crías, abortos y hechos reproductivos almacenada localmente en la base de datos del dispositivo móvil.
- **Comportamiento de sincronización:** Las consultas y transiciones de pantalla funcionan de inmediato sin necesidad de señal. Cualquier edición de abortos o registro de crías realizado desde esta vista se guarda localmente y se sincroniza automáticamente con la nube en cuanto el dispositivo recupere la conexión a internet.

### Reglas de Negocio y Restricciones
- **Consolidación y orden cronológico de eventos:**
  - La tabla reúne los datos provenientes de tres fuentes zootécnicas: crías registradas asociadas a la madre, eventos de abortos guardados y hechos de partos asentados en el sistema.
  - Los registros se ordenan de manera automática en sentido cronológico descendente (los eventos más recientes en la parte superior).
  - El sistema aplica una regla de deduplicación automática de eventos de parto para evitar registros repetidos que coincidan en la misma fecha calendario.
- **Acceso a la hoja de vida de la cría:**
  - En los eventos de tipo Parto que cuenten con una cría vinculada, al pulsar sobre la fila se abre la hoja de vida completa del ternero o cría nacida.
  - Si el parto no tiene un animal hijo vinculado en el inventario o la cría fue transferida sin registro individual activo, la fila no abrirá una hoja de vida.
- **Edición de abortos:**
  - En los eventos clasificados como Aborto, al pulsar sobre la fila el sistema abre directamente la pantalla de edición del aborto con sus datos precargados (sexo del feto, fecha y observaciones).
  - Para guardar modificaciones en el registro del aborto, el usuario debe poseer el permiso de actualización de abortos en la finca activa.
- **Registro rápido de cría con madre preasignada:**
  - Al presionar el botón flotante con el icono de más (**+**), la aplicación abre el formulario de creación de animales estableciendo a la hembra activa como madre obligatoria del nuevo ejemplar.
  - Si la cuenta de la finca ha alcanzado el límite máximo de animales permitidos por su plan o membresía, el sistema bloqueará la creación del nuevo ejemplar.

### Flujo Paso a Paso para el Usuario
- **Ruta de acceso en la aplicación:**
  - En la barra inferior de navegación, toque **Animales** > Seleccione en el listado a la vaca o novilla > Presione el módulo **Reproducción** > Desplácese hasta la sección **Partos/Abortos** > Presione la flecha ubicada a la derecha del título de la sección para desplegar la tabla completa.

#### Barra Superior y Cinta de Identificación
- **Barra de navegación superior:** Presenta el título **Partos/Abortos** alineado a la izquierda sobre el color de fondo institucional. Incorpora únicamente el botón de retroceso (flecha hacia la izquierda) para descartar la vista y volver a la pantalla de resumen reproductivo de la hembra (sin botones de menú o acciones adicionales a la derecha).
- **Cinta de identidad del animal:** Franja horizontal centrada con fondo gris claro, ubicada inmediatamente debajo de la barra superior, que exhibe el icono del género de la hembra y su identificación compuesta (nombre y código de arete visual entre paréntesis) en una sola línea, manteniendo visible la trazabilidad zootécnica de la consulta en todo momento.

#### Estructura y Columnas de la Tabla
La tabla presenta la información organizada en cuatro columnas principales:
1. **Fecha:** Muestra la fecha en que ocurrió el parto o el aborto en formato local (día, mes y año).
2. **Tipo:** Indica la naturaleza del evento zootécnico: **Parto** o **Aborto**.
3. **Género:** Exhibe el sexo de la cría nacida o del feto abortado (**Macho** o **Hembra**).
4. **Cría:** Muestra el código de arete identificador de la cría en los partos que tengan un ejemplar registrado en el sistema. En abortos o partos sin registro individual de cría, este espacio permanece en blanco.

#### Acciones Interactivas y Navegación
- **Ver detalle o editar registro:** Al presionar sobre una fila de la tabla:
  - Si la fila corresponde a un **Parto** con cría asociada, el sistema abre la pantalla de resumen zootécnico y productivo del hijo.
  - Si la fila corresponde a un **Aborto**, el sistema redirige al formulario de edición de aborto para modificar o consultar los detalles del evento.
- **Registrar nueva cría de esta hembra:** Presione el botón flotante circular con el icono de más (**+**) ubicado en la esquina inferior de la pantalla para abrir la pantalla de creación de animales con la madre preasignada.

- **Pantalla de llegada tras salir:**
  - Al presionar la flecha de regreso en la barra superior, la aplicación retorna a la pantalla de resumen reproductivo de la hembra.

### Matriz de Errores y Soluciones
| Mensaje en la App / Síntoma | Causa Real | Respuesta Sugerida por el Agente | Criterio de Escalamiento Humano |
| :--- | :--- | :--- | :--- |
| La tabla aparece vacía sin registros de partos ni abortos | La hembra no tiene crías registradas, abortos cargados ni hechos de parto en el sistema de la finca | "Esta hembra no cuenta aún con registros de partos o abortos en su historial reproductivo. Para asentar un nuevo evento, puede registrar un aborto desde el botón de acciones reproductivas o registrar una cría usando el botón circular (+)." | No escalar, comportamiento esperado en hembras primerizas o sin historial reproductivo. |
| Al presionar una fila de tipo Parto no abre la ficha de la cría | El parto está registrado únicamente como un hecho zootécnico sin un animal hijo vinculado en el inventario | "El parto se encuentra registrado en el historial de la madre pero no tiene una cría asociada en el inventario de la finca. Para que aparezca vinculada, debe registrar al ternero e indicar a esta vaca como su madre." | No escalar, orientación zootécnica sobre asociación de crías. |
| "Con tu perfil de [Rol], NO tienes permisos para realizar esta acción." | El colaborador no tiene permisos para editar abortos o registrar nuevos animales en la finca activa | "Su usuario no cuenta con los permisos necesarios para modificar registros reproductivos o dar de alta nuevos animales. Solicite al propietario de la finca que le actualice sus permisos en la sección de colaboradores." | No escalar, depende de la configuración de roles y permisos del propietario de la finca. |
| Círculo de espera infinito / Pantalla congelada en cargando | Proceso en segundo plano bloqueado o timeout en el dispositivo al consultar la base de datos local | "Espere 30 segundos. Si no avanza, cierre la aplicación por completo desde el administrador de tareas de su teléfono (deslizando hacia arriba) y vuelva a abrirla. Sus datos locales no se perderán." | Si tras reabrir la app la tabla no carga y la pantalla vuelve a congelarse, transferir de inmediato a soporte humano con correo y modelo del teléfono. |

### Directivas de Seguridad y Guardrails
- NUNCA solicite contraseñas, credenciales de acceso ni números de cuenta al usuario para brindar asistencia en consultas reproductivas.
- Recuerde al usuario que la eliminación o modificación de eventos de aborto y parto afecta directamente los indicadores de intervalo entre partos y los diagnósticos de preñez activos en la finca.
- Aclare al ganadero que para que una cría figure con su código en la columna **Cría**, debe haberse registrado previamente como animal en el inventario vinculando a la vaca como madre.
