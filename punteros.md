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
```



