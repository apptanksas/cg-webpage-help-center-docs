---
title: "Registro Masivo de Tratamientos"
modulo_id: "sanidad-registro-masivo-tratamientos"
nombre_funcionalidad: "Registro Masivo de Tratamientos"
tipo_documento: "guia-app"
categoria: "sanidad-reproduccion"
submodulo: "sanidad"
especies_aplicables: ["todas"]
version_minima_app: "2026.10.1"
confianza_reglas: "verificada-con-tests"
fecha_actualizacion: "2026-11-04"
intenciones_y_sinonimos:
  - "como aplicar un tratamiento a varios animales al mismo tiempo"
  - "registro masivo de medicamentos para el ganado"
  - "como curar o medicar un lote de animales"
  - "como registrar la dosis en tratamientos masivos"
  - "poner tratamiento a un grupo de vacas"
  - "registro en lote de sanidad y tratamientos"
---

# Registro Masivo de Tratamientos

### Resumen y Alcance Funcional
Permite registrar y aplicar un mismo tratamiento veterinario o protocolo de medicación a un grupo o lote completo de animales en una sola operación dentro de la finca. Esta funcionalidad agiliza el manejo sanitario en campo, permitiendo filtrar animales por especie o criterios específicos, definir la duración en días, el tipo de tratamiento, el diagnóstico, el medicamento administrado, la dosis aplicada con su unidad de medida y la enfermedad asociada, calculando automáticamente la fecha de inicio y de culminación del tratamiento para cada animal seleccionado.

- **Especies a las que aplica:** Aplica a todas las especies administradas en la aplicación: bovinos, bufalinos, equinos, caprinos, ovinos y porcinos.
- **¿Funciona sin conexión a internet (Modo Offline)?:** Sí.
- **Comportamiento de sincronización:** Los tratamientos aplicados en lote se guardan de forma instantánea en la base de datos local del dispositivo móvil. En cuanto el teléfono detecte conexión a internet (red móvil o Wi-Fi), los registros sanitarios se sincronizan automáticamente en segundo plano con el servidor de la finca.

### Reglas de Negocio y Restricciones
- **Permisos requeridos:** El usuario debe contar con permisos activos para registrar tratamientos en la finca. Si el rol del usuario no tiene asignado este privilegio, el sistema no permitirá guardar el registro masivo.
- **Selección obligatoria de animales:** Es indispensable seleccionar al menos un animal mediante el filtro de animales antes de procesar el registro. Si la lista resultante está vacía, el sistema impedirá el guardado y mostrará un mensaje de advertencia ("No hay animales seleccionados").
- **Tipo de animal:** Si la finca tiene configurada más de una especie animal (por ejemplo, bovinos, equinos o bufalinos), el selector de tipo de animal estará activo para elegir la especie correspondiente antes de aplicar el filtro. Si la finca maneja una sola especie, esta se selecciona automáticamente de forma predeterminada.
- **Campos obligatorios del tratamiento:**
    - **Fecha:** Fecha de inicio de la medicación (no se admiten fechas fuera del rango permitido ni años futuros no válidos).
    - **Días de tratamiento:** Número entero obligatorio comprendido entre 1 y 365 días. La fecha de finalización se calcula sumando estos días a la fecha de inicio.
    - **Tipo de tratamiento:** Clasificación obligatoria según el protocolo veterinario a aplicar.
    - **Medicamento:** Nombre del fármaco, antibiótico o compuesto sanitario suministrado.
- **Campos opcionales del tratamiento:**
    - **Dosis aplicada:** Campo numérico decimal para especificar la cantidad administrada a cada animal.
    - **Medida de dosis:** Selector desplegable con las unidades: "Mililitros" (ml) y "Miligramos" (mg).
    - **Nombre del tratamiento:** Identificador o nombre personalizado del protocolo médico.
    - **Enfermedad:** Patología o afección diagnosticada asociada al tratamiento.
    - **Diagnóstico:** Detalle clínico o descripción médica del diagnóstico.
    - **Notas u observaciones:** Comentarios adicionales o instrucciones de seguimiento.

### Flujo Paso a Paso para el Usuario
- **Ruta de acceso en la aplicación:** Pantalla principal de la finca > Botón flotante central con ícono de casa y suma (+) > Menú de opciones rápidas > Opción "Tratamiento / Vacunación" > Opción "Tratamiento masivo".

1. **Verificar el tipo de animal:**
    - En la parte superior del formulario, en el campo "Tipo de animal", verifique la especie sobre la cual aplicará el tratamiento (disponible si su finca administra múltiples especies).
