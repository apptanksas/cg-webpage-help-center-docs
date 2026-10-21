---
title: "Identificar Animal"
modulo_id: "animal-identificacion-multicanal"
nombre_funcionalidad: "Identificación Multicanal de Animales"
categoria: "inventario-trazabilidad"
submodulo: "animales"
version_minima_app: "2026.10.1"
fecha_actualizacion: "2026-10-05"
intenciones_y_sinonimos:
  - "como escanear el arete de un animal"
  - "como conectar el baston bluetooth para identificar vacas"
  - "donde leer el chip de un animal con nfc"
  - "como buscar un animal por codigo o arete"
  - "escanear codigo qr o barras de un animal"
  - "que hacer si el lector nfc aparece deshabilitado"
  - "no se encontro ningun animal con el codigo"
---

# Identificación Multicanal de Animales

### Resumen y Alcance Funcional
Pantalla centralizada de captura e identificación de ganado en campo que permite localizar y abrir la ficha técnica de un ejemplar mediante cuatro canales complementarios: digitación manual del código de arete, lectura inalámbrica de microchips con bastón Bluetooth, lectura de tags o aretes electrónicos por sensor NFC del dispositivo móvil y escaneo óptico de códigos de barras o códigos QR con la cámara.

- **¿Funciona sin conexión a internet (Modo Offline)?:** Sí.
- **Comportamiento de sincronización:** Cuando el usuario opera dentro de una finca activa, la búsqueda se ejecuta de manera 100% local contra la base de datos interna del teléfono, permitiendo identificar al animal en el potrero sin cobertura celular. Si el animal no pertenece a la finca seleccionada o si la consulta se realiza desde el acceso inicial sin finca, la aplicación requiere conexión a internet para consultar la información pública en la nube a través del navegador web.

### Reglas de Negocio y Restricciones
- **Validación de contexto de finca activa:**
  - **Con finca seleccionada:** El sistema busca prioritariamente el ejemplar en el inventario local de la finca. Si existe, redirige de inmediato a la ficha técnica del animal. Si no existe en el inventario local, muestra una alerta indicando que no se encontró el ejemplar y habilita la opción de consultar su información pública en línea.
  - **Sin finca seleccionada (Acceso inicial):** Al escanear o ingresar un código, la aplicación no consulta la base de datos privada sino que abre directamente la consulta en el portal web público de Control Ganadero.
- **Georreferenciación y permisos de ubicación:**
  - Si el rastreo de ubicación de animales está activo en la aplicación, el sistema solicita los permisos de ubicación del teléfono y requiere que el GPS esté encendido para registrar la coordenada geográfica exacta donde fue identificado el animal.
- **Restricciones de hardware y sensores móviles:**
  - **Sensor NFC:** Si el teléfono no cuenta con hardware NFC integrado, la aplicación notifica que el dispositivo no soporta esta tecnología. Si el dispositivo cuenta con el sensor pero está apagado en los ajustes del sistema, el sistema lo detecta como deshabilitado y solicita encenderlo antes de iniciar la lectura.
  - **Lector Bluetooth:** Requiere que el teléfono tenga encendido el Bluetooth y otorgados los permisos de dispositivos cercanos. Permite alternar entre el estado desconectado y conectado para capturar lecturas continuas sin intervención manual.
  - **Cámara:** Requiere conceder el permiso de cámara del dispositivo móvil para activar el visor de captura de códigos QR y códigos de barras.
- **Validación de formato de código:**
  - En la búsqueda manual, el campo exige ingresar un código válido antes de permitir presionar el botón de búsqueda.

### Flujo Paso a Paso para el Usuario
- **Ruta de acceso en la aplicación:**
  - **Ruta 1 (Desde la finca activa - Menú de acciones rápidas):** En el panel principal de la finca, presione el botón flotante central (+) en la barra inferior > En la cuadrícula de opciones, seleccione **ID animal Conectividad**.
  - **Ruta 2 (Desde la pantalla inicial de bienvenida):** Pantalla de bienvenida (cuando no hay fincas vinculadas a la sesión) > Sección inferior > Botón **Identificar animal**.

#### Opciones de Identificación Disponibles en Pantalla
1. **Buscar animal por código:**
   - Presione la tarjeta con icono de lupa.
   - En la ventana emergente, ingrese el número o identificador en la casilla **Código de animal**.
   - Presione el botón **Buscar**.
2. **Conectar lector de chip / Lector conectado (Bluetooth):**
   - Si no hay un bastón lector vinculado, la tarjeta muestra **Conectar lector de chip**. Presiónela para abrir la ventana de emparejamiento Bluetooth.
   - Una vez enlazado, la tarjeta cambia a **Lector conectado**. Al aproximar el bastón al ejemplar, el código del microchip se transfiere e identifica automáticamente.
