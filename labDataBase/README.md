# labDataBase

## Qué hace el proyecto

Es una plantilla Android básica sin lógica adicional visible en el código fuente revisado. La actividad principal solo carga la vista y ajusta los Insets del sistema.

## MainActivity.java

### Línea 1

```java
package com.movil.labdatabase;
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

Importan las clases para usar Edge-to-Edge y ajustar márgenes según las barras del sistema.

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

Inicializa la actividad, activa Edge-to-Edge, carga el layout y ajusta el padding de la vista principal.

## Para el examen

Este proyecto sirve como base vacía para empezar a construir una interfaz más compleja.