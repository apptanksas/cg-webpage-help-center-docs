---
title: "Registro Masivo de Leche"
modulo_id: "animal-batch-milking"
nombre_funcionalidad: "Registro Masivo de Leche"
tipo_documento: "guia-app"
categoria: "produccion-hardware"
submodulo: "lecheria"
especies_aplicables: ["bovinos", "bufalinos", "caprinos"]
version_minima_app: "2025.05.1"
confianza_reglas: "verificada-con-tests"
fecha_actualizacion: "2026-10-19"
intenciones_y_sinonimos:
  - "como registrar el pesaje de leche de varias vacas"
  - "control de leche en lote durante el ordeño"
  - "pesar leche de varias vacas al mismo tiempo"
  - "registro masivo de ordeño y concentrado"
  - "como anotar los litros de leche con baston o chip"
  - "control lechero diario masivo"
---

# Registro Masivo de Leche

### Resumen y Alcance Funcional
Pantalla de captura lechera asistida por pasos que permite registrar la producción individual de leche y el consumo de alimento concentrado de múltiples hembras lecheras en una sola sesión continua durante la rutina de ordeño de la finca ganadera. Diseñada para agilizar el pesaje en la sala de ordeño, permite seleccionar la jornada por turnos ("Mañana", "Tarde" o "Mañana y Tarde"), vincular la sesión a un hato o potrero, sincronizar bastones o lectores electrónicos por Bluetooth para identificación inmediata de los animales, y consolidar en tiempo real los totales de animales pesados, leche recolectada y concentrado suministrado antes de finalizar el registro del lote.

- **Especies a las que aplica:** Aplica exclusivamente a especies ordeñables con aptitud lechera registradas en la finca: bovinos, bufalinos y caprinos. Las demás especies (ovinos, porcinos y equinos) están excluidas del control lechero.
- **¿Funciona sin conexión a internet (Modo Offline)?:** Sí. El asistente de pasos, los filtros de animales elegibles, la conexión con lectores Bluetooth, la tabla acumulada y el guardado de la sesión funcionan completamente sin conexión a internet.
- **Comportamiento de sincronización:** Los pesajes de leche individuales y el seguimiento de la sesión en lote se guardan de inmediato en la base de datos local del dispositivo móvil. Al recuperar conexión a internet (Wi-Fi o datos móviles), los datos se sincronizan automáticamente en segundo plano con el servidor de la finca ganadera.
- **Plataformas:** Funciona igual en Android y en iOS.

### Reglas de Negocio y Restricciones
- **Permisos requeridos por rol en la finca:**
  - El usuario debe contar con el permiso de creación de ordeño en la finca activa, tanto para añadir registros individuales a la lista como para guardar y finalizar la sesión masiva.
  - Si el colaborador carece de dicho permiso, el sistema bloquea la acción mostrando la alerta: "Con tu perfil de %1$s, NO tienes permisos para realizar esta acción."
- **Población de animales elegible en el selector:**
  - **Sexo:** Únicamente hembras (sexo hembra).
  - **Especie:** Restringido a especies lecheras compatibles: bovinos, bufalinos y caprinos.
  - **Etapa productiva:** Solo hembras en etapas "Adulto" o "Senior".
  - **Propósito productivo:** Exclusivamente animales cuyo propósito sea "Leche" o "Doble propósito".
  - **Estado y presencia:** El animal debe estar vivo (excluye fallecidos) y físicamente presente en la finca actual (excluye vendidos, trasladados o ausentes).
  - **Exclusión por pesaje previo en la sesión:** Si una hembra ya fue agregada a la lista de la sesión en curso, se excluye automáticamente del selector para evitar duplicar su pesaje en la misma fecha.
- **Identificación electrónica mediante lector Bluetooth:**
  - Es posible escanear el microchip o arete electrónico de la hembra utilizando un bastón o lector inalámbrico vinculado.
  - Si el chip leído corresponde a un animal macho, una cría joven, o un ejemplar de aptitud no lechera (como carne exclusiva o especie no lechera), la aplicación rechaza la lectura alertando: "El animal no es compatible para ser ordeñado".
  - Si el código de chip no existe en los registros de la finca, la app alerta: "No se encontró ningún animal con el código %1$s".
