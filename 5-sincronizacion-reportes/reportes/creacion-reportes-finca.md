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
fecha_actualizacion: "2026-10-14"
intenciones_y_sinonimos:
  - "como sacar un reporte de produccion de leche de las vacas de los ultimos meses"
  - "guiame paso a paso para crear un reporte de leche o hembras lactantes"
  - "que opciones y datos dinamicos aparecen en pantalla al crear un informe"
  - "que tipo de reporte o informe puedo sacar en la aplicacion"
  - "cuales son todos los reportes disponibles en control ganadero"
  - "por que mi reporte de ganado sale vacio o sin datos"
  - "como calcula el sistema la ganancia diaria de peso gdp o los dias abiertos"
  - "que parametros y columnas puedo elegir en cada reporte"
---

# Catálogo y Diagnóstico del Motor de Reportes

### Resumen y Alcance Funcional
Este documento describe el catálogo exhaustivo de los **15 tipos de reportes analíticos**, cómo funciona el asistente interactivo paso a paso, qué opciones y listas dinámicas se cargan desde el servidor según la finca, y cómo opera el motor de cálculo del servidor central. Proporciona a los agentes de soporte la capacidad de guiar al ganadero con precisión exacta según el objetivo productivo deseado (ej. producción de leche, pesajes, reproducción o inventarios).

- **Tipo de funcionalidad:** Catálogo analítico, asistente guiado y servicio de cómputo en segundo plano.
- **¿Funciona sin conexión a internet (Modo Offline)?:** No. El asistente requiere conexión activa para consultar las listas dinámicas de la finca (hatos, lotes, razas presentes, compradores) y el servidor procesa los reportes sobre datos previamente sincronizados en la nube.
- **Comportamiento de sincronización o procesamiento:**
  1. **Recepción e Idempotencia:** La solicitud llega al servidor con un identificador único que previene duplicados.
  2. **Cola de Tareas en Segundo Plano:** El reporte se crea en estado *Pendiente* y se asigna a una cola de cálculo sin bloquear el teléfono móvil.
  3. **Evaluación de Nodos y Filtrado:** El motor ejecuta secuencialmente los filtros seleccionados (especie $\rightarrow$ tipo de reporte $\rightarrow$ filtros específicos de raza, etapa, lote, fechas o estado reproductivo).
  4. **Cálculo de Variables y Agregaciones:** Se resuelven las fórmulas individuales por animal y se consolidan las métricas totales y promedios zootécnicos.
  5. **Finalización:** El reporte cambia su estado a *Completado* (o *Fallido* si los datos presentan inconsistencias críticas), quedando listo para visualización y exportación a Excel / PDF.

### Reglas de Negocio, Criterios de Validación y Restricciones
- **Condiciones de Visibilidad y Habilitación:**
  - *Especies Lecheras:* Las opciones de producción y consumo de leche (Listado de ordeños por día, Producción por potrero, Ventas de leche, Consumo de leche en crías y Consumo de concentrado) solo se habilitan para Bovinos, Bufalinos, Ovinos y Caprinos. En Equinos o Porcinos no aparecen disponibles.
  - *Módulos Especiales:* Los reportes de incidentes y seguridad pecuaria (Abigeato) solo son visibles si la finca tiene habilitado el módulo de seguridad.
- **Reglas de Selección Múltiple y Límites de Columnas (Plan Estándar vs Membresía PRO):**
  - En todos los reportes con selección de columnas (Hembras, Machos, Lotes, Propietarios), el sistema presenta un catálogo amplio de variables zootécnicas (hasta 29 parámetros en hembras y 19 en machos/lotes).
  - *Mínimo Obligatorio:* El usuario debe seleccionar al menos **2 parámetros** para habilitar la creación del informe.
  - *Límite Máximo en Plan Estándar / Gratuito:* El sistema restringe la selección a un **máximo de 5 parámetros**. Una vez alcanzado el tope de 5 casillas marcadas, las opciones restantes se bloquean para evitar sobrecarga en la tabla.
  - *Límite Máximo con Membresía / Suscripción PRO:* Si la finca cuenta con una membresía activa, el tope máximo se amplía automáticamente a **hasta 11 parámetros simultáneos**.
  - *Inclusión Automática:* El código principal o arete del animal siempre se incluye por defecto sin descontar del límite de parámetros del usuario.
