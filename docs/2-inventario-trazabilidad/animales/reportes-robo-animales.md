---
title: "Reportes de Robo"
modulo_id: "animales-reportes-robo"
nombre_funcionalidad: "Mis Reportes de Robo de Animales"
tipo_documento: "guia-app"
categoria: "inventario-trazabilidad"
submodulo: "animales"
especies_aplicables: ["todas"]
version_minima_app: "2025.05.1"
confianza_reglas: "verificada-con-tests"
fecha_actualizacion: "2026-10-19"
intenciones_y_sinonimos:
  - "como ver mis denuncias de ganado robado"
  - "consultar reportes de abigeato de la finca"
  - "donde veo los animales reportados como robados"
  - "como abrir el enlace publico de mi reporte de robo"
  - "crear un nuevo reporte de robo de animales"
  - "no me aparece la opcion de reportar robo de animales"
---

# Mis Reportes de Robo de Animales

### Resumen y Alcance Funcional
Pantalla de consulta y gestión donde el productor visualiza el historial de denuncias y reportes de robo de animales registrados en su finca ganadera. Permite verificar la fecha del incidente, la ubicación geográfica en coordenadas de latitud y longitud correspondientes al suceso, el número total de animales involucrados y acceder de inmediato a la página web pública de cada reporte para compartirla con autoridades policiales, gremios ganaderos o vecinos. Asimismo, desde esta vista es posible iniciar el registro de un nuevo reporte de robo de animales mediante un botón de acceso directo.

- **Especies a las que aplica:** Aplica por igual a todas las especies manejadas en la finca ganadera (bovinos, bufalinos, equinos, caprinos, ovinos y porcinos).
- **¿Funciona sin conexión a internet (Modo Offline)?:** No. Esta funcionalidad exige conexión a internet activa y obligatoria para consultar la configuración de seguridad y descargar los reportes de robo vigentes desde el servidor central. De igual manera, la apertura de las fichas públicas de cada reporte se realiza mediante enlaces web en el navegador del teléfono.
- **Comportamiento de sincronización:** Requiere conexión a internet para descargar y actualizar el listado de reportes en tiempo real directamente con el servidor. No almacena denuncias en la base de datos local para consulta offline.
- **Plataformas:** Funciona con idéntica interfaz y comportamiento tanto en dispositivos Android como en iOS.

### Reglas de Negocio y Restricciones
- **Disponibilidad de la funcionalidad (Bandera de funcionalidad):**
  - La herramienta de reporte y consulta de robo de animales está condicionada a la activación del servicio de seguridad contra robo de animales en la aplicación.
  - Si la funcionalidad se encuentra desactivada, el sistema interrumpe el acceso y redirige automáticamente hacia la pantalla principal.
- **Permisos requeridos por rol en la finca:**
  - Para visualizar la opción en el menú de acciones rápidas y gestionar las denuncias, el usuario debe tener asignado el permiso de creación de reporte de robo de animales en la finca activa.
- **Configuración de seguridad previa obligatoria:**
  - Para consultar el listado o registrar un reporte, la finca debe contar previamente con su configuración de reporte de robo establecida (datos de contacto del propietario y red de contactos de emergencia). Si dicha configuración no existe, el sistema solicita completarla antes de acceder a la lista.
- **Redirección automática ante lista vacía (Verificado con tests):**
  - Si la finca activa no posee reportes de robo registrados en el sistema, la aplicación redirige de manera automática al formulario de creación de reporte de robo, permitiendo al productor registrar de inmediato el suceso sin pasar por una lista en blanco.
- **Restricción operativa sobre animales reportados:**
  - Los animales incluidos dentro de un reporte de robo activo quedan identificados en el sistema como sustraídos, bloqueándose operativamente en la finca para evitar traslados, ventas o registros productivos cotidianos mientras el reporte permanezca vigente.

### Flujo Paso a Paso para el Usuario
- **Ruta de acceso en la aplicación:**
  - **Ruta principal:** Barra inferior de navegación > Presionar el botón central de menú rápido (+) > Seleccionar la opción "Reportar robo de animales" > Si la finca ya tiene configuración guardada y cuenta con denuncias activas, se abre el listado.
  - **Ruta tras guardar configuración:** Si se ingresó a configurar los contactos de emergencia y la finca ya tiene denuncias previas, el sistema navega directamente a este listado.

#### 1. Encabezado y Acción de Nuevo Reporte
1. En la barra superior, confirme el título "Mis reportes de robo de animales".
2. En la parte superior de la pantalla, ubique el encabezado de sección "Reportes".
3. A la derecha del encabezado, presione el botón "Crear nuevo reporte" si requiere registrar una nueva denuncia de sustracción de animales. El sistema abrirá inmediatamente el formulario de registro de reporte de robo.

