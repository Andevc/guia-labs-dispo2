# lab4

## Qué hace el proyecto

Ejemplo de almacenamiento externo específico de la app. Guarda y lee un archivo dentro de getExternalFilesDir(null), sin pedir una ruta manual al usuario.

## MainActivity.java

### Línea 1

```java
package com.movil.lab4;
```

Declara el paquete de la actividad.

### Líneas 3 a 15

```java
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.TextView;
import android.widget.Toast;

import androidx.appcompat.app.AppCompatActivity;

import java.io.BufferedReader;
import java.io.File;
import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.IOException;
import java.io.InputStreamReader;
```

Importan las clases que permiten trabajar con la interfaz, archivos externos y lectura de texto.

### Líneas 17 a 21

```java
public class MainActivity extends AppCompatActivity {

	private EditText Escribe;
	private TextView Resultado;
	private final String grdArchivo = "archivoExterno.txt";
```

Declaran la pantalla, el campo de texto, el resultado y el nombre del archivo externo.

### Líneas 24 a 49

```java
@Override
protected void onCreate(Bundle savedInstanceState) {
	super.onCreate(savedInstanceState);
	setContentView(R.layout.activity_main);

	Escribe = findViewById(R.id.Escribe);
	Resultado = findViewById(R.id.Resultado);

	Button btnGuardar = findViewById(R.id.btnGuardar);
	Button btnLeer = findViewById(R.id.btnLeer);

	btnGuardar.setOnClickListener(new View.OnClickListener() {
		@Override
		public void onClick(View v) {
			guardarExt(Escribe.getText().toString().trim());
		}
	});
	btnLeer.setOnClickListener(new View.OnClickListener() {
		@Override
		public void onClick(View v) {
			mostrarExterno();
		}
	});
}
```

Inicializa la pantalla, enlaza los controles y conecta los botones con las funciones de guardar y leer.

### Líneas 51 a 74

```java
private void guardarExt(String texto) {
	if (texto.isEmpty()) {
		Toast.makeText(this, "Ingrese un texto", Toast.LENGTH_SHORT).show();
		return;
	}

	File ruta = getExternalFilesDir(null);

	if (ruta == null) {
		Toast.makeText(this, "No se pudo acceder al almacenamiento", Toast.LENGTH_SHORT).show();
		return;
	}

	File archivo = new File(ruta, grdArchivo);

	try {
		FileOutputStream fos = new FileOutputStream(archivo);
		fos.write(texto.getBytes());
		fos.flush();
		fos.close();

		Escribe.setText("");

		Toast.makeText(this, "Guardado en: " + archivo.getAbsolutePath(), Toast.LENGTH_LONG).show();

	} catch (IOException e) {
		Toast.makeText(this, "Error al guardar el archivo", Toast.LENGTH_SHORT).show();
	}
}
```

Valida el texto, obtiene la carpeta externa privada de la app y escribe el contenido en un archivo.

### Líneas 75 a 104

```java
private void mostrarExterno() {

	File ruta = getExternalFilesDir(null);

	if (ruta == null) {
		Toast.makeText(this, "No se pudo acceder al almacenamiento", Toast.LENGTH_SHORT).show();
		return;
	}

	File archivo = new File(ruta, grdArchivo);

	if (!archivo.exists()) {
		Toast.makeText(this, "El archivo no existe", Toast.LENGTH_SHORT).show();
		Resultado.setText("");
		return;
	}

	StringBuilder sb = new StringBuilder();

	try {
		FileInputStream fis = new FileInputStream(archivo);
		InputStreamReader isr = new InputStreamReader(fis);
		BufferedReader reader = new BufferedReader(isr);

		String linea;
		while ((linea = reader.readLine()) != null) {
			sb.append(linea).append("\n");
		}

		Resultado.setText(sb.toString());

	} catch (IOException e) {
		Toast.makeText(this, "Error al leer el archivo", Toast.LENGTH_SHORT).show();
	}
}
```

Comprueba que el archivo exista, lo lee línea por línea y lo muestra en pantalla.

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

Crean el contenedor principal de la interfaz.

### Líneas 9 a 22

```xml
<EditText
	android:id="@+id/Escribe"
	android:layout_width="250dp"
	android:layout_height="39dp"
	android:layout_marginStart="50dp"
	android:layout_marginTop="50dp"
	android:layout_marginEnd="105dp"
	android:layout_marginBottom="35dp"
	android:ems="10"
	android:inputType="text"
	android:text="Escribe"
	app:layout_constraintBottom_toTopOf="@+id/btnGuardar"
	app:layout_constraintEnd_toEndOf="parent"
	app:layout_constraintStart_toStartOf="parent"
	app:layout_constraintTop_toTopOf="parent" />
```

Definen el campo donde el usuario escribe el texto.

### Líneas 24 a 37

```xml
<Button
	android:id="@+id/btnGuardar"
	android:layout_width="250dp"
	android:layout_height="51dp"
	android:layout_marginStart="100dp"
	android:layout_marginEnd="100dp"
	android:layout_marginBottom="20dp"
	android:text="Guardar Archivo"
	app:layout_constraintBottom_toTopOf="@+id/btnLeer"
	app:layout_constraintEnd_toEndOf="parent"
	app:layout_constraintHorizontal_bias="0.512"
	app:layout_constraintStart_toStartOf="parent" />
```

Crean el botón para guardar el texto en el archivo.

### Líneas 39 a 52

```xml
<Button
	android:id="@+id/btnLeer"
	android:layout_width="250dp"
	android:layout_height="51dp"
	android:layout_marginStart="100dp"
	android:layout_marginEnd="100dp"
	android:layout_marginBottom="28dp"
	android:text="Leer"
	app:layout_constraintBottom_toTopOf="@+id/Resultado"
	app:layout_constraintEnd_toEndOf="parent"
	app:layout_constraintHorizontal_bias="0.512"
	app:layout_constraintStart_toStartOf="parent" />
```

Crean el botón para leer el contenido guardado.

### Líneas 54 a 63

```xml
<TextView
	android:id="@+id/Resultado"
	android:layout_width="match_parent"
	android:layout_height="wrap_content"
	android:layout_marginTop="50dp"
	android:text="TextView"
	android:textAlignment="center"
	app:layout_constraintEnd_toEndOf="parent"
	app:layout_constraintHorizontal_bias="0.498"
	app:layout_constraintStart_toStartOf="parent"
	app:layout_constraintTop_toBottomOf="@+id/btnLeer" />
```

Muestran el texto leído desde el archivo.

## Para el examen

La diferencia clave con lab2 es que aquí el archivo se guarda en almacenamiento externo privado de la app, no en almacenamiento interno.