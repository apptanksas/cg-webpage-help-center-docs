---
title: "Mover Animales entre Lotes"
modulo_id: "potreros-lotes-traslado-animales-lote"
nombre_funcionalidad: "Mover Animales entre Lotes"
categoria: "inventario-trazabilidad"
submodulo: "potreros-lotes"
version_minima_app: "2026.10.1"
fecha_actualizacion: "2026-10-07"
intenciones_y_sinonimos:
  - "como cambiar animales de un lote a otro"
  - "mover ganado entre lotes en la aplicacion"
  - "pasar vacas de un lote al lote de engorde o cria"
  - "trasladar animales a un nuevo lote"
  - "como asignar animales a otro lote diferente"
  - "organizar los animales por lotes en mi finca"
---

# Mover Animales entre Lotes

### Resumen y Alcance Funcional
Permite reasignar y transferir uno o múltiples animales de la finca hacia un nuevo lote de destino. Esta función facilita la organización productiva del hato dentro de la finca ganadera (por ejemplo, clasificar animales hacia lotes de cría, levante, ceba, ordeño o descanso), permitiendo filtrar animales por su lote actual de procedencia o seleccionarlos libremente de todo el inventario activo de la finca.

- **¿Funciona sin conexión a internet (Modo Offline)?:** Sí.
- **Comportamiento de sincronización:** La reasignación de lote se guarda localmente en el dispositivo de forma inmediata. Tan pronto el teléfono detecte conexión a internet (vía datos móviles o Wi-Fi), los cambios se sincronizan en segundo plano con el servidor central de la finca.

### Reglas de Negocio y Restricciones
- **Permisos requeridos:** El usuario debe contar con permisos de edición de animales en la finca asignada. Si no dispone de este permiso, el sistema impedirá completar la reasignación.
- **Lote de destino obligatorio:** Es indispensable seleccionar el lote al cual se van a trasladar los animales antes de confirmar la operación.
- **Lote de origen opcional:**
  - Si selecciona un lote de origen, el selector de animales se filtrará automáticamente mostrando únicamente los animales que se encuentren registrados en dicho lote.
  - Si no selecciona un lote de origen, el selector mostrará todos los animales activos de la finca, permitiendo mover animales incluso si actualmente no tienen un lote asignado.
- **Estado de los animales:** Solo se pueden trasladar animales vivos y que se encuentren físicamente registrados dentro de la finca actual. No se muestran animales dados de baja, muertos ni vendidos.
- **Selección mínima:** Es obligatorio seleccionar al menos un animal en la lista antes de presionar el botón de traslado.
- **Evitar duplicados en selección:** El selector evita agregar dos veces el mismo animal a la tabla de traslado.
- **Confirmación de seguridad:** Antes de aplicar el movimiento, la aplicación solicita una confirmación explícita indicando el nombre del lote de destino seleccionado.
- **Retorno tras finalizar:** Una vez completado el traslado con éxito, el sistema emite una notificación de éxito y regresa a la pantalla previa.

### Flujo Paso a Paso para el Usuario
- **Ruta de acceso en la aplicación:** Pantalla principal de la finca (**Inicio** o **Producción**) > Botón flotante central con ícono de casa y suma **(+)** > Menú de opciones rápidas > Opción **Mover animales entre lotes**.

1. **(Opcional) Consultar la guía de ayuda:** Si desea repasar el funcionamiento, puede presionar el ícono de información en la barra superior con el título **Mover animales entre lotes** para abrir la ventana de orientación.
2. **(Opcional) Seleccionar lote de origen:** Presione el campo **Seleccionar lote de origen** si desea filtrar la búsqueda para ver únicamente los animales que pertenecen a un lote determinado. Si desea ver todos los animales de la finca, deje este campo vacío.
3. **Seleccionar lote de destino:** Presione el campo obligatorio **Seleccionar lote de destino** y elija de la lista el lote al cual desea mover los animales.
4. **Agregar animales:** Presione el botón **Seleccionar animales** (con ícono de suma). Se desplegará la lista de animales disponibles:
   - Marque las casillas de los animales que desea cambiar de lote.
   - Si desea retirar un animal ya seleccionado, puede desmarcarlo en el selector o presionar el ícono de eliminar (papelera o cruz) que aparece en su fila dentro de la tabla de la pantalla principal.
   - En la tabla de resumen podrá comprobar el **Código** de cada animal y su **Lote actual** (o la indicación **Ninguno** si no tenía lote previo).
