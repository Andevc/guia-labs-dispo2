# formulario

## Qué hace el proyecto

Simula una ficha de inscripción. El usuario completa varios campos, guarda todo en un archivo de texto interno y luego puede volver a cargar los datos en los EditText y en un TextView resumen.

## MainActivity.java

### Línea 1

```java
package com.movil.formulario;
```

Declara el paquete principal.

### Líneas 3 a 15

```java
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
import java.io.InputStreamReader;
```

Traen las clases para la interfaz, Edge-to-Edge y lectura o escritura de archivos.

### Líneas 19 a 26

```java
private EditText etNombre, etLugarFecha, etDNI, etCorreo, etDireccion, etCP, etCiudad, etMovil, etFecha, etFirma;
private Button btnGuardar, btnLeer;
private final String FILE_NAME = "datos_formulario.txt";
```

Declaran todos los campos del formulario, los botones y el nombre del archivo interno.

### Líneas 28 a 57

```java
@Override
protected void onCreate(Bundle savedInstanceState) {
	super.onCreate(savedInstanceState);
	EdgeToEdge.enable(this);
	setContentView(R.layout.activity_main);

	View mainView = findViewById(R.id.main);
	if (mainView != null) {
		ViewCompat.setOnApplyWindowInsetsListener(mainView, (v, insets) -> {
			Insets systemBars = insets.getInsets(WindowInsetsCompat.Type.systemBars());
			v.setPadding(systemBars.left, systemBars.top, systemBars.right, systemBars.bottom);
			return insets;
		});
	}

	etNombre = findViewById(R.id.etNombre);
	etLugarFecha = findViewById(R.id.etLugarFecha);
	etDNI = findViewById(R.id.etDNI);
	etCorreo = findViewById(R.id.etCorreo);
	etDireccion = findViewById(R.id.etDireccion);
	etCP = findViewById(R.id.etCP);
	etCiudad = findViewById(R.id.etCiudad);
	etMovil = findViewById(R.id.etMovil);
	etFecha = findViewById(R.id.etFecha);
	etFirma = findViewById(R.id.etFirma);

	btnGuardar = findViewById(R.id.btnGuardar);
	btnLeer = findViewById(R.id.btnLeer);

	btnGuardar.setOnClickListener(new View.OnClickListener() {
		@Override
		public void onClick(View v) {
			guardarDatos();
		}
	});

	btnLeer.setOnClickListener(new View.OnClickListener() {
		@Override
		public void onClick(View v) {
			leerDatos();
		}
	});
}
```

Inicializa la pantalla, ajusta los márgenes y conecta los campos y botones con sus funciones.

### Líneas 70 a 87

```java
private void guardarDatos() {
	String datos = etNombre.getText().toString() + "\n" +
			etLugarFecha.getText().toString() + "\n" +
			etDNI.getText().toString() + "\n" +
			etCorreo.getText().toString() + "\n" +
			etDireccion.getText().toString() + "\n" +
			etCP.getText().toString() + "\n" +
			etCiudad.getText().toString() + "\n" +
			etMovil.getText().toString() + "\n" +
			etFecha.getText().toString() + "\n" +
			etFirma.getText().toString();

	try (FileOutputStream fos = openFileOutput(FILE_NAME, MODE_PRIVATE)) {
		fos.write(datos.getBytes());
		Toast.makeText(this, "Datos guardados correctamente", Toast.LENGTH_SHORT).show();
	} catch (Exception e) {
		e.printStackTrace();
		Toast.makeText(this, "Error al guardar: " + e.getMessage(), Toast.LENGTH_SHORT).show();
	}
}
```

Une todos los campos en un solo texto, lo guarda en un archivo interno y muestra un mensaje al usuario.

### Líneas 89 a 146

```java
private void leerDatos() {
	try (FileInputStream fis = openFileInput(FILE_NAME);
		 InputStreamReader isr = new InputStreamReader(fis);
		 BufferedReader br = new BufferedReader(isr)) {

		String nombre     = br.readLine();
		String lugarFecha = br.readLine();
		String dni        = br.readLine();
		String correo     = br.readLine();
		String direccion  = br.readLine();
		String cp         = br.readLine();
		String ciudad     = br.readLine();
		String movil      = br.readLine();
		String fecha      = br.readLine();
		String firma      = br.readLine();

		etNombre.setText(nombre);
		etLugarFecha.setText(lugarFecha);
		etDNI.setText(dni);
		etCorreo.setText(correo);
		etDireccion.setText(direccion);
		etCP.setText(cp);
		etCiudad.setText(ciudad);
		etMovil.setText(movil);
		etFecha.setText(fecha);
		etFirma.setText(firma);

		TextView tvResultado = findViewById(R.id.Resultado);
		tvResultado.setText(
			"Nombre: "     + nombre     + "\n" +
			"Nac.: "       + lugarFecha + "\n" +
			"DNI: "        + dni        + "\n" +
			"Correo: "     + correo     + "\n" +
			"Dirección: "  + direccion  + "\n" +
			"CP: "         + cp         + "\n" +
			"Ciudad: "     + ciudad     + "\n" +
			"Móvil: "      + movil      + "\n" +
			"Fecha: "      + fecha      + "\n" +
			"Firma: "      + firma
		);

		Toast.makeText(this, "Datos cargados correctamente", Toast.LENGTH_SHORT).show();

	} catch (Exception e) {
		e.printStackTrace();
		Toast.makeText(this, "No se encontraron datos guardados", Toast.LENGTH_SHORT).show();
	}
}
```

Lee el archivo línea por línea, vuelve a llenar los campos del formulario y crea un resumen visible en pantalla.

## activity_main.xml

### Líneas 1 a 8

```xml
<ScrollView
	xmlns:android="http://schemas.android.com/apk/res/android"
	android:id="@+id/main"
	android:layout_width="match_parent"
	android:layout_height="match_parent"
	android:background="#F5F5F5">
```

Crean una vista desplazable con fondo gris claro.

### Líneas 10 a 14

```xml
<LinearLayout
	android:layout_width="match_parent"
	android:layout_height="wrap_content"
	android:orientation="vertical"
	android:padding="20dp"
	android:background="@android:color/white">
```

Definen el contenedor vertical principal del formulario.

### Líneas 16 a 27

```xml
<TextView
	android:layout_width="match_parent"
	android:layout_height="wrap_content"
	android:text="FICHA DE INSCRIPCIÓN"
	android:textSize="22sp"
	android:textStyle="bold"
	android:textColor="#1A237E"
	android:gravity="center"
	android:paddingBottom="4dp"/>

<TextView
	android:layout_width="match_parent"
	android:layout_height="wrap_content"
	android:text="GRUPO / FORMACIÓN"
	android:textSize="13sp"
	android:textColor="#5C6BC0"
	android:gravity="center"
	android:paddingBottom="16dp"/>
```

Muestran el título y subtítulo de la ficha.

### Líneas 39 a 295

Este bloque define cada etiqueta y campo del formulario, incluyendo nombre, lugar y fecha de nacimiento, correo, DNI, dirección, ciudad, CP, móvil, fecha, firma, botones guardar y leer, y el TextView Resultado.

## Para el examen

Este proyecto enseña cómo guardar un formulario completo en un archivo de texto y luego reconstruir la pantalla leyendo cada línea en el mismo orden.