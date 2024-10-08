# TAD LINEALES

## Introducción
Los TAD constituyen una forma de generalizar y encapsular los aspectos más importantes de la información que manejamos dentro del programa, olvidando hasta el momento de la implementación como se va a representar esa información dentro del ordenador. 

El TAD se puede ver como un conjunto de valores y operaciones que se definen sobre ellos independientes de su implementación 

Los TAD se dividen en:
  - **TAD Lineales:** Aquellas estructuras abstractas de datos en que cada elemento, salvo el primero y el último, tiene como mucho dos elementos adyacentes (posterior y/o anterior) y desde un elemento cualquiera sólo se puede acceder a uno de estos dos elementos como máximo.

  - **TAD no Lineales**: Aquellas estructuras cuyos elementos pueden tener más de dos elementos adyacentes, a los que pueden acceder directamente (no tiene sentido el concepto de anterior/siguiente), como los **árboles o grafos**

En este tema se estudia la primera gran familia de TADs, los TAD lineales, todos ellos derivados del concepto de secuencia: **listas, pilas y colas.**

Los diferentes TADs basados en este concepto se diferenciarán por las operaciones de acceso a los elementos y manipulación de la estructura
Las operaciones básicas para dichas estructuras son: 
  1. crear la secuencia vacía
  2. añadir un elemento a la secuencia
  3. borrar un elemento de la secuencia
  4. consultar un elemento de la secuencia
  5. comprobar si la secuencia está vacía 

La diferencia entre las tres estructuras que se estudiarán vendrá dada por la posición del elemento a añadir, borrar y consultar:
  - **Listas:** las tres operaciones se realizan sobre una posición cualquiera de la secuencia.
  - **Pilas:** las tres operaciones actúan sobre un extremo de la secuencia.
  - **Colas:** se añade por un extremo y se borra y consulta por el otro. 


## TAD Lista

**Una lista es un conjunto ordenado de elementos homogéneos en la que no hay restricciones de acceso, la introducción y borrado de elementos puede realizarse en cualquier posición de la misma.** 
  -  Son TAD en los que los elementos están organizados siguiendo un orden secuencial
  -  Cada elemento tiene un anterior y un siguiente en la lista
  -  Las listas genéricas son estructuras muy flexibles, no existe una restricción en la localización de los elementos insertados o extraídos
  -  Las listas pueden crecer o acortarse.
  -  A los elementos de una lista se les suele llamar **nodos** (o celdas).

En la implementación del TAD lista de manera estática, la eliminación o inserción de un elemento supondrá la reorganización del resto de elementos del vector. 

La implementación dinámica es mucho más eficiente, y mediante ella podremos construir: 
  - Listas Simplemente Enlazadas (cada elemento tiene acceso al siguiente)
  - Listas Doblemente Enlazadas (cada elemento tiene acceso al anterior y al siguiente)
  - Listas Circulares (el último elemento tiene acceso al inicio de la lista)

Lista.h:
```cpp
  // FICHERO TADLista.h
# define MAX 30
# include <iostream>
using namespace std;
class lista {
 int elementos[MAX];//elementos de la lista
 int n;//nº de elementos que tiene la lista
public:
lista();
lista(int e);
 bool esvacia();
 int longitud();
 void anadirIzq(int e);
 void anadirDch(int e);
 void eliminarIzq();
 void eliminarDch();
 int observarIzq();
 int observarDch();
 void concatenar(lista l);
 bool pertenece(int e);
 void insertar(int i, int e);
 void eliminar(int i);
 void modificar(int i, int e);
 int observar(int i);
 int posicion(int e);
};
```
lista.cpp
```cpp
//FICHERO TADLista.cpp
# include “TADLista.h”
lista::lista() {n=0;}
lista::lista(int e)
{
 n=1;
 elementos[0]=e;
}
void lista::insertar(int i, int e)
{
int pos,postabla;
postabla=i-1;
if (n < MAX){
 for (pos=n-1; pos>=postabla; pos--)
 elementos[pos+1]=elementos[pos];//Desplazamiento
 elementos[postabla]=e;
 n++;
}
}
void lista::eliminar(int i){
 int postabla;
 postabla=i-1;
 while (postabla<n-1)
 {
 elementos[postabla]=elementos[postabla+1];
//Desplazamiento
 postabla++;
 }
 n--;
}
void lista::modificar(int i, int e){
elementos[i-1]=e;}
int lista::observar(int i){
return(elementos[i-1]);}
bool lista::esvacia (){return (n == 0);}
int lista::posicion(int e){
int i=0;
while ( (elementos[i] != e) && (i < n) )
 i++;
if (elementos[i] == e) return(i+1);
else return (-1);
}
int lista::longitud (){return n;}
void lista::anadirIzq(int e){insertar(1,e);}

void lista::anadirDch(int e){insertar(n+1,e);} 
void lista::eliminarIzq()
 {
 for (int i=0;i<n-1;i++)
 elementos[i]=elementos[i+1];
 n--;
 }
void lista::eliminarDch(){ n--; }

int lista::observarIzq() {return(observar(1));}
int lista::observarDch(){ return(observar(n)); }
void lista::concatenar(lista l)
 {
 int lon=l.longitud();
 for (int i=1;i<=lon;i++)
 insertar(n+1,l.observar(i));
 }
bool lista::pertenece(int e)
 {
 return (posicion(e)==-1?false:true);
 }
```
### Aplicaciones 
  Existen multitud de ejemplos donde se hace uso de este tipo abstracto de dato. Si pensamos en una lista de la compra o en una guía telefónica estamos manejando listas. 

  Asimismo existen numerosas estructuras relacionadas directamente con las listas y distintas variantes que ofrecen diferentes propiedades de acceso. Es el caso de los TAD pila y cola que se verán a continuación y para los que veremos diversas aplicaciones con detalle. 

## TAD Pila (STACK)
**Una pila es un tipo especial de lista en la que la inserción y la eliminación de sus elementos se realizan sólo por un extremo que se denomina tope (cima, cabeza o cabecera)**

Es un TAD que se caracteriza por el modo de acceso a sus elementos:

Ej: un montón de platos. 

La pila es una estructura con numerosas analogías en la vida real, su comportamiento es similar al de un conjunto de elementos apilados unos sobre otros, p.e.: una pila de platos, una pila de monedas, una pila de libros, etc.,

Estructuras donde los elementos sólo pueden eliminarse en orden inverso al que se insertan en la pila.

• En estos TAD, el último elemento que se pone en la pila es el primero que se puede sacar, por eso a estas estructuras se les conoce por el nombre “listas LIFO” (Last In, First Out, o último en entrar, primero en salir).

• No existe un método de acceso directo a cualquier elemento de la pila, para acceder a uno de ellos es necesario desapilar los anteriores (los que estén "por encima" de éste).

• Llevan asociados una variable llamada tope que indica la posición del último elemento apilado.

• Los elementos se insertan de uno en uno (apilar)

• Se sacan en el orden inverso al cual se han insertado (desapilar)

• El único elemento que se puede observar dentro de la pila es el último insertado (tope o cima) 

Pila.h
```cpp
  // FICHERO TADPila.h
# define MAX 30
# include <iostream>
using namespace std;
class pila {
 int elementos[MAX]; //elementos de la pila
 int tope ;//tope de la pila
public:
pila(); // constructor de la clase
void apilar(int e);
void desapilar();
int cima();
bool esvacia();
int longitud();
};
```

Pila.cpp
```cpp
//FICHERO TADPila.cpp
# include “TADPila.h”
pila::pila(){tope=-1;}
void pila::apilar(int e){
if (tope+1<MAX){
tope++;
elementos[tope]=e;
}
}
int pila::longitud(){ return tope+1; }
void pila::desapilar(){tope--;}
/* El elemento no se "borra" del vector */
int pila::cima(){return(elementos[tope]);}
bool pila::esvacia (){return (tope == -1);
} 
```
### Aplicaciones de la Pila

Las pilas son utilizadas ampliamente para solucionar una gran variedad de problemas. Se utilizan en compiladores, sistemas operativos y en programas de aplicación. 

Algunas de estas aplicaciones son:
  - El gestor de programas del S.O. utiliza una pila para guardar momentáneamente los parámetros y dirección de retorno de la función que se está procesando actualmente.
  - Los editores de texto proporcionan normalmente un botón deshacer que cancela las operaciones de edición recientes y restablece el  estado anterior del documento. La secuencia de operaciones recientes se mantiene en una pila.
  - Los navegadores permiten habitualmente volver hacia atrás en la secuencia de páginas visitadas. Las direcciones de los sitios visitados se almacenan en una pila.
-  Estructuras auxiliares en numerosos algoritmos y esquemas de programación:
    - recorridos de árboles y grafos
    - evaluación de expresiones
    -  conversión entre notaciones (postfija, prefija, infija)

Veamos con más detalle una de sus aplicaciones más comunes: 

**Llamadas a subprogramas.**
Cuando dentro de un programa se realizan llamadas a subprogramas, el programa principal debe de recordar el lugar desde donde se hizo la llamada, de modo que pueda retornar allí cuando el subprograma se haya terminado de ejecutar.

Ejemplo

Supongamos que tenemos tres subprogramas llamados A1, A2 y A3, y un programa principal P y que se realizan las llamadas que se muestran gráficamente. De esta manera A1 que es el primero que se ejecuta será el último en terminar y devolver el control al programa principal que sólo así podrá terminar. Esta operación se consigue disponiendo las direcciones de retorno en una pila. 
![image](https://github.com/user-attachments/assets/340e5967-4052-479b-8828-38ddb0ae7f95)

Cuando un subprograma termina debe retornar a la dirección siguiente a la instrucción que le llamó. Cada vez que se invoca a un subprograma, la dirección siguiente (r, s o t) se introduce en la pila. El vaciado de la pila se realizará por los sucesivos retornos, decrementándose el tope de la pila que queda siempre en la siguiente dirección de retorno.


## TAD Cola (QUEUE)
**Son TADs formados por una secuencia de elementos, caracterizados porque sus elementos se insertan por un extremo y se extraen por el extremo opuesto (el primer elemento en insertarse es el primero en extraerse).**
![image](https://github.com/user-attachments/assets/df7dc111-aad0-45ac-96e3-5f0276d1d88c)

Las colas son estructuras lineales de datos, similar a las pilas, diferenciándose de ellas en el modo de insertar/eliminar elementos.

Una cola es otro tipo especial de lista en la cual los elementos se insertan por un extremo – por el final de la lista - y se eliminan por el otro extremo –por el principio de la lista -.

En las colas el elemento que entró el primero, sale también el primero, por ello se conocen como “listas FIFO” (First Input, First Output, o primero en entrar, primero en salir).

 La diferencia con las pilas reside en el modo de entrada/salida de datos; en las colas las inserciones se realizan al final de la lista, no al principio.

 Se denomina así porque el comportamiento de esta estructura de datos es similar al de una cola de personas en un cine, de coches en un atasco, etc., y por ello se usan para almacenar datos que necesitan ser procesados según el orden de llegada.

El único elemento observable en todo momento es el primero que fue insertado. 

Fichero TADCola.h
```cpp
# define MAX 30
# include <iostream>
using namespace std;
class cola {
 int elementos[MAX]; //elementos de la cola
 int inicio, fin;//principio y fin de la cola
public: 
cola(); // constructor de la clase
void encolar(int e);
void desencolar();
int primero();
bool esvacia();
int longitud() ;
}; 
```

Fichero TADCola.cpp
```cpp
//FICHERO TADCola.cpp
# include ”TADCola.h”
cola::cola(){
inicio=0;
fin=-1;
}
void cola::encolar(int e){
if (fin+1<MAX){
fin++;
elementos[fin]=e;
}
}
int cola:longitud() { return fin+1;}
void cola::desencolar(){
for(int i=inicio;i<fin;i++)
elementos[i]=elementos[i+1]; //Desplazamiento
fin--;
} 
int cola::primero(){
return(elementos[inicio]);
}
bool cola::esvacia (){
return (fin == -1);
}
```






















