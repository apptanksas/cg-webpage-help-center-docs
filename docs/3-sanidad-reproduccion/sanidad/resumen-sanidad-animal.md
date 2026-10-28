---
title: "Datos Veterinarios"
modulo_id: "sanidad-resumen-datos-veterinarios"
nombre_funcionalidad: "Resumen de Datos Veterinarios y Sanidad del Animal"
categoria: "sanidad-reproduccion"
submodulo: "sanidad"
version_minima_app: "2026.10.1"
fecha_actualizacion: "2026-10-08"
intenciones_y_sinonimos:
  - "como ver el historial clinico o veterinario de un animal"
  - "donde consultar los tratamientos y vacunas aplicadas a la vaca"
  - "por que el encabezado de datos veterinarios sale en color rojo"
  - "resumen de sanidad mastitis y secado del ganado"
  - "como ver las tareas y eventos pendientes de salud del animal"
  - "que significa la tarjeta de alerta de tratamiento o secado"
---

# Resumen de Datos Veterinarios y Sanidad del Animal

### Resumen y Alcance Funcional
Proporciona una vista centralizada del historial clínico y sanitario del animal en la finca ganadera. Permite al productor y al personal veterinario consultar en una sola pantalla el estado sanitario actual, alertas destacadas de tratamientos médicos o periodos de secado vigentes, los últimos tratamientos administrados, las vacunas aplicadas, los episodios de mastitis registrados y las tareas o eventos veterinarios programados a futuro.

- **¿Funciona sin conexión a internet (Modo Offline)?:** Sí.
- **Comportamiento de sincronización:** Todo el historial clínico, alertas y tablas se leen directamente desde la base de datos local del dispositivo móvil. Al registrar un nuevo evento sanitario o al sincronizarse novedades con Horus en segundo plano, la información se actualiza de forma automática en la pantalla.

### Reglas de Negocio y Restricciones
- **Validación de estado del animal (Bloqueo o baja):**
    - Si el animal se encuentra bloqueado o dado de baja en la finca ganadera (registrado como fallecido, vendido o descartado), el sistema restringe el acceso al resumen sanitario y regresa de forma automática a la pantalla anterior para proteger la integridad de los datos.
- **Color y estado del encabezado:**
    - El encabezado superior muestra el título **Datos veterinarios** junto al estado sanitario actual del animal.
    - Si el animal no se encuentra bajo tratamiento médico activo, el encabezado se muestra en el color principal de la aplicación.
    - Si el animal tiene un tratamiento médico o proceso clínico activo, el encabezado cambia automáticamente a color rojo de advertencia visual para alertar al operario.
- **Tarjeta de alerta de tratamiento o periodo de secado activo:**
    - Cuando el estado sanitario del animal indica que está en tratamiento, se despliega una tarjeta de alerta destacada debajo del encabezado que muestra:
      - **Tipo de alerta:** Identifica si se trata de un **Tratamiento** general o si la vaca se encuentra **En periodo de secado**, acompañado del ícono correspondiente.
      - **Medicamento o nombre:** Indica el nombre del tratamiento o el fármaco prescrito.
      - **Duración y fecha límite:** Muestra la cantidad total de días del tratamiento y la fecha estimada de finalización según la zona horaria del usuario.
      - Al presionar dicha tarjeta, el sistema abre directamente el formulario de edición o detalle del tratamiento activo.
- **Tablas de historial y límite de filas en el resumen:**
    - Las secciones del resumen (**Tratamiento**, **Registro de secado**, **Vacunación**, **Mastitis** y **Eventos y tareas**) muestran únicamente las **5 filas más recientes** para garantizar una navegación ágil.
    - Para consultar el historial completo de cualquiera de estas categorías, se debe presionar la flecha ubicada a la derecha del título de cada sección.
    - Al presionar sobre cualquier fila de las tablas de tratamientos, secados, vacunas o mastitis, se abre el formulario de edición correspondiente. Al presionar sobre un evento o tarea, se abre la pantalla con el detalle de dicha actividad.
- **Estado vacío:**
    - Si el animal no cuenta con ningún registro histórico de tratamientos, secados, vacunas, mastitis ni tareas pendientes, la pantalla muestra una vista limpia con el indicador de estado sin información.
- **Botón flotante de acciones rápidas (+):**
    - La pantalla incluye un botón flotante circular con el signo más (**+**) que despliega el menú de acciones sanitarias para registrar rápidamente nuevos tratamientos, vacunas, diagnósticos de mastitis o periodos de secado.

### Flujo Paso a Paso para el Usuario

- **Ruta de acceso en la aplicación:** Menú inferior **Animales** > Seleccionar el animal > En la ficha del animal, presionar la tarjeta o acceso **Sanidad** (o **Datos veterinarios**).

