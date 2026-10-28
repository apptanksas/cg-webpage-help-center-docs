---
title: "Crear o Editar Finca"
modulo_id: "farm-crear-editar"
nombre_funcionalidad: "Creación y Modificación de Fincas Ganaderas"
categoria: "cuentas-usuarios"
submodulo: "fincas"
version_minima_app: "2026.10.1"
fecha_actualizacion: "2026-10-09"
intenciones_y_sinonimos:
  - "como crear una finca nueva en la app"
  - "como registrar mi predio ganadero desde cero"
  - "como editar los datos o el nombre de mi finca"
  - "como cambiar el area ganadera o la ubicacion de la finca"
  - "error al obtener la ubicacion gps de la finca"
  - "el area ganadera no puede ser mayor al area total"
  - "debes seleccionar al menos un tipo de animal"
---

# Creación y Modificación de Fincas Ganaderas

### Resumen y Alcance Funcional
Asistente interactivo por pasos diseñado para cumplir dos propósitos esenciales en la gestión ganadera: registrar una nueva explotación pecuaria desde cero o modificar la configuración integral de una finca existente. 

En el flujo de **creación desde cero**, el productor define la identidad de su predio (nombre, propósito productivo, fotografía y unidades de medida), delimita sus superficies (área total y área efectiva dedicada a la ganadería), establece la ubicación geográfica mediante coordenadas satelitales GPS o división administrativa, y habilita las especies animales gestionadas con sus parámetros reproductivos iniciales. Al finalizar, la explotación se guarda en el servidor central, se activa automáticamente como la finca de trabajo principal y redirige al panel de inicio.

En el flujo de **modificación o edición**, el asistente precarga toda la información actual de la finca activa, permitiendo al usuario corregir nombres, actualizar superficies, reclasificar el propósito productivo, ajustar coordenadas de georreferenciación o incorporar nuevas especies pecuarias a su plan de manejo. Al confirmar los cambios, los datos se sincronizan con el servidor y la aplicación regresa a la ficha informativa del predio.

- **¿Funciona sin conexión a internet (Modo Offline)?:** No.
- **Comportamiento de sincronización:** Requiere conexión activa a internet (datos móviles o red Wi-Fi) tanto para la creación como para la edición. Las operaciones validan los datos en tiempo real en los servidores, suben las fotografías, consultan los catálogos territoriales y resuelven las coordenadas satelitales mediante georreferenciación inversa.

### Reglas de Negocio y Restricciones
- **Permisos y roles requeridos en la plataforma:**
    - *Para crear una finca nueva:* Se requiere el permiso de creación de fincas asociado a la cuenta de usuario.
    - *Para editar una finca existente:* Se requiere el permiso de actualización de fincas (otorgado exclusivamente al propietario del predio y a administradores autorizados).
    - Los colaboradores con roles de empleado o visitante no disponen del botón de edición ni tienen autorización para modificar la ficha técnica de la propiedad.
- **Diferenciación entre el Modo Creación y el Modo Edición:**
    - *Título en cabecera:* El asistente muestra el título *"Creando finca"* durante el alta de un nuevo predio, o *"Editando finca"* cuando se ingresa a modificar una existente.
    - *Acción de salida rápida:* En la esquina superior derecha, el botón muestra el texto **OMITIR** al crear (permite salir sin registrar la finca), mientras que en modo edición muestra el texto **SALIR** (permite cancelar las modificaciones y regresar a la pantalla de información de la finca sin alterar los datos).
    - *Carga de datos:* En creación, el formulario inicia con campos limpios y valores estándar; en edición, se precargan todos los registros almacenados (fotografía, áreas, listas geográficas y parámetros de cada especie pecuaria activa).
- **Reglas del Paso 1 (Datos Básicos y Parámetros Productivos):**
    - **Nombre de la finca:** Campo obligatorio en ambos modos. Debe contener un mínimo de tres caracteres.
    - **Propósito productivo:** Selección obligatoria entre los esquemas zootécnicos del sistema: *Doble propósito*, *Producción de carne*, *Producción de leche*, *Cría*, *Levante* o *Bravura*.
    - **Área total y área ganadera:** Ambos campos exigen valores numéricos enteros válidos.
    - **Restricción estricta de áreas:** El área dedicada a la ganadería no puede superar numéricamente el área total del predio. Si el usuario ingresa un área ganadera mayor a la total, el sistema bloqueará el paso mostrando la advertencia de inconsistencia.
    - **Unidades de medida:** Es obligatorio definir las unidades base de trabajo: superficie (hectáreas, metros cuadrados, entre otras), volumen de leche (litros o galones) y peso animal (kilogramos o libras).
    - **Fotografía de la finca:** Campo opcional. Permite cargar una imagen representativa desde la cámara o galería del dispositivo.
