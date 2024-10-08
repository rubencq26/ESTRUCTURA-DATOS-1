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
En el ejemplo, se está declarando una tabla de cuatro punteros a reales (**no cuatro reales**) y una tabla de 10 punteros a objetos Polinomio (**no 10 objetos Polinomio**).

Se puede dar el caso de que varios punteros apunten a la misma variable. Para ello el valor de la dirección de memoria será el mismo para ambos punteros. Tampoco es infrecuente encontrar tablas de punteros de más de un nivel como por ejemplo:
``` cpp
cliente **TPC1[10];
```

![image](https://github.com/user-attachments/assets/41107689-b774-42e6-b80f-ecbb785c5379)






