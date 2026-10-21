---
title: "Registro de Vacunación"
modulo_id: "sanidad-registro-vacuna-animal"
nombre_funcionalidad: "Registro y Edición de Vacunación Individual"
categoria: "sanidad-reproduccion"
submodulo: "sanidad"
version_minima_app: "2026.10.1"
fecha_actualizacion: "2026-10-08"
intenciones_y_sinonimos:
  - "como registrar una vacuna a una vaca"
  - "donde anotar la aplicacion de aftosa o brucelosis al animal"
  - "como modificar la fecha de una vacuna registrada"
  - "por que no me permite guardar la vacuna del ganado"
  - "registro sanitario de vacunas y biologicos aplicados"
  - "como cambiar el tipo de vacuna administrada"
---

# Registro y Edición de Vacunación Individual

### Resumen y Alcance Funcional
Permite registrar y gestionar de manera individual la aplicación de vacunas y biológicos sanitarios administrados a un animal en la finca ganadera. Facilita el cumplimiento de los planes sanitarios oficiales y preventivos del predio registrando la fecha de aplicación, el tipo de vacuna administrada y cualquier observación o número de lote pertinente. Al guardar el registro, la dosis queda asentada inmediatamente en el historial sanitario del animal para consultas veterinarias, certificaciones o inspecciones sanitarias.

- **¿Funciona sin conexión a internet (Modo Offline)?:** Sí.
- **Comportamiento de sincronización:** Los registros de vacunación se almacenan localmente en la base de datos del dispositivo móvil. En cuanto el teléfono detecta conectividad a internet, los datos se sincronizan automáticamente en segundo plano con Horus.

### Reglas de Negocio y Restricciones
- **Campos obligatorios:**
  - **Fecha:** Día en que se suministró la dosis biológica. Por defecto toma la fecha actual del sistema. El sistema valida que la fecha no sea anterior a la fecha de nacimiento registrada para el animal ni posterior al día presente.
  - **Vacuna:** Selección obligatoria del biológico administrado mediante una hoja de opciones desplegable. Incluye catálogo veterinario estandarizado:
    - Fiebre Aftosa
    - Brucelosis
    - Tuberculosis
    - Leptospirosis
    - Rinotraqueítis Infecciosa Bovina (IBR)
    - Diarrea Viral Bovina (DVB)
    - Pasteurelosis
    - Clostridium
    - Paratuberculosis
    - Campilobacteriosis
    - Rabia
    - Complejo Clostridial
    - Complejo Respiratorio
    - Complejo Reproductivo
    - PPCB
    - Antiparasitario
    - Vacuna Viral
    - Vacuna Bacteriana
    - Otra Vacuna
- **Campos opcionales:**
  - **Notas y observaciones:** Espacio de texto multilínea para consignar datos complementarios, tales como el laboratorio fabricante, número de lote de la vacuna, vía de inoculación (subcutánea, intramuscular) o dosis en mililitros.
- **Permisos de usuario requeridos:**
  - Para registrar una nueva dosis se requiere el permiso de creación de vacunas.
  - Para modificar una dosis previa se requiere el permiso de actualización de vacunas.
  - Para remover una dosis registrada se requiere el permiso de eliminación de vacunas. Si el usuario no tiene los privilegios asignados en la finca, el sistema restringe el guardado.

### Flujo Paso a Paso para el Usuario
- **Ruta de acceso en la aplicación:**
  - **Ruta 1 (Acceso directo desde sanidad):** Menú inferior **Animales** > Seleccionar el animal > **Datos Veterinarios** > Botón flotante circular con el signo más (**+**) > **Vacunación**.
  - **Ruta 2 (Desde el historial de vacunas):** Menú inferior **Animales** > Seleccionar el animal > **Datos Veterinarios** > En la sección **Vacunación**, presionar la flecha orientada a la derecha > Presionar el botón flotante circular con el signo más (**+**) para crear o tocar un registro previo en la tabla para editar.

1. **Identificación de la pantalla y del animal:**
   - En la barra superior confirme el título **Agregar Vacuna** (o **Editar Vacuna** si está modificando un registro existente).
   - En la parte superior verifique la cinta identificadora del animal con su nombre y sexo.
2. **Diligenciamiento del formulario de vacunación:**
   - **Fecha:** Toque el selector de fecha para ajustar el día de inoculación. Por defecto el campo sugiere la fecha de hoy.
   - **Vacuna:** Toque el campo para abrir la lista de biológicos y seleccione la vacuna administrada (por ejemplo, Fiebre Aftosa, Brucelosis, Rabia o Complejo Respiratorio).
   - **Notas y observaciones:** Escriba el número de lote, laboratorio o detalles de la aplicación si dispone de ellos (campo opcional).
3. **Guardado del registro:**
   - Presione el botón **Registrar**.
   - El sistema valida la información y muestra un mensaje de confirmación (**Vacuna creado exitosamente** o **Vacuna actualizado exitosamente**).
- **Pantalla de llegada tras guardar:** Al guardarse la información con éxito o al presionar la equis (**X**) de cierre en la barra superior, la aplicación retorna a la pantalla anterior (el resumen de sanidad o la tabla de historial de vacunas del animal).

### Matriz de Errores y Soluciones
| Mensaje en la App / Síntoma | Causa Real | Respuesta Sugerida por el Agente | Criterio de Escalamiento Humano |
| :--- | :--- | :--- | :--- |
| El botón "Registrar" no realiza ninguna acción o el campo Vacuna se resalta | No se ha seleccionado el tipo de vacuna obligatoria en el formulario | "Por favor seleccione el tipo de biológico o vacuna administrada en la lista desplegable antes de presionar Registrar." | No escalar. Guiar al usuario a completar la selección de la vacuna. |
| El calendario no permite seleccionar una fecha anterior | Se intentó registrar una fecha anterior al nacimiento del animal | "La fecha de aplicación de la vacuna no puede ser anterior a la fecha de nacimiento registrada para este animal. Seleccione una fecha válida a partir de su nacimiento." | Si la fecha de nacimiento asentada en la ficha del animal es errónea, orientar al usuario a corregirla en los datos básicos del animal. |
| Mensaje de advertencia o bloqueo indicando permisos denegados | El usuario no posee los permisos asignados para crear o modificar vacunas en la finca | "Su cuenta de usuario no cuenta con los permisos necesarios para gestionar vacunas en esta finca ganadera. Solicite al administrador de la finca que le habilite los permisos correspondientes desde la administración de colaboradores." | No escalar. Indicar al usuario que contacte al propietario o administrador de la finca. |
| Error general al intentar guardar o actualizar la vacuna | Inconsistencia puntual en el almacenamiento local del dispositivo | "Cierre la aplicación por completo deslizándola hacia arriba en el administrador de aplicaciones de su dispositivo móvil y vuelva a abrirla. Posteriormente, intente guardar el registro de vacunación nuevamente." | Si el error persiste tras reiniciar la app, solicitar el identificador del animal y escalar a soporte técnico. |

### Directivas de Seguridad y Guardrails
- NUNCA solicite contraseñas, códigos de verificación SMS ni datos personales bancarios al usuario en WhatsApp ni en ningún canal de soporte.
- No recomiende planes sanitarios personalizados, dosis de fármacos ni biológicos específicos; oriente al usuario a seguir los lineamientos de la entidad sanitaria de su país y las indicaciones de su médico veterinario.
- No modifique ni borre registros sanitarios directamente en el sistema sin la autorización del administrador de la finca ganadera.
