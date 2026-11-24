---
title: "Sincronización de Finca"
modulo_id: "sincronizacion-finca"
nombre_funcionalidad: "Sincronización de Datos desde la Pantalla de la Finca"
tipo_documento: "guia-app"
categoria: "sincronizacion-reportes"
submodulo: "sincronizacion"
especies_aplicables: ["todas"]
version_minima_app: "2026.5.0"
confianza_reglas: "verificada-con-tests"
fecha_actualizacion: "2026-11-24"
intenciones_y_sinonimos:
  - "como sincronizar los datos de mi finca con el servidor"
  - "por que me sale el mensaje tienes datos pendientes en la pantalla de la finca"
  - "que significa el icono de sincronizacion en la barra superior"
  - "como subir los registros guardados sin conexion a internet"
  - "error al sincronizar se ha excedido el numero maximo de animales permitidos"
  - "que hacer si la sincronizacion se queda cargando en el inicio"
---

# Sincronización de Datos desde la Pantalla de la Finca

### Resumen y Alcance Funcional
Mecanismo central de conciliación y actualización de datos que opera directamente desde el panel principal de la finca. Esta funcionalidad permite al productor ganadero, administradores y trabajadores mantener sincronizada la información local del teléfono móvil con los servidores de Control Ganadero, asegurando que todos los registros de animales, pesajes, eventos sanitarios, tareas y traslados efectuados en campo se respalden en la nube y estén disponibles para todos los integrantes autorizados de la explotación.

- **Especies a las que aplica:** Aplica igual para todas las especies (bovinos, equinos, bufalinos, caprinos, ovinos y porcinos).
- **¿Funciona sin conexión a internet (Modo Offline)?:** Parcialmente. Los registros de la finca se pueden consultar, crear y modificar en el teléfono sin conexión a internet; sin embargo, el proceso de sincronización con los servidores remotos requiere obligatoriamente una conexión de red activa (Wi-Fi o datos móviles).
- **Comportamiento de sincronización:** Los registros ingresados sin señal permanecen resguardados de forma segura en la base de datos local del teléfono. Al recuperar la conectividad o presionar manualmente la acción de sincronizar, la aplicación envía los registros locales pendientes hacia la nube y descarga las modificaciones más recientes efectuadas por otros miembros de la finca.
- **Plataformas:** Funciona igual en Android y en iOS. En ambos sistemas operativos el proceso se ejecuta como tarea prioritaria para evitar que el sistema detenga la subida de datos si el usuario minimiza temporalmente la aplicación.

### Reglas de Negocio y Restricciones
- **Verificación automática al ingresar a la finca:** Al entrar a la pantalla principal de la finca, el sistema comprueba de forma autónoma si existen cambios pendientes de sincronizar en la base de datos local o si ya hay un proceso de sincronización en ejecución.
- **Detección dinámica de red:** La pantalla monitorea en segundo plano el estado de la conexión a internet. Si el dispositivo recupera la señal, la interfaz reevalúa automáticamente el estado de los datos locales sin necesidad de reiniciar la aplicación.
- **Estados visuales del proceso de sincronización:**
    - **Completado:** Indica que todos los datos registrados en el teléfono están respaldados en la nube y no existen operaciones locales pendientes. Se identifica con un icono verde de verificación.
    - **Pendiente:** Señala que existen registros nuevos o editados guardados en el teléfono que aún no han subido al servidor. Muestra un icono de advertencia y despliega la barra interactiva amarilla.
    - **En progreso:** Indica que el motor de sincronización está comunicándose activamente con los servidores para transferir datos. Muestra un indicador circular de carga en movimiento continuo.
    - **Sin internet:** Indica que se intentó iniciar una sincronización pero el dispositivo carece de conexión de datos activa.
    - **Error:** Señala una interrupción o fallo inesperado durante la comunicación con el servidor.
- **Interacción con el Modo Offline:** Si el usuario tiene habilitado el Modo Offline en sus ajustes y presiona la acción para sincronizar, la aplicación no inicia la sincronización de inmediato; en su lugar, presenta un diálogo modal para solicitarle desactivar el modo sin conexión antes de proceder.
- **Control de límites y cuotas de suscripción:** Si la cuenta excede el número máximo de animales o de fincas permitidas por el plan de suscripción contratado, el sistema interrumpe la sincronización y muestra una notificación superior específica alertando sobre la restricción.
- **Protección contra duplicidad:** El sistema previene ejecuciones simultáneas. Si ya existe una sincronización en marcha, cualquier intento adicional se acopla al proceso en curso sin duplicar solicitudes de red.

### Flujo Paso a Paso para el Usuario
- **Ruta de acceso en la aplicación:**
    - Menú lateral o pantalla de selección de fincas > Seleccionar la finca deseada > Pantalla principal de la finca (panel de inicio).

#### 1. Verificación del Estado en la Barra Superior
1. Al ingresar a la finca seleccionada, observe la barra de estado ubicada inmediatamente debajo del calendario horizontal de actividades.
2. A la derecha de la etiqueta "Sincronización:", revise el icono de estado:
    - Si observa el icono verde de verificación, la información está al día ("Completado").
    - Si observa el icono de advertencia, existen datos guardados en el teléfono pendientes de subir a la nube ("Pendiente").
    - Si observa un círculo girando, la aplicación está transfiriendo datos en ese instante ("Sincronizando").

