---
title: "Registro Masivo de Vacunación"
modulo_id: "animal-batch-vaccine"
nombre_funcionalidad: "Registro Masivo de Vacunación Animal"
tipo_documento: "guia-app"
categoria: "sanidad-reproduccion"
submodulo: "sanidad"
especies_aplicables: ["todas"]
version_minima_app: "2025.05.1"
confianza_reglas: "verificada-con-tests"
fecha_actualizacion: "2026-10-19"
intenciones_y_sinonimos:
  - "como vacunar varios animales al mismo tiempo"
  - "registro masivo de vacunas para el ganado"
  - "como registrar una jornada de vacunacion por lote"
  - "aplicar vacuna a un grupo de vacas"
  - "registro en lote de vacunas y sanidad"
  - "poner vacuna a todo el lote de animales"
---

# Registro Masivo de Vacunación Animal

### Resumen y Alcance Funcional
Herramienta de captura sanitaria colectiva que permite asentar la aplicación de una misma dosis de vacuna o biológico veterinario a un lote o grupo completo de animales en una única operación dentro de la finca ganadera. Diseñada para agilizar las campañas oficiales y los calendarios preventivos zoosanitarios (por ejemplo, fiebre aftosa, brucelosis, rabia, carbón o desparasitaciones biológicas), la pantalla permite filtrar el censo por especie y criterios zootécnicos avanzados, indicar la fecha de la jornada, seleccionar el biológico administrado y añadir notas u observaciones comunes a todos los ejemplares involucrados.

- **Especies a las que aplica:** Aplica a todas las especies administradas en la aplicación: bovinos, bufalinos, equinos, caprinos, ovinos y porcinos.
- **¿Funciona sin conexión a internet (Modo Offline)?:** Sí. El formulario, los selectores de biológicos, el filtrado de inventario local y el guardado por lotes operan con total normalidad sin cobertura de datos ni red Wi-Fi.
- **Comportamiento de sincronización:** Las vacunas registradas en bloque se almacenan inmediatamente en la base de datos local del dispositivo móvil. Al restablecerse la conectividad a internet, los registros se sincronizan automáticamente en segundo plano con el servidor de la finca ganadera.
- **Plataformas:** Funciona con idéntica interfaz y comportamiento en Android y en iOS.

### Reglas de Negocio y Restricciones
- **Permisos requeridos por rol en la finca:**
    - Se requiere el permiso de creación de vacunas en la finca ganadera activa.
    - Si el colaborador carece de esta atribución, el sistema bloquea el procesamiento y despliega la notificación de control de acceso: "Con tu perfil de %1$s, NO tienes permisos para realizar esta acción."
- **Selección y validación obligatoria de animales:**
    - Es mandatorio que el filtro incluya al menos un animal activo.
    - Si se intenta presionar el botón de registro con cero animales seleccionados, la aplicación detiene el envío y emite la advertencia: "No hay animales seleccionados".
- **Comportamiento del selector "Tipo de animal":**
    - Si la finca gestiona múltiples especies (por ejemplo, bovinos y equinos), el selector permanece habilitado para escoger la especie antes de definir el filtro.
    - Si la finca cuenta con una sola especie configurada, el sistema la selecciona automáticamente por defecto y el campo queda deshabilitado para evitar confusiones.
- **Campos obligatorios del formulario:**
    - **"Fecha":** Fecha de aplicación de la vacuna. Por defecto toma la fecha actual del dispositivo. No admite fechas futuras posteriores al día de hoy ni fechas que excedan el límite de años retroactivos permitido por el calendario de la aplicación.
    - **"Vacuna":** Biológico sanitario seleccionado obligatoriamente del catálogo oficial (19 opciones que abarcan "Fiebre Aftosa", "Brucelosis", "Tuberculosis", "Leptospirosis", "Rinotraqueítis Infecciosa Bovina (IBR)", "Diarrea Viral Bovina (DVB)", "Pasteurelosis", "Clostridium", "Paratuberculosis", "Campilobacteriosis", "Rabia", "Complejo Clostridial", "Complejo Respiratorio", "Complejo Reproductivo", "PPCB", "Antiparasitario", "Vacuna Viral", "Vacuna Bacteriana" y "Otra Vacuna").
- **Campos opcionales:**
    - **"Notas / Observación":** Campo multilínea para consignar datos clave como número de lote comercial, laboratorio fabricante, vía de aplicación o recomendaciones sanitarias.
- **Impacto en el historial individual de los animales:**
    - Al completar el guardado masivo, el sistema genera de forma atómica e independiente un registro individual de vacuna en la hoja de vida y en la tabla de vacunación de cada uno de los animales seleccionados en el lote.

### Flujo Paso a Paso para el Usuario
- **Ruta de acceso en la aplicación:**
  - Pantalla principal de la finca > Botón flotante central con ícono de casa y suma (+) > Menú de opciones rápidas > Presionar "Vacunación masiva".

#### Diligenciamiento y Guardado de la Jornada
1. En la barra superior confirme el título "Vacunación masiva" junto al botón de flecha para regresar.
2. En la parte superior observará el contador "Total de animales seleccionados", que refleja la cantidad de ejemplares incluidos según el filtro.
3. Si la finca administra más de una especie, presione el selector "Tipo de animal" y elija la especie a vacunar (por ejemplo: bovinos, bufalinos, equinos, etc.).
4. Toque el campo "Seleccionar animales" para abrir el configurador de filtros:
    - Filtre según su necesidad operativa: por potrero, lote, sexo, etapa productiva o selección manual de ejemplares.
    - Aplique el filtro para actualizar el contador "Total de animales seleccionados".