- **Protección de sesión activa en progreso:**
  - Mientras existan animales pesados en la lista temporal de la sesión, los selectores generales de "Fecha", "Hato" y "Potrero" quedan deshabilitados en el Paso 1, mostrándose la advertencia: "Hay una sesión de registro en progreso; continúa el proceso o finalízalo."
  - Esto garantiza que todos los pesajes consolidados en la tabla compartan exactamente la misma fecha y ubicación de pastoreo.
- **Validaciones zootécnicas y de formulario:**
  - **Fecha del control:** Por defecto sugiere el día actual. Admite fechas pasadas (hasta el rango máximo configurado en la app), pero no admite fechas futuras.
  - **Período del día:** Admite turnos simples ("Mañana" o "Tarde") o turnos compuestos ("Mañana y Tarde"). Al elegir turnos compuestos, el formulario despliega subsecciones independientes de pesaje para cada horario.
  - **Cantidades numéricas:** Los campos de "Concentrado" y "Leche" admiten valores numéricos decimales mayores o iguales a cero, acompañados de las unidades de medida oficiales configuradas en la finca (litros para leche; kilogramos o libras para concentrado). Ambos campos son obligatorios al momento de presionar "Agregar".
- **Acumulados y tabla en lote:**
  - Cada animal agregado actualiza automáticamente los contadores de "Cantidad de animales", total de "Concentrado" y "Total de leche".
  - La tabla inferior muestra las columnas "Animal", "Período del día", "Concentrado" y "Total de leche". Cada fila cuenta con un icono de retiro que permite eliminar el pesaje del lote de inmediato.
- **Confirmación de finalización:**
  - Al presionar "Finalizar", el sistema solicita confirmación mediante el diálogo: "¿Quieres finalizar el proceso de registro de ordeño?". Al confirmar, se guardan los pesajes en el historial individual de cada hembra y se crea el seguimiento del lote, mostrando el mensaje "Registro masivo creado exitosamente".

### Flujo Paso a Paso para el Usuario
- **Ruta de acceso en la aplicación:**
  - **Ruta principal (Desde el menú contextual de acciones rápidas):** En la pantalla principal de la finca, presione el botón flotante central (+) > En el menú "¿Qué quieres hacer hoy?", seleccione "Registro masivo de leche".

#### Paso 1: Configurar los datos generales de la sesión
1. En la barra superior visualizará el título "Registro masivo" y la flecha de navegación para volver a la pantalla anterior.
2. Si dispone de un bastón o lector de microchip Bluetooth, puede verificar el botón con icono de antena en la barra superior para comprobar la vinculación del dispositivo lector.
3. En la primera vista del asistente configure:
   - **"Fecha":** Confirme la fecha de la jornada de pesaje. Sugiere la fecha de hoy; si asienta un control anterior, presione el campo para desplegar el selector de fecha.
   - **"Período del día":** Seleccione en el menú desplegable el turno del pesaje: "Mañana", "Tarde" o "Mañana y Tarde".
   - **"Hato" (Opcional):** Si agrupa sus animales por lotes lecheros, presione el campo para seleccionar el hato correspondiente.
   - **"Potrero" (Opcional):** Si desea registrar la pradera donde pastaron las vacas antes del ordeño, seleccione el potrero correspondiente.
4. Deslice la pantalla hacia la izquierda o avance para ingresar a la vista de pesaje individual de animales.

#### Paso 2: Registrar la producción individual de las hembras
1. En el encabezado "Producción del animal", seleccione la hembra a registrar:
   - **Selección manual:** Presione el campo "Seleccionar animal". Se abrirá el selector con las hembras lecheras adultas activas que aún no han sido pesadas en la sesión. Busque y elija el animal por arete o nombre.
   - **Lectura por bastón electrónico:** Acerque el lector Bluetooth al arete electrónico o microchip del animal. El sistema reconocerá automáticamente a la hembra y la seleccionará en el formulario.
2. Debajo del animal seleccionado, complete los campos para cada período configurado:
   - **"Concentrado":** Ingrese la cantidad de alimento balanceado suministrado en el comedero (acompañado de la unidad de peso de la finca).
   - **"Leche":** Ingrese la producción de leche obtenida del ordeño (acompañada de la unidad de volumen de la finca).
