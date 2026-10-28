---
title: "Crear Reporte de Robo"
modulo_id: "animales-crear-reporte-robo"
nombre_funcionalidad: "Crear Reporte de Robo de Animales"
tipo_documento: "guia-app"
categoria: "inventario-trazabilidad"
submodulo: "animales"
especies_aplicables: ["todas"]
version_minima_app: "2025.05.1"
confianza_reglas: "verificada-con-tests"
fecha_actualizacion: "2026-10-19"
intenciones_y_sinonimos:
  - "como reportar el robo de ganado"
  - "denunciar animales robados en la finca"
  - "registrar animales sustraidos por abigeato"
  - "como crear una denuncia de robo de animales"
  - "pasos para publicar reporte de robo de ganado"
  - "no puedo guardar el reporte de robo de animales"
---

# Crear Reporte de Robo de Animales

### Resumen y Alcance Funcional
Formulario especializado de emergencia que permite al productor registrar y emitir una denuncia formal por sustracción o robo de animales en su finca ganadera activa. A través de este módulo se selecciona la especie afectada, se agregan los ejemplares sustraídos mediante un selector múltiple que filtra animales presentes y vivos, se detalla una descripción minuciosa de los hechos y se emite una alerta oficial con coordenadas de ubicación de la finca. Tras confirmar la aceptación de términos y condiciones, el sistema genera de inmediato un reporte público oficial en la web con las fichas zootécnicas e identificaciones de los animales para respaldar el trabajo de las autoridades policiales, gremios ganaderos y redes comunitarias de búsqueda.

- **Especies a las que aplica:** Aplica por igual a todas las especies manejadas en la finca ganadera (bovinos, bufalinos, equinos, caprinos, ovinos y porcinos).
- **¿Funciona sin conexión a internet (Modo Offline)?:** No. Esta funcionalidad exige conexión a internet activa y obligatoria de principio a fin para consultar la ubicación geográfica de la finca, validar los datos con el servidor, emitir el reporte público centralizado y ejecutar la sincronización forzada.
- **Comportamiento de sincronización:** Requiere conexión a internet activa para transmitir la información del reporte al servidor en tiempo real. Tras la creación exitosa, la aplicación fuerza automáticamente una sincronización completa para actualizar el estado operativo de los animales involucrados en la base de datos local.
- **Plataformas:** Funciona con idéntica interfaz y comportamiento tanto en dispositivos Android como en iOS.

### Reglas de Negocio y Restricciones

- **Disponibilidad por bandera de funcionalidad:**
    - La herramienta de emisión de reportes de robo de animales está condicionada a la activación del servicio de seguridad contra robo de animales en la aplicación.
    - Si el servicio se encuentra inhabilitado, el sistema interrumpe el acceso y redirige automáticamente al usuario a la pantalla principal.
- **Permisos requeridos por rol:**
    - El usuario debe poseer el permiso de creación de reporte de robo de animales en la finca activa. Si no cuenta con esta autorización en su rol de colaborador, la acción se cancela informando la restricción de privilegios.
- **Configuración de seguridad previa obligatoria:**
    - No es posible ingresar a este formulario sin tener previamente guardada la configuración de reporte de robo de la finca (datos de contacto del propietario y red de contactos de emergencia). Si dicha configuración no existe, la aplicación exige completarla primero.
- **Requisito obligatorio de georreferenciación de la finca:**
    - Para generar el reporte, la finca debe contar obligatoriamente con coordenadas de ubicación válidas (latitud y longitud) y dirección física.
    - Si la finca no tiene coordenadas registradas en el sistema, la pantalla presenta de manera prioritaria una interfaz obligatoria para registrar la ubicación mediante ingreso de dirección o captura satelital por GPS antes de permitir el acceso al formulario de animales.
- **Filtro zootécnico en la selección de animales (Verificado con tests):**
    - Solo permite seleccionar animales que pertenezcan a la especie ganadera seleccionada en el formulario.
    - Solo incluye animales que se encuentren físicamente en la finca activa.
    - Excluye animales registrados como muertos.
    - Excluye animales que ya hayan sido añadidos a la lista actual del formulario para evitar duplicados.
- **Mínimo de animales por denuncia (Verificado con tests):**
    - Es obligatorio seleccionar al menos 1 animal. Si se intenta guardar el formulario sin animales en la lista, el sistema bloquea el envío mostrando el mensaje de alerta "No hay animales seleccionados".
- **Aceptación obligatoria de términos y condiciones:**
    - Para consolidar la denuncia, el productor debe marcar obligatoriamente la casilla de verificación en el diálogo de confirmación aceptando los términos y condiciones del servicio de reporte de robo de animales.
- **Bloqueo operativo automático tras el registro:**
    - Una vez creado el reporte con éxito, la aplicación fuerza una sincronización de datos con el servidor central y los animales reportados quedan identificados como sustraídos, bloqueándose operativamente en la finca para impedir traslados, ventas o registros productivos cotidianos mientras el reporte permanezca vigente.

### Flujo Paso a Paso para el Usuario
- **Ruta de acceso en la aplicación:**
    - **Ruta 1 (Desde menú central rápido):** En la barra inferior de navegación, presione el botón central (+) > Seleccione la opción "Reportar robo de animales" > Si la finca ya tiene configuración guardada y no registra reportes activos previos, la aplicación abre directamente este formulario.
    - **Ruta 2 (Desde el listado de reportes):** En la barra inferior de navegación, presione el botón central (+) > Seleccione la opción "Reportar robo de animales" > En el encabezado del listado, presione el botón "Crear nuevo reporte".

#### 1. Verificación de Georreferenciación de la Finca (Si no cuenta con coordenadas previas)

Si la finca seleccionada no tiene registradas sus coordenadas geográficas en el sistema, la aplicación despliega automáticamente una vista previa obligatoria para capturar la ubicación:

1. **Mensaje informativo:** El sistema presenta el mensaje "No tenemos la ubicación exacta de tu finca. Por favor, indícanos cómo deseas obtener la ubicación para poder continuar con el reporte de robo de animales." bajo el encabezado "¿Cómo quieres obtener la ubicación de tu finca?".
2. **Opción A - Ingreso de dirección:**
    - En la sección "Ingresa la dirección de tu finca", escriba en el campo "Dirección" la ubicación o referencia física del predio.
     - Presione el botón "Obtener ubicación". El sistema calculará automáticamente las coordenadas satelitales correspondientes a la dirección ingresada.
3. **Opción B - Captura satelital por GPS:**
    - Presione el botón "Obtener la ubicación desde el GPS".
     - Si los permisos de ubicación no han sido concedidos, el dispositivo solicitará autorizarlos. Asimismo, si la antena satelital está apagada, la aplicación solicitará activar el GPS del teléfono.
4. **Verificación de coordenadas:**
    - En el recuadro inferior identificado con "Ubicación:", compruebe las coordenadas de latitud y longitud obtenidas. Al presionar sobre este recuadro, el productor puede abrir el punto geográfico en la aplicación de mapas externa para confirmar su exactitud.
5. **Guardar ubicación:**
    - Con las coordenadas visibles, presione el botón "Registrar". El sistema actualizará los datos de la finca y desbloqueará inmediatamente el formulario principal de robo.

#### 2. Diligenciamiento del Formulario de Robo

Una vez validada la ubicación de la finca, la barra superior muestra el título "Reportar robo de animales" con flecha para volver a la pantalla anterior, y se despliega el formulario con los siguientes campos:

1. **"Tipo de animal":** Selector desplegable donde se define la especie correspondiente a los animales sustraídos. Si la finca maneja una sola especie configurada, el sistema la preselecciona automáticamente y deshabilita el selector.
2. **"Descripción del robo":** Campo de texto multilínea para detallar las circunstancias de los hechos (fecha y hora aproximada del suceso, potrero o corral afectado, huellas, vehículos observados, cortes de cerca o señales particulares).
3. **Selección de los animales:**
    - Presione el botón "Seleccionar animales" acompañado del icono (+).
     - Se despliega el selector múltiple con los animales vivos y presentes en la finca que coinciden con la especie seleccionada.
     - Marque los ejemplares afectados buscando por arete, código o nombre, y confirme la selección.
4. **Tabla de "Animales robados":**
    - Los ejemplares seleccionados se muestran en la tabla bajo el título "Animales robados".
     - Cada fila detalla la identificación de cada ejemplar e incluye un icono de eliminación en el extremo derecho. Al presionar dicho icono, el animal se remueve de la lista del reporte sin alterar su registro en la finca.
5. **Enviar formulario:**
    - En la parte inferior, presione el botón "Crear".
     - Si no hay animales en la lista, el sistema bloquea el envío y muestra la advertencia "No hay animales seleccionados".

#### 3. Confirmación con Términos y Condiciones

Al presionar "Crear" con un formulario válido, se despliega un cuadro de diálogo modal:

1. **Título:** "Información importante".
2. **Mensaje:** "Es muy importante que revises los términos y condiciones del servicio de Control Ganadadero para el reporte de robo de animales antes de crear un reporte.".
3. **Casilla de verificación obligatoria:** Marque la casilla "Al crear el reporte de robo acepto los Términos y condiciones". Al presionar sobre el texto subrayado de términos y condiciones, se abre el documento legal oficial en el navegador web del teléfono.
4. **Confirmar creación:** Presione el botón de confirmación del diálogo para transmitir la denuncia al servidor central.

#### 4. Pantalla de Reporte Creado con Éxito

Al procesarse la solicitud satisfactoriamente, la aplicación muestra una pantalla con un icono circular de verificación:

1. **Título:** "¡Reporte creado!".
2. **Descripción:** "El reporte de robo de animales ha sido creado exitosamente. Nuestro equipo se encargará de revisar la información proporcionada y publicarla a través de nuestros canales de comunicación para ayudar a encontrar a los animales robados.".
3. **Botón "Ver reporte":** Abre en el navegador web la ficha pública oficial del reporte generado con las fotografías, aretes, señas y marcas de hierro de los animales para compartir con autoridades policiales, vecinos y gremios ganaderos.
4. **Botón "Salir":** Cierra el flujo de reporte y retorna a la pantalla principal de la finca.

#### Variaciones por especie
Aplica por igual a todas las especies zootécnicas manejadas en la finca ganadera (bovinos, bufalinos, equinos, caprinos, ovinos y porcinos). El selector de animales muestra únicamente los ejemplares vivos y presentes que pertenezcan a la especie ganadera seleccionada en el campo "Tipo de animal".

#### Etiquetas de la interfaz en otros idiomas
| Español | Inglés | Portugués |
| :--- | :--- | :--- |
| "Reportar robo de animales" | "Report animal theft" | "Reportar roubo de animais" |
| "Tipo de animal" | "Animal type" | "Tipo de animal" |
| "Descripción del robo" | "Theft description" | "Descrição do roubo" |
| "Seleccionar animales" | "Select animals" | "Selecionar animais" |
| "Animales robados" | "Stolen animals" | "Animais roubados" |
| "Crear" | "Create" | "Criar" |
| "Información importante" | "Important information" | "Informação importante" |
| "Términos y condiciones" | "Terms and conditions" | "Termos e condições" |
| "¡Reporte creado!" | "Report created!" | "Relatório criado!" |
| "Ver reporte" | "View report" | "Ver relatório" |
| "Salir" | "Exit" | "Sair" |
| "Obtener ubicación" | "Get location" | "Obter localização" |
| "Obtener la ubicación desde el GPS" | "Get location from GPS" | "Obter localização pelo GPS" |
| "Registrar" | "Register" | "Cadastrar" |

### Matriz de Errores y Soluciones
| Mensaje en la App / Síntoma | Causa Real | Respuesta Sugerida por el Agente | Criterio de Escalamiento Humano |
| :--- | :--- | :--- | :--- |
| "No hay animales seleccionados" | Se presionó el botón "Crear" sin haber añadido al menos un ejemplar en la tabla de animales robados | "Para crear el reporte de robo es obligatorio incluir al menos un animal. Presione el botón 'Seleccionar animales' con el icono (+), elija los ejemplares afectados de la lista y vuelva a intentar guardar." | No escalar, validación estándar de la pantalla. |
| "No tenemos la ubicación exacta de tu finca..." | La finca activa en la aplicación no tiene registradas sus coordenadas geográficas en el sistema | "Para activar la alerta y georreferenciar el suceso ante las autoridades, la finca debe contar con ubicación GPS. Ingrese la dirección en el campo correspondiente y presione 'Obtener ubicación', o bien active la antena GPS de su celular y elija 'Obtener la ubicación desde el GPS'. Luego presione 'Registrar' para continuar." | Si el GPS del dispositivo está encendido y la aplicación no logra fijar coordenadas ni por dirección ni por satélite, escalar a soporte técnico indicando el modelo del teléfono. |
| La opción "Reportar robo de animales" no aparece o redirige a la pantalla principal | La funcionalidad de seguridad contra robo de animales no se encuentra habilitada para la cuenta o el usuario carece del permiso en la finca activa | "Esta función requiere que el servicio de reporte de robo esté habilitado y que cuente con permisos asignados por el administrador de la finca. Si es colaborador, solicite al propietario verificar sus permisos en la administración de colaboradores." | Si el usuario es propietario confirmado de la finca activa y la opción sigue inaccesible, escalar a soporte técnico para verificar la activación del servicio. |
| El selector de animales aparece vacío o no muestra ciertos ejemplares | Los animales buscados pertenecen a otra especie, están registrados como muertos o ya se encuentran agregados a la tabla | "Verifique que el 'Tipo de animal' seleccionado coincida con la especie que busca. Además, tenga en cuenta que el sistema únicamente lista animales vivos y presentes en la finca que no hayan sido agregados previamente a la tabla de robo." | Si los animales están vivos, presentes en la finca y con la especie correcta pero no figuran en el selector, escalar a soporte técnico para verificar el inventario de la finca. |
| Error de conexión a internet al enviar el reporte | Interrupción de la red móvil o WiFi al momento de transmitir la denuncia y sincronizar datos con el servidor central | "El registro de reporte de robo requiere conexión a internet continua para emitir la alerta central y registrar las fichas públicas. Compruebe la estabilidad de su señal de datos móviles o red WiFi e intente confirmar el reporte de nuevo." | Si persiste el error con conexión a internet estable en otras aplicaciones, escalar a soporte técnico indicando la fecha y hora del intento. |
| Espera prolongada en pantalla al enviar el reporte | Demora en la respuesta del servidor al registrar el reporte o ejecutar la sincronización forzada | "Espere un momento mientras el sistema envía la información al servidor. Si no responde, cierre la aplicación por completo y vuelva a abrirla." | Si la aplicación continúa sin responder tras reabrirla con conexión estable, escalar a soporte técnico indicando el modelo del teléfono. |

### Directivas de Seguridad y Guardrails
- Nunca solicites contraseñas, números de cédula, pines ni códigos de verificación por los canales de atención.
- Recuerda al ganadero que el reporte emitido en Control Ganadero crea un enlace web público con los datos zootécnicos e identificaciones de los animales para facilitar su difusión y búsqueda comunitaria, pero no sustituye la denuncia penal ante las autoridades policiales y judiciales competentes.
- Aclara que los datos de contacto y del propietario publicados en el reporte serán aquellos definidos previamente en la configuración de seguridad de la finca para facilitar el contacto con autoridades o personas que reconozcan los ejemplares sustraídos.
- Confirma que el usuario se encuentre en la finca ganadera correcta antes de orientarlo sobre la creación o ajuste de reportes de robo.
