---
title: "Datos Generales del Animal"
modulo_id: "animal-info"
nombre_funcionalidad: "Ficha Técnica y Datos Generales del Animal"
tipo_documento: "guia-app"
categoria: "inventario-trazabilidad"
submodulo: "animales"
especies_aplicables: ["todas"]
version_minima_app: "2025.05.1"
confianza_reglas: "verificada-con-tests"
fecha_actualizacion: "2026-10-16"
intenciones_y_sinonimos:
  - "como ver la ficha tecnica o datos generales de un animal"
  - "donde consultar los datos de una vaca o toro"
  - "como ver los padres y genealogia de un ejemplar"
  - "donde consultar el microchip arete o codigo nfc del animal"
  - "como ver las ultimas ubicaciones y mapa satelital del ganado"
  - "donde ver y subir documentos o certificados sanitarios del animal"
---

# Ficha Técnica y Datos Generales del Animal

### Resumen y Alcance Funcional
Pantalla de consulta exhaustiva y ficha biológica que reúne la información de identificación, características zootécnicas, procedencia comercial, genealogía parental, historial de ubicaciones georreferenciadas y gestión documental del ejemplar en la finca. Permite al ganadero verificar los diferentes códigos de identificación (arete visual, microchip electrónico, código de barras o QR, arete NFC), consultar edad, raza, pureza racial y notas de campo, navegar a la ficha de compra comercial, acceder a la hoja de vida de los progenitores (padre y madre), abrir en mapas las últimas lecturas satelitales del animal y gestionar archivos adjuntos oficiales (certificados de raza pura, propiedad, sanitarios, vacunación o documentos personalizados).

- **Especies a las que aplica:** Aplica igual para todas las especies (bovinos, equinos, bufalinos, caprinos, ovinos y porcinos).
- **¿Funciona sin conexión a internet (Modo Offline)?:** Sí, para la consulta de información general, genealogía, compras, ubicaciones y documentos locales.
- **Comportamiento de sincronización:** Toda la información del animal, sus vínculos genealógicos y registros de geolocalización se consultan y almacenan en la base de datos interna del teléfono. La carga y eliminación de archivos adjuntos se guarda localmente y se sincroniza automáticamente con el servidor cuando el dispositivo dispone de conexión a internet. La visualización de coordenadas en Google Maps y la descarga de documentos no cacheados requieren conectividad a internet.

### Reglas de Negocio y Restricciones
- **Permisos requeridos por rol en la finca:**
  - **Edición del animal:** Para modificar la información general del animal desde el botón de edición rápida (icono de lápiz) y para cargar nuevos documentos mediante el botón "Agregar documento" se requiere el permiso de actualización de animales en la finca activa.
  - **Solo lectura:** Los usuarios sin permisos de edición pueden visualizar los datos y abrir documentos ya existentes, pero no tienen disponible el botón "Agregar documento" ni las opciones de eliminación de archivos.
- **Bloqueo operativo por estado del animal (Animal bloqueado):**
  - Si el animal se encuentra bloqueado (por ejemplo, con registro de fallecimiento activo, marcado como vendido o en un traslado en curso), el botón flotante de edición rápida (icono de lápiz) sobre la portada se oculta automáticamente para preservar la trazabilidad histórica del ejemplar.
- **Comportamiento genealógico (Padres):**
  - La sección "Padres" se muestra únicamente si el animal cuenta con al menos un progenitor registrado (padre o madre). Al presionar el chip interactivo de cualquiera de los padres, la aplicación abre la pantalla de resumen del progenitor correspondiente.
- **Historial y verificación de ubicaciones:**
  - El sistema muestra las últimas 5 ubicaciones registradas del ejemplar, ordenadas cronológicamente de la más reciente a la más antigua.
  - Cada registro incluye la fecha relativa del evento, las coordenadas geográficas, el nombre del usuario verificador (con insignia de verificación) y el método utilizado (lectura por báscula, bastón electrónico o lector Bluetooth). Al presionar sobre un registro de ubicación, la aplicación abre la coordenada satelital en Google Maps.
- **Información de compra comercial:**
  - La tarjeta "Información de compra" se despliega únicamente si el ejemplar cuenta con un registro de adquisición o compra vinculado a la finca. Al presionar sobre ella, la aplicación redirige al listado consolidado de compras de ganado de la finca según la especie del ejemplar.