1. **Revisión del encabezado y estado sanitario:**
    - Observe la parte superior de la pantalla: verifique el estado sanitario del animal mostrado debajo de **Datos veterinarios** (por ejemplo, Sano o En tratamiento).
    - Si el encabezado se torna de color rojo, preste atención a la alerta clínica activa.
2. **Consulta de alerta de tratamiento activo (si aplica):**
    - Si el animal está bajo medicación o secado, revise la tarjeta de alerta para verificar el medicamento aplicado, los días de duración y la fecha en que concluye el tratamiento. Presione sobre la tarjeta si necesita editar o actualizar los datos del tratamiento.
3. **Exploración de tablas del historial clínico:**
    - Deslice hacia abajo para revisar las distintas secciones de salud:
        - **Tratamiento:** Muestra los tratamientos médicos generales aplicados recientemente.
        - **Vacunación:** Detalla las últimas vacunas administradas junto con su fecha.
        - **Mastitis:** En hembras lecheras, presenta los diagnósticos recientes de mastitis y el cuarto mamario afectado.
        - **Registro de secado:** Presenta los registros de secado y tratamientos intramamarios de secado.
        - **Eventos y tareas:** Lista las próximas actividades sanitarias programadas (recordatorios de revacunación, revisiones periódicas o tareas pendientes).
4. **Acceso al historial completo o edición:**
    - Para ver todas las filas históricas de un área específica, presione la flecha orientada a la derecha junto al título de la sección deseada.
    - Para modificar un registro previo, presione directamente sobre la fila correspondiente en la tabla.
5. **Registro de un nuevo evento de sanidad:**
    - Presione el botón flotante circular con el ícono (**+**) para abrir el menú de sanidad y seleccionar si desea registrar un tratamiento, una vacuna, un control de mastitis o un secado.
    - **Pantalla de llegada tras salir:** Al presionar la flecha de regreso en la barra superior, la aplicación retorna a la ficha principal del animal.

### Matriz de Errores y Soluciones
| Mensaje en la App / Síntoma | Causa Real | Respuesta Sugerida por el Agente | Criterio de Escalamiento Humano |
| :--- | :--- | :--- | :--- |
| Al presionar sobre Sanidad la pantalla se cierra o regresa de inmediato a la lista de animales | El animal se encuentra marcado como fallecido, vendido o dado de baja en la finca | "El historial veterinario se deshabilita automáticamente cuando el animal figura como inactivo, vendido o fallecido. Si el animal sigue activo en su finca, verifique y actualice su estado en la hoja de vida." | Si el usuario confirma que el animal está físicamente activo en la finca pero el sistema lo tiene bloqueado, transferir a soporte técnico indicando el código del animal. |
| El encabezado de datos veterinarios aparece en color rojo | El animal tiene un tratamiento clínico o periodo de secado activo en curso | "El color rojo en el encabezado es una alerta visual que indica que el animal está actualmente bajo tratamiento o en periodo de secado. Revise la tarjeta superior para ver la fecha de finalización y el medicamento asignado." | No escalar. Guiar al usuario a consultar la tarjeta de alerta activa. |
| Solo aparecen 5 registros en la tabla de vacunas o tratamientos y faltan los más antiguos | La pantalla de resumen está diseñada para mostrar únicamente las 5 entradas más recientes de cada categoría | "La pantalla principal muestra las últimas 5 actividades para que la consulta sea rápida. Para revisar el historial completo de vacunas o tratamientos, presione la flecha ubicada al lado derecho del título de la sección." | No escalar. Indicar al usuario cómo ingresar a la tabla completa. |
| La pantalla aparece completamente en blanco sin tablas ni tarjetas de salud | El animal es de reciente ingreso en la finca y aún no registra tratamientos, vacunas, mastitis ni tareas | "El animal no tiene eventos sanitarios registrados hasta el momento. Puede presionar el botón circular con el signo (+) para registrar su primera vacuna, tratamiento o control sanitario." | No escalar. Orientar al usuario sobre cómo agregar el primer registro clínico. |
| Aparece un mensaje de error al intentar abrir o cargar la información de sanidad | Error momentáneo al consultar la base de datos local del teléfono | "Cierre la aplicación deslizando hacia arriba en el administrador de tareas de su teléfono y vuelva a abrirla para refrescar la lectura de los datos locales." | Si tras reiniciar la aplicación el error persiste para ese animal, transferir a soporte técnico indicando el código del animal y modelo del dispositivo. |

### Directivas de Seguridad y Guardrails
- NUNCA solicite contraseñas, números de identificación personal ni códigos confidenciales por WhatsApp ni por canales de soporte.
- No emita diagnósticos clínicos veterinarios, prescripciones farmacológicas ni dosificaciones de medicamentos; oriente siempre al usuario a consultar con su médico veterinario de confianza.
- No altere diagnósticos ni elimine historiales médicos veterinarios directamente en la base de datos sin la autorización expresa del administrador de la finca ganadera.
