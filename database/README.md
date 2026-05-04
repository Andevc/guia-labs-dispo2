# database

## Qué hace el proyecto

Es una app CRUD completa con SQLite. Permite listar personas, agregar nuevas, editar existentes y eliminar registros. Usa RecyclerView para mostrar la lista y una base de datos local para guardar los datos.

## MainActivity.java

### Línea 1

```java
package com.movil.database;
```

Declara el paquete donde vive esta clase.

### Líneas 3 a 12

```java
import android.app.AlertDialog;
import android.content.Intent;
import android.os.Bundle;
import android.widget.Button;
import android.widget.Toast;

import androidx.appcompat.app.AppCompatActivity;
import androidx.recyclerview.widget.LinearLayoutManager;
import androidx.recyclerview.widget.RecyclerView;
```

Importan las clases necesarias para mostrar la interfaz, abrir otras pantallas, usar botones, enseñar mensajes y trabajar con el RecyclerView.

### Línea 14

```java
public class MainActivity extends AppCompatActivity implements PersonaAdapter.OnPersonaClickListener {
```

Define la pantalla principal e indica que recibirá eventos de editar y eliminar desde el adaptador.

### Líneas 15 a 18

```java
private RecyclerView rvPersonas;
private PersonaAdapter adapter;
private DatabaseHelper dbHelper;
private Button btnAdd;
```

Declaran las variables que se usarán para mostrar la lista, manejar la base de datos y abrir la pantalla de agregado.

### Líneas 21 a 35

```java
@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_main);
    
    dbHelper = new DatabaseHelper(this);
    rvPersonas = findViewById(R.id.rvPersonas);
    btnAdd = findViewById(R.id.btnAdd);
    
    setupRecyclerView();
    
    btnAdd.setOnClickListener(v -> {
        Intent intent = new Intent(MainActivity.this, AddEditPersonaActivity.class);
        startActivity(intent);
    });
}
```

Esta parte inicia la pantalla, carga el layout, crea el helper de base de datos, enlaza las vistas, configura el RecyclerView y abre la pantalla para agregar una persona nueva.

### Líneas 38 a 41

```java
@Override
protected void onResume(){
    super.onResume();
    refreshList();
}
```

Cada vez que la pantalla vuelve a mostrarse, refresca la lista para traer los datos más recientes.

### Líneas 44 a 48

```java
private void refreshList() {
    if (adapter != null) {
        adapter.updateList(dbHelper.getAllPersonas());
    }
}
```

Vuelve a cargar los datos desde SQLite y se los pasa al adaptador.

### Líneas 51 a 55

```java
private void setupRecyclerView() {
    rvPersonas.setLayoutManager(new LinearLayoutManager(this));
    adapter = new PersonaAdapter(dbHelper.getAllPersonas(), this);
    rvPersonas.setAdapter(adapter);
}
```

Configura la lista vertical y conecta el adaptador con los datos de la base.

### Líneas 58 a 62

```java
@Override
public void onPersonaClick(Persona persona){
    Intent intent = new Intent(this, AddEditPersonaActivity.class);
    intent.putExtra("persona", persona);
    startActivity(intent);
}
```

Cuando se pulsa editar en una persona, abre la pantalla de edición y le envía el objeto completo.

### Líneas 65 a 77

```java
@Override
public void onDeleteClick(Persona persona){
    new AlertDialog.Builder(this)
            .setTitle("Eliminar Persona")
            .setMessage("¿Estas seguro de que deseas eliminar este registro?")
            .setPositiveButton("Eliminar", (dialog, which) -> {
                dbHelper.deletePersona(persona.getId());
                refreshList();
                Toast.makeText(this, "Persona eliminada", Toast.LENGTH_SHORT).show();
            })
            .setNegativeButton("Cancelar", null)
            .show();
}
```

Muestra una confirmación antes de borrar. Si el usuario acepta, elimina el registro, recarga la lista y muestra un mensaje.

## AddEditPersonaActivity.java