#### 2. Consulta de Reportes Registrados
En el cuerpo de la pantalla se despliega el listado de tarjetas correspondientes a los reportes de robo registrados:
1. **Fecha del incidente:** Junto al icono de calendario, visualice la fecha en la que se registró o sucedió el robo.
2. **Coordenadas de ubicación:** Junto al icono de localización geográfica, observe las coordenadas de latitud y longitud donde ocurrió el suceso (formateadas con 4 decimales).
3. **Insignia de animales reportados:** En el recuadro destacado a la derecha de la tarjeta, visualice:
   - La etiqueta "Reportado".
   - La cantidad total de ejemplares incluidos en la denuncia en color de alerta.
   - El término "Animales".

#### 3. Apertura y Difusión del Enlace Público
1. Presione sobre cualquier tarjeta de reporte en el listado.
2. La aplicación abrirá automáticamente en el navegador web del dispositivo la ficha pública oficial del reporte de robo.
3. En dicho enlace público, cualquier persona o autoridad puede verificar las fotografías, aretes, códigos, razas, señas particulares y marcas de hierro de los animales sustraídos para facilitar su localización comunitaria e identificación en retenes o ferias.

- **Pantalla de llegada tras salir:** Al presionar la flecha de regreso en la barra superior, el usuario retorna a la pantalla o menú de origen.

#### Variaciones por especie
Aplica por igual a todas las especies zootécnicas manejadas en la finca ganadera (bovinos, bufalinos, equinos, caprinos, ovinos y porcinos). Los reportes y enlaces públicos muestran las características identificatorias de los ejemplares sin distinción de especie.

#### Etiquetas de la interfaz en otros idiomas
| Español | Inglés | Portugués |
| :--- | :--- | :--- |
| "Mis reportes de robo de animales" | "My animal theft reports" | "Meus relatórios de roubo de animais" |
| "Reportes" | "Reports" | "Relatórios" |
| "Crear nuevo reporte" | "Create new report" | "Criar novo relatório" |
| "Reportado" | "Reported" | "Reportado" |
| "Animales" | "Animals" | "Animais" |

### Matriz de Errores y Soluciones
| Mensaje en la App / Síntoma | Causa Real | Respuesta Sugerida por el Agente | Criterio de Escalamiento Humano |
| :--- | :--- | :--- | :--- |
| La opción "Reportar robo de animales" no aparece en el menú central (+) | El usuario no tiene asignado el permiso de creación de reportes de robo en la finca o la funcionalidad no está habilitada para su cuenta | "Para acceder a esta función, el propietario o administrador de la finca debe otorgarle el permiso de reporte de robo de animales en la administración de colaboradores. Verifique también que la funcionalidad esté habilitada en su cuenta." | Si el usuario es propietario confirmado de la finca activa y la opción no aparece, escalar a soporte técnico para verificar la activación del servicio. |
| La pantalla se redirige directamente a la pantalla de crear reporte de robo sin mostrar la lista | La finca no registra reportes de robo activos en el sistema | "La aplicación lo dirige de manera automática al formulario de registro debido a que su finca no tiene reportes de robo registrados en este momento. Desde allí puede registrar de inmediato los datos del suceso." | No escalar, comportamiento esperado del sistema cuando la lista de reportes está vacía. |
| Error de conexión a internet o mensaje de red requerida al ingresar | El teléfono no tiene conexión a internet activa (datos móviles o WiFi) al momento de consultar los reportes | "El módulo de reportes de robo requiere conexión a internet para consultar los datos en tiempo real con el servidor. Compruebe que sus datos móviles o conexión WiFi estén activos e intente ingresar nuevamente." | Si el usuario cuenta con navegación estable en otras aplicaciones pero el módulo continúa indicando error de conexión, escalar a soporte técnico. |
| El navegador no abre la página web del reporte al presionar la tarjeta | Bloqueo en el navegador web predeterminado del teléfono o falla temporal de conectividad | "Asegúrese de contar con conexión a internet y verifique que el navegador de su teléfono esté habilitado para abrir enlaces externos. Si el enlace no abre, intente presionarlo de nuevo." | Si el enlace público continúa sin cargar tras varios intentos con conexión estable, escalar a soporte técnico reportando el identificador del reporte. |
| Espera prolongada en pantalla al cargar los reportes | Demora en la respuesta del servidor al validar la configuración o consultar la lista de denuncias | "Espere un momento mientras el sistema descarga los reportes desde el servidor. Si no responde, cierre la aplicación por completo y vuelva a abrirla." | Si la aplicación continúa sin responder tras reabrirla con conexión estable, escalar a soporte técnico indicando el modelo del teléfono. |

### Directivas de Seguridad y Guardrails
- Nunca solicites contraseñas, números de cédula, pines ni códigos de verificación por los canales de atención.
- Recuerda al ganadero que los reportes de robo generan enlaces públicos con la información zootécnica de los animales para facilitar su identificación comunitaria, resguardando los datos personales conforme a las políticas de privacidad.
- Aclara siempre al productor que el registro de robo dentro de la aplicación es una herramienta de difusión y control interno, pero no reemplaza la denuncia formal ante las autoridades policiales y judiciales competentes.
- Confirma que el usuario se encuentre en la finca ganadera correcta antes de orientarlo sobre la consulta o registro de denuncias.
