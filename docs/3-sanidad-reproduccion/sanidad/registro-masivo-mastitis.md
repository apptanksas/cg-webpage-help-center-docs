---
title: "Control Masivo de Mastitis"
modulo_id: "animal-batch-mastitis"
nombre_funcionalidad: "Control Masivo de Mastitis"
tipo_documento: "guia-app"
categoria: "sanidad-reproduccion"
submodulo: "sanidad"
especies_aplicables: ["bovinos", "bufalinos", "caprinos", "ovinos", "porcinos"]
version_minima_app: "2025.05.1"
confianza_reglas: "verificada-con-tests"
fecha_actualizacion: "2026-10-19"
intenciones_y_sinonimos:
  - "como registrar mastitis a varias vacas o cabras"
  - "control de mastitis en lote en la aplicacion"
  - "reportar ubres infectadas o pezones con mastitis"
  - "registro masivo de mastitis y tratamientos sanitarios"
  - "como calificar la severidad de mastitis por cuarto o pezon"
  - "anotar hembras con mastitis durante el ordeño"
---

# Control Masivo de Mastitis

### Resumen y Alcance Funcional
Pantalla de captura sanitaria que permite registrar diagnósticos de mastitis y asignar tratamientos médicos de forma consecutiva a múltiples hembras de la finca ganadera sin salir del formulario. Diseñada para agilizar la labor durante o después de la rutina de ordeño y revisión veterinaria, permite calificar individualmente la severidad de cada cuarto mamario (pezón), prescribir días de medicación y descripción terapéutica, y visualizar en una tabla acumulada los registros realizados con opción de editarlos o eliminarlos.

- **Especies a las que aplica:** Aplica para hembras adultas de especies lecheras o susceptibles de la finca (bovinos, bufalinos, caprinos, ovinos y porcinos). Los equinos están excluidos de este control.
- **¿Funciona sin conexión a internet (Modo Offline)?:** Sí. El formulario, las validaciones de campos, la consulta de hembras activas en la finca y la tabla de registros guardados operan sin conexión a internet.
- **Comportamiento de sincronización:** Las evaluaciones sanitarias y los tratamientos asociados se guardan de inmediato en la base de datos local del teléfono y se sincronizan en segundo plano con el servidor cuando el dispositivo dispone de conexión a internet.
- **Plataformas:** Funciona igual en Android y en iOS.

### Reglas de Negocio y Restricciones
- **Permisos requeridos por rol en la finca:**
  - **Creación de registro:** Se requiere el permiso de creación de mastitis en la finca. Si se activa la opción de tratamiento médico, también se requiere el permiso de creación de tratamientos.
  - **Modificación de registro:** Al seleccionar una fila de la tabla para editar, se requiere el permiso de actualización de mastitis y, de aplicar tratamiento, el permiso de actualización de tratamientos.
  - **Eliminación de registro:** Al presionar el botón de eliminar una fila seleccionada, se requiere el permiso de eliminación de mastitis y, si tenía tratamiento vinculado, el permiso de eliminación de tratamientos.
  - Si el usuario carece de los permisos correspondientes, el sistema bloquea la operación mostrando el mensaje: "Con tu perfil de %1$s, NO tienes permisos para realizar esta acción."
- **Población de animales elegible en el selector:**
  - El selector filtra exclusivamente hembras (sexo hembra).
  - La hembra debe pertenecer a la etapa productiva adulta o senior según los parámetros zootécnicos de su especie.
  - El animal debe estar vivo y físicamente presente en la finca activa (excluye vendidos, fallecidos, trasladados o ausentes).
  - Se excluyen estrictamente los animales de especie equina.
- **Validaciones zootécnicas y de formulario:**
  - **Fecha del control:** Por defecto sugiere el día actual. No admite fechas posteriores al día de hoy ni anteriores a la fecha de nacimiento del animal.
  - **Severidad por pezón o cuarto mamario:** Es posible evaluar de 1 a 4 cuartos mamarios de manera independiente. Cada pezón admite los siguientes niveles de severidad:
    - "Oculta (Subclínica)"
    - "Leve"
    - "Moderada"
    - "Grave"
    - "Extrema (Gangrenosa)"
    - "Destruida y Perdida"
    - Los pezones sanos o no afectados pueden permanecer sin selección (valor nulo).
  - **Tratamiento médico:**
    - La opción "Poner en tratamiento" es opcional.
    - Si se activa la casilla, los campos "Días de tratamiento" y "Descripción del tratamiento" son obligatorios. Si alguno se deja vacío, el sistema bloquea el guardado alertando: "Datos de tratamiento requeridos".
    - El número de días de tratamiento debe ser un número entero válido entre 1 y 365 días.
    - Al guardarse el tratamiento, el sistema genera automáticamente un registro vinculado en el historial de tratamientos del animal con fecha de fin calculada a partir de los días indicados.