### Línea 1

```java
package com.movil.database;
```

Declara el paquete de la pantalla de agregar y editar.

### Líneas 3 a 11

```java
import android.os.Bundle;
import android.text.TextUtils;
import android.widget.Button;
import android.widget.EditText;
import android.widget.TextView;
import android.widget.Toast;

import androidx.appcompat.app.AppCompatActivity;
```

Importan las clases necesarias para leer los campos, validar datos y mostrar mensajes.

### Líneas 13 a 21

```java
public class AddEditPersonaActivity extends AppCompatActivity {

    private EditText etNombres, etApellidos, etCi;
    private Button btnSave;
    private TextView tvTitle;
    private DatabaseHelper dbHelper;
    private Persona existingPersona;
```

Declara la actividad, sus controles y la persona que se editará si ya venía cargada.

### Líneas 24 a 50

```java
@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_add_edit_persona);

    dbHelper = new DatabaseHelper(this);

    etNombres = findViewById(R.id.etNombres);
    etApellidos = findViewById(R.id.etApellidos);
    etCi = findViewById(R.id.etCi);
    btnSave = findViewById(R.id.btnSave);
    tvTitle = findViewById(R.id.tvTitle);

    if (getIntent().hasExtra("persona")) {
        existingPersona = (Persona)
                getIntent().getSerializableExtra("persona");

        etNombres.setText(existingPersona.getNombres());
        etApellidos.setText(existingPersona.getApellidos());
        etCi.setText(existingPersona.getCi());

        tvTitle.setText("Editar Persona");
        btnSave.setText("Actualizar");
    }

    btnSave.setOnClickListener(v -> savePersona());
}
```

Carga el formulario, detecta si viene una persona para editar y cambia el modo de la pantalla cuando corresponde.

### Líneas 53 a 88

```java
private void savePersona() {
    String nombres = etNombres.getText().toString().trim();
    String apellidos = etApellidos.getText().toString().trim();
    String ciStr = etCi.getText().toString().trim();

    if (TextUtils.isEmpty(nombres) ||
            TextUtils.isEmpty(apellidos) ||
            TextUtils.isEmpty(ciStr)) {

        Toast.makeText(this,
                "Por favor completa todos los campos",
                Toast.LENGTH_SHORT).show();
        return;
    }

    if (existingPersona != null) {
        existingPersona.setNombres(nombres);
        existingPersona.setApellidos(apellidos);
        existingPersona.setCi(ciStr);

        dbHelper.updatePersona(existingPersona);

        Toast.makeText(this,
                "Persona actualizada",
                Toast.LENGTH_SHORT).show();

    } else {
        Persona newPersona =
                new Persona(nombres, apellidos, ciStr);

        dbHelper.addPersona(newPersona);

        Toast.makeText(this,
                "Persona guardada",
                Toast.LENGTH_SHORT).show();
    }

    finish();
}
```

Valida que no haya campos vacíos. Si ya existía una persona, la actualiza; si no, crea una nueva y la guarda.

## DatabaseHelper.java

### Línea 1

```java
package com.movil.database;
```

Declara el paquete donde vive la clase de base de datos.

### Líneas 3 a 12

```java
import android.annotation.SuppressLint;
import android.content.ContentValues;
import android.content.Context;
import android.database.Cursor;
import android.database.sqlite.SQLiteDatabase;
import android.database.sqlite.SQLiteOpenHelper;

import java.util.ArrayList;
import java.util.List;
```

Importan las clases que permiten crear, consultar, actualizar y eliminar datos en SQLite.

### Líneas 14 a 26

