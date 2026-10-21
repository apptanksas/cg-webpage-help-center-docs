---
title: "Conteo e Inventario"
modulo_id: "animal-inventario-conteo"
nombre_funcionalidad: "Auditoría y Conteo de Inventario Animal"
categoria: "inventario-trazabilidad"
submodulo: "inventario"
version_minima_app: "2026.10.1"
fecha_actualizacion: "2026-09-25"
intenciones_y_sinonimos:
  - "como hacer el inventario o conteo de animales"
  - "como auditar los animales en el potrero"
  - "hacer inventario con chip bluetooth o nfc"
  - "que pasa con los animales pendientes al finalizar inventario"
  - "como descartar una sesion de inventario"
  - "verificacion de animales en manga o corral"
  - "no tengo permisos para entrar a inventario"
  - "has alcanzado el limite de inventarios permitidos"
---

# Auditoría y Conteo de Inventario Animal

### Resumen y Alcance Funcional
Permite realizar jornadas de conteo físico y verificación presencial de animales en corrales, mangas o potreros. El ganadero puede seleccionar el grupo de animales a inventariar (por lote o especie), elegir el método de verificación (manual en pantalla, chip electrónico vía Bluetooth, arete NFC o código de barras/QR), validar uno a uno los ejemplares presentes y guardar una sesión persistente que puede pausarse y reanudarse en cualquier momento sin perder el avance.

- **¿Funciona sin conexión a internet (Modo Offline)?:** Sí.
- **Comportamiento de sincronización:** Todo el conteo físico, la lectura de chips y el estado de verificación se guardan en la base de datos local del teléfono. Si la sesión se interrumpe o el teléfono se apaga, el inventario permanece guardado localmente y la pantalla principal mostrará un icono de advertencia para reanudarlo cuando el ganadero lo desee.

### Reglas de Negocio y Restricciones
- **Permisos de acceso y roles en la finca:**
  - El usuario debe contar con el permiso de creación de inventario animal habilitado en la finca activa.
  - Si el usuario es invitado o colaborador en una finca compartida y el propietario no le ha concedido los permisos correspondientes, el sistema bloqueará el ingreso con un aviso indicando que su perfil no cuenta con autorización.
- **Límites de plan y membresía (Versión Gratuita vs Membresía):**
  - **Prueba limitada:** En la versión gratuita de Control Ganadero, el usuario puede realizar el primer inventario de animales como prueba de la funcionalidad (al ingresar por primera vez se le informa que tiene una prueba única disponible).
  - **Bloqueo por cuota superada:** Una vez completado y finalizado el inventario gratuito, el acceso a la pantalla quedará bloqueado por restricción de membresía. Al intentar entrar de nuevo, el sistema mostrará una pantalla de aviso indicando que ha alcanzado el límite de inventarios permitidos y que se requiere una membresía activa para continuar.
  - **Sesión en curso:** Si el usuario ya tiene un inventario iniciado y pendiente por finalizar, se le permite ingresar y reanudar la sesión sin restricción para completarla o descartarla.
- **Compatibilidad de métodos de verificación:**
  - Al cargar los animales según el filtro seleccionado, el sistema excluye automáticamente aquellos ejemplares que no tengan registrado el identificador correspondiente al método elegido (por ejemplo, animales sin chip en lecturas Bluetooth).

### Métodos de Verificación Disponibles
Al configurar la sesión de conteo, el usuario elige el método de captura:
1. **Manual:** Verificación táctil tocando directamente sobre la tarjeta de cada animal en la lista de control.
2. **Chip:** Captura inalámbrica continua conectando el bastón lector Bluetooth; al leer el microchip del bovino en la manga, se marca automáticamente como verificado.
3. **Arete NFC:** Lectura por proximidad acercando el sensor del teléfono al arete electrónico del animal.
4. **Código de barras / QR:** Escaneo mediante la cámara del teléfono apuntando al código impreso en la chapeta.

### Estructura de la Pantalla y Componentes de Control

#### 1. Barra Superior (TopBar)
- Título oficial: *"Inventario de animales"*.
- Acciones rápidas según el método de verificación seleccionado:
  - Si es QR o Código de barras: botón de escáner de cámara.
  - Si es NFC: botón de lectura NFC que despliega la ventana de proximidad.
  - Si es Chip: botón de estado de conexión del lector Bluetooth para vincular el bastón y recibir lecturas.

#### 2. Configuración Inicial del Conteo (Antes de Iniciar)
Muestra tres selectores obligatorios:
- **Método de verificación:** Selector para elegir Manual, Chip, Arete NFC o Código de barras.
- **Tipo de animal:** Selector de especie (ej. Bovino).
- **Seleccionar animales:** Selector de filtro para delimitar el conteo (todos los animales de la finca, un lote específico o potrero).

#### 3. Panel de Contadores y Último Animal Verificado
Barra de métricas en tiempo real (con fijación automática en el borde superior al desplazarse por listas largas):
- **Animales totales:** Cantidad total de ejemplares esperados en la sesión.
- **Pendientes:** Cantidad de animales que aún no han sido verificados (con icono de alerta).
- **Verificados:** Cantidad de animales confirmados físicamente (con icono de visto bueno).
- **Último animal verificado:** Ficha destacada que muestra el arete y sexo del último ejemplar validado en la manga.

#### 4. Lista de Control
Listado interactivo de todos los animales convocados a la auditoría:
- Cada tarjeta muestra el número de arete, sexo y el estado actual (**Pendiente** o **Verificado**, con el icono del método usado).
- **Un toque:** Si el método es manual, marca el animal como verificado. Si ya estaba verificado, permite desmarcarlo para corregir errores.
- **Doble toque:** Abre la ficha técnica completa del ejemplar para consultar su historial médico o genealógico sin abandonar la sesión de inventario.