- **Comportamiento del flujo en lote:**
  - Tras presionar "Guardar", el sistema persiste el registro, limpia el formulario y deselecciona el animal para permitir el registro ágil de la siguiente hembra.
  - La tabla inferior se actualiza de inmediato mediante el bus de eventos de la aplicación, mostrando el código del animal, fecha, cuartos afectados y días de tratamiento.

### Flujo Paso a Paso para el Usuario
- **Ruta de acceso en la aplicación:**
  - **Ruta principal (Desde el menú contextual de acciones rápidas):** En la pantalla principal de la finca, presione el botón flotante central (+) > En el menú "¿Qué quieres hacer hoy?", seleccione "Mastitis masivo".

#### 1. Encabezado y Selección del Animal
1. En la barra superior visualizará el título "Control de mastitis" y la flecha de navegación para regresar a la pantalla anterior.
2. En la parte superior del formulario presione el campo "Animal". Se desplegará el listado con las hembras adultas y seniors disponibles en la finca.
3. Busque y seleccione la hembra correspondiente por su código de arete o nombre. Al seleccionarla, sus datos quedarán fijados en el encabezado del formulario.

#### 2. Fecha y Evaluación de Cuartos Mamarios
1. **"Fecha":** Compruebe la fecha de evaluación. El sistema sugiere la fecha de hoy. Si el diagnóstico se realizó en días pasados, toque el campo para desplegar el calendario y elija la fecha correspondiente.
2. **"Ubres infectadas":** Encontrará el esquema de evaluación con cuatro pezones o cuartos mamarios numerados:
   - "Ubre 1" (frontal izquierdo) y "Ubre 3" (posterior izquierdo).
   - "Ubre 2" (frontal derecho) y "Ubre 4" (posterior derecho).
3. Toque el menú desplegable del cuarto mamario afectado y seleccione el nivel de afectación: "Oculta (Subclínica)", "Leve", "Moderada", "Grave", "Extrema (Gangrenosa)" o "Destruida y Perdida". Los cuartos sanos se mantienen sin selección.

#### 3. Notas y Tratamiento Médico Opcional
1. **"Notas":** Ingrese observaciones zootécnicas o veterinarias de campo (aspecto de la leche, grumos, sensibilidad o indicaciones especiales).
2. **"Poner en tratamiento":** Si la hembra requiere medicación o terapia intramamaria, marque la casilla de verificación.
3. Al activarla, se desplegarán los campos obligatorios de tratamiento:
   - **"Días de tratamiento":** Ingrese la duración del tratamiento en días (rango admitido: de 1 a 365 días).
   - **"Descripción del tratamiento":** Ingrese el antibiótico, antiinflamatorio o producto veterinario administrado.

#### 4. Guardar Registro y Continuidad en Lote
1. En la parte inferior del formulario presione el botón "Guardar".
2. El sistema guarda el registro de mastitis y el tratamiento asociado, muestra el mensaje de confirmación "Guardado exitosamente" y limpia automáticamente los campos del formulario.
3. El cursor y el selector de animal quedan listos para seleccionar a la siguiente hembra sin salir de la pantalla.

#### 5. Consulta, Edición y Eliminación desde la Tabla de Lote
1. Debajo del formulario se ubica la tabla de registros acumulados, con columnas que detallan: animal evaluado, fecha del control, cuartos afectados y días de tratamiento.
2. **Para editar un registro:** Presione la fila correspondiente en la tabla. Los datos se cargarán en el formulario superior para modificar los cuartos evaluados, notas o tratamiento. Presione "Guardar" para actualizar los cambios.
3. **Para eliminar un registro:** Al tener seleccionada una fila de la tabla, presione el botón rojo con icono de papelera. Se abrirá el diálogo de confirmación: "¿Estas seguro de eliminar este registro?". Confirme la acción presionando "Eliminar". El registro y su tratamiento asociado se cancelarán y la tabla se actualizará automáticamente.
- **Pantalla de llegada tras guardar:** El usuario permanece en la pantalla de "Control de mastitis" para continuar con la captura masiva. Al finalizar el lote, presione la flecha de regreso en la barra superior para volver a la pantalla principal.

#### Variaciones por especie
- **Hembras productivas por especie:** El selector filtra hembras adultas y seniors adaptándose a la clasificación zootécnica de cada especie presente en la finca (por ejemplo: vacas en bovinos, búfalas en bufalinos, cabras en caprinos, ovejas en ovinos, o cerdas en porcinos).
- **Exclusión de equinos:** Las yeguas y hembras de la especie equina no aparecen en el selector de esta pantalla, ya que el control de mastitis está restringido a especies lecheras y ganaderas compatibles.
- **Morfología mamaria:** El esquema de 4 pezones aplica morfológicamente para bovinos y bufalinos. En especies con 2 pezones funcionales (como caprinos y ovinos) o con múltiples pares mamarios (porcinos), el productor califica los pezones afectados utilizando las casillas disponibles del formulario.

