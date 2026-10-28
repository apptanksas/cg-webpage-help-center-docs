---
title: "Resumen Reproductivo"
modulo_id: "animal-reproductivo-resumen"
nombre_funcionalidad: "Resumen Reproductivo del Animal"
categoria: "sanidad-reproduccion"
submodulo: "reproduccion"
version_minima_app: "2026.10.1"
fecha_actualizacion: "2026-10-06"
intenciones_y_sinonimos:
  - "como ver el estado reproductivo y dias de gestacion de mi vaca"
  - "resumen de inseminaciones y chequeos de prenez"
  - "consultar dias abiertos e intervalo entre partos"
  - "historial reproductivo de un toro o reproductor"
  - "por que no me aparece el boton flotante de agregar evento reproductivo"
  - "donde consultar la fecha del proximo parto estimado"
---

# Resumen Reproductivo del Animal

### Resumen y Alcance Funcional
Pantalla central de gestión y auditoría reproductiva individual que consolida la hoja de vida zootécnica del ejemplar (hembra o macho). En hembras reproductoras, presenta en una cabecera especializada los indicadores clave de fertilidad —estado reproductivo actual, fecha del último parto o aborto, días de gestación, fecha proyectada y cuenta regresiva de próximo parto, días abiertos e intervalo entre partos— junto con tablas resumen de eventos (partos y abortos, fecundaciones o servicios, chequeos de preñez e hijos transferidos por biotecnología). En machos reproductores (toros), exhibe su historial de crías nacidas y las montas o inseminaciones en las que ha participado, facilitando el control genético y la toma de decisiones zootécnicas en la finca.

- **¿Funciona sin conexión a internet (Modo Offline)?:** Sí, todos los datos, cálculos zootécnicos de días e intervalos, y tablas de historial se procesan y consultan a partir de los registros locales almacenados en el teléfono.
- **Comportamiento de sincronización:** Las consultas e indicadores operan inmediatamente sin señal. Cualquier nuevo evento registrado (inseminación, palpación, parto o aborto) se guarda localmente en el dispositivo y se sincroniza con la nube automáticamente cuando el teléfono recupere conexión a internet.

### Reglas de Negocio y Restricciones
- **Diferenciación automática por género:**
    - **Hembras:** El sistema calcula y muestra la cabecera completa con métricas zootécnicas avanzadas (estado reproductivo, gestación, próximo parto, días abiertos e intervalo entre partos) y habilita hasta cuatro tablas de historial: **Partos/Abortos**, **Fecundaciones**, **Chequeo** e **Hijos transferidos** (si registra crías con madres receptoras).
    - **Machos:** La cabecera zootécnica femenina no aplica; la pantalla presenta de manera directa las dos tablas correspondientes a la actividad del reproductor: **Hijos** (crías biológicas engendradas) y **Fecundaciones** (servicios de inseminación o montas asistidas).
- **Cálculo condicional de indicadores zootécnicos en hembras:**
    - **Días de gestación y próximo parto:** Solo se calculan y muestran si el estado reproductivo actual de la vaca es confirmada como preñada. Si el parto se encuentra dentro de la fecha proyectada o la fecha ya fue rebasada sin confirmación de nacimiento, el sistema resalta el estado como parto inminente.
    - **Días abiertos:** Únicamente se calculan y visualizan cuando la hembra se encuentra en estado no preñada o vacía, contabilizando el tiempo transcurrido desde el último parto sin una nueva preñez confirmada.
    - **Intervalo entre partos:** Solo se calcula cuando la vaca tiene registrados dos o más partos en su historial, determinando el promedio de días entre alumbramientos sucesivos.
    - **Último evento reproductivo:** Muestra dinámicamente si el último hecho asentado fue un parto o un aborto, reflejando su fecha respectiva.