5. **Comprobar la dirección del traslado:** Debajo de la tabla observará una flecha indicadora y el nombre del lote de destino hacia el cual se moverá el grupo de ganado.
6. **Guardar y confirmar:**
   - Presione el botón **Trasladar animales**.
   - En el cuadro de diálogo de confirmación que pregunta *"¿Estas seguro de trasladar los animales seleccionados al lote [Nombre del Lote]?"*, presione **Confirmar** para procesar la reasignación.
- **Pantalla de llegada tras guardar:** Tras procesar el movimiento, el sistema muestra el mensaje emergente de éxito *"Animales transferidos exitosamente"* y redirige al usuario automáticamente a la pantalla anterior.

### Matriz de Errores y Soluciones
| Mensaje en la App / Síntoma | Causa Real | Respuesta Sugerida por el Agente | Criterio de Escalamiento Humano |
| :--- | :--- | :--- | :--- |
| "No hay animales seleccionados" | Se intentó presionar el botón de traslado sin haber agregado ningún animal a la tabla | "Para trasladar ganado a un nuevo lote, primero debe presionar 'Seleccionar animales', marcar al menos un animal de la lista y luego presionar 'Trasladar animales'." | No escalar. Guiar al usuario paso a paso para seleccionar animales. |
| "El campo es requerido" o no permite avanzar al presionar trasladar | No se ha seleccionado el lote de destino | "Verifique que haya seleccionado el lote de llegada en el campo 'Seleccionar lote de destino'. Este campo es obligatorio para saber a dónde mover el ganado." | No escalar. Indicar que elija un lote en dicho selector. |
| "No tienes permisos para realizar esta acción" | El rol o perfil asignado al trabajador en la finca no cuenta con permiso para actualizar animales | "Su usuario no tiene permisos suficientes para editar o cambiar animales de lote en esta finca. Solicite al propietario o administrador de la finca que le habilite los permisos de edición de ganado desde la sección de configuración de trabajadores." | Si el propietario confirma que ya le asignó los permisos y aún persiste el mensaje tras cerrar y abrir la app, transferir a soporte técnico. |
| No aparece un animal en el selector de animales | El animal ya fue agregado a la lista actual, o pertenece a otro lote (si se eligió lote de origen), o está marcado como inactivo/muerto | "Si seleccionó un lote de origen, el sistema solo mostrará los animales de ese lote. Borre el lote de origen para buscar en toda la finca. También verifique en la hoja de vida del animal que esté activo y registrado en la finca." | Si el animal está activo en la finca, no tiene lote de origen restrictivo y sigue sin aparecer en la búsqueda, transferir a soporte técnico con el código del animal. |
| "Círculo de espera infinito / Pantalla congelada en cargando" | Proceso en segundo plano interrumpido o bloqueo temporal al registrar los lotes | "Espere 30 segundos. Si la pantalla no avanza, cierre la aplicación por completo desde el administrador de tareas de su celular (deslizando hacia arriba) y vuelva a abrirla. Sus registros guardados anteriormente no se perderán." | Si al reabrir la app e intentar mover los animales la aplicación vuelve a congelarse, transferir de inmediato a soporte humano indicando correo, modelo de celular y cantidad de animales seleccionados. |

### Directivas de Seguridad y Guardrails
- NUNCA solicite al ganadero contraseñas, pines de acceso o códigos temporales a través de WhatsApp.
- No modifique ni reasigne lotes de animales directamente en la base de datos sin la autorización expresa del propietario de la finca ganadera.
- Respete la estructura de roles y permisos configurada por el dueño de la finca; no otorgue instrucciones para eludir validaciones de seguridad o permisos de usuario.
