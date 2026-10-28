---
title: "Registrar Animal"
modulo_id: "animal-create"
nombre_funcionalidad: "Registro Individual de Animales"
tipo_documento: "guia-app"
categoria: "inventario-trazabilidad"
submodulo: "animales"
especies_aplicables: ["todas"]
version_minima_app: "2025.05.1"
confianza_reglas: "verificada-con-tests"
fecha_actualizacion: "2026-10-16"
intenciones_y_sinonimos:
  - "como registrar un animal nuevo en la finca"
  - "donde ingreso un ternero vaca o toro"
  - "como conectar el chip o escanear qr del animal"
  - "error el codigo del animal ya existe"
  - "como registrar cruces de razas o porcentaje"
  - "como asignar padre y madre a una cria"
  - "no tengo permisos para crear animales"
  - "tu cuenta excede la cantidad maxima de animales permitidos"
---

# Registro Individual de Animales

### Resumen y Alcance Funcional
Pantalla de captura y registro zootécnico que permite dar de alta a un nuevo ejemplar en el inventario ganadero de la finca de manera individual, o actualizar los datos básicos de un animal existente. Reúne la selección fotográfica de portada, clasificación por sexo y especie, asignación de código principal de arete, captura de identificadores electrónicos mediante lectores externos o sensores del teléfono (microchip inyectable por bastón Bluetooth, arete de proximidad por sensor NFC y código QR o de barras por cámara), características zootécnicas, composición de razas o cruces porcentuales, registro de pesajes históricos (nacimiento, destete y al año), genealogía parental (padre y madre reproductores), ubicación en lote, titularidad y notas de campo.

- **Especies a las que aplica:** Aplica para todas las especies configuradas en la finca (bovinos, equinos, bufalinos, caprinos, ovinos y porcinos). Si la finca cuenta con una sola especie configurada, el selector de especie se preselecciona automáticamente.
- **¿Funciona sin conexión a internet (Modo Offline)?:** Sí. Todo el formulario, la validación de unicidad local de códigos, la captura por Bluetooth, NFC y cámara funcionan sin conexión.
- **Comportamiento de sincronización:** Los datos del ejemplar se guardan de inmediato en la base de datos local del teléfono y se sincronizan en segundo plano con el servidor cuando el dispositivo dispone de conexión a internet. La fotografía adjunta se almacena localmente y se transfiere al servidor en el proceso de sincronización multimedia.

### Reglas de Negocio y Restricciones
- **Permisos requeridos por rol en la finca:**
    - **Creación de animal:** Para registrar un nuevo ejemplar se requiere el permiso de creación de animales en la finca activa. Si el usuario carece de esta autorización, el sistema bloquea el guardado mostrando el mensaje: "Con tu perfil de [rol], NO tienes permisos para realizar esta acción." (por ejemplo: *"Con tu perfil de Vaquero, NO tienes permisos..."*).
    - **Edición de animal:** Al ingresar en modo edición desde la ficha técnica o el resumen del animal, se requiere el permiso de actualización de animales.
- **Capacidad y límites de la membresía (Límite de animales alcanzado):**
    - El registro de nuevos ejemplares está sujeto al límite máximo de animales contratado en el plan de la finca. Si la cuenta alcanza o supera esta capacidad, el sistema detiene el proceso y muestra: "Tu cuenta excede la cantidad máxima de animales permitidos...".
- **Unicidad obligatoria de identificadores:**
    - **Código de arete:** Es de carácter obligatorio. No puede existir otro animal en la misma finca con el mismo código. Si se ingresa uno duplicado, la aplicación alerta: "El código del animal [código] ya existe" (por ejemplo: *"El código del animal 104 ya existe"*).
    - **Código de chip (Microchip):** Se captura en modo de solo lectura desde el lector Bluetooth. Si el código ya pertenece a otro ejemplar en el sistema, la app muestra: "El código de chip [número de chip] ya existe en otro animal".
    - **Código Tag NFC:** Se captura mediante el sensor NFC del teléfono. Si el código ya está en uso por otro animal, el sistema alerta: "El código de tag NFC [código NFC] ya existe en otro animal".
    - **Código QR / Barras:** Se escanea con la cámara del dispositivo. Si el identificador ya está asignado a otro animal, la app muestra: "El código QR o de barras [código] ya existe en otro animal".
