---
title: "Pesaje con Báscula"
modulo_id: "pesajes-registro-masivo-pesaje"
nombre_funcionalidad: "Registro Masivo de Pesaje con Báscula"
tipo_documento: "guia-app"
categoria: "produccion-hardware"
submodulo: "pesajes"
especies_aplicables: ["todas"]
version_minima_app: "2025.05.1"
confianza_reglas: "verificada-con-tests"
fecha_actualizacion: "2026-10-19"
intenciones_y_sinonimos:
  - "como pesar el ganado por lote"
  - "pesar animales con bascula bluetooth"
  - "registro masivo de peso de animales"
  - "conectar la romana o bascula al telefono"
  - "pesar vacas con baston lector de chip"
  - "jornada de pesaje continuo en la manga"
---

# Registro Masivo de Pesaje con Báscula

### Resumen y Alcance Funcional
Herramienta de pesaje masivo y continuo diseñada para registrar el peso corporal de múltiples animales de forma ágil y consecutiva durante trabajos en la manga, báscula o corral de la finca ganadera. Permite capturar el peso de cada animal mediante digitación manual o en tiempo real a través de básculas ganaderas electrónicas vinculadas por Bluetooth, además de admitir la identificación instantánea mediante bastones lectores de chip RFID. El sistema computa de forma automática la ganancia o pérdida individual frente al pesaje inmediatamente anterior, actualiza las métricas acumuladas de la sesión (conteo de animales, peso total y ganancia neta) y consolida el historial en la base de datos de la finca.

- **Especies a las que aplica:** Aplica a todas las especies gestionadas en la aplicación: bovinos, bufalinos, equinos, caprinos, ovinos y porcinos.
- **¿Funciona sin conexión a internet (Modo Offline)?:** Sí. Toda la captura de pesos, conexión de dispositivos Bluetooth (báscula e identificador de chips), cálculo de ganancias y almacenamiento en tabla operan de manera local sin necesidad de internet ni cobertura celular.
- **Comportamiento de sincronización:** Cada pesaje individual añadido a la sesión se guarda de manera inmediata en la base de datos local del dispositivo móvil. Al finalizar la jornada, se crea el seguimiento del lote y, tan pronto el teléfono detecte conexión a internet (Wi-Fi o datos móviles), todos los pesajes y cálculos se sincronizan automáticamente en segundo plano con el servidor de la finca ganadera.
- **Plataformas:** Funciona con idéntica interfaz y capacidades operativas en Android y en iOS. La vinculación de dispositivos inalámbricos (báscula y lector de chip) requiere habilitar los permisos de Bluetooth del sistema operativo en el teléfono.

### Reglas de Negocio y Restricciones
- **Permisos requeridos por rol en la finca:**
    - Requiere el permiso de creación de pesos en la finca ganadera activa.
    - Para vincular la báscula ganadera electrónica por Bluetooth, el usuario requiere el permiso de conexión Bluetooth y otorgar los permisos de hardware solicitados por el sistema operativo del teléfono.
    - Si el colaborador carece de los permisos correspondientes, la aplicación detiene la acción y despliega: "Con tu perfil de %1$s, NO tienes permisos para realizar esta acción."
- **Fecha de la jornada:**
    - El campo "Fecha" toma de forma automática e invariable la fecha actual del dispositivo móvil.
    - Se encuentra deshabilitado para edición manual con el fin de garantizar la veracidad cronológica del pesaje en manga.
    - Si la báscula Bluetooth está conectada, el selector de fecha se oculta automáticamente para optimizar el espacio de trabajo en pantalla.
- **Dispositivos inalámbricos (Hardware opcional):**
    - **"Lector de chip":** Permite conectar un bastón lector RFID por Bluetooth. Al escanear una orejera electrónica, la aplicación busca el animal en el inventario y lo selecciona en el formulario. Si el chip no existe en la finca, muestra la alerta: "No se encontró ningún animal con el código de chip %1$s."
    - **"Báscula":** Permite emparejar un indicador de pesaje Bluetooth compatible. Al vincularse, el botón cambia su etiqueta a "Conectado" en color azul y muestra la notificación "Bascula conectada". El campo de texto de peso se sustituye por el visor digital ("DigitalWeightDisplay") con indicador de peso estabilizado. Si el dispositivo se apaga o pierde cobertura, el sistema avisa con el mensaje: "La bascula se ha desconectado".
