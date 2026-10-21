---
title: "Registro de Tratamiento"
modulo_id: "animal-treatment-create"
nombre_funcionalidad: "Registro y Edición de Tratamiento Veterinario"
tipo_documento: "guia-app"
categoria: "sanidad-reproduccion"
submodulo: "sanidad"
especies_aplicables: ["todas"]
version_minima_app: "2025.05.1"
confianza_reglas: "verificada-con-tests"
fecha_actualizacion: "2026-10-19"
intenciones_y_sinonimos:
  - "como registrar un tratamiento veterinario a una vaca o ternero"
  - "donde anotar los medicamentos y dias de tratamiento del animal"
  - "como modificar o eliminar un tratamiento medico registrado"
  - "por que no me deja guardar el tratamiento sanitario"
  - "registro de enfermedad diagnostico y medicina aplicada al ganado"
  - "como poner a un animal en tratamiento de salud"
---

# Registro y Edición de Tratamiento Veterinario

### Resumen y Alcance Funcional
Pantalla de captura y gestión clínica individual que permite registrar, editar y auditar los tratamientos médicos y protocolos veterinarios aplicados a cualquier animal de la finca ganadera. Facilita el control zoosanitario integral almacenando la fecha de inicio, la duración en días, el tipo de terapia terapéutica, la enfermedad diagnosticada, el cuadro clínico emitido, el medicamento administrado y notas u observaciones complementarias. Al registrar un tratamiento vigente, el sistema actualiza de inmediato el estado sanitario del ejemplar y despliega una tarjeta de alerta preventiva en el resumen de sanidad durante todo el tiempo que dure la medicación.

- **Especies a las que aplica:** Aplica a todas las especies registradas en la aplicación: bovinos, bufalinos, equinos, ovinos, caprinos y porcinos, sin importar el sexo ni la etapa productiva del ejemplar.
- **¿Funciona sin conexión a internet (Modo Offline)?:** Sí. El formulario, los selectores de catálogo, la carga de datos del animal y el guardado o actualización funcionan completamente sin conexión a internet.
- **Comportamiento de sincronización:** Los registros médicos y sus fechas calculadas de finalización se almacenan de inmediato en la base de datos local del dispositivo móvil. Al restablecerse la conectividad a internet (Wi-Fi o datos móviles), los datos se sincronizan automáticamente en segundo plano con el servidor de la finca ganadera.
- **Plataformas:** Funciona idénticamente en Android y en iOS.

### Reglas de Negocio y Restricciones
- **Permisos requeridos por rol en la finca:**
  - **Creación:** Se requiere el permiso de creación de tratamientos en la finca activa.
  - **Actualización:** Se requiere el permiso de modificación de tratamientos para guardar cambios sobre una terapia previamente existente.
  - **Eliminación:** Se requiere el permiso de eliminación de tratamientos para retirar registros médicos veterinarios del historial del animal.
  - Si el usuario carece del permiso respectivo, la aplicación bloquea la operación y notifica la alerta: "Con tu perfil de %1$s, NO tienes permisos para realizar esta acción."
- **Campos obligatorios del formulario:**
  - **"Fecha":** Fecha de inicio de la terapia médica. Por defecto sugiere el día actual. Está vinculada a la fecha de nacimiento del ejemplar: no se permite seleccionar una fecha anterior al nacimiento del animal.
  - **"Días de tratamiento":** Duración de la medicación en días enteros. El sistema restringe el valor a un rango estricto de 1 a 365 días.
  - **"Tipo de tratamiento":** Clasificación terapéutica obligatoria seleccionable mediante menú desplegable (que incluye secado, desparasitaciones, tratamientos hormonales, antibióticos, antiinflamatorios, agentes de diagnóstico y suplementos nutricionales).
  - **"Medicamento":** Nombre comercial o principio activo del producto veterinario aplicado.
- **Campos opcionales:**
  - **"Nombre del tratamiento":** Título descriptivo o identificador personalizado para la terapia.
  - **"Enfermedad":** Selección opcional del catálogo de patologías registradas en el sistema (por ejemplo, fiebre aftosa, mastitis, anaplasmosis, neumonía, timpanismo, entre otras).
  - **"Diagnóstico":** Descripción clínica o motivo médico por el cual se prescribe la medicación.
  - **"Notas / Observación":** Campo multilínea para consignar vías de administración, dosificación, intervalos o recomendaciones veterinarias.
