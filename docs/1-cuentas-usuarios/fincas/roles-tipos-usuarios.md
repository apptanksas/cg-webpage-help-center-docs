---
title: "Roles y Tipos de Usuarios"
modulo_id: "fincas-roles-tipos-usuarios"
nombre_funcionalidad: "Guía de Tipos de Usuarios, Permisos y Restricciones de Colaboradores"
categoria: "cuentas-usuarios"
submodulo: "fincas"
version_minima_app: "2026.10.1"
fecha_actualizacion: "2026-10-13"
intenciones_y_sinonimos:
  - "cuales son los tipos de usuarios y roles en la finca"
  - "que permisos tiene un administrador o un veterinario"
  - "que puede hacer un empleado en control ganadero"
  - "diferencias entre propietario administrador y empleado"
  - "por que mi trabajador no puede eliminar animales"
  - "como saber que restricciones tiene el rol visitante"
---

# Guía de Tipos de Usuarios, Permisos y Restricciones de Colaboradores

### Resumen y Alcance Funcional
Proporciona al ganadero y propietario de la finca una guía informativa clara y detallada sobre las atribuciones, niveles de responsabilidad, permisos operativos y restricciones asociadas a cada tipo de usuario disponible en Control Ganadero (Propietario, Administrador, Veterinario, Empleado y Visitante). Permite entender con precisión qué labores cotidianas puede desempeñar cada colaborador antes o después de asignarle un perfil en la explotación ganadera.

- **¿Funciona sin conexión a internet (Modo Offline)?:** Sí.
- **Comportamiento de sincronización:** La pantalla es puramente informativa y de consulta de directrices del sistema. Todo el contenido y las descripciones de los perfiles están almacenados de forma local dentro de la aplicación móvil, por lo que el ganadero puede acceder y revisar los roles en cualquier momento y lugar, sin necesidad de conexión a internet activa.

### Reglas de Negocio y Restricciones
- **Disponibilidad para consulta:**
    - La pantalla informativa está accesible para cualquier usuario que consulte la sección de miembros del equipo de la finca, permitiendo conocer las funciones operativas de cada perfil.
- **Perfiles predeterminados en la finca y desglose normativo:**
    - **Propietario:**
      - *Descripción:* Cuenta con acceso total a todas las funciones y registros de la aplicación.
      - *Permisos:* Leer, crear, editar y eliminar cualquier registro de la aplicación; administrar animales y fincas; invitar, administrar y eliminar usuarios; compartir informes y hojas de vida de los animales; crear, editar y eliminar eventos o tareas; gestionar permisos y trabajadores.
      - *Restricciones:* Ninguna.
    - **Administrador:**
      - *Descripción:* Encargado de supervisar y administrar la operación diaria de la finca.
      - *Permisos:* Leer, crear, editar y eliminar registros de la aplicación; administrar información operativa y productiva; crear, editar y eliminar eventos o tareas.
      - *Restricciones:* No puede administrar trabajadores de la finca.
    - **Veterinario:**
      - *Descripción:* Responsable del seguimiento sanitario y reproductivo de los animales. Puede registrar datos y actualizar datos.
      - *Permisos:* Leer registros de la aplicación; crear y editar registros veterinarios y reproductivos; actualizar tratamientos, diagnósticos y estados de salud; crear eventos o tareas relacionadas con controles veterinarios.
      - *Restricciones:* No puede eliminar registros ni administrar usuarios.
    - **Empleado:**
      - *Descripción:* Responsable del registro de actividades e información productiva. Solo puede registrar datos, pero no puede editar ni eliminar.
      - *Permisos:* Leer registros autorizados de la aplicación; crear nuevos registros y actividades; crear eventos o tareas.
      - *Restricciones:* No puede editar ni eliminar registros existentes; no puede administrar usuarios ni configuraciones.
    - **Visitante:**
      - *Descripción:* Usuario con acceso únicamente de consulta y lectura.
      - *Permisos:* Solo puede leer la información de la finca.
      - *Restricciones:* No puede crear, editar ni eliminar registros.
- **Navegación e inmutabilidad:**
    - La pantalla no contiene campos editables ni botones de confirmación que alteren la base de datos; su propósito es instruir sobre las políticas de seguridad y perfiles de la plataforma pecuaria.