- **Origen de Opciones en Pantalla:**
  - *Fijas del Sistema:* Tipos de reportes principales, etapas de desarrollo (*Ternera, Novilla, Vaca, Ternero, Torete, Toro, Buey*), estados reproductivos (*Vacía, Preñada, Lactante, Seca*), meses del año y rangos predefinidos de fechas.
  - *Dinámicas de la Finca:* Nombres de lotes creados, nombres de socios/propietarios, nombres de hatos de ordeño, compradores de leche y razas presentes en el inventario.
- **Prerrequisitos de Ciclo de Vida y Estados:**
  - Para figurar en reportes de *Lactancia/Ordeño*, la hembra debe tener registrado un evento de parto previo.
  - Para calcular la *Ganancia Diaria de Peso (GDP)*, el animal debe tener al menos dos pesajes en fechas distintas.
- **Consecuencias Automáticas en el Sistema:** Al concluir la generación, el reporte se almacena en el historial de la finca y queda disponible para descarga en Excel y PDF.

### Parámetros y Campos Configurables
| Campo / Parámetro | ¿Es Fijo o Dinámico? | Valores Permitidos | Comportamiento e Impacto en el Sistema |
| :--- | :---: | :--- | :--- |
| "Tipo de Reporte Inicial" | Fijo del sistema | 15 modalidades autorizadas | Determina la rama del árbol de decisión y los filtros posteriores. |
| "Hato de Ordeño" | Dinámico de la finca | Hatos creados + opción "Todos" | Filtra los registros de producción lechera por grupo de manejo. |
| "Lote / Potrero" | Dinámico de la finca | Lotes activos en la finca | Restringe los animales o mediciones al potrero seleccionado. |
| "Comprador de Leche" | Dinámico de la finca | Clientes/Plantas registradas | Filtra los comprobantes de venta y liquidación de leche. |
| "Columnas Seleccionables" | Fijo del sistema | 2 a 5 variables marcadas | Define las columnas personalizadas que integrarán la tabla final. |
| "Rango de Fechas" | Interactivo / Atajos | Desde $\le$ Hasta | Establece el período cronológico de consolidación de datos. |

### Descripción Detallada de la Funcionalidad, Variaciones y Desencadenadores

Esta sección desglosa exhaustivamente todas las rutas, opciones y ramificaciones que se desencadenan según la elección del ganadero en la aplicación:

#### 1. Rama de Hembras (12 Opciones en el Menú de Selección)
Al seleccionar "Hembras" en la primera pregunta del asistente, el sistema despliega las siguientes **12 opciones de filtrado** (11 fijas de base y 1 especializada de sanidad lechera):

1. **Estado Reproductivo:** Permite segmentar las hembras por su condición ginecológica. Al elegir esta opción, abre un submenú con 3 alternativas:
   - *Preñadas / Cargadas:* Hembras con confirmación diagnóstica de preñez activa.
   - *Vacías:* Hembras abiertas sin diagnóstico de gestación.
   - *Pendientes de Confirmación:* Hembras servidas que aún no tienen chequeo reproductivo verificado.
   - *Desencadenador Posterior:* Solicita de 2 a 5 columnas informativas.