#### 2. Sincronización Manual ante Datos Pendientes
1. Si el estado es pendiente, aparecerá una barra horizontal de color amarillo sobre el contenido de la pantalla con el mensaje "Tienes datos pendientes.".
2. Presione sobre el texto de acción "Sincronizar" ubicado al costado derecho de la barra amarilla.
3. Si el Modo Offline se encuentra activado, la aplicación mostrará la ventana emergente "Modo sin conexión detectado ¿Quieres desactivarlo?". Desactive el interruptor para continuar.
4. El icono de la barra superior cambiará a un indicador circular de carga y el sistema procesará la subida de los registros de la finca.
5. Al finalizar con éxito, la barra amarilla desaparece automáticamente y el icono de estado cambia al icono verde de verificación.

- **Pantalla de llegada tras guardar:** El usuario permanece en la pantalla principal de la finca, con la información y resúmenes de animales, pesajes y actividades actualizados con los datos de la nube.

#### Variaciones por especie
Aplica igual para todas las especies. El motor de sincronización procesa los registros de bovinos, equinos, bufalinos, caprinos, ovinos y porcinos bajo las mismas reglas y formatos de base de datos.

#### Etiquetas de la interfaz en otros idiomas
- "Sincronización" → Inglés: "Synchronization" → Portugués: "Sincronização"
- "Completado" → Inglés: "Complete" → Portugués: "Completo"
- "Pendiente" → Inglés: "Pending" → Portugués: "Pendente"
- "Sincronizar" → Inglés: "Synchronize" → Portugués: "Sincronizar"
- "Tienes datos pendientes." → Inglés: "You have pending data." → Portugués: "Você tem dados pendentes."
- "Sin internet" → Inglés: "No internet" → Portugués: "Sem internet"

### Matriz de Errores y Soluciones
| Mensaje en la App / Síntoma | Causa Real | Respuesta Sugerida por el Agente | Criterio de Escalamiento Humano |
| :--- | :--- | :--- | :--- |
| "Tienes datos pendientes." | Existen registros almacenados en el teléfono que no se han transmitido al servidor por falta de conectividad o sincronización manual previa. | "Este aviso le indica que tiene registros guardados en su teléfono que aún no se han subido a la nube. Para respaldarlos, asegúrese de tener conexión a internet y pulse sobre el botón 'Sincronizar' en la barra amarilla." | No requiere escalamiento; es un aviso informativo ordinario del sistema fuera de línea. |
| "No se pudo sincronizar la información porque se ha excedido el número máximo de animales permitidos en la suscripción actual." | La finca superó el límite de animales autorizados según el plan de suscripción activo. | "La sincronización no pudo completarse porque la cantidad de animales en su finca supera el cupo de su plan actual. Para continuar sincronizando nuevos animales, es necesario actualizar o ampliar su plan de suscripción desde nuestra plataforma." | Escalar a soporte comercial si el usuario ya realizó el pago de ampliación de cupo y el sistema no lo reconoce. |
| "No se pudo sincronizar la información porque se ha excedido el número máximo de fincas permitidas en la suscripción currente." | El usuario sobrepasó la cantidad máxima de fincas asignadas a su cuenta de usuario. | "La sincronización se detuvo porque ha alcanzado el límite de fincas permitidas para su cuenta. Puede acceder a nuestra plataforma web en la sección de complementos de su cuenta para adquirir fincas adicionales." | Escalar a soporte comercial si el usuario cuenta con fincas adicionales contratadas activas. |
| Icono de desconexión / Estado "Sin internet" | El teléfono móvil no dispone de conexión de datos móviles ni señal Wi-Fi activa al intentar sincronizar. | "No se detecta conexión a internet en su dispositivo. Sus datos continúan guardados de forma segura en el teléfono. Verifique que sus datos móviles o red Wi-Fi estén activos y vuelva a presionar 'Sincronizar'." | Si el dispositivo navega con normalidad en otras aplicaciones pero la app no detecta red tras varios intentos, transferir a soporte técnico. |
| "Modo sin conexión detectado ¿Quieres desactivarlo?" | El usuario intentó sincronizar teniendo activada la preferencia de modo fuera de línea en los ajustes de la app. | "Tiene activado el modo sin conexión en la aplicación. Para permitir que los datos se suban al servidor, confirme la desactivación del modo sin conexión en la ventana emergente y presione nuevamente 'Sincronizar'." | No requiere escalamiento; comportamiento previsto de la configuración de usuario. |
| Círculo de espera continuo en el estado de sincronización | La aplicación está transmitiendo un volumen elevado de registros o la conexión de red experimenta intermitencia. | "El sistema está transfiriendo los registros pendientes con el servidor; espere un momento mientras finaliza el proceso. Sus datos guardados en el dispositivo no se pierden. Si el proceso no avanza después de varios minutos, cierre la aplicación por completo y vuelva a abrirla." | Transferir a soporte técnico si tras reiniciar la aplicación la sincronización permanece bloqueada indefinidamente. |

### Directivas de Seguridad y Guardrails
- Nunca pida contraseñas, números de tarjeta de crédito ni códigos de verificación por el chat de soporte.
- Nunca sugiera desinstalar la aplicación ni borrar el almacenamiento de la app si el usuario tiene el aviso "Tienes datos pendientes.", ya que los datos locales que no se han subido a la nube se perderían irremediablemente.
- Verifique siempre que el usuario se encuentre en la finca correspondiente antes de evaluar errores de sincronización o discrepancias de inventario.
- Los datos guardados de forma local en el dispositivo están resguardados; tranquilice al productor informándole que la falta de sincronización temporal no borra su trabajo de campo.
