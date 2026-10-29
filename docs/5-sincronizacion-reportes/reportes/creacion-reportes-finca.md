---
title: "Catálogo y Diagnóstico de Reportes"
modulo_id: "reportes-backend-motor-generacion"
nombre_funcionalidad: "Catálogo y Diagnóstico del Motor de Reportes"
categoria: "sincronizacion-reportes"
submodulo: "reportes"
tipo_documento: "complemento-backend"
doc_complementario_app: "crear-informe"
proposito_soporte: "reglas-dinamicas-y-diagnostico"
version_minima_app: "2026.10.1"
fecha_actualizacion: "2026-10-22"
intenciones_y_sinonimos:
  - "como sacar un reporte de produccion de leche de las vacas de los ultimos meses"
  - "guiame paso a paso para crear un reporte de leche o hembras lactantes"
  - "que opciones y datos dinamicos aparecen en pantalla al crear un informe"
  - "que tipo de reporte o informe puedo sacar en la aplicacion"
  - "cuales son todos los reportes disponibles en control ganadero"
  - "por que mi reporte de ganado sale vacio o sin datos"
  - "como calcula el sistema la ganancia diaria de peso gdp o los dias abiertos"
  - "que parametros y columnas puedo elegir en cada reporte"
  - "como consultar el reporte de animales vendidos y el total de ventas o peso promedio"
  - "por que no me aparece el precio o el peso en el reporte de ventas de animales"
---

# Catálogo y Diagnóstico del Motor de Reportes

### Resumen y Alcance Funcional
El motor analítico de reportes pecuarios permite generar **15 modalidades de informes consolidados** para las **6 especies pecuarias soportadas** en la plataforma: bovinos, equinos, bufalinos, caprinos, ovinos y porcinos. Este servicio centralizado procesa los datos zootécnicos, sanitarios, productivos y comerciales de la finca activa, resolviendo las fórmulas de cálculo zootécnico y estructurando tablas personalizadas o formatos predeterminados listos para consulta y exportación a Excel y PDF.

- **Tipo de funcionalidad:** Catálogo analítico multiespecie, asistente de consulta guiada y motor de cálculo asíncrono en segundo plano.
- **¿Funciona sin conexión a internet (Modo Offline)?:** No. El módulo requiere conexión a internet activa para consultar las listas dinámicas de la finca (lotes, socios, hatos, compradores y razas registradas) y para enviar la orden de procesamiento a la nube.
- **Comportamiento de sincronización o procesamiento:**
  - *Recepción e Idempotencia:* La solicitud de creación del reporte se registra con un identificador único que previene solicitudes duplicadas en el servidor.
  - *Cola de Tareas en Segundo Plano:* El informe se registra en estado pendiente y se procesa asíncronamente en los servidores sin bloquear la navegación del usuario en la aplicación móvil.
  - *Filtrado Secuencial Multiespecie:* El motor evalúa los filtros seleccionados (especie activa, rama de reporte, categorías etarias, estados reproductivos, lotes o intervalos de fechas).
  - *Cálculo de Variables y Agregaciones:* El servidor resuelve las fórmulas zootécnicas individuales por animal y consolida totales y promedios globales.
  - *Disponibilidad Final:* Al finalizar el cálculo, el estado cambia a completado y el informe queda disponible en el historial de la explotación para visualización y descarga en formatos Excel y PDF.

### Reglas de Negocio, Criterios de Validación y Restricciones
- **Condiciones de Visibilidad y Habilitación por Especie Pecuaria:**
  - *Especies Lecheras (Bovinos, Bufalinos y Caprinos):* Habilitan las 5 modalidades de producción y consumo de leche (Listado de ordeños por día, Producción por potrero, Ventas de leche, Consumo de leche en crías y Consumo de concentrado) y la opción sanitaria de hembras con mastitis.
  - *Especies No Lecheras (Equinos, Porcinos y Ovinos):* Las opciones de ordeño y mastitis permanecen **estrictamente ocultas** en el menú del asistente. La plataforma adapta los filtros hacia inventario, crecimiento, pesajes, dietas, compras, ventas y proyecciones reproductivas según la especie activa.
  - *Funcionalidades Universales (Las 6 Especies):* Pesajes recientes y ganancia diaria de peso (GDP), dietas de alimentación (10 tipos), inventario físico cerrado, compras, ventas, lotes, propietarios y trazabilidad genealógica operan de forma idéntica en todas las especies.
  - *Módulos Especiales:* Los reportes de incidentes y seguridad pecuaria (Abigeato) son visibles únicamente si la finca tiene contratada y activa la función de seguridad.
