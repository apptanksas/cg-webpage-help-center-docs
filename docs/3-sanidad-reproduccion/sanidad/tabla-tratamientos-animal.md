---
title: "Tabla de Tratamientos"
modulo_id: "sanidad-tabla-tratamientos-animal"
nombre_funcionalidad: "Tabla de Historial de Tratamientos Veterinarios"
categoria: "sanidad-reproduccion"
submodulo: "sanidad"
version_minima_app: "2026.10.1"
fecha_actualizacion: "2026-10-08"
intenciones_y_sinonimos:
  - "donde consultar todo el historial de tratamientos de una vaca"
  - "como ver la tabla completa de medicamentos y terapias aplicadas al animal"
  - "como editar o modificar un tratamiento veterinario desde la lista"
  - "por que no aparecen los tratamientos de secado en esta tabla"
  - "como registrar un nuevo tratamiento desde el historial clinico"
  - "historial cronologico de enfermedades y medicamentos del ganado"
---

# Tabla de Historial de Tratamientos Veterinarios

### Resumen y Alcance Funcional
Proporciona la vista cronológica completa y detallada de todos los tratamientos médicos y terapias veterinarias generales registradas para un animal en la finca ganadera. Permite al productor, mayordomo o médico veterinario revisar con exactitud cada fecha de intervención, el medicamento administrado, la patología diagnosticada y la duración prescrita en días. Asimismo, permite seleccionar cualquier fila para consultar o editar la información del tratamiento y cuenta con acceso rápido para registrar una nueva terapia sanitaria.

- **¿Funciona sin conexión a internet (Modo Offline)?:** Sí.
- **Comportamiento de sincronización:** Todo el historial de tratamientos se consulta directamente desde la base de datos local en el dispositivo móvil. Cada vez que se registra o actualiza un tratamiento, o cuando la aplicación sincroniza novedades en segundo plano con Horus al recuperar conexión, la tabla se actualiza de forma automática e inmediata.

### Reglas de Negocio y Restricciones
- **Filtro de exclusión de secados:**
  - Esta pantalla lista exclusivamente tratamientos médicos generales (preventivos, curativos, sintomáticos u otros).
  - Los tratamientos intramamarios o procedimientos de secado se gestionan en su propio módulo clínico y quedan excluidos de esta tabla.
- **Cinta identificadora del animal:**
  - En la parte superior de la vista, justo debajo de la barra de navegación, se muestra la cinta con el identificador visual, número de arete, nombre, sexo y estado del animal seleccionado.
- **Columnas de la tabla de tratamientos:**
  - **Fecha:** Muestra la fecha de inicio del tratamiento médico adaptada a la zona horaria del usuario.
  - **Medicamento:** Presenta el nombre comercial o principio activo del fármaco prescrito.
  - **Enfermedad:** Muestra el nombre oficial de la enfermedad o diagnóstico registrado para la terapia. Si no se especificó patología, la columna queda en blanco.
  - **Días de tratamiento:** Refleja el número total de días de duración prescritos para la terapia.
- **Interacción y edición de tratamientos:**
  - Al presionar cualquier fila dentro de la tabla, el sistema abre directamente el formulario de registro y edición de tratamiento con los datos cargados para su consulta o modificación.
- **Botón flotante para nuevo tratamiento:**
  - La pantalla incluye un botón flotante circular con el signo más (**+**) que permite navegar directamente al formulario de creación para registrar una nueva terapia al animal sin salir de la tabla.

### Flujo Paso a Paso para el Usuario
- **Ruta de acceso en la aplicación:** Menú inferior **Animales** > Seleccionar el animal > **Sanidad** (o **Datos veterinarios**) > En la sección **Tratamiento**, presionar la flecha orientada a la derecha ubicada al lado del título.

1. **Identificación de la pantalla y del animal:**
   - En la barra superior confirme el título **Tratamiento**.
   - Justo debajo verifique la cinta identificadora del animal con su código, nombre y datos generales.
2. **Exploración del historial de tratamientos:**
   - Deslice hacia abajo para revisar la lista completa de tratamientos médicos ordenados cronológicamente.
   - Consulte la información en las columnas: **Fecha**, **Medicamento**, **Enfermedad** y **Días de tratamiento**.
3. **Edición o modificación de un tratamiento previo:**
   - Presione directamente sobre la fila correspondiente al tratamiento que desea revisar o corregir.
   - El sistema abrirá la pantalla de edición con todos los datos previamente diligenciados.
   - Aplique los cambios necesarios y presione el botón **Registrar** para guardar las actualizaciones.
4. **Registro de un nuevo tratamiento desde la tabla:**
   - Presione el botón flotante circular con el signo más (**+**) ubicado en la pantalla.
   - Se abrirá el formulario para registrar una nueva terapia médica para el animal.
- **Pantalla de llegada tras salir:** Al presionar la flecha de regreso en la barra superior, la aplicación retorna a la pantalla de resumen de **Datos veterinarios** (Sanidad) del animal.

### Matriz de Errores y Soluciones
| Mensaje en la App / Síntoma | Causa Real | Respuesta Sugerida por el Agente | Criterio de Escalamiento Humano |
| :--- | :--- | :--- | :--- |
| La tabla aparece completamente vacía sin registros de tratamientos | El animal no tiene terapias médicas generales registradas en la finca | "El animal no cuenta con tratamientos registrados hasta el momento. Puede presionar el botón circular con el signo (+) para registrar la primera terapia médica." | No escalar. Guiar al usuario sobre cómo registrar el primer tratamiento. |
| No aparece en la tabla un tratamiento de secado aplicado a una vaca | Los tratamientos asociados al periodo de secado se almacenan y visualizan de manera separada en el registro de secado | "Los tratamientos intramamarios o registros de secado no se muestran en esta tabla. Puede consultarlos regresando a Datos veterinarios en la sección Registro de secado." | No escalar. Explicar al usuario la separación funcional entre tratamientos generales y registros de secado. |
| Al presionar una fila de la tabla no se puede editar o no permite guardar cambios | El usuario actual no cuenta con los permisos de actualización de tratamientos veterinarios en la finca | "Su cuenta de usuario no tiene permisos para modificar tratamientos en esta finca. Solicite al administrador de la finca que le asigne los permisos necesarios desde la configuración de colaboradores." | No escalar. Orientar al usuario a contactar al administrador de su finca ganadera. |
| La fecha mostrada en la tabla difiere del día en que se aplicó el medicamento | La zona horaria configurada en el perfil del usuario difiere de la hora local donde se realizó la medicación | "Verifique la configuración de zona horaria en los ajustes de su cuenta para asegurarse de que coincida con la hora local de su finca ganadera." | No escalar. Orientar al usuario en la revisión de su zona horaria en los ajustes de perfil. |

### Directivas de Seguridad y Guardrails
- NUNCA solicite contraseñas, claves personales ni códigos de acceso a los usuarios a través de WhatsApp ni ningún canal de soporte.
- No prescriba medicamentos veterinarios, dosis farmacológicas ni diagnósticos clínicos; oriente siempre al usuario a consultar con su médico veterinario colegiado.
- No altere ni elimine registros médicos veterinarios directamente en la base de datos sin la autorización explícita del administrador de la finca ganadera.
