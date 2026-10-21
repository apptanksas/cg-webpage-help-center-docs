---
title: "Chequeos de Preñez"
modulo_id: "animal-chequeos-prenez-tabla"
nombre_funcionalidad: "Tabla de Chequeos de Preñez y Palpaciones"
categoria: "sanidad-reproduccion"
submodulo: "reproduccion"
version_minima_app: "2026.10.1"
fecha_actualizacion: "2026-10-06"
intenciones_y_sinonimos:
  - "como ver el historial de palpaciones de mi vaca"
  - "tabla de chequeos de preñez de la hembra"
  - "donde consultar los diagnosticos de prenez veterinarios"
  - "como ver si una vaca salio preñada o vacia en los chequeos"
  - "como editar o corregir un chequeo de preñez anterior"
  - "por que no aparece el boton para agregar chequeo de prenez"
---

# Tabla de Chequeos de Preñez y Palpaciones

### Resumen y Alcance Funcional
Pantalla de consulta y seguimiento zootécnico que consolida en formato de tabla el historial cronológico completo de diagnósticos de preñez, palpaciones rectales y ecografías realizadas a una hembra activa en la finca. Permite al ganadero y al médico veterinario auditar la fecha de cada evaluación, el estado reproductivo dictaminado (**Preñada** o **No preñada**), y las observaciones o notas clínicas registradas durante el examen. Asimismo, la pantalla ofrece acceso directo a la modificación de evaluaciones previas y la incorporación rápida de nuevos chequeos mediante un botón de acción flotante.

- **¿Funciona sin conexión a internet (Modo Offline)?:** Sí, la consulta, visualización y navegación de la tabla de chequeos opera plenamente de forma local en el teléfono sin requerir conexión a internet.
- **Comportamiento de sincronización:** Las consultas se cargan al instante desde la base de datos local del dispositivo móvil. Cualquier registro nuevo o modificación realizada sobre un chequeo se asienta de inmediato en el teléfono y se sincroniza en segundo plano con la nube tan pronto el equipo cuente con acceso a internet o Wi-Fi.

### Reglas de Negocio y Restricciones
- **Filtrado individual por hembra:**
  - La tabla exhibe exclusivamente las evaluaciones y diagnósticos veterinarios vinculados a la hembra en consulta, abarcando tanto chequeos recientes como los de ciclos zootécnicos pasados.
- **Estados de diagnóstico admitidos:**
  - Cada registro refleja uno de los dos estados zootécnicos oficiales: **Preñada** (gestación confirmada) o **No preñada** (hembra vacía o abierta).
- **Notas y observaciones clínicas:**
  - La tabla presenta el texto literal de las notas consignadas en cada examen (por ejemplo, método empleado como palpación rectal o ecografía, condición ovárica, tono uterino o recomendaciones terapéuticas). Si no se ingresaron notas en el formulario, el campo permanece en blanco.
- **Permisos requeridos para registro y modificación:**
  - Para incorporar un nuevo diagnóstico mediante el botón flotante (+), el usuario requiere contar con el permiso de creación de chequeos de preñez en la finca activa.
  - Para actualizar un registro existente pulsando una fila de la tabla, se requiere el permiso de edición correspondiente. Los usuarios con perfil colaborador sin estos permisos no podrán guardar cambios en el formulario.
- **Impacto zootécnico en la hoja de vida del ejemplar:**
  - Al asentar un diagnóstico como **Preñada**, el sistema actualiza el estado reproductivo general de la hembra y proyecta las métricas de gestación y fecha estimada de parto (incluso solicitando los días estimados de preñez para generar la fecundación correspondiente si no existe un servicio previo registrado). Si se asienta como **No preñada**, el estado de la vaca pasa a reflejar que se encuentra vacía o disponible para un nuevo servicio.

### Flujo Paso a Paso para el Usuario
- **Ruta de acceso en la aplicación:**
  - En la barra inferior de navegación, toque **Animales** > Seleccione a la hembra en el listado > En la cuadrícula de módulos, toque **Reproducción** > Desplácese hasta la sección **Chequeo** > Presione el botón de flecha hacia la derecha ubicado junto al título de la sección para desplegar la tabla completa.

