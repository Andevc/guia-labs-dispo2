# ejemplo1

## Qué hace el proyecto

Muestra un formulario con nombre, apellidos y carnet. Al presionar Mostrar, envía los datos a otra actividad, donde se concatenan el nombre completo y el carnet invertido.

## MainActivity.java

- Línea 1: declara el paquete com.movil.ejemplo1.
- Línea 3: deja espacio entre el paquete y los imports.
- Líneas 4 a 10: importan clases de actividad, Edge-to-Edge, Insets, ViewCompat, WindowInsetsCompat, Intent y controles de interfaz.
- Línea 11: importa AppCompatActivity otra vez por duplicado; esta importación no es necesaria y puede eliminarse.
- Línea 12: inicia la clase MainActivity.
- Línea 13: declara los EditText campoNombres, campoApellidos y campoCarnet.
- Línea 14: declara los botones botonMostrar y botonSalir.
- Línea 19: ejecuta el método base de la actividad.
- Línea 20: carga el layout activity_main.
- Línea 21: enlaza el campo de nombres.
- Línea 22: enlaza el campo de apellidos.
- Línea 23: enlaza el campo de carnet.
- Línea 24: enlaza el botón Mostrar.
- Línea 25: enlaza el botón Salir.
- Línea 26: abre el listener del botón Mostrar.
- Línea 27: toma el texto del campo de nombres.
- Línea 28: toma el texto del campo de apellidos.
- Línea 29: toma el texto del campo de carnet.
- Línea 30: crea un Intent para abrir ResultadoActivity.
- Línea 31: guarda el nombre dentro del Intent con la clave nombre.
- Línea 32: guarda los apellidos con la clave apellidos.
- Línea 33: guarda el carnet con la clave carnet.
- Línea 34: abre la pantalla ResultadoActivity.
- Línea 35: cierra el listener del botón Mostrar.
- Línea 36: abre el listener del botón Salir.
- Línea 37: cierra la actividad actual con finish.
- Línea 38: cierra el listener.
- Línea 39: cierra la clase.

## ResultadoActivity.java

- Línea 1: declara el paquete com.movil.ejemplo1.
- Línea 3: deja espacio para los imports.
- Línea 4: importa Bundle.
- Línea 5: importa TextView.
- Línea 6: importa AppCompatActivity.
- Línea 8: define la segunda pantalla.
- Línea 9: declara los TextView cilnvertido y nombreMod.
- Línea 12: llama al método base de inicio.
- Línea 13: carga el layout activity_resultado.
- Línea 14: enlaza el TextView del nombre completo.
- Línea 15: enlaza el TextView del carnet invertido.
- Línea 16: obtiene el nombre enviado desde la actividad anterior.
- Línea 17: obtiene los apellidos.
- Línea 18: obtiene el carnet.
- Línea 19: si nombre es nulo, lo reemplaza por una cadena vacía.
- Línea 20: si apellidos es nulo, lo reemplaza por una cadena vacía.
- Línea 21: si carnet es nulo, lo reemplaza por una cadena vacía.
- Línea 22: invierte el carnet con StringBuilder.
- Línea 23: une nombre y apellidos con un espacio.
- Línea 24: coloca el carnet invertido en pantalla.
- Línea 25: coloca el nombre completo en pantalla.
- Línea 26: cierra la clase.

## activity_main.xml

- Líneas 1 a 5: crean el ConstraintLayout principal.
- Líneas 7 a 16: muestran el título EJEMPLO 1.
- Líneas 18 a 102: forman el bloque de entrada con etiquetas y tres campos para nombres, apellidos y carnet.
- Líneas 104 a 137: colocan los botones Mostrar y Salir.
- Líneas 139 a 146: muestran el nombre del autor.

## activity_resultado.xml

- Líneas 1 a 5: crean el contenedor principal.
- Líneas 7 a 18: muestran el título DATOS RECOLECTADOS.
- Líneas 20 a 74: presentan el nombre completo y el carnet invertido.
- Líneas 76 a 83: muestran el nombre del autor.

## Para el examen

La idea clave es el paso de datos entre actividades usando Intent y putExtra, y luego reconstruir la información recibida en la segunda pantalla.