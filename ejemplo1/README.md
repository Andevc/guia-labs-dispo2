# ejemplo1

## Qué hace el proyecto

Muestra un formulario con nombre, apellidos y carnet. Al presionar Mostrar, envía los datos a otra actividad, donde se concatenan el nombre completo y el carnet invertido.

## MainActivity.java

### Línea 1

```java
package com.movil.ejemplo1;
```

Declara el paquete de la actividad principal.

### Líneas 3 a 12

```java
import android.os.Bundle;

import androidx.activity.EdgeToEdge;
import androidx.appcompat.app.AppCompatActivity;
import androidx.core.graphics.Insets;
import androidx.core.view.ViewCompat;
import androidx.core.view.WindowInsetsCompat;
import androidx.appcompat.app.AppCompatActivity;
import android.content.Intent;
import android.widget.Button;
import android.widget.EditText;
```

Importan las clases para la pantalla, los controles y el paso de datos entre actividades.

### Líneas 13 a 14

```java
public class MainActivity extends AppCompatActivity {
	private EditText campoNombres, campoApellidos, campoCarnet;
	private Button botonMostrar, botonSalir;
```

Declaran la pantalla y los controles que se van a usar.

### Líneas 18 a 39

```java
@Override
protected void onCreate(Bundle savedInstanceState) {
	super.onCreate(savedInstanceState);
	setContentView(R.layout.activity_main);
	campoNombres = findViewById(R.id.idNombres);
	campoApellidos = findViewById(R.id.idApellidos);
	campoCarnet = findViewById(R.id.idCarnet);
	botonMostrar = findViewById(R.id.btnMostrar);
	botonSalir = findViewById(R.id.btnSalir);
	botonMostrar.setOnClickListener(v -> {
		String nombre = campoNombres.getText().toString();
		String apellidos = campoApellidos.getText().toString();
		String carnet = campoCarnet.getText().toString();
		Intent siguiente = new Intent(MainActivity.this, ResultadoActivity.class);
		siguiente.putExtra("nombre", nombre);
		siguiente.putExtra("apellidos", apellidos);
		siguiente.putExtra("carnet", carnet);
		startActivity(siguiente);
	});
	botonSalir.setOnClickListener(v -> finish());
}
```

Carga la interfaz, recoge lo que escribió el usuario y abre la segunda pantalla enviando los datos por Intent.

## ResultadoActivity.java

### Línea 1

```java
package com.movil.ejemplo1;
```

Declara el paquete de la segunda pantalla.

### Líneas 3 a 6

```java
import android.os.Bundle;
import android.widget.TextView;
import androidx.appcompat.app.AppCompatActivity;
```

Importan las clases necesarias para mostrar el resultado.

### Líneas 7 a 26

```java
public class ResultadoActivity extends AppCompatActivity {
	private TextView cilnvertido, nombreMod;

	@Override
	protected void onCreate(Bundle savedInstanceState) {
		super.onCreate(savedInstanceState);
		setContentView(R.layout.activity_resultado);
		nombreMod = findViewById(R.id.idNomComp);
		cilnvertido = findViewById(R.id.idCarnetInv);
		String nombre = getIntent().getStringExtra("nombre");
		String apellidos = getIntent().getStringExtra("apellidos");
		String carnet = getIntent().getStringExtra("carnet");
		if (nombre == null) nombre = "";
		if (apellidos == null) apellidos = "";
		if (carnet == null) carnet = "";
		String carnetInvertido = new StringBuilder(carnet).reverse().toString();
		String nombreModificado = nombre + " " + apellidos;
		cilnvertido.setText(carnetInvertido);
		nombreMod.setText(nombreModificado);
	}
}
```

Recibe los datos enviados, evita nulos, invierte el carnet y muestra el nombre completo.

## activity_main.xml

### Líneas 1 a 146

