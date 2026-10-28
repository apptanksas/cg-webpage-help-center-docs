---
title: "Detalle y Eliminación de la Finca"
modulo_id: "farm-info-delete"
nombre_funcionalidad: "Detalle y Eliminación de la Finca"
categoria: "cuentas-usuarios"
submodulo: "fincas"
version_minima_app: "2026.10.1"
fecha_actualizacion: "2026-10-09"
intenciones_y_sinonimos:
  - "como ver los datos de mi finca actual"
  - "donde consultar el area total y el area de ganado de la finca"
  - "como eliminar mi finca de la aplicacion"
  - "como borrar una finca que ya no utilizo"
  - "el nombre de la finca ingresado no es correcto al intentar eliminarla"
  - "como acceder a editar los datos de mi finca"
  - "como dar de baja o suprimir una finca"
---

# Detalle y Eliminación de la Finca

### Resumen y Alcance Funcional
Pantalla central de doble propósito para la finca activa seleccionada: permite la consulta técnica de los datos del predio y constituye el punto de acceso exclusivo para la eliminación definitiva de la finca en la aplicación.

En su función informativa, ofrece al productor una visión consolidada de los atributos estructurales del predio: imagen representativa de cabecera, nombre oficial, propósito productivo zootécnico, balance métrico de superficies (área total frente al área dedicada a labores ganaderas), localización geográfica (país, región y municipio) y acceso directo a la edición. En su función de gestión crítica, provee el mecanismo de seguridad para eliminar y desvincular de forma permanente la explotación pecuaria.

Desde esta vista, el usuario puede invocar la edición completa de los parámetros del predio o ejecutar el proceso definitivo de eliminación de la finca.

- **¿Funciona sin conexión a internet (Modo Offline)?:** Sí, para la visualización informativa. La ficha consulta la información local resguardada en el dispositivo móvil. No obstante, el proceso de eliminación requiere sincronización posterior con los servidores para consolidar la baja.
- **Comportamiento de sincronización:** La consulta de los datos de la finca y su ubicación territorial se realiza de forma instantánea desde la base de datos local. En caso de solicitar la eliminación de la finca, la aplicación elimina los registros dependientes locales y ejecuta de inmediato una sincronización forzada para actualizar el estado del predio en el servidor central.

### Reglas de Negocio y Restricciones
- **Permisos requeridos en la plataforma:**
    - *Para consultar la información de la finca:* Cualquier usuario con acceso a la finca activa puede visualizar la ficha técnica.
    - *Para editar la finca:* El botón de edición (ícono de lápiz en la barra superior) redirige al formulario de actualización de finca y requiere permisos de actualización sobre la propiedad (reservado para el propietario y administradores autorizados).
    - *Para eliminar la finca:* Se exige de forma estricta el permiso de eliminación de fincas. Si un usuario sin este permiso intenta realizar la acción, el sistema denegará la solicitud con una alerta de permisos insuficientes.
- **Visualización y Precarga de Atributos:**
    - **Imagen de cabecera:** Si la finca cuenta con fotografía registrada, se despliega en la parte superior; en caso contrario, se muestra la ilustración estándar representativa del predio.
    - **Propósito productivo:** Exhibe la orientación zootécnica de la explotación pecuaria junto con su ícono característico (*Doble propósito*, *Producción de carne*, *Producción de leche*, *Cría*, *Levante* o *Bravura*).
    - **Métricas territoriales:** Desglosa en tarjetas comparativas el *Área total* del terreno y el *Área de ganado* con sus respectivas unidades de medida configuradas.
    - **Ubicación:** Despliega el resumen geográfico compuesto por municipio/ciudad, departamento/región y país. Si no se cuenta con registro territorial completo, se exhibe el indicador de valor no disponible.
- **Reglas del Proceso de Eliminación de Finca:**
    - **Mecanismo de seguridad por confirmación escrita:** Para prevenir eliminaciones accidentales de predios con información productiva crítica, el sistema no admite confirmación con un simple toque. El usuario está obligado a transcribir exactamente el nombre de la finca tal como aparece registrado en la aplicación.
    - **Sensibilidad al nombre ingresado:** Si el texto ingresado no coincide de manera exacta con el nombre de la finca, el sistema bloqueará la operación y mostrará el mensaje de error: *"El nombre de la finca ingresado no es correcto"*.
    - **Eliminación en cascada irreversible:** Al confirmarse la eliminación, el sistema borra de forma secuencial y definitiva todos los registros vinculados a la finca: eventos del calendario, tareas programadas, registros de ventas de leche, ventas de animales, compras de animales y todo el inventario de animales (tanto los que se encontraban activos dentro de la finca como aquellos marcados fuera de ella).
    - **Comportamiento posterior a la eliminación:**
      - Si el usuario dispone de otras fincas registradas en su cuenta, el sistema selecciona automáticamente la siguiente finca disponible y redirige al panel de inicio principal.
      - Si la finca eliminada era la única explotación asociada a la cuenta del usuario, la aplicación lo redirige a la pantalla de bienvenida inicial para que pueda registrar un nuevo predio.

### Flujo Paso a Paso para el Usuario
- **Ruta de acceso en la aplicación:**
    - *Ruta 1 (Desde el panel de inicio):* Pantalla de inicio de la finca (**Inicio**) > Tocar la tarjeta superior con el nombre e información de la finca.