- **Validaciones zootécnicas y de calendario:**
    - **Fecha de nacimiento:** Solo admite fechas pasadas o el día actual (no permite seleccionar fechas futuras). Al seleccionar o modificar la fecha de nacimiento, el sistema calcula y actualiza automáticamente la etapa productiva del ejemplar según su especie y sexo.
    - **Peso destete:** Se habilita exclusivamente si la etapa del animal calculada a partir de su edad y especie corresponde a destete o a una etapa superior.
    - **Peso año:** Se habilita exclusivamente si la edad calculada a partir de la fecha de nacimiento es igual o superior a 12 meses (1 año).
    - **Unidad de pesaje:** Los campos de peso muestran la unidad de medida oficial configurada para la finca (kg o lb).
- **Genealogía y filtros de reproductores:**
    - **Padre:** El selector filtra exclusivamente machos adultos o reproductores de la misma especie registrados en la finca, excluyendo al propio animal si se encuentra en edición.
    - **Madre:** El selector filtra exclusivamente hembras adultas o reproductoras de la misma especie registradas en la finca, excluyendo al propio animal si se encuentra en edición.

### Flujo Paso a Paso para el Usuario
- **Ruta de acceso en la aplicación:**
    - **Ruta 1 (Desde la pantalla principal):** En la barra superior o sección de acciones rápidas presione el botón "+" o "Crear animal".
    - **Ruta 2 (Desde el menú contextual inferior):** Toque el botón central flotante (+) > Seleccione "Crear animal".
    - **Ruta 3 (Desde el listado de animales):** En la barra de navegación inferior presione "Animales" > Toque el botón de opciones (tres puntos) en la esquina superior derecha > Seleccione "Crear animal".
    - **Ruta 4 (Desde la ficha técnica para edición):** En la barra inferior toque "Animales" > Seleccione un animal > Presione "Datos generales" > Toque el botón flotante con icono de lápiz sobre la foto de portada.
    - **Ruta 5 (Desde el resumen del animal para edición):** En la barra inferior toque "Animales" > Seleccione un animal > Toque el botón de edición rápida (icono de lápiz) en el encabezado.
    - **Ruta 6 (Desde partos y nacimientos):** Al registrar un parto múltiple o nacimiento con cría en las pantallas reproductivas, la aplicación permite enlazar directamente al formulario de creación precargando el tipo de animal, sexo, fecha de nacimiento y madre.

#### 1. Barra Superior y Lectura Rápida de Identificadores

En la barra superior encontrará el título dinámico ("Crear animal" o "Editar animal"), la flecha de regreso y tres accesos de captura automática:

1. **Escáner QR / Código de barras (icono de escáner):** Toque el icono para abrir la cámara del teléfono. Al enfocar el código de barras o QR impreso en el arete, el valor se captura y se asigna al campo "Código QR/barras", expandiendo automáticamente la sección de identificación.
2. **Lectura NFC (icono de NFC):** Si el teléfono cuenta con sensor NFC habilitado, toque el icono para abrir el diálogo "Leer tag NFC" y acerque el arete o botón electrónico a la parte trasera del dispositivo. El código capturado se asigna a "Código tag NFC".
3. **Estado del Lector Bluetooth (icono de Bluetooth):** Muestra el estado de enlace con el bastón lector o báscula ganadera inalámbrica. Al recibir la lectura inalámbrica del microchip, el número se traslada automáticamente al campo "Código de chip".

#### 2. Selección de Fotografía

1. Toque el círculo central sobre la silueta del animal para abrir el selector de imagen.
2. Elija tomar una foto con la cámara del dispositivo o seleccionar una imagen desde la galería de fotos.
3. Si no adjunta ninguna fotografía, el sistema conservará la silueta ilustrada por defecto.

#### 3. Clasificación y Código Principal

1. **Sexo:** Seleccione entre "Macho" o "Hembra" mediante los botones de selección excluyente.
2. **"Tipo de animal":** Si la finca maneja múltiples especies ganaderas, seleccione la especie correspondiente en el menú desplegable (bovino, equino, bufalino, caprino, ovino o porcino). Si la finca solo maneja una especie, vendrá seleccionada de forma predeterminada.
3. **"Código":** Escriba el número de arete o identificador visual principal del animal (campo obligatorio y alfanumérico).

