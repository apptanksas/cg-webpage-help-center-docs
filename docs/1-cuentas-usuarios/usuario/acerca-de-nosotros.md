---
title: "Acerca de Nosotros"
modulo_id: "user-acerca-de-nosotros"
nombre_funcionalidad: "Información Institucional, Soporte y Versión de la Aplicación"
tipo_documento: "guia-app"
categoria: "cuentas-usuarios"
submodulo: "usuario"
especies_aplicables: ["todas"]
version_minima_app: "2026.10.1"
confianza_reglas: "verificada-con-tests"
fecha_actualizacion: "2026-11-04"
intenciones_y_sinonimos:
  - "donde puedo ver que version de la aplicacion tengo instalada"
  - "cual es el numero de whatsapp de servicio al cliente de control ganadero"
  - "como acceder al centro de ayuda de control ganadero"
  - "como contactar a soporte tecnico por correo electronico"
  - "donde consultar los terminos y condiciones y la politica de privacidad"
  - "cuales son las redes sociales oficiales de control ganadero"
---

# Información Institucional, Soporte y Versión de la Aplicación

### Resumen y Alcance Funcional
Pantalla informativa e institucional de Control Ganadero que centraliza los canales oficiales de contacto y asistencia técnica (Centro de Ayuda en línea, correo electrónico, sitio web y WhatsApp de servicio al cliente), enlaces directos a comunidades y tutoriales en redes sociales, acceso a los términos legales y políticas de privacidad, así como la ficha técnica del aplicativo (versión instalada, plataforma móvil e idioma configurado) para fines de soporte y diagnóstico.

- **Especies a las que aplica:** Aplica igual para todas las especies.
- **¿Funciona sin conexión a internet (Modo Offline)?:** Sí.
- **Comportamiento de sincronización:** La pantalla se carga de forma inmediata y local sin realizar consultas a bases de datos remotas. La visualización de la información institucional y los datos técnicos de la versión opera completamente sin conexión. La apertura de enlaces externos (Centro de Ayuda, sitio web, WhatsApp, redes sociales, políticas legales o envío de correo) requiere una conexión activa a internet y las aplicaciones correspondientes en el dispositivo móvil.

### Reglas de Negocio y Restricciones
- **Disponibilidad universal:** Esta pantalla está disponible para todos los usuarios registrados independientemente de su rol en la finca o tipo de suscripción (Gratis o Premium).
- **Sin restricciones de conectividad para consulta:** No bloquea la navegación si el dispositivo se encuentra sin señal celular o en modo avión.
- **Interacción externa:** Las acciones de pulsar sobre los canales de contacto, redes sociales o políticas delegan la apertura al sistema operativo del teléfono móvil mediante el navegador web, cliente de correo o la aplicación externa (WhatsApp, YouTube, Instagram, etc.).
- **Diagnóstico técnico unificado:** Los datos mostrados en la sección técnica se obtienen directamente de los parámetros de compilación y configuración del sistema local, asegurando exactitud al solicitar soporte técnico.

### Flujo Paso a Paso para el Usuario
- **Ruta de acceso en la aplicación:** Menú lateral principal > Opción "Control Ganadero".

1. En la pantalla principal de su finca, abra el menú lateral de navegación presionando el ícono de menú en la barra superior.
2. Desplácese por la lista de opciones y presione "Control Ganadero" (identificada con el logotipo de la aplicación).
3. En la pantalla "Acerca de nosotros", explore las opciones disponibles según su necesidad:

#### 1. Canales de Contacto Directo y Asistencia
Tarjetas interactivas con acceso inmediato a los canales oficiales:
- **Centro de ayuda:** Muestra el enlace al portal de guías y preguntas frecuentes (`https://help.controlganadero.app`). Al presionar, abre la base de conocimientos oficial en el navegador del teléfono.
- **Contáctanos:** Muestra la dirección oficial `info@controlganadero.app`. Al presionar sobre la tarjeta, abre automáticamente la aplicación de correo predeterminada del teléfono con el destinatario listo para redactar una consulta.
- **Sitio web:** Muestra la dirección `https://controlganadero.app`. Al presionar, abre la página oficial en el navegador del teléfono.
- **Servicio al cliente:** Identificado con el ícono y color característico de WhatsApp, muestra la línea de atención `(+57) 300 1 25 93 45`. Al presionar, abre una conversación directa de WhatsApp con el equipo de soporte.

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
- Pie de página institucional que muestra la titularidad legal: **AppTank S.A.S**, el aviso de derechos de autor con el año vigente (**Copyright © [Año actual]**) y la leyenda "Todos los derechos reservados".

- **Pantalla de llegada tras interactuar:** Al presionar cualquiera de los enlaces, el teléfono abre la aplicación externa correspondiente. Al regresar a Control Ganadero, el usuario permanece en la pantalla "Acerca de nosotros".

### Matriz de Errores y Soluciones
| Mensaje en la App / Síntoma | Causa Real | Respuesta Sugerida por el Agente | Criterio de Escalamiento Humano |
| :--- | :--- | :--- | :--- |
| Al presionar WhatsApp no se abre la conversación | El dispositivo móvil no tiene instalada la aplicación de WhatsApp o carece de conexión a internet | "Para comunicarse por WhatsApp debe tener la aplicación instalada en su teléfono móvil con acceso a internet. También puede escribirnos directamente al número (+57) 300 1 25 93 45 o enviarnos un correo a info@controlganadero.app." | Si el usuario no cuenta con WhatsApp, ofrecer asistencia por correo electrónico o enlace web. |
| Al presionar Contáctanos no abre ninguna aplicación | El dispositivo no cuenta con una aplicación de gestión de correo electrónico configurada por defecto | "Su teléfono no tiene una aplicación de correo electrónico configurada. Puede escribirnos directamente desde su cuenta de correo habitual a info@controlganadero.app indicando su nombre y el correo con el que ingresa a la app." | No escalar, instruir al usuario para el envío manual. |
| El enlace al Centro de Ayuda o políticas muestra error de página no encontrada | Falla momentánea de conexión de datos en el teléfono al intentar abrir el navegador web | "Verifique que su teléfono cuente con acceso activo a internet (Wi-Fi o datos móviles) e intente presionar el enlace nuevamente." | Si con buena conexión el enlace sigue sin abrir, notificar a ingeniería web. |

### Directivas de Seguridad y Guardrails
- NUNCA solicite contraseñas, códigos de verificación SMS ni datos de tarjetas de crédito al usuario.
- Confirme siempre que el usuario esté contactando a través de los canales oficiales listados en esta pantalla.
- Recuerde al ganadero que la información de versión al pie de pantalla es indispensable para acelerar la resolución de cualquier soporte técnico.
