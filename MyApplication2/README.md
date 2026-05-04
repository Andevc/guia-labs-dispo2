# MyApplication2

## Qué hace el proyecto

Otro proyecto base con una pantalla simple. Tiene una versión normal y otra en layout-land para adaptar la interfaz cuando el dispositivo está en horizontal.

## MainActivity.java

### Línea 1

```java
package com.example.myapplication;
```

Declara el paquete de la clase principal.

### Líneas 3 a 8

```java
import android.os.Bundle;

import androidx.activity.EdgeToEdge;
import androidx.appcompat.app.AppCompatActivity;
import androidx.core.graphics.Insets;
import androidx.core.view.ViewCompat;
import androidx.core.view.WindowInsetsCompat;
```

Importan las clases necesarias para la actividad y el ajuste visual a las barras del sistema.

### Línea 10

```java
public class MainActivity extends AppCompatActivity {
```

Define la pantalla principal.

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

Inicializa la pantalla, activa Edge-to-Edge y ajusta el padding de la vista principal.

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

Muestran el texto centrado en pantalla.

## layout-land/activity_main.xml

### Línea 1

```xml
<?xml version="1.0" encoding="utf-8"?>
```

Declara el archivo XML para orientación horizontal.

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

Crean el contenedor principal para modo paisaje.

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

Muestran el mismo texto, pero usando el layout alternativo para horizontal.

## Para el examen

La idea importante aquí es entender que Android puede cargar layouts distintos según la orientación.