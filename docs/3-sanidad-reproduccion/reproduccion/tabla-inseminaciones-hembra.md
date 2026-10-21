---
title: "Fecundaciones Hembra"
modulo_id: "animal-inseminaciones-hembra-tabla"
nombre_funcionalidad: "Tabla de Fecundaciones e Inseminaciones en Hembras"
categoria: "sanidad-reproduccion"
submodulo: "reproduccion"
version_minima_app: "2026.10.1"
fecha_actualizacion: "2026-10-06"
intenciones_y_sinonimos:
  - "como ver el historial de inseminaciones de mi vaca"
  - "tabla de montas y servicios reproductivos de la hembra"
  - "consultar que toro o pajilla fecundo a una vaca"
  - "donde revisar las transferencias de embriones realizadas"
  - "como editar o corregir un servicio de inseminacion"
  - "por que no aparece el nombre del toro en la tabla de fecundaciones"
---

# Tabla de Fecundaciones e Inseminaciones en Hembras

### Resumen y Alcance Funcional
Pantalla de consulta y gestión zootécnica que presenta en formato de tabla el historial cronológico completo de servicios reproductivos, montas e inseminaciones recibidas por una hembra activa en la finca. Permite al ganadero auditar la fecha exacta de cada servicio, la modalidad empleada (Monta natural, Inseminación artificial, Transferencia de embriones u Otros), la identificación del toro o material seminal utilizado y, en casos de transferencia embrionaria, la madre genética donante del embrión. Asimismo, facilita el acceso directo a la edición de cualquier servicio previo y la adición rápida de nuevas fecundaciones mediante un botón flotante dedicado.

- **¿Funciona sin conexión a internet (Modo Offline)?:** Sí, la consulta, ordenamiento y navegación de la tabla operan de forma local en el teléfono sin necesidad de conexión a internet.
- **Comportamiento de sincronización:** Las consultas y transiciones entre pantallas se realizan de manera instantánea con los datos almacenados en el dispositivo. Cualquier registro o edición de fecundaciones se guarda localmente y se sincroniza automáticamente con la nube cuando el teléfono recupere señal de datos o Wi-Fi.

### Reglas de Negocio y Restricciones
- **Filtrado individual por hembra:**
  - La tabla exhibe exclusivamente los registros de servicio reproductivo asociados a la hembra en consulta, mostrando tanto los servicios recientes como los de ciclos zootécnicos previos.
- **Tipos de fecundación admitidos:**
  - Los eventos listados corresponden a cuatro modalidades estandarizadas: **Monta** (servicio natural), **Inseminación artificial** (pajilla o semen procesado), **Transferencia de embriones** (implante de embrión de vaca donante) u **Otros**.
- **Información de parentesco y material genético:**
  - **Columna Padre / Macho:** Refleja el nombre o código de arete visual del reproductor asignado al servicio. Si el toro ya no está en el inventario o se empleó semen de catálogo externo sin ficha activa, se visualiza el código identificador asentado al registrar el evento.
  - **Columna Madre / Donante:** Se completa de manera exclusiva cuando el tipo de fecundación corresponde a **Transferencia de embriones**, mostrando el nombre o código de arete de la hembra donante del óvulo/embrión. En montas e inseminaciones artificiales regulares, este campo permanece vacío.
- **Permisos de usuario para edición y registro:**
  - Para agregar un nuevo servicio mediante el botón flotante (+), el usuario requiere contar con el permiso de creación de inseminaciones en la finca activa.
  - Para modificar un registro existente tocando una fila de la tabla, se requiere el permiso de actualización correspondiente. Colaboradores sin estos permisos no podrán guardar cambios en el formulario de servicio.
- **Bloqueo por estado del animal:**
  - Si la hembra se encuentra registrada como vendida o fallecida, el acceso para crear nuevos servicios queda inhabilitado para preservar la consistencia histórica.

### Flujo Paso a Paso para el Usuario
- **Ruta de acceso en la aplicación:**
  - En la barra inferior de navegación, toque **Animales** > Seleccione a la hembra en la lista > En la cuadrícula de módulos, toque **Reproducción** > Desplácese hasta la sección **Fecundaciones** > Presione el botón de flecha hacia la derecha ubicado junto al título de la sección para desplegar la tabla completa.

