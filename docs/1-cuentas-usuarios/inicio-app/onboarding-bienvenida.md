---
title: "Guía de Inicio"
modulo_id: "onboarding-guia-inicio"
nombre_funcionalidad: "Guía de Bienvenida y Tutorial Inicial"
tipo_documento: "guia-app"
categoria: "cuentas-usuarios"
submodulo: "inicio-app"
especies_aplicables: ["todas"]
version_minima_app: "2026.10.1"
confianza_reglas: "inferida-de-dominio"
fecha_actualizacion: "2026-10-19"
intenciones_y_sinonimos:
  - "como funciona la aplicacion control ganadero"
  - "tutorial de inicio de control ganadero"
  - "cuales son las funciones principales de la app"
  - "donde inicio sesion o me registro al abrir por primera vez"
  - "como pasar las diapositivas de bienvenida"
  - "que hace control ganadero en la finca"
---

# Guía de Bienvenida y Tutorial Inicial

### Resumen y Alcance Funcional
Pantalla de bienvenida y presentación interactiva que se visualiza al abrir la aplicación por primera vez en un dispositivo o tras cerrar la sesión activa. A través de 5 diapositivas ilustradas, presenta a los productores los pilares fundamentales de la plataforma y proporciona los accesos directos para iniciar sesión o registrar una nueva cuenta.

- **Especies a las que aplica:** Aplica igual para todas las especies pecuarias (bovinos, bufalinos, equinos, ovinos, caprinos y porcinos).
- **¿Funciona sin conexión a internet (Modo Offline)?:** Sí. Las diapositivas y gráficos están empaquetados localmente en la aplicación y se pueden explorar sin requerir conexión a internet.
- **Comportamiento de sincronización:** Las diapositivas informativas no requieren sincronización con el servidor. Al presionar los botones inferiores para ingresar o registrarse, el sistema redirige a los formularios correspondientes de autenticación.

### Reglas de Negocio y Restricciones
- **Condición de visualización inicial:** La pantalla de bienvenida se despliega automáticamente cuando el usuario abre la aplicación por primera vez en el dispositivo o cuando no existe una sesión de usuario guardada localmente.
- **Sin requisitos de autenticación ni permisos:** No exige credenciales de acceso ni permisos de finca previos para interactuar con las diapositivas del carrusel.
- **Estructura del carrusel:** Consta exactamente de 5 diapositivas informativas numeradas que presentan las capacidades principales de la plataforma ganadera (administración de fincas, ficha individual del animal, producción y reproducción, calendario de tareas y trabajo sin conexión a internet).
- **Navegación gestual e interactiva:** El usuario puede transicionar entre diapositivas deslizando horizontalmente la pantalla hacia la izquierda o hacia la derecha, o pulsando directamente sobre cualquiera de los 5 puntos indicadores ubicados en la barra inferior.
- **Vías exclusivas de salida:** La pantalla dispone de dos únicos puntos de salida claramente diferenciados en la parte inferior: el botón "INICIAR SESIÓN" (que redirige al formulario de ingreso para usuarios con cuenta existente) y el botón "REGISTRARME" (que redirige al formulario de registro de nueva cuenta).
- **Persistencia de sesión:** Una vez que el usuario inicia sesión o completa su registro exitosamente, el sistema no vuelve a desplegar este tutorial en futuros arranques de la aplicación, a menos que el usuario cierre sesión explícitamente o reinstale la aplicación.

### Las 5 Diapositivas Informativas
El tutorial cuenta con un carrusel deslizable con indicador de puntos interactivo que resume las capacidades del sistema:

1. **Bienvenido a Control Ganadero:**
   - *Subtítulo:* "Controla tus fincas desde un solo lugar"
   - *Detalle:* Visualiza resúmenes generales de inventario, producción, reproducción y eventos clave de cada una de tus propiedades ganaderas de manera centralizada.
2. **Información detallada de cada animal:**
   - *Subtítulo:* "Accede fácilmente a la ficha técnica de cada ejemplar"
   - *Detalle:* Consulta datos generales, historial veterinario, pesajes, genealogía y estado reproductivo de cada animal desde tu teléfono móvil.
3. **Optimiza la producción y reproducción:**
   - *Subtítulo:* "Monitorea gráficos de rendimiento de leche y pesajes"
   - *Detalle:* Lleva un control total de partos, inseminaciones, pesajes de leche y evolución de peso para tomar mejores decisiones en tu finca.
4. **Organiza las tareas de tu equipo:**
   - *Subtítulo:* "Programa eventos en el calendario integrado"
   - *Detalle:* Asigna actividades diarias como chequeos veterinarios, vacunaciones y rotación de potreros para mantener a tu equipo sincronizado.
5. **Trabaja sin internet y sin preocupaciones:**
   - *Subtítulo:* "Registra datos directamente en el potrero, incluso sin cobertura"
   - *Detalle:* Tu información se mantendrá segura en tu teléfono y se sincronizará automáticamente tan pronto recuperes conexión a internet.

### Flujo Paso a Paso para el Usuario
- **Ruta de acceso en la aplicación:** Se muestra automáticamente tras la pantalla de carga cuando el usuario abre la aplicación por primera vez en el dispositivo o no tiene una sesión guardada.
1. Deslice la pantalla hacia la izquierda o presione los puntos circulares inferiores para avanzar entre las 5 diapositivas informativas.
2. Si ya dispone de una cuenta registrada: presione el botón "INICIAR SESIÓN" en la parte inferior.
3. Si es un usuario nuevo: presione el botón "REGISTRARME" en la parte inferior.
- **Pantalla de llegada tras guardar:** Pantalla de **Inicio de Sesión** (al presionar "INICIAR SESIÓN") o pantalla de **Registro de Usuario** (al presionar "REGISTRARME").

#### Etiquetas de la interfaz en otros idiomas
- "INICIAR SESIÓN" → Inglés: "LOG IN" → Portugués: "INICIAR SESSÃO"
- "REGISTRARME" → Inglés: "REGISTER" → Portugués: "REGISTRAR-SE"

### Matriz de Errores y Soluciones
| Mensaje en la App / Síntoma | Causa Real | Respuesta Sugerida por el Agente | Criterio de Escalamiento Humano |
| :--- | :--- | :--- | :--- |
| "No avanza la diapositiva al deslizar" | Deslizamiento táctil fuera del área interactiva del carrusel o gesto muy diagonal | "Asegúrese de deslizar el dedo horizontalmente en el centro de la pantalla, o toque directamente sobre los puntos circulares ubicados en la parte inferior para cambiar de página." | No requiere escalamiento; orientación de navegación gestual. |
| "Al tocar INICIAR SESIÓN o REGISTRARME no abre la pantalla" | Interrupción momentánea en el gestor de navegación del teléfono | "Cierre la aplicación por completo y vuelva a abrirla para presionar nuevamente el botón deseado." | Si tras reiniciar la app los botones continúan sin responder, transferir a soporte técnico indicando el modelo del teléfono. |

### Directivas de Seguridad y Guardrails
- Nunca solicite contraseñas, pines ni códigos de verificación por el chat de soporte durante la etapa de bienvenida.
- Oriente al usuario a elegir "REGISTRARME" si es la primera vez que utiliza Control Ganadero, o "INICIAR SESIÓN" si ya cuenta con una cuenta previamente registrada por él mismo o por su empresa ganadera.
- No prometa características que no correspondan a las opciones reales del sistema.