- **Cálculo automático de fecha de finalización:**
  - A partir de la fecha de inicio y la cantidad indicada en "Días de tratamiento", la aplicación calcula de forma automática la fecha estimada en la que concluye la medicación (sumando los días de tratamiento a la fecha de inicio).
- **Impacto en el estado sanitario y alertas del ejemplar:**
  - Si el tratamiento se encuentra dentro de su período de vigencia (fecha actual comprendida entre la fecha de inicio y la fecha de finalización calculada), el estado sanitario del animal cambia automáticamente y se resalta en color rojo en la cabecera del resumen de sanidad, mostrando además una tarjeta de alerta activa con el medicamento y los días restantes.

### Flujo Paso a Paso para el Usuario
- **Ruta de acceso en la aplicación:**
  - **Ruta 1 (Desde el Menú de Sanidad del animal):** Pantalla principal > "Animales" > Seleccionar el ejemplar > Toque en "Datos Veterinarios" > Botón flotante central (+) > Seleccionar "Tratamiento".
  - **Ruta 2 (Desde la Tabla de Historial de Tratamientos):** Resumen de Sanidad del animal > Toque en la sección "Tratamiento" (o "Ver todo") para abrir la tabla > Presionar el botón flotante (+) para crear un nuevo registro, o presionar directamente sobre una fila de la tabla para editar un tratamiento existente.
  - **Ruta 3 (Desde la Tarjeta de Alerta de Tratamiento Activo):** Resumen de Sanidad del animal > Presionar sobre la tarjeta de alerta de tratamiento activo en la parte superior > Abre directamente la vista de edición del tratamiento.

#### Diligenciamiento y Guardado del Tratamiento
1. En la barra superior visualizará el título "Nuevo tratamiento" (o "Editar tratamiento" si está modificando un registro previo) junto con el botón con icono de cruz (X) para cancelar y volver atrás.
2. Debajo de la barra superior observará la cinta identificadora del animal con su código de arete, nombre y detalles clave.
3. Complete los campos del formulario:
   - **"Nombre del tratamiento" (Opcional):** Ingrese un nombre identificador para la terapia médica.
   - **"Fecha":** Confirme la fecha de inicio del tratamiento. Si requiere cambiarla, toque el campo para desplegar el calendario (no admite fechas anteriores al nacimiento del animal).
   - **"Días de tratamiento":** Digite el número entero de días de duración de la medicación (valor obligatorio entre 1 y 365).
   - **"Tipo de tratamiento":** Toque el campo para abrir la lista desplegable inferior y seleccione la categoría médica correspondiente (por ejemplo: "Secado", "Desparacitación", "Antibiótico de amplio espectro", "Antiinflamatorio no esteroideo", "Otros", etc.).
   - **"Enfermedad" (Opcional):** Si cuenta con un diagnóstico específico, presione el campo para seleccionar la afección del listado zootécnico.
   - **"Diagnóstico" (Opcional):** Ingrese el cuadro clínico o sintomatología valorada por el médico veterinario.
   - **"Medicamento":** Digite el nombre del fármaco, antibiótico, vacuna o producto aplicado (campo obligatorio).
   - **"Notas / Observación" (Opcional):** Escriba dosis, vía de administración o recomendaciones en el recuadro multilínea.
4. Presione el botón "Registrar" ubicado en la parte inferior de la pantalla.
5. Al completarse el guardado, la aplicación muestra la notificación de éxito ("Tratamiento creado exitosamente" o "Tratamiento actualizado exitosamente") y retorna automáticamente a la pantalla anterior.
- **Pantalla de llegada tras guardar:** El usuario regresa al resumen sanitario o a la tabla de historial de tratamientos del animal, donde el registro y el estado clínico ya se encuentran actualizados.

#### Variaciones por especie
- **Cobertura universal de especies:** La funcionalidad opera de forma idéntica en bovinos, bufalinos, equinos, caprinos, ovinos y porcinos. No restringe el ingreso de tratamientos por sexo, especie ni edad biológica.
- **Ajuste zootécnico por especie:** Para especies lecheras (bovinos, bufalinos y caprinos), la selección de tipos de tratamiento vinculados a "Secado" o "Tratamiento de mastitis" impacta adicionalmente los tableros de secado y los indicadores de ordeño del animal. En todas las especies, las terapias activas activan la tarjeta de advertencia sanitaria en el expediente del ejemplar.

