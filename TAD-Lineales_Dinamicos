# TAD Lineales Dinámicos

## Implementación dinámica del TAD Lista. 
El uso de tablas presenta ventajas ya vistas, pero también presentan desventajas:
  - Reserva constante de memoria independientemente de su utilización y aprovechamiento.
  - Limitación del número de elementos que puede contener.
  - Imposibilidad de aumentar su capacidad. 

La solución de estos problemas puede ser: 

1. Evitar el problema que tienen las tablas de no poder crecer o decrecer utilizando para ellos **tablas dinámicas.**
-  **Ventaja:** el acceso a las tablas dinámicas es el mismo que a las tablas estáticas.
-  **Inconveniente:** cada vez que se modifica el tamaño de las tablas dinámicas, el S.O debe encontrar una zona en la memoria que se ajuste al nuevo tamaño pudiéndose dar el caso de que no exista.

2. Utilizando una estructura de datos encadenada mediante punteros que nos permite tener distribuidos en la memoria los elementos de la lista.
- **Ventaja:** los nodos de la lista son almacenados en distintas partes de la memoria del ordenador. Para evitar su perdida, se utiliza en cada nodo un puntero que apunte al siguiente nodo.

- **Inconveniente:** se necesita más memoria para almacenar el puntero al siguiente nodo de la lista. 

### Implementacion con tabla dinámica
Tiene la posibilidad de aumentar y disminuir el tamaño de las tablas en tiempo de ejecución. Pasos:
  - Encontrar un espacio de memoria libre por parte del S.O. 
  - Traspasar los datos de la zona original de memoria a la nueva zona que puede ser mayor o menor que la zona original.
  - Liberar el espacio de memoria antiguo para el uso por otro programa.


TADLista.h

```cpp
  // FICHERO TADLista.h
#include <iostream>
#define INCREMENTO 4
using namespace std;
class lista {
 float *elementos; // elementos de la lista
 int n; // nº de elementos que tiene la lista
 int Tama; // tamaño de la tabla en cada momento
 public:
 lista(); // constructor de la clase
 ~lista(); // destructor de la clase
 lista(float e);
 bool esvacia();
 int longitud();
 void anadirIzq(float e);
 void anadirDch(float e);
 void eliminarIzq();
 void eliminarDch();
 float observarIzq();
 float observarDch();
 void concatenar(lista l);
 bool pertenece(float e);
 void insertar(int i, float e);
 void eliminar(int i);
 void modificar(int i, float e);
 float observar(int i);
 int posicion(float e);
};
```

//FICHERO TADLista.cpp
# include “TADLista.h”
lista::lista()
{
 elementos=new float[INCREMENTO];
 if (elementos!=NULL)
 {
 Tama=INCREMENTO;
 n=0;
 }
 else
 {
 Tama=n=-1;
 }
} 
lista::~lista()
{
 if (elementos!=NULL)
 delete [] elementos;
 elementos=NULL;
 Tama=n=0;
}
void lista::insertar(int i, float e)
{
 int pos;
 if (n==Tama)
 {
 float *NuevaZona=new float[Tama+INCREMENTO];
 if (NuevaZona!=NULL)
 {
 for (int i=0;i<n; i++)
 NuevaZona[i]=elementos[i];
 Tama+=INCREMENTO;
 delete [] elementos;
 elementos=NuevaZona;
 }
 };

 if (n<Tama)
 {
 for (pos=n-1; pos>=i-1; pos--)
 elementos[pos+1]=elementos[pos]; // Desplazamiento
 elementos[i-1]=e;
 n++;
 }
}
void lista::modificar(int i, float e) {
 elementos[i-1]=e;
}
float lista::observar(int i) {
 return(elementos[i-1]);
}
bool lista::esvacia() {
 return (n == 0);
} 
