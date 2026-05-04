# formulario

## Qué hace el proyecto

Simula una ficha de inscripción. El usuario completa varios campos, guarda todo en un archivo de texto interno y luego puede volver a cargar los datos en los EditText y en un TextView resumen.

## MainActivity.java

- Línea 1: declara el paquete com.movil.formulario.
- Línea 3: separa los imports del código principal.
- Líneas 4 a 14: importan clases para vistas, Edge-to-Edge, insets y archivos.
- Línea 15: importa Toast para mostrar mensajes al usuario.
- Línea 17: inicia la clase MainActivity.
- Líneas 19 a 23: declaran todos los campos del formulario, los botones y el nombre del archivo datos_formulario.txt.
- Línea 24: declara el botón guardar.
- Línea 25: declara el botón leer.
- Línea 26: define el nombre del archivo interno.
- Línea 28: abre onCreate.
- Línea 29: llama al constructor de la clase padre.
- Línea 30: activa Edge-to-Edge.
- Línea 31: carga el layout activity_main.
- Línea 34: obtiene la vista principal con id main.
- Líneas 35 a 41: si la vista existe, registra un listener para ajustar padding con los insets del sistema.
- Línea 43: termina la validación de la vista principal.
- Líneas 45 a 54: enlazan los campos etNombre, etLugarFecha, etDNI, etCorreo, etDireccion, etCP, etCiudad, etMovil, etFecha y etFirma.
- Línea 56: enlaza el botón Guardar.
- Línea 57: enlaza el botón Leer.
- Líneas 60 a 65: el botón Guardar llama a guardarDatos.
- Líneas 68 a 73: el botón Leer llama a leerDatos.
- Línea 76: abre guardarDatos.
- Líneas 78 a 87: une todos los valores del formulario con saltos de línea para guardarlos en una sola cadena.
- Línea 89: abre un FileOutputStream para el archivo interno.
- Línea 90: escribe la cadena completa como bytes.
- Línea 91: muestra un mensaje de éxito.
- Línea 92: captura cualquier excepción.
- Línea 93: imprime el error en consola para depuración.
- Línea 94: muestra un mensaje de error al usuario.
- Línea 95: cierra el bloque catch.
- Línea 96: cierra el método guardarDatos.
- Línea 98: abre leerDatos.
- Línea 99: abre FileInputStream para el archivo interno.
- Línea 100: convierte bytes a texto con InputStreamReader.
- Línea 101: usa BufferedReader para leer línea por línea.
- Líneas 103 a 112: leen cada valor del archivo en el mismo orden en que se guardó.
- Líneas 115 a 124: colocan los datos leídos nuevamente en cada EditText.
- Línea 127: busca el TextView de resultado.
- Líneas 128 a 139: construyen un resumen legible con etiquetas para cada campo.
- Línea 141: muestra un mensaje indicando que la carga fue correcta.
- Línea 143: captura errores si no existe el archivo o si falla la lectura.
- Línea 144: imprime el error en consola.
- Línea 145: avisa que no se encontraron datos guardados.
- Línea 146: cierra el catch.
- Línea 147: cierra el método leerDatos.
- Línea 148: cierra la clase.

## activity_main.xml

- Líneas 1 a 8: crean un ScrollView para permitir desplazamiento vertical.
- Líneas 10 a 14: abren un LinearLayout vertical con padding.
- Líneas 16 a 27: muestran el título y subtítulo de la ficha.
- Líneas 29 a 32: agregan una línea separadora.
- Líneas 34 a 37: abren la sección Datos personales.
- Líneas 39 a 45: muestran la etiqueta Nombre y apellidos y el EditText etNombre.
- Líneas 47 a 55: crean una fila horizontal con Lugar y fecha de nacimiento y Correo.
- Líneas 57 a 76: definen el campo etLugarFecha.
- Líneas 78 a 95: definen el campo etCorreo.
- Líneas 97 a 105: muestran la etiqueta DNI y el campo etDNI.
- Líneas 107 a 116: muestran la etiqueta Dirección y el campo etDireccion.
- Líneas 118 a 127: crean una fila horizontal con Ciudad y CP.
- Líneas 129 a 147: definen el campo etCiudad.
- Líneas 149 a 166: definen el campo etCP.
- Líneas 168 a 177: crean una fila horizontal para Móvil y Fecha.
- Líneas 179 a 197: definen el campo etMovil.
- Líneas 199 a 217: definen el campo etFecha.
- Líneas 219 a 223: agregan un separador antes de firma.
- Líneas 225 a 236: muestran la etiqueta Firma y el campo etFirma.
- Líneas 238 a 256: crean la fila con los botones btnGuardar y btnLeer.
- Líneas 258 a 267: separan visualmente la parte de resultados.
- Líneas 269 a 277: muestran el título Datos guardados.
- Líneas 279 a 295: definen el TextView Resultado donde se verá el resumen cargado.

## Para el examen

Este proyecto enseña cómo guardar un formulario completo en un archivo de texto y luego reconstruir la pantalla leyendo cada línea en el mismo orden.