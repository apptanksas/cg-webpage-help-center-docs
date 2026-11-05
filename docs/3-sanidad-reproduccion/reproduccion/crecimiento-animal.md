---
title: "Crecimiento del Animal"
modulo_id: "animal-crecimiento-etapas"
nombre_funcionalidad: "Crecimiento y Etapas del Animal"
tipo_documento: "guia-app"
categoria: "sanidad-reproduccion"
submodulo: "reproduccion"
especies_aplicables: ["todas"]
version_minima_app: "2026.10.1"
confianza_reglas: "verificada-con-tests"
fecha_actualizacion: "2026-11-04"
intenciones_y_sinonimos:
  - "como ver las etapas de crecimiento de un animal"
  - "fecha estimada de destete y madurez de mi animal"
  - "por que me redirige al resumen reproductivo en vez de crecimiento"
  - "consultar cuando pasa de cria a destetado o adulto"
  - "ver el calendario de evolucion y etapas zootecnicas"
  - "donde consultar la edad y proxima etapa del animal"
---

# Crecimiento y Etapas del Animal

### Resumen y Alcance Funcional
Pantalla de seguimiento zootécnico diseñada para visualizar la evolución del ejemplar a través de sus distintas etapas biológicas de desarrollo (Cría/Infante, Destetado, Crecimiento/Juvenil y Adulto). Permite al ganadero auditar la fecha estimada o confirmada en que el animal alcanza cada hito de crecimiento —destacando la fecha de destete en la cabecera— y comprobar visualmente en qué etapa se encuentra actualmente en relación con su ciclo de vida y los tiempos de transición configurados para la especie en la finca.

- **Especies a las que aplica:** Aplica igual para todas las especies.
- **¿Funciona sin conexión a internet (Modo Offline)?:** Sí, la pantalla calcula y presenta las fechas zootécnicas a partir de la fecha de nacimiento y los registros zootécnicos almacenados localmente en la base de datos del dispositivo móvil.
- **Comportamiento de sincronización:** La consulta y el cálculo de etapas operan de inmediato sin conexión. Cualquier actualización en la fecha de nacimiento, pesaje de destete o configuración de parámetros de transición en la finca se almacena en el teléfono y se sincroniza automáticamente con el servidor cuando el dispositivo disponga de señal de red.

### Reglas de Negocio y Restricciones
- **Redirección automática por registros reproductivos activos:**
    - Al abrir este módulo, el sistema valida de manera inmediata si el ejemplar cuenta con algún registro o antecedente reproductivo previo (inseminaciones, chequeos de preñez/palpaciones, partos, abortos o crías registradas).
    - Si el animal posee al menos un registro reproductivo activo, la aplicación omite la pantalla de crecimiento y redirige de forma automática a la pantalla completa de resumen reproductivo, ya que el ejemplar ha iniciado formalmente su vida reproductiva.
- **Cálculo dinámico de fechas de etapas zootécnicas:**
    - Si existe un hecho zootécnico registrado en el historial del animal para una etapa específica (por ejemplo, fecha confirmada de destete), el sistema utiliza la fecha real asentada.
    - Si no existe un registro manual, la aplicación calcula la fecha proyectada sumando a la fecha de nacimiento el umbral en días estipulado en la configuración de la especie para la finca (tiempo de destete, tiempo de transición a etapa juvenil y tiempo de transición a etapa adulta).
- **Atenuación visual por etapa alcanzada:**
    - Las tarjetas de etapas correspondientes a la fase actual y a las fases ya superadas por el animal se muestran con opacidad total y realce visual.
    - Las etapas futuras o pendientes se muestran con un estilo atenuado para distinguir claramente la fase zootécnica en la que se encuentra el ejemplar.
- **Restricción de etapas en animales con defunción registrada:**
    - Si el animal tiene registrada una defunción en el sistema, la pantalla oculta de manera automática todas aquellas etapas cuya fecha proyectada sea posterior a la fecha de muerte del ejemplar, evitando proyecciones biológicas sobre animales fallecidos.

### Flujo Paso a Paso para el Usuario
- **Ruta de acceso en la aplicación:**
    - En la barra inferior de navegación, toque "Animales" > Seleccione al animal en crecimiento en el listado > Presione el botón "Reproducción" (o "Crecimiento del animal" si el botón muestra la etapa joven del ejemplar).