- **Reglas de Selección Múltiple y Límites de Columnas (Plan Estándar vs Membresía PRO):**
  - En los reportes que solicitan configuración de columnas (Hembras, Machos, Lotes, Propietarios y Dietas), el sistema ofrece un catálogo de variables zootécnicas.
  - *Mínimo Obligatorio:* El usuario debe marcar al menos **2 parámetros** para habilitar la orden de creación.
  - *Límite Máximo en Plan Estándar / Gratuito:* El sistema permite seleccionar hasta un **máximo de 5 parámetros**. Al alcanzar 5 casillas marcadas, las demás opciones se bloquean temporalmente.
  - *Límite Ampliado con Membresía PRO:* Si la finca cuenta con suscripción activa, el tope máximo se amplía automáticamente a **hasta 11 parámetros simultáneos**.
  - *Inclusión Automática:* El código principal o arete del animal siempre se incluye por defecto en la tabla final sin descontar del cupo de parámetros del usuario.
- **Origen de Opciones en el Sistema:**
  - *Opciones Fijas del Catálogo Central:* Tipos de reportes principales, etapas etarias adaptadas por especie, estados reproductivos (Vacía, Preñada, Lactante, Seca), los 10 tipos de dieta, meses del año y atajos de fecha.
  - *Listas Dinámicas de la Finca Activa:* Nombres de lotes creados, nombres de socios/dueños registrados, nombres de hatos de ordeño, compradores de leche y razas presentes en los animales vivos de la finca.
- **Prerrequisitos de Ciclo de Vida y Estados:**
  - Para calificar en reportes de *Lactancia/Ordeño*, la hembra debe tener registrado un evento de parto exitoso previo en el sistema.
  - Para calcular la *Ganancia Diaria de Peso (GDP)*, el animal debe contar con al menos dos registros de peso en fechas distintas.
  - *Consolidación de Ventas de Animales y Métricas Comerciales:* Para el reporte de animales vendidos, el sistema consolida automáticamente cada transacción comercial registrando la fecha de venta, código del animal, comprador, peso registrado al momento de la venta y precio individual con su divisa. El sistema procesa tres tarjetas de métricas automáticas: Total de venta (suma de ingresos comerciales), Peso total (suma acumulada de peso de animales pesados) y Peso promedio (calculado dividiendo el peso total acumulado entre la cantidad de animales con pesaje registrado). Si un animal se comercializó sin pesaje o sin precio registrado, el sistema muestra el campo vacío sin distorsionar el cálculo del promedio ni el conteo de animales pesados.
- **Consecuencias Automáticas en el Sistema:** Al completarse la generación, el informe queda registrado en el historial de la finca, accesible para todos los usuarios con permisos de consulta.

### Parámetros y Campos Configurables
| Campo / Parámetro | ¿Es Fijo o Dinámico? | Valores Permitidos | Comportamiento e Impacto en el Sistema |
| :--- | :---: | :--- | :--- |
| "Tipo de Reporte Inicial" | Fijo del sistema | 15 modalidades autorizadas | Define la rama principal del árbol de decisiones y los filtros posteriores. |
| "Hato de Ordeño" | Dinámico de la finca | Hatos registrados + opción "Todos" | Filtra las mediciones de leche por grupo de ordeño. |
| "Lote / Potrero" | Dinámico de la finca | Lotes activos en la explotación | Restringe los animales o registros al potrero seleccionado. |
| "Comprador de Leche" | Dinámico de la finca | Clientes/Plantas registradas | Filtra los comprobantes de venta y liquidación de leche. |
| "Columnas Seleccionables" | Fijo del sistema | 2 a 5 variables (hasta 11 con PRO) | Define las variables personalizadas que integrarán la tabla final. |
| "Rango de Fechas" | Interactivo / Atajos | Desde $\le$ Hasta | Establece el período cronológico de consolidación de datos. |

### Descripción Detallada de la Funcionalidad, Variaciones y Desencadenadores

Esta sección desglosa exhaustivamente todas las rutas, opciones y ramificaciones que se desencadenan según la elección del usuario:

#### 1. Rama de Hembras (12 Opciones en el Menú de Selección)
Al seleccionar "Hembras" en la primera pregunta del asistente, el sistema despliega las siguientes **12 opciones de filtrado** (11 fijas de base y 1 especializada de sanidad lechera):

