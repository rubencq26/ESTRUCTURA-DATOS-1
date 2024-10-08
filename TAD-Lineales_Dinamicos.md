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

TADLista.cpp
```cpp
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
void lista::eliminar(int i)
{
 while (i<n)
 {
 elementos[i-1]=elementos[i]; // Desplazamiento
 i++;
 }
 n--;
 if (Tama-n>=INCREMENTO && Tama>INCREMENTO)
 {
 float *NuevaZona=new float[Tama-INCREMENTO];
 if (NuevaZona!=NULL)
 {
 Tama-=INCREMENTO;
 for (int i=0;i<Tama; i++)
 NuevaZona[i]=elementos[i];
 delete [] elementos;
 elementos=NuevaZona;
 };
 };
}
int lista::posicion(float e)
{
 int i=0;
 while (elementos[i]!=e && i < n)
 i++;
 return (i == n ? -1 : i+1);
}
int lista::longitud()
{
 return n;
}
lista::lista(float e)
{
 elementos=new float[INCREMENTO];
 if (elementos!=NULL) {
 Tama=INCREMENTO;
 n=1;
 elementos[0]=e;
 }
 else {
 Tama=n=-1;
 }
}
void lista::anadirIzq(float e)
{
 insertar(1, e);
}
void lista::anadirDch(float e)
{
 insertar(n+1, e);
}
void lista::eliminarIzq()
{
 eliminar(1);
}
void lista::eliminarDch()
{
 eliminar(n);
}
float lista::observarIzq()
{
 return(observar(1));
}
float lista::observarDch()
{
 return(observar(n));
}
void lista::concatenar(lista l)
{
 int lon = l.longitud();
 for (int i=1; i<=lon; i++)
 insertar(n+1, l.observar(i));
}
bool lista::pertenece(float e)
{
 return (posicion(e) != -1);
}
```
### Implementacion con nodos enlazados
En vez de tener toda la información (nodos de la lista) agrupada en una misma zona de memoria (como las tablas estáticas y dinámicas), ahora se pretende dispersar cada elemento o nodo de la lista por cualquier zona de la memoria.

![image](https://github.com/user-attachments/assets/eb2abfaa-e63c-48e8-8727-8cc654433c85)

**Inconvenientes**: **No se puede acceder** de manera directa a cualquier nodo de la lista. 
                   **Se necesita más memoria** para almacenar los distintos punteros. 

**Ventajas: Exige** menos movimiento de información cada vez que se modifica la lista
          **Evita** el problema de falta de espacio que se da con otras implementaciones. 

Existen varios tipos de listas dinámicas enlazadas de datos que son: 
- **Lista simplemente enlazada:**

 ![image](https://github.com/user-attachments/assets/9fdedc60-ba97-43db-97ab-a6baa76a0456)

- **Lista doblemente enlazada:**

  ![image](https://github.com/user-attachments/assets/387a2c6a-1ba8-455f-b816-bef803eb4477)

- **Lista Circular: **

![image](https://github.com/user-attachments/assets/e3481292-4bfd-439c-b256-015ea97d92f3)

- **Lista con nodo cabecera: **

![image](https://github.com/user-attachments/assets/5e238dc9-264b-4483-85c6-7d2219863c1c)

#### Operaciones básicas sobre listas enlazadas
```cpp
//Lista simplemente enlazada
struct TNodo_Lista
{
 Tipo_elemento Datos; //Datos a almacenar en cada nodo
 TNodo_Lista *Siguiente; //Puntero al siguiente nodo
};
TNodo_Lista *elementos; //Puntero al primer elemento


//Lista doblemente enlazada
struct TNodo_Lista
{
 Tipo_elemento Datos; //Datos a almacenar en cada nodo
 TNodo_Lista *Anterior; //Puntero al nodo anterior
 TNodo_Lista *Siguiente; //Puntero al siguiente nodo
};
TNodo_Lista *elementos; //Puntero al primer elemento

//Creacion Lista
//La lista no contiene ningún nodo.
TNodo_Lista *elementos=NULL; 

//Lista con nodo cabecera
TNodo_Lista *elementos;
elementos=new TNodo_Lista;
if (elementos!=NULL)
{
 elementos->Siguiente=NULL;
 elementos->Anterior=NULL;
}
```
    


