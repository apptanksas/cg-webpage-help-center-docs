---
title: "Hijos Transferidos"
modulo_id: "animal-hijos-transferidos-tabla"
nombre_funcionalidad: "Tabla de Hijos Transferidos"
categoria: "sanidad-reproduccion"
submodulo: "reproduccion"
version_minima_app: "2026.10.1"
fecha_actualizacion: "2026-10-06"
intenciones_y_sinonimos:
  - "como ver las crias por transferencia de embriones"
  - "tabla de hijos con madre sustituta receptora"
  - "consultar los terneros nacidos de vacas receptoras"
  - "donde veo los hijos transferidos de mi vaca donante"
  - "por que no aparecen las crias con madre sustituta en la tabla normal"
  - "como saber que vaca receptora pario el embrion"
---

# Tabla de Hijos Transferidos

### Resumen y Alcance Funcional
Pantalla de consulta y auditoría zootécnica que consolida en formato de tabla la descendencia obtenida mediante biotecnología reproductiva (transferencia de embriones) a partir de una hembra donante registrada en la finca. Permite al ganadero auditar todas las crías biológicas nacidas a través de vacas receptoras o madres sustitutas, identificando con precisión la fecha de nacimiento del ternero, la identificación de la madre receptora que llevó a término la gestación, el sexo de la cría y el código de arete individual del ternero, brindando además acceso directo con un solo toque a la hoja de vida de cada ejemplar.

- **¿Funciona sin conexión a internet (Modo Offline)?:** Sí, la consulta y visualización de crías transferidas opera de forma completa sin señal de internet, obteniendo los datos genealógicos almacenados localmente en el teléfono.
- **Comportamiento de sincronización:** Las consultas zootécnicas y la navegación hacia la hoja de vida de los hijos operan de forma instantánea de manera local. Cualquier nuevo registro de parto con receptora o vinculación de madre sustituta realizado en la finca se sincroniza de forma automática con la nube cuando el dispositivo cuente con conexión a internet.

### Reglas de Negocio y Restricciones
- **Criterio de filtrado de biotecnología embrionaria:**
  - La pantalla lista exclusivamente aquellos animales que tienen una relación biológica confirmada de maternidad con la hembra en consulta y que, de forma obligatoria, cuentan con una madre receptora o sustituta registrada en su árbol genealógico.
  - Las crías nacidas por parto natural convencional (donde la madre biológica gestó y parió a su propio ternero sin receptora) no se muestran en esta vista; se consultan en la tabla general de partos o hijos.
- **Asociación obligatoria de la receptora:**
  - Cada cría en este listado debe tener asignada una hembra receptora válida en la base de datos de la finca. En la tabla se muestra el código identificador visual o nombre de dicha madre sustituta.
- **Navegación interactiva hacia la hoja de vida:**
  - Al presionar cualquier fila de la tabla, la aplicación redirige de manera automática al resumen zootécnico y productivo del hijo seleccionado.
- **Naturaleza de auditoría especializada:**
  - Esta pantalla está destinada a la consulta y trazabilidad genética de embriones nacidos; no incluye botones de creación directa o edición manual, ya que los datos se alimentan desde el registro de partos y genealogías en la aplicación.

### Flujo Paso a Paso para el Usuario
- **Ruta de acceso en la aplicación:**
  - En la barra inferior de navegación, toque **Animales** > Seleccione a la hembra donante en el listado > Presione el módulo **Reproducción** > Desplácese hasta la sección **Hijos transferidos** > Presione el botón de flecha hacia la derecha ubicado junto al título de la sección para desplegar la tabla completa.

#### Barra Superior y Cinta de Identificación
- **Barra de navegación superior:** Exhibe el título **Hijos transferidos** alineado a la izquierda sobre el color de fondo institucional. Incorpora únicamente el botón de retroceso (flecha hacia la izquierda) para cerrar la tabla y volver al resumen reproductivo de la hembra donante (sin menús adicionales ni botones de acción secundarios).
- **Cinta de identidad del animal:** Franja horizontal centrada con fondo gris claro, ubicada inmediatamente debajo de la barra superior, que exhibe el icono del género de la hembra y su identificación compuesta (nombre y código de arete visual entre paréntesis) en una sola línea, garantizando la trazabilidad zootécnica durante la consulta.