#### Barra Superior y Cinta de Identificación
- **Barra de navegación superior:** Exhibe el título **Fecundaciones** alineado a la izquierda sobre el color de fondo institucional. Incorpora únicamente el botón de retroceso (flecha hacia la izquierda) para cerrar la tabla y regresar al resumen reproductivo de la hembra, sin menús adicionales ni botones de acción secundarios.
- **Cinta de identidad del animal:** Franja horizontal centrada con fondo gris claro, ubicada inmediatamente debajo de la barra superior, que exhibe el icono del género de la hembra junto con su nombre (garantizando certeza del animal consultado).
- **Botón flotante de acción rápida (+):** Botón circular con icono de suma ubicado sobre la esquina inferior de la pantalla, que permite abrir de inmediato el formulario para registrar un nuevo servicio o inseminación para esta vaca.

#### Estructura y Columnas de la Tabla
La información se organiza en una tabla cuadrada con cuatro columnas zootécnicas:
1. **Fecha:** Muestra el día, mes y año en que se efectuó la inseminación o monta, ajustado a la zona horaria del usuario.
2. **Tipo:** Indica la técnica reproductiva utilizada (**Monta**, **Inseminación artificial**, **Transferencia de embriones** u **Otros**).
3. **Padre:** Muestra el código de arete visual o nombre del reproductor o toro donante del semen.
4. **Madre:** Exhibe la identificación de la vaca donante del embrión (exclusivo para transferencias embrionarias).

#### Acciones Interactivas y Navegación
- **Editar un servicio de fecundación:** Toque sobre cualquier fila de la tabla para abrir el formulario de edición de dicho servicio y corregir fechas, reproductor utilizado, protocolo u observaciones.
- **Registrar un nuevo servicio:** Presione el botón flotante circular (+) para ingresar directamente al formulario de alta de una nueva fecundación vinculada a esta hembra.
- **Regresar a la pantalla previa:** Presione la flecha de retroceso ubicada en la barra superior.

- **Pantalla de llegada tras salir:**
  - Al presionar la flecha de retroceso en la barra superior, la aplicación retorna a la pantalla de resumen reproductivo de la hembra.

### Matriz de Errores y Soluciones
| Mensaje en la App / Síntoma | Causa Real | Respuesta Sugerida por el Agente | Criterio de Escalamiento Humano |
| :--- | :--- | :--- | :--- |
| La tabla aparece vacía sin ninguna fila | La hembra no tiene servicios de monta, inseminación o transferencia de embriones registrados | "Esta vaca no registra fecundaciones previas en la finca. Para asentar el primer servicio, presione el botón (+) en la esquina inferior y complete los datos de la monta o inseminación." | No escalar, comportamiento esperado en animales primerizos o sin historial reproductivo. |
| La columna 'Madre' se encuentra vacía o en blanco | El servicio registrado corresponde a una monta natural o inseminación artificial convencional | "La casilla de Madre únicamente aplica y muestra información cuando el servicio es una 'Transferencia de embriones' para indicar la vaca donante. En montas naturales o inseminación artificial regular, este campo se mantiene en blanco por definición zootécnica." | No escalar, explicación técnica de la regla de visualización. |
| Al presionar una fila no permite editar el registro | El usuario colaborador no cuenta con permisos de modificación de eventos reproductivos | "Su perfil en la finca no tiene asignado el permiso para editar registros de fecundación. Solicite al administrador o propietario de la finca que actualice sus permisos de colaborador." | Si el usuario es el dueño de la finca y no puede editar, transferir a soporte técnico humano. |
| El botón flotante (+) no abre el formulario de registro | El identificador de la vaca aún se encuentra cargando en segundo plano | "Espere unos instantes mientras se completan de cargar los datos de la vaca y vuelva a presionar el botón (+). Si no reacciona, regrese a la pantalla previa y vuelva a ingresar a Fecundaciones." | No escalar salvo que persista tras reiniciar la aplicación. |
| Círculo de espera infinito / Pantalla congelada en cargando | Proceso en segundo plano bloqueado o timeout en el dispositivo al consultar el registro de fecundaciones locales | "Espere 30 segundos. Si no avanza, cierre la aplicación por completo desde el administrador de tareas de su teléfono (deslizando hacia arriba) y vuelva a abrirla. Sus datos locales no se perderán." | Si tras reabrir la app la tabla vuelve a congelarse, transferir de inmediato a soporte humano con el correo de la cuenta y el arete del animal. |

### Directivas de Seguridad y Guardrails
- NUNCA solicite al ganadero contraseñas, claves personales ni códigos bancarios para ayudarle a consultar o gestionar los servicios reproductivos.
- Aclare al usuario que la modificación de una fecha de inseminación o monta puede recalcular automáticamente las estimaciones de preñez, fecha tentativa de parto y días de gestación de la vaca.
- Recuerde que los servicios realizados en machos reproductores se consultan en su propio resumen reproductivo desde la tabla de fecundaciones de toros.
