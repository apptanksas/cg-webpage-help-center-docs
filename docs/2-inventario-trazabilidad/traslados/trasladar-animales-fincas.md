---
title: "Traslado de Animales entre Fincas"
modulo_id: "traslados-trasladar-animales-fincas"
nombre_funcionalidad: "Traslado de Animales entre Fincas Propias"
categoria: "inventario-trazabilidad"
submodulo: "traslados"
version_minima_app: "2026.10.1"
fecha_actualizacion: "2026-10-06"
intenciones_y_sinonimos:
  - "como pasar animales a otra de mis fincas"
  - "trasladar ganado entre mis fincas"
  - "cambiar vacas de una finca a otra finca propia"
  - "no me sale la opcion de trasladar animales entre fincas"
  - "mover lote de animales a otra propiedad"
  - "transferir ganado entre predios"
---

# Traslado de Animales entre Fincas Propias

### Resumen y Alcance Funcional
Módulo operativo que permite transferir ejemplares de forma masiva o individual desde la finca activa actual hacia otra finca ganadera perteneciente a la misma cuenta del propietario en Control Ganadero. Esta funcionalidad garantiza la continuidad de la trazabilidad zootécnica e histórica del animal al cambiar de predio físico, asignando automáticamente los ejemplares seleccionados al inventario de la finca receptora sin necesidad de registrarlos nuevamente.

- **¿Funciona sin conexión a internet (Modo Offline)?:** No.
- **Comportamiento de sincronización:** Requiere conexión a internet activa y obligatoria en todo momento. La consulta de fincas propias de destino y el procesamiento del traslado entre fincas se efectúan en tiempo real contra los servidores centrales de Control Ganadero.

### Reglas de Negocio y Restricciones
- **Propiedad de la finca de origen:** El usuario debe ser el propietario registrado de la finca activa actual.
- **Disponibilidad de múltiples fincas propias:** La opción en el menú solo está disponible si la cuenta del usuario tiene registradas más de 1 finca propia (al menos una finca de origen y una finca de destino distinta). Si el ganadero administra una sola finca, la opción no se mostrará en las acciones rápidas.
- **Permisos requeridos por rol:** Se requiere contar con el permiso explícito para registrar traslados de animales en la finca.
- **Conectividad a internet obligatoria:** La pantalla no permite operar de manera local ni sin conexión activa a datos móviles o red WiFi. Cualquier intento de apertura o traslado sin internet bloquea el proceso informando el error de comunicación.
- **Finca de destino:**
  - El selector de finca receptora excluye automáticamente la finca activa de origen, mostrando únicamente las demás fincas propias del ganadero.
  - El sistema preselecciona por defecto la primera finca de destino disponible de la lista.
- **Selección de animales y estado sanitario:**
  - Solo se pueden seleccionar animales que se encuentren físicamente en la finca activa de origen.
  - El selector excluye de forma automática a los animales fallecidos o dados de baja.
  - Los animales ya agregados a la lista del traslado actual quedan excluidos del diálogo de selección para impedir registros duplicados.
- **Requisito mínimo de animales:** Es estrictamente obligatorio incluir al menos 1 animal en el listado para poder ejecutar el traslado.
- **Confirmación de seguridad obligatoria:** Antes de procesar la solicitud, el sistema despliega un mensaje modal de confirmación indicando el nombre de la finca de destino seleccionada para prevenir traslados accidentales.
- **Resultado post-traslado:** Tras confirmarse el traslado con éxito en los servidores, la aplicación notifica el resultado satisfactorio y regresa a la pantalla anterior. Los animales trasladados dejan de figurar en el inventario de la finca de origen y quedan vinculados a la finca de destino.

### Flujo Paso a Paso para el Usuario
- **Ruta de acceso en la aplicación:**
  - En la barra inferior de navegación, presione el botón central (+) > En el menú de acciones rápidas, seleccione la opción **Trasladar animales entre fincas**.

#### Configuración del Destino y Filtros de Búsqueda
1. **Finca de destino:**
   - En el menú desplegable **Finca de destino**, verifique o seleccione la finca propia a la cual desea enviar los animales.
2. **Sección colapsable "Aplicar filtros animales" (Opcional):**
   - Presione sobre la sección desplegable **Aplicar filtros animales** para abrir los criterios zootécnicos de búsqueda si desea ubicar rápidamente un grupo específico de ejemplares.
   - **Tipo de animal:** Si la finca maneja más de una especie (por ejemplo, bovinos, bufalinos, ovinos o caprinos), seleccione la especie deseada en el selector desplegable.
   - **Filtros avanzados de animales:** Seleccione criterios adicionales como potrero, lote, categoría o estado reproductivo para acotar el listado de selección.