- **Reglas del Paso 2 (Ubicación Geográfica y Territorial):**
    - **Selección territorial:** Es obligatorio definir país, región/departamento y municipio/ciudad. Los selectores son secuenciales y dependientes.
    - **Georreferenciación satelital (GPS):** Permite capturar la ubicación exacta mediante el sensor satelital del teléfono. Requiere permisos de localización activos en el dispositivo y conexión a internet para resolver la dirección y demarcación administrativa.
    - **Dirección física:** Campo opcional para registrar indicaciones, veredas o caminos rurales de acceso.
- **Reglas del Paso 3 (Configuración de Especies Pecuarias):**
    - **Selección mínima obligatoria:** La finca debe mantener al menos una especie pecuaria seleccionada: *Bovinos*, *Equinos*, *Bufalinos*, *Caprinos*, *Ovinos* o *Porcinos*. Si se desmarcan todas, el sistema no permitirá continuar y emitirá la alerta: *"Debes seleccionar al menos un tipo de animal"*.
    - **Parámetros zootécnicos por especie:** Cada especie seleccionada permite configurar el tiempo de destete (en días), la unidad de edad (días, meses o años) y, en especies ordeñables (*Bovinos*, *Bufalinos*, *Caprinos* y *Ovinos*), el tiempo de secado previo al parto (en días).
    - **Botón de acción inferior:** En modo creación, el botón inferior muestra el texto **SIGUIENTE** para avanzar al paso final. En modo edición, el botón cambia su etiqueta a **GUARDAR** para procesar directamente la actualización.
- **Reglas del Paso 4 (Procesamiento y Confirmación):**
    - En modo creación, tras avanzar del paso 3 se despliega la pantalla de finalización (*"Creando finca"*), guarda la explotación en el servidor y redirige al usuario al panel de inicio principal.
    - En modo edición, al presionar **GUARDAR** en el paso 3, la pantalla de finalización muestra *"Editando finca"*, procesa los cambios y redirige al usuario de vuelta a la ficha informativa del predio.
    - Si ocurre un fallo en el servidor o corte de red, el sistema muestra el mensaje de error y regresa automáticamente al paso anterior preservando la información ingresada.

### Flujo Paso a Paso para el Usuario
- **Ruta de acceso en la aplicación:**
    - *Ruta para Crear Finca (Primer registro al acceder sin fincas):* Inicio de sesión o registro de cuenta nueva > Pantalla de bienvenida > Presionar el botón **Crear mi finca**.
    - *Ruta para Crear Finca (Desde el menú lateral principal):* Menú lateral desplegable > Tocar la lista desplegable de fincas en la parte superior del menú > Seleccionar la opción para registrar una nueva finca.
    - *Ruta para Crear Finca (Desde el selector de fincas):* Menú lateral desplegable > Selección de fincas > Presionar el botón para añadir una finca.
    - *Ruta para Modificar / Editar Finca (Desde el panel de inicio):* Pantalla de inicio de la finca (**Inicio**) > Tocar la tarjeta superior con el nombre e información de la finca > En la pantalla de detalle (**Finca**), presionar el botón de editar con ícono de lápiz en la esquina superior derecha.

#### 1. Paso 1: Información Básica y Parámetros Productivos
- **Fotografía representativa:** Toque el círculo superior con ícono de cámara o imagen para capturar una foto del predio o elegir una desde la galería. En modo edición, se muestra la fotografía previamente asignada.
- **Nombre de la finca:** Ingrese o modifique el nombre del predio ganadero (mínimo 3 caracteres).
- **Propósito de la finca:** Despliegue el menú y seleccione la orientación zootécnica de la explotación pecuaria.
- **Áreas del terreno:**
    - *Área total:* Digite la extensión completa del terreno en números enteros.
    - *Área de ganado:* Digite el área destinada a pastos y labores con animales. Asegúrese de que este valor sea menor o igual al área total.
- **Unidades de medida:** Seleccione en los menús desplegables las unidades de trabajo:
    - *Área:* Hectáreas, metros cuadrados, entre otras.
    - *Leche:* Litros o galones.
    - *Peso:* Kilogramos o libras.
- Presione el botón **Siguiente** en la barra inferior para continuar.

#### 2. Paso 2: Ubicación Geográfica y División Territorial
- **Ubicación satelital automática:** Presione el botón con ícono de mapa/satélite. La aplicación consultará las coordenadas GPS del dispositivo y rellenará de manera automática el país, la región/departamento y el municipio/ciudad, además de la dirección estimada.
- **Configuración territorial manual:** Si no dispone de cobertura satelital o prefiere definir la localidad manualmente:
    - Seleccione su **País** en el primer selector.
    - Seleccione la **Región** o departamento correspondiente.
    - Seleccione la **Ciudad** o municipio en el tercer selector.
- **Dirección física:** Ingrese opcionalmente el nombre de la vereda, sector rural o indicaciones de acceso.
- Presione el botón **Siguiente** para avanzar (o **Atrás** si necesita corregir algún dato del primer paso).

