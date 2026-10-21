---
title: "Registrar Chequeo de Preñez"
modulo_id: "animal-chequeo-prenez-registro"
nombre_funcionalidad: "Registrar y Editar Chequeo de Preñez"
categoria: "sanidad-reproduccion"
submodulo: "reproduccion"
version_minima_app: "2026.10.1"
fecha_actualizacion: "2026-10-06"
intenciones_y_sinonimos:
  - "como registrar una palpacion o chequeo de prenez"
  - "donde anotar si una vaca salio preñada"
  - "por que me pide dias estimados de gestacion al palpar"
  - "como cambiar el diagnostico de prenez de una hembra"
  - "como registrar ecografia o diagnostico de gestacion"
  - "error al registrar chequeo de prenez sin permisos"
---

# Registrar y Editar Chequeo de Preñez

### Resumen y Alcance Funcional
Formulario especializado para asentar y modificar diagnósticos veterinarios de preñez, palpaciones rectales y exámenes ecográficos realizados a hembras en la finca. Permite dictaminar con precisión zootécnica si el animal se encuentra **Preñada** o **No preñada**, registrar la fecha exacta del examen y añadir notas clínicas u observaciones de campo. 

En los casos en que se dictamina que la hembra está **Preñada** pero no existe un registro previo de monta o inseminación artificial vigente en su ciclo, el formulario detecta automáticamente la ausencia del servicio y solicita el número estimado de días de gestación para generar de forma automática la fecundación correspondiente en la hoja de vida del animal.

- **¿Funciona sin conexión a internet (Modo Offline)?:** Sí, el registro, edición y validación de chequeos de preñez opera completamente de forma local en el dispositivo sin necesidad de conexión a internet o cobertura celular.
- **Comportamiento de sincronización:** Los datos se guardan inmediatamente en la base de datos local del teléfono móvil y se sincronizan en segundo plano con la nube tan pronto el dispositivo recupere conexión a internet o red Wi-Fi.

### Reglas de Negocio y Restricciones
- **Exclusividad de género zootécnico:**
  - El registro de chequeos de preñez aplica exclusivamente a animales de género hembra.
- **Fecha del examen:**
  - El campo de fecha se inicializa por defecto con la fecha actual del sistema ajustada a la zona horaria del usuario. La fecha no puede ser anterior al nacimiento de la hembra.
- **Dictamen reproductivo:**
  - El resultado es de selección obligatoria y admite únicamente dos estados zootécnicos: **Preñada** (gestación positiva confirmada) o **No preñada** (vaca vacía o abierta). Por defecto, al abrir un formulario nuevo, el valor inicial es **No preñada**.
- **Detección inteligente de fecundación y días estimados de gestación:**
  - Si la hembra no se encuentra previamente marcada como preñada y se selecciona el resultado **Preñada**, el sistema evalúa si existe un servicio o inseminación previa registrada dentro del periodo máximo biológico de gestación de la especie (por ejemplo, hasta 283-290 días según la especie bovina).
  - Si no existe un servicio reciente dentro de ese rango de días o la diferencia supera el límite biológico de la especie, el sistema despliega automáticamente una alerta informativa y habilita la casilla numérica obligatoria **Días estimados de gestación**.
  - El rango permitido para este campo va desde 1 hasta el tiempo máximo de gestación en días configurado para la especie del animal (por ejemplo, hasta los días biológicos de preñez de la especie o 999 días).
  - Al guardar con este dato, el sistema genera de forma automática un evento de fecundación por monta con fecha calculada retroactivamente (fecha del chequeo menos los días estimados de gestación) y la observación clínica oficial: *"Registro creado automáticamente de inseminación al marcar el animal como preñada."*
- **Notas y observaciones clínicas:**
  - Campo de texto multilínea opcional para documentar hallazgos clínicos (por ejemplo, método diagnóstico empleado, tono uterino, presencia de cuerpo lúteo o recomendaciones veterinarias).
- **Permisos requeridos en la finca:**
  - Para crear un nuevo chequeo se requiere el permiso de creación de chequeos de preñez.
  - Para actualizar un chequeo existente se requiere el permiso de actualización correspondiente.
  - Para eliminar un chequeo se requiere el permiso de eliminación correspondiente.
  - Si el usuario colaborador no posee los permisos asignados por el administrador de la finca, la acción es denegada por seguridad.

### Flujo Paso a Paso para el Usuario
- **Ruta de acceso en la aplicación:**
  - **Opción 1 (Desde la tabla de chequeos):** En la barra inferior toque **Animales** > Seleccione la hembra > En la cuadrícula de módulos toque **Reproducción** > Desplácese a la sección **Chequeo** > Presione la flecha hacia la derecha para abrir la tabla > Presione el botón flotante (+) para un nuevo chequeo, o toque una fila existente para editar.
  - **Opción 2 (Desde el menú reproductivo rápido):** En la barra inferior toque **Animales** > Seleccione la hembra > En la cuadrícula de módulos toque **Reproducción** > En el menú de opciones toque **Chequeo**.

