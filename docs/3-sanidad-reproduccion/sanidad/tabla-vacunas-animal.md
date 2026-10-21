---
title: "Tabla de Vacunación"
modulo_id: "sanidad-tabla-vacunas-animal"
nombre_funcionalidad: "Tabla de Historial de Vacunación Animal"
categoria: "sanidad-reproduccion"
submodulo: "sanidad"
version_minima_app: "2026.10.1"
fecha_actualizacion: "2026-10-08"
intenciones_y_sinonimos:
  - "donde consultar todo el historial de vacunas de una vaca"
  - "como ver la tabla completa de dosis y biologicos aplicados al animal"
  - "como editar o modificar una vacuna desde la lista"
  - "como registrar una nueva vacuna desde el historial sanitario"
  - "donde ver las notas o lotes de las vacunas puestas al ganado"
  - "historial cronologico de vacunacion del animal"
---

# Tabla de Historial de Vacunación Animal

### Resumen y Alcance Funcional
Proporciona la vista cronológica completa de todas las dosis de vacunas y biológicos sanitarios aplicados a un animal en la finca ganadera. Permite al productor, mayordomo o médico veterinario revisar con exactitud cada fecha de vacunación, el biológico administrado y las observaciones o números de lote registrados. Además, permite seleccionar cualquier fila para consultar o modificar la información de una dosis previa y dispone de un acceso rápido para registrar una nueva vacuna.

- **¿Funciona sin conexión a internet (Modo Offline)?:** Sí.
- **Comportamiento de sincronización:** Todo el historial de vacunas se consulta directamente desde la base de datos local en el dispositivo móvil. Cada vez que se registra o modifica una vacuna, o cuando el dispositivo sincroniza novedades en segundo plano con Horus al recuperar señal de internet, la tabla se actualiza de forma automática e inmediata.

### Reglas de Negocio y Restricciones
- **Cinta identificadora del animal:**
  - En la parte superior de la pantalla se muestra la cinta con el nombre y sexo seleccionado.
- **Columnas de la tabla de vacunación:**
  - **Fecha:** Muestra el día en que se administró la dosis biológica, adaptada a la zona horaria del usuario.
  - **Vacuna:** Presenta el nombre oficial del biológico sanitario administrado (según el catálogo estándar veterinario: Fiebre Aftosa, Brucelosis, Rabia, IBR, DVB, Carbón/Clostridium, etc.).
  - **Notas:** Muestra las observaciones, número de lote, laboratorio o vía de inoculación registrados. Si no se registraron observaciones, la columna muestra un guion indicativo de ausencia de información.
- **Interacción y edición de vacunas:**
  - Al presionar cualquier fila dentro de la tabla, el sistema abre la pantalla de edición del registro de vacunación correspondiente, cargando los datos guardados para su ajuste o consulta detallada.
- **Botón flotante para nueva vacuna:**
  - La pantalla incluye un botón flotante circular con el signo más (**+**) que permite navegar directamente al formulario de registro de vacuna para añadir una nueva dosis sin abandonar el flujo del animal.
- **Permisos requeridos:**
  - Para consultar el historial se requiere acceso a la finca y a los datos sanitarios del animal.
  - Para modificar una dosis o registrar una nueva desde esta vista se requieren los permisos de actualización o creación de vacunas en la finca.

### Flujo Paso a Paso para el Usuario
- **Ruta de acceso en la aplicación:** Menú inferior **Animales** > Seleccionar el animal > **Sanidad** (o **Datos veterinarios**) > En la sección **Vacunación**, presionar la flecha orientada a la derecha ubicada al lado del título.

1. **Identificación de la pantalla y del animal:**
   - En la barra superior confirme el título **Vacunación**.
   - En la parte superior verifique la cinta identificadora del animal con su identificación, nombre y datos generales.
2. **Exploración del historial de vacunación:**
   - Deslice verticalmente para revisar la lista cronológica de vacunas aplicadas al ejemplar.
   - Consulte la información en las columnas: **Fecha**, **Vacuna** y **Notas**.
3. **Edición o consulta detallada de una vacuna:**
   - Presione directamente sobre la fila correspondiente a la dosis que desea consultar o corregir.
   - El sistema abrirá la pantalla de edición con los campos previamente diligenciados.
   - Aplique los cambios requeridos y presione el botón **Registrar** para guardar las actualizaciones.
4. **Registro de una nueva vacuna desde la tabla:**
   - Presione el botón flotante circular con el signo más (**+**) ubicado en la pantalla.
   - Se abrirá el formulario para registrar una nueva aplicación de biológico para el animal.
- **Pantalla de llegada tras salir:** Al presionar la flecha de regreso en la barra superior, la aplicación retorna a la pantalla de resumen de **Datos veterinarios** (Sanidad) del animal.

### Matriz de Errores y Soluciones
| Mensaje en la App / Síntoma | Causa Real | Respuesta Sugerida por el Agente | Criterio de Escalamiento Humano |
| :--- | :--- | :--- | :--- |
| La tabla aparece completamente vacía sin registros de vacunación | El animal no tiene vacunas o biológicos registrados hasta el momento en la finca | "El animal no cuenta con registros de vacunación previos. Puede presionar el botón circular con el signo (+) para asentar la primera dosis aplicada." | No escalar. Guiar al usuario sobre cómo registrar la primera vacuna. |
| Al presionar una fila de la tabla no permite guardar cambios en la vacuna | El usuario actual no cuenta con los permisos de actualización de vacunas en la finca | "Su cuenta de usuario no tiene permisos para modificar registros de vacunación en esta finca ganadera. Solicite al administrador de la finca que le asigne los permisos necesarios desde la administración de colaboradores." | No escalar. Indicar al usuario que contacte al propietario o administrador de la finca. |
| La fecha mostrada en la tabla difiere del día en que se administró la dosis | La zona horaria configurada en la cuenta del usuario difiere de la zona horaria del lugar donde se realizó la aplicación | "Verifique la configuración de zona horaria en los ajustes de su perfil de usuario para asegurarse de que coincida con la hora local de su finca ganadera." | No escalar. Orientar al usuario a revisar la configuración de zona horaria en su perfil. |
| No aparece una vacuna registrada recientemente por otro colaborador | El dispositivo aún no ha completado el ciclo de sincronización de datos con el servidor | "Asegúrese de que su dispositivo cuente con conexión a internet y espere unos momentos a que la sincronización automática actualice las novedades registradas en la finca." | Si transcurridos varios minutos con buena conexión el registro no aparece en ningún dispositivo, solicitar los datos del animal y escalar a soporte técnico. |

### Directivas de Seguridad y Guardrails
- NUNCA solicite contraseñas, pines de acceso ni códigos de verificación SMS a los usuarios a través de WhatsApp ni ningún canal de soporte.
- No prescriba esquemas de vacunación, dosis de biológicos ni marcas comerciales de fármacos; recuerde siempre al usuario acatar las directivas de las autoridades sanitarias oficiales y consultar a su médico veterinario.
- No modifique ni borre registros sanitarios directamente en la base de datos sin la autorización explícita del administrador de la finca ganadera.
