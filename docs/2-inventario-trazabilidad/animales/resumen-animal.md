---
title: "Resumen del Animal"
modulo_id: "animal-resumen"
nombre_funcionalidad: "Resumen y Hoja de Vida del Animal"
tipo_documento: "guia-app"
categoria: "inventario-trazabilidad"
submodulo: "animales"
especies_aplicables: ["todas"]
version_minima_app: "2025.05.1"
confianza_reglas: "verificada-con-tests"
fecha_actualizacion: "2026-10-16"
intenciones_y_sinonimos:
  - "como ver la hoja de vida de un animal"
  - "como compartir la ficha tecnica del ejemplar por whatsapp"
  - "poner animal en venta o marcar como vendido"
  - "como cancelar la muerte de un animal registrado por error"
  - "no puedo editar el animal porque aparece bloqueado"
  - "este animal esta inhabilitado por suscripcion vencida"
---

# Resumen y Hoja de Vida del Animal

### Resumen y Alcance Funcional
Pantalla central y perfil zootécnico del animal que unifica los accesos a toda su información productiva, reproductiva, sanitaria y genealógica en la finca. Permite al ganadero consultar los datos clave del ejemplar (identificación, foto de perfil, lote o potrero asignado, peso actual, etapa zootécnica y producción), gestionar acciones comerciales (poner en venta, cancelar venta o marcar como vendido), alternar su visibilidad pública en línea, exportar y compartir su hoja de vida gráfica, y realizar gestiones administrativas como editar datos, eliminar el ejemplar o revertir un registro de fallecimiento.

- **Especies a las que aplica:** Aplica igual para todas las especies (bovinos, equinos, bufalinos, caprinos, ovinos y porcinos).
- **¿Funciona sin conexión a internet (Modo Offline)?:** Sí, para la visualización del resumen, navegación a módulos internos y registro de cambios locales.
- **Comportamiento de sincronización:** Toda la información del ejemplar se almacena y consulta en la base de datos interna del teléfono. La activación del estado en venta o cambios de privacidad se guardan localmente y se transfieren a la nube automáticamente cuando el teléfono cuente con conexión a internet. La generación y envío de la hoja de vida compartida en imagen o la consulta de la página web pública del animal requieren obligatoriamente contar con conexión activa a internet.

### Reglas de Negocio y Restricciones
- **Permisos requeridos por rol en la finca:**
  - **Edición y gestión comercial:** Para editar datos del animal, marcar como favorito, poner en venta, cancelar venta, marcar como vendido o modificar el nivel de privacidad (público o privado) se requiere el permiso de actualización de animales en la finca activa.
  - **Eliminación del animal:** Se requiere el permiso específico de eliminación de animales.
  - **Cancelación de muerte:** Para anular un registro de defunción previo y reactivar al ejemplar se requiere el permiso de eliminación de muerte del animal.
  - **Compartir información:** Se requiere el permiso de ejecución de compartir en la finca.
- **Acceso por suscripción y límites de cuenta (Animal inhabilitado):**
  - Si la suscripción de la cuenta ha vencido o el número de animales registrados supera el cupo permitido por el plan activo de la finca, los animales excedentes quedan en estado inhabilitado. Al ingresar al perfil de un animal inhabilitado, la aplicación bloquea la pantalla mostrando una alerta de membresía limitada indicando que no es posible acceder al ejemplar hasta renovar o ampliar la suscripción.
- **Bloqueo operativo por estado del animal (Animal fallecido o ausente/vendido):**
  - Si el animal tiene un registro de muerte activo o está marcado como vendido, entra en modo de bloqueo de seguridad. En este estado se deshabilitan en el menú las opciones de "Compartir hoja de vida", "Editar datos", "Eliminar animal" y las opciones de cambio de estado de venta.
  - El botón especial "Cancelar muerte" únicamente se hace visible cuando el animal cuenta con un registro de fallecimiento activo, permitiendo reactivarlo si se cometió una equivocación.