#### 4. Sección Desplegable "Identificación"

Presione la cabecera "Identificación" para desplegar los códigos complementarios:

1. **"Código de raza":** Ingrese el código alfanumérico de registro genealógico si el ejemplar pertenece a una asociación de raza. Puede tocar el icono de ayuda (?) para consultar la descripción del campo.
2. **"Código de chip":** Muestra el código de microchip inyectable o bolo ruminal capturado por el lector Bluetooth (campo protegido de solo lectura manual).
3. **"Código tag NFC":** Muestra el identificador de proximidad leído por el sensor NFC del teléfono.
4. **"Código QR/barras":** Muestra el código capturado mediante el escáner de la cámara.

#### 5. Sección "Información"

1. **"Nombre":** Ingrese el nombre asignado al animal (opcional).
2. **"Fecha de nacimiento":** Toque el selector de calendario para indicar el día de nacimiento del animal (no admite fechas posteriores al día actual). Al seleccionarla, la app calcula automáticamente su etapa de desarrollo zootécnico.
3. **"Propietario":** Seleccione en la lista al titular o dueño legal del ejemplar dentro de la finca.
4. **"Lote":** Asigne el potrero, división o lote de manejo inicial del animal.
5. **"Raza" y Cruces Raciales:**
    - Para raza pura o predominante: Seleccione la raza en el menú desplegable "Raza".
     - Para animales mestizos o cruzados: Presione el botón con icono de cruce racial ubicado junto al selector. Se abrirá la ventana "Seleccionar cruce de razas":
       - Seleccione la primera raza en "Raza" e ingrese su porcentaje en "Porcentaje" (1 al 100%).
       - Seleccione la segunda raza en "Cruce de razas". El sistema autocompleta el porcentaje restante para sumar 100%.
       - Presione "Listo" para guardar la composición racial del ejemplar.
6. **"Propósito":** Seleccione la orientación productiva del animal en la finca ("Carne", "Leche", "Doble propósito" o "Trabajo").
7. **"¿Está en la finca?":** Marque la casilla de verificación si el animal se encuentra físicamente en el predio o desmárquela si está en tránsito, pastoreo externo o préstamo.

#### 6. Sección "Pesajes"
Indica los pesos corporales según la unidad oficial de la finca (kg o lb):
1. **"Peso nacimiento":** Ingrese el peso registrado al momento del parto (disponible siempre).
2. **"Peso destete":** Ingrese el peso al destete (se habilitará únicamente si la etapa del animal calculada por edad y especie es destetado o superior).
3. **"Peso al año":** Ingrese el peso a los doce meses de edad (se habilitará únicamente si el animal cuenta con al menos 1 año de edad cumplido según su fecha de nacimiento).

#### 7. Sección "Origen" (Genealogía Parental)
1. **"Padre":** Toque el selector para elegir al padre biológico. La lista filtra exclusivamente machos adultos o reproductores registrados en la finca. Al seleccionarlo, se despliega una tarjeta con los datos del reproductor.
2. **"Madre":** Toque el selector para elegir a la madre biológica. La lista filtra exclusivamente hembras adultas o reproductoras de la finca. Al seleccionarla, se despliega una tarjeta con los datos de la reproductora.

#### 8. Sección "Otros"
1. **"Notas y observaciones":** Campo de texto multilínea para ingresar señas particulares, cicatrices, tatuajes de fierro o detalles de manejo.

#### 9. Guardar Registro
1. En la parte inferior de la pantalla presione el botón "Crear" (o "Actualizar" si está en modo de edición).
2. Tras completar el guardado exitosamente, la aplicación muestra la confirmación "Animal creado exitosamente" (o "Animal actualizado exitosamente") y retorna a la pantalla anterior (listado de animales o ficha técnica).

