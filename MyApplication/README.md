# MyApplication

## Qué hace el proyecto

Es la plantilla de Kotlin equivalente a un proyecto Android básico. Solo carga una vista y ajusta los Insets para Edge-to-Edge.

## MainActivity.kt

### Línea 1

```kotlin
package com.example.myapplication
```

Declara el paquete de la actividad en Kotlin.

### Líneas 3 a 7

```kotlin
import android.os.Bundle
import androidx.activity.enableEdgeToEdge
import androidx.appcompat.app.AppCompatActivity
import androidx.core.view.ViewCompat
import androidx.core.view.WindowInsetsCompat
```

Importan las clases necesarias para iniciar la pantalla y aplicar Edge-to-Edge.

### Línea 9

```kotlin
class MainActivity : AppCompatActivity() {
```

Define la actividad principal.

### Líneas 10 a 19

```kotlin
override fun onCreate(savedInstanceState: Bundle?) {
	super.onCreate(savedInstanceState)
	enableEdgeToEdge()
	setContentView(R.layout.activity_main)
	ViewCompat.setOnApplyWindowInsetsListener(findViewById(R.id.main)) { v, insets ->
		val systemBars = insets.getInsets(WindowInsetsCompat.Type.systemBars())
		v.setPadding(systemBars.left, systemBars.top, systemBars.right, systemBars.bottom)
		insets
	}
}
```

Inicia la pantalla, carga el layout y ajusta el padding para que el contenido no quede debajo de las barras del sistema.

## activity_main.xml

### Línea 1

```xml
<?xml version="1.0" encoding="utf-8"?>
```

Declara el archivo XML.

### Líneas 2 a 7

```xml
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
	xmlns:app="http://schemas.android.com/apk/res-auto"
	xmlns:tools="http://schemas.android.com/tools"
	android:id="@+id/main"
	android:layout_width="match_parent"
	android:layout_height="match_parent"
	tools:context=".MainActivity">
```

Crean el contenedor principal.

### Líneas 9 a 16

```xml
<TextView
	android:layout_width="wrap_content"
	android:layout_height="wrap_content"
	android:text="Prueba Nro 1"
	app:layout_constraintBottom_toBottomOf="parent"
	app:layout_constraintEnd_toEndOf="parent"
	app:layout_constraintStart_toStartOf="parent"
	app:layout_constraintTop_toTopOf="parent" />
```

Muestran un texto centrado.

## Para el examen

Sirve para recordar la estructura base de una app Android hecha en Kotlin y el uso de Edge-to-Edge.