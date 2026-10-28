---
title: "Configuración de Reporte de Robo"
modulo_id: "animales-configuracion-reporte-robo"
nombre_funcionalidad: "Configuración de Reporte de Robo de Animales"
categoria: "inventario-trazabilidad"
submodulo: "animales"
version_minima_app: "2026.10.1"
fecha_actualizacion: "2026-10-06"
intenciones_y_sinonimos:
  - "como configurar el reporte de robo de ganado"
  - "datos del propietario para denuncia de abigeato"
  - "como agregar contactos de emergencia para robo de animales"
  - "cambiar telefono o cedula en reporte de robo"
  - "verificar telefono del propietario para reporte de robo"
  - "limite de contactos en denuncia de robo de ganado"
---

# Configuración de Reporte de Robo de Animales

### Resumen y Alcance Funcional
Módulo de seguridad preventiva y configuración previa obligatoria que establece la identidad del propietario de los animales y la red de contactos de emergencia de la finca para la gestión de incidentes de abigeato o robo de ganado. A través de este formulario se registran y validan el nombre completo del titular, su documento de identidad y su número de teléfono verificado (mediante código de confirmación), junto con un listado de hasta 5 contactos clave de auxilio (como policía local, vecinos colindantes, familiares o gremios ganaderos). Estos datos son los que se publican de forma oficial en la ficha web del reporte y a los que se remiten las notificaciones inmediatas por mensajería en caso de registrarse una sustracción de animales en el predio.

- **¿Funciona sin conexión a internet (Modo Offline)?:** No.
- **Comportamiento de sincronización:** Requiere conexión a internet activa y obligatoria en todo momento. La carga de la configuración existente, la validación del número telefónico del propietario contra la pasarela de autenticación y el guardado o actualización de los datos del propietario y sus contactos de emergencia se realizan en tiempo real contra los servidores centrales de Control Ganadero.

### Reglas de Negocio y Restricciones
- **Disponibilidad por bandera de funcionalidad:** La herramienta está sujeta a la activación del servicio de seguridad contra robo de animales en Control Ganadero. Si el servicio se encuentra inhabilitado globalmente o en la suscripción, la aplicación redirige de inmediato a la pantalla principal.
- **Conectividad a internet obligatoria:** La pantalla no permite operar de manera local ni sin conexión activa a datos móviles o red WiFi. Cualquier intento de apertura o guardado sin internet bloquea el proceso informando el error de comunicación.
- **Finca activa seleccionada:** La configuración queda estrictamente asociada al identificador de la finca activa en el momento de completar el registro.
- **Campos del propietario obligatorios:**
    - **Nombre:** Obligatorio. Se precarga de forma automática con el nombre y apellidos registrados en la cuenta del usuario, admitiendo ajustes respetando el formato de nombres válidos.
    - **Número de identificación:** Obligatorio. Documento de identidad nacional, cédula de ciudadanía o registro fiscal del propietario del ganado.
    - **Indicativo de país:** Selector obligatorio según el catálogo oficial de países disponibles. Se preselecciona con el país registrado en la cuenta del usuario.
    - **Número de teléfono:** Obligatorio. Formato de número telefónico móvil local.
- **Verificación obligatoria del teléfono del propietario:**
    - Si el número móvil ingresado coincide con el teléfono validado en la cuenta de usuario o con el registrado previamente en la configuración guardada, se considera verificado de inmediato y muestra un icono de confirmación.
    - Si el número no ha sido verificado o si el usuario cambia el número en el formulario, el sistema marca el teléfono con un icono de advertencia. Al presionar dicho icono o al pulsar el botón para continuar y guardar el formulario, la aplicación abre obligatoriamente un diálogo emergente de verificación telefónica por código SMS.
    - No es posible finalizar ni crear la configuración sin que el teléfono del titular esté debidamente verificado.
- **Gestión de la red de contactos de emergencia:**
    - **Límite máximo de contactos:** Se pueden agregar hasta un máximo de 5 contactos de auxilio. Al alcanzar los 5 contactos registrados, el botón para agregar se deshabilita automáticamente.
    - **Control de duplicidad:** El sistema no permite agregar dos veces el mismo número telefónico completo (indicativo más teléfono móvil). Si se intenta registrar un número existente, se ignora la adición.
    - **Requisitos por contacto:** Cada contacto requiere obligatoriamente su nombre, indicativo de país y número telefónico móvil local válido.
    - **Eliminación individual:** Los contactos añadidos pueden ser removidos en cualquier momento presionando el icono de eliminación ubicado al lado de su número en la lista.