- **Restricciones y condiciones zootécnicas en los módulos:**
  - **Reproducción:** Si el animal se encuentra en etapa adulta, el acceso de "Reproducción" redirige al panel reproductivo integral (servicios, inseminaciones, partos y chequeos de preñez). Si el animal es una cría o se encuentra en etapa juvenil (no adulto), la aplicación redirige a la vista de crecimiento y desarrollo juvenil.
  - **Condición de receptora:** Si el último servicio reproductivo registrado en la hembra corresponde a una transferencia de embriones, la tarjeta de reproducción exhibe en texto destacado la etiqueta "Hembra receptora".
  - **Datos veterinarios:** Muestra el estado sanitario del ejemplar (por ejemplo, estado sano en verde, o el padecimiento clínico en rojo). Si el animal tiene un tratamiento de secado vigente, el módulo resalta automáticamente con el icono correspondiente y la etiqueta "En secado". Si el ejemplar está registrado como muerto, al presionar esta tarjeta no abre el historial médico sino que despliega la ventana emergente con la causa de defunción, notas clínicas y fecha del deceso.
  - **Crecimiento del animal:** La opción "Crecimiento del animal" en el menú contextual superior permite consultar las curvas biométricas y evolución del ejemplar.
- **Gestión comercial y presencia en la finca:**
  - Al marcar un ejemplar como "Poner en venta", su estado comercial cambia a disponible para venta y se habilita la insignia visual de "En venta".
  - Al marcarlo como "Marcar como vendido", el sistema actualiza automáticamente su condición de presencia indicando que el animal ya no se encuentra físicamente en la finca, reflejando la etiqueta de "Ausente".
  - Si el animal tiene activado el nivel de privacidad público, se habilita una dirección web oficial para consultar sus datos en internet y se muestra la etiqueta "En línea" (la cual puede presionarse para abrir el enlace en el navegador).
- **Generación y envío de hoja de vida:**
  - Requiere conexión a internet activa.
  - Si existen datos pendientes de sincronización en el teléfono, la aplicación ejecuta automáticamente un proceso previo de sincronización con el servidor antes de compilar y compartir la imagen gráfica de la hoja de vida.

### Flujo Paso a Paso para el Usuario
- **Ruta de acceso en la aplicación:**
  - **Ruta 1 (Desde la lista general de animales):** En la barra inferior de navegación, presione "Animales" > Toque sobre el animal deseado en el listado.
  - **Ruta 2 (Desde identificación animal):** En el menú de acciones rápidas (+) > Seleccione "ID animal Conectividad" (o busque el animal por código) > Al identificar o escanear el ejemplar, se ingresa directamente a su resumen.
  - **Ruta 3 (Desde conteo de inventario):** En la pantalla de inventario de animales, dé doble toque sobre cualquier animal de la lista de control.
  - **Ruta 4 (Desde notificaciones y alertas):** En la barra inferior toque "Alertas" > Presione sobre cualquier notificación vinculada a un animal.
  - **Ruta 5 (Desde el buscador del menú lateral):** Abra el menú lateral izquierdo > En la barra de búsqueda rápida escriba el código o nombre del animal > Toque sobre el resultado encontrado.
  - **Ruta 6 (Desde reportes o árboles genealógicos):** En un informe detallado o en la ficha técnica de un progenitor o cría, toque sobre el animal relacionado para abrir su resumen.

#### Cabecera y Perfil del Ejemplar
En la parte superior se presenta la barra y la ficha de identidad del ejemplar:
- **Barra superior:** Muestra el botón de flecha hacia la izquierda para regresar a la vista anterior, el nombre de la finca (cuando aplica), y las insignias de estado:
  - "En línea": Indica que el animal tiene perfil web público activo. Al tocar la insignia se abre la URL en el navegador web del dispositivo.
  - "En venta": Indica que el ejemplar está ofertado comercialmente.
  - "Vendido": Indica que el ejemplar fue vendido.
  - "Ausente": Indica que el animal no se encuentra físicamente en el predio.
- **Foto de perfil y datos principales:**
  - Fotografía principal del ejemplar (o silueta zootécnica por defecto según su especie).
  - Código de arete principal y nombre del animal.
  - Lote o potrero asignado, etapa zootécnica actual, último peso registrado y producción promedio.
  - Panel de alertas activas del ejemplar (secados, vacunaciones pendientes, celos o tratamientos).