```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
	xmlns:app="http://schemas.android.com/apk/res-auto"
	xmlns:tools="http://schemas.android.com/tools"
	android:id="@+id/main"
	android:layout_width="match_parent"
	android:layout_height="match_parent"
	tools:context=".MainActivity">

	<TextView
		android:id="@+id/textView"
		android:layout_width="wrap_content"
		android:layout_height="wrap_content"
		android:layout_marginBottom="1dp"
		android:text="EJEMPLO 1"
		android:textSize="34sp"
		app:layout_constraintBottom_toTopOf="@+id/constraintLayout"
		app:layout_constraintEnd_toEndOf="parent"
		app:layout_constraintStart_toStartOf="parent"
		app:layout_constraintTop_toTopOf="parent" />

	<androidx.constraintlayout.widget.ConstraintLayout
		android:id="@+id/constraintLayout"
		android:layout_width="400dp"
		android:layout_height="300dp"
		android:layout_marginStart="1dp"
		android:layout_marginTop="1dp"
		android:layout_marginEnd="1dp"
		android:layout_marginBottom="1dp"
		app:layout_constraintBottom_toTopOf="@+id/constraintLayout2"
		app:layout_constraintEnd_toEndOf="parent"
		app:layout_constraintStart_toStartOf="parent"
		app:layout_constraintTop_toBottomOf="@+id/textView">

		<TextView
			android:id="@+id/textView3"
			android:layout_width="wrap_content"
			android:layout_height="wrap_content"
			android:layout_marginStart="50dp"
			android:layout_marginTop="32dp"
			android:layout_marginEnd="24dp"
			android:layout_marginBottom="32dp"
			android:text="Nombres"
			app:layout_constraintBottom_toTopOf="@+id/textView6"
			app:layout_constraintEnd_toStartOf="@+id/idNombres"
			app:layout_constraintHorizontal_bias="0.0"
			app:layout_constraintStart_toStartOf="parent"
			app:layout_constraintTop_toTopOf="parent" />

		<TextView
			android:id="@+id/textView6"
			android:layout_width="wrap_content"
			android:layout_height="wrap_content"
			android:layout_marginStart="50dp"
			android:layout_marginTop="32dp"
			android:layout_marginEnd="24dp"
			android:layout_marginBottom="32dp"
			android:text="Apellidos"
			app:layout_constraintBottom_toTopOf="@+id/textView7"
			app:layout_constraintEnd_toStartOf="@+id/idApellidos"
			app:layout_constraintStart_toStartOf="parent"
			app:layout_constraintTop_toBottomOf="@+id/textView3" />

		<TextView
			android:id="@+id/textView7"
			android:layout_width="wrap_content"
			android:layout_height="wrap_content"
			android:layout_marginStart="50dp"
			android:layout_marginTop="32dp"
			android:layout_marginEnd="24dp"
			android:layout_marginBottom="76dp"
			android:text="Carnet"
			app:layout_constraintBottom_toBottomOf="parent"
			app:layout_constraintEnd_toStartOf="@+id/idCarnet"
			app:layout_constraintStart_toStartOf="parent"
			app:layout_constraintTop_toBottomOf="@+id/textView6" />

		<EditText
			android:id="@+id/idNombres"
			android:layout_width="wrap_content"
			android:layout_height="wrap_content"
			android:layout_marginStart="46dp"
			android:layout_marginTop="32dp"
			android:layout_marginEnd="36dp"
			android:layout_marginBottom="24dp"
			android:ems="10"
			android:inputType="text"
			app:layout_constraintBottom_toTopOf="@+id/idApellidos"
			app:layout_constraintEnd_toEndOf="parent"
			app:layout_constraintStart_toEndOf="@+id/textView3"
			app:layout_constraintTop_toTopOf="parent" />

		<EditText
			android:id="@+id/idApellidos"
			android:layout_width="wrap_content"
			android:layout_height="wrap_content"
			android:layout_marginStart="45dp"
			android:layout_marginTop="24dp"
			android:layout_marginEnd="36dp"
			android:layout_marginBottom="24dp"
			android:ems="10"
			android:inputType="text"
			app:layout_constraintBottom_toTopOf="@+id/idCarnet"
			app:layout_constraintEnd_toEndOf="parent"
			app:layout_constraintStart_toEndOf="@+id/textView6"
			app:layout_constraintTop_toBottomOf="@+id/idNombres" />

		<EditText
			android:id="@+id/idCarnet"
			android:layout_width="wrap_content"
			android:layout_height="wrap_content"
			android:layout_marginStart="50dp"
			android:layout_marginTop="24dp"
			android:layout_marginEnd="36dp"
			android:layout_marginBottom="69dp"
			android:ems="10"
			android:inputType="text"
			app:layout_constraintBottom_toBottomOf="parent"
			app:layout_constraintEnd_toEndOf="parent"
			app:layout_constraintStart_toEndOf="@+id/textView7"
			app:layout_constraintTop_toBottomOf="@+id/idApellidos" />

	</androidx.constraintlayout.widget.ConstraintLayout>

	<androidx.constraintlayout.widget.ConstraintLayout
		android:id="@+id/constraintLayout2"
		android:layout_width="400dp"
		android:layout_height="100dp"
		android:layout_marginStart="1dp"
		android:layout_marginTop="1dp"
		android:layout_marginEnd="1dp"
		app:layout_constraintBottom_toBottomOf="parent"
		app:layout_constraintEnd_toEndOf="parent"
		app:layout_constraintStart_toStartOf="parent"
		app:layout_constraintTop_toBottomOf="@+id/constraintLayout">

		<Button
			android:id="@+id/btnMostrar"
			android:layout_width="wrap_content"
			android:layout_height="wrap_content"
			android:layout_marginStart="50dp"
			android:layout_marginTop="26dp"
			android:layout_marginEnd="50dp"
			android:layout_marginBottom="26dp"
			android:text="Mostrar"
			app:layout_constraintBottom_toBottomOf="parent"
			app:layout_constraintEnd_toStartOf="@+id/btnSalir"
			app:layout_constraintStart_toStartOf="parent"
			app:layout_constraintTop_toTopOf="parent" />

		<Button
			android:id="@+id/btnSalir"
			android:layout_width="wrap_content"
			android:layout_height="wrap_content"
			android:layout_marginStart="50dp"
			android:layout_marginTop="26dp"
			android:layout_marginEnd="50dp"
			android:layout_marginBottom="26dp"
			android:text="Salir"
			app:layout_constraintBottom_toBottomOf="parent"
			app:layout_constraintEnd_toEndOf="parent"
			app:layout_constraintStart_toEndOf="@+id/btnMostrar"
			app:layout_constraintTop_toTopOf="parent" />
	</androidx.constraintlayout.widget.ConstraintLayout>

	<TextView
		android:id="@+id/textView8"
		android:layout_width="wrap_content"
		android:layout_height="wrap_content"
		android:layout_marginStart="62dp"
		android:layout_marginTop="23dp"
		android:layout_marginEnd="140dp"
		android:layout_marginBottom="31dp"
		android:text="Cristhian Andres Escobar Herrera"
		app:layout_constraintBottom_toTopOf="@+id/constraintLayout"
		app:layout_constraintEnd_toEndOf="parent"
		app:layout_constraintStart_toStartOf="parent"
		app:layout_constraintTop_toBottomOf="@+id/textView" />

</androidx.constraintlayout.widget.ConstraintLayout>
```