3. Presione el botón "Agregar".
4. El animal se añadirá a la tabla inferior, el formulario de animal se limpiará automáticamente, y los resúmenes en pantalla se actualizarán:
   - **"Cantidad de animales":** Número total de hembras registradas en la jornada.
   - **"Concentrado":** Total acumulado de alimento balanceado consumido por el grupo.
   - **"Total de leche":** Total acumulado de leche producida en la sesión.
5. Continúe seleccionando o escaneando las siguientes hembras y presionando "Agregar" consecutivamente.

#### Paso 3: Revisión y Retiro de Registros en la Tabla
1. En la parte inferior revise la tabla de registros acumulados, con columnas: "Animal", "Período del día", "Concentrado" y "Total de leche".
2. **Para corregir o eliminar un pesaje:** Presione el icono de caneca o retiro ubicado al final de la fila de la hembra correspondiente. El registro se eliminará de la lista, la hembra volverá a estar disponible en el selector de animales y los acumulados generales se recalcularán de inmediato.

#### Paso 4: Finalizar la Sesión de Ordeño
1. Una vez concluido el pesaje de todo el lote de ordeño, presione el botón "Finalizar" ubicado en la barra de control inferior.
2. Aparecerá la ventana de confirmación: "¿Quieres finalizar el proceso de registro de ordeño?".
3. Presione la opción de confirmar. El sistema almacenará definitivamente todos los pesajes, mostrará la notificación emergente "Registro masivo creado exitosamente" y regresará a la pantalla previa.
- **Pantalla de llegada tras guardar:** El usuario regresa a la pantalla principal o menú previo de la aplicación con la sesión completada y respaldada en la memoria del dispositivo.

#### Variaciones por especie
- **Especies admitidas en ordeño:** El sistema filtra exclusivamente hembras pertenecientes a bovinos (vacas), bufalinos (búfalas) y caprinos (cabras).
- **Especies no compatibles:** Las especies porcina (cerdas), ovina (ovejas) y equina (yeguas) no son admitidas en este control lechero. Si se intenta escanear el chip de un animal de estas especies, la aplicación bloquea la selección indicando: "El animal no es compatible para ser ordeñado".
- **Unidades de medida zootécnicas:** Los campos de pesaje de leche y alimento reflejan las unidades oficiales establecidas en la configuración de la finca (por ejemplo, litros para leche y kilogramos o libras para concentrado).

#### Etiquetas de la interfaz en otros idiomas
| Español | Inglés | Portugués |
| :--- | :--- | :--- |
| "Registro masivo" | "Bulk registration" | "Registrar em massa" |
| "Registro masivo de leche" | "Milking Bulk Registration" | "Registro de leite em massa" |
| "Fecha" | "Date" | "Data" |
| "Período del día" | "Period day" | "Período do dia" |
| "Mañana" | "Morning" | "Manhã" |
| "Tarde" | "Afternoon" | "Tarde" |
| "Hato" | "Herd" | "Rebanho" |
| "Potrero" | "Pasture" | "Pasto" |
| "Producción del animal" | "Animal production" | "Produção animal" |
| "Seleccionar animal" | "Select animal" | "Selecionar animal" |
| "Concentrado" | "Concentrate" | "Concentrado" |
| "Leche" | "Milk" | "Leite" |
| "Total de leche" | "Total milk" | "Total de leite" |
| "Cantidad de animales" | "Quantity of animals" | "Quantidade de animais" |
| "Agregar" | "Add" | "Adicionar" |
| "Finalizar" | "Finish" | "Finalizar" |

