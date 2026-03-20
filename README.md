# Laboratorio-1-Computo-2

RENE OSWALDO ORELLANA DE LA O SMSS018422
ALLISSON LOURDES GUEVARA PALMA SMIS038421

PREGUNTAS
1 ¿Que es Vue.js y cual es su funcion?
Vue.js es un framework o marco de trabajo de JavaScript que sirve para crear interfaces de usuario de forma sencilla y eficiente. En la pagina su funcion es actuar como el cerebro reactivo. En lugar de que tu tengas que escribir codigo para decirle al navegador: "ahora borra este texto y pon este otro", Vue detecta cuando los datos cambian y actualiza la pantalla automaticamente.
Basicamente conecta la logica de tu inventario con lo que el cliente ve en el navegador.

2 ¿Describa qué variables reactivas utilizó en su aplicación y cuál es la función de 
cada una dentro del sistema?
Usamos 5 variables principales
1. nuevoNombre: Almacena temporalmente el nombre del repuesto que estas escribiendo.
2. nuevoPrecio: Guarda el precio unitario del producto antes de agregarlo.
3. nuevaCantidad: Controla cuantas piezas del mismo repuesto se van a cotizar.
4. carrito: Es un arreglo (lista) que guarda todos los objetos que ya validaste y agregaste a la cotizacion.
5. mensajeError: Almacena el texto de alerta que se muestra cuando el usuario intenta ingresar datos validos.

3 ¿Explique la diferencia entre las siguientes directivas utilizadas en su proyecto: v
bind y v-model?
v-model (Bidireccional): Crea una conexión de "ida y vuelta". Si el usuario escribe en el input, la variable cambia; y si tú cambias la variable desde el código, el input se actualiza. Lo usamos para capturar los datos del formulario.

v-bind (Unidireccional): Sirve para enlazar una variable a un atributo de una etiqueta HTML (como src, class, disabled, etc.). En tu proyecto, lo usamos para deshabilitar el botón de "Agregar" (:disabled) si el campo de nombre está vacío. Los datos solo viajan del código hacia el atributo.

4 ¿Mencione al menos un ejemplo de evento utilizado dentro de su aplicación?
El evento principal fue @submit.prevent.

@submit: Escucha cuando el usuario presiona el botón de enviar o da "Enter" en el formulario.
.prevent: Es un modificador que evita que la página se recargue (comportamiento por defecto de los formularios en HTML), permitiendo que Vue maneje el envío internamente.

5 ¿Explique para qué utilizó la directiva v-for dentro de su aplicación?
La utilizamos para renderizar listas dinámicas. Su función es recorrer el arreglo carrito y, por cada objeto que encuentre dentro, generar automáticamente una fila (<tr>) en la tabla con sus respectivos datos. Sin v-for, tendrías que crear cada fila a mano en el HTML, lo cual es imposible si no sabes cuántos productos agregará el cliente.

6 ¿Describa en qué situación utilizó v-if y qué problema resuelve dentro de su 
interfaz?
Utilizamos v-if en dos lugares clave:

En el mensaje de error: Solo aparece si la variable mensajeError tiene contenido. Resuelve el problema de tener alertas vacías o molestas ocupando espacio cuando todo está correcto.

En la tabla de cotización: Solo muestra la tabla si el carrito tiene al menos un producto. Resuelve el problema visual de mostrar una tabla vacía (solo con encabezados) que se ve poco profesional cuando el usuario aún no ha empezado a cotizar.

7 ¿Explique cómo se realiza la validación de datos en su aplicación y por qué es 
importante validar la información ingresada por el usuario?
La validación se realiza mediante una condición lógica (if) dentro de la función agregarAlCarrito. Verificamos que el texto no sea solo espacios en blanco y que los números sean mayores a cero.

¿Por qué es importante?

Integridad de la información: Evita que el sistema procese "basura" (como un producto sin nombre o con precio de -$50).

Experiencia de usuario: Le indica al usuario qué hizo mal en el momento exacto, guiándolo para que use la herramienta correctamente.

Prevención de errores lógicos: Evita que los cálculos matemáticos (como el total de la venta) den resultados incoherentes o errores de sistema (NaN).