```java
public class DatabaseHelper extends SQLiteOpenHelper {

    private static final String DATABASE_NAME = "personas.db";
    private static final int DATABASE_VERSION = 1;
    private static final String TABLE_PERSONAS = "personas";
    private static final String COLUMN_ID = "id";
    private static final String COLUMN_NOMBRES = "nombres";
    private static final String COLUMN_APELLIDOS = "apellidos";
    private static final String COLUMN_CI = "ci";

    private static final String CREATE_TABLE = "CREATE TABLE " + TABLE_PERSONAS + " ("
            + COLUMN_ID + " INTEGER PRIMARY KEY AUTOINCREMENT, "
            + COLUMN_NOMBRES + " TEXT NOT NULL, "
            + COLUMN_APELLIDOS + " TEXT NOT NULL, "
            + COLUMN_CI + " TEXT NOT NULL)";
```

Define el nombre de la base, la versión, la tabla, sus columnas y la instrucción SQL para crearla.

### Líneas 28 a 38

```java
DatabaseHelper(Context context){
    super(context, DATABASE_NAME, null, DATABASE_VERSION);
}

@Override
public void onCreate(SQLiteDatabase db){
  db.execSQL(CREATE_TABLE);
}

@Override
public void onUpgrade(SQLiteDatabase db, int oldVersion, int newVersion){
    db.execSQL("DROP TABLE IF EXISTS "+ TABLE_PERSONAS);
    onCreate(db);
}
```

Inicializa el helper, crea la tabla cuando la base aparece por primera vez y la vuelve a crear si cambia la versión.

### Líneas 43 a 51

```java
public long addPersona(Persona persona){
    SQLiteDatabase db = this.getWritableDatabase();
    ContentValues values = new ContentValues();
    values.put(COLUMN_NOMBRES, persona.getNombres());
    values.put(COLUMN_APELLIDOS, persona.getApellidos());
    values.put(COLUMN_CI, persona.getCi());

    return db.insert(TABLE_PERSONAS, null, values);
}
```

Inserta una persona nueva usando los valores del objeto Persona.

### Líneas 55 a 78

```java
@SuppressLint("Range")
public List<Persona> getAllPersonas() {
    List<Persona> personas = new ArrayList<>();
    String selectQuery = "SELECT * FROM " + TABLE_PERSONAS
            + " ORDER BY " + COLUMN_ID + " DESC";
    SQLiteDatabase db = this.getReadableDatabase();
    Cursor cursor = db.rawQuery(selectQuery, null);

    if (cursor.moveToFirst()) {
        do {
            Persona persona = new Persona(
                    cursor.getInt(cursor.getColumnIndex(COLUMN_ID)),
                    cursor.getString(cursor.getColumnIndex(COLUMN_NOMBRES)),
                    cursor.getString(cursor.getColumnIndex(COLUMN_APELLIDOS)),
                    cursor.getString(cursor.getColumnIndex(COLUMN_CI))
            );
            personas.add(persona);
        } while (cursor.moveToNext());
    }

    cursor.close();
    db.close();
    return personas;
}
```

Lee todos los registros, recorre el Cursor y convierte cada fila en un objeto Persona para llenar la lista.

### Líneas 82 a 90

```java
public int updatePersona(Persona persona) {
    SQLiteDatabase db = this.getWritableDatabase();
    ContentValues values = new ContentValues();
    values.put(COLUMN_NOMBRES, persona.getNombres());
    values.put(COLUMN_APELLIDOS, persona.getApellidos());
    values.put(COLUMN_CI, persona.getCi());

    return db.update(TABLE_PERSONAS, values,
            COLUMN_ID + " = ?",
            new String[]{String.valueOf(persona.getId())});
}
```

Actualiza una fila concreta usando el id de la persona.

### Líneas 94 a 100

```java
public void deletePersona(int id) {
    SQLiteDatabase db = this.getWritableDatabase();
    db.delete(TABLE_PERSONAS,
            COLUMN_ID + " = ?",
            new String[]{String.valueOf(id)});
    db.close();
}
```

Elimina un registro por id y cierra la base.

## Persona.java

### Líneas 1 a 44

