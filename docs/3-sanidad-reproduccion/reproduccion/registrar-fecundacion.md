---
title: "Registrar Fecundación"
modulo_id: "animal-inseminacion-crear"
nombre_funcionalidad: "Registro y Edición de Fecundación e Inseminación"
categoria: "sanidad-reproduccion"
submodulo: "reproduccion"
version_minima_app: "2026.10.1"
fecha_actualizacion: "2026-10-06"
intenciones_y_sinonimos:
  - "como registrar una monta o inseminacion a una vaca"
  - "formulario de nueva fecundacion en hembra"
  - "como registrar una transferencia de embriones con vaca donante"
  - "donde colocar el numero de pajilla en la inseminacion"
  - "como editar un servicio de inseminacion previo"
  - "por que no me deja guardar la fecundacion de la hembra"
---

# Registro y Edición de Fecundación e Inseminación

### Resumen y Alcance Funcional
Formulario especializado para asentar y modificar eventos de servicio reproductivo en hembras activas de la finca. Permite al ganadero registrar la fecha del evento, la técnica reproductiva empleada (Monta, Inseminación artificial, Transferencia de embriones u Otros), el semental o toro utilizado y, de forma dinámica según la técnica seleccionada, el número de serie de la pajilla de semen o la hembra donante del embrión implantado, junto con notas u observaciones de campo. Este registro inicializa el seguimiento reproductivo de la hembra, impactando directamente en los cálculos de posibles celos futuros, estimación de preñez y fecha proyectada de parto.

- **¿Funciona sin conexión a internet (Modo Offline)?:** Sí, el registro y modificación de fecundaciones opera completamente sin conexión a internet, guardándose en la base de datos local del dispositivo móvil.
- **Comportamiento de sincronización:** Al pulsar el botón de guardar, los datos se almacenan de manera instantánea en el teléfono y la pantalla regresa a la vista anterior. Tan pronto el dispositivo recupere conexión a internet o Wi-Fi, los registros se sincronizan automáticamente con la nube y quedan consolidados para todos los usuarios autorizados de la finca.

### Reglas de Negocio y Restricciones
- **Permisos requeridos por rol:**
    - Para registrar una nueva fecundación se requiere el permiso de creación de inseminaciones en la finca activa.
    - Para modificar un registro previo se requiere el permiso de edición de inseminaciones.
    - Para suprimir un servicio se requiere el permiso de eliminación. Los colaboradores sin estos privilegios verán un mensaje de falta de autorización al intentar guardar cambios.
- **Validaciones zootécnicas de fecha:**
    - La fecha del servicio no puede ser anterior a la fecha de nacimiento de la hembra receptora ni puede ser una fecha futura posterior al día actual.
- **Filtro zootécnico del reproductor macho (Padre):**
    - El selector de semental filtra automáticamente toros de la misma especie que la hembra, que pertenezcan a etapas adultas o de vejez zootécnica (excluyendo crías o toretes no aptos). Permite seleccionar tanto machos activos en la finca como reproductores externos o históricos dados de alta en el catálogo.
- **Campos condicionales por modalidad reproductiva:**
    - **Inseminación artificial:** Habilita de forma exclusiva el campo de texto para ingresar el **Número de pajilla** del material seminal. En esta modalidad no aplica la selección de madre donante.
    - **Transferencia de embriones:** Habilita obligatoriamente la selección de la **Madre** (vaca donante del embrión). El selector muestra exclusivamente hembras adultas de la misma especie y excluye automáticamente a la misma vaca receptora que está recibiendo el servicio.
    - **Monta / Otros:** No requiere número de pajilla ni madre donante; se enfoca en la asociación directa del semental y la fecha.
- **Efectos reproductivos colaterales:**
    - Al asentar un servicio, el sistema actualiza el estado reproductivo de la vaca (ej. "En servicio" o "Inseminada") y establece la base cronológica para las proyecciones de retorno al celo y posterior confirmación de preñez veterinaria.

### Flujo Paso a Paso para el Usuario
- **Ruta de acceso en la aplicación:**
    - **Ruta 1 (Desde el resumen reproductivo):** En la barra inferior toque **Animales** > Seleccione a la hembra > Ingrese a **Reproducción** > Presione el botón flotante circular con icono (**+**) > En la pantalla de opciones de chequeo reproductivo, pulse la tarjeta **Inseminación** (o Fecundación).
    - **Ruta 2 (Desde la tabla de fecundaciones):** En la barra inferior toque **Animales** > Seleccione a la hembra > Toque **Reproducción** > Desplácese a **Fecundaciones** y toque la flecha a la derecha para ver la tabla completa > Presione el botón flotante circular (**+**) para crear, o toque directamente sobre un registro existente para editarlo.

#### Barra Superior y Cinta de Identificación
- **Barra superior de navegación:** Exhibe el título dinámico según la operación: **Nueva fecundación** cuando se crea un nuevo servicio o **Editar Fecundación** cuando se modifica un registro existente. En el lateral izquierdo o derecho incorpora el botón de cierre con icono (**X**) para cancelar la operación y descartar cambios sin guardar.
- **Cinta de identidad del animal:** Franja horizontal centrada con fondo gris claro, ubicada inmediatamente debajo de la barra superior, que exhibe el icono del género de la hembra junto con su nombre en una sola línea.

