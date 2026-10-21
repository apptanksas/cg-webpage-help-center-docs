---
title: "Cerrar Sesión"
modulo_id: "auth-cerrar-sesion"
nombre_funcionalidad: "Cierre de Sesión Seguro y Protección de Datos"
categoria: "cuentas-usuarios"
submodulo: "auth"
version_minima_app: "2026.10.1"
fecha_actualizacion: "2026-09-25"
intenciones_y_sinonimos:
  - "como cierro mi sesion en control ganadero"
  - "como salir de mi cuenta en la aplicacion"
  - "quiero cambiar de usuario en el telefono"
  - "aviso de perdida de datos al cerrar sesion"
  - "que pasa si cierro sesion sin sincronizar"
  - "donde esta el boton de desconectar mi cuenta"
---

# Cierre de Sesión Seguro y Protección de Datos

### Resumen y Alcance Funcional
Permite a los usuarios finalizar de forma segura su sesión activa en el dispositivo móvil para alternar de cuenta o proteger la privacidad de la finca. La aplicación cuenta con un protocolo preventivo que comprueba si existen registros recopilados en campo pendientes de enviar a la nube antes de permitir la salida, evitando la pérdida accidental de información ganadera.

- **¿Funciona sin conexión a internet (Modo Offline)?:** Sí, permite cerrar sesión localmente, pero con advertencias estrictas sobre la información no sincronizada.
- **Comportamiento de sincronización:** Antes de cerrar sesión, el sistema intenta transmitir automáticamente todos los datos pendientes al servidor central. Si el dispositivo no tiene internet o la sincronización no ha concluido, la aplicación solicita una confirmación explícita advirtiendo el riesgo de pérdida de datos.

### Reglas de Negocio y Restricciones
- Al solicitar el cierre de sesión, el sistema muestra el diálogo de confirmación: *"¿Estás seguro de cerrar tu sesión?"*.
- **Salvaguarda de Datos No Sincronizados:** Si existen eventos (pesajes, tratamientos, partos) guardados en la memoria local del teléfono que aún no se han subido al servidor:
  - La aplicación muestra una advertencia de seguridad: *"¿Estás seguro de cerrar tu sesión sin sincronizar los datos? Si cierra sesión sin sincronizar los datos, perderá la información que no haya sido guardada y que no se haya sincronizado con el servidor."*
- Si el usuario decide continuar y confirma la salida sin sincronizar, se eliminan las credenciales locales de la cuenta y los registros locales no enviados no podrán recuperarse.
- Una vez completado el cierre de sesión, se revoca el acceso a las fincas y el usuario es redirigido a la pantalla inicial de bienvenida.

### Flujo Paso a Paso para el Usuario
- **Ruta de acceso en la aplicación:** Menú lateral de la aplicación > Opción **Cerrar sesión**.
1. En el menú de navegación de la aplicación, presione la opción **Cerrar sesión**.
2. Si todos sus datos están al día con la nube:
   - Aparecerá el diálogo: *"¿Estás seguro de cerrar tu sesión?"*.
   - Presione el botón **Cerrar sesión** para confirmar.
3. Si tiene registros recopilados sin internet pendientes de sincronizar:
   - Aparecerá el aviso de advertencia: *"¿Estás seguro de cerrar tu sesión sin sincronizar los datos?"*.
   - **Recomendación prioritaria:** Presione **Cancelar**, conéctese a una red Wi-Fi o señal móvil y sincronice sus datos antes de salir.
   - Si de todas formas desea salir bajo su responsabilidad, presione el botón **Cerrar sesión**.
- **Pantalla de llegada tras guardar:** Pantalla inicial de **Bienvenida** (con las opciones de Iniciar Sesión y Registrarse).

### Matriz de Errores y Soluciones
| Mensaje en la App / Síntoma | Causa Real | Respuesta Sugerida por el Agente | Criterio de Escalamiento Humano |
| :--- | :--- | :--- | :--- |
| "Si cierra sesión sin sincronizar los datos, perderá la información..." | Hay registros locales en el teléfono que no se han subido a la nube | "¡Atención! Tiene información recopilada en campo que aún no se ha respaldado en el servidor. Presione 'Cancelar', vaya a Configuración y presione 'Sincronizar Ahora' con conexión a internet antes de salir para no perder sus datos." | Si el usuario afirma que cerró sesión por error y perdió registros de días anteriores, solicitar correo y transferir a soporte técnico. |
| "Sincronizando datos..." | El sistema está enviando transacciones acumuladas antes de desloguear | "La aplicación está respaldando sus últimos cambios en la nube antes de cerrar su cuenta. Espere unos momentos hasta que finalice el proceso." | No escalar, es un estado de protección de datos normal. |
| "Círculo de espera infinito / Pantalla congelada en cargando" | El proceso de cierre o sincronización final quedó bloqueado | "Espere 30 segundos. Si no finaliza, cierre la aplicación por completo desde el administrador de tareas de su celular (deslizando hacia arriba) y vuelva a abrirla. Verifique que sus datos sigan allí antes de forzar la salida." | Si la aplicación se congela repetidamente al intentar cerrar sesión, transferir a soporte técnico con el correo de la cuenta. |

### Directivas de Seguridad y Guardrails
- NUNCA recomiende al usuario cerrar sesión a la ligera si reporta problemas de sincronización en campo, ya que esto podría borrar sus registros pendientes en el teléfono.
- Si un usuario pregunta si al cerrar sesión se borran los animales de la finca, aclárele que todos los datos sincronizados previamente en la nube permanecen 100% seguros y estarán disponibles cuando vuelva a iniciar sesión.
- Si el usuario comparte el teléfono con otro trabajador, recuérdele la importancia de sincronizar y cerrar sesión al finalizar la jornada para que su compañero ingrese con su propio usuario.
