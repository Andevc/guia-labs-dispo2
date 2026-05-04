# lab4

## Qué hace el proyecto

Ejemplo de almacenamiento externo específico de la app. Guarda y lee un archivo dentro de getExternalFilesDir(null), sin pedir una ruta manual al usuario.

## MainActivity.java

- Línea 1: declara el paquete com.movil.lab4.
- Línea 3: separa los imports del cuerpo de la clase.
- Líneas 4 a 14: importan vistas, archivos, entrada y salida; todo lo necesario para guardar y leer un archivo externo.
- Línea 15: importa InputStreamReader para convertir bytes en texto.
- Línea 17: inicia la actividad principal.
- Línea 19: declara el campo Escribe.
- Línea 20: declara el TextView Resultado.
- Línea 21: guarda el nombre del archivo externo.
- Línea 24: comienza onCreate.
- Línea 25: ejecuta el constructor de la clase padre.
- Línea 26: carga activity_main.
- Línea 28: enlaza el campo de texto.
- Línea 29: enlaza el resultado.
- Líneas 31 a 33: enlazan el botón Guardar.
- Línea 34: cierra el bloque de inicialización del botón guardar.
- Líneas 35 a 42: al pulsar Guardar, toma el texto escrito, lo recorta y lo envía a guardarExt.
- Línea 43: cierra el bloque.
- Líneas 44 a 48: al pulsar Leer, ejecuta mostrarExterno.
- Línea 49: cierra el bloque.
- Línea 51: abre el método guardarExt.
- Línea 52: valida que el texto no esté vacío.
- Línea 53: si está vacío, muestra un mensaje y termina.
- Línea 54: obtiene la carpeta externa privada de la app.
- Línea 55: verifica que la ruta exista.
- Línea 56: si no existe, muestra error y termina.
- Línea 57: crea el objeto File con la ruta y el nombre del archivo.
- Línea 59: abre el bloque try.
- Línea 60: crea el FileOutputStream para escribir.
- Línea 61: escribe el texto convertido a bytes.
- Línea 62: fuerza el vaciado del buffer.
- Línea 63: cierra el flujo.
- Línea 65: limpia el campo de texto.
- Línea 67: informa la ruta exacta donde se guardó.
- Línea 69: captura errores de escritura.
- Línea 70: muestra un mensaje si falla el guardado.
- Línea 73: abre el método mostrarExterno.
- Línea 74: obtiene otra vez la ruta externa.
- Línea 75: verifica que la carpeta sea accesible.
- Línea 76: si no, muestra error y termina.
- Línea 77: crea el objeto File con el nombre del archivo.
- Línea 79: verifica si el archivo existe.
- Línea 80: si no existe, avisa al usuario.
- Línea 81: limpia el resultado visual.
- Línea 82: termina el método.
- Línea 85: crea un StringBuilder para acumular el texto leído.
- Línea 87: abre el bloque try de lectura.
- Línea 88: abre FileInputStream.
- Línea 89: crea InputStreamReader.
- Línea 90: crea BufferedReader.
- Línea 92: declara la variable linea.
- Línea 93: inicia la lectura línea por línea.
- Línea 94: añade cada línea al acumulador.
- Línea 95: añade un salto de línea.
- Línea 96: termina el ciclo cuando no hay más contenido.
- Línea 98: escribe el texto final en Resultado.
- Línea 100: captura errores de lectura.
- Línea 101: avisa si ocurre un problema al leer.
- Línea 103: cierra el método.
- Línea 104: cierra la clase.

## activity_main.xml

- Línea 1: declara el XML.
- Líneas 2 a 7: crean el ConstraintLayout principal.
- Líneas 9 a 22: definen el EditText de entrada.
- Líneas 24 a 37: definen el botón Guardar Archivo.
- Líneas 39 a 52: definen el botón Leer.
- Líneas 54 a 63: muestran el contenido leído.

## Para el examen

La diferencia clave con lab2 es que aquí el archivo se guarda en almacenamiento externo privado de la app, no en almacenamiento interno.