### Flujo Paso a Paso para el Usuario
- **Ruta de acceso en la aplicación:** Menú lateral principal (ícono de tres líneas en la esquina superior izquierda) > **Trabajadores** > En la barra superior, presione el ícono de información (i) o **Más información**.

#### 1. Visualización del encabezado y propósito
1. En la barra superior de la pantalla se despliega el título **Más información** con el botón de flecha hacia atrás para regresar cuando se desee.
2. Al inicio del contenido observará el encabezado principal **Tipos de usuarios**, acompañado del texto orientativo: *"Cada tipo de usuario tiene unas funciones en la app, elija bien el rol de cada invitado para que puedan desempeñar todas sus labores cotidianas."*

#### 2. Lectura y consulta de cada perfil
1. Deslice la pantalla hacia abajo para explorar de manera secuencial los bloques de cada perfil, delimitados por una línea divisoria:
    - **Propietario:** Lea la descripción de acceso total, el desglose de permisos amplios y la indicación de que no posee restricciones.
     - **Administrador:** Consulte las facultades de supervisión de la operación diaria, sus permisos sobre datos productivos y la restricción específica de no poder gestionar colaboradores.
     - **Veterinario:** Revise las atribuciones médicas y reproductivas, el registro de tratamientos y la imposibilidad de eliminar información o invitar a otros miembros.
     - **Empleado:** Valide las facultades de captura de actividades de campo (pesajes, eventos) y sus restricciones de no editar ni borrar información preexistente.
     - **Visitante:** Confirme el modo de solo lectura para auditorías o supervisores externos sin facultades de modificación.

#### 3. Salida o retorno
1. Una vez revisada la información, presione el botón de flecha hacia atrás ubicado en la barra superior.

**Pantalla de llegada tras guardar o salir:** El usuario regresa a la pantalla **Trabajadores**, donde se visualiza el listado general de miembros e invitaciones de la finca activa.

### Matriz de Errores y Soluciones
| Mensaje en la App / Síntoma | Causa Real | Respuesta Sugerida por el Agente | Criterio de Escalamiento Humano |
| :--- | :--- | :--- | :--- |
| Un colaborador reporta que no le aparece el botón de eliminar o editar en un animal o pesaje | El colaborador tiene asignado un rol con restricciones de edición o eliminación (como Empleado, Veterinario o Visitante) | "En Control Ganadero, los colaboradores con perfiles de Empleado, Veterinario o Visitante no tienen permisos para editar o eliminar registros para proteger la integridad de los datos de la finca. Si requiere que el colaborador pueda modificar registros, el propietario de la finca debe asignarle un rol de Administrador o realizar la corrección desde la cuenta de propietario." | No escalar. Corresponde al modelo de permisos y seguridad de la finca. |
| Un colaborador con rol Administrador no puede invitar a nuevos trabajadores | El perfil Administrador tiene la restricción explícita de no poder administrar ni invitar trabajadores a la finca | "Por diseño de seguridad de la plataforma pecuaria, la administración e invitación de nuevos colaboradores está reservada exclusivamente para el Propietario de la finca. El dueño de la explotación debe enviar la invitación directamente desde su cuenta en la sección Trabajadores." | No escalar. Regla de negocio estándar de la aplicación. |
| El botón de información (i) en la barra superior de Trabajadores no abre la pantalla de roles | La pantalla de Trabajadores se encuentra en modo de selección para eliminación múltiple (barra superior en color de borrado) | "Cuando tiene uno o más trabajadores seleccionados para eliminar, la barra superior cambia a modo de borrado. Presione la flecha de regreso en la esquina superior izquierda para cancelar la selección; una vez restaurada la barra habitual de Trabajadores, presione el ícono de información (i) en la esquina superior derecha." | No escalar. Guía de uso de la interfaz. |

### Directivas de Seguridad y Guardrails
- NUNCA solicite credenciales personales, contraseñas de correo ni datos sensibles a los usuarios.
- Explique claramente que las restricciones de los roles son medidas de seguridad diseñadas para salvaguardar la veracidad y trazabilidad de los datos productivos y sanitarios del hato ganadero.
- Si el dueño de una finca desea que un empleado adquiera mayores privilegios, guíelo para cancelar la invitación previa desde **Trabajadores** y emitir una nueva seleccionando el perfil adecuado (ej. Administrador).