2. **Etapa de Desarrollo:** Segmenta las hembras según su categoría etaria y de crecimiento adaptada a la especie pecuaria (*Ternera, Destetada, Novilla, Vaca adulta, Vaca vieja*). Desencadena la selección de 2 a 5 columnas.
3. **Todas las Hembras:** Listado completo del inventario femenino activo en la finca sin filtros preliminares. Pasa de inmediato a la selección de 2 a 5 columnas zootécnicas.
4. **Raza:** Carga dinámicamente las razas registradas entre las hembras de la explotación. *(Condición de desbloqueo: Si la lista aparece vacía, es porque ningún animal femenino tiene raza asignada en su ficha individual).*
5. **En Venta:** Relaciona a las hembras que están marcadas con bandera activa de comercialización en la explotación. Al seleccionar esta opción, el sistema filtra a las hembras disponibles para venta y avanza inmediatamente al catálogo de **variables y parámetros seleccionables**, donde el usuario puede combinar libremente desde **mínimo 2 y hasta 5 parámetros en plan estándar (o hasta 11 con membresía PRO)** entre las opciones disponibles:
   - *Parámetros Biométricos y de Identificación:* Nombre, código de chip electrónico, raza, código de raza, fecha de nacimiento, edad, fecha de registro.
   - *Parámetros de Peso y Ganancia:* Último peso registrado, fecha del último peso, promedio de ganancia diaria de peso (GDP), peso al nacer, peso al destete.
   - *Parámetros de Manejo y Ubicación:* Lote o potrero actual, propietario o socio asignado, tipo de dieta/alimentación.
   - *Parámetros Reproductivos y Lecheros:* Estado reproductivo, fecha de último parto, número de partos, próximo parto estimado, días restantes para el parto, intervalo entre partos (IEP), fecha de última inseminación, días de gestación, días de lactancia, días promedio en ordeño, padre y madre del ejemplar.
6. **Próximas a Parir / Mes de Parto:** Despliega una lista con los **12 meses futuros proyectados** (ej. *Octubre 2026, Noviembre 2026, etc.*) según el cálculo de fecha estimada de parto (días de gestación). Al elegir el mes, avanza a la selección de columnas.
7. **Animales por Lote:** Despliega los lotes o potreros creados en la finca y filtra únicamente a las hembras que pastorean o residen en el lote seleccionado. Solicita de 2 a 5 columnas.
8. **Animales por Propietario:** Despliega los socios o propietarios registrados en la finca y lista a las hembras asociadas al dueño seleccionado. Solicita de 2 a 5 columnas.
9. **Animales por Peso:** Abre el selector numérico de rango de peso corporal (peso mínimo y máximo) para agrupar hembras dentro de ese intervalo biométrico. Solicita de 2 a 5 columnas.
10. **Hembras Vendidas:** Consulta histórica de hembras comercializadas y retiradas del inventario activo. Solicita de 2 a 5 columnas.
11. **Hembras Fallecidas:** Historial sanitario de mortalidad y bajas de hembras en la explotación. Solicita de 2 a 5 columnas.
12. **Animales con Mastitis (Opción Sanitaria Especial):** *(Condición de visibilidad: Solo aparece en especies lecheras como Bovinos, Bufalinos y Caprinos; en otras especies no se muestra).* Filtra las hembras con registro activo de alerta de mastitis clínica o subclínica para control veterinario. Solicita de 2 a 5 columnas.

#### 2. Rama de Machos (9 Opciones en el Menú de Selección)
Al seleccionar "Machos", el sistema habilita las siguientes **9 opciones de filtrado**:

1. **Etapa de Desarrollo:** Segmenta los machos según su edad y categoría zootécnica (*Ternero, Destetado, Torete, Toro adulto, Buey / Castrado*).
2. **Todos los Machos:** Inventario general masculino sin filtros intermedios; avanza directo a selección de columnas.
3. **Raza:** Carga dinámicamente las razas registradas en los machos de la finca.
4. **Animales por Lote:** Machos asignados a un potrero o lote determinado.
5. **Animales por Propietario:** Machos asociados a un socio o dueño específico.
6. **Animales por Peso:** Filtro por intervalo numérico de peso corporal.
7. **En Venta:** Machos marcados como disponibles para comercialización.
8. **Machos Vendidos:** Historial de machos transferidos o comercializados.
9. **Machos Fallecidos:** Historial de bajas y mortalidad en ejemplares machos.
- *Desencadenador Final de Machos:* Solicita de 2 a 5 columnas específicas de machos, excluyendo de forma automática parámetros ginecológicos o de producción lechera.