- **Gestión de documentos y certificados adjuntos:**
  - Formatos admitidos: Archivos en formato PDF e imágenes en formato PNG, JPG o JPEG.
  - Tipos de documentos y límites máximos por animal:
    - "Certificado de raza pura": Máximo 1 documento.
    - "Certificado de propiedad": Máximo 1 documento.
    - "Certificado sanitario": Hasta 20 documentos (permite asignar nombre personalizado).
    - "Certificado de vacunación": Hasta 50 documentos (permite asignar nombre personalizado).
    - "Documento personalizado": Hasta 50 documentos (permite asignar nombre personalizado).
  - Si un tipo de documento ha alcanzado el límite máximo permitido para ese ejemplar, no aparecerá en la lista de opciones al agregar un nuevo archivo.
  - Los documentos pendientes de subida muestran la etiqueta "Pendiente".

### Flujo Paso a Paso para el Usuario
- **Ruta de acceso en la aplicación:**
  - **Ruta 1 (Desde el resumen del animal):** En la barra inferior toque "Animales" > Seleccione un animal de la lista para ingresar a su "Resumen del Animal" > En la cuadrícula de módulos funcionales presione la tarjeta "Datos generales".

#### Cabecera y Foto de Portada
1. En la parte superior se despliega la barra con la flecha de regreso, el código y nombre del animal, y la foto de portada (o silueta zootécnica por defecto).
2. Si el ejemplar está registrado como raza pura, la portada exhibe la insignia destacada "Raza pura" con icono de verificación.
3. Si el animal no está bloqueado, se muestra el botón circular de edición rápida con icono de lápiz sobre el extremo inferior de la foto de portada. Al presionarlo, conduce al formulario de edición de datos del animal.

#### Pestaña "Información"
Presenta de forma organizada los atributos estructurales del animal:
1. **Identificadores y características biológicas:**
   - "Nombre": Nombre asignado al ejemplar.
   - "Código": Código de arete principal.
   - "Código de chip": Número de microchip inyectable o electrónico (si aplica).
   - "Código QR/barras": Identificador de código de barras o código QR (si aplica).
   - "Código tag NFC": Identificador de arete o etiqueta NFC (si aplica).
   - "Propósito": Orientación productiva del ejemplar (leche, carne, doble propósito o trabajo).
   - "Etapa del animal": Clasificación zootécnica actual adaptada a la especie y sexo del animal.
   - "Fecha de nacimiento": Fecha de parto registrada.
   - "Edad": Tiempo de vida calculado en años y meses.
   - "Raza": Composición racial del ejemplar (con icono de verificación si es raza pura).
   - "Propietario": Titular registrado del animal.
   - "Lote": Potrero o lote de manejo al que pertenece.
   - "Fecha de registro": Fecha en que el animal fue creado en el sistema.
   - "Notas y observaciones": Anotaciones o comentarios zootécnicos de campo.
2. **Tarjeta "Información de compra":**
   - Visible si el animal fue adquirido comercialmente. Despliega la "Fecha" y el "Valor" pagado por el ejemplar. Al tocar la tarjeta, se abre la tabla de compras de la finca correspondiente a la especie del animal.
3. **Sección "Padres":**
   - Visible si el animal tiene padre o madre registrados. Muestra el chip interactivo de cada progenitor con su identificación. Al tocar cualquiera de los dos chips, la aplicación navega directamente a la hoja de vida de dicho progenitor.
4. **Sección "Últimas ubicaciones":**
   - Muestra las últimas 5 lecturas de geolocalización satelital. Cada elemento contiene la fecha relativa de registro, las coordenadas geográficas, el colaborador responsable y el icono del método de verificación (báscula, bastón o lector de chip). Al pulsar sobre cualquier ubicación, se abre el mapa de Google Maps en el navegador o en la aplicación de mapas del dispositivo.

#### Pestaña "Documentos"
Permite administrar los certificados y archivos asociados al animal:
1. Presione la pestaña "Documentos".
2. **Para agregar un nuevo archivo:**
   - Toque el botón "Agregar documento" (disponible si tiene permisos de edición).
   - En la ventana modal inferior, seleccione el tipo de documento ("Certificado de raza pura", "Certificado de propiedad", "Certificado sanitario", "Certificado de vacunación" o "Documento personalizado").
   - Si el tipo lo admite, ingrese el nombre descriptivo en el campo "Nombre".
   - Presione el selector de archivo para adjuntar el documento en formato PDF o imagen (PNG, JPG, JPEG) desde la memoria del teléfono.
   - Toque "Subir archivo" para guardar el documento.
