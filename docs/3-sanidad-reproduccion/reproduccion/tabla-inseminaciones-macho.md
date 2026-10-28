---
title: "Fecundaciones Macho"
modulo_id: "animal-inseminaciones-macho-tabla"
nombre_funcionalidad: "Tabla de Fecundaciones y Servicios del Macho"
categoria: "sanidad-reproduccion"
submodulo: "reproduccion"
version_minima_app: "2026.10.1"
fecha_actualizacion: "2026-10-06"
intenciones_y_sinonimos:
  - "como ver el historial de montas e inseminaciones de un toro"
  - "tabla de vacas servidas por el reproductor"
  - "consultar que hembras fueron fecundadas por el macho"
  - "donde revisar los servicios reproductivos realizados por el toro"
  - "como editar un servicio reproductivo desde la ficha del macho"
  - "por que no aparece el boton de agregar servicio en el toro"
---

# Tabla de Fecundaciones y Servicios del Macho

### Resumen y Alcance Funcional
Pantalla de consulta y trazabilidad zootécnica que presenta en formato de tabla el historial cronológico completo de servicios reproductivos, montas naturales e inseminaciones en las que un reproductor macho (toro) ha participado activamente dentro de la finca. Permite al ganadero auditar la fecha exacta de cada servicio, la modalidad técnica utilizada (Monta, Inseminación artificial, Transferencia de embriones u Otros) y la identificación de la hembra o vaca servida (madre receptora del semen). Asimismo, proporciona navegación directa e interactiva para editar o consultar el formulario del servicio tocando sobre la fila correspondiente.

- **¿Funciona sin conexión a internet (Modo Offline)?:** Sí, la consulta, ordenamiento y visualización de los servicios del reproductor funcionan de forma autónoma sin señal de internet, utilizando la base de datos local del teléfono.
- **Comportamiento de sincronización:** Las transiciones de pantalla y la consulta de registros operan instantáneamente en local. Cualquier ajuste o edición realizado sobre un servicio reproductivo se almacena en el dispositivo y se sincroniza automáticamente con la nube una vez que el teléfono cuente con conexión de red.

### Reglas de Negocio y Restricciones
- **Filtrado individual por reproductor macho:**
    - La tabla exhibe exclusivamente aquellos registros de inseminación o monta donde el ejemplar consultado está asignado como padre o semental donante.
- **Tipos de fecundación zootécnica admitidos:**
    - Los eventos reflejan las modalidades registradas en el sistema: **Monta** (servicio natural en potrero o corral), **Inseminación artificial** (colecta o pajilla del reproductor), **Transferencia de embriones** u **Otros**.
- **Identificación de la hembra servida:**
    - La columna **Madre** muestra el código de arete visual y nombre de la hembra que recibió el servicio. Si la vaca fue dada de baja o trasladada, se conserva el identificador registrado en el momento del evento para garantizar la trazabilidad histórica.
- **Ausencia de botón flotante de creación (+):**
    - En esta pantalla no existe un botón flotante para registrar nuevos servicios. Conforme a las reglas zootécnicas del sistema, los servicios de fecundación se asientan sobre la hembra receptora (desde su respectiva ficha o menú reproductivo) seleccionando a este reproductor como padre.
- **Navegación interactiva y permisos de edición:**
    - Al presionar cualquier fila de la tabla, la aplicación redirige al formulario de edición del servicio de fecundación vinculado a la hembra correspondiente.
    - Para guardar modificaciones en el servicio, el usuario requiere contar con permisos de actualización de eventos reproductivos en la finca activa; de lo contrario, el formulario operará en modo de solo lectura.

### Flujo Paso a Paso para el Usuario
- **Ruta de acceso en la aplicación:**
    - En la barra inferior de navegación, toque **Animales** > Seleccione al toro o reproductor en la lista > En la cuadrícula de módulos, presione **Reproducción** > Desplácese hasta la sección **Fecundaciones** > Toque el botón de flecha hacia la derecha ubicado junto al título de la sección para desplegar la tabla completa.