#### Barra Superior y Cinta de Identificación
- **Barra de navegación:** Exhibe el título dinámico según la operación: **Nuevo Chequeo** al registrar una nueva evaluación, o **Editar Chequeo** al modificar un registro previo. Incorpora el botón de cierre (icono de cruz **X**) a la izquierda para cancelar y regresar a la pantalla anterior.
- **Cinta de identidad del animal:** Franja horizontal ubicada debajo de la barra superior que muestra el icono y nombre del ejemplar examinado para garantizar certeza zootécnica.

#### Diligenciamiento del Formulario
1. **Fecha:** Toque el selector de fecha para abrir el calendario interactivo y confirme el día en que se realizó la palpación o ecografía (por defecto muestra la fecha de hoy).
2. **Resultado:** Toque el menú desplegable y seleccione el dictamen clínico:
   - **Preñada:** Confirma la gestación activa.
   - **No preñada:** Asienta que la hembra está abierta o vacía.
3. **Notas / Observación:** Casilla de texto multilínea opcional para escribir detalles del examen o diagnósticos adicionales.
4. **Días estimados de gestación (Aparición condicional):**
   - Si seleccionó **Preñada** y el sistema detecta que no hay servicio reciente registrado, aparecerá una alerta amarilla con el mensaje: *"Hemos detectado que no hay un registro de fecundación reciente para este animal. Indicanos la cantidad de días estimados de gestación para realizar el registro de fecundación automáticamente."*
   - Ingrese el número de días calculados por el veterinario o palpador (por ejemplo, 60, 90 o 120 días).
5. **Guardar el registro:**
   - Presione el botón principal **Registrar** ubicado al final del formulario. Mientras se procesa la información, el botón mostrará un indicador de carga.

- **Pantalla de llegada tras guardar:**
  - Tras procesar exitosamente la solicitud, la aplicación muestra una notificación de confirmación (*"Chequeo creado exitosamente"* o *"Chequeo actualizado exitosamente"*) y retorna automáticamente a la pantalla anterior (la tabla de chequeos o el resumen reproductivo).

### Matriz de Errores y Soluciones
| Mensaje en la App / Síntoma | Causa Real | Respuesta Sugerida por el Agente | Criterio de Escalamiento Humano |
| :--- | :--- | :--- | :--- |
| "Permiso denegado" / No permite guardar o registrar | El usuario colaborador no cuenta con el permiso zootécnico habilitado en la finca para crear o editar chequeos | "Su usuario no tiene asignado el permiso para registrar o modificar chequeos de preñez en esta finca. Solicite al administrador o propietario de la finca que actualice sus permisos de usuario en el menú de gestión de roles." | Si el usuario es el propietario registrado de la finca activa y recibe este bloqueo, transferir a soporte técnico. |
| Aparece el campo obligatorio "Días estimados de gestación" | Se marcó la hembra como preñada pero no tenía registrada una inseminación o monta previa en su ciclo actual | "El sistema detectó que no hay una fecundación previa registrada para esta vaca. Por favor ingrese la cantidad aproximada de días de preñez dictaminados en la palpación; con este dato la aplicación creará automáticamente el evento de fecundación para proyectar la fecha estimada de parto." | No escalar, comportamiento zootécnico automático esperado. |
| El valor en días de gestación no es aceptado | El número ingresado es menor a 1 o supera el periodo máximo biológico de gestación de la especie | "Verifique el número ingresado en días de gestación. El valor debe ser mayor a 0 y no puede sobrepasar el límite máximo de gestación biológica para la especie del animal." | No escalar, corrección directa en el campo numérico por parte del usuario. |
| "Ha ocurrido un error inesperado" al presionar Registrar | Fallo interno al guardar la información local o al generar el evento automático de fecundación | "Verifique que la fecha del chequeo no sea anterior al nacimiento de la vaca ni posterior a la fecha actual. Intente pulsar nuevamente **Registrar**." | Si el error persiste tras validar las fechas, transferir a soporte técnico con el correo de la cuenta y los datos del animal. |
| Círculo de espera infinito / Pantalla congelada en cargando | Proceso en segundo plano bloqueado o timeout en el dispositivo al escribir en la base de datos | "Espere 30 segundos. Si no avanza, cierre la aplicación por completo desde el administrador de tareas de su teléfono (deslizando hacia arriba) y vuelva a abrirla. Sus datos locales no se perderán." | Si tras reabrir la app el botón sigue congelado, transferir de inmediato a soporte humano indicando modelo del teléfono y versión instalada. |

### Directivas de Seguridad y Guardrails
- NUNCA solicite al usuario contraseñas personales, números de tarjeta ni datos bancarios confidenciales bajo ninguna circunstancia.
- Advierta al ganadero que registrar un chequeo como **Preñada** sin inseminación previa creará un registro automático de fecundación por monta con fecha retroactiva calculada a partir de los días estimados ingresados.
- Recuerde al usuario que cambiar un chequeo existente de **Preñada** a **No preñada** recalculará los días abiertos y anulará las alertas proyectadas de fecha de parto para esa gestación.