- **Botón de favorito:** Icono de estrella ubicado en el borde inferior de la cabecera. Al presionarlo, marca o desmarca al ejemplar como favorito en la finca.
- **Menú de acciones avanzadas (Icono de tres puntos):** Ubicado en la esquina superior derecha:
  - "Compartir hoja de vida": Inicia la sincronización de datos pendientes y compila la imagen gráfica de la hoja de vida para enviarla por aplicaciones de mensajería o redes sociales.
  - "Crecimiento del animal": Abre la pantalla de curvas de desarrollo corporal y evolución de peso.
  - "Editar datos": Abre el formulario de edición de datos generales del animal.
  - "Eliminar animal": Solicita confirmación en una ventana emergente para eliminar de manera definitiva el registro del animal.
  - "Poner en venta" / "Cancelar venta": Alterna el estado comercial del ejemplar mediante un diálogo de confirmación.
  - "Marcar como vendido": Permite asentar la venta definitiva del animal y actualizar su estado a ausente.
  - "Publicar Animal": Interruptor al final del menú para activar o desactivar la URL web pública del ejemplar. Al activarlo, muestra una ventana con la dirección web asignada.

#### Cuadrícula de Módulos Funcionales
En el cuerpo de la pantalla se despliegan cuatro tarjetas principales en cuadrícula:
1. "Datos generales": Acceso a la información biológica detallada, genealogía (padre y madre), códigos de identificación secundaria (microchips, collares electrónicos, aretes oficiales) y documentos anexos.
2. "Producción": Acceso al histórico de pesajes, evolución de ganancia diaria de peso y controles de pesaje de leche.
3. "Datos veterinarios": Muestra la condición de salud actual del animal o la indicación "En secado" si se encuentra en periodo seco. Permite gestionar tratamientos médicos, vacunas y controles sanitarios. Si el animal está fallecido, al tocar esta tarjeta se despliega la ventana emergente con la causa de muerte, notas clínicas y fecha de defunción.
4. "Reproducción": Exhibe la condición reproductiva actual del ejemplar (y la etiqueta "Hembra receptora" si proviene de transferencia embrionaria). Al pulsar, conduce al historial reproductivo de servicios, inseminaciones, chequeos de preñez y partos (o a desarrollo juvenil si es un animal en crecimiento).

#### Botones de Acción Directa
- "Poner en venta": Botón visible debajo de las tarjetas funcionales si el animal no está en venta y no está bloqueado. Al tocarlo, abre el diálogo de confirmación para publicarlo comercialmente.
- "Cancelar muerte": Botón visible si el ejemplar tiene registrado un fallecimiento activo. Al presionarlo, elimina el evento de defunción y reactiva al ejemplar en el inventario de la finca.

- **Pantalla de llegada tras guardar o salir:**
  - Al presionar la flecha de regreso en la barra superior, retorna a la lista o pantalla de origen.
  - Si se elimina el ejemplar, el sistema notifica el éxito del proceso mediante el mensaje "Animal eliminado exitosamente" y redirige automáticamente a la pantalla anterior.

#### Variaciones por especie
- **Aplica para todas las especies:** La estructura general de la pantalla, la cabecera, el menú de acciones y las cuatro tarjetas principales operan de manera homogénea en bovinos, equinos, bufalinos, caprinos, ovinos y porcinos.
- **Etapas zootécnicas e iconos:** Las siluetas por defecto en la cabecera y en la tarjeta de reproducción se adaptan automáticamente a la especie y sexo del ejemplar (por ejemplo, vaca, toro, novilla, ternero en bovinos; yegua, potro, caballo en equinos; cerda, lechón, verraco en porcinos).
- **Indicador de secado:** El estado "En secado" se presenta únicamente si el animal cuenta con un tratamiento activo de secado registrado, aplicable a las especies de orientación lechera (bovinos, bufalinos, caprinos y ovinos).

#### Etiquetas de la interfaz en otros idiomas
| Español | Inglés | Portugués |
| :--- | :--- | :--- |
| "Datos generales" | "General data" | "Dados gerais" |
| "Datos veterinarios" | "Veterinary data" | "Dados veterinários" |
| "Reproducción" | "Reproduction" | "Reprodução" |
| "Compartir hoja de vida" | "Share resume" | "Compartilhar currículo" |
| "Editar datos" | "Edit data" | "Editar dados" |
| "Eliminar animal" | "Delete animal" | "Remover animal" |
| "Cancelar muerte" | "Cancel death" | "Cancelar morte" |
| "Cancelar venta" | "Cancel sale" | "Cancelar venda" |
| "Marcar como vendido" | "Mark as sold" | "Marcar como vendido" |
| "Publicar Animal" | "Publish Animal" | "Publicar animal" |
| "En línea" | "Online" | "Online" |
| "En venta" | "On sale" | "À venda" |
| "Vendido" | "Sold" | "Vendido" |
| "Ausente" | "Absentee" | "Ausente" |

