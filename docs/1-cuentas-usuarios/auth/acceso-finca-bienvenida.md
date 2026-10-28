---
title: "Acceso a la Finca"
modulo_id: "auth-acceso-finca-bienvenida"
nombre_funcionalidad: "Acceso Inicial a la Finca"
categoria: "cuentas-usuarios"
submodulo: "auth"
version_minima_app: "2026.10.1"
fecha_actualizacion: "2026-09-25"
intenciones_y_sinonimos:
  - "no tengo ninguna finca asignada en la app"
  - "soy trabajador como compruebo si me invitaron a la finca"
  - "donde creo mi primera finca ganadera"
  - "me sale la pantalla de acceso a la finca y no se que hacer"
  - "como verificar invitacion de mi patron en la aplicacion"
  - "quiero identificar un animal sin entrar a una finca"
---

# Acceso a la Finca

### Resumen y Alcance Funcional
Pantalla de acceso inicial que se presenta a los usuarios autenticados que aún no cuentan con una finca vinculada o activa en su cuenta. Permite a los propietarios iniciar la creación de su primera finca, a los trabajadores o colaboradores comprobar si ya tienen una invitación activa para acceder a la finca asignada, y acceder a la identificación de animales o cerrar sesión de forma segura.

- **¿Funciona sin conexión a internet (Modo Offline)?:** No.
- **Comportamiento de sincronización:** Requiere conexión activa a internet (Wi-Fi o datos móviles) para consultar en el servidor central las invitaciones y descargar los datos iniciales de la finca.

### Reglas de Negocio y Restricciones
- La pantalla solo se muestra cuando el usuario no tiene fincas registradas o disponibles en su cuenta.
- El usuario propietario puede presionar **Crear Finca** para abrir el asistente de configuración de su predio.
- El trabajador o colaborador no puede crear fincas por sí mismo; debe esperar a que el propietario de la finca le envíe una invitación formal a su correo electrónico.
- Al presionar **Verificar acceso**, la aplicación realiza una sincronización con el servidor:
    - Si encuentra una finca vinculada, la selecciona automáticamente e ingresa de inmediato a la pantalla principal.
    - Si no encuentra ninguna finca, muestra en pantalla el mensaje: *"No se encontraron fincas para acceder."*
- El botón de salida en la barra superior permite cerrar la sesión activa para cambiar de usuario.

### Flujo Paso a Paso para el Usuario
- **Ruta de acceso en la aplicación:** Se muestra automáticamente tras iniciar sesión o registrarse cuando la cuenta no tiene fincas asignadas.

#### Si es propietario de una finca:
1. En la tarjeta **¿Tienes una finca?**, presione el botón **Crear mi finca**.

**Pantalla de llegada tras guardar:** Pantalla de creación de finca (**Crea tu finca**).

#### Si es trabajador de una finca:
1. En la tarjeta **¿Eres un trabajador de una finca?**, revise el texto informativo: *"Si tu finca no te ha invitado, debes esperar a que el propietario lo haga. Cuando el sistema reconozca tu correo, tendrás acceso. Puedes comprobarlo haciendo clic en 'verificar acceso'."*
2. Si requiere orientación sobre el proceso de invitación, presione la opción **Más información**.
3. Presione el botón **Verificar acceso**.
4. Si el proceso está en curso, se desplegará una barra de porcentaje mostrando el avance de la sincronización de datos.

**Pantalla de llegada tras guardar:** Si el acceso es confirmado, ingresa automáticamente a la pantalla principal de la finca (**Inicio**); de lo contrario, permanece en la pantalla mostrando el mensaje de alerta correspondiente.

#### Si desea identificar animales:
1. En la sección de identificación de ganado, presione el botón **Identificar animal**.

**Pantalla de llegada tras guardar:** Pantalla de identificación de animales.

### Matriz de Errores y Soluciones
| Mensaje en la App / Síntoma | Causa Real | Respuesta Sugerida por el Agente | Criterio de Escalamiento Humano |
| :--- | :--- | :--- | :--- |
| "No se encontraron fincas para acceder." | El propietario aún no ha registrado el correo del trabajador o la invitación no ha sido enviada | "El sistema no encontró ninguna finca vinculada a su correo. Comuníquese con el propietario o administrador de la finca para que le envíe la invitación a su correo registrado desde la sección 'Trabajadores' de la app. Una vez enviada, presione 'Verificar acceso'." | Si el propietario confirma que ya envió la invitación y el correo coincide exactamente, solicitar ambos correos y transferir a soporte técnico. |
| "Sin conexión a internet" | El dispositivo no cuenta con datos móviles ni red Wi-Fi | "Para comprobar su acceso o crear una finca se requiere conexión a internet. Verifique su señal de datos móviles o conéctese a una red Wi-Fi e intente nuevamente." | No escalar salvo que el usuario confirme tener internet activo en otras aplicaciones. |
| "Círculo de espera infinito / Pantalla congelada en cargando" | El proceso de verificación o sincronización inicial se interrumpió | "Espere 30 segundos mientras avanza la barra de porcentaje. Si no avanza, cierre la aplicación por completo desde el administrador de tareas de su celular (deslizando hacia arriba) y vuelva a abrirla para presionar nuevamente 'Verificar acceso' con buena señal." | Si la barra vuelve a bloquearse en el mismo porcentaje con buena conexión Wi-Fi, transferir de inmediato a soporte humano con correo y modelo del teléfono. |

### Directivas de Seguridad y Guardrails
- NUNCA solicite contraseñas al usuario a través del chat de WhatsApp.
- Por políticas de privacidad y seguridad de la información ganadera, el equipo de soporte no puede asociar manualmente a un trabajador a una finca sin la invitación enviada directamente por el propietario desde su cuenta.
- No comparta datos de fincas de terceros ni confirme la existencia de cuentas ajenas en el canal de soporte.