- **Detección de configuración existente (Alerta de revisión):**
    - Si la finca ya cuenta con una configuración guardada previamente, al ingresar la aplicación despliega un cuadro de diálogo informativo notificando que ya existe una configuración definida.
    - El ganadero puede optar por presionar el botón para continuar hacia los reportes (o creación de denuncia si no tiene reportes activos) o presionar el botón para revisar la configuración, el cual cierra el diálogo y permite inspeccionar y editar los campos del formulario.
- **Guardado y actualización:**
    - Si no existía configuración previa, el sistema crea un nuevo registro vinculado a la finca.
    - Si ya existía, el sistema actualiza la configuración existente conservando su identificador original.
    - Tras guardar con éxito: si la finca tiene reportes de robo activos, el sistema navega a la lista de reportes; si no tiene reportes activos, avanza directamente al formulario para crear un nuevo reporte de robo.

### Flujo Paso a Paso para el Usuario
- **Ruta de acceso en la aplicación:**
    - **Ruta 1 (Acceso inicial desde menú rápido):** En la barra inferior de navegación, presione el botón central (+) > Seleccione la opción **Reportar robo de animales** > Si la finca nunca ha configurado el servicio, el sistema abrirá directamente esta pantalla.
    - **Ruta 2 (Revisión de configuración existente):** En la barra inferior de navegación, presione el botón central (+) > Seleccione la opción **Reportar robo de animales** > En el cuadro de diálogo emergente que indica que ya existe una configuración definida, presione **Revisar configuración**.

#### Detección de Configuración Previa (Cuadro de Diálogo Emergente)

Si la finca ya tiene datos registrados, al entrar aparece un diálogo con:

- **Título:** **Atención**
- **Mensaje:** "Ya tienes un configuración definida para reportar robo de ganado."
- **Botón "Continuar":** Omite la edición y redirige a la lista de reportes de robo (si hay activos) o a la creación de un nuevo reporte.
- **Botón "Revisar configuración":** Cierra el mensaje emergente y da paso al formulario completo para modificar o actualizar los datos del propietario o los contactos.

#### Diligenciamiento de la Sección Información del Propietario

En la parte superior del formulario se ubica el bloque **Información del propietario**, acompañado de una explicación sobre la importancia de estos datos para las autoridades y la publicación oficial:

1. **Nombre:** Campo de texto donde figura el nombre del propietario. Puede modificarse si el titular del ganado difiere del usuario administrador.
2. **Número de identificación:** Campo para ingresar el documento de identidad oficial, cédula o registro tributario del propietario.
3. **Indicativo de país y Número de teléfono:**
    - En el selector de la izquierda, verifique o elija el indicativo internacional de su país.
     - En el campo de la derecha, ingrese el número móvil local.
     - **Validación del número:** Si el teléfono está verificado, se visualizará un icono de verificación en color de éxito. Si requiere confirmación, se exhibe un icono de advertencia; al pulsarlo, se desplegará el diálogo emergente para validar el teléfono mediante código.

#### Diligenciamiento de la Sección Contactos a Reportar

En el segundo bloque de la pantalla se gestionan las personas y entidades de emergencia que recibirán la alerta directa en caso de robo:

1. **Tarjetas de referencia y ejemplos:** La pantalla presenta tarjetas orientativas con ejemplos de contactos clave para la red de apoyo:
    - **Policía:** Reporte Oficial.
     - **Vecinos:** Alerta Cercana.
     - **Familia:** Soporte Personal.
2. **Listado de contactos registrados:**
    - Si ya se han agregado contactos, se muestran bajo el título **Contactos registrados**.
     - Cada contacto muestra su nombre, su número telefónico formateado y un botón circular con icono de eliminación. Al presionar dicho icono, el contacto se elimina inmediatamente de la lista.