#### Variaciones por especie
- **Etapa productiva zootécnica:** Al modificar la fecha de nacimiento o el sexo, la clasificación zootécnica interna se recalcula adaptándose a la especie seleccionada (por ejemplo: ternero/novillo/toro/vaca en bovinos; potro/potranca/caballo/yegua en equinos; lechón/verraco/cerda en porcinos).
- **Tiempo de destete:** El cálculo de la edad para habilitar la casilla "Peso destete" se rige por los días de destete configurados en los parámetros zootécnicos de la especie en la finca.
- **Filtros genealógicos:** Los selectores de "Padre" y "Madre" muestran únicamente ejemplares adultos de la misma especie elegida para la cría.

#### Etiquetas de la interfaz en otros idiomas
| Español | Inglés | Portugués |
| :--- | :--- | :--- |
| "Crear animal" | "Create animal" | "Criar animal" |
| "Editar animal" | "Edit animal" | "Editar animal" |
| "Macho" | "Male" | "Macho" |
| "Hembra" | "Female" | "Fêmea" |
| "Tipo de animal" | "Animal type" | "Tipo de animal" |
| "Código" | "Code" | "Código" |
| "Identificación" | "Identification" | "Identificação" |
| "Código de raza" | "Breed code" | "Código da raça" |
| "Código de chip" | "Chip code" | "Código do chip" |
| "Código tag NFC" | "NFC tag code" | "Código da etiqueta NFC" |
| "Código QR/barras" | "QR/Bar code" | "Código QR/barras" |
| "Información" | "Information" | "Informação" |
| "Nombre" | "Name" | "Nome" |
| "Fecha de nacimiento" | "Date of birth" | "Data de nascimento" |
| "Propietario" | "Owner" | "Proprietário" |
| "Lote" | "Lot" | "Lote" |
| "Raza" | "Breed" | "Raça" |
| "Cruces" | "Crosses" | "Cruzas" |
| "Seleccionar cruce de razas" | "Select breed cross" | "Selecionar cruza de raças" |
| "Porcentaje" | "Percentage" | "Porcentagem" |
| "Propósito" | "Purpose" | "Propósito" |
| "¿Está en la finca?" | "Is it on the farm?" | "Está na fazenda?" |
| "Pesajes" | "Weights" | "Pesagens" |
| "Peso nacimiento" | "Birth weight" | "Peso ao nascer" |
| "Peso destete" | "Weaning weight" | "Peso ao desmame" |
| "Peso al año" | "Weight year" | "Peso ao ano" |
| "Origen" | "Origin" | "Origem" |
| "Padre" | "Father" | "Pai" |
| "Madre" | "Mother" | "Mãe" |
| "Otros" | "Others" | "Outros" |
| "Notas y observaciones" | "Notes and observations" | "Notas e observações" |
| "Crear" | "Create" | "Criar" |
| "Listo" | "Ready" | "Pronto" |
| "Animal creado exitosamente" | "Animal created successfully" | "Animal criado com sucesso" |
| "Animal actualizado exitosamente" | "Animal updated successfully" | "Animal atualizado com sucesso" |