1. **Estado Reproductivo:** Permite segmentar las hembras por su condición ginecológica. Despliega un submenú con 3 alternativas:
   - *Preñadas / Cargadas:* Hembras con confirmación diagnóstica de preñez activa.
   - *Vacías:* Hembras abiertas sin diagnóstico de gestación.
   - *Pendientes de Confirmación:* Hembras servidas que aún no tienen chequeo reproductivo verificado.
   - *Desencadenador Posterior:* Solicita de 2 a 5 columnas informativas (hasta 11 con PRO).
2. **Etapa de Desarrollo:** Segmenta las hembras según su categoría etaria adaptada automáticamente por el sistema a la terminología oficial de la especie activa:
   - *Bovinos (Vacuno):* Ternera, Destetada, Novilla, Vaca adulta, Vaca vieja.
   - *Equinos (Caballar):* Potranca, Destetada, Yegua joven, Yegua adulta, Yegua vieja.
   - *Bufalinos:* Bufalita, Búfala destetada, Búfala joven, Búfala adulta, Búfala vieja.
   - *Caprinos (Cabras):* Cabrita, Destetada, Chivata, Cabra adulta, Cabra vieja.
   - *Ovinos (Ovejas):* Cordera, Destetada, Borrega, Oveja adulta, Oveja vieja.
   - *Porcinos (Cerdos / Granjas):* Lechona, Destetada, Marrana joven, Cerda adulta de cría, Cerda vieja.
   - *Desencadenador Posterior:* Pasa a la selección de columnas zootécnicas.
3. **Todas las Hembras:** Listado completo del inventario femenino activo en la finca sin filtros preliminares. Pasa de inmediato a la selección de columnas zootécnicas.
4. **Raza:** Carga dinámicamente las razas registradas entre las hembras de la explotación. *(Condición de desbloqueo: Si la lista aparece vacía, es porque ningún animal femenino tiene raza asignada en su ficha individual).*
5. **En Venta:** Relaciona a las hembras que están marcadas con bandera activa de comercialización en la explotación. Pasa inmediatamente al catálogo de variables seleccionables:
   - *Identificación y Biometría:* Nombre, chip electrónico, raza, código de raza, fecha de nacimiento, edad, fecha de registro.
   - *Peso y Ganancia:* Último peso registrado, fecha del último peso, promedio de ganancia diaria de peso (GDP), peso al nacer, peso al destete.
   - *Manejo y Dieta:* Lote o potrero actual, propietario/socio asignado, tipo de dieta/alimentación.
   - *Genealogía y Reproducción:* Estado reproductivo, fecha de último parto, total de partos, próximo parto estimado, días restantes para el parto, intervalo entre partos (IEP), fecha de última inseminación, días de gestación, días de lactancia, días promedio en ordeño, padre y madre del ejemplar.
6. **Próximas a Parir / Mes de Parto:** Despliega una lista con los **12 meses futuros proyectados** en el calendario según la fecha estimada de parto calculada para la especie. Al elegir el mes, avanza a la selección de columnas.
7. **Animales por Lote:** Despliega los lotes creados en la finca y filtra únicamente a las hembras que residen en el lote seleccionado. Solicita columnas.
8. **Animales por Propietario:** Despliega los socios o dueños registrados en la finca y lista a las hembras asociadas al propietario seleccionado. Solicita columnas.
9. **Animales por Peso:** Abre el selector numérico de rango de peso corporal (peso mínimo y máximo) para agrupar hembras dentro de ese intervalo biométrico. Solicita columnas.
10. **Hembras Vendidas:** Consulta histórica de hembras comercializadas y retiradas del inventario activo. Solicita columnas.
11. **Hembras Fallecidas:** Historial sanitario de mortalidad y bajas de hembras en la explotación. Solicita columnas.
12. **Animales con Mastitis (Opción Sanitaria Especial):** *(Condición de visibilidad: Solo aparece en especies lecheras como Bovinos, Bufalinos y Caprinos; en otras especies no se muestra).* Filtra las hembras con registro activo de alerta de mastitis clínica o subclínica para control veterinario. Solicita columnas.

#### 2. Rama de Machos (9 Opciones en el Menú de Selección)
Al seleccionar "Machos", el sistema habilita las siguientes **9 opciones de filtrado**:

1. **Etapa de Desarrollo:** Segmenta los machos según su edad y categoría zootécnica adaptada a la especie:
   - *Bovinos (Vacuno):* Ternero, Destetado, Novillo, Toro adulto, Toro viejo.
   - *Equinos (Caballar):* Potrillo, Destetado, Potro, Caballo adulto, Caballo viejo.
   - *Bufalinos:* Bufalito, Búfalo destetado, Búfalo joven, Búfalo adulto, Búfalo viejo.
   - *Caprinos (Cabras):* Cabrito, Destetado, Chivato, Cabro adulto, Cabro viejo.
   - *Ovinos (Ovejas):* Cordero, Destetado, Borrego, Carnero adulto, Carnero viejo.
   - *Porcinos (Cerdos / Granjas):* Lechón, Destetado, Cochinillo, Verraco adulto, Verraco viejo.
2. **Todos los Machos:** Inventario general masculino sin filtros intermedios; avanza directo a selección de columnas.
3. **Raza:** Carga dinámicamente las razas registradas en los machos de la finca.
4. **Animales por Lote:** Machos asignados a un potrero o lote determinado.
5. **Animales por Propietario:** Machos asociados a un socio o dueño específico.
6. **Animales por Peso:** Filtro por intervalo numérico de peso corporal.
7. **En Venta:** Machos marcados como disponibles para comercialización.
8. **Machos Vendidos:** Historial de machos transferidos o comercializados.
9. **Machos Fallecidos:** Historial de bajas y mortalidad en ejemplares machos.
- *Desencadenador Final de Machos:* Solicita de 2 a 5 columnas específicas de machos (hasta 11 con PRO), excluyendo automáticamente parámetros reproductivos femeninos y de producción lechera.

#### 3. Rama de Producción de Leche y Ordeño (Especies Lecheras)
- **Condición Obligatoria de Visibilidad:** Solo visible si la finca tiene activa una especie lechera (*Bovinos, Bufalinos, Caprinos*). En *Equinos*, *Porcinos* u *Ovinos* esta rama no aparece en el menú.
- **Variaciones:**
  - *Listado de Ordeños por Día:* Despliega los hatos de ordeño creados en la finca más la opción "Todos los hatos". Luego abre el selector de rango de fechas (con atajos: Hoy, Última semana, Este mes, Último mes). *(Formato fijo: no solicita columnas; entrega desglose AM/PM, totales diarios y promedio por animal).*
  - *Producción por Potrero:* Despliega los potreros de pastoreo de la finca y solicita rango de fechas para evaluar el rendimiento forrajero en leche.
  - *Ventas de Leche:* Despliega los compradores o plantas pasteurizadoras registradas en la finca y solicita rango de fechas. Desencadena reporte comercial con litros vendidos, precio unitario y valor liquidado.

#### 4. Rama de Animales por Tipo de Dieta / Alimentación (10 Categorías)
- **Desencadenador:** Seleccionar "Tipo de Dieta" en la primera pregunta del asistente.
- **Variaciones y Categorías del Sistema (10 Opciones de Alimentación):**
  Despliega el catálogo oficial con los **10 tipos de dieta zootécnica** soportados:
  1. *Pastoreo:* Animales alimentados exclusivamente a base de pastos en potrero.
  2. *Pastoreo + Concentrado:* Manejo mixto de pasturas con suplementación balanceada.
  3. *Heno:* Alimentación basada en pacas o rollos de heno seco.
  4. *Ensilaje:* Raciones de silo de maíz, sorgo o pasto fermentado.
  5. *Concentrado:* Dieta basada predominantemente en balanceados comerciales.
  6. *Suplementos:* Manejo con sales mineralizadas, melaza o bloques nutricionales.
  7. *Forraje:* Suministro de pastos de corte verde picado.
  8. *Raciones Totalmente Mezcladas (TMR):* Dietas unificadas formuladas integralmente.
  9. *Estabulación:* Animales en confinamiento total en corrales o establos.
  10. *Otros:* Cualquier otro esquema alimenticio no categorizado.
- **Desencadenador Posterior:** Filtra a todos los animales (machos y hembras) que tengan asignada esa alimentación y pasa a la **selección de columnas genéricas** (entre 2 y 5 parámetros, o hasta 11 con PRO), incluyendo variables de peso, ganancia diaria de peso (GDP), edad, lote y sexo del animal.

#### 5. Rama de Nutrición y Consumos Directos
- **Consumo de Leche en Crías:** Abre selector de rangos predefinidos (*Hoy, Última semana, Este mes, Último mes*) y consolida los litros de leche suministrados a terneros o infantes.
- **Consumo de Concentrado:** Abre selector de fechas y consolida los kilos de alimento concentrado suministrados por animal y lote.