### Matriz de Errores y Soluciones
| Mensaje en la App / Síntoma | Causa Real | Respuesta Sugerida por el Agente | Criterio de Escalamiento Humano |
| :--- | :--- | :--- | :--- |
| "No puedes acceder a este animal porque tu suscripción ha vencido. Te invitamos a renovar tu suscripción para que puedas acceder a todos tus animales." | La cuenta ha alcanzado o superado el límite de animales permitidos en su plan actual o la membresía expiró | "El acceso a este animal se encuentra inhabilitado porque su cuenta ha superado el cupo de animales de su plan actual o su membresía ha caducado. Para volver a consultar y gestionar el animal, ingrese a la sección de membresía de su cuenta y renueve o amplíe su suscripción." | Si el usuario cuenta con un pago vigente confirmado y la pantalla continúa bloqueada, transferir a soporte con comprobante de pago. |
| "Con tu perfil de %1$s, NO tienes permisos para realizar esta acción." | El colaborador no tiene asignado el permiso para editar, eliminar o cambiar el estado comercial del ejemplar en la finca | "Su perfil en esta finca no tiene permisos para realizar esta acción sobre el animal. Solicite al propietario o administrador de la finca que le habilite los permisos de edición o gestión de animales en la sección de colaboradores." | No escalar, depende de la configuración de roles por parte del dueño de la finca. |
| "Necesitas una conexión a internet para compartir la hoja de vida del animal." | Se intentó compilar o compartir la imagen gráfica de la hoja de vida sin conexión de datos o WiFi activa | "Para compilar y compartir la imagen de la hoja de vida del animal es indispensable contar con conexión a internet. Verifique que sus datos móviles o red WiFi estén activos e inténtelo de nuevo." | No escalar, limitación técnica por requerimiento de red para procesar y transferir la imagen. |
| Opciones de editar, eliminar o poner en venta deshabilitadas | El ejemplar se encuentra registrado como fallecido o vendido (bloqueo de seguridad) | "El animal se encuentra en estado bloqueado debido a que tiene un registro de muerte o venta registrado. Para volver a habilitar sus datos si hubo un error en la defunción, presione el botón 'Cancelar muerte' visible en la parte inferior o en el menú de tres puntos." | Si el animal aparece bloqueado sin tener defunción ni venta registrada, transferir a soporte técnico. |
| El enlace web del animal publicado muestra error en el navegador | Los cambios recientes de privacidad aún no se han sincronizado con el servidor web | "Al activar el animal como público, la información debe enviarse primero a la nube. Asegúrese de que su teléfono tenga conexión a internet y espere unos minutos a que se complete la sincronización automática antes de abrir el enlace." | Si tras confirmar que no hay datos pendientes por sincronizar el enlace sigue inaccesible, transferir a soporte técnico. |
| Pantalla de espera prolongada con el mensaje "Generando hoja de vida del animal..." | Proceso de sincronización previa o generación gráfica de la imagen bloqueado o con demora por conectividad | "Espere un momento mientras el sistema finaliza la sincronización y genera la imagen. Si la pantalla no avanza, cierre la aplicación por completo y vuelva a abrirla. Los datos de su animal guardados en el dispositivo no se perderán." | Si tras reabrir la app el proceso vuelve a quedar detenido de manera continua, transferir a soporte humano con correo de cuenta y modelo del teléfono. |

### Directivas de Seguridad y Guardrails
- Nunca pidas contraseñas, códigos SMS, códigos de verificación ni datos de pago completos por el chat.
- Verifica que el usuario esté en la finca correcta antes de sugerir eliminar o modificar registros del animal.
- No prometas funciones, plazos ni resultados que no estén documentados.
- No compartas información de otras fincas ni de otros usuarios.
- Aclare siempre al usuario que la opción "Eliminar animal" borra definitivamente el historial del ejemplar de la base de datos local y del servidor; si el animal murió o se vendió, recomiende utilizar el registro de fallecimiento o la opción "Marcar como vendido" en lugar de eliminarlo para conservar el historial zootécnico y financiero de la finca.
- Si el ganadero consulta sobre el enlace público del animal, recuérdele que la URL solo expone información general zootécnica orientada a la venta y nunca revelará datos sensibles de contacto ni ubicación privada sin su autorización.