#### Selección y Gestión de Animales a Trasladar
1. **Contador de animales seleccionados:**
   - En la parte superior de la pantalla se muestra el indicador **Total de animales seleccionados**, el cual inicia en 0 y se actualiza dinámicamente con la cantidad de ejemplares agregados.
2. **Agregar animales al traslado:**
   - Presione el botón **Seleccionar animales**.
   - Se abrirá un cuadro de diálogo con el selector múltiple de animales, mostrando los ejemplares vivos presentes en la finca activa (y filtrados según los criterios configurados previamente).
   - Marque las casillas de los animales que desea trasladar y presione el botón de confirmación del selector.
   - Los animales elegidos se añadirán inmediatamente a la tabla inferior y se sumarán al contador superior.
3. **Revisión y remoción en la tabla de animales:**
   - En la tabla inferior se visualiza la información básica de cada animal incorporado (identificador, arete o código).
   - Para remover un animal que se agregó por error, presione el icono de eliminación (X o papelera) ubicado al final de la fila correspondiente al animal. El ejemplar se retirará de la lista y el contador disminuirá de inmediato.

#### Ejecución y Confirmación del Traslado
1. Una vez elegida la finca de destino y habiendo agregado al menos 1 animal a la tabla, presione el botón **Trasladar**.
2. **Cuadro de diálogo de confirmación:**
   - Aparecerá un cuadro emergente en pantalla con la pregunta: "¿Estas seguro de trasladar estos animales a la finca [Nombre de la Finca Destino]?".
   - Si los datos son correctos, confirme la operación en el diálogo.
3. **Finalización del proceso:**
   - El sistema procesará la transferencia a través de internet.
   - Al completarse, se exhibirá el mensaje de éxito **Animales transferidos exitosamente**.
   - La pantalla se cerrará automáticamente regresando a la vista previa.

- **Pantalla de llegada tras guardar:** Pantalla anterior (menú principal o panel de la finca activa).

### Matriz de Errores y Soluciones
| Mensaje en la App / Síntoma | Causa Real | Respuesta Sugerida por el Agente | Criterio de Escalamiento Humano |
| :--- | :--- | :--- | :--- |
| No aparece la opción "Trasladar animales entre fincas" en el menú central (+) | El usuario tiene registrada solo 1 finca en su cuenta, o no es el propietario registrado de la finca activa actual | "La opción de traslado entre fincas requiere que usted sea el propietario de la finca activa y que tenga registradas al menos dos fincas propias en su cuenta. Si solo administra un predio o tiene un rol de colaborador sin permisos de propietario, esta opción no se habilitará." | Si el usuario es el propietario legal de múltiples fincas vinculadas a la misma cuenta y no visualiza la opción, verificar asignación de roles en base de datos. |
| "Debe agregar al menos un animal" (o el botón no procesa el envío) | Se presionó el botón 'Trasladar' sin haber seleccionado ningún animal en la tabla | "Para realizar el traslado debe seleccionar al menos un animal. Presione el botón 'Seleccionar animales', elija los ejemplares que desea mover y luego confirme la transferencia." | No escalar, validación operativa del formulario. |
| Error de conexión o mensaje de fallo de red al trasladar | El dispositivo no cuenta con conexión activa a internet (datos móviles o WiFi) | "El traslado de animales entre fincas requiere conexión activa a internet para actualizar de inmediato el inventario entre ambos predios. Compruebe su conexión a internet e intente presionar 'Trasladar' nuevamente." | Si el dispositivo navega con normalidad en otras aplicaciones pero el traslado no se procesa tras varios intentos, transferir a soporte técnico. |
| Círculo de espera infinito / Pantalla congelada en cargando | Proceso en segundo plano bloqueado o timeout en el dispositivo al procesar la transferencia masiva | "Espere 30 segundos. Si no avanza, cierre la aplicación por completo desde el administrador de tareas de su teléfono (deslizando hacia arriba) y vuelva a abrirla. Sus datos locales no se perderán." | Si tras reabrir la app el botón sigue deshabilitado o la pantalla vuelve a congelarse, transferir de inmediato a soporte humano con correo y modelo del teléfono. |

### Directivas de Seguridad y Guardrails
- NUNCA solicite contraseñas de acceso ni códigos confidenciales del ganadero para asistir en el traslado de animales.
- Advierta al usuario que al confirmar el traslado, los animales se retirarán del inventario de la finca actual y se sumarán al inventario de la finca seleccionada como destino.
- Aclare que esta opción está diseñada para movimientos internos entre fincas de su propia cuenta; para traspasos a otros productores externos se debe utilizar el módulo de venta de animales.
