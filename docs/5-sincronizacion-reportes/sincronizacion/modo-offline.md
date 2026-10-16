---
title: "Sincronización de Datos"
modulo_id: "sync-modo-offline"
nombre_funcionalidad: "Trabajo en Campo Sin Internet y Sincronización Automática"
categoria: "sincronizacion-reportes"
submodulo: "sincronizacion"
version_minima_app: "2.4"
fecha_actualizacion: "2026-09-25"
intenciones_y_sinonimos:
  - "como funciona la aplicacion sin senal en el potrero"
  - "no tengo internet en la finca y necesito guardar datos"
  - "mis datos no se sincronizan con la nube"
  - "como forzar la sincronizacion de mis animales"
  - "se me perdieron los registros al salir del campo"
  - "puedo registrar pesajes sin datos moviles"
---

# Trabajo en Campo Sin Internet y Sincronización Automática

### Resumen y Alcance Funcional
Permite a los ganaderos registrar pesajes, eventos sanitarios, partos, traslados y altas de animales directamente en potreros o zonas rurales donde no existe cobertura celular ni conexión a internet. La aplicación almacena de forma segura todas las transacciones en la memoria local del dispositivo y, tan pronto detecta conexión a internet (Wi-Fi o datos móviles), sincroniza automáticamente todos los cambios con el servidor central sin perder información.

- **¿Funciona sin conexión a internet (Modo Offline)?:** Sí, 100% operativo en campo.
- **Comportamiento de sincronización:** Todos los eventos registrados sin cobertura se guardan de inmediato en la base de datos local del teléfono. Al recuperar señal de internet (Wi-Fi o datos móviles), el motor de sincronización sube los cambios en segundo plano sin interrumpir las labores del ganadero.

### Reglas de Negocio y Restricciones
- Todas las operaciones en la finca (pesajes, servicios, tratamientos) pueden crearse y consultarse sin conexión activa.
- La sincronización automática se activa en segundo plano en cuanto el teléfono recupera acceso a internet.
- El usuario puede solicitar en cualquier momento una sincronización manual forzada desde el menú de configuración de la app.
- Durante un proceso de sincronización activo, las solicitudes concurrentes se gestionan en cola para proteger la consistencia de los datos.
- Si un proceso de sincronización se interrumpe abruptamente (por ejemplo, por apagado del teléfono), el sistema reanuda automáticamente las transacciones pendientes en el siguiente inicio.

### Flujo Paso a Paso para el Usuario
- **Ruta de acceso en la aplicación:** Menú Principal > Configuración > Sincronización de Datos
1. Trabaje con normalidad en su finca registrando datos (la app indicará que se encuentra en modo local).
2. Al regresar a una zona con señal o conectarse a una red Wi-Fi, abra Control Ganadero.
3. Observe el icono de sincronización en la parte superior; una barra de progreso indicará el avance del envío de datos.
4. Si desea forzar el envío inmediato: ingrese a **Menú Principal** > **Configuración y Sincronización**.
5. Presione el botón **Sincronizar Ahora**.
6. Espere el mensaje de confirmación que indique que su hato está al día con la nube.
- **Pantalla de llegada tras guardar:** Estado de Sincronización Actualizado (permanece en la pantalla con el indicador verde de sincronizado).

### Matriz de Errores y Soluciones
| Mensaje en la App / Síntoma | Causa Real | Respuesta Sugerida por el Agente | Criterio de Escalamiento Humano |
| :--- | :--- | :--- | :--- |
| "Sincronización en curso" | El sistema está transmitiendo registros pendientes | "Su aplicación está enviando los registros acumulados en campo a la nube. Espere unos momentos hasta que la barra llegue al 100%." | No escalar, es un estado de espera normal. |
| "Error de sincronización: Conexión inestable" | La señal de internet se cortó durante el envío | "La señal de internet se interrumpió antes de completar el envío. Conéctese a una red Wi-Fi estable y presione 'Sincronizar Ahora' en Configuración." | Si el problema persiste tras 3 intentos con Wi-Fi estable, transferir a soporte técnico. |
| "Conflicto de registros detectado" | Dos dispositivos modificaron el mismo animal sin conexión | "Se detectaron cambios simultáneos sobre el mismo animal desde dos teléfonos. La aplicación conservará la información más reciente de acuerdo con la fecha de registro." | Si el usuario reporta inconsistencia en el historial genealógico, escalar con ID de finca. |
| "Memoria local saturada" | Gran volumen de fotos o registros sin sincronizar durante meses | "Tiene un volumen alto de información acumulada sin enviar. Conéctese a una red Wi-Fi de alta velocidad para completar la carga completa." | Si la aplicación se detiene inesperadamente, escalar a soporte prioritario. |
| "Círculo de espera infinito / Pantalla congelada en cargando" | El proceso de sincronización quedó atrapado en un socket bloqueado | "Espere 30 segundos. Si no avanza, cierre la app desde el administrador de tareas de su celular (deslizando hacia arriba) y vuelva a abrirla. Sus registros de campo siguen a salvo en el teléfono." | Si al presionar nuevamente 'Sincronizar Ahora' el círculo se vuelve a quedar infinito, transferir a soporte técnico con el nombre de la finca y correo. |

### Directivas de Seguridad y Guardrails
- NUNCA recomiende al usuario desinstalar la aplicación ni borrar los datos locales si tiene registros pendientes de sincronizar, ya que esto ocasionaría la pérdida definitiva de la información recopilada en campo.
- Siempre guíe al usuario a verificar su conexión Wi-Fi o datos móviles antes de realizar diagnósticos avanzados.
- Si se requiere intervención humana, solicite únicamente el nombre de la finca y el correo de la cuenta para verificar el estado de la base de datos en la nube.