Este layout organiza el formulario, los botones y la información del autor.

## activity_resultado.xml

### Líneas 1 a 83

```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
	xmlns:app="http://schemas.android.com/apk/res-auto"
	xmlns:tools="http://schemas.android.com/tools"
	android:layout_width="match_parent"
	android:layout_height="match_parent">

	<TextView
		android:id="@+id/textView"
		android:layout_width="wrap_content"
		android:layout_height="wrap_content"
		android:layout_marginStart="104dp"
		android:layout_marginTop="64dp"
		android:layout_marginEnd="106dp"
		android:layout_marginBottom="16dp"
		android:text="DATOS RECOLECTADOS"
		android:textAlignment="center"
		android:textSize="34sp"
		app:layout_constraintBottom_toTopOf="@+id/constraintLayout"
		app:layout_constraintEnd_toEndOf="parent"
		app:layout_constraintHorizontal_bias="0.493"
		app:layout_constraintStart_toStartOf="parent"
		app:layout_constraintTop_toTopOf="parent" />

	<androidx.constraintlayout.widget.ConstraintLayout
		android:id="@+id/constraintLayout3"
		android:layout_width="409dp"
		android:layout_height="300dp"
		android:layout_marginStart="1dp"
		android:layout_marginTop="30dp"
		android:layout_marginEnd="1dp"
		android:layout_marginBottom="303dp"
		app:layout_constraintBottom_toBottomOf="parent"
		app:layout_constraintEnd_toEndOf="parent"
		app:layout_constraintHorizontal_bias="1.0"
		app:layout_constraintStart_toStartOf="parent"
		app:layout_constraintTop_toBottomOf="@+id/textView"
		app:layout_constraintVertical_bias="0.0">

		<TextView
			android:id="@+id/textView10"
			android:layout_width="wrap_content"
			android:layout_height="wrap_content"
			android:layout_marginStart="39dp"
			android:layout_marginTop="16dp"
			android:layout_marginEnd="199dp"
			android:layout_marginBottom="16dp"
			android:text="NOMBRE COMPLETO"
			android:textSize="18sp"
			app:layout_constraintBottom_toTopOf="@+id/idNomComp"
			app:layout_constraintEnd_toEndOf="parent"
			app:layout_constraintStart_toStartOf="parent"
			app:layout_constraintTop_toTopOf="parent" />

		<TextView
			android:id="@+id/textView6"
			android:layout_width="wrap_content"
			android:layout_height="wrap_content"
			android:layout_marginStart="39dp"
			android:layout_marginTop="12dp"
			android:layout_marginEnd="301dp"
			android:layout_marginBottom="16dp"
			android:text="CARNET"
			android:textSize="18sp"
			app:layout_constraintBottom_toTopOf="@+id/idCarnetInv"
			app:layout_constraintEnd_toEndOf="parent"
			app:layout_constraintStart_toStartOf="parent"
			app:layout_constraintTop_toBottomOf="@+id/idNomComp" />

		<TextView
			android:id="@+id/idNomComp"
			android:layout_width="350dp"
			android:layout_height="40dp"
			android:layout_marginStart="39dp"
			android:layout_marginEnd="20dp"
			android:layout_marginBottom="16dp"
			android:textSize="20sp"
			app:layout_constraintBottom_toTopOf="@+id/textView6"
			app:layout_constraintEnd_toEndOf="parent"
			app:layout_constraintStart_toStartOf="parent"
			app:layout_constraintTop_toBottomOf="@+id/textView10" />

		<TextView
			android:id="@+id/idCarnetInv"
			android:layout_width="350dp"
			android:layout_height="40dp"
			android:layout_marginStart="39dp"
			android:layout_marginEnd="20dp"
			android:layout_marginBottom="16dp"
			android:textSize="20sp"
			app:layout_constraintBottom_toBottomOf="parent"
			app:layout_constraintEnd_toEndOf="parent"
			app:layout_constraintStart_toStartOf="parent"
			app:layout_constraintTop_toBottomOf="@+id/textView6" />
	</androidx.constraintlayout.widget.ConstraintLayout>

	<TextView
		android:id="@+id/textView2"
		android:layout_width="wrap_content"
		android:layout_height="wrap_content"
		android:layout_marginStart="24dp"
		android:layout_marginTop="8dp"
		android:layout_marginBottom="3dp"
		android:text="Cristhian Andres Escobar Herrera"
		app:layout_constraintBottom_toTopOf="@+id/constraintLayout3"
		app:layout_constraintEnd_toEndOf="parent"
		app:layout_constraintStart_toStartOf="parent"
		app:layout_constraintTop_toBottomOf="@+id/textView" />
</androidx.constraintlayout.widget.ConstraintLayout>
```

Este layout muestra los datos recibidos desde la primera pantalla.

## Para el examen

La idea clave es el paso de datos entre actividades usando Intent y putExtra, y luego reconstruir la información recibida en la segunda pantalla.