```java
package com.movil.database;

import java.io.Serializable;

public class Persona implements Serializable {
    private int id;
    private String nombres;
    private String apellidos;
    private String ci;

    public Persona(int id, String nombres, String apellidos, String ci) {
        this.id = id;
        this.nombres = nombres;
        this.apellidos = apellidos;
        this.ci = ci;
    }

    public Persona(String nombres, String apellidos, String ci) {
        this.nombres = nombres;
        this.apellidos = apellidos;
        this.ci = ci;
    }

    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    public String getNombres() {
        return nombres;
    }

    public void setNombres(String nombres) {
        this.nombres = nombres;
    }

    public String getApellidos() {
        return apellidos;
    }

    public void setApellidos(String apellidos) {
        this.apellidos = apellidos;
    }

    public String getCi() {
        return ci;
    }

    public void setCi(String ci) {
        this.ci = ci;
    }
}
```

Representa una persona en memoria y permite enviar el objeto entre actividades porque implementa Serializable.

## PersonaAdapter.java

### Líneas 1 a 77

```java
package com.movil.database;

import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;
import android.widget.Button;
import android.widget.TextView;

import androidx.annotation.NonNull;
import androidx.recyclerview.widget.RecyclerView;

import java.util.List;

public class PersonaAdapter extends
        RecyclerView.Adapter<PersonaAdapter.PersonaViewHolder> {

    private List<Persona> personalist;
    private OnPersonaClickListener listener;

    public interface OnPersonaClickListener {
        void onPersonaClick(Persona persona);
        void onDeleteClick(Persona persona);
    }

    public PersonaAdapter(List<Persona> personalist,
                          OnPersonaClickListener listener) {
        this.personalist = personalist;
        this.listener = listener;
    }

    @NonNull
    @Override
    public PersonaViewHolder onCreateViewHolder(@NonNull
                                                ViewGroup parent, int viewType) {
        View view = LayoutInflater.from(parent.getContext())
                .inflate(R.layout.item_persona, parent, false);
        return new PersonaViewHolder(view);
    }

    @Override
    public void onBindViewHolder(@NonNull
                                 PersonaViewHolder holder, int position) {

        Persona persona = personalist.get(position);

        holder.tvNombres.setText(persona.getNombres());
        holder.tvApellidos.setText(persona.getApellidos());
        holder.tvCi.setText("CI: " + persona.getCi());

        holder.btnEdit.setOnClickListener(v ->
                listener.onPersonaClick(persona));

        holder.btnDelete.setOnClickListener(v ->
                listener.onDeleteClick(persona));
    }

    @Override
    public int getItemCount() {
        return personalist.size();
    }

    public void updateList(List<Persona> newList) {
        this.personalist = newList;
        notifyDataSetChanged();
    }

    public static class PersonaViewHolder extends RecyclerView.ViewHolder {

        TextView tvNombres, tvApellidos, tvCi;
        Button btnDelete, btnEdit;

        public PersonaViewHolder(@NonNull View itemView) {
            super(itemView);

            tvNombres = itemView.findViewById(R.id.tvNombres);
            tvApellidos = itemView.findViewById(R.id.tvApellidos);
            tvCi = itemView.findViewById(R.id.tvCi);

            btnDelete = itemView.findViewById(R.id.btnDelete);
            btnEdit = itemView.findViewById(R.id.btnEdit);
        }
    }
}
```

Este adaptador pinta cada persona dentro del RecyclerView y conecta los botones Editar y Eliminar con la actividad principal.

## activity_main.xml

### Línea 1 a 44

```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:padding="32dp">

    <TextView
        android:id="@+id/tvTitulo"
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:text="Lista de Personas"
        android:textSize="20sp"
        android:textStyle="bold"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintEnd_toStartOf="@id/btnAdd"
        app:layout_constraintTop_toTopOf="parent" />

    <Button
        android:id="@+id/btnAdd"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Añadir"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintEnd_toEndOf="parent" />

    <androidx.recyclerview.widget.RecyclerView
        android:id="@+id/rvPersonas"
        android:layout_width="0dp"
        android:layout_height="0dp"
        app:layout_constraintTop_toBottomOf="@id/tvTitulo"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintBottom_toBottomOf="parent"
        android:layout_marginTop="16dp"/>

</androidx.constraintlayout.widget.ConstraintLayout>
```