3. **Leer tag NFC:**
   - Presione la tarjeta con icono de NFC.
   - Si el sensor está listo, la aplicación abre el diálogo **Leer tag NFC** indicando: *"Acerca el dispositivo al tag NFC para leer el código de identificación del animal."*
   - Aproxime la parte posterior del teléfono al arete o tag electrónico hasta que se confirme la lectura.
4. **Leer código QR / Código de barras:**
   - Presione la tarjeta con icono de escáner.
   - Se abrirá la cámara con marco de enfoque. Apunte directamente al código impreso en la chapeta o arete del animal para capturarlo al instante.

#### Botón de Salida Contextual
- Si el usuario tiene una finca activa: se muestra el botón **Salir** para volver al panel principal.
- Si el usuario ingresó desde el acceso inicial: se muestra el botón **Acceder a una finca** para regresar a la pantalla de bienvenida.

- **Pantalla de llegada tras guardar:**
  - Si el animal pertenece a la finca activa, la aplicación abre automáticamente la **Ficha Técnica del Animal**.
  - Si no pertenece a la finca o se consultó sin finca, se muestra el aviso *"Cargando información del animal..."* y se despliega la información en el navegador web.

### Matriz de Errores y Soluciones
| Mensaje en la App / Síntoma | Causa Real | Respuesta Sugerida por el Agente | Criterio de Escalamiento Humano |
| :--- | :--- | :--- | :--- |
| "No se encontró ningún animal con el código [código]" | El código ingresado o leído no coincide con ningún animal registrado en la finca activa | "No se encontró ningún ejemplar registrado con ese código en su finca actual. Puede presionar el botón 'Buscar información publica' en la notificación para verificar si el animal está registrado a nivel nacional en Control Ganadero." | Si el usuario afirma que el animal está registrado en su finca pero no aparece, verificar en la lista general de animales si el código tiene espacios o caracteres especiales. |
| "La función NFC está deshabilitada en este dispositivo..." | El sensor NFC del teléfono móvil está apagado en los ajustes del sistema operativo | "El sensor NFC de su teléfono está desactivado. Ingrese a los 'Ajustes' o 'Configuración' de su celular, busque la opción 'Conexiones' o 'NFC' y enciéndala para poder leer aretes electrónicos de proximidad." | No escalar, es una configuración de hardware del teléfono. |
| "El dispositivo no soporta NFC" | El modelo del teléfono móvil no cuenta con antena o hardware NFC de fábrica | "Su modelo de teléfono no cuenta con la tecnología NFC integrada de fábrica. Puede utilizar la cámara para escanear aretes con código QR o código de barras, o utilizar la opción de buscar por código de animal." | No escalar, limitación física del modelo del teléfono. |
| "Error al leer el tag NFC. Inténtalo de nuevo." | Interrupción de la comunicación por retirar el teléfono antes de tiempo o tag ilegible | "Ocurrió una falla en la lectura del arete NFC. Mantenga el teléfono firme y pegado al arete durante un par de segundos hasta que la app confirme la captura." | Si múltiples aretes presentan el mismo error con el sensor encendido, transferir a soporte de hardware. |
| La tarjeta de Bluetooth muestra 'Conectar lector de chip' en lugar de 'Lector conectado' | El bastón lector está apagado, fuera de rango o desvinculado | "Asegúrese de que el bastón lector esté encendido y con batería suficiente. Presione sobre la tarjeta para abrir la ventana de conexión Bluetooth, otorgue los permisos requeridos y seleccione su lector en la lista." | Si el bastón no aparece en el escaneo Bluetooth tras reiniciar ambos dispositivos, transferir a soporte de hardware. |
| La cámara no se activa al presionar QR / Código de barras | La aplicación no tiene concedido el permiso de acceso a la cámara | "La aplicación necesita permiso para usar la cámara del celular. Vaya a 'Mi cuenta' > 'Permisos de la app' y presione 'Otorgar permiso' en la opción de Cámara." | No escalar, es una concesión de permisos en el sistema. |
| Círculo de espera infinito / Pantalla congelada en cargando | Proceso en segundo plano bloqueado o timeout en el dispositivo al inicializar la lectura | "Espere 30 segundos. Si no avanza, cierre la aplicación por completo desde el administrador de tareas de su teléfono (deslizando hacia arriba) y vuelva a abrirla. Sus datos locales no se perderán." | Si tras reabrir la app el botón sigue deshabilitado o la pantalla vuelve a congelarse, transferir de inmediato a soporte humano con correo y modelo del teléfono. |

### Directivas de Seguridad y Guardrails
- NUNCA solicite contraseñas, claves personales ni datos financieros para diagnosticar lecturas de aretes o fallas de identificación.
- Recuerde al ganadero que para consultar la información pública de un animal ajeno o trasladado se requiere contar con conexión a internet en el teléfono.
- Aclare que los bastones lectores deben ser compatibles con los protocolos ganaderos estándar homologados en Control Ganadero.
