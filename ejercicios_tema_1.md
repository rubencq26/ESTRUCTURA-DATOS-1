#Ejercicios de Punteros y Ficheros
## Ejercicio 1
Declarar y construir la siguiente tabla dinámica de datos e inicializarla con el valor 0: 
Destruir la estructura del ejercicio anterior, calculando previamente la suma de los elementos que contiene
![image](https://github.com/user-attachments/assets/576ff2b5-8c04-4bb1-ae4d-4444c6186d50)

Solucion: 
```cpp
#include <iostream>
#include <conio.h>

using namespace std;

int main() {
	float *Tabla;
	char respuesta;
	float suma = 0;
	int fila, col;
	
	float **Datos = new float*[100];
  
	if (Datos != NULL) {
		for (int i=0; i<100; i++) {
			Datos[i] = new float[100-i];
			Tabla = Datos[i];
			for (int j=0; j<100-i; j++)
				Tabla[j] = 0;
				//Datos[i][j] = 0;
			}
	}
	
	do {
		cout << "Deme fila (1 a 100)\n";
		cin >> fila;
		Tabla = Datos[fila-1];
		cout << "Deme columna (1 a " << 100-fila+1 << ")\n";
		cin >> col;
		cout << "Deme valor\n";
		cin >> Tabla[col-1];
		cout << "\n Desea continuar (S/N)\n";
		respuesta = toupper(getch());
   } while (respuesta != 'N');                    
  
	for (int i=0; i<100; i++) {
		Tabla = Datos[i];
		for (int j=0; j<100-i; j++) 
			suma += Tabla[j];
			//suma += Datos[i][j]; 
		delete [] Tabla;
		//delete [] Datos[i];
	}   
  
	cout << "La suma vale " << suma << endl << endl;

	delete [] Datos;

	system("pause");
	return 0;
}
```
## Ejercicio 3
Diseñe un programa que permita crear dos ficheros con información referente a los
artículos de un almacén.
- Uno llamado "precios.dat", cuyos elementos son del tipo siguiente: 
```cpp
struct reg1 {
int codigo;
int cantidad;
int precio;
}; 
```
- Y otro llamado "pesos.dat", cuyos elementos son del tipo siguiente:
```cpp
struct reg2 {
int codigo;
int peso;
int cantidad;
};
```
Los artículos en ambos ficheros estarán ordenados ascendentemente por código. 

Solucion: 
```cpp
#include <conio.h>
#include <iostream>
#include <fstream>

using namespace std;

struct reg1 {
	int codigo;
	int cantidad;
	int precio;
};

struct reg2 {
	int codigo;
	int cantidad;
	int peso;
};

void creapesos();
void creaprecios();

int main() {
	char opcion;
	
	do {
		system("cls");
		cout << "Este programa crea los ficheros \n";
		cout << "Los codigos ordenados \n";
		cout << " Elija opcion\n";
		cout << " 1 - Crear fichero de pesos\n";
		cout << " 2 - Crear fichero de precios\n";
		cout << " 3 - Salir\n";
		opcion = getch();
		switch (opcion) {
			case '1': creapesos(); break;
			case '2': creaprecios(); break;
			case '3': break;
			default: cout<<"Opcion incorrecta\n"; break;
		}
	} while (opcion!='3');
	
	return 0;
}

void creaprecios() {
	reg1 r1;
	int ultimo = -1;
	char seguir;
	
	ofstream f1("precios.dat", ios::binary);
	if (f1) {
		cout << "Se crea fichero de precios\n";
		do {
			do {
				cout <<"Deme codigo\n ";
				cin >> r1.codigo;
			} while (r1.codigo <= ultimo);
			
			ultimo = r1.codigo;
			
			cout <<"Deme cantidad\n ";
			cin >> r1.cantidad;
			cout <<"Deme precio\n ";
			cin >> r1.precio;
			
			f1.write((char*) &r1, sizeof(reg1));
			
			cout << "Desea mas datos (s/n)?\n";
			seguir = getch();
		} while (seguir != 'n');
		f1.close();
	}
	else
		cout << "Error en la apertura del fichero\n";
}

void creapesos() {
	reg2 r2;
	int ultimo = -1;
	char seguir;
	
	ofstream f2("pesos.dat", ios::binary);
	if (f2) {
		cout << "Se crea fichero de pesos\n";
		do {
			do {
				cout <<"Deme codigo\n ";
				cin >> r2.codigo;
			} while (r2.codigo <= ultimo);
			
			ultimo = r2.codigo;
			
			cout <<"Deme cantidad\n ";
			cin >> r2.cantidad;
			cout <<"Deme peso\n ";
			cin >> r2.peso;
			
			f2.write((char*) &r2, sizeof(reg2));
			
			cout << "Desea mas datos (s/n)?\n";
			seguir = getch();
		} while (seguir != 'n');
		f2.close();
	}
	else
		cout << "Error en la apertura del fichero\n";
}
```

## Ejercicio 4
A partir de los ficheros del ejercicio anterior, cree un algoritmo que fusione la información de ambos ficheros en otro que se llamará "mezcla.dat", cuyos elementos estarán ordenados ascendentemente según el campo código y serán del tipo: 
```cpp
struct reg3 {
int codigo;
int cantidad;
int datos[2];
 /* posición 0: precio
 posición 1: peso */
}; 
```
Si un artículo tiene información en ambos ficheros, en el campo cantidad se almacenará
la suma de las dos cantidades que aparecen. 

Solucion: 
```cpp
#include <iostream>
#include <fstream>
#include <conio.h>
using namespace std;
struct reg1{
int codigo;
int cantidad;
int precio;
};
struct reg2{
int codigo;
int cantidad;
int peso;
};
struct reg3{
int codigo;
int cantidad;
int datos[2];
};
int main() {
reg1 r1;
reg2 r2;
reg3 r3;
ifstream f1(“precios.dat”, ios::binary);
if (f1){
ifstream f2("pesos.dat", ios::binary);
if (f2) {
ofstream f3("mezcla.dat", ios::binary);
if (f3) {
f1.read((char*) &r1, sizeof(reg1));
f2.read((char*)&r2, sizeof(reg2));
while (!f1.eof() && !f2.eof()){
if (r1.codigo < r2.codigo) {
r3.codigo = r1.codigo;
r3.cantidad = r1.cantidad;
r3.datos[0] = r1.precio;
r3.datos[1] = 0;
f1.read((char*)&r1, sizeof(reg1));
}
else if (r1.codigo > r2.codigo) {
r3.codigo = r2.codigo;
r3.cantidad = r2.cantidad;
r3.datos[1] = r2.peso;
r3.datos[0] = 0;
f2.read((char*)&r2, sizeof(reg2));
}
else {
r3.codigo = r1.codigo;
r3.cantidad = r1.cantidad+r2.cantidad;
r3.datos[0] = r1.precio;
r3.datos[1] = r2.peso;
f1.read((char*)&r1, sizeof(reg1));
f2.read((char*)&r2, sizeof(reg2));
}
f3.write((char*)&r3, sizeof(reg3));
}
while (!f1.eof()) {
r3.codigo = r1.codigo;
r3.cantidad = r1.cantidad;
r3.datos[0] = r1.precio;
r3.datos[1] = 0;
f1.read((char*)&r1, sizeof(reg1));
f3.write((char*)&r3, sizeof(reg3)); }
while (!f2.eof()) {
r3.codigo = r2.codigo;
r3.cantidad = r2.cantidad;
r3.datos[1] = r2.peso;
r3.datos[0] = 0;
f2.read((char*)&r2, sizeof(reg2));
f3.write((char*)&r3, sizeof(reg3));
}
f1.close();
f2.close();
f3.close();
}
}
else cout <<"Error en la apertura de pesos";
}
else cout <<"Error en la apertura de precios";
getch();
return 0;
}
```
## Ejercicio 5
Realizar un programa que a partir de un fichero “datos1.txt”, escriba su contenido en otro fichero “datos2.txt” pero al revés, sin usar ninguna estructura de datos auxiliar. 
```cpp
#include <iostream>
#include <fstream>

using namespace std;

int main() {
	char c;
	int num;
 
	ifstream in("datos1.txt", ios::binary); //apertura en modo binario y para lectura de datos1
 	if (!in.fail()) { //si no hay fallo
		ofstream out("datos2.txt", ios::binary); //apertura binaria para escritura de datos2. Se situa al principio
		in.seekg(0, ios::end);  //posicionamiento al final del fichero datos1 
		num = in.tellg(); //obtenemos cuantos bytes tiene datos1
		while (num != 0) //mientras haya "bytes" que recorrer
		{   
			in.seekg(sizeof(char)*(num-1), ios::beg); //nos situamos en el último byte (num-1), siguiente vuelta num vale uno menos..penúltimo, luego antepenúltimo...
			in.read((char*) &c, sizeof(char)); //leeemos el byte (char) existente en la posición en cuestión
			out.write((char*) &c, sizeof(char)); //escribimos dicho byte (char) en el fichero datos2 
			num--; //ya queda un byte menos que recorrer
		}
		out.close(); //cerramos el fichero datos2
	}
 	else
	{
		cout<<"Error al abrir el fichero \n";
		in.clear();
 	}
 	in.close();   //cierre de datos1

	system("pause");
	return 0;
}

```