#### 1. Barra Superior y Datos de Identidad
- **Barra de navegación superior:** Muestra el botón de retroceso (flecha hacia la izquierda) para volver a la hoja de vida del animal. A la derecha, exhibe el componente de identidad del ejemplar con su nombre, código de arete visual y foto de perfil.

#### 2. Cabecera Informativa de Destete
- **Franja superior de cabecera:** Panel destacado sobre el fondo primario institucional que contiene:
    - Título principal: "Crecimiento del animal".
    - Fila informativa de destete: Exhibe la etiqueta "Destetado" junto con la fecha proyectada o confirmada en que el ejemplar culmina la etapa de lactancia. Si el animal falleció antes de dicha fecha, el dato no se muestra.

#### 3. Cuadrícula de Etapas del Ciclo de Vida
El cuerpo de la pantalla presenta cuatro tarjetas organizadas en pares según la edad del animal:
1. **Cría / Infante (Etapa 1):** Muestra el icono de la cría, el nombre zootécnico del estado y la fecha de nacimiento registrada.
2. **Destetado (Etapa 2):** Exhibe el icono zootécnico de animal destetado, el nombre oficial de la etapa y la fecha en que cumplió o cumplirá el destete según los días configurados en la finca.
3. **Crecimiento / Juvenil (Etapa 3):** Muestra el icono juvenil de la especie (ej. novillo/novilla, potro/potranca), el nombre de la etapa y la fecha proyectada de transición a la juventud zootécnica según el tiempo de transición juvenil de la finca.
4. **Adulto (Etapa 4):** Exhibe el icono adulto (toro/vaca, caballo/yegua), el nombre de la fase y la fecha proyectada en que el animal alcanza su madurez zootécnica según el tiempo de transición adulta de la finca.

- **Pantalla de llegada tras salir:**
  - Al pulsar la flecha de regreso en la barra superior, la aplicación retorna a la pantalla de resumen y hoja de vida del animal.

#### Variaciones por especie
- Las denominaciones de las etapas juveniles y adultas varían según la especie del animal (por ejemplo: novillo/novilla y toro/vaca en bovinos; potro/potranca y caballo/yegua en equinos; lechón/cerda en porcinos).
- Los umbrales de edad en días para el cálculo de destete, paso a juvenil y paso a adulto se configuran de forma personalizada para cada especie en la sección de parámetros de la finca.

### Matriz de Errores y Soluciones
| Mensaje en la App / Síntoma | Causa Real | Respuesta Sugerida por el Agente | Criterio de Escalamiento Humano |
| :--- | :--- | :--- | :--- |
| Al presionar Reproducción se abre directamente el resumen reproductivo | El animal cuenta con antecedentes reproductivos registrados (palpaciones, servicios, partos o crías) | "La pantalla de Crecimiento del animal se muestra en ejemplares jóvenes sin actividad reproductiva. Al registrarse una palpación, inseminación, parto o cría, el sistema lo habilita como reproductor y abre directamente su módulo de Reproducción." | No escalar, comportamiento zootécnico normal del sistema. |
| La fecha de destete o de etapas muestra sin valor o guiones | El animal no tiene registrada la fecha de nacimiento en su ficha de datos generales | "Para calcular las fechas de crecimiento y destete, el animal debe contar con una fecha de nacimiento registrada. Ingrese a la ficha técnica del ejemplar, edite sus datos generales e introduzca la fecha de nacimiento." | No escalar, orientación al usuario para completar los datos generales del animal. |
| Algunas etapas no se muestran en pantalla | El ejemplar tiene una fecha de defunción registrada y las etapas faltantes son posteriores a su muerte | "El sistema no muestra proyecciones de crecimiento para etapas cuya fecha calculada sea posterior al fallecimiento registrado del animal." | No escalar, comportamiento esperado en animales con registro de muerte. |

### Directivas de Seguridad y Guardrails
- NUNCA solicite contraseñas ni códigos de verificación para orientar al ganadero en la consulta de etapas de crecimiento.
- Recuerde al usuario que los umbrales de edad y destete pueden ajustarse de manera global para toda la finca desde la configuración zootécnica de especies.
- Aclare al ganadero que la transición de etapa en la interfaz es un indicador visual de referencia y que no altera de forma obligatoria los registros médicos o de pesaje previos.
