# database

## Qué hace el proyecto

Es una app CRUD completa con SQLite. Permite listar personas, agregar nuevas, editar existentes y eliminar registros. Usa RecyclerView para mostrar la lista y una base de datos local para guardar los datos.

## MainActivity.java

- Línea 1: declara el paquete com.movil.database.
- Línea 3: deja espacio antes de los imports.
- Línea 4: importa AlertDialog para confirmar eliminaciones.
- Línea 5: importa Intent para abrir otra actividad.
- Línea 6: importa Bundle para el ciclo de vida.
- Línea 7: importa Button para el botón Añadir.
- Línea 8: importa Toast para mensajes breves.
- Línea 10: importa AppCompatActivity.
- Línea 11: importa LinearLayoutManager para ordenar la lista verticalmente.
- Línea 12: importa RecyclerView para mostrar las personas.
- Línea 14: declara la clase principal e implementa el listener del adaptador.
- Línea 15: declara el RecyclerView rvPersonas.
- Línea 16: declara el adaptador PersonaAdapter.
- Línea 17: declara el helper de base de datos.
- Línea 18: declara el botón btnAdd.
- Línea 21: abre onCreate.
- Línea 22: llama al método base de la actividad.
- Línea 23: carga activity_main.
- Línea 25: crea el helper de SQLite.
- Línea 26: enlaza el RecyclerView.
- Línea 27: enlaza el botón Añadir.
- Línea 29: configura el RecyclerView.
- Línea 31: abre el listener del botón Añadir.
- Línea 32: crea un Intent para AddEditPersonaActivity.
- Línea 33: inicia la pantalla para agregar una persona nueva.
- Línea 34: cierra el listener.
- Línea 35: cierra onCreate.
- Línea 38: abre onResume.
- Línea 39: llama al onResume de la clase padre.
- Línea 40: refresca la lista cuando la actividad vuelve a primer plano.
- Línea 41: cierra onResume.
- Línea 44: abre el método refreshList.
- Línea 45: verifica que el adaptador exista.
- Línea 46: actualiza el adaptador con los datos actuales de SQLite.
- Línea 47: cierra la condición.
- Línea 48: cierra el método.
- Línea 51: abre setupRecyclerView.
- Línea 52: coloca un LinearLayoutManager vertical.
- Línea 53: crea el adaptador con los datos cargados desde la base.
- Línea 54: asigna el adaptador al RecyclerView.
- Línea 55: cierra el método.
- Línea 58: abre onPersonaClick.
- Línea 59: crea un Intent para editar la persona.
- Línea 60: envía el objeto Persona como extra serializable.
- Línea 61: abre la pantalla de edición.
- Línea 62: cierra el método.
- Línea 65: abre onDeleteClick.
- Líneas 66 a 71: muestran un diálogo de confirmación antes de borrar.
- Línea 72: si el usuario acepta, borra la persona por id.
- Línea 73: refresca la lista para quitar el registro eliminado.
- Línea 74: muestra un mensaje de confirmación.
- Línea 76: cierra el diálogo sin borrar.
- Línea 77: muestra el cuadro de diálogo.
- Línea 78: cierra el método.
- Línea 79: cierra la clase.

## AddEditPersonaActivity.java