3. **Para consultar o gestionar un documento existente:**
   - Toque sobre el documento en la lista.
   - Si el archivo aún está pendiente de carga ("Pendiente"), se abrirá nuevamente la ventana de subida para completar el archivo.
   - Si el archivo ya está guardado, se abrirá el diálogo con las opciones "Ver documento" (para previsualizarlo o abrirlo en el visor de documentos) y "Eliminar" (para borrar el archivo).
   - Si presiona "Eliminar", el sistema solicita confirmación mediante la alerta "¿Estas seguro de eliminar este documento?"; toque el botón de confirmación para eliminarlo definitivamente.

- **Pantalla de llegada tras guardar o salir:**
  - Al presionar la flecha de regreso en la barra superior, retorna al resumen del animal.
  - Al presionar el botón de edición rápida (icono de lápiz), la aplicación abre la pantalla de edición del animal.

#### Variaciones por especie
- **Aplica para todas las especies:** La consulta de identificadores electrónicos, genealogía, compras, ubicaciones y documentos opera de la misma manera en bovinos, equinos, bufalinos, caprinos, ovinos y porcinos.
- **Etapa del animal:** La denominación de la etapa zootécnica exhibida en "Etapa del animal" se adapta según la especie y el sexo del ejemplar (por ejemplo, vaca, toro, novilla o ternero en bovinos; yegua, caballo, potro en equinos; cerda, verraco, lechón en porcinos).
- **Tabla de compras:** Al presionar la tarjeta "Información de compra", la aplicación abre la lista de compras filtrada específicamente para la especie del ejemplar consultado.

#### Etiquetas de la interfaz en otros idiomas
| Español | Inglés | Portugués |
| :--- | :--- | :--- |
| "Datos generales" | "General data" | "Dados gerais" |
| "Información" | "Information" | "Informação" |
| "Documentos" | "Documents" | "Documentos" |
| "Nombre" | "Name" | "Nome" |
| "Código" | "Code" | "Código" |
| "Código de chip" | "Chip code" | "Código do chip" |
| "Código QR/barras" | "QR/Bar code" | "Código QR/barras" |
| "Código tag NFC" | "NFC tag code" | "Código da etiqueta NFC" |
| "Propósito" | "Purpose" | "Propósito" |
| "Etapa del animal" | "Animal stage" | "Estágio do animal" |
| "Fecha de nacimiento" | "Date of birth" | "Data de nascimento" |
| "Edad" | "Age" | "Idade" |
| "Raza" | "Breed" | "Raça" |
| "Raza pura" | "Purebred" | "Raça pura" |
| "Propietario" | "Owner" | "Proprietário" |
| "Lote" | "Lot" | "Lote" |
| "Fecha de registro" | "Registration date" | "Data de registro" |
| "Notas y observaciones" | "Notes and observations" | "Notas e observações" |
| "Información de compra" | "Purchase information" | "Informações de compra" |
| "Fecha" | "Date" | "Data" |
| "Valor" | "Value" | "Valor" |
| "Padres" | "Parents" | "Pais" |
| "Últimas ubicaciones" | "Last locations" | "Últimas localizações" |
| "Método de verificación" | "Verification method" | "Método de verificação" |
| "Agregar documento" | "Add document" | "Adicionar documento" |
| "Subir archivo" | "Upload file" | "Enviar arquivo" |
| "Pendiente" | "Pending" | "Pendente" |
| "Ver documento" | "View document" | "Ver documento" |
| "Eliminar" | "Delete" | "Excluir" |
| "¿Estas seguro de eliminar este documento?" | "Are you sure you want to delete this document?" | "Tem certeza de que deseja excluir este documento?" |
| "Certificado de raza pura" | "Purebred certificate" | "Certificado de raça pura" |
| "Certificado de propiedad" | "Certificate of ownership" | "Certificado de propriedade" |
| "Certificado sanitario" | "Health certificate" | "Certificado sanitário" |
| "Certificado de vacunación" | "Vaccination certificate" | "Certificado de vacinação" |
| "Documento personalizado" | "Custom document" | "Documento personalizado" |

