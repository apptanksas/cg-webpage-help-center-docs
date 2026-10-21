---
title: "Acerca de nosotros"
modulo_id: "user-acerca-de-nosotros"
nombre_funcionalidad: "Información Institucional, Soporte y Versión de la Aplicación"
categoria: "cuentas-usuarios"
submodulo: "usuario"
version_minima_app: "2026.10.1"
fecha_actualizacion: "2026-10-09"
intenciones_y_sinonimos:
  - "donde puedo ver que version de la aplicacion tengo instalada"
  - "cual es el numero de whatsapp de servicio al cliente de control ganadero"
  - "donde encuentro los tutoriales en video de la aplicacion"
  - "como contactar a soporte tecnico por correo electronico"
  - "donde consultar los terminos y condiciones y la politica de privacidad"
  - "cuales son las redes sociales oficiales de control ganadero"
---

# Información Institucional, Soporte y Versión de la Aplicación

### Resumen y Alcance Funcional
Pantalla informativa e institucional de Control Ganadero que centraliza los canales oficiales de contacto y asistencia técnica (correo electrónico, sitio web y WhatsApp de servicio al cliente), enlaces directos a comunidades y tutoriales en redes sociales, acceso a los términos legales y políticas de privacidad, así como la ficha técnica del aplicativo (versión instalada, plataforma móvil e idioma configurado) para fines de soporte y diagnóstico.

- **¿Funciona sin conexión a internet (Modo Offline)?:** Sí.
- **Comportamiento de sincronización:** La pantalla se carga de forma inmediata y local sin realizar consultas a bases de datos remotas. La visualización de la información institucional y los datos técnicos de la versión opera completamente sin conexión. La apertura de enlaces externos (sitio web, WhatsApp, redes sociales, políticas legales o envío de correo) requiere una conexión activa a internet y las aplicaciones correspondientes en el dispositivo móvil.

### Reglas de Negocio y Restricciones
- **Disponibilidad universal:** Esta pantalla está disponible para todos los usuarios registrados independientemente de su rol en la finca o tipo de suscripción (Gratis o Premium).
- **Sin restricciones de conectividad para consulta:** No bloquea la navegación si el dispositivo se encuentra sin señal celular o en modo avión.
- **Interacción externa:** Las acciones de pulsar sobre los canales de contacto, redes sociales o políticas delegan la apertura al sistema operativo del teléfono móvil mediante el navegador web, cliente de correo o la aplicación externa (WhatsApp, YouTube, Instagram, etc.).
- **Diagnóstico técnico unificado:** Los datos mostrados en la sección técnica se obtienen directamente de los parámetros de compilación y configuración del sistema local, asegurando exactitud al solicitar soporte técnico.

### Flujo Paso a Paso para el Usuario
- **Ruta de acceso en la aplicación:** Menú lateral principal > Opción **Control Ganadero**.

1. En la pantalla principal de su finca, abra el menú lateral de navegación presionando el ícono de menú en la barra superior.
2. Desplácese por la lista de opciones y presione **Control Ganadero** (identificada con el logotipo de la aplicación).
3. En la pantalla **Acerca de nosotros**, explore las opciones disponibles según su necesidad:

#### 1. Canales de Contacto Directo
Tarjetas interactivas con acceso inmediato a los canales oficiales:
- **Contáctanos:** Muestra la dirección oficial `info@controlganadero.app`. Al pulsar sobre la tarjeta, abre automáticamente la aplicación de correo predeterminada del teléfono con el destinatario listo para redactar una consulta.
- **Sitio web:** Muestra la dirección `https://controlganadero.app`. Al pulsar, abre la página oficial en el navegador del teléfono.
- **Servicio al cliente:** Identificado con el ícono y color característico de WhatsApp, muestra la línea de atención `(+57) 310 2 60 46 52`. Al pulsar, abre una conversación directa de WhatsApp con el equipo de soporte.