3. **Agregar un nuevo contacto:**
    - En el campo **Nombre**, escriba el nombre o entidad del contacto (por ejemplo: "Comando de Policía Rural" o "Vecino Potrero Norte").
     - Seleccione el indicativo de país y escriba el número en el campo **Número de teléfono móvil**.
     - Presione el botón **Agregar**. El botón solo se habilitará si el nombre y el teléfono son válidos y si la lista contiene menos de 5 contactos.
     - Al tocarlo, el contacto se añade al listado superior y los campos de captura se limpian para permitir un nuevo ingreso.

#### Guardado y Continuación
1. Una vez completada la información del propietario y registrados los contactos necesarios, presione el botón **Continuar**.
2. Si el número de teléfono del propietario no estaba verificado, la aplicación abrirá automáticamente el diálogo emergente para completar la validación telefónica antes de transmitir los datos.
3. Al procesar el guardado con éxito:
    - Si la finca posee reportes de robo vigentes, la aplicación avanza al listado de reportes activos.
     - Si no existen reportes activos, la aplicación avanza de inmediato al formulario de registro de animales robados.

**Pantalla de llegada tras guardar:** Lista de reportes de robo de animales (si existen denuncias activas) o el formulario de creación de reporte de robo.

### Matriz de Errores y Soluciones
| Mensaje en la App / Síntoma | Causa Real | Respuesta Sugerida por el Agente | Criterio de Escalamiento Humano |
| :--- | :--- | :--- | :--- |
| "Cargando configuración..." persistente o error de red al abrir | Sin conexión a datos móviles o WiFi, o falla en la comunicación con el servidor central | "La configuración del reporte de robo requiere conexión a internet para consultar los datos de la finca. Por favor, asegúrese de contar con señal estable de datos o WiFi e intente abrir la opción nuevamente." | Si el usuario cuenta con navegación fluida en otras aplicaciones pero el error persiste, transferir a soporte técnico. |
| El botón "Agregar" contacto permanece deshabilitado | El nombre o el número de teléfono del contacto están incompletos, contienen caracteres inválidos o ya se alcanzó el límite de 5 contactos | "Verifique que haya ingresado tanto el nombre como el número móvil del contacto. Tenga presente que el sistema admite hasta un máximo de 5 contactos de emergencia. Si ya tiene 5 y desea registrar uno nuevo, debe eliminar uno de los existentes presionando el icono con el símbolo de menos (-)." | No escalar, validación operativa estándar de la pantalla. |
| Aparece un icono de advertencia junto al teléfono del propietario | El número de teléfono ingresado no ha sido verificado mediante el código de confirmación del sistema | "Para garantizar que las alertas y autoridades puedan comunicarse con el propietario, el número debe estar confirmado. Toque el icono de advertencia al lado del teléfono o presione 'Continuar' para recibir y escribir el código de confirmación SMS en el diálogo emergente." | Si el mensaje con el código SMS de verificación no llega tras varios reintentos en un lapso de 5 minutos, escalar a soporte técnico para verificar el proveedor de mensajería. |
| El contacto no se agrega tras presionar el botón "Agregar" | El número telefónico ingresado ya está registrado en la lista de contactos de esta configuración | "Ese número de teléfono ya se encuentra agregado en el listado de contactos registrados. No es posible duplicar números de emergencia dentro de la misma finca." | No escalar, comportamiento esperado del sistema para evitar envíos duplicados de alertas. |
| Círculo de espera infinito / Pantalla congelada en cargando | Proceso en segundo plano bloqueado o timeout en el dispositivo al guardar la configuración | "Espere 30 segundos. Si no avanza, cierre la aplicación por completo desde el administrador de tareas de su teléfono (deslizando hacia arriba) y vuelva a abrirla. Sus datos locales no se perderán." | Si tras reabrir la app el botón sigue deshabilitado o la pantalla vuelve a congelarse, transferir de inmediato a soporte humano con correo y modelo del teléfono. |

### Directivas de Seguridad y Guardrails
- NUNCA solicite contraseñas de acceso a la cuenta ni códigos de verificación SMS enviados al teléfono del ganadero para asistir en la configuración.
- Recuerde al usuario que los datos del propietario registrados en este módulo serán visibles públicamente en la ficha web oficial de la denuncia para permitir que las autoridades y miembros de la comunidad que reconozcan el ganado puedan contactar al dueño.
- Aclare que los números agregados en la lista de contactos de emergencia recibirán notificaciones de alerta directa sobre los sucesos de abigeato reportados en la finca.