#### 3. Rama de Producción de Leche y Ordeño
- **Condición Obligatoria de Visibilidad:** Solo visible si la finca tiene activa una especie lechera (*Bovinos, Bufalinos, Ovinos, Caprinos*). En *Equinos* o *Porcinos* esta rama no aparece.
- **Variaciones:**
  - *Listado de Ordeños por Día:* Despliega los hatos de ordeño creados en la finca más la opción "Todos los hatos". Luego abre el selector de rango de fechas (con atajos: Hoy, Última semana, Este mes, Último mes). *(Formato fijo: no solicita columnas; entrega desglose AM/PM, totales y promedio por vaca).*
  - *Producción por Potrero:* Despliega los potreros de pastoreo de la finca y solicita rango de fechas para evaluar el rendimiento forrajero en leche.
  - *Ventas de Leche:* Despliega los compradores o plantas pasteurizadoras registradas en la finca y solicita rango de fechas. Desencadena reporte comercial con litros vendidos, precio unitario y valor liquidado.

#### 4. Rama de Animales por Tipo de Dieta / Alimentación
- **Desencadenador:** Seleccionar "Tipo de Dieta" en la primera pregunta del asistente.
- **Variaciones y Categorías del Sistema (10 Opciones de Alimentación):**
  Al ingresar a esta rama, el sistema despliega el catálogo oficial con los **10 tipos de dieta zootécnica** para segmentar los animales de la finca:
  1. *Pastoreo:* Animales alimentados exclusivamente a base de pastos en potrero.
  2. *Pastoreo + Concentrado:* Manejo mixto de forraje verde con raciones de concentrado.
  3. *Heno:* Alimentación basada en pacas o rollos de heno seco.
  4. *Ensilaje:* Raciones de silo de maíz, sorgo o pasto fermentado.
  5. *Concentrado:* Dieta basada predominantemente en balanceados comerciales.
  6. *Suplementos:* Manejo con sales mineralizadas, melaza o bloques nutricionales.
  7. *Forraje:* Suministro de pastos de corte verde picado.
  8. *Raciones Totalmente Mezcladas (TMR):* Dietas unificadas formuladas integralmente.
  9. *Estabulación:* Animales en confinamiento total en corrales o establos.
  10. *Otros:* Cualquier otro esquema alimenticio no categorizado.
- **Desencadenador Posterior:** Tras elegir el tipo de dieta, el sistema filtra a todos los animales (machos y hembras) que tengan asignada esa alimentación y pasa a la **selección múltiple de columnas genéricas** (entre 2 y 5 parámetros en plan estándar, o hasta 11 con membresía PRO), incluyendo la columna de género/sexo y variables de peso, GDP y edad.

#### 5. Rama de Nutrición y Consumos Directos
- **Consumo de Leche en Crías:** Abre selector de rangos predefinidos (*Hoy, Última semana, Este mes, Último mes*) y consolida los litros de leche suministrados a terneros o infantes.
- **Consumo de Concentrado:** Abre selector de fechas y consolida los kilos de alimento concentrado suministrados por animal y lote.

#### 6. Rama de Animales por Lote y por Propietario (Generales)
- **Animales por Lote (General):** Despliega los lotes de la finca y permite generar un reporte consolidado mixto (machos y hembras) con selección de 2 a 5 parámetros genéricos más sexo del animal.
- **Animales por Propietario (General):** Despliega los socios registrados y genera el consolidado mixto de animales asociados a ese dueño con selección de 2 a 5 parámetros.

#### 7. Rama de Pesajes y Crecimiento
- **Pesajes Recientes:** Permite filtrar por *Machos*, *Hembras*, *Lote* o *Propietario*. Desencadena el cálculo de Ganancia Diaria de Peso (GDP) diferencial entre los dos pesajes más recientes de cada ejemplar y los días transcurridos entre ambas tomas.