#### 2. Nuestras Redes Sociales y Tutoriales
Sección delimitada que agrupa los accesos a las comunidades oficiales y material formativo:
- **Instagram:** Redirige al perfil oficial de Control Ganadero en Instagram (`@controlganadero`).
- **TikTok:** Enlaza a la cuenta oficial en TikTok (`@controlganadero`) con videos explicativos y novedades del campo.
- **Youtube - Tutoriales:** Enlace directo al canal oficial de YouTube con guías paso a paso, seminarios y tutoriales de uso de cada herramienta.
- **Facebook:** Redirige a la página comunitaria oficial de Control Ganadero en Facebook.

#### 3. Nuestras Políticas
Accesos directos a los marcos normativos y de tratamiento de datos:
- **Términos y condiciones:** Abre en el navegador las condiciones de uso de la plataforma.
- **Política de privacidad:** Abre en el navegador las políticas de tratamiento y protección de datos personales.

#### 4. Acerca de la Aplicación (Ficha Técnica)
Tarjeta técnica con los parámetros de diagnóstico del aplicativo en el dispositivo:
- **Version:** Muestra el número de versión instalada (por ejemplo, 2026.10.1). Dato indispensable al reportar incidencias técnicas.
- **Platform:** Indica el sistema operativo del dispositivo móvil (Android o iOS).
- **Locale:** Muestra el código de idioma y país activo en la aplicación (por ejemplo, es).
- **Release:** Indicador de compilación oficial para producción (O) o versión de pruebas (X).

#### 5. Titularidad y Derechos de Autor
- Pie de página institucional que muestra la titularidad legal: **AppTank S.A.S**, el aviso de derechos de autor con el año vigente (**Copyright © [Año actual]**) y la leyenda **Todos los derechos reservados**.

- **Pantalla de llegada tras interactuar:** Al presionar cualquiera de los enlaces, el teléfono abre la aplicación externa correspondiente. Al regresar a Control Ganadero, el usuario permanece en la pantalla **Acerca de nosotros**.

### Matriz de Errores y Soluciones
| Mensaje en la App / Síntoma | Causa Real | Respuesta Sugerida por el Agente | Criterio de Escalamiento Humano |
| :--- | :--- | :--- | :--- |
| "Al presionar Contáctanos no se abre ninguna aplicación" | El teléfono no tiene una aplicación de correo electrónico instalada o configurada como predeterminada | "Para redactar el mensaje directamente necesita una aplicación de correo como Gmail o Mail en su teléfono. También puede escribirnos directamente desde su correo a info@controlganadero.app." | Si el usuario requiere soporte urgente y no puede enviar correo, atender directamente por el canal de WhatsApp. |
| "Al presionar Servicio al cliente o un enlace de red social no abre la página o chat" | No hay conexión a internet activa en el teléfono o la aplicación requerida no está instalada | "Verifique que su teléfono cuente con conexión a internet (datos móviles o Wi-Fi). Si va a comunicarse por WhatsApp, asegúrese de tener la aplicación instalada, o agregue directamente a sus contactos el número (+57) 310 2 60 46 52." | Si el usuario confirma conexión y no logra comunicarse, verificar disponibilidad del servicio de mensajería. |
| "Los enlaces de Términos y condiciones o Política de privacidad muestran error al cargar" | El navegador web del dispositivo no tiene conexión a internet o el enlace web presenta intermitencia temporal | "Compruebe que dispone de acceso a internet en su navegador móvil. Si persiste la intermitencia, puede consultar directamente las políticas ingresando desde cualquier navegador a https://www.controlganadero.app/terminos." | Si el enlace oficial presenta falla de disponibilidad web generalizada, notificar al equipo de desarrollo y sistemas. |

### Directivas de Seguridad y Guardrails
- Los únicos canales de soporte y comunicación autorizados son el correo `info@controlganadero.app` y la línea oficial de WhatsApp `(+57) 310 2 60 46 52`.
- El personal de soporte nunca solicitará contraseñas de acceso ni códigos de verificación por WhatsApp ni por correo electrónico.
- Para validación de incidencias en soporte, solicitar al ganadero el dato exacto que aparece en el campo **Version** dentro de **Acerca de la aplicación**.