- Línea 1: declara el paquete.
- Línea 3: separa los imports.
- Línea 4: importa Bundle.
- Línea 5: importa TextUtils para validar campos vacíos.
- Línea 6: importa Button.
- Línea 7: importa EditText.
- Línea 8: importa TextView.
- Línea 9: importa Toast.
- Línea 11: importa AppCompatActivity.
- Línea 13: define la pantalla para agregar o editar.
- Línea 15: declara el campo de nombres.
- Línea 16: declara el campo de apellidos.
- Línea 17: declara el campo de CI.
- Línea 18: declara el botón Guardar.
- Línea 19: declara el título de la pantalla.
- Línea 20: declara el helper de base de datos.
- Línea 21: declara la persona que se edita, si existe.
- Línea 24: abre onCreate.
- Línea 25: llama al método base.
- Línea 26: carga activity_add_edit_persona.
- Línea 28: crea el helper de base de datos.
- Línea 30: enlaza el campo de nombres.
- Línea 31: enlaza el campo de apellidos.
- Línea 32: enlaza el campo de CI.
- Línea 33: enlaza el botón Guardar.
- Línea 34: enlaza el título.
- Línea 36: verifica si la actividad recibió una persona para editar.
- Línea 37: si la recibió, la recupera desde el Intent.
- Línea 40: coloca el nombre actual en el campo.
- Línea 41: coloca los apellidos actuales.
- Línea 42: coloca el CI actual.
- Línea 44: cambia el título a Editar Persona.
- Línea 45: cambia el botón a Actualizar.
- Línea 48: agrega el listener del botón Guardar.
- Línea 49: llama al método savePersona.
- Línea 50: cierra onCreate.
- Línea 53: abre savePersona.
- Línea 54: toma el texto de nombres y lo recorta.
- Línea 55: toma el texto de apellidos y lo recorta.
- Línea 56: toma el texto del CI y lo recorta.
- Líneas 58 a 63: validan que ningún campo esté vacío.
- Línea 65: muestra un mensaje si falta información.
- Línea 66: termina el método.
- Línea 69: verifica si se está editando una persona existente.
- Línea 70: actualiza el nombre en el objeto.
- Línea 71: actualiza los apellidos.
- Línea 72: actualiza el CI.
- Línea 74: llama al método updatePersona del helper.
- Línea 76: muestra un mensaje de actualización.
- Línea 79: si no existe persona previa, crea una nueva.
- Línea 80: instancia Persona con los datos nuevos.
- Línea 82: inserta la persona en SQLite.
- Línea 84: muestra el mensaje Persona guardada.
- Línea 87: cierra la pantalla al terminar.
- Línea 88: cierra el método.
- Línea 89: cierra la clase.

## DatabaseHelper.java

- Línea 1: declara el paquete.
- Línea 3: separa imports.
- Línea 4: importa SuppressLint para la lectura del Cursor.
- Línea 5: importa ContentValues para insertar y actualizar.
- Línea 6: importa Context.
- Línea 7: importa Cursor.
- Línea 8: importa SQLiteDatabase.
- Línea 9: importa SQLiteOpenHelper.
- Línea 11: importa ArrayList.
- Línea 12: importa List.
- Línea 14: define la clase que gestiona la base de datos.
- Línea 16: nombre del archivo de base de datos.
- Línea 17: versión de la base.
- Línea 18: nombre de la tabla.
- Línea 19: nombre de la columna id.
- Línea 20: nombre de la columna nombres.
- Línea 21: nombre de la columna apellidos.
- Línea 22: nombre de la columna ci.
- Líneas 24 a 26: construyen el SQL para crear la tabla personas.
- Línea 28: constructor que recibe el Context.
- Línea 29: llama al constructor de SQLiteOpenHelper con nombre y versión.
- Línea 32: crea la base si no existe.
- Línea 33: ejecuta el SQL de creación.
- Línea 36: maneja actualizaciones de versión.
- Línea 37: elimina la tabla si ya existe.
- Línea 38: vuelve a crear la estructura.
- Línea 43: abre el método addPersona.
- Línea 44: obtiene la base en modo escritura.
- Línea 45: crea ContentValues.
- Línea 46: guarda el nombre.
- Línea 47: guarda los apellidos.
- Línea 48: guarda el CI.
- Línea 50: inserta el registro en la tabla.
- Línea 51: devuelve el id insertado.
- Línea 55: abre el método getAllPersonas.
- Línea 56: crea una lista vacía.
- Línea 57: arma la consulta SELECT ordenada de más nuevo a más viejo.
- Línea 59: abre la base en modo lectura.
- Línea 60: ejecuta la consulta y obtiene un Cursor.
- Línea 62: verifica si existe al menos un registro.
- Línea 63: entra al ciclo de lectura.
- Líneas 65 a 70: construyen un objeto Persona con los valores de cada columna.
- Línea 71: agrega la persona a la lista.
- Línea 72: avanza a la siguiente fila.
- Línea 73: repite hasta terminar.
- Línea 76: cierra el Cursor.
- Línea 77: cierra la base.
- Línea 78: devuelve la lista completa.
- Línea 82: abre updatePersona.
- Línea 83: abre la base en modo escritura.
- Línea 84: crea ContentValues con los nuevos datos.
- Línea 85: guarda el nombre actualizado.
- Línea 86: guarda los apellidos actualizados.
- Línea 87: guarda el CI actualizado.
- Línea 89: actualiza la fila cuyo id coincide con la persona.
- Línea 90: devuelve cuántas filas fueron afectadas.
- Línea 94: abre deletePersona.
- Línea 95: obtiene la base en modo escritura.
- Línea 96: elimina la fila con el id recibido.
- Línea 99: cierra la base.
- Línea 100: cierra el método.
- Línea 101: cierra la clase.