- **Tipo de alimentación del lote:**
    - Selector desplegable con 10 regímenes nutricionales del catálogo: "Pastoreo", "Pastoreo + Concentrado", "Heno", "Ensilage", "Concentrado", "Suplementos", "Forraje", "Raciones mezcladas", "Estabulación" y "Otros".
    - Por defecto, el sistema asigna "Pastoreo".
- **Filtro de animales elegibles:**
    - Sección colapsable "Aplicar filtro de animales" para delimitar la búsqueda en lotes grandes.
    - **"Tipo de animal":** Si la finca tiene configurada más de una especie, permite seleccionar la especie a filtrar; si la finca administra una única especie, el selector se bloquea en esa especie por defecto.
    - **"Seleccionar filtro de animales":** Permite acotar por potrero, lote o categoría zootécnica.
    - Solo se muestran animales vivos que se encuentren físicamente en la finca activa.
    - **Prevención estricta de duplicados:** Un animal que ya haya sido pesado y añadido a la tabla de la sesión activa queda excluido automáticamente del selector de animales para evitar duplicidades en la misma jornada.
- **Cálculo automático de ganancia de peso:**
    - Al ingresar o capturar el peso de un animal, el sistema busca en su historial su pesaje inmediatamente anterior (con desplazamiento de un registro hacia atrás).
    - La columna "Ganancia" muestra la diferencia matemática exacta (peso actual menos peso previo).
    - Si el ejemplar no cuenta con pesajes anteriores registrados en la finca, se toma el peso actual como valor base inicial.
    - En el panel de estadísticas, la "Ganancia de peso total" se resalta con signo positivo y color verde si la ganancia neta es superior a cero, o en color rojo si representa una pérdida de peso acumulada.
- **Gestión de la sesión y tabla de pesajes:**
    - Cada animal pesado mediante el botón "Agregar" se inserta en la parte superior de la tabla y se notifica con el mensaje: "Peso registrado exitosamente".
    - El usuario puede descartar o corregir un registro erróneo presionando el ícono de papelera ubicado en el extremo derecho de la fila en la tabla de datos, lo que reincorpora al animal al selector y recalcula los totales.
    - Para finalizar la jornada mediante el botón "Finalizar", es requisito contar con al menos un pesaje en la tabla. Si la tabla está vacía, el sistema muestra: "No hay pesos para registrar. Por favor, agregue al menos un peso para continuar."
    - Al presionar "Finalizar", la app solicita confirmación mediante el diálogo: "¿Quieres finalizar el proceso de registro pesos?". Tras confirmar, crea el seguimiento de lote, emite el mensaje "Registro masivo creado exitosamente" y regresa a la pantalla previa.

### Flujo Paso a Paso para el Usuario
- **Ruta de acceso en la aplicación:**
    - Pantalla principal de la finca > Botón flotante central con ícono de casa y suma (+) > Menú de opciones rápidas > Presionar "Pesaje con bascula".

#### 1. Preparación de Dispositivos y Filtros de Lote
1. En la barra superior confirme el título "Pesaje con bascula" junto al botón de flecha para volver.
2. En la sección "Conectar dispositivos", vincule sus equipos inalámbricos (opcional):
    - Presione "Lector de chip" para emparejar el bastón RFID por Bluetooth.
     - Presione "Báscula" para conectar el indicador de peso electrónico. Al conectarse, observará la notificación "Bascula conectada" y la etiqueta cambiará a "Conectado".
3. En el campo "Tipo de alimentación", seleccione el régimen alimenticio del lote si difiere de "Pastoreo".
4. Si requiere trabajar con un subgrupo particular del ganado, despliegue "Aplicar filtro de animales":
    - Seleccione el "Tipo de animal" (si la finca maneja múltiples especies).
     - Presione "Seleccionar filtro de animales" y delimite por potrero, lote o categoría.

#### 2. Identificación del Animal y Captura del Peso
1. En la sección "Registrar peso", identifique el ejemplar:
    - Toque "Seleccionar animal" para escogerlo de la lista, o escanee su orejera electrónica con el bastón lector RFID conectado.