#### Etiquetas de la interfaz en otros idiomas
| Español | Inglés | Portugués |
| :--- | :--- | :--- |
| "Control de mastitis" | "Mastitis Control" | "Controle de Mastite" |
| "Mastitis masivo" | "Bulk Mastitis" | "Mastite em massa" |
| "Ubres infectadas" | "Infected Udders" | "Úberes Infectadas" |
| "Poner en tratamiento" | "Put Under Treatment" | "Colocar em Tratamento" |
| "Días de tratamiento" | "Treatment Days" | "Dias de Tratamento" |
| "Descripción del tratamiento" | "Treatment Description" | "Descrição do Tratamento" |
| "Oculta (Subclínica)" | "Hidden (Subclinical)" | "Oculta (Subclínica)" |
| "Leve" | "Mild" | "Leve" |
| "Moderada" | "Moderate" | "Moderada" |
| "Grave" | "Severe" | "Grave" |
| "Extrema (Gangrenosa)" | "Extreme (Gangrenous)" | "Extrema (Gangrenosa)" |
| "Destruida y Perdida" | "Destroyed and Lost" | "Destruída e Perdida" |
| "Guardar" | "Save" | "Salvar" |
| "Eliminar" | "Delete" | "Excluir" |

### Matriz de Errores y Soluciones
| Mensaje en la App / Síntoma | Causa Real | Respuesta Sugerida por el Agente | Criterio de Escalamiento Humano |
| :--- | :--- | :--- | :--- |
| "Datos de tratamiento requeridos" | Se activó la casilla "Poner en tratamiento" pero se omitió ingresar los días o la descripción del tratamiento | "Al activar 'Poner en tratamiento', es obligatorio ingresar los 'Días de tratamiento' y la 'Descripción del tratamiento'. Complete ambos campos o desmarque la casilla si no va a medicar al animal." | No escalar, validación de formulario del dispositivo. |
| "Con tu perfil de %1$s, NO tienes permisos para realizar esta acción." | El colaborador carece de permisos de creación, modificación o eliminación de mastitis o tratamientos sanitarios | "Su usuario no cuenta con autorización para registrar o modificar controles de mastitis o tratamientos en esta finca. Solicite al propietario o administrador de la finca que le habilite los permisos correspondientes en la administración de colaboradores." | No escalar, restricción de permisos del predio configurada por el propietario. |
| "¿Estas seguro de eliminar este registro?" | Diálogo de confirmación al presionar el botón de eliminar una fila seleccionada de la tabla | "El sistema le solicita confirmación antes de borrar el diagnóstico sanitario y su tratamiento médico. Presione 'Eliminar' para confirmar o 'Cancelar' para conservar el registro." | No escalar, diálogo de seguridad de la aplicación. |
| La hembra no figura en la lista del selector "Animal" | El animal es macho, es de especie equina, está en etapa de cría joven, o está marcado como inactivo/fallecido/vendido | "El selector de mastitis solo muestra hembras en etapa adulta o senior que se encuentren activas y físicamente en la finca. Verifique en el listado de animales que el ejemplar cumpla con estos requisitos y no pertenezca a la especie equina." | Si la hembra cumple con todos los requisitos zootécnicos y sigue sin figurar en la lista, transferir a soporte técnico indicando el código de arete. |
| El registro guardado no aparece de inmediato en la tabla | Retraso puntual en la actualización del bus de eventos o filtro de registros en el dispositivo | "Salga un momento de la pantalla presionando la flecha de regreso y vuelva a ingresar a 'Mastitis masivo' desde el menú central (+). Esto forzará la recarga completa de la tabla de registros de la finca." | Si tras volver a ingresar el registro continúa ausente habiendo mostrado confirmación de guardado, escalar a soporte técnico indicando código del animal y fecha. |
| Espera prolongada en carga | Proceso en segundo plano bloqueado o timeout en el dispositivo al guardar el lote | "Espere un momento. Si la pantalla no avanza, cierre la aplicación por completo y vuelva a abrirla. Sus registros guardados previamente en el dispositivo no se pierden." | Si tras reiniciar la aplicación la pantalla vuelve a congelarse al guardar, transferir a soporte técnico con el correo de la cuenta y el modelo del teléfono. |

### Directivas de Seguridad y Guardrails
- Nunca solicites contraseñas, códigos SMS, pines ni datos bancarios por el chat.
- Los agentes de soporte y asistentes de IA no deben prescribir dosificaciones farmacológicas, antibióticos ni planes terapéuticos específicos; la selección de medicamentos y días de tratamiento es responsabilidad exclusiva del ganadero o de su médico veterinario.
- Verifica siempre que el ganadero se encuentre ubicado en la finca correcta antes de orientar la eliminación o modificación de registros sanitarios.
- No alteres diagnósticos sanitarios ni elimines tratamientos directamente en bases de datos sin la autorización explícita del propietario de la finca.
- Confirma al usuario que todos los registros de mastitis y tratamientos efectuados sin conexión a internet en el corral u ordeño quedan asegurados en su teléfono y se sincronizarán automáticamente con la nube cuando disponga de cobertura.
