---
title: "Registrar Aborto"
modulo_id: "animal-aborto-crear"
nombre_funcionalidad: "Registro y Edición de Aborto"
categoria: "sanidad-reproduccion"
submodulo: "reproduccion"
version_minima_app: "2026.10.1"
fecha_actualizacion: "2026-10-05"
intenciones_y_sinonimos:
  - "como registrar el aborto de una vaca"
  - "anotar perdida de prenez en una novilla"
  - "como cambiar la fecha de un aborto registrado"
  - "eliminar un registro de aborto equivocado"
  - "no tengo permisos para registrar aborto"
  - "guardar notas y sexo del feto abortado"
---

# Registro y Edición de Aborto

### Resumen y Alcance Funcional
Módulo reproductivo especializado que permite asentar la interrupción involuntaria de la gestación en hembras reproductoras (vacas o novillas) de la finca. Su registro actualiza el historial ginecológico del ejemplar, resetea el ciclo reproductivo, interrumpe el seguimiento del diagnóstico de preñez activo y documenta las características del feto (sexo asignado) junto con observaciones sanitarias para el control veterinario del predio. Permite crear nuevos eventos de aborto, editar datos previamente registrados y eliminar registros erróneos.

- **¿Funciona sin conexión a internet (Modo Offline)?:** Sí, la consulta de datos del animal y el registro, edición o eliminación de abortos funcionan de forma completa sin conexión a internet.
- **Comportamiento de sincronización:** Los registros se guardan de inmediato en la base de datos local del dispositivo móvil. En cuanto el teléfono detecta señal de red o conexión WiFi, los datos se sincronizan automáticamente con la nube y quedan reflejados en todos los dispositivos vinculados a la finca.

### Reglas de Negocio y Restricciones
- **Permisos requeridos por rol en la finca:**
  - **Creación de aborto:** Se requiere contar con el permiso de creación de abortos en la finca activa. Si el colaborador no tiene este rol asignado, el sistema denegará la acción e impedirá guardar el formulario.
  - **Edición y actualización:** Para modificar la fecha, sexo del feto u observaciones de un aborto existente se requiere el permiso de actualización de abortos.
  - **Eliminación del registro:** Para dar de baja un evento de aborto guardado se requiere el permiso de eliminación de abortos.
- **Validaciones zootécnicas y de calendario:**
  - **Fecha del evento:** Es obligatoria y se establece por defecto en la fecha actual del sistema. El selector de fecha restringe la selección impidiendo ingresar fechas futuras o fechas anteriores al nacimiento de la hembra.
  - **Sexo del feto:** Es un campo obligatorio para la estadística zootécnica de pérdidas perinatales; el sistema selecciona Macho por defecto y permite alternar a Hembra.
  - **Notas y observaciones:** Campo de texto multilínea opcional para documentar posibles causas zootécnicas o patológicas (ej. traumas físicos, sospechas de brucelosis, condiciones climáticas o tratamientos previos).

### Flujo Paso a Paso para el Usuario
- **Ruta de acceso en la aplicación:**
  - **Ruta 1 (Registro desde el resumen reproductivo):** En la barra inferior de navegación, toque **Animales** > Seleccione a la vaca o novilla en el listado > Presione el módulo **Reproducción** > En la parte inferior, presione el botón flotante circular con el icono de más (**+**) > En el menú de opciones **Chequeo reproductivo**, seleccione **Aborto** (identificado con icono de hembra en tono marrón).
  - **Ruta 2 (Edición desde la tabla de partos y abortos):** En la barra inferior, toque **Animales** > Seleccione a la hembra > Presione **Reproducción** > Desplácese a la sección **Partos/Abortos** > Toque directamente sobre la fila del aborto registrado que necesita corregir.
  - **Ruta 3 (Edición desde la tabla completa de eventos de cría):** En el resumen de **Reproducción** de la hembra > En la sección **Partos/Abortos**, presione el icono de flecha hacia la derecha para abrir la tabla completa > Localice el registro y presione el botón de edición.

