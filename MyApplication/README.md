# MyApplication

## Qué hace el proyecto

Es la plantilla de Kotlin equivalente a un proyecto Android básico. Solo carga una vista y ajusta los Insets para Edge-to-Edge.

## MainActivity.kt

- Línea 1: declara el paquete com.example.myapplication.
- Línea 2: deja una línea vacía antes de los imports.
- Línea 3: importa android.os.Bundle.
- Línea 4: importa enableEdgeToEdge para activar contenido a borde completo.
- Línea 5: importa AppCompatActivity.
- Línea 6: importa ViewCompat para manipular insets de la vista.
- Línea 7: importa WindowInsetsCompat para obtener las barras del sistema.
- Línea 9: define la clase MainActivity en Kotlin.
- Línea 10: abre onCreate.
- Línea 11: llama al método base de la actividad.
- Línea 12: activa Edge-to-Edge.
- Línea 13: carga activity_main.
- Línea 14: busca la vista principal con id main.
- Línea 15: registra el listener para ajustar padding.
- Línea 16: obtiene el tamaño de las barras del sistema.
- Línea 17: aplica padding a la vista.
- Línea 18: devuelve los insets procesados.
- Línea 19: cierra el bloque del listener.
- Línea 20: cierra onCreate.
- Línea 21: cierra la clase.

## activity_main.xml

- Líneas 1 a 7: crean el ConstraintLayout principal.
- Líneas 9 a 16: muestran el texto Prueba Nro 1 centrado.
- Líneas 18 a 21: agregan una vista auxiliar sin funcionalidad relevante.

## Para el examen

Sirve para recordar la estructura base de una app Android hecha en Kotlin y el uso de Edge-to-Edge.