### Matriz de Errores y Soluciones
| Mensaje en la App / Síntoma | Causa Real | Respuesta Sugerida por el Agente | Criterio de Escalamiento Humano |
| :--- | :--- | :--- | :--- |
| "El código del animal [código] ya existe" | Ya existe otro ejemplar registrado con el mismo código de arete en la finca activa | "El código de arete ingresado ya se encuentra registrado en su finca. Verifique el arete físico e ingrese una identificación que no esté en uso." | Si el usuario indica que el animal anterior fue dado de baja o vendido pero el código sigue bloqueado, transferir a soporte técnico. |
| "El código de chip [número de chip] ya existe en otro animal" | El microchip capturado por Bluetooth ya está asignado a otro ejemplar en la base de datos | "El código de microchip detectado ya pertenece a otro animal registrado en el sistema. Asegúrese de que no se esté escaneando un ejemplar previamente ingresado." | Si se trata de un chip reutilizado tras una baja formal, escalar a soporte técnico. |
| "El código de tag NFC [código NFC] ya existe en otro animal" | El arete o botón NFC leído por el sensor ya fue registrado en otro ejemplar | "El identificador NFC leído ya se encuentra asignado a otro animal en su cuenta. Verifique el arete electrónico antes de continuar." | Si el arete es nuevo y original de fábrica, transferir a soporte. |
| "El código QR o de barras [código] ya existe en otro animal" | El código de barras o QR escaneado con la cámara ya está en uso en la finca | "El código escaneado con la cámara ya pertenece a otro ejemplar en su finca. Revise el arete visual del lote." | Si se verifica que el arete no está duplicado, escalar a soporte. |
| "Tu cuenta excede la cantidad máxima de animales permitidos..." | Se alcanzó el cupo máximo de animales según la suscripción o plan activo de la finca | "Ha alcanzado el límite máximo de animales permitidos en su membresía actual. Para continuar registrando animales, amplíe o actualice su plan en la sección de suscripción." | Si el ganadero ya realizó el pago de una ampliación y aún no se refleja en su cuenta, transferir a facturación con el comprobante de pago. |
| "Con tu perfil de [rol], NO tienes permisos para realizar esta acción." | El colaborador no cuenta con el permiso de creación o edición de animales en la finca activa | "Su usuario no tiene autorización para registrar o modificar animales en esta finca. Solicite al propietario o administrador de la finca que le otorgue los permisos correspondientes en la administración de colaboradores." | No escalar, restricción de permisos del predio configurada por el propietario. |
| "Este dispositivo no soporta la lectura de tags NFC" | El teléfono móvil no cuenta con hardware de sensor NFC integrado | "Su teléfono no cuenta con sensor NFC para lectura de aretes de proximidad. Puede ingresar la identificación manualmente o utilizar el lector Bluetooth de microchips y el escáner de cámara." | No escalar, incompatibilidad física de hardware del dispositivo móvil. |
| "Fallo en la lectura, inténtalo de nuevo." | Error de lectura por mal contacto o interferencia al aproximar el arete NFC | "No fue posible leer el arete NFC. Mantenga el arete firme contra la parte trasera del teléfono durante 2 a 3 segundos e inténtelo nuevamente." | Si persiste en múltiples aretes con NFC activado, verificar configuración de NFC del teléfono. |
| Las casillas "Peso destete" o "Peso al año" aparecen deshabilitadas | La fecha de nacimiento o la etapa zootécnica no cumplen los requisitos biológicos mínimos | "Por consistencia zootécnica, el peso al destete solo se habilita para animales en etapa de destete o superior, y el peso al año requiere que el animal tenga al menos 12 meses cumplidos según su fecha de nacimiento." | No escalar, validación biológica y zootécnica esperada. |
| No captura la lectura de microchip desde el bastón Bluetooth | El lector inalámbrico no está enlazado o carece de permisos de Bluetooth | "Verifique que el bastón lector esté encendido y que el icono de Bluetooth en la barra superior aparezca conectado. Asegúrese de haber concedido los permisos de Bluetooth a la aplicación en los ajustes de su teléfono." | Si el lector está conectado y no transmite datos a la app, transferir a soporte de hardware indicando la marca y modelo del bastón. |
| Círculo de espera infinito / Pantalla congelada en cargando | Proceso en segundo plano bloqueado o timeout en el dispositivo al guardar | "Espere 30 segundos. Si no avanza, cierre la aplicación por completo desde el administrador de tareas de su teléfono (deslizando hacia arriba) y vuelva a abrirla. Sus datos locales no se perderán." | Si tras reabrir la app la pantalla vuelve a congelarse, transferir de inmediato a soporte humano con correo y modelo del teléfono. |

### Directivas de Seguridad y Guardrails
- Nunca solicites contraseñas, códigos SMS, pines ni datos bancarios o tarjetas de crédito por el chat.
- Verifica siempre que el ganadero esté ubicado en la finca correcta antes de orientar la creación o edición de animales.
- No prometas funciones, compatibilidades con lectores no soportados ni plazos que no estén documentados.
- No compartas información de otras fincas ni de otros usuarios registrados en el sistema.
- Recuerda al ganadero que los códigos de arete, microchip y NFC deben ser estrictamente únicos dentro de su predio para asegurar la trazabilidad oficial y pesajes sin confusiones.
- Confirma al usuario que todos los ejemplares registrados sin conexión a internet en el potrero quedan guardados en su teléfono y se sincronizarán automáticamente con la nube al recuperar cobertura.
