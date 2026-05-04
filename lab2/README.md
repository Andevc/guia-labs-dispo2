# lab2

## Qué hace el proyecto

Ejemplo de persistencia interna. El usuario escribe texto, lo guarda en un archivo privado de la app y luego puede leerlo desde el mismo almacenamiento.

## MainActivity.java

- Línea 1: declara el paquete com.movil.lab2.
- Línea 3: separa visualmente los imports del resto de la clase.
- Líneas 4 a 21: importan clases para contexto, archivos, interfaz, lectura y escritura; cada una se usa para guardar o leer datos desde almacenamiento interno.
- Línea 22: inicia la clase MainActivity.
- Línea 23: declara el EditText donde se escribe, el TextView donde se muestra el resultado y el nombre fijo del archivo.
- Línea 24: declara el TextView Resultado.
- Línea 25: guarda el nombre EjPersistencia.txt como archivo interno.
- Línea 26: la anotación reduce una advertencia del compilador relacionada con ids inflados.
- Línea 29: marca el inicio de onCreate.
- Línea 30: ejecuta la inicialización de la clase padre.
- Línea 31: activa Edge-to-Edge.
- Línea 32: carga el layout activity_main.
- Línea 34: enlaza el campo de entrada Escribe con su id.
- Línea 35: enlaza el TextView Resultado.
- Línea 36: enlaza el botón Guardar.
- Línea 37: enlaza el botón Leer.
- Líneas 39 a 46: al hacer clic en Guardar, obtiene el texto del EditText y lo envía a guardarArchivo.
- Línea 47: cierra el bloque del botón guardar.
- Líneas 49 a 55: al hacer clic en Leer, llama a leerArchivo.
- Línea 56: cierra el bloque del botón leer.
- Línea 60: abre el método que guarda el contenido en el archivo interno.
- Línea 61: abre un bloque try con recurso automático para FileOutputStream.
- Línea 62: escribe los bytes del texto dentro del archivo.
- Línea 63: limpia el campo de escritura después de guardar.
- Línea 64: muestra un mensaje con la ubicación del archivo.
- Línea 65: cierra el try.
- Línea 66: captura errores de entrada y salida.
- Línea 67: lanza una excepción si ocurre un problema grave.
- Línea 69: abre el método que lee el archivo interno.
- Línea 70: inicia un try con FileInputStream, InputStreamReader y BufferedReader.
- Línea 71: crea un StringBuilder para acumular el texto leído.
- Línea 72: declara la variable linea.
- Línea 73: inicia el ciclo de lectura línea por línea.
- Línea 74: agrega cada línea al StringBuilder.
- Línea 75: agrega un salto de línea para conservar el formato.
- Línea 76: termina el ciclo cuando no hay más texto.
- Línea 77: pone el resultado final en el TextView.
- Línea 78: cierra el bloque try.
- Línea 79: captura cualquier excepción.
- Línea 80: lanza una excepción en caso de error.
- Línea 81: cierra el método leerArchivo.
- Línea 82: cierra la clase.

## activity_main.xml

- Línea 1: declara el XML.
- Líneas 2 a 7: crean el ConstraintLayout principal con id main.
- Líneas 9 a 22: colocan el EditText donde el usuario escribe el texto.
- Líneas 24 a 37: definen el botón Guardar Archivo.
- Líneas 39 a 52: definen el botón Leer.
- Líneas 54 a 63: muestran el resultado leído del archivo.

## Para el examen

Lo importante aquí es recordar que openFileOutput con MODE_PRIVATE guarda dentro del almacenamiento interno privado de la app y que openFileInput recupera exactamente ese mismo archivo.