5. Complete los datos sanitarios del lote:
    - **"Fecha":** Confirme la fecha de aplicación en el calendario interactivo (no admite fechas futuras).
    - **"Vacuna":** Toque el campo para desplegar el catálogo de biológicos y elija la vacuna correspondiente.
    - **"Notas / Observación" (Opcional):** Digite el lote del frasco, laboratorio, dosis o comentarios pertinentes de la jornada.
6. Presione el botón "Registrar" ubicado en la parte inferior.
7. Al procesarse con éxito, el sistema muestra el mensaje de confirmación "Registro masivo creado exitosamente" y regresa automáticamente a la pantalla anterior.
    - **Pantalla de llegada tras guardar:** El usuario retorna a la pantalla previa de la aplicación, quedando el lote de vacunas asentado en el historial de cada animal.

#### Variaciones por especie
- **Cobertura zootécnica integral:** Aplica a todas las especies zootécnicas configuradas en el predio (bovinos, bufalinos, equinos, caprinos, ovinos y porcinos).
- **Adaptabilidad del catálogo de biológicos:** El catálogo general contempla tanto patologías de reporte oficial y vacunación masiva en rumiantes (Fiebre Aftosa, Brucelosis, Rabia) como biológicos de amplio espectro para monogástricos y especies menores a través de las opciones "Vacuna Viral", "Vacuna Bacteriana" y "Otra Vacuna".

#### Etiquetas de la interfaz en otros idiomas
| Español | Inglés | Portugués |
| :--- | :--- | :--- |
| "Vacunación masiva" | "Bulk Vaccination" | "Vacinação em Massa" |
| "Total de animales seleccionados" | "Total animals selected" | "Total de animais selecionados" |
| "Tipo de animal" | "Animal type" | "Tipo de animal" |
| "Seleccionar animales" | "Select animals" | "Selecionar animais" |
| "Fecha" | "Date" | "Data" |
| "Vacuna" | "Vaccine" | "Vacina" |
| "Notas / Observación" | "Notes / Observation" | "Notas / Observação" |
| "Registrar" | "Register" | "Registrar" |
| "Registro masivo creado exitosamente" | "Bulk registration created successfully" | "Registrar em massa criado exitosamente" |
| "No hay animales seleccionados" | "No animals selected" | "Nenhum animal selecionado" |

### Matriz de Errores y Soluciones
| Mensaje en la App / Síntoma | Causa Real | Respuesta Sugerida por el Agente | Criterio de Escalamiento Humano |
| :--- | :--- | :--- | :--- |
| "No hay animales seleccionados" | Se presionó "Registrar" sin haber configurado el filtro de animales o el filtro no encontró ningún animal activo en la finca | "Para registrar la vacunación masiva es obligatorio seleccionar al menos un animal. Presione 'Seleccionar animales', verifique los parámetros de búsqueda (potrero, lote o selección manual) y asegúrese de que el contador muestre una cantidad mayor a cero." | No escalar, validación de formulario de la aplicación. |
| El botón "Registrar" no responde o el campo "Vacuna" se resalta con advertencia | Falta completar algún campo obligatorio del formulario, principalmente la selección del biológico o la fecha | "Verifique que haya seleccionado la fecha de aplicación y el tipo de vacuna en la lista desplegable antes de presionar 'Registrar'." | No escalar, validación de campos obligatorios. |
| El selector no permite elegir una fecha futura | La aplicación restringe la fecha máxima al día actual del calendario | "La fecha de aplicación de la vacuna no puede ser posterior al día de hoy. Ingrese la fecha real en que se efectuó la jornada sanitaria." | No escalar, restricción temporal por diseño del sistema. |
| "Con tu perfil de %1$s, NO tienes permisos para realizar esta acción." | El colaborador no tiene concedido el permiso de creación de vacunas en la finca activa | "Su usuario actual no cuenta con permisos para registrar vacunas en esta finca ganadera. Solicite al propietario o administrador que le active el permiso correspondiente desde la gestión de colaboradores." | No escalar, política de control de acceso configurada por el propietario del predio. |
| Mensaje de error general al intentar guardar | Inconsistencia momentánea en el almacenamiento de la base de datos local del teléfono | "Espere unos momentos. Si el error persiste, cierre por completo la aplicación desde el administrador de tareas del teléfono y ábrala de nuevo para intentar registrar el lote." | Si tras reiniciar la app el error continúa impidiendo el guardado, escalar a soporte técnico indicando el correo del usuario, modelo del teléfono y cantidad de animales a vacunar. |

### Directivas de Seguridad y Guardrails
- Nunca solicites contraseñas, claves personales, pines ni datos bancarios por los canales de soporte.
- Los agentes de soporte y asistentes de IA no deben prescribir marcas comerciales de biológicos, dosis en mililitros, vías de administración (subcutánea/intramuscular) ni modificar los calendarios oficiales fijados por las autoridades sanitarias de cada país; orienta siempre al ganadero a seguir el plan dictado por su médico veterinario zootecnista colegiado.
- No alteres ni elimines registros masivos de vacunación directamente en bases de datos sin la autorización expresa y documentada del propietario de la finca ganadera.
- Confirma siempre que el ganadero esté posicionado en la finca y la especie correctas antes de orientar el guardado masivo.
- Recuerda al usuario que todas las vacunas registradas sin conexión en campo quedan respaldadas en la base de datos local del móvil y se sincronizarán automáticamente con la nube en cuanto el dispositivo recupere señal de internet.