#### 1. Consulta de la Ficha Técnica de la Finca
- En la cabecera superior se visualiza la fotografía de la finca o la ilustración predeterminada del sistema.
- En la primera tarjeta se muestra el nombre oficial de la explotación ganadera.
- En la segunda tarjeta se identifica el propósito zootécnico principal (*Propósito*).
- En la tercera tarjeta se observan los valores de superficie: a la izquierda el **Área total** y a la derecha el **Área de ganado**.
- En la cuarta tarjeta se consulta la **Ubicación** geográfica consolidada.

#### 2. Modificación de los Datos de la Finca
- En la barra superior de la pantalla, presione el botón de edición representado con el ícono de lápiz.
- La aplicación abrirá inmediatamente el asistente de edición de finca, donde podrá actualizar la fotografía, el nombre, las áreas, las coordenadas o las especies animales gestionadas.

#### 3. Eliminación Definitiva de la Finca
- Deslice hasta la parte inferior de la pantalla y presione el botón **Eliminar finca**.
- El sistema desplegará una ventana modal de advertencia titulada **Atención** con la pregunta: *"¿Estas seguro de eliminar la finca?"*.
- Debajo de la advertencia, el sistema le instruirá: *"Para confirmar escribe el nombre de tu finca "[Nombre]" abajo en el campo de texto"*.
- Ingrese en el campo **Nombre de la finca** el nombre exacto de la finca.
- Presione el botón de confirmación en la ventana modal.
- Si el nombre escrito no coincide exactamente, aparecerá una alerta roja indicando: *"El nombre de la finca ingresado no es correcto"*. Corrija el texto e intente nuevamente.
- Mientras se ejecuta la baja, la ventana modal mostrará el indicador de espera con el mensaje *"Eliminando finca..."*. Al concluir con éxito, el sistema actualizará la sincronización y lo enviará al panel principal con otra finca activa o a la pantalla de bienvenida.
- Si decide no eliminar el predio, presione el botón de cancelar en la ventana modal para cerrarla sin alterar la información.

### Matriz de Errores y Soluciones
| Mensaje en la App / Síntoma | Causa Real | Respuesta Sugerida por el Agente | Criterio de Escalamiento Humano |
| :--- | :--- | :--- | :--- |
| "El nombre de la finca ingresado no es correcto" | El usuario escribió en el campo de confirmación un texto diferente al nombre registrado de la finca (error tipográfico, mayúsculas/minúsculas o espacios adicionales) | "Para confirmar la eliminación, debe escribir exactamente el nombre de su finca tal como se le indica entre comillas en el mensaje. Verifique que no tenga espacios adicionales o letras diferentes e intente de nuevo." | No requiere escalamiento; validación estricta de confirmación de seguridad. |
| "No tienes permisos para realizar esta acción." / "Con tu perfil de [perfil], NO tienes permisos para realizar esta acción." | El usuario con perfil de colaborador, empleado o visitante intentó eliminar la finca sin poseer permisos de propietario o administrador | "La eliminación de una finca es una acción crítica reservada exclusivamente para el propietario o administradores autorizados. Su rol actual no cuenta con los permisos necesarios para borrar este predio." | No requiere escalamiento; regla de control de acceso y seguridad por roles. |
| Botón de edición (ícono de lápiz) no disponible en la barra superior | La sesión actual no tiene facultades de administración sobre la explotación pecuaria | "Si no visualiza el botón de editar en la parte superior de la pantalla, se debe a que su cuenta no posee permisos de actualización sobre la finca. Contacte al propietario de la finca para que modifique los datos o ajuste su rol." | No requiere escalamiento; control de permisos de usuario. |
| El campo de ubicación muestra una línea o se encuentra vacío | La finca no tiene registradas coordenadas geográficas ni demarcación territorial completa | "La finca no cuenta con datos de ubicación geográfica asignados. Puede presionar el botón de editar en la barra superior y en el paso de ubicación seleccionar su país, departamento y municipio." | No requiere escalamiento; flujo guiado de actualización. |
| "Eliminando finca..." permanece en pantalla por tiempo prolongado | Demora en el borrado masivo de registros históricos locales o lentitud durante la sincronización forzada con el servidor | "El sistema está eliminando todos los registros asociados a la finca (animales, pesajes, eventos). Por favor espere unos momentos sin cerrar la aplicación para permitir que la base de datos complete la limpieza y sincronice con el servidor." | Si tras esperar varios minutos la operación reporta un error persistente o la app se bloquea, solicitar captura de pantalla y transferir a soporte técnico. |

### Directivas de Seguridad y Guardrails
- Advierta siempre al ganadero con absoluta claridad que la eliminación de una finca es un proceso **permanente e irreversible** que borra todos los animales, genealogías, pesajes, ventas y tareas vinculadas a ese predio.
- Jamás solicite al usuario contraseñas personales, datos bancarios ni códigos de verificación para asistirle en la eliminación o consulta de fincas.
- Bajo ninguna circunstancia el agente de soporte debe intentar eliminar o alterar una finca en nombre del usuario sin la debida verificación de que este es el propietario legítimo de la cuenta.