2. Obtenga el peso corporal:
    - Si la báscula Bluetooth está conectada, coloque al animal sobre la plataforma y espere a que el visor digital muestre la lectura estabilizada.
     - Si realiza captura manual, digite el peso en el campo "Peso" (en la unidad configurada para la finca: kilogramos o libras).
3. Presione el botón "Agregar" (se habilita únicamente cuando hay un animal seleccionado y el peso es mayor a cero).
4. El sistema emite la notificación "Peso registrado exitosamente", añade el registro a la tabla, actualiza los contadores acumulados y limpia el formulario para el siguiente animal.

#### 3. Revisión de Totales y Cierre de la Sesión
1. Debajo del botón de adición, revise los paneles de resumen:
    - "Cantidad de animales": Número de animales procesados en la sesión.
     - "Peso total": Sumatoria de kilos o libras registrados en el lote.
     - "Ganancia de peso total": Balance neto de ganancia o pérdida respecto a los pesajes anteriores.
2. En la tabla de datos inferior verifique las columnas "Animal", "Peso" y "Ganancia". Si necesita retirar un pesaje equivocado, presione el ícono de eliminar fila en la tarjeta correspondiente.
3. Al terminar de pesar a todos los animales, presione el botón "Finalizar".
4. En la ventana emergente confirme la pregunta: "¿Quieres finalizar el proceso de registro pesos?".

**Pantalla de llegada tras guardar:** El sistema consolida el lote, muestra la confirmación "Registro masivo creado exitosamente" y redirige al usuario de vuelta a la pantalla previa.

#### Variaciones por especie
- **Cobertura zootécnica universal:** Aplica a todas las especies administradas en la finca (bovinos, bufalinos, equinos, caprinos, ovinos y porcinos).
- **Parámetros zootécnicos:** La unidad de pesaje (kg o lb) y la dinámica de pesaje en manga son uniformes para todas las especies según la configuración general de la finca ganadera activa.

#### Etiquetas de la interfaz en otros idiomas
| Español | Inglés | Portugués |
| :--- | :--- | :--- |
| "Pesaje con bascula" | "Scale weighing" | "Pesagem com balança" |
| "Conectar dispositivos" | "Connect devices" | "Conectar dispositivos" |
| "Lector de chip" | "Chip reader" | "Leitor de chip" |
| "Báscula" | "Scale" | "Balança" |
| "Conectado" | "Connected" | "Conectado" |
| "Fecha" | "Date" | "Data" |
| "Tipo de alimentación" | "Feed type" | "Tipo de alimentação" |
| "Aplicar filtro de animales" | "Apply animal filter" | "Aplicar filtro de animais" |
| "Tipo de animal" | "Animal type" | "Tipo de animal" |
| "Seleccionar filtro de animales" | "Select animal filter" | "Selecionar filtro de animais" |
| "Registrar peso" | "Register weight" | "Registrar peso" |
| "Seleccionar animal" | "Select animal" | "Selecionar animal" |
| "Peso" | "Weight" | "Peso" |
| "Agregar" | "Add" | "Adicionar" |
| "Cantidad de animales" | "Animals quantity" | "Quantidade de animais" |
| "Peso total" | "Total weight" | "Peso total" |
| "Ganancia de peso total" | "Total weight gain" | "Ganho total de peso" |
| "Animal" | "Animal" | "Animal" |
| "Ganancia" | "Gain" | "Ganho" |
| "Finalizar" | "Finish" | "Finalizar" |
| "Bascula conectada" | "Scale connected" | "Balança conectada" |
| "La bascula se ha desconectado" | "The scale has been disconnected" | "A balança foi desconectada" |
| "Peso registrado exitosamente" | "Weight registered successfully" | "Peso registrado com sucesso" |
| "Registro masivo creado exitosamente" | "Bulk registration created successfully" | "Registrar em massa criado exitosamente" |
| "¿Quieres finalizar el proceso de registro pesos?" | "Do you want to complete the weight registration process?" | "Você deseja finalizar o processo de registro de pesos?" |