## Persona.java

- Línea 1: declara el paquete.
- Línea 3: importa Serializable.
- Línea 5: define la clase Persona.
- Línea 6: declara el id.
- Línea 7: declara nombres.
- Línea 8: declara apellidos.
- Línea 9: declara ci.
- Líneas 11 a 16: constructor completo para registros que ya tienen id.
- Líneas 18 a 22: constructor para nuevos registros sin id.
- Líneas 24 a 27: getter y setter del id.
- Líneas 29 a 32: getter y setter de nombres.
- Líneas 34 a 37: getter y setter de apellidos.
- Líneas 39 a 42: getter y setter de ci.
- Línea 44: cierra la clase.

## PersonaAdapter.java

- Línea 1: declara el paquete.
- Línea 3: separa imports.
- Líneas 4 a 8: importan LayoutInflater, View, ViewGroup, Button, TextView y NonNull.
- Línea 9: importa RecyclerView.
- Línea 11: importa List.
- Línea 13: define el adaptador de la lista.
- Línea 15: guarda la lista de personas.
- Línea 16: guarda el listener de clics.
- Líneas 18 a 22: definen la interfaz para editar y eliminar desde cada fila.
- Líneas 24 a 28: constructor que recibe la lista y el listener.
- Línea 31: crea la vista de cada fila.
- Línea 32: infla item_persona.xml.
- Línea 34: devuelve un ViewHolder con la vista inflada.
- Línea 39: recibe un ViewHolder y una posición.
- Línea 41: obtiene la persona de esa posición.
- Línea 43: coloca los nombres en la fila.
- Línea 44: coloca los apellidos.
- Línea 45: coloca el CI con el prefijo CI.
- Línea 47: el botón Editar llama al listener.
- Línea 50: el botón Eliminar llama al listener.
- Línea 54: devuelve el tamaño total de la lista.
- Líneas 57 a 60: reemplazan la lista y notifican al RecyclerView.
- Línea 62: define la clase interna ViewHolder.
- Línea 64: declara los TextView y botones de la fila.
- Líneas 66 a 74: enlazan cada vista del item con su id.
- Línea 76: cierra la clase interna.
- Línea 77: cierra la clase principal.

## activity_main.xml

- Línea 1: abre el ConstraintLayout principal.
- Líneas 2 a 7: definen el contenedor con padding de 32dp.
- Líneas 9 a 19: crean el título Lista de Personas.
- Líneas 21 a 31: crean el botón Añadir.
- Líneas 33 a 43: definen el RecyclerView que mostrará los registros.
- Línea 44: cierra el layout.

## activity_add_edit_persona.xml

- Líneas 1 a 7: crean el contenedor principal.
- Líneas 9 a 19: muestran el título Añadir Persona.
- Líneas 21 a 28: crean el campo etNombres.
- Líneas 30 a 37: crean el campo etApellidos.
- Líneas 39 a 46: crean el campo etCi.
- Líneas 48 a 56: crean el botón btnSave.
- Línea 57: cierra el layout.

## item_persona.xml

- Líneas 1 a 7: crean una CardView para cada registro.
- Líneas 9 a 13: crean el contenedor interno con padding.
- Líneas 15 a 28: muestran los nombres de la persona.
- Líneas 30 a 42: muestran los apellidos.
- Líneas 44 a 56: muestran el CI.
- Líneas 58 a 69: crean el botón Editar.
- Líneas 71 a 83: crean el botón Eliminar.
- Línea 84: cierra el item.

## Nota importante

El manifiesto de este proyecto declara AddPersonActivity, pero en el código revisado no aparece esa clase. Si el proyecto da error al compilar, ese es el primer punto a revisar.

## Para el examen

La idea central es el flujo completo: SQLite guarda los datos, RecyclerView los muestra, y la interfaz permite crear, editar y borrar personas.