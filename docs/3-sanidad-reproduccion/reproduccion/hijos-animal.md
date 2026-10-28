---
title: "Hijos del Reproductor"
modulo_id: "animal-hijos-tabla"
nombre_funcionalidad: "Tabla de Hijos del Reproductor"
categoria: "sanidad-reproduccion"
submodulo: "reproduccion"
version_minima_app: "2026.10.1"
fecha_actualizacion: "2026-10-05"
intenciones_y_sinonimos:
  - "como ver todos los hijos o crias de un toro"
  - "tabla de descendencia y progenie de un reproductor"
  - "consultar la lista de hijos de un animal"
  - "ver la ficha de una cria desde los hijos del padre"
  - "por que no sale la madre en la tabla de hijos"
  - "como saber que vacas parieron crias de este toro"
---

# Tabla de Hijos del Reproductor

### Resumen y Alcance Funcional
Pantalla de consulta zootécnica que consolida en formato de tabla la descendencia directa (hijos o crías) de un animal reproductor (principalmente machos reproductores o toros) registrado en la finca ganadera. Permite al ganadero auditar la progenie del reproductor, conocer las fechas de nacimiento, el sexo de cada cría, identificar el código de arete de la madre receptora del servicio y acceder directamente con un toque a la hoja de vida y seguimiento productivo de cada hijo.

- **¿Funciona sin conexión a internet (Modo Offline)?:** Sí, la pantalla consulta la información de genealogía y crías almacenada localmente en la base de datos del dispositivo móvil.
- **Comportamiento de sincronización:** Las consultas y la navegación hacia la hoja de vida de los ejemplares funcionan de inmediato sin conexión. Cualquier nuevo nacimiento registrado o vinculación de parentesco realizada en otros módulos se almacena en el teléfono y se sincroniza automáticamente con la nube cuando el dispositivo disponga de señal de internet.

### Reglas de Negocio y Restricciones
- **Filtro de relación parental directa:**
    - El sistema muestra exclusivamente los animales que tienen una relación biológica parental directa confirmada como padre o madre con el ejemplar activo.
    - Se excluyen automáticamente relaciones no biológicas o receptoras como madres sustitutas.
- **Identificación de la madre en la descendencia:**
    - Si el animal en consulta es el padre (macho reproductor), la columna correspondiente exhibe el código de arete visual de la madre de la cría.
    - Si la madre no se encuentra registrada en el inventario de la finca o fue asignada sin un código identificador individual, el campo permanece en blanco.
    - Cuando se consulta la descendencia desde una hembra, la columna de madre se mantiene vacía para evitar redundancias de información.
- **Acceso interactivo a la hoja de vida:**
    - Al pulsar sobre cualquiera de las filas de la tabla, la aplicación redirige de forma automática al resumen zootécnico y productivo del hijo seleccionado.
- **Visualización de consulta zootécnica:**
    - Esta pantalla está diseñada como una vista especializada de auditoría y trazabilidad genética; no cuenta con botón directo de creación o alta rápida de animales, por lo que los registros provienen de los partos y nacimientos dados de alta en el sistema.

### Flujo Paso a Paso para el Usuario
- **Ruta de acceso en la aplicación:**
    - En la barra inferior de navegación, toque **Animales** > Seleccione al macho reproductor o toro en el listado > Presione el módulo **Reproducción** > Desplácese hasta la sección **Hijos** > Presione el botón de flecha hacia la derecha ubicado junto al título de la sección para desplegar la tabla completa.

#### Barra Superior y Cinta de Identificación
- **Barra de navegación superior:** Presenta el título **Hijos** alineado a la izquierda sobre el fondo institucional. Contiene únicamente el botón de retroceso (flecha hacia la izquierda) para descartar la vista y volver a la pantalla de resumen reproductivo del ejemplar (sin botones secundarios de menú ni acciones de edición).
- **Cinta de identidad del animal:** Franja horizontal centrada con fondo gris claro, ubicada inmediatamente debajo de la barra superior, que exhibe el icono del género del reproductor y su identificación (nombre y código de arete visual entre paréntesis) en una sola línea, manteniendo visible la trazabilidad zootécnica de la consulta en todo momento.

