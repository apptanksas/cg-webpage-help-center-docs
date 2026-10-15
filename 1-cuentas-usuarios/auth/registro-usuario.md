---
title: "Registro de Usuario"
modulo_id: "auth-registro-usuario"
nombre_funcionalidad: "Registro de Nueva Cuenta de Usuario"
categoria: "cuentas-usuarios"
submodulo: "auth"
version_minima_app: "2.4"
fecha_actualizacion: "2026-09-25"
intenciones_y_sinonimos:
  - "como me registro en la aplicacion"
  - "como crear una cuenta nueva en control ganadero"
  - "no puedo registrarme me dice que el correo ya existe"
  - "donde creo mi usuario para administrar mi finca"
  - "error al registrar mi telefono en la cuenta"
  - "soy trabajador como entro a la finca que me invitaron"
---

# Registro de Nueva Cuenta de Usuario

### Resumen y Alcance Funcional
Permite a productores agropecuarios, administradores, mayordomos y médicos veterinarios crear una cuenta personal en Control Ganadero. Durante el registro, el sistema valida la identidad del usuario, vincula su ubicación geográfica (país, departamento/estado y municipio/ciudad) y configura el perfil inicial según sea propietario de finca o colaborador invitado.

- **¿Funciona sin conexión a internet (Modo Offline)?:** No.
- **Comportamiento de sincronización:** Requiere conexión activa a internet (Wi-Fi o datos móviles) para verificar la disponibilidad del correo electrónico en el servidor central, registrar las credenciales de seguridad y autenticar automáticamente el dispositivo al finalizar.

### Reglas de Negocio y Restricciones
- El correo electrónico debe ser único en el sistema; no se permite registrar dos cuentas con el mismo correo.
- El nombre y apellido son obligatorios y deben contener caracteres válidos de texto personal.
- El número telefónico debe incluir el código internacional del país correspondiente.
- La contraseña debe definirse cumpliendo los estándares de seguridad de la plataforma.
- La selección de ubicación es jerárquica y obligatoria: primero se selecciona el país, lo que habilita la lista de estados/regiones, y posteriormente se habilita el municipio/ciudad correspondiente.
- Si el usuario activa la opción **"Soy propietario de finca"**, la aplicación lo guiará de inmediato al asistente de creación de su primera finca.
- Si el usuario es un trabajador o colaborador invitado por un dueño de hato, debe dejar desmarcada la opción de propietario para ingresar a la espera de su invitación.
- Es obligatorio aceptar los términos y condiciones del servicio antes de enviar el formulario.

### Flujo Paso a Paso para el Usuario
- **Ruta de acceso en la aplicación:** Pantalla de Bienvenida inicial > Botón inferior **Registrarse**
1. Abra la aplicación Control Ganadero en su teléfono móvil.
2. En la pantalla inicial de bienvenida, presione la opción **Registrarse** (ubicada debajo del botón de ingreso).
3. Complete los campos obligatorios del formulario:
   - **Correo electrónico:** Su dirección de email personal o empresarial.
   - **Nombre y Apellidos:** Sus datos de identificación.
   - **Contraseña:** Su clave privada de acceso.
   - **País y Teléfono:** Seleccione su país e ingrese su número celular.
   - **Región/Estado y Ciudad:** Seleccione su ubicación geográfica.
4. Active el interruptor **"Soy propietario de finca"** si usted es el dueño o titular del predio ganadero. Si es colaborador o mayordomo, déjelo apagado.
5. Presione el enlace de **Términos y Condiciones** para consultarlos si lo desea.
6. Presione el botón verde **Registrarse**.
7. Espere unos momentos mientras el sistema valida sus datos e inicia sesión automáticamente.
- **Pantalla de llegada tras guardar:** Si marcó "Soy propietario de finca", la app lo redirige al formulario de **Creación de Finca**; si no lo marcó, lo redirige a la pantalla de **Bienvenida del Usuario**.

### Matriz de Errores y Soluciones
| Mensaje en la App / Síntoma | Causa Real | Respuesta Sugerida por el Agente | Criterio de Escalamiento Humano |
| :--- | :--- | :--- | :--- |
| "El usuario ya se encuentra registrado" | Ya existe una cuenta creada con ese mismo correo electrónico | "El correo ingresado ya tiene una cuenta en Control Ganadero. En pantalla le aparecerá un mensaje de atención; presione 'Aceptar' para ir a la pantalla de inicio de sesión e ingresar su contraseña. Si no la recuerda, presione '¿Olvidó su contraseña?'." | Si el usuario afirma que nunca se ha registrado con ese correo, solicitar el correo y transferir a soporte técnico. |
| "Formato de teléfono o correo no válido" | Caracteres incompletos o formato incorrecto | "Por favor revise que su correo contenga el signo @ y su extensión (.com, etc.), y que el número telefónico incluya el código de área sin símbolos adicionales." | No escalar, corrección visual en pantalla. |
| "Debe seleccionar país, región y ciudad" | Faltó seleccionar uno de los niveles de ubicación geográfica | "La aplicación necesita conocer su ubicación para configurar las unidades de medida y normativas de su región. Seleccione su país en la lista para que se habiliten los departamentos y municipios." | No escalar, asistencia de navegación guiada. |
| "Registro exitoso pero falló el inicio de sesión automático" | El usuario se creó en la nube pero ocurrió un microcorte antes de descargar las credenciales | "Su cuenta fue creada con éxito en el sistema. Por favor presione 'Iniciar Sesión', escriba el correo y la contraseña que acaba de registrar e ingrese normalmente." | Si persiste el fallo de ingreso tras 2 intentos con buena conexión, transferir a soporte con el correo del usuario. |
| "Círculo de espera infinito / Pantalla congelada en cargando" | Proceso de creación bloqueado por latencia excesiva o interrupción de red | "Espere 30 segundos. Si la pantalla no reacciona, cierre la aplicación por completo desde el administrador de tareas de su celular (deslizando hacia arriba) y vuelva a abrirla. Intente iniciar sesión directamente; si no le permite, complete nuevamente el registro." | Si el botón permanece deshabilitado o la pantalla vuelve a congelarse, transferir de inmediato a soporte humano con correo y modelo del teléfono. |

### Directivas de Seguridad y Guardrails
- NUNCA solicite contraseñas al usuario por WhatsApp bajo ningún motivo.
- Si un usuario indica que es trabajador y no ve los animales de la finca, explíquele amablemente que el dueño de la finca debe enviarle una invitación desde su cuenta para darle acceso.
- No registre cuentas manualmente a nombre de terceros por chat; guíe siempre al usuario a completar el formulario en la app.
