# MyApplication2

## Qué hace el proyecto

Otro proyecto base con una pantalla simple. Tiene una versión normal y otra en layout-land para adaptar la interfaz cuando el dispositivo está en horizontal.

## MainActivity.java

- Línea 1: declara el paquete com.example.myapplication.
- Línea 2: deja una línea vacía antes de los imports.
- Línea 3: importa Bundle.
- Línea 4: importa EdgeToEdge.
- Línea 5: importa AppCompatActivity.
- Línea 6: importa Insets.
- Línea 7: importa ViewCompat.
- Línea 8: importa WindowInsetsCompat.
- Línea 10: inicia la clase MainActivity.
- Línea 12: abre onCreate.
- Línea 13: llama al método base.
- Línea 14: activa Edge-to-Edge.
- Línea 15: carga el layout activity_main.
- Línea 16: busca la vista principal main.
- Línea 17: obtiene los insets de las barras del sistema.
- Línea 18: aplica el padding a la vista.
- Línea 19: devuelve los insets.
- Línea 20: cierra el listener.
- Línea 21: cierra onCreate.
- Línea 22: cierra la clase.

## activity_main.xml

- Líneas 1 a 7: crean el contenedor principal.
- Líneas 9 a 16: muestran el texto Prueba Nro 1 centrado.

## layout-land/activity_main.xml

- Líneas 1 a 7: crean el contenedor principal para orientación horizontal.
- Líneas 9 a 16: repiten el texto Prueba Nro 1 pero usando el layout especial para paisaje.

## Para el examen

La idea importante aquí es entender que Android puede cargar layouts distintos según la orientación.