- **Acceso al menú de registro de eventos (Botón flotante +):**
    - El botón flotante circular con icono (**+**) solo se visualiza en hembras y siempre que el animal no se encuentre bloqueado por defunción o venta. Al pulsarlo, abre la pantalla completa de opciones para registrar eventos reproductivos (Inseminación, Palpación/Chequeo de preñez, Parto o Aborto).
    - En machos, el botón flotante no está disponible en esta pantalla; sus registros de monta o servicios se originan al asentar la inseminación o servicio sobre la hembra servida.
- **Límite de visualización en tablas resumen:**
    - Cada tabla en esta vista resume únicamente los registros más recientes (hasta un máximo de 5 filas por tabla) para garantizar agilidad visual. Cada sección cuenta con una flecha hacia la derecha para ingresar a la tabla completa e ilimitada del historial.
- **Navegación interactiva bidireccional:**
    - Al pulsar sobre un registro de parto o aborto, inseminación o chequeo de preñez, el sistema abre la pantalla de edición del registro correspondiente.
    - Al presionar sobre un animal hijo en las tablas de descendencia, la aplicación redirige de inmediato a la hoja de vida zootécnica de dicha cría.

### Flujo Paso a Paso para el Usuario
- **Ruta de acceso en la aplicación:**
    - **Ruta 1 (Desde la hoja de vida del animal):** En la barra inferior toque **Animales** > Seleccione al ejemplar en el listado > En la cuadrícula de módulos, presione el botón **Reproducción**.
    - **Ruta 2 (Redirección desde crecimiento):** Si ingresa a **Reproducción** en un ejemplar joven que ya cuenta con al menos un antecedente reproductivo (palpación, servicio o cría), el sistema redirige automáticamente a este resumen reproductivo.

#### Barra Superior y Datos del Animal
- **Barra de navegación:** Con diseño de fondo institucional sobre la cabecera, incorpora el botón de retroceso (flecha hacia la izquierda) para retornar a la hoja de vida del ejemplar, en el lateral derecho exhibe la identificación compuesta del animal (nombre y código de arete visual entre paréntesis en texto blanco) junto al icono en color blanco representativo del género del ejemplar (macho o hembra).
- **Botón flotante de acción rápida (+):** Presente únicamente en hembras activas y vivas (ubicado sobre la esquina inferior). Al presionarlo, despliega el menú de opciones para asentar un nuevo evento reproductivo (Inseminación, Chequeo de preñez, Parto o Aborto).

#### Cabecera Informativa de Estado Reproductivo (En Hembras)

Panel superior destacado con fondo primario institucional que contiene el título **Estado reproductivo** y las siguientes métricas según el historial del animal:

- **Último parto / Último aborto:** Etiqueta dinámica que exhibe la fecha del hecho reproductivo más reciente.
- **Próximo parto:** Muestra la fecha calculada para el alumbramiento junto con los días relativos faltantes entre corchetes, o bien la alerta de parto inminente.
- **Estado:** Condición reproductiva actual de la vaca (ej. Vacía, Preñada, En servicio, Inseminada).
- **Días de gestación:** Total de días transcurridos de preñez acumulados.
- **Intervalo entre partos:** Días transcurridos entre partos consecutivos.
- **Días abiertos:** Cantidad de días transcurridos desde el último parto sin confirmación de una nueva gestación.

#### Tablas Resumen en Hembras

Si la vaca cuenta con registros, el cuerpo de la pantalla muestra hasta cuatro bloques con acceso a tablas detalladas:

1. **Partos/Abortos:** Muestra las últimas crías nacidas o pérdidas gestacionales. Incluye botón de flecha para abrir la tabla completa. Al pulsar una fila de aborto se abre su edición, y al pulsar una cría se abre la hoja de vida del hijo.
2. **Fecundaciones:** Lista los servicios o inseminaciones artificiales más recientes. Incluye botón de flecha para abrir la tabla completa de inseminaciones y permite editar el servicio pulsando sobre la fila.
3. **Chequeo:** Presenta los diagnósticos de preñez y palpaciones veterinarias recientes. Incluye flecha de acceso a la tabla general de chequeos y permite editar un diagnóstico con un toque.
4. **Hijos transferidos:** Si la hembra ha actuado como donante de embriones y cuenta con crías nacidas a través de vacas receptoras, se muestra este bloque con flecha hacia la tabla completa de descendencia por transferencia de embriones.