Muestra el título, el botón Añadir y el RecyclerView que contiene la lista de personas.

## activity_add_edit_persona.xml

### Línea 1 a 57

```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:padding="32dp">

    <TextView
        android:id="@+id/tvTitle"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Añadir Persona"
        android:textSize="24sp"
        android:textStyle="bold"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        android:layout_marginBottom="24dp"/>

    <EditText
        android:id="@+id/etNombres"
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:hint="Nombres"
        android:layout_marginTop="16dp"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@id/tvTitle" />

    <EditText
        android:id="@+id/etApellidos"
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:layout_marginTop="16dp"
        android:hint="Apellidos"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@id/etNombres" />

    <EditText
        android:id="@+id/etCi"
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:layout_marginTop="16dp"
        android:hint="CI"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@id/etApellidos" />

    <Button
        android:id="@+id/btnSave"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="24dp"
        android:text="GUARDAR"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@id/etCi" />

</androidx.constraintlayout.widget.ConstraintLayout>
```

Es el formulario donde se capturan o actualizan los datos de una persona.

## item_persona.xml

### Línea 1 a 84

```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.cardview.widget.CardView
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:layout_margin="8dp"
    app:cardCornerRadius="8dp"
    app:cardElevation="4dp">

    <androidx.constraintlayout.widget.ConstraintLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:padding="16dp">

        <TextView
            android:id="@+id/tvNombres"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_marginEnd="8dp"
            android:text="Nombres"
            android:textColor="@android:color/black"
            android:textSize="18sp"
            android:textStyle="bold"
            app:layout_constraintEnd_toStartOf="@+id/btnEdit"
            app:layout_constraintStart_toStartOf="parent"
            app:layout_constraintTop_toTopOf="parent" />

        <TextView
            android:id="@+id/tvApellidos"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_marginTop="4dp"
            android:layout_marginEnd="8dp"
            android:text="Apellidos"
            android:textSize="16sp"
            app:layout_constraintEnd_toStartOf="@+id/btnEdit"
            app:layout_constraintStart_toStartOf="parent"
            app:layout_constraintTop_toBottomOf="@id/tvNombres" />

        <TextView
            android:id="@+id/tvCi"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_marginTop="4dp"
            android:layout_marginEnd="8dp"
            android:text="CI: 0000000"
            android:textColor="@android:color/darker_gray"
            android:textSize="14sp"
            app:layout_constraintEnd_toStartOf="@+id/btnEdit"
            app:layout_constraintStart_toStartOf="parent"
            app:layout_constraintTop_toBottomOf="@id/tvApellidos" />

        <Button
            android:id="@+id/btnEdit"
            style="?android:attr/buttonBarButtonStyle"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="EDITAR"
            android:textColor="@android:color/holo_blue_dark"
            app:layout_constraintEnd_toEndOf="parent"
            app:layout_constraintTop_toTopOf="parent" />

        <Button
            android:id="@+id/btnDelete"
            style="?android:attr/buttonBarButtonStyle"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_marginTop="4dp"
            android:text="ELIMINAR"
            android:textColor="@android:color/holo_red_dark"
            app:layout_constraintEnd_toEndOf="parent"
            app:layout_constraintTop_toBottomOf="@id/btnEdit" />

    </androidx.constraintlayout.widget.ConstraintLayout>
</androidx.cardview.widget.CardView>
```

Define la tarjeta visual que se repite por cada persona en la lista.

## Nota importante

El manifiesto de este proyecto declara AddPersonActivity, pero en el código revisado no aparece esa clase. Si el proyecto da error al compilar, ese es el primer punto a revisar.

## Para el examen

La idea central es el flujo completo: SQLite guarda los datos, RecyclerView los muestra, y la interfaz permite crear, editar y borrar personas.