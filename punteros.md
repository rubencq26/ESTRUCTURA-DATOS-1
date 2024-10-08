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