#### Barra Superior y Cinta de Identificación
- **Barra de navegación superior:** Exhibe el título **Fecundaciones** alineado a la izquierda sobre el color de fondo institucional. Incorpora únicamente el botón de retroceso (flecha hacia la izquierda) para volver al resumen reproductivo del macho, sin botones de acción secundarios ni botón flotante.
- **Cinta de identidad del animal:** Franja horizontal centrada con fondo gris claro, ubicada inmediatamente debajo de la barra superior, que exhibe el icono del género del reproductor (macho) garantizando certeza sobre el ejemplar en consulta.

#### Estructura y Columnas de la Tabla

La información se presenta ordenada en una tabla con diseño cuadrado y tres columnas zootécnicas:

1. **Fecha:** Exhibe la fecha en que se llevó a cabo el servicio o inseminación, adaptada a la zona horaria del usuario.
2. **Tipo:** Indica la modalidad reproductiva empleada (**Monta**, **Inseminación artificial**, **Transferencia de embriones** u **Otros**).
3. **Madre:** Muestra el código de arete visual o nombre de la hembra que recibió el servicio del reproductor.

#### Acciones Interactivas y Navegación
- **Consultar o editar un servicio:** Toque sobre cualquier fila de la tabla para abrir directamente el formulario de registro del servicio reproductivo y modificar datos como la fecha, protocolo u observaciones.
- **Regresar a la pantalla previa:** Presione la flecha de retroceso ubicada en la barra superior.

- **Pantalla de llegada tras salir:**
  - Al presionar la flecha de retroceso en la barra superior, la aplicación retorna a la pantalla de resumen reproductivo del reproductor macho.

### Matriz de Errores y Soluciones
| Mensaje en la App / Síntoma | Causa Real | Respuesta Sugerida por el Agente | Criterio de Escalamiento Humano |
| :--- | :--- | :--- | :--- |
| La tabla aparece vacía sin ninguna fila | El reproductor no tiene servicios de monta o inseminaciones registradas en la finca | "Este toro aún no tiene registros de fecundación en el sistema. Para que figuren servicios en este listado, debe registrar la monta o inseminación desde la ficha de la hembra servida seleccionando a este macho como padre." | No escalar, comportamiento esperado en machos jóvenes o sin actividad reproductiva asentada. |
| No aparece el botón (+) para agregar servicios | Los servicios de reproducción se originan desde la hembra servida y no desde el macho | "Por regla zootécnica de la aplicación, las fecundaciones e inseminaciones se registran directamente en la ficha reproductiva de la vaca servida, donde se elige a este reproductor como padre del servicio." | No escalar, explicación de la regla de negocio del sistema. |
| La columna 'Madre' se muestra en blanco o con guion | La hembra servida fue eliminada del inventario local o no se vinculó un animal registrado | "Si la vaca servida fue dada de baja de la finca o se ingresó un registro sin vincular la hembra activa, la casilla puede aparecer vacía. Puede presionar sobre la fila para revisar el detalle del servicio." | No escalar salvo que se trate de una inconsistencia masiva de datos en la base de datos. |
| Al presionar una fila no permite guardar los cambios del servicio | El usuario colaborador no cuenta con permisos de actualización de eventos reproductivos | "Su perfil en la finca no tiene habilitado el permiso para modificar eventos reproductivos. Solicite al propietario o administrador de la finca que actualice sus permisos de colaborador." | Si el usuario es el propietario de la finca y no puede guardar, transferir a soporte técnico humano. |
| Círculo de espera infinito / Pantalla congelada en cargando | Proceso en segundo plano bloqueado o timeout en el dispositivo al consultar los servicios del macho en la base de datos local | "Espere 30 segundos. Si no avanza, cierre la aplicación por completo desde el administrador de tareas de su teléfono (deslizando hacia arriba) y vuelva a abrirla. Sus datos locales no se perderán." | Si tras reabrir la app la tabla vuelve a congelarse, transferir de inmediato a soporte humano con el correo de la cuenta y el arete del reproductor. |

### Directivas de Seguridad y Guardrails
- NUNCA solicite al ganadero contraseñas, claves personales ni códigos bancarios para orientarle en la consulta de servicios reproductivos de sus toros.
- Recuerde al usuario que cualquier modificación en la fecha de un servicio desde esta vista afectará directamente el cálculo de gestación y fecha estimada de parto de la vaca asociada.
- Indique claramente que las fecundaciones recibidas por vacas se consultan en el resumen reproductivo de cada hembra en su propia tabla de fecundaciones.