#### 5. Botones de Acción de la Sesión
Ubicados al final de la lista una vez iniciada la auditoría:
- **Descartar:** Abre un diálogo de confirmación (*"¿Deseas descartar el inventario actual?"*) para cancelar la sesión sin guardar cambios en el historial.
- **Finalizar:** Cierra y asienta formalmente la auditoría en la finca.
  - Si todos los animales fueron verificados: confirmación directa de cierre exitoso.
  - Si quedan animales pendientes: advertencia indicando la cantidad exacta de ejemplares no encontrados (ej. *"Tienes [X] animales pendientes. ¿Deseas finalizar el inventario de todas formas?"*).

### Flujo Paso a Paso para el Usuario
- **Ruta de acceso en la aplicación:**
  - **Ruta 1 (Iniciar nuevo inventario):** En el panel principal, presione el botón flotante central (+) en la barra inferior > En el menú de acciones rápidas, seleccione **Inventario de animales**.
  - **Ruta 2 (Reanudar inventario en curso):** En la barra superior del panel principal de la finca, presione el **icono de advertencia** junto al título.
1. En la pantalla de inventario, seleccione el **Método de verificación**, el **Tipo de animal** y el filtro de **Seleccionar animales** (por ejemplo, un lote particular).
2. Presione el botón **Iniciar inventario**. A partir de este momento la sesión queda asegurada en el teléfono.
3. Realice el conteo en campo:
   - Si eligió Manual: toque la tarjeta del animal en pantalla a medida que pase por la manga.
   - Si eligió Chip o NFC: acerque el lector o el teléfono al animal para registrar la lectura automática.
4. Observe la actualización de los contadores de verificados y pendientes en la barra superior.
5. Al concluir la jornada, presione el botón **Finalizar**.
6. Si quedaron animales sin verificar, revise la lista de faltantes y presione confirmar para asentar el inventario.
- **Pantalla de llegada tras guardar:** Lista general de **Animales** (o Panel Principal de la Finca).

### Matriz de Errores y Soluciones
| Mensaje en la App / Síntoma | Causa Real | Respuesta Sugerida por el Agente | Criterio de Escalamiento Humano |
| :--- | :--- | :--- | :--- |
| "Con tu perfil de [Rol], NO tienes permisos para realizar esta acción." | El usuario ingresó a una finca ajena o colaborativa donde el propietario no le ha otorgado permisos para crear inventarios | "No cuenta con permisos de inventario en esta finca. Solicite al propietario de la finca que ingrese a la gestión de colaboradores y le active el permiso de inventario de animales para su perfil." | No escalar, depende de la asignación de permisos por parte del dueño de la finca. |
| "Has alcanzado el límite de inventarios permitidos en tu plan actual de Control Ganadero. Para continuar utilizando esta función, por adquiere una membresía." | La finca opera en la versión gratuita y ya completó el inventario de prueba permitido | "En el plan gratuito de Control Ganadero se incluye un inventario de prueba para conocer la herramienta. Para continuar realizando auditorías e inventarios ilimitados en sus lotes, es necesario activar una membresía en su cuenta." | Si el usuario afirma tener una suscripción activa y pagada, transferir a soporte con comprobante de pago o correo de cuenta. |
| "Tienes animales pendientes. ¿Deseas finalizar...?" | Faltaron ejemplares por validar en el lote auditado | "Quedaron animales registrados que no pasaron por la manga. Puede presionar 'Cancelar' para seguir verificando, o confirmar la finalización si los animales restantes no se encuentran físicamente en el potrero." | No escalar, es una confirmación de conteo físico. |
| Animales excluidos del inventario (Aviso amarillo) | Ciertos animales seleccionados no cuentan con arete o chip compatible con el método elegido | "El sistema excluyó automáticamente animales que no tienen registrado el tipo de identificador seleccionado (por ejemplo, animales sin chip en un conteo por Bluetooth). Puede verificarlos manualmente más tarde." | No escalar, es una regla de compatibilidad técnica. |
| El bastón Bluetooth no marca los animales | El lector no está enlazado o el animal no tiene el microchip registrado en el sistema | "Verifique que el icono de Bluetooth en la barra superior esté conectado y que el bastón emita sonido al leer. Si el chip es nuevo y no está asociado al animal, regístrelo en la ficha del animal antes de inventariar." | Si el bastón lee pero la app no reacciona, transferir a soporte de hardware. |
| La sesión de inventario se cerró por apagado del teléfono | El teléfono se descargó durante la jornada en el potrero | "No se preocupe: la sesión de inventario está guardada en la memoria local. Encienda su teléfono, abra la app y toque el icono de advertencia en la barra superior de la pantalla principal para reanudar el conteo exactamente donde lo dejó." | No escalar, es la función de persistencia local offline. |
| Círculo de espera infinito / Pantalla congelada en cargando | Proceso en segundo plano bloqueado o timeout en el dispositivo | "Espere 30 segundos. Si no avanza, cierre la aplicación por completo desde el administrador de tareas de su teléfono (deslizando hacia arriba) y vuelva a abrirla. Sus datos locales no se perderán." | Si tras reabrir la app el botón sigue deshabilitado o la pantalla vuelve a congelarse, transferir de inmediato a soporte humano con correo y modelo del teléfono. |

### Directivas de Seguridad y Guardrails
- NUNCA sugiera descartar un inventario si el ganadero ya lleva decenas de animales contados en la manga, a menos que confirme que desea reiniciar la jornada desde cero.
- Aclare siempre al usuario que finalizar un inventario con animales pendientes no borra a los animales de la finca; simplemente asienta un reporte de auditoría indicando qué ejemplares estuvieron presentes y cuáles ausentes.