### Matriz de Errores y Soluciones
| Mensaje en la App / Síntoma | Causa Real | Respuesta Sugerida por el Agente | Criterio de Escalamiento Humano |
| :--- | :--- | :--- | :--- |
| "No se encontró ningún animal con el código de chip %1$s." | El código RFID leído con el bastón no corresponde a ninguna orejera asociada a los animales de la finca activa | "El código del chip escaneado no está registrado en el inventario de su finca ganadera. Verifique que el número de arete o transpondedor esté asignado en la hoja de vida del animal o selecciónelo manualmente con el buscador." | Si el usuario confirma que el código está correctamente asociado en la ficha del animal y la app no lo identifica, escalar a soporte técnico indicando el código y la identificación del ejemplar. |
| "La bascula se ha desconectado" | Se interrumpió el enlace Bluetooth con el indicador de pesaje (apagado, batería baja o fuera de rango) | "La comunicación con la báscula se ha perdido. Verifique que el indicador esté encendido, con batería suficiente y a menos de 5 metros del teléfono celular. Luego presione de nuevo el botón 'Báscula' para reanudar la conexión." | Si la báscula está encendida pero el teléfono no logra emparejarla tras reiniciar la app y el Bluetooth del celular, escalar indicando marca y modelo del indicador de pesaje. |
| "No hay pesos para registrar. Por favor, agregue al menos un peso para continuar." | Se presionó el botón "Finalizar" con la tabla de pesajes vacía (sin haber añadido ningún animal con el botón "Agregar") | "Para concluir la jornada de pesaje es necesario registrar al menos un animal en la tabla. Seleccione un animal, confirme su peso y presione el botón 'Agregar' antes de finalizar." | No escalar, validación de flujo de la aplicación. |
| El botón "Agregar" permanece deshabilitado | No se ha seleccionado un animal o el peso ingresado es igual a cero o está vacío | "Para agregar el pesaje a la lista, asegúrese de haber seleccionado un animal y de ingresar un peso mayor a cero en la casilla correspondiente o esperar la estabilización de la báscula." | No escalar, validación de campos obligatorios. |
| El animal no aparece en la lista de selección | El animal ya fue pesado en la sesión actual, está registrado como muerto o pertenece a otra finca | "Si el animal ya fue registrado durante esta misma jornada, el sistema lo oculta automáticamente de la lista para prevenir duplicados. Si aún no lo ha pesado, revise que el animal no se encuentre archivado como baja o dado de baja en el inventario." | Si el animal está activo en el censo pero no figura ni en la tabla ni en la búsqueda, escalar reportando la identificación del animal. |
| "Con tu perfil de %1$s, NO tienes permisos para realizar esta acción." | El colaborador no tiene asignado el permiso de creación de pesos o de conexión Bluetooth en la finca activa | "Su usuario actual no dispone de permisos para registrar pesajes o enlazar dispositivos inalámbricos en esta finca. Pida al propietario o administrador de la finca que le asigne los permisos correspondientes desde la configuración del equipo de trabajo." | No escalar, directiva de control de acceso configurada por el propietario del predio. |
| Mensaje de error general al intentar finalizar | Falla momentánea en la persistencia local de la base de datos | "Espere unos instantes y vuelva a presionar 'Finalizar'. Si el problema continúa, cierre la aplicación por completo y ábrala de nuevo; los pesajes agregados a la sesión permanecen resguardados en el dispositivo." | Si tras reabrir la app persiste el error de finalización, transferir a soporte técnico indicando cantidad de animales pesados y modelo de teléfono. |

### Directivas de Seguridad y Guardrails
- Nunca solicites contraseñas, claves personales, pines ni datos bancarios por los canales de soporte.
- No alteres ni elimines registros históricos de pesajes ni sesiones de lote directamente en bases de datos sin la autorización expresa y documentada del propietario de la finca ganadera.
- Si un usuario reporta diferencias abruptas o biológicamente anómalas en la columna de ganancia diaria o ganancia total de peso, orienta a verificar la calibración de la plataforma de pesaje, la nivelación de las barras de carga y la presencia de suciedad bajo los soportes mecánicos antes de atribuirlo a un fallo del sistema.
- Confirma siempre que el ganadero esté posicionado en la finca y la especie correctas antes de iniciar la jornada de pesaje en manga.
- Recuerda al usuario que todos los pesajes capturados en manga quedan guardados de forma segura en la memoria interna del teléfono y se sincronizarán automáticamente con la nube en cuanto el dispositivo recupere conexión a internet.
