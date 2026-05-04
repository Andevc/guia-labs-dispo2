# labDataBase

## Qué hace el proyecto

Es una plantilla Android básica sin lógica adicional visible en el código fuente revisado. La actividad principal solo carga la vista y ajusta los Insets del sistema.

## MainActivity.java

- Línea 1: declara el paquete com.movil.labdatabase.
- Línea 3: separa el área de imports.
- Líneas 4 a 8: importan Bundle, EdgeToEdge, AppCompatActivity, Insets, ViewCompat y WindowInsetsCompat.
- Línea 10: define la actividad principal.
- Línea 12: abre onCreate.
- Línea 13: indica que se sobreescribe el método de la clase padre.
- Línea 14: prepara la actividad con la inicialización base de Android.
- Línea 15: activa Edge-to-Edge.
- Línea 16: carga el layout activity_main.
- Línea 17: busca la vista principal con id main.
- Línea 18: registra el listener que ajusta el padding.
- Línea 19: toma los insets de las barras del sistema.
- Línea 20: aplica el padding para respetar la zona visible.
- Línea 21: devuelve los insets sin cambiarlos.
- Línea 22: cierra el listener.
- Línea 23: cierra onCreate.
- Línea 24: cierra la clase.

## Para el examen

Este proyecto sirve como base vacía para empezar a construir una interfaz más compleja.