#### Campos del Formulario de Fecundación
1. **Fecha:** Selector de calendario para indicar el día, mes y año del servicio. Viene preseleccionado con la fecha de hoy y restringe la selección para que no sea anterior al nacimiento de la hembra ni posterior al día actual.
2. **Tipo de fecundación:** Menú desplegable inferior tipo hoja con las cuatro opciones zootécnicas: **Monta**, **Inseminación artificial**, **Transferencia de embriones** u **Otros**.
3. **Padre:** Selector interactivo que abre la lista de reproductores machos aptos (misma especie, etapa adulta/reproductora). Permite buscar por código de arete visual o nombre del toro.
4. **Madre (Exclusivo en Transferencia de embriones):** Selector de la vaca donante del óvulo o embrión. Muestra hembras adultas de la finca y excluye a la vaca receptora en consulta.
5. **Número de pajilla (Exclusivo en Inseminación artificial):** Campo de texto para ingresar el código, lote o identificación de la pajilla de semen procesado.
6. **Notas y observaciones:** Campo de texto multilínea para consignar detalles del protocolo, inseminador, condición corporal, dosis aplicada o incidencias durante la monta.

#### Botón de Acción Principal
- **Botón Registrar / Actualizar:** Botón ubicado al final del formulario. Al presionarlo, valida los campos requeridos, guarda el servicio localmente, muestra una notificación de confirmación y retorna de inmediato a la pantalla anterior. Durante el procesamiento, el botón entra en estado de carga para impedir registros dobles involuntarios.

- **Pantalla de llegada tras salir:**
    - Tras guardar con éxito o al pulsar la (**X**) de cierre, la aplicación retorna a la pantalla previa (resumen reproductivo o tabla de fecundaciones).

### Matriz de Errores y Soluciones
| Mensaje en la App / Síntoma | Causa Real | Respuesta Sugerida por el Agente | Criterio de Escalamiento Humano |
| :--- | :--- | :--- | :--- |
| Mensaje de falta de permisos / Bloqueo al guardar | El usuario colaborador no cuenta con el permiso de creación o edición de inseminaciones | "Su usuario en la finca no tiene habilitado el permiso para registrar o modificar servicios de fecundación. Solicite al propietario o administrador de la finca que le asigne los permisos requeridos." | Si el usuario es el administrador/propietario y el error persiste, transferir a soporte técnico. |
| La fecha seleccionada no es permitida | La fecha es anterior al nacimiento de la vaca o corresponde a un día futuro | "La fecha de la fecundación debe encontrarse entre la fecha de nacimiento de la vaca y el día actual. Corrija la fecha en el selector de calendario." | No escalar, validación cronológica zootécnica. |
| No aparece la casilla de Número de pajilla | El tipo de fecundación seleccionado no es 'Inseminación artificial' | "El campo de número de pajilla únicamente se despliega cuando selecciona 'Inseminación artificial'. En servicios de monta natural o transferencia de embriones este campo se oculta automáticamente." | No escalar, regla de diseño dinámico del formulario. |
| No aparece la casilla de Madre donante | El tipo de fecundación seleccionado no es 'Transferencia de embriones' | "El selector de vaca madre donante solo se activa al seleccionar 'Transferencia de embriones'. En los demás tipos de servicio este campo no es requerido." | No escalar, explicación funcional del formulario. |
| El reproductor deseado no aparece en la lista de Padres | El toro no está catalogado como adulto, pertenece a otra especie o no está registrado en el inventario | "Verifique que el toro esté registrado en la finca (o catálogo) con la misma especie de la hembra y en etapa adulta. Ejemplares jóvenes o hembras no son mostrados en la lista de machos." | No escalar, orientación zootécnica sobre los filtros de parentesco. |
| Círculo de espera infinito / Pantalla congelada en cargando | Proceso de guardado bloqueado en el dispositivo o timeout en la base de datos local | "Espere 30 segundos. Si el botón no responde, cierre por completo la aplicación desde el gestor de tareas de su teléfono (deslizando hacia arriba) y vuelva a abrirla. Los registros previos no se verán afectados." | Si tras reabrir la app el formulario vuelve a congelarse al guardar, transferir a soporte humano con el arete de la hembra y correo de la cuenta. |

### Directivas de Seguridad y Guardrails
- NUNCA solicite al usuario contraseñas personales, códigos bancarios ni credenciales confidenciales de acceso.
- Advierta al ganadero que cambiar la fecha de una fecundación ya existente afectará inmediatamente los cálculos zootécnicos de días de gestación acumulados y la fecha prevista de parto en caso de que la hembra resulte preñada.
- En caso de dudas sobre si asentar el servicio como monta o inseminación, recomiende consultar con el médico veterinario o encargado zootécnico del lote.