#### Estructura y Columnas de la Tabla

La tabla presenta la lista de descendencia organizada en cuatro columnas principales:

1. **Fecha:** Muestra la fecha exacta de nacimiento de la cría en formato local (día, mes y año).
2. **Género:** Indica el sexo zootécnico de la cría (**Macho** o **Hembra**).
3. **Madre:** Muestra el código de arete visual de la vaca madre con la que se concibió la cría.
4. **Código:** Exhibe el código de arete identificador del hijo en el inventario de la finca.

#### Acciones Interactivas y Navegación
- **Ver hoja de vida del hijo:** Presione sobre cualquier fila de la tabla para abrir de inmediato la pantalla de resumen zootécnico, genealógico y productivo de la cría seleccionada.
- **Regresar al resumen reproductivo:** Toque la flecha de retroceso ubicada en la barra de navegación superior para retornar a la vista reproductiva del padre.

- **Pantalla de llegada tras salir:**
    - Al presionar la flecha de regreso en la barra superior, la aplicación retorna a la pantalla de resumen reproductivo del animal en consulta.

### Matriz de Errores y Soluciones
| Mensaje en la App / Síntoma | Causa Real | Respuesta Sugerida por el Agente | Criterio de Escalamiento Humano |
| :--- | :--- | :--- | :--- |
| La tabla aparece vacía sin registros de hijos | El reproductor no tiene crías vinculadas como padre en los nacimientos o partos registrados en la finca | "Este ejemplar aún no cuenta con hijos o crías vinculadas en su historial. Para que aparezcan en esta tabla, debe registrar los partos o dar de alta las crías indicando a este reproductor como su padre." | No escalar, comportamiento esperado en toretes jóvenes o reproductores sin partos asentados. |
| La columna Madre aparece en blanco en algunas crías | El ternero fue registrado sin especificar la madre o la madre no está registrada como un animal individual en la finca | "La columna de madre muestra el arete de la vaca si fue vinculada al registrar el nacimiento. Si la madre no fue registrada en el inventario o se omitió al crear el animal, el espacio aparecerá en blanco." | No escalar, orientación zootécnica sobre registro genealógico de crías. |
| Al presionar una cría no abre la pantalla de resumen | Identificador zootécnico del ejemplar no localizado en la base de datos local | "Espere unos instantes y vuelva a tocar la fila. Si el problema persiste, regrese al menú anterior y vuelva a ingresar a la tabla de hijos." | Si tras reintentar no es posible acceder a la ficha del hijo, transferir a soporte humano con los códigos de arete del padre y del hijo. |
| Círculo de espera infinito / Pantalla congelada en cargando | Proceso en segundo plano bloqueado o timeout en el dispositivo al consultar la base de datos local | "Espere 30 segundos. Si no avanza, cierre la aplicación por completo desde el administrador de tareas de su teléfono (deslizando hacia arriba) y vuelva a abrirla. Sus datos locales no se perderán." | Si tras reabrir la app la tabla no carga y la pantalla vuelve a congelarse, transferir de inmediato a soporte humano con correo y modelo del teléfono. |

### Directivas de Seguridad y Guardrails
- NUNCA solicite contraseñas, credenciales de acceso ni números de cuenta al usuario para brindar asistencia en consultas reproductivas o genealógicas.
- Recuerde al usuario que la vinculación de parentesco (padre y madre) se establece al momento de dar de alta la cría o asentar el parto, y que cualquier modificación en la ficha del animal actualiza automáticamente su presencia en la tabla de descendencia.
- Aclare al ganadero que para auditar las crías comercializadas o trasladadas fuera de la finca existe una sección diferenciada de crías trasladadas en el resumen reproductivo.