#### 6. Rama de Animales por Lote y por Propietario (Generales)
- **Animales por Lote (General):** Despliega los lotes de la finca y permite generar un reporte consolidado mixto (machos y hembras) con selección de columnas genéricas más sexo del animal.
- **Animales por Propietario (General):** Despliega los socios registrados y genera el consolidado mixto de animales asociados a ese dueño con selección de columnas.

#### 7. Rama de Pesajes y Crecimiento
- **Pesajes Recientes:** Permite filtrar por *Machos*, *Hembras*, *Lote* o *Propietario*. Desencadena el cálculo de Ganancia Diaria de Peso (GDP) diferencial entre los dos pesajes más recientes de cada ejemplar y los días transcurridos entre ambas tomas.

#### 8. Rama de Transacciones Comerciales, Inventarios y Seguridad
- **Ventas de Animales (Animales Vendidos):**
  - *Desencadenador:* Seleccionar "Ventas de animales" en la primera pregunta del asistente.
  - *Comportamiento de Ejecución:* Generación directa sin selección de columnas. El motor extrae todas las ventas registradas para la especie activa en la explotación.
  - *Columnas de la Tabla de Resultados (5 Columnas Consolidadas):*
    1. *Fecha de venta:* Día y mes del comprobante de venta.
    2. *Código:* Arete o código identificador del animal comercializado.
    3. *Comprador:* Nombre del cliente o comprador registrado en la transacción.
    4. *Peso:* Peso corporal registrado del animal al momento de la venta, convertido automáticamente a la unidad de medida de peso configurada en la finca (Kilogramos o Libras). Si no se ingresó pesaje en la transacción, se presenta vacío.
    5. *Precio de venta:* Monto monetario individual pactado por el ejemplar con el símbolo y código de divisa correspondiente. Si no se registró valor monetario, se presenta vacío.
  - *Tarjetas de Resumen y Métricas Consolidadas:*
    1. *Total de venta:* Monto monetario total acumulado de todos los ingresos por animales vendidos en la consulta, formateado con la divisa correspondiente e ícono monetario verde.
    2. *Peso total:* Suma acumulada de los kilos o libras de todos los animales que registraron pesaje en la venta, con ícono de báscula azul.
    3. *Peso promedio:* Promedio zootécnico de peso por ejemplar vendido, calculado automáticamente dividiendo el peso total acumulado entre la cantidad de animales con registro de peso válido, con ícono de balanza azul. Si ningún ejemplar tiene pesaje registrado, refleja cero.
- **Compras de Animales:**
  - *Desencadenador:* Seleccionar "Compras de animales" en el asistente.
  - *Comportamiento de Ejecución:* Generación directa agrupada por fecha.
  - *Columnas de la Tabla:* Fecha de compra, cantidad de animales adquiridos, precio unitario por peso y total liquidado.
- **Inventario Físico:**
  - *Desencadenador:* Seleccionar "Inventario físico" en el asistente.
  - *Comportamiento de Ejecución:* Despliega la lista dinámica de inventarios físicos cerrados en la finca.
  - *Columnas de la Tabla:* Código del animal y Verificación en campo (Sí / No).
  - *Métricas Automáticas del Censo:* Filtro aplicado, método de verificación utilizado, fecha de cierre, usuario que realizó el inventario, duración de la jornada, total de animales censados, animales verificados (presentes) y animales no verificados (faltantes).
- **Inventario por Género y Edad:**
  - *Desencadenador:* Seleccionar "Inventario por género y edad" en el asistente.
  - *Comportamiento de Ejecución:* Generación directa que compila la pirámide poblacional del hato categorizada por sexo y rangos etarios.
- **Reportes de Abigeato / Incidentes de Seguridad:**
  - *(Condición de visibilidad: Solo visible si la finca tiene contratada y activa la función de seguridad).*
  - Despliega dos opciones de consulta: Historial de denuncias de hurto o Resumen consolidado de animales hurtados y recuperados.

