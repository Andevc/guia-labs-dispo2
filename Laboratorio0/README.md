# Laboratorio0

## Qué hace el proyecto

Proyecto base de Android con una sola pantalla. Sirve para reconocer la estructura mínima de una app y el uso de Edge-to-Edge.
## MainActivity.java

### Línea 1

```java
package com.movil.laboratorio0;
```

Declara el paquete donde vive esta clase.
### Líneas 3 a 8

```java
import android.os.Bundle;

import androidx.activity.EdgeToEdge;
import androidx.appcompat.app.AppCompatActivity;
import androidx.core.graphics.Insets;
import androidx.core.view.ViewCompat;
import androidx.core.view.WindowInsetsCompat;
```

Importan las clases necesarias para crear la actividad y ajustar la vista a las barras del sistema.
### Línea 10

```java
public class MainActivity extends AppCompatActivity {
```

Define la pantalla principal de la app.
### Líneas 13 a 22

```java
@Override
protected void onCreate(Bundle savedInstanceState) {
	super.onCreate(savedInstanceState);
	EdgeToEdge.enable(this);
	setContentView(R.layout.activity_main);
	ViewCompat.setOnApplyWindowInsetsListener(findViewById(R.id.main), (v, insets) -> {
		Insets systemBars = insets.getInsets(WindowInsetsCompat.Type.systemBars());
		v.setPadding(systemBars.left, systemBars.top, systemBars.right, systemBars.bottom);
		return insets;
	});
}
```

Este bloque inicia la pantalla, activa Edge-to-Edge, carga el layout y agrega padding para que el contenido no quede debajo de las barras del sistema.
## activity_main.xml

### Línea 1

```xml
<?xml version="1.0" encoding="utf-8"?>
```

Declara que el archivo es XML.
### Líneas 2 a 6

```xml
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
	xmlns:app="http://schemas.android.com/apk/res-auto"
	xmlns:tools="http://schemas.android.com/tools"
	android:id="@+id/main"
	android:layout_width="match_parent"
	android:layout_height="match_parent"
	tools:context=".MainActivity">
```

Crean el contenedor principal de la pantalla.
### Líneas 8 a 14

```xml
<TextView
	android:layout_width="wrap_content"
	android:layout_height="wrap_content"
	android:text="Hello World!"
	app:layout_constraintBottom_toBottomOf="parent"
	app:layout_constraintEnd_toEndOf="parent"
	app:layout_constraintStart_toStartOf="parent"
	app:layout_constraintTop_toTopOf="parent" />
```

Muestran un texto centrado en la pantalla.
### Línea 16

```xml
</androidx.constraintlayout.widget.ConstraintLayout>
```

Cierra el contenedor principal.
## Para el examen

La idea importante es identificar la estructura mínima: una actividad, un layout y un ajuste de insets para que la vista no quede debajo de las barras del sistema.
# Laboratorio0

## Qué hace el proyecto

Proyecto base de Android con una sola pantalla. Sirve para reconocer la estructura mínima de una app y el uso de Edge-to-Edge.

## MainActivity.java

- Línea 1: declara el paquete com.movil.laboratorio0.
- Línea 3: deja un espacio antes de los imports para separar visualmente la clase de sus dependencias.
- Líneas 4 a 8: importan Bundle, EdgeToEdge, AppCompatActivity, Insets, ViewCompat y WindowInsetsCompat; todas se usan para crear la actividad y ajustar márgenes según las barras del sistema.
- Línea 10: define la clase MainActivity como una pantalla de Android.
- Línea 12: abre la declaración de onCreate, que es el primer método importante cuando la pantalla se crea.
- Línea 13: indica que el método sobrescribe el comportamiento de la clase padre.
- Línea 14: llama al onCreate de AppCompatActivity para que Android prepare correctamente la actividad.
- Línea 15: activa Edge-to-Edge para que el contenido pueda extenderse hasta los bordes.
- Línea 16: carga el archivo activity_main.xml como interfaz visual.
- Línea 17: busca la vista con id main, que es el contenedor principal del layout.
- Línea 18: registra un listener para modificar los márgenes cuando cambian los insets del sistema.
- Línea 19: obtiene el espacio ocupado por la barra superior, barra inferior y otras zonas del sistema.
- Línea 20: aplica padding a la vista para evitar que el contenido quede tapado por las barras.
- Línea 21: devuelve los insets sin modificarlos para que el sistema continúe procesándolos.
- Línea 22: cierra el bloque del listener.
- Línea 23: cierra el método onCreate.
- Línea 24: cierra la clase.

## activity_main.xml

- Línea 1: declara el XML.
- Líneas 2 a 6: crean el contenedor principal ConstraintLayout, le asignan el id main y definen que ocupe toda la pantalla.
- Línea 7: cierra los atributos iniciales del layout.
- Línea 8: abre el TextView que muestra el mensaje principal.
- Línea 9: define el ancho automático del texto.
- Línea 10: define la altura automática del texto.
- Línea 11: escribe Hello World! como contenido visible.
- Líneas 12 a 15: colocan el texto en el centro usando restricciones arriba, abajo, izquierda y derecha.
- Línea 16: cierra el TextView.
- Línea 17: cierra el ConstraintLayout.

## Para el examen

La idea importante es identificar la estructura mínima: una actividad, un layout y un ajuste de insets para que la vista no quede debajo de las barras del sistema.