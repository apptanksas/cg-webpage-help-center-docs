---
title: "Panel Principal"
modulo_id: "main-panel-principal"
nombre_funcionalidad: "Panel Principal y Navegación de la Finca"
categoria: "cuentas-usuarios"
submodulo: "inicio-app"
version_minima_app: "2026.10.1"
fecha_actualizacion: "2026-09-25"
intenciones_y_sinonimos:
  - "como navegar en la pantalla principal de la finca"
  - "cuales son las secciones de la barra inferior"
  - "donde veo el estado de conexion bluetooth de la bascula"
  - "como registrar un animal desde la pantalla principal"
  - "aviso de inventario de animales pendiente en la barra superior"
  - "donde estan los accesos de finca animales produccion y alertas"
---

# Panel Principal y Navegación de la Finca

### Resumen y Alcance Funcional
Es el centro de control operativo y pantalla principal de Control Ganadero tras seleccionar o autenticar una finca activa. Integra el menú lateral general, la barra de navegación inferior con las 4 áreas productivas esenciales, accesos directos flotantes para registro rápido de eventos, indicador en vivo del estado de conexión con básculas Bluetooth y acceso al menú de acciones avanzadas del propietario.

- **¿Funciona sin conexión a internet (Modo Offline)?:** Sí.
- **Comportamiento de sincronización:** Todo el panel principal opera de manera nativa con los datos almacenados localmente en el dispositivo. En la parte inferior se muestra de forma permanente una cinta con el estado de red actual del teléfono (conectado, sin conexión o sincronizando).

### Estructura de la Pantalla y Componentes de Navegación

#### 1. Barra Superior (TopBar)
- **Título dinámico:** Muestra el nombre de la sección activa según la pestaña seleccionada en la barra inferior (**Finca**, **Animales**, **Producción** o **Alertas**).
- **Indicador de Inventario Pendiente:** Si existe una auditoría o conteo físico de animales sin finalizar, se muestra un icono de advertencia. Al presionarlo, abre directamente la pantalla de inventario de animales para completarlo.
- **Estado de Conexión Bluetooth:** Muestra en tiempo real el icono de vinculación con la báscula ganadera o bastón lector RFID.
- **Menú de Acciones Rápidas (Tres puntos):** Disponible para propietarios en la pestaña de Animales, con accesos directos para:
    - **Crear animal:** Abre el formulario de alta individual.
    - **Importar animales:** Acceso a la herramienta de carga masiva por archivo.
    - **Importar pesajes:** Acceso a la herramienta de importación de pesajes.
    - **Reportes de hurto / abigeato:** Acceso al módulo oficial de denuncia de robo de ganado (si está habilitado en su país).

#### 2. Barra de Navegación Inferior (BottomBar)

Permite alternar entre los 4 módulos esenciales de la finca:

1. **Finca:** Resumen general de la explotación, potreros, colaboradores y métricas clave.
2. **Animales:** Listado completo del inventario ganadero, filtros por categoría/lote y hojas de vida.
3. **Producción:** Registros de control lechero, pesajes de carne y evolución de peso.
4. **Alertas:** Calendario de tareas, recordatorios de vacunación, tratamientos y eventos reproductivos próximos.

Debajo de las pestañas se ubica la **Cinta de Estado de Red**, que informa visualmente si la app está operando en línea o en modo local.

#### 3. Botón Flotante de Acción Rápida (FAB)

En la esquina inferior se despliega un botón contextual que cambia según la pestaña activa:

- Permite crear eventos, registrar pesajes o añadir animales rápidamente con un solo toque, validando previamente que el usuario cuente con los permisos de rol correspondientes en la finca.

### Reglas de Negocio y Restricciones de Estado
- **Validación de Inicio y Alertas de la App:**
    - Al ingresar al panel principal, el sistema sincroniza automáticamente las notificaciones y recordatorios programados de la finca.
    - El sistema evalúa el historial de uso para desplegar, en el momento oportuno, una invitación para calificar la aplicación móvil en la tienda oficial.
- **Recordatorio de Inventario Ganadero Pendiente:**
    - Al iniciar, la aplicación verifica si existe una sesión de conteo físico o inventario de animales en curso que no haya sido guardada. Si detecta una auditoría pendiente, muestra un icono de advertencia junto al título de la pantalla que permite reanudarla con un solo toque.