#### Tablas Resumen en Machos
En toros reproductores, el cuerpo de la pantalla exhibe dos bloques:
1. **Hijos:** Tabla resumen con las crías directas engendradas por el macho. Al tocar sobre cualquier fila se accede a la hoja de vida del hijo, y la flecha de cabecera abre la tabla completa de descendencia.
2. **Fecundaciones:** Tabla resumen con los servicios de monta o inseminaciones realizadas con material genético de este toro. Permite editar el registro y acceder a la tabla completa mediante la flecha lateral.

- **Pantalla de llegada tras salir:**
  - Al pulsar la flecha de regreso en la barra superior, la aplicación retorna a la pantalla de resumen general del animal.

### Matriz de Errores y Soluciones
| Mensaje en la App / Síntoma | Causa Real | Respuesta Sugerida por el Agente | Criterio de Escalamiento Humano |
| :--- | :--- | :--- | :--- |
| Pantalla sin tablas / Estado vacío bajo la cabecera | El animal no cuenta con eventos reproductivos previos (partos, servicios, chequeos ni crías) | "La pantalla se encuentra vacía porque este ejemplar aún no tiene eventos reproductivos registrados. Si es una hembra, presione el botón (+) para asentar su primera inseminación, palpación o parto." | No escalar, comportamiento esperado en animales primerizos o sin historial. |
| No aparece el botón flotante (+) para registrar eventos | El animal seleccionado es un macho o la hembra se encuentra bloqueada por venta o defunción | "El botón de agregar eventos reproductivos (+) solo está disponible en hembras vivas y activas en la finca. En los machos, los servicios quedan asentados al registrar la monta o inseminación en la hembra correspondiente." | No escalar, regla de negocio del sistema. |
| No aparecen los días de gestación ni la fecha de próximo parto | El estado reproductivo de la vaca no es 'Preñada' | "Los días de gestación y la fecha estimada de parto solo se calculan cuando la vaca tiene un chequeo de preñez con resultado positivo o confirmación de preñez activa en el sistema." | No escalar, orientación zootécnica sobre los estados de preñez. |
| Los días abiertos muestran un valor en cero o no aparecen | La vaca se encuentra actualmente registrada como preñada o no tiene fecha de último parto | "El indicador de días abiertos únicamente se contabiliza cuando la hembra está vacía (no preñada), midiendo el tiempo transcurrido desde el último parto hasta una nueva confirmación de preñez." | No escalar, explicación funcional de la métrica zootécnica. |
| Círculo de espera infinito / Pantalla congelada en cargando | Proceso en segundo plano bloqueado o timeout en el dispositivo al consolidar el historial reproductivo local | "Espere 30 segundos. Si no avanza, cierre la aplicación por completo desde el administrador de tareas de su teléfono (deslizando hacia arriba) y vuelva a abrirla. Sus datos locales no se perderán." | Si tras reabrir la app la pantalla sigue congelada al ingresar al resumen reproductivo, transferir de inmediato a soporte humano con el código de arete del ejemplar. |

### Directivas de Seguridad y Guardrails
- NUNCA solicite al ganadero contraseñas, claves personales ni códigos de acceso bancario para asistirle en la consulta de su historial reproductivo.
- Aclare al usuario que las fechas proyectadas de parto son estimaciones zootécnicas basadas en el promedio de gestación de la especie configurada en la finca y no reemplazan el diagnóstico del médico veterinario.
- Recuerde que la edición o eliminación de registros reproductivos puede alterar los cálculos de días abiertos e intervalos entre partos de la hembra.
