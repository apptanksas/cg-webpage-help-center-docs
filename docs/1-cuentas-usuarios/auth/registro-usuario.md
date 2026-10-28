---
title: "Registro de Usuario"
modulo_id: "auth-registro-usuario"
nombre_funcionalidad: "Registro de Nueva Cuenta de Usuario"
categoria: "cuentas-usuarios"
submodulo: "auth"
version_minima_app: "2026.10.1"
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
Permite a productores agropecuarios, administradores, mayordomos y médicos veterinarios crear una cuenta personal en Control Ganadero. Durante el registro, el sistema valida la identidad del usuario, vincula su ubicación geográfica (país, región/departamento y ciudad/municipio) y configura el perfil inicial según sea propietario de finca o colaborador invitado.

- **¿Funciona sin conexión a internet (Modo Offline)?:** No.
- **Comportamiento de sincronización:** Requiere conexión activa a internet (Wi-Fi o datos móviles) para verificar la disponibilidad del correo electrónico en el servidor central, registrar las credenciales de seguridad y autenticar automáticamente el dispositivo al finalizar.

### Reglas de Negocio y Restricciones
- La pantalla cuenta con los siguientes campos y selectores oficiales:
    - **Email:** Obligatorio, validado con formato de correo electrónico.
    - **Nombre:** Obligatorio (validación de nombre personal).
    - **Apellidos:** Obligatorio (validación de nombre personal).
    - **Contraseña:** Obligatorio.
    - **País:** Selector obligatorio. Al cambiar de país, se reinician los valores de región y ciudad.
    - **Teléfono:** Obligatorio, validado bajo el estándar internacional de telefonía móvil.
    - **Región / Departamento:** Selector que se habilita únicamente cuando el país ha sido seleccionado.
    - **Ciudad / Municipio:** Selector que se habilita únicamente cuando la región ha sido seleccionada.
    - **Interruptor "¿Eres dueño de una finca?":** Permite definir si el usuario es titular de un predio o colaborador.
    - **Términos y condiciones:** Enlace de lectura obligatoria con acceso a los términos del servicio (`https://www.controlganadero.app/terminos`).
- **Validación de Usuario Único:** Si el correo electrónico ya existe en el sistema, la app abre un diálogo de confirmación con el mensaje: *"El usuario ya se encuentra registrado. ¿Deseas iniciar sesión?"*. Al confirmar, redirige automáticamente a la pantalla de inicio de sesión con el correo precargado.

### Flujo Paso a Paso para el Usuario
**Ruta de acceso en la aplicación:** Pantalla de Bienvenida inicial > Botón **Registrarse** (o desde la pantalla de inicio de sesión > enlace **Registrarme**).

1. En la pantalla de bienvenida o inicio de sesión, presione la opción **Registrarse**.
2. En el formulario de registro, complete los campos en orden:
   - En la casilla **Email**, escriba su correo electrónico.
   - En la casilla **Nombre**, escriba su nombre de pila.
   - En la casilla **Apellidos**, escriba sus apellidos.
   - En la casilla **Contraseña**, escriba su clave personal.
   - En el selector de país, elija su país de residencia.
   - En la casilla **Teléfono**, escriba su número celular.
   - En el selector de región, elija su departamento o estado.
   - En el selector de ciudad, elija su municipio o localidad.
3. Si usted es el propietario de la finca, active el interruptor **¿Eres dueño de una finca?**. Si es trabajador o colaborador invitado, déjelo desactivado.
4. Si desea consultar los términos legales, presione el enlace **términos y condiciones**.
5. Presione el botón **Registrarse**.
6. Espere unos momentos mientras el sistema valida el formulario e inicia sesión automáticamente.

**Pantalla de llegada tras guardar:** Si activó "¿Eres dueño de una finca?", la app lo redirige a la pantalla para crear su predio (**Crea tu finca**); si lo dejó desactivado, lo redirige a la pantalla de **Acceso a la Finca** a la espera de su invitación.

### Secciones Complementarias en la Pantalla
- **Información para trabajadores invitados:** En la parte inferior, la sección de ayuda responde a la pregunta *"¿Eres un trabajador de una finca?"* con el texto *"Si tu finca no te ha invitado, debes esperar a que el propietario lo haga. Cuando el sistema reconozca tu correo, tendrás acceso. Puedes comprobarlo haciendo clic en 'verificar acceso'."*, e incluye el enlace **Más información**.

### Matriz de Errores y Soluciones
| Mensaje en la App / Síntoma | Causa Real | Respuesta Sugerida por el Agente | Criterio de Escalamiento Humano |
| :--- | :--- | :--- | :--- |
| "El usuario ya se encuentra registrado" | Ya existe una cuenta creada con ese mismo correo electrónico | "El correo ingresado ya tiene una cuenta en Control Ganadero. En pantalla le aparecerá el aviso de confirmación; presione 'Aceptar' para ir a la pantalla de inicio de sesión con su correo listo para ingresar su clave. Si no la recuerda, presione 'Olvidé mi contraseña'." | Si el usuario afirma que nunca se ha registrado con ese correo, solicitar el correo y transferir a soporte técnico. |
| "Formato de teléfono o correo no válido" | Caracteres incompletos o formato incorrecto | "Revise que su correo contenga el signo @ y su extensión (.com, etc.), y que el número telefónico incluya el código de área internacional sin símbolos adicionales." | No escalar, es una corrección directa en pantalla. |
| "Debe seleccionar país, región y ciudad" | Faltó seleccionar uno de los niveles de ubicación geográfica | "La aplicación necesita conocer su ubicación para configurar las unidades de medida y normativas de su región. Seleccione su país en la lista para que se habiliten los departamentos y municipios." | No escalar, asistencia de navegación guiada. |
| "Sin conexión a internet" | No hay cobertura celular de datos ni red Wi-Fi disponible | "Para completar el registro de su cuenta se requiere conexión a internet para sincronizar con el servidor central. Conéctese a una red Wi-Fi o active sus datos móviles e intente de nuevo." | No escalar salvo que el usuario confirme tener internet en otras aplicaciones. |
| "Círculo de espera infinito / Pantalla congelada en cargando" | Proceso de creación bloqueado por latencia excesiva o interrupción de red | "Espere 30 segundos. Si la pantalla no reacciona, cierre la aplicación por completo desde el administrador de tareas de su celular (deslizando hacia arriba) y vuelva a abrirla. Intente iniciar sesión directamente; si no le permite, complete nuevamente el registro." | Si el botón permanece deshabilitado o la pantalla vuelve a congelarse, transferir de inmediato a soporte humano con correo y modelo del teléfono. |

### Directivas de Seguridad y Guardrails
- NUNCA solicite contraseñas al usuario por WhatsApp bajo ningún motivo.
- Si un usuario indica que es trabajador y no ve los animales de la finca, explíquele amablemente que el dueño de la finca debe enviarle una invitación desde su cuenta para darle acceso.
- No registre cuentas manualmente a nombre de terceros por chat; guíe siempre al usuario a completar el formulario en la app.
