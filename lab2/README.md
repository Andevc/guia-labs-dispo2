# lab2

## Qué hace el proyecto

Ejemplo de persistencia interna. El usuario escribe texto, lo guarda en un archivo privado de la app y luego puede leerlo desde el mismo almacenamiento.

## MainActivity.java

### Línea 1

```java
package com.movil.lab2;
```

Declara el paquete de la clase principal.

### Líneas 3 a 21

```java
import android.annotation.SuppressLint;
import android.content.Context;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.TextView;
import android.widget.Toast;

import androidx.activity.EdgeToEdge;
import androidx.appcompat.app.AppCompatActivity;
import androidx.core.graphics.Insets;
import androidx.core.view.ViewCompat;
import androidx.core.view.WindowInsetsCompat;

import java.io.BufferedReader;
import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.IOException;
import java.io.InputStreamReader;
import java.nio.Buffer;
```

Traen las clases para interfaz, almacenamiento interno y lectura o escritura de archivos.

### Líneas 23 a 25

```java
private EditText Escribe;
private TextView Resultado;
private final String nomArchivo="EjPersistencia.txt";
```

Declaran el campo de entrada, el resultado y el nombre del archivo que se va a guardar.

### Líneas 29 a 56

```java
@Override
protected void onCreate(Bundle savedInstanceState) {
	super.onCreate(savedInstanceState);
	EdgeToEdge.enable(this);
	setContentView(R.layout.activity_main);

	Escribe=findViewById(R.id.Escribe);
	Resultado=findViewById(R.id.Resultado);
	Button btnGuardar = findViewById(R.id.btnGuardar);
	Button btnLeer = findViewById(R.id.btnLeer);

	btnGuardar.setOnClickListener(new View.OnClickListener() {
		@Override
		public void onClick(View v) {
			String textoaGuardar = Escribe.getText().toString();
			guardarArchivo(textoaGuardar);
		}
	});

	btnLeer.setOnClickListener(new View.OnClickListener(){
			@Override
			public void onClick(View v){
				leerArchivo();
			}

	});
}
```

Inicializa la pantalla, enlaza las vistas y conecta los botones con las funciones de guardar y leer.

### Líneas 60 a 67

```java
private void guardarArchivo(String contenido) {
	try(FileOutputStream guarda=openFileOutput(nomArchivo, Context.MODE_PRIVATE)) {
		guarda.write(contenido.getBytes());
		Escribe.setText("");
		Toast.makeText(this, "Guardado en:"+getFilesDir(), Toast.LENGTH_LONG).show();
	}catch (IOException e){
		throw new RuntimeException(e);
	}
}
```

Guarda el texto en un archivo interno privado, limpia el campo y muestra la ruta donde quedó guardado.

### Líneas 69 a 84

```java
private void leerArchivo(){
	try(FileInputStream mostrar = openFileInput(nomArchivo);
		InputStreamReader isr = new InputStreamReader(mostrar);
		BufferedReader reader = new BufferedReader(isr);
	){
		StringBuilder sb=new StringBuilder();
		String linea;
		while((linea=reader.readLine()) != null){
			sb.append(linea).append("\n");
		}
		Resultado.setText(sb.toString());
	}
	catch(Exception e){
		throw new RuntimeException(e);
	}

}
```

Abre el archivo, lee cada línea y la muestra en el TextView Resultado.

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

Lo importante aquí es recordar que openFileOutput con MODE_PRIVATE guarda dentro del almacenamiento interno privado de la app y que openFileInput recupera exactamente ese mismo archivo.