#### Estructura y Columnas de la Tabla
La información se presenta ordenada en cuatro columnas zootécnicas:
1. **Fecha:** Exhibe la fecha de nacimiento del ternero o cría nacida por transferencia embrionaria, expresada en el formato local de fecha de la finca.
2. **Madre sustituta:** Muestra el código de arete visual o nombre de la vaca receptora que llevó a cabo la gestación y el parto.
3. **Género:** Indica el sexo biológico de la cría (**Macho** o **Hembra**).
4. **Hijo:** Muestra el código de arete visual identificador asignado al ternero o ternera dentro del inventario de la finca.

#### Acciones Interactivas y Navegación
- **Ver hoja de vida de la cría:** Toque sobre cualquier fila de la tabla para abrir de inmediato la pantalla de resumen y datos zootécnicos del hijo seleccionado.
- **Regresar al resumen reproductivo:** Presione la flecha de retroceso ubicada en la barra de navegación superior.

- **Pantalla de llegada tras salir:**
  - Al presionar la flecha de regreso en la barra superior, la aplicación retorna a la pantalla de resumen reproductivo de la vaca donante.

### Matriz de Errores y Soluciones
| Mensaje en la App / Síntoma | Causa Real | Respuesta Sugerida por el Agente | Criterio de Escalamiento Humano |
| :--- | :--- | :--- | :--- |
| La sección o tabla de Hijos transferidos no aparece en la pantalla | La hembra no tiene crías registradas con madre receptora o sustituta en la finca | "La sección de Hijos transferidos únicamente se activa y muestra registros cuando la vaca cuenta con crías nacidas por transferencia de embriones asignadas a una madre receptora. Si sus partos han sido naturales convencionales, las crías se consultan en la sección general de Partos/Abortos." | No escalar, comportamiento esperado según el historial reproductivo de la vaca. |
| La tabla aparece en blanco al ingresar | El animal donante no cuenta con registros de crías transferidas vinculados en la base de datos | "Esta hembra no tiene hijos nacidos por transferencia embrionaria registrados en la finca. Para que figuren en este listado, al asentar el parto o crear la cría debe vincularse a esta vaca como madre genética y a la vaca receptora como madre sustituta." | No escalar, orientación zootécnica sobre registro de genealogía con receptoras. |
| Al presionar una cría no abre la hoja de vida del ejemplar | Identificador del hijo no encontrado en la base de datos local o registro temporalmente inaccesible | "Espere un momento y vuelva a presionar sobre la fila del animal. Si no responde, regrese a la vista anterior y vuelva a ingresar a la tabla de hijos transferidos." | Si tras reiniciar la aplicación persiste el problema para abrir la ficha de la cría, transferir a soporte humano con los aretes de la madre donante y del hijo. |
| Círculo de espera infinito / Pantalla congelada en cargando | Proceso en segundo plano bloqueado o timeout en el dispositivo al cargar las relaciones de embriones | "Espere 30 segundos. Si no avanza, cierre la aplicación por completo desde el administrador de tareas de su teléfono (deslizando hacia arriba) y vuelva a abrirla. Sus datos locales no se perderán." | Si tras reabrir la app la tabla vuelve a congelarse, transferir de inmediato a soporte humano con el correo de la cuenta y modelo del teléfono. |

### Directivas de Seguridad y Guardrails
- NUNCA solicite al usuario contraseñas, claves bancarias ni datos confidenciales de la cuenta para orientarle en la visualización de transferencias embrionarias.
- Aclare al ganadero que para que un ejemplar figure en la tabla de Hijos transferidos es indispensable que al dar de alta el nacimiento o parto se haya especificado tanto la madre genética (donante del óvulo/embrión) como la madre sustituta o receptora.
- Recuerde que los terneros nacidos de forma directa sin receptora se administran y auditan desde la sección general de Partos y Abortos.