### Matriz de Errores y Soluciones
| Mensaje en la App / Síntoma | Causa Real | Respuesta Sugerida por el Agente | Criterio de Escalamiento Humano |
| :--- | :--- | :--- | :--- |
| El botón de edición rápida (icono de lápiz) no aparece sobre la foto | El ejemplar está registrado como fallecido, vendido o se encuentra en un traslado activo (bloqueo de seguridad) | "El botón de edición no se muestra si el animal se encuentra bloqueado debido a un registro de defunción, venta o traslado entre predios en curso. Para volver a habilitar los datos si hubo un error en la defunción, ingrese al resumen del animal y presione 'Cancelar muerte'." | Si el animal aparece bloqueado sin tener defunción, venta ni traslado registrado, transferir a soporte técnico. |
| El botón "Agregar documento" no aparece en la pestaña "Documentos" | El colaborador no tiene asignado el permiso de edición de animales en la finca activa | "Su usuario en esta finca no cuenta con el permiso para adjuntar o modificar documentos del animal. Solicite al propietario o administrador de la finca que le habilite los permisos de edición de animales en la sección de colaboradores." | No escalar, depende de los roles y permisos asignados por el administrador de la finca. |
| "Con tu perfil de %1$s, NO tienes permisos para realizar esta acción." | Se intentó realizar una modificación documental sin el permiso correspondiente | "Su rol actual en la finca no permite realizar esta operación sobre los documentos del animal. Comuníquese con el administrador del predio para verificar sus permisos de colaborador." | No escalar, restricción de permisos del predio. |
| La sección "Padres" no aparece en la pantalla | El ejemplar no tiene padre ni madre vinculados en su registro genealógico | "La sección de padres únicamente se muestra cuando el ejemplar cuenta con al menos un progenitor registrado en el sistema. Para agregar la genealogía, presione el botón de edición (icono de lápiz) y seleccione el padre o la madre en los campos correspondientes." | No escalar, comportamiento esperado cuando no hay genealogía cargada. |
| La tarjeta "Información de compra" no se muestra | El ejemplar nació en la finca o fue registrado sin datos de adquisición comercial previa | "La tarjeta de compra solo se despliega si el animal fue registrado originalmente como una compra comercial en la finca. Si el animal nació en el predio o se ingresó sin costo de compra, esta tarjeta permanece oculta." | No escalar, comportamiento esperado según el origen del ejemplar. |
| No abre el mapa satelital al presionar una ubicación | El dispositivo móvil no cuenta con una aplicación de mapas compatible o carece de conexión a internet activa | "Para abrir la coordenada en Google Maps se requiere conexión a internet y tener un navegador web o la aplicación de mapas instalada en su teléfono móvil. Verifique su conexión e inténtelo nuevamente." | No escalar, limitación del dispositivo o de conectividad. |
| La opción de un tipo de documento no aparece en el selector al agregar documento | Se alcanzó la cantidad máxima permitida para ese tipo de archivo en el ejemplar (por ejemplo, 1 certificado de raza pura o de propiedad) | "Ese tipo de documento ya alcanzó el cupo máximo permitido para este animal (por ejemplo, solo se permite un certificado de raza pura o propiedad por ejemplar). Para subir uno nuevo, elimine primero el certificado anterior desde la lista de documentos." | No escalar, validación de cupo máximo por tipo de documento. |

### Directivas de Seguridad y Guardrails
- Nunca pidas contraseñas, códigos SMS, códigos de verificación ni datos de pago completos por el chat.
- Verifica que el usuario esté en la finca correcta antes de sugerir eliminar o modificar registros del animal o sus documentos adjuntos.
- No prometas funciones, plazos ni resultados que no estén documentados.
- No compartas información de otras fincas ni de otros usuarios.
- Recuerde al usuario que los códigos de identificación oficiales (arete visual, microchip, código QR y arete NFC) deben ser únicos para evitar inconsistencias en lecturas electrónicas y pesajes.
- Advierta al usuario que al presionar "Eliminar" sobre un documento adjunto, el archivo se desvincula de forma permanente de la hoja de vida del ejemplar.