### Matriz de Errores y Soluciones
| Mensaje en la App / Síntoma | Causa Real | Respuesta Sugerida por el Agente | Criterio de Escalamiento Humano |
| :--- | :--- | :--- | :--- |
| "El animal no es compatible para ser ordeñado" | Se escaneó un microchip perteneciente a un macho, una cría, una hembra de aptitud cárnica estricta, o una especie no lechera (equino, porcino u ovino) | "El registro masivo de ordeño solo permite ingresar hembras adultas o seniors de propósito leche o doble propósito de las especies bovina, bufalina o caprina. Verifique en la hoja de vida del animal su sexo, especie y propósito productivo." | No escalar, validación zootécnica de la aplicación. |
| "No se encontró ningún animal con el código %1$s" | El código de microchip leído por el bastón Bluetooth no existe en la base de datos de la finca activa | "El microchip escaneado no está registrado en los animales de esta finca. Verifique que el código coincida con el arete físico del ejemplar o agregue el código de chip en la ficha técnica del animal antes de escanearlo." | No escalar, verificar inventario de animales de la finca. |
| "Hay una sesión de registro en progreso; continúa el proceso o finalízalo." | Se intentó modificar la fecha, el hato o el potrero en el Paso 1 mientras ya existen animales agregados a la lista de la sesión | "Para mantener la consistencia de la jornada, la fecha, el hato y el potrero no pueden cambiarse mientras haya animales agregados en la lista. Finalice el pesaje actual o retire los animales de la tabla si requiere modificar estos datos iniciales." | No escalar, regla de consistencia de la sesión en lote. |
| "Con tu perfil de %1$s, NO tienes permisos para realizar esta acción." | El colaborador carece del permiso de registro de ordeño en la finca activa | "Su usuario no cuenta con autorización para registrar controles de ordeño en esta finca. Solicite al propietario o administrador de la finca que le habilite los permisos correspondientes en la administración de colaboradores." | No escalar, restricción de permisos del predio configurada por el propietario. |
| "¿Quieres finalizar el proceso de registro de ordeño?" | Diálogo de confirmación del sistema al presionar el botón "Finalizar" | "El sistema le solicita confirmación antes de almacenar de forma definitiva la sesión de pesaje. Presione 'Aceptar' para guardar todos los registros y cerrar la jornada, o cancele si aún faltan vacas por registrar." | No escalar, diálogo de seguridad de la aplicación. |
| La hembra no figura en la lista del selector "Seleccionar animal" | El animal ya fue agregado en la sesión actual, es macho, cría joven, no tiene aptitud lechera, o se encuentra inactivo/vendido | "El selector solo muestra hembras lecheras activas que aún no han sido pesadas en esta sesión. Compruebe si el animal ya se encuentra en la tabla inferior o revise en la lista general de animales que cumpla con los requisitos de etapa y aptitud lechera." | Si el usuario confirma que la hembra cumple con todos los requisitos y no figura en la tabla ni en el selector, escalar a soporte técnico indicando el código de arete. |
| El botón "Agregar" no responde al presionarlo | No se ha seleccionado una hembra o los campos de leche o concentrado se encuentran vacíos | "Asegúrese de haber seleccionado una hembra en el campo 'Seleccionar animal' y de haber digitado valores numéricos válidos en los campos de 'Concentrado' y 'Leche' para cada período del día configurado." | No escalar, validación de campos obligatorios del formulario. |
| Espera prolongada al finalizar la sesión | Interrupción momentánea en el almacenamiento de la base de datos local o en el proceso de tracking | "Espere unos segundos. Si la pantalla no avanza, cierre la aplicación por completo y vuelva a abrirla. Los pesajes previamente guardados en su dispositivo móvil se mantendrán seguros." | Si tras reiniciar la aplicación la pantalla vuelve a congelarse al presionar 'Finalizar', escalar a soporte técnico indicando el correo del usuario y modelo del teléfono. |

### Directivas de Seguridad y Guardrails
- Nunca solicites contraseñas, códigos SMS, pines ni datos bancarios por el chat.
- Los agentes de soporte no deben alterar registros de producción láctea, acumulados ni datos de pesaje directamente en bases de datos sin autorización explícita del propietario de la finca ganadera.
- Confirma siempre que el ganadero esté posicionado en la finca correcta antes de orientar la eliminación de registros de ordeño o lotes de producción.
- No brindes instrucciones para alterar calibraciones de equipos de medición ni omitir controles oficiales de calidad lechera.
- Informa al usuario que todos los pesajes registrados sin conexión a internet en la sala de ordeño quedan respaldados de forma segura en la memoria de su teléfono y se sincronizarán automáticamente con la nube una vez que el dispositivo cuente con señal.
