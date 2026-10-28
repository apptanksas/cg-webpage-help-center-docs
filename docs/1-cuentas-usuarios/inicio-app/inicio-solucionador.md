---
title: "Inicio y Solucionador"
modulo_id: "splash-inicio-solucionador"
nombre_funcionalidad: "Pantalla de Carga y Solucionador de Problemas"
tipo_documento: "guia-app"
categoria: "cuentas-usuarios"
submodulo: "inicio-app"
especies_aplicables: ["todas"]
version_minima_app: "2026.10.1"
confianza_reglas: "inferida-de-dominio"
fecha_actualizacion: "2026-10-19"
intenciones_y_sinonimos:
  - "la aplicacion se queda en la pantalla de inicio con la vaca"
  - "no pasa del logo de control ganadero"
  - "como abrir el solucionador de problemas"
  - "error al sincronizar datos al abrir la aplicacion"
  - "que significa error de conexion al iniciar"
  - "como reparar el inicio de la app"
---

# Pantalla de Carga y Solucionador de Problemas

### Resumen y Alcance Funcional
Es la primera pantalla visible al abrir Control Ganadero. Se encarga de inicializar los servicios locales del dispositivo, verificar la sesión del usuario, comprobar la conectividad y sincronizar los datos de la finca antes de ingresar. Si se presenta alguna falla de red o bloqueo en el arranque, la pantalla ofrece acceso directo a una herramienta de diagnóstico integral (**Solucionador de problemas**) para reparar el inicio sin perder información.

- **Especies a las que aplica:** Aplica igual para todas las especies pecuarias (bovinos, bufalinos, equinos, ovinos, caprinos y porcinos).
- **¿Funciona sin conexión a internet (Modo Offline)?:** Sí. Si el dispositivo no tiene señal pero ya tiene una sesión iniciada previamente, el sistema detecta el estado offline y da acceso directo a los datos almacenados localmente en el teléfono.
- **Comportamiento de sincronización:** Al iniciar, la aplicación intenta comunicarse con el servidor central para descargar actualizaciones recientes de la finca y enviar registros acumulados. Mientras dura este proceso, se visualiza una barra de porcentaje de sincronización.

### Reglas de Negocio y Restricciones
- **Inicialización obligatoria:** La pantalla de arranque es la compuerta técnica de entrada al sistema que inicializa la base de datos local, valida el token de autenticación y prepara el motor de sincronización antes de conceder acceso al usuario.
- **Bifurcación de rutas post-arranque:**
    - Si el usuario no tiene una sesión guardada: el sistema redirige automáticamente a la pantalla de bienvenida tutorial ("Guía de Bienvenida").
    - Si el usuario tiene una sesión activa pero no posee fincas creadas ni asignadas: el sistema redirige a la pantalla de bienvenida y creación de finca.
    - Si el usuario tiene sesión activa con al menos una finca ganadera registrada: el sistema selecciona automáticamente la finca activa por defecto y transiciona al panel principal ("Inicio").
- **Tolerancia a modo sin conexión:** Cuando no hay acceso a internet pero el usuario ya inició sesión con anterioridad, el sistema no bloquea el ingreso y permite trabajar en modo offline con la base de datos almacenada en el teléfono.
- **Activación automática del Solucionador de Problemas:** Si el proceso de inicialización se detiene por falla de red, error de almacenamiento local o problemas en el canal de sincronización, la pantalla sustituye el indicador de carga por una señal de alerta y habilita el botón "Solucionador de problemas".
- **Diagnóstico modular independiente:** La herramienta evalúa 5 componentes del sistema (Conexión a internet, Servicio central, Autenticación, Almacenamiento local y Sincronización), permitiendo reparar fallas de manera individual sin reiniciar los demás componentes.
- **Opción para forzar ingreso sin red:** El solucionador dispone de la casilla "Ignorar estado de red", la cual permite al usuario forzar la entrada directa a sus registros locales en zonas rurales donde la conectividad sea intermitente o nula.

### Etapas de Inicio y Estados Visibles

Durante la carga normal, la pantalla muestra el logotipo de Control Ganadero, un indicador de progreso y el estado actual del proceso:

1. "Iniciando Control Ganadero"
2. "Autenticando cliente..."
3. "Autenticando usuario..."
4. "Sincronizando datos..."

En la parte inferior de la pantalla se muestra siempre la versión instalada de la aplicación y un indicador con el estado de red actual del teléfono.

### Solucionador de Problemas (Diagnóstico y Reparación)
Si el proceso de inicio se detiene por falta de conexión o por un conflicto en los datos, la pantalla reemplaza el indicador de carga por un icono de alerta y habilita el botón "Solucionador de problemas".