#### 3. Paso 3: Configuración de Especies Pecuarias
- La pantalla presenta las tarjetas de las especies de animales disponibles (*Bovinos*, *Equinos*, *Bufalinos*, *Caprinos*, *Ovinos*, *Porcinos*).
- **En modo creación:** Toque sobre las especies que maneja en su finca para activarlas.
- **En modo edición:** Las especies previamente activadas se muestran seleccionadas; puede modificar sus parámetros o habilitar nuevas especies según la evolución de su explotación.
- **Parámetros zootécnicos desplegables:** Al seleccionar una especie, se despliegan sus campos específicos:
    - Verifique y ajuste el tiempo de destete estimado (en días).
    - En especies ordeñables (*Bovinos*, *Bufalinos*, *Caprinos*, *Ovinos*), revise o ajuste el tiempo de secado previo al parto (en días).
    - Seleccione la unidad temporal para visualizar la edad de los animales (días, meses o años).
- Al menos una especie debe quedar con su casilla de verificación marcada.
- **Guardado y avance:**
    - *Si está creando una finca nueva:* Presione el botón **Siguiente** en la barra inferior para ir a la confirmación final.
    - *Si está editando una finca existente:* El botón inferior muestra **Guardar**. Presiónelo para registrar los cambios y pasar al procesamiento.

#### 4. Paso 4: Finalización y Confirmación
- La pantalla presenta un indicador de procesamiento junto al nombre del predio y la imagen asignada:
    - Si es una nueva finca, se muestra el título *"Creando finca"*.
    - Si es una modificación, se muestra el título *"Editando finca"*.
- El sistema procesa y resguarda los datos en los servidores centrales de Control Ganadero.
- **Pantalla de llegada tras procesar:**
    - *Al culminar una creación:* La aplicación establece el predio como la finca activa y redirige directamente a la pantalla de inicio principal (**Inicio**).
    - *Al culminar una edición:* La aplicación guarda las actualizaciones y retorna automáticamente a la pantalla de información de la finca (**Finca**) reflejando los nuevos datos.

### Matriz de Errores y Soluciones
| Mensaje en la App / Síntoma | Causa Real | Respuesta Sugerida por el Agente | Criterio de Escalamiento Humano |
| :--- | :--- | :--- | :--- |
| "El nombre de la finca debe tener al menos 3 caracteres." | El nombre del predio está vacío o no alcanza la longitud mínima de 3 letras | "El nombre de la finca es obligatorio y debe tener al menos 3 caracteres. Por favor escriba un nombre válido para su predio antes de continuar." | No requiere escalamiento; validación directa de formulario. |
| "El área para ganadería no puede ser superior al área total de la finca" / "El área de ganado no puede ser mayor que el área total de la finca" | El valor numérico del área ganadera sobrepasa la superficie total de la finca | "El área dedicada a la ganadería no puede superar el área total del predio. Por favor ajuste las cifras para que el área de ganado sea igual o menor al área total." | No requiere escalamiento; regla de consistencia territorial. |
| "Debes seleccionar al menos un tipo de animal" | Se intentó guardar o avanzar en el paso 3 sin tener marcada ninguna especie animal | "Es obligatorio tener seleccionada al menos una especie pecuaria (bovinos, equinos, etc.) para su finca. Marque la casilla de los animales que maneja en su predio para continuar." | No requiere escalamiento; regla obligatoria de configuración. |
| "Parece que tienes problemas con tu conexión a internet. Por favor, verifica tu conexión e intenta de nuevo." | Ausencia de conexión de datos móviles o Wi-Fi al momento de guardar, actualizar o capturar la ubicación GPS | "La creación y modificación de fincas requiere conexión activa a internet. Por favor verifique su conexión e intente presionar el botón de nuevo." | Si el usuario dispone de conexión estable comprobada y el error persiste de forma continua, derivar a soporte técnico. |
| El botón de ubicación satelital no completa los campos territoriales | Señal de satélite insuficiente, permisos de localización no otorgados o retraso del servicio de georreferenciación | "Si su teléfono no captura las coordenadas satelitales en este momento, puede desplegar manualmente las listas de país, región y ciudad para indicar la ubicación de su finca." | No requiere escalamiento; la aplicación permite la selección manual inmediata. |
| "Algo salio mal al realizar la operación, por favor intentalo de nuevo." | Falla temporal de comunicación con el servidor al registrar los metadatos o la fotografía de la finca | "Se presentó una interrupción momentánea al procesar la información en el servidor. Por favor verifique su conexión y pulse nuevamente el botón; sus datos diligenciados no se han perdido." | Si tras reintentar varias veces el guardado sigue fallando, solicitar captura de pantalla y transferir al equipo técnico. |

### Directivas de Seguridad y Guardrails
- Recuerde al usuario que los datos territoriales y de superficie de su finca se encuentran resguardados bajo su cuenta personal y solo son visibles para los colaboradores que él invite formalmente.
- No solicite contraseñas, documentos de tenencia de tierras ni credenciales privadas por los canales de chat al asistir en la creación o edición de predios.
- Si un usuario no encuentra la opción de editar en la pantalla de su finca, infórmele con cordialidad que dicha función está reservada al propietario o administradores autorizados; los perfiles de trabajador o colaborador no tienen habilitado el botón de modificación.