#### Barra Superior y Cinta de Identificación
- **Barra de navegación:** Exhibe el título contextual de la acción: **Nuevo Aborto** al registrar por primera vez, o **Editar Aborto** cuando se modifican los datos de un evento existente. Incluye un botón de cierre (**X**) a la izquierda que descarta los cambios no guardados y regresa a la vista previa.
- **Cinta de identidad del animal:** Franja fija superior que despliega el código de arete visual y el nombre del ejemplar para asegurar que el evento se asocie a la hembra correspondiente.

#### Formulario de Registro
1. **Sexo del feto:** En el selector de género, elija el sexo identificado en el feto expulsado marcando el botón globo de **Macho** o **Hembra** (por defecto aparece seleccionado Macho).
2. **Fecha:** Toque el selector de fecha para abrir el calendario emergente y confirme el día exacto en que ocurrió el aborto. El sistema bloquea de manera automática cualquier fecha previa al nacimiento de la vaca o posterior al día actual.
3. **Notas y observaciones:** En el campo de texto multilínea opcional, ingrese detalles clínicos o zootécnicos del evento (sospechas de enfermedades, causas aparentes, síntomas previos o tratamientos aplicados).
4. **Guardar el registro:** Presione el botón **Registrar** ubicado al final del formulario. Durante el proceso de guardado, el botón se bloquea temporalmente para evitar registros duplicados.

- **Pantalla de llegada tras guardar o salir:**
  - Al presionar el botón de cierre (**X**), se cancela la operación y se regresa a la pantalla reproductiva de origen.
  - Al completar el registro con éxito, el sistema emite el mensaje de confirmación (*"Aborto creado exitosamente"* o *"Aborto actualizado exitosamente"*) y redirige de forma automática al resumen de **Reproducción** de la hembra con los indicadores actualizados.

### Matriz de Errores y Soluciones
| Mensaje en la App / Síntoma | Causa Real | Respuesta Sugerida por el Agente | Criterio de Escalamiento Humano |
| :--- | :--- | :--- | :--- |
| "Con tu perfil de [Rol], NO tienes permisos para realizar esta acción." | El usuario colaborador no cuenta con el permiso para crear, actualizar o eliminar registros de abortos en la finca | "Su perfil actual en esta finca no tiene permisos para gestionar eventos de aborto. Solicite al propietario o administrador de la finca que le habilite los permisos de gestión reproductiva en la sección de colaboradores." | No escalar, depende de la configuración de roles y permisos otorgados por el dueño de la finca. |
| "Ha ocurrido un error inesperado..." | Conflicto momentáneo en la base de datos local o fallo en la validación interna del registro | "No fue posible registrar el aborto. Verifique que la fecha seleccionada sea coherente con la edad del animal, cierre la pantalla y vuelva a intentar. Si el problema persiste, reinicie la aplicación." | Si tras verificar los datos y reiniciar la app persiste el error de guardado, escalar a soporte técnico. |
| La fecha seleccionada no se puede marcar en el calendario | Se intenta seleccionar una fecha anterior al nacimiento de la vaca o posterior a la fecha actual | "El sistema no permite seleccionar fechas futuras ni fechas previas a la fecha de nacimiento de la vaca. Por favor seleccione la fecha real en que se produjo la pérdida reproductiva dentro del rango válido." | No escalar, restricción de integridad zootécnica de la aplicación. |
| Círculo de espera infinito / Pantalla congelada en cargando | Proceso en segundo plano bloqueado o timeout en el dispositivo al procesar el guardado local | "Espere 30 segundos. Si no avanza, cierre la aplicación por completo desde el administrador de tareas de su teléfono (deslizando hacia arriba) y vuelva a abrirla. Sus datos locales no se perderán." | Si tras reabrir la app el botón sigue deshabilitado o la pantalla vuelve a congelarse, transferir de inmediato a soporte humano con correo y modelo del teléfono. |

### Directivas de Seguridad y Guardrails
- NUNCA solicite contraseñas, credenciales de inicio de sesión ni información bancaria para asistir en el registro de eventos reproductivos.
- Recuerde al ganadero que el registro de un aborto altera el estado de preñez de la vaca; si el animal contaba con un diagnóstico de gestación positiva previa, el evento de aborto concluye formalmente dicho período reproductivo en los balances de fertilidad de la finca.
- Indique al usuario que para eliminar un registro erróneo debe contar con los permisos correspondientes de eliminación reproductiva, y que al borrarlo la aplicación restablecerá los indicadores históricos anteriores.