### Diagnóstico Predictivo y Matriz de Errores Comunes
| Síntoma o Consulta del Ganadero | Causa Real en el Servidor / Finca | Explicación y Solución Sugerida por el Agente | Criterio de Escalamiento Humano |
| :--- | :--- | :--- | :--- |
| "No me aparece la opción de Listado de ordeños por día en el menú" | La finca tiene activa una especie no lechera (ej. Equinos, Porcinos u Ovinos) en la configuración superior de la app. | "Las opciones de ordeño solo se habilitan para especies lecheras (Bovinos, Bufalinos y Caprinos). Verifica en la barra superior de la app que tengas seleccionada la especie correspondiente." | Si la especie seleccionada es lechera y la opción continúa sin figurar en el menú. |
| "Al filtrar por Raza la lista me aparece vacía y no me deja continuar" | Ningún animal del inventario activo en el servidor tiene asignada una raza en su ficha individual. | "El filtro de razas consulta las razas registradas en los animales de tu finca. Si la lista está vacía, debes ingresar a la ficha de tus animales y asignarles su raza correspondiente." | Si los animales ya tienen raza asignada y sincronizada, pero la lista continúa vacía. |
| "El reporte de hembras en lactancia no incluye a animales que estoy ordeñando" | Las hembras no tienen registrado su evento de parto previo en el sistema, por lo que su estado no es 'Lactante'. | "Para que una hembra califique como lactante en los reportes, el sistema requiere que tenga registrado su evento de parto. Registra el parto correspondiente para actualizar su estado reproductivo." | Si el parto ya está registrado en la ficha del animal pero no es tomado por el reporte. |
| "El reporte de ordeño o pesajes sale con datos desactualizados o en ceros" | Las mediciones se ingresaron en el teléfono sin conexión y no han sincronizado a la base central. | "El motor de reportes procesa los datos alojados en la nube. Conecta tu teléfono a internet para que la sincronización en segundo plano actualice las mediciones antes de generar el informe." | Si tras verificar que los datos están sincronizados en el servidor el reporte persiste sin datos. |
| "El reporte de animales vendidos no muestra el peso o el precio de algunos ejemplares" | En el registro de venta del animal no se ingresó el peso de báscula o el precio unitario pactado. | "El reporte presenta el peso y precio ingresados en el comprobante de venta. Si se comercializó sin registrar pesaje o valor, el sistema deja la casilla en blanco. Puedes editar la venta en la app para ingresar estos datos." | Si el peso y precio están registrados en el comprobante de venta sincronizado pero no aparecen en el reporte. |
| "El peso promedio o el peso total en el reporte de ventas sale en cero" | Ninguno de los animales comercializados en la consulta cuenta con un pesaje registrado en su comprobante de venta. | "El sistema calcula el peso promedio y el peso total únicamente con los animales que tienen pesaje registrado. Si ninguno fue pesado al venderse, el total y promedio reflejan cero." | Si los animales vendidos tienen pesajes confirmados en el servidor pero el cálculo permanece en cero. |
| "Las ventas de ganado registradas hoy no aparecen en el reporte de animales vendidos" | Los comprobantes de venta se crearon en el teléfono sin conexión y no han sincronizado con la base central. | "El motor de reportes consolida las ventas sincronizadas en la nube. Conecta tu dispositivo a internet para que la sincronización en segundo plano actualice las ventas antes de generar el reporte." | Si tras confirmar la sincronización completa en el servidor las ventas continúan sin figurar. |
| "El reporte permanece en estado Pendiente / En Proceso por más de 15 minutos" | Sobrecarga temporal en la cola de tareas del servidor o volumen masivo de datos históricos. | "Tu reporte continúa en cola de procesamiento. Debido al volumen de registros históricos se ha demorado más de lo habitual. Puedes continuar usando la app mientras finaliza." | Si el reporte supera los **15 minutos continuos** sin pasar a completado ni fallido. |

### Directivas de Seguridad y Guardrails para el Agente de Soporte
- **Verificación de Sincronización Previa:** Ante cualquier reporte de *"faltan datos"* o *"no coincide el inventario"*, solicitar siempre al usuario que verifique si sus colaboradores sincronizaron los dispositivos móviles antes de sospechar de un fallo en el servidor.
- **Respeto a la Privacidad de la Explotación Ganadera:** La información consolidada de inventarios, costos de compra, compradores de leche e ingresos comerciales es estrictamente confidencial. Nunca compartir datos ni confirmar cifras con personas que no figuren como propietarios o administradores autorizados en la cuenta.
- **No Forzar Reintentos Masivos:** Si el servidor experimenta demoras en colas de procesamiento, orientar al usuario para que no genere múltiples solicitudes consecutivas del mismo reporte, ya que esto prolonga el tiempo de respuesta.