2. **Definir el grupo de animales a tratar:**
    - Presione el selector "Seleccionar animales".
    - Configure los criterios del filtro (por ejemplo, por lote, potrero, etapa productiva, sexo o selección manual) para agrupar los animales que recibirán la medicación.
    - Al confirmar el filtro, el encabezado superior mostrará la cantidad en el indicador "Total de animales seleccionados".
3. **Ingresar la información del tratamiento:**
    - **Nombre del tratamiento (Opcional):** Digite un nombre de referencia para el tratamiento.
    - **Fecha:** Seleccione la fecha de inicio de la aplicación en el calendario (por defecto sugiere el día de hoy).
    - **Días de tratamiento:** Digite la cantidad de días que durará la medicación (valor entre 1 y 365).
    - **Tipo de tratamiento:** Despliegue el selector y elija la categoría correspondiente.
    - **Enfermedad (Opcional):** Elija la patología vinculada en caso de aplicar a una afección específica.
    - **Diagnóstico (Opcional):** Escriba el diagnóstico veterinario de los animales.
    - **Medicamento:** Ingrese el nombre comercial o principio activo del fármaco administrado.
    - **Dosis aplicada (Opcional):** Digite la dosis aplicada por ejemplar.
    - **Medida de dosis (Opcional):** Seleccione "Mililitros" o "Miligramos".
    - **Notas u observaciones (Opcional):** Redacte cualquier apunte clínico relevante sobre la aplicación.
4. **Guardar el registro masivo:**
    - Presione el botón "Registrar".
- **Pantalla de llegada tras guardar:** El sistema procesa y almacena el lote de tratamientos, retornando de forma automática e inmediata a la pantalla previa.

#### Etiquetas de la interfaz en otros idiomas
| Español | Inglés | Portugués |
| :--- | :--- | :--- |
| "Tratamiento masivo" | "Bulk Treatment" | "Tratamento em Massa" |
| "Total de animales seleccionados" | "Total animals selected" | "Total de animais selecionados" |
| "Tipo de animal" | "Animal type" | "Tipo de animal" |
| "Seleccionar animales" | "Select animals" | "Selecionar animais" |
| "Fecha" | "Date" | "Data" |
| "Días de tratamiento" | "Treatment Days" | "Dias de Tratamento" |
| "Tipo de tratamiento" | "Treatment Type" | "Tipo de Tratamento" |
| "Medicamento" | "Medicine" | "Medicamento" |
| "Dosis aplicada" | "Dose applied" | "Dose aplicada" |
| "Medida de dosis" | "Dose measure" | "Medida da dose" |
| "Mililitros" | "Milliliters" | "Mililitros" |
| "Miligramos" | "Milligrams" | "Miligramas" |
| "Registrar" | "Register" | "Registrar" |

### Matriz de Errores y Soluciones
| Mensaje en la App / Síntoma | Causa Real | Respuesta Sugerida por el Agente | Criterio de Escalamiento Humano |
| :--- | :--- | :--- | :--- |
| "No hay animales seleccionados" | Se intentó presionar el botón "Registrar" sin haber aplicado un filtro o el filtro configurado no contiene ningún animal activo | "Para registrar el tratamiento masivo, primero debe presionar 'Seleccionar animales' y elegir el grupo o los criterios de filtro deseados. Verifique que el filtro incluya al menos un animal antes de guardar." | No escalar. Guiar al usuario para configurar el filtro de animales. |
| El botón "Registrar" no responde o no permite enviar el formulario | Falta completar campos obligatorios como el medicamento, los días de tratamiento (debe ser entre 1 y 365), la fecha o el tipo de tratamiento | "Revise el formulario y asegúrese de haber completado todos los datos requeridos: el nombre del medicamento, los días de tratamiento (un número entre 1 y 365) y el tipo de tratamiento." | No escalar. Indicar al usuario que complete los campos obligatorios señalados. |
| "No tienes permisos para realizar esta acción" | El rol del usuario en la finca no cuenta con privilegios para registrar tratamientos sanitarios | "Su usuario no tiene permisos habilitados para crear tratamientos en esta finca. Solicite al propietario o administrador que le active los permisos de salud animal desde la gestión de trabajadores." | Si el administrador confirma que los permisos están asignados y el error persiste tras reiniciar la app, escalar a soporte técnico. |

### Directivas de Seguridad y Guardrails
- NUNCA solicite contraseñas, pines de acceso o códigos temporales a los usuarios por WhatsApp o canales de soporte.
- Los agentes de soporte no deben recetar dosis farmacológicas, indicar medicamentos veterinarios específicos ni alterar planes de tratamiento sin indicación expresa del médico veterinario de la finca.
- No modifique historiales sanitarios ni tratamientos aplicados directamente en bases de datos sin la autorización explícita del propietario de la finca.