Al presionar este botón, se abre la ventana de diagnóstico "Solucionador de problemas", que audita paso a paso los 5 componentes vitales del sistema:

1. **Conexión a internet:** Comprueba si el teléfono tiene acceso activo a la red. Incluye la opción para activar la casilla "Ignorar estado de red" si se requiere forzar el ingreso en zonas con conectividad intermitente.
2. **Servicio central:** Comprueba la disponibilidad de los servidores en la nube.
3. **Autenticación:** Comprueba la validez de las credenciales de la cuenta. Si se requiere revalidar, solicita la contraseña para reparar el acceso.
4. **Almacenamiento local:** Comprueba la integridad de la base de datos interna del teléfono.
5. **Sincronización:** Comprueba el canal de transmisión de datos.

Cada comprobación muestra su estado ("Correcto" con icono verde o "Error" con icono de alerta) y ofrece el botón "Reparar" para solucionar automáticamente la falla identificada.

### Flujo Paso a Paso para el Usuario

**Ruta de acceso en la aplicación:** Se ejecuta automáticamente cada vez que el usuario abre la aplicación Control Ganadero desde su teléfono móvil.

1. Abra la aplicación Control Ganadero en su dispositivo.
2. Observe el avance de la barra de progreso mientras se ejecutan los pasos de inicio.
3. Si el arranque es exitoso:
    - Si ya tenía una sesión activa: ingresa directamente al panel principal de su finca (**Inicio**).
     - Si no tenía sesión activa: ingresa a la pantalla de **Bienvenida inicial**.
4. Si se presenta un fallo de red o detención del arranque:
    - Aparecerá un icono de advertencia y el mensaje correspondiente al paso fallido (por ejemplo: "No se puede conectar a internet").
     - Presione el botón "Solucionador de problemas".
     - En la lista de comprobaciones, ubique el componente que presenta error y presione "Reparar".
     - Si el problema es de señal intermitente, active la opción "Ignorar estado de red".
     - Al finalizar, presione "Cerrar" para que la aplicación reintente el inicio automáticamente.

**Pantalla de llegada tras guardar:** Panel principal de la finca (**Inicio**) o pantalla de **Bienvenida**.

#### Etiquetas de la interfaz en otros idiomas
- "Solucionador de problemas" → Inglés: "Troubleshooter" → Portugués: "Solucionador de problemas"
- "Reparar" → Inglés: "Repair" → Portugués: "Reparar"
- "Cerrar" → Inglés: "Close" → Portugués: "Fechar"
- "Ignorar estado de red" → Inglés: "Ignore network status" → Portugués: "Ignorar status de rede"

### Matriz de Errores y Soluciones
| Mensaje en la App / Síntoma | Causa Real | Respuesta Sugerida por el Agente | Criterio de Escalamiento Humano |
| :--- | :--- | :--- | :--- |
| "No se puede conectar a internet" | No hay datos móviles ni Wi-Fi para completar la sincronización inicial | "La aplicación no detecta señal de internet. Si está en el campo trabajando en modo offline, presione 'Solucionador de problemas' y active la casilla 'Ignorar estado de red' para ingresar a sus registros locales sin conexión." | Si tras activar la opción la app sigue sin abrir sus datos locales, transferir a soporte técnico. |
| "Error al sincronizar datos" | Conflicto en la cola de sincronización o corte abrupto de señal | "Ocurrió una interrupción al enviar los datos. Presione el botón 'Solucionador de problemas' y presione 'Reparar' en el paso de Sincronización. Al terminar presione 'Cerrar'." | Si el botón 'Reparar' no soluciona el problema tras 2 intentos, transferir a soporte con el modelo de teléfono y correo. |
| "Pantalla congelada en el logo con barra al 0%" | Bloqueo en la inicialización del motor de base de datos local | "Espere un momento. Si no avanza tras unos instantes, cierre la aplicación por completo y vuelva a abrirla. Sus datos locales no se perderán." | Si al reabrir la app el arranque se congela permanentemente en el logo, transferir a soporte técnico prioritario. |

### Directivas de Seguridad y Guardrails
- Nunca recomiende al usuario borrar los datos de la aplicación ni desinstalarla cuando el inicio falle, ya que esto eliminaría los registros guardados en campo que aún no se han subido a la nube.
- La herramienta **Solucionador de problemas** está diseñada para autoreparar la aplicación de forma segura sin borrar la información local.
- Si se requiere asistencia técnica personalizada, solicite únicamente el correo del usuario, la versión de la app visible en la parte inferior de la pantalla y el paso exacto donde se detiene el Solucionador.