#### 8. Rama de Transacciones Comerciales, Inventarios y Seguridad
- **Compras de Animales y Ventas de Animales:** Generación directa sin selección de columnas. Desencadena resumen financiero de compras/ventas, valores monetarios y procedencias/destinos.
- **Inventario Físico:** Despliega la lista dinámica de inventarios físicos cerrados en la finca. Desencadena tabla de conciliación (animales presentes, faltantes, no leídos y novedades).
- **Inventario por Género y Edad:** Generación directa que compila la pirámide poblacional del hato categorizada por sexo y rangos de edad.
- **Reportes de Abigeato / Incidentes de Seguridad:** *(Condición de visibilidad: Solo visible si la finca tiene activo el módulo de seguridad pecuaria).* Permite consultar el historial de denuncias o el resumen de animales hurtados y recuperados.

### Diagnóstico Predictivo y Matriz de Errores Comunes
| Síntoma o Consulta del Ganadero | Causa Real en el Backend / Finca | Explicación y Solución Sugerida por el Agente | Criterio de Escalamiento Humano |
| :--- | :--- | :--- | :--- |
| "No me aparece la opción de Listado de ordeños por día en el menú" | La finca tiene activa una especie no lechera (ej. Equinos, Porcinos) o la especie no está clasificada como ordeñable. | "Las opciones de ordeño solo se habilitan para especies lecheras (Bovinos, Bufalinos, Ovinos y Caprinos). Verifica en la barra superior de la app que tengas seleccionada la especie bovina." | Si la especie seleccionada es bovina y la opción sigue sin figurar en el menú. |
| "Al filtrar por Raza la lista me aparece vacía y no me deja continuar" | Ningún animal del inventario activo en el servidor tiene asignada una raza en su ficha individual. | "El filtro de razas consulta las razas registradas en los animales de tu finca. Si la lista está vacía, debes ingresar a la ficha de tus animales y asignarles su raza correspondiente." | Si los animales ya tienen raza asignada y sincronizada, pero la lista continúa vacía. |
| "El reporte de hembras en lactancia no incluye a vacas que estoy ordeñando" | Las vacas no tienen registrado su evento de parto previo en el sistema, por lo que su estado no es 'Lactante'. | "Para que una vaca califique como lactante en los reportes, el sistema requiere que tenga registrado su evento de parto. Registra el parto correspondiente para actualizar su estado reproductivo." | Si el parto ya está registrado en la ficha del animal pero no es tomado por el reporte. |
| "El reporte de ordeño o pesajes sale con datos desactualizados o en ceros" | Los ordeños o pesajes se ingresaron en el teléfono sin conexión y no han sincronizado a la base central. | "El motor de reportes procesa los datos alojados en la nube. Conecta tu teléfono a internet para que la sincronización en segundo plano actualice las mediciones antes de generar el informe." | Si tras verificar que los datos están sincronizados en el servidor el reporte persiste sin datos. |
| "El reporte permanece en estado Pendiente / En Proceso por más de 15 minutos" | Sobrecarga temporal en la cola de tareas del servidor o volumen masivo de datos históricos. | "Tu reporte continúa en cola de procesamiento. Debido al volumen de registros históricos se ha demorado más de lo habitual. Puedes continuar usando la app mientras finaliza." | Si el reporte supera los **15 minutos continuos** sin pasar a completado ni fallido. |

### Directivas de Seguridad y Guardrails para el Agente de Soporte
- **Verificación de Sincronización Previa:** Ante cualquier reporte de *"faltan datos"* o *"no coincide el inventario"*, solicitar siempre al usuario que verifique si sus colaboradores sincronizaron los dispositivos móviles antes de sospechar de un fallo en el servidor.
- **Respeto a la Privacidad de la Explotación Ganadera:** La información consolidada de inventarios, costos de compra, compradores de leche e ingresos comerciales es estrictamente confidencial. Nunca compartir datos ni confirmar cifras con personas que no figuren como propietarios o administradores autorizados en la cuenta.
- **No Forzar Reintentos Masivos:** Si el servidor experimenta demoras en colas de procesamiento, orientar al usuario para que no genere múltiples solicitudes consecutivas del mismo reporte, ya que esto prolonga el tiempo de respuesta.
