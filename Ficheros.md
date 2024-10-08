# Archivos lógicos y físicos

## Introduccion a ficheros
- El significado más genérico de archivo o fichero es de flujo o sucesión de elementos que entran o salen del ordenador.
- Normalmente hablaremos de ficheros cuando el caudal de datos viaje o proceda desde el disco o soporte de almacenamiento estable (fichero en disco o archivo).

Un fichero podría definirse como un elemento de almacenamiento de datos sobre un medio permanente con las siguientes características:
  - Es una estructura de datos dinámica.
  - Permite el almacenamiento permanente de la información.
  - No tiene un tamaño fijo preestablecido ni un máximo.
  - Tener un acceso lento a la información, si lo comparamos con los accesos a memoria principal

**Archivo lógico** es una abstracción que nos ofrece el lenguaje de programación, de forma que nos permita manejar ficheros independientemente de su representación, almacenamiento, etc.

**Archivo físico** es una colección de datos real que ocupa un espacio exacto y concreto en el disco físico y que tiene asociado un nombre, un tamaño y otras informaciones adicionales.

**Asignación** es el momento en el que se asocia un fichero lógico con su
correspondiente fichero físico.

## Tipos de archivos
###En cuanto a su modo de acceso.
El modo de acceso a los archivos depende principalmente del soporte empleado para los mismos y del modo físico en el que se ha organizado su información.
  - **Acceso secuencial**: se accederá a cada elemento del archivo uno tras otro en el mismo orden en el que se situaron.
  - **Acceso directo**: permite acceder a un elemento determinado sin tener que acceder previamente a otros precedentes.

###En cuanto a su contenido
  - **Ficheros de texto**
  - **Ficheros binarios**

## Operaciones con archivos
### Declaración y apertura de ficheros.
Las funciones específicas en C++ para el manejo de archivos parten de
vincular, en su apertura, dicho archivo a un flujo (stream). Hay tres tipos de
flujos:
```cpp
//Entrada
#include<ifstream> //para leer desde un fichero
//Salida
#include<ofstream> //para escribir desde un fichero
//Entrada/Salida
#include<fstream>
```
La asociación de un archivo lógico con un archivo físico se realiza con el
método **open**:
```cpp
open( char* nombreFichero, ios_base::openmode modo )
fichero.open("nombreFichero", ios::in | ios::out | ios::binary)
```
Donde nombreFichero es la ruta completa de localización del archivo,
pudiendo incluir un especificador de camino. Y modo determina cómo se
abre el archivo, debiendo ser uno (o varios, uniéndolos con |) de los valores:

| **ios::in**     | Apertura para lectura                        |
| **ios::out**    | Apertura para escritura                      |
| **ios::binary** | Apertura en modo binario (no en modo texto)  |
| **ios::app**    | Para añadir únicamente por el final del fichero |
| **ios::trunc**  | Borra previamente el contenido del fichero   |

