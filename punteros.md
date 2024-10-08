## Punteros

[volver al inicio](https://github.com/rubencq26/ESTRUCTURA-DATOS-1)

Un puntero, hablando de manera aproximada, es una variable de tipo entero que contiene un valor numérico que es en realidad la dirección de memoria donde está situada otra variable del programa.

### Declaracion de una variable puntero
Una variable puntero se declara exactamente igual que una variable normal añadiendo antes del identificador uno o más asteriscos **‘*’**.
Cuando se declara un puntero sólo se está reservando una posición de memoria donde se va a almacenar la dirección de otra variable, pero no se reserva memoria para la variable apuntada.
``` cpp
  float *valor;
  Polinomio *P;
```
La zona de memoria donde apunta un puntero puede ser además otro puntero que apunte a otra zona de memoria. Esto se conoce como encadenamiento de punteros
``` cpp
  cliente **PPC1; //Dos asteriscos
```
### Declaración de tablas de punteros.
Se declara una tabla de punteros añadiendo a la declaración de un puntero el tamaño de cada dimensión. Hay que tener en cuenta que cuando se declara una tabla de punteros sólo se reserva memoria para la tabla y no para los datos a los que apuntará cada puntero.
``` cpp
float *TPValor[4];
Polinomio *TP1[10];
```
![image](https://github.com/user-attachments/assets/65dc7ea6-91ef-4a94-9fad-2cb97848eed9)

En el ejemplo, se está declarando una tabla de cuatro punteros a reales (**no cuatro reales**) y una tabla de 10 punteros a objetos Polinomio (**no 10 objetos Polinomio**).

Se puede dar el caso de que varios punteros apunten a la misma variable. Para ello el valor de la dirección de memoria será el mismo para ambos punteros. Tampoco es infrecuente encontrar tablas de punteros de más de un nivel como por ejemplo:
``` cpp
cliente **TPC1[10];
```
### Operaciones con punteros
[volver al inicio](https://github.com/rubencq26/ESTRUCTURA-DATOS-1)
#### Inicializacion de punteros
Las variables puntero han de ser inicializadas con direcciones de memoria o con un valor especial que indica una dirección nula, la constante NULL.
``` cpp
float *PValor = NULL;
Polinomio ** PPolinomio = NULL;
```
#### Asignacion de punteros
Existe el **operador de referencia ‘&’** que nos devuelve la dirección de una variable si éste se coloca justo delante del identificador de la variable. 
``` cpp
float *PValor = NULL, Valor = 50.6;
PValor = &Valor;
//&Valor devuelve la direccion de Valor, 2345 en este caso
```
![image](https://github.com/user-attachments/assets/9444efd7-6ace-440f-9e83-cb1ee94c2c97)
#### Acceso a punteros
En todo momento se puede acceder a dos tipos de información: al **propio valor** de la variable puntero (mediante el identificador de la misma) y a la **información a la que apunta** mediante el operador denominado **desreferencia ‘*’**. 
``` cpp
float *PValor = NULL, Valor = 50.6;
PValor = &Valor;
float *Copia_de_PValor, Suma;

Copia_de_PValor = PValor; /*PValor devuelve su contenido, es decir 2345,
que es la direccion de la variable valor*/
Suma = *PValor + 10;  //Suma contiene 60.6
```
**Nota:** Dependiendo del lugar donde aparece, el símbolo ‘*’ tiene un significado distinto.
```cpp
float Producto = *PValor * *PValor; //Contiene 50.6*50.6=2560.36
```
Para acceder a los campos (métodos) de una estructura (clase) apuntados por una variable puntero se puede utilizar el operador punto **‘.’** .
```cpp
Cliente *PCli=NULL, Cli;
PCli = &Cli;
(*PCli).Edad = 20;
cout << (*PCli).Nombre;
```
El operador ‘**->**’ simplifica la escritura de programas. Como podemos ver en el siguiente ejemplo, el operador ‘**->**’ nos indica que el nombre del cliente está apuntado y accedido a través el puntero PCli.
```cpp
Cliente *PCli=NULL, Cli;
PCli = &Cli;
PCli->Edad = 20;
cout << PCli->Nombre;
```
#### Comparacion de punteros
Una variable puntero puede ser comparada con otra variable puntero o con la constante NULL; aunque todos los operadores relacionales están permitidos, sólo los operadores != y == tienen una verdadera utilidad práctica. 
![image](https://github.com/user-attachments/assets/48b81b4c-7cfb-4442-9ebd-17368cb8cc7f)
```cpp
float *PValor1 = NULL, *PValor2 = NULL, Valor1 = 50.6, Valor2 = 30.2;
PValor1 = &Valor1;
PValor2 = &Valor2;
if (PValor1<PValor2) //Comparación 1ª
 cout << ”Valor1 está situada en la memoria antes de Valor2”;
else
 cout << ”Valor2 está situada en la memoria antes o en la misma
 posición de Valor1”;
if (*PValor1 < *PValor2) //Comparación 2ª
 cout << *PValor2 << ” es mayor que ” << *PValor1;
else
 cout << *PValor2 << ” es menor o igual que ” << *PValor1;

/*La salida por pantalla del código del ejemplo anterior es el siguiente:
  Comparación 1ª:
    Valor1 está situada en la memoria antes de Valor2
  Comparación 2ª:
    30.2 es menor o igual que 50.6 */
```
### Variables dinámicas
[volver al inicio](https://github.com/rubencq26/ESTRUCTURA-DATOS-1)
Mediante el uso de punteros se nos permite disponer de nuevas variables en tiempo de ejecución. Las variables dinámicas tienen como identificador la dirección de memoria donde están situadas. El programador tiene la responsabilidad de solicitar la creación y eliminación de variables dinámicas.
#### Creación de variables dinámicas.
En el lenguaje C++ se cuenta con el operador **new** para solicitar el uso de memoria dinámica. Posee la capacidad de ejecutar los constructores definidos en la clase del objeto que se instancia. Además permite traspasar valores a los parámetros definidos en los constructores de la clase. 
```cpp
//Crea una variable dinámica de tipo float
float *v = new float;
```
![image](https://github.com/user-attachments/assets/0749b6d1-c1c7-4083-805c-226398ac486c)

```cpp
//Crea una tabla dinámica de 100 enteros
int *tabla = new int[100];
for (int i=0; i<100; i++){
 tabla[i] = i; /*No es necesario inicializar solo es para mostrar como dar
valores a la tabla*/
}
```
![image](https://github.com/user-attachments/assets/8fbeddfe-dec5-4127-9f34-4c710b13806b)
Todas las funciones y operadores que reservan memoria, devuelven o bien la dirección de memoria reservada o bien la constante **NULL** para indicar que el S.O. no ha encontrado ninguna zona de memoria con el tamaño que ha sido solicitado.
```cpp
cliente *C1 = new cliente;
/*Crea un objeto cliente en memoria dinámica
y ejecuta el constructor por defecto*/
cliente *C2 = new cliente(“Antonio”, 28343334);
/*Crea un objeto cliente en memoria dinámica
y ejecuta el constructor con dos parámetros,
nombre y dni*/
```
![image](https://github.com/user-attachments/assets/d151ecc5-fcd1-4f1e-be6f-d31d1ac960f3)

#### Eliminacion de variables dinamicas
C++ permite la liberación de memoria dinámica con el operador **delete**. Posee la capacidad de ejecutar el destructor definido en la clase del objeto que se destruye. 
```cpp
delete v;
delete [] tabla;
// para liberar un array creado dinámicamente con new
// invoca al destructor de cada elemento del array
```
#### Aritmética de punteros
Como toda variable numérica, las variables de tipo puntero permiten realizar ciertas operaciones aritméticas sobre la dirección de memoria que almacenan. Las operaciones normales son la suma y resta de posiciones de memoria. 
```cpp
  int *tabla = new int[100];
for (int i=0; i<100; i++)
 tabla[i] = i;
tabla++; //contiene 14672 el siguiente elemento
cout << *tabla; //escribe 1
tabla++; //contiene 14674 el tercer elemento de la tabla
cout << *tabla; //escribe 2
```
![image](https://github.com/user-attachments/assets/f3abc070-21e6-4367-b999-b6b34eaf7ba2)
El estado anterior de la tabla es tal que el primer elemento de la tabla es el valor 2 y no el 0 y además el número de elementos de la tabla es de **98** elementos y no de **100**. 
```cpp
cout << tabla[0]; //escribe 2
cout << tabla[-1]; //escribe 1
```
Este funcionamiento es **independiente** del tipo de datos de la variable puntero. La agregación de valores a una variable puntero **incrementa** su contenido en el **mismo número** de bytes que ocupa el tipo de la variable puntero. 
[volver al inicio](https://github.com/rubencq26/ESTRUCTURA-DATOS-1)