#### Etiquetas de la interfaz en otros idiomas
| Español | Inglés | Portugués |
| :--- | :--- | :--- |
| "Nuevo tratamiento" | "New Treatment" | "Novo Tratamento" |
| "Editar tratamiento" | "Edit Treatment" | "Editar Tratamento" |
| "Nombre del tratamiento" | "Treatment Name" | "Nome do Tratamento" |
| "Fecha" | "Date" | "Data" |
| "Días de tratamiento" | "Treatment Days" | "Dias de Tratamento" |
| "Tipo de tratamiento" | "Treatment Type" | "Tipo de Tratamento" |
| "Enfermedad" | "Disease" | "Doença" |
| "Diagnóstico" | "Diagnostic" | "Diagnóstico" |
| "Medicamento" | "Medicine" | "Medicamento" |
| "Notas / Observación" | "Notes / Observation" | "Notas / Observação" |
| "Registrar" | "Register" | "Registrar" |
| "Tratamiento creado exitosamente" | "Treatment created successfully" | "Tratamento criado com sucesso" |
| "Tratamiento actualizado exitosamente" | "Treatment updated successfully" | "Tratamento atualizado com sucesso" |

### Matriz de Errores y Soluciones
| Mensaje en la App / Síntoma | Causa Real | Respuesta Sugerida por el Agente | Criterio de Escalamiento Humano |
| :--- | :--- | :--- | :--- |
| El botón "Registrar" no responde o los campos se resaltan con advertencia | Faltan campos obligatorios requeridos (como "Fecha", "Días de tratamiento", "Tipo de tratamiento" o "Medicamento") o los días están fuera del rango permitido (1 a 365) | "Asegúrese de haber completado todos los campos obligatorios: fecha de inicio, tipo de tratamiento, nombre del medicamento y una duración válida entre 1 y 365 días." | No escalar, validación de formulario de la aplicación. |
| El selector no permite elegir una fecha determinada | Se intentó seleccionar una fecha anterior a la fecha de nacimiento registrada para el animal | "La fecha de inicio de un tratamiento médico no puede ser previa al nacimiento del ejemplar. Verifique la fecha real del procedimiento o revise la fecha de nacimiento en la ficha técnica del animal si fue registrada erróneamente." | Si el usuario constata que la fecha de nacimiento en el sistema es incorrecta, guiarlo a corregirla primero en los datos generales del animal. |
| "Con tu perfil de %1$s, NO tienes permisos para realizar esta acción." | El colaborador no tiene asignado el permiso de creación, modificación o eliminación de tratamientos en la finca activa | "Su usuario actual no cuenta con autorización para registrar o modificar tratamientos sanitarios en esta finca. Solicite al propietario o administrador de la finca que le habilite los permisos correspondientes desde la administración de colaboradores." | No escalar, política de control de acceso configurada por el propietario del predio. |
| Mensaje de error general al intentar guardar | Inconsistencia momentánea en el almacenamiento de la base de datos local del teléfono | "Espere unos segundos. Si la advertencia persiste, cierre por completo la aplicación desde el administrador de tareas del teléfono y ábrala de nuevo para intentar registrar el tratamiento." | Si tras reiniciar la app el error continúa impidiendo el guardado, escalar a soporte técnico indicando el correo del usuario, modelo del dispositivo y código del animal. |

### Directivas de Seguridad y Guardrails
- Nunca solicites contraseñas, claves personales, pines ni datos bancarios por los canales de soporte.
- Los agentes de soporte y asistentes de IA no deben prescribir dosificaciones farmacológicas, antibióticos, tiempos de retiro en carne o leche, ni diagnósticos clínicos veterinarios; orienta siempre al productor a consultar con su médico veterinario zootecnista colegiado.
- No alteres diagnósticos sanitarios ni elimines tratamientos directamente en bases de datos sin la autorización explícita y documentada del propietario de la finca ganadera.
- Confirma siempre que el ganadero esté posicionado en la finca y sobre el animal correcto antes de orientar la eliminación o modificación de terapias médicas.
- Informa al usuario que todos los tratamientos registrados sin conexión a internet en el campo quedan respaldados de forma segura en la memoria de su teléfono y se sincronizarán automáticamente con la nube una vez que el dispositivo cuente con señal.