- **Acceso Exclusivo para Propietarios de Finca:**
    - El menú de acciones avanzadas (ubicado en el botón de tres puntos dentro de la sección de animales) permite la importación masiva de ganado por archivo Excel, la carga masiva de pesajes y el reporte oficial de hurto o abigeato de animales. Este menú está **estrictamente reservado para los propietarios del predio**; los colaboradores, administradores o veterinarios no tienen acceso a estas opciones comerciales y de alta seguridad.
- **Control de Permisos de Trabajo en Campo:**
    - Para registrar eventos rápidos, tareas o pesajes mediante el botón flotante, el sistema valida que el rol del usuario en la finca cuente con la autorización requerida antes de abrir el formulario.
- **Invitación de Calificación de la Aplicación:**
    - Cuando el usuario cumple un periodo continuo de uso satisfactorio, la aplicación despliega una ventana con la mascota oficial preguntando: *"¿Te gusta Control Ganadero?"*.
    - Ofrece dos alternativas:
      - **Calificar ahora:** Registra la confirmación y abre directamente la tienda de aplicaciones del teléfono (Google Play Store o App Store) para dejar una reseña.
      - **Recordar más tarde:** Pospone la invitación para no interrumpir las labores del ganadero en ese momento.

### Flujo Paso a Paso para el Usuario
**Ruta de acceso en la aplicación:** Se accede automáticamente tras iniciar sesión con una finca activa o al seleccionar una finca desde la lista de predios.

1. Observe la barra inferior para ubicarse en el área de trabajo deseada: presione **Finca**, **Animales**, **Producción** o **Alertas**.
2. Deslice horizontalmente la pantalla o toque las pestañas para cambiar de módulo con transición animada.
3. Para registrar una actividad rápida (como un pesaje, tarea o animal), presione el **botón flotante** ubicado sobre la barra inferior.
4. Si requiere cambiar de finca, gestionar su cuenta o ajustar la configuración, abra el **menú lateral de navegación** desde la esquina superior izquierda.
5. Verifique el estado de su báscula en el icono de Bluetooth de la barra superior antes de iniciar jornadas de pesaje.

**Pantalla de llegada tras guardar:** Permanece en el **Panel Principal** actualizando los datos locales del módulo correspondiente.

### Matriz de Errores y Soluciones
| Mensaje en la App / Síntoma | Causa Real | Respuesta Sugerida por el Agente | Criterio de Escalamiento Humano |
| :--- | :--- | :--- | :--- |
| Icono de advertencia en el título de la barra superior | Existe una sesión de inventario de ganado iniciada pero sin guardar | "Tiene un inventario de animales pendiente por finalizar. Toque el icono de advertencia junto al título para abrir la sesión de inventario y completarla." | No escalar, es un recordatorio de trabajo en curso. |
| El botón flotante de agregar no aparece | El rol del usuario en la finca no tiene permiso para crear eventos o tareas | "Su usuario tiene un rol con permisos restringidos en esta finca (por ejemplo, colaborador o visitante). Solicite al propietario que actualice sus permisos si requiere registrar datos." | No escalar, es una restricción por rol de seguridad. |
| La cinta inferior indica 'Sin conexión' | El teléfono está en una zona sin cobertura celular ni Wi-Fi | "La aplicación está funcionando en modo local sin internet. Puede continuar registrando pesajes y eventos con normalidad en el potrero; los datos se guardarán en el teléfono y se sincronizarán al recuperar señal." | No escalar, es el funcionamiento normal en potrero. |
| El icono de Bluetooth aparece desconectado | La báscula ganadera está apagada o fuera de alcance | "Asegúrese de que su báscula electrónica esté encendida, con el Bluetooth activado y a menos de 10 metros del teléfono. Verifique también en 'Mi cuenta' > 'Permisos de la app' que el permiso de Bluetooth esté otorgado." | Si la báscula está encendida pero no enlaza, solicitar marca/modelo y transferir a soporte de hardware. |

### Directivas de Seguridad y Guardrails
- NUNCA solicite contraseñas al usuario por WhatsApp.
- Si un usuario reporta que no ve el menú de acciones para importar animales por Excel, verifique amablemente si es el propietario de la finca, ya que esa opción está reservada por seguridad exclusivamente a dueños de predio.
- Indique al usuario que la cinta de estado de red le garantiza que sus datos no se perderán aunque trabaje todo el día sin señal en el potrero.