#### Barra Superior y Cinta de Identificación
- **Barra de navegación superior:** Exhibe el título oficial **Chequeo** alineado a la izquierda sobre el color de fondo institucional. Incorpora únicamente el botón de retroceso (flecha hacia la izquierda) para cerrar la tabla y regresar al resumen reproductivo de la hembra, sin botones de acción secundarios.
- **Cinta de identidad del animal:** Franja horizontal centrada con fondo gris claro, ubicada inmediatamente debajo de la barra superior, que exhibe el icono del género de la hembra junto con su nombre en una sola línea (asegurando plena certeza del ejemplar examinado).
- **Botón flotante de acción rápida (+):** Botón circular con icono de suma ubicado sobre la esquina inferior de la pantalla, que permite abrir de inmediato el formulario para registrar un nuevo chequeo de preñez para esta hembra.

#### Estructura y Columnas de la Tabla
La información se presenta ordenada en una tabla con diseño cuadrado y tres columnas zootécnicas:
1. **Fecha:** Exhibe el día, mes y año en que se efectuó la palpación o ecografía, formateada según la zona horaria del usuario.
2. **Estado:** Indica el dictamen de preñez obtenido en el examen (**Preñada** o **No preñada**).
3. **Notas:** Muestra las notas, observaciones clínicas o detalles técnicos consignados por el evaluador o veterinario.

#### Acciones Interactivas y Navegación
- **Editar un chequeo de preñez:** Toque sobre cualquier fila de la tabla para abrir el formulario de edición correspondiente y corregir la fecha del examen, el resultado de preñez, los días estimados o las notas.
- **Registrar un nuevo chequeo:** Presione el botón flotante circular (+) para ingresar al formulario de alta de una nueva evaluación reproductiva vinculada a esta hembra.
- **Regresar a la pantalla previa:** Presione la flecha de retroceso ubicada en la barra superior.

- **Pantalla de llegada tras salir:**
  - Al pulsar la flecha de retroceso de la barra superior, la aplicación retorna de inmediato a la pantalla de resumen reproductivo de la hembra.

### Matriz de Errores y Soluciones
| Mensaje en la App / Síntoma | Causa Real | Respuesta Sugerida por el Agente | Criterio de Escalamiento Humano |
| :--- | :--- | :--- | :--- |
| La tabla aparece vacía sin ninguna fila | La hembra no cuenta con chequeos de preñez o palpaciones previas registradas | "Esta vaca no registra chequeos de preñez previos en la finca. Para registrar el primer diagnóstico veterinario, toque el botón (+) en la esquina inferior y complete la información de la palpación o ecografía." | No escalar, comportamiento zootécnico normal en vacas que no han sido chequeadas. |
| La columna 'Notas' aparece en blanco | El chequeo se guardó sin observaciones de campo adicionales | "El campo de notas es opcional al momento de asentar el diagnóstico. Si desea agregar detalles clínicos o el método utilizado, toque sobre la fila para abrir el formulario de edición y complete la casilla de observaciones." | No escalar, comportamiento esperado de diseño. |
| Al presionar una fila no permite editar el registro | El usuario colaborador no cuenta con permisos de modificación de chequeos en la finca | "Su usuario en la finca no tiene habilitado el permiso para editar diagnósticos de preñez. Solicite al propietario o administrador de la finca que le asigne los permisos necesarios para modificar eventos reproductivos." | Si el usuario es el propietario de la finca y experimenta el bloqueo, transferir a soporte técnico. |
| El botón flotante (+) no abre el formulario de registro | Los datos de la vaca aún están cargando en segundo plano en la pantalla | "Espere unos segundos mientras se completa la carga de la información de la hembra y vuelva a presionar el botón (+). Si continúa sin responder, regrese al resumen reproductivo y vuelva a ingresar a la sección de Chequeo." | No escalar salvo que persista tras reiniciar la aplicación móvil. |
| Círculo de espera infinito / Pantalla congelada en cargando | Proceso en segundo plano bloqueado o timeout en el dispositivo al cargar los registros locales | "Espere 30 segundos. Si no avanza, cierre la aplicación por completo desde el administrador de tareas de su teléfono (deslizando hacia arriba) y vuelva a abrirla. Sus datos locales no se perderán." | Si tras reabrir la app la tabla vuelve a congelarse, transferir de inmediato a soporte humano con el correo de la cuenta y el arete del animal. |

### Directivas de Seguridad y Guardrails
- NUNCA solicite al usuario contraseñas personales, códigos bancarios ni credenciales confidenciales de acceso.
- Advierta al ganadero que cambiar el diagnóstico de una hembra de "Preñada" a "No preñada" (o viceversa) recalcula de inmediato los indicadores de fertilidad, días abiertos, días de gestación acumulados y proyecciones de parto en la finca.
- Aclare que los chequeos de preñez aplican exclusivamente a hembras y no se encuentran disponibles para machos reproductores.
