
[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/kuYFMccO)
# parte1
✏️ Parte I – Completar una función del CRUD
📝 Instrucciones:
A continuación te damos un programa incompleto que implementa parte del CRUD de estudiantes usando estructuras (struct), funciones y manejo de archivos. Tu tarea es completar la función faltante correspondiente a una operación del CRUD , siguiendo las indicaciones.

Puedes usar o no el manejo de archivos según lo desees, pero si lo implementas correctamente obtendrás **2 puntos extra**.
🔧 Código proporcionado (incompleto):


```cpp
#include <iostream>
#include <fstream>
using namespace std;

struct Estudiante {
    string nombre;
    string carnet;
    int edad;
};

// Función para agregar estudiante (CREATE)
void agregarEstudiante() {
    Estudiante e;
    cout << "Nombre (sin espacios): ";
    cin >> e.nombre;
    cout << "Carnet: ";
    cin >> e.carnet;
    cout << "Edad: ";
    cin >> e.edad;

    ofstream archivo("estudiantes.txt", ios::app);
    if (archivo.is_open()) {
        archivo << e.nombre << " " << e.carnet << " " << e.edad << endl;
        archivo.close();
        cout << "Estudiante agregado correctamente.\n";
    } else {
        cout << "Error al abrir el archivo.\n";
    }
}

// Función para mostrar estudiantes (READ)
void mostrarEstudiantes() {
    ifstream archivo("estudiantes.txt");
    Estudiante e;

    if (archivo.is_open()) {
        cout << "\n--- Lista de Estudiantes ---\n";
        while (archivo >> e.nombre >> e.carnet >> e.edad) {
            cout << "Nombre: " << e.nombre 
                 << ", Carnet: " << e.carnet
                 << ", Edad: " << e.edad << endl;
        }
        archivo.close();
    } else {
        cout << "Error al abrir el archivo.\n";
    }
}

// Función para modificar estudiante (UPDATE)
void modificarEstudiante() {
    ifstream archivo("estudiantes.txt");
    ofstream temp("temp.txt");
    Estudiante e;
    string buscado;
    bool modificado = false;

    cout << "Ingrese carnet a modificar: ";
    cin >> buscado;

    if (archivo.is_open() && temp.is_open()) {
        while (archivo >> e.nombre >> e.carnet >> e.edad) {
            if (e.carnet == buscado) {
                Estudiante nuevo;
                cout << "Nuevo nombre (sin espacios): ";
                cin >> nuevo.nombre;
                cout << "Nuevo carnet: ";
                cin >> nuevo.carnet;
                cout << "Nueva edad: ";
                cin >> nuevo.edad;

                temp << nuevo.nombre << " " << nuevo.carnet << " " << nuevo.edad << endl;
                modificado = true;
            } else {
                temp << e.nombre << " " << e.carnet << " " << e.edad << endl;
            }
        }
        archivo.close();
        temp.close();
        remove("estudiantes.txt");
        rename("temp.txt", "estudiantes.txt");

        if (modificado)
            cout << "Estudiante modificado correctamente.\n";
        else
            cout << "Carnet no encontrado.\n";
    } else {
        cout << "Error abriendo los archivos.\n";
    }
}

// -----------------------------
// 👇 TU TAREA: Completa esta función (DELETE)
void eliminarEstudiante() {
   int main() {
    string estudiantes[3][2] = {
        {"A123", "Juan"},
        {"B456", "María"},
        {"C789", "Pedro"}
    };
    
    cout << "=== ELIMINAR ESTUDIANTE ===\n";
    cout << "Estudiantes actuales:\n";
    for(int i = 0; i < 3; i++) {
        cout << estudiantes[i][0] << " - " << estudiantes[i][1] << endl;
    }
    
    string carnet;
    cout << "\nIngrese carnet a eliminar: ";
    cin >> carnet;
    
    bool encontrado = false;
    for(int i = 0; i < 3; i++) {
        if(estudiantes[i][0] == carnet) {
            // "Eliminamos" marcando como vacío (lo haría mejor un alumno avanzado)
            estudiantes[i][0] = "ELIMINADO";
            estudiantes[i][1] = "";
            encontrado = true;
        }
    }
    
    if(encontrado) {
        cout << "\nEstudiante eliminado (a medias)\n";
        cout << "Lista actualizada:\n";
        for(int i = 0; i < 3; i++) {
            if(estudiantes[i][0] != "ELIMINADO") {
                cout << estudiantes[i][0] << " - " << estudiantes[i][1] << endl;
            }
        }
    } else {
        cout << "\nCarnet no encontrado :(\n";
    }
    
// -----------------------------

// Menú principal
int main() {
    int opcion;
    do {
        cout << "\n=== CRUD de Estudiantes ===\n";
        cout << "1. Agregar estudiante\n";
        cout << "2. Mostrar todos\n";
        cout << "3. Modificar estudiante\n";
        cout << "4. Eliminar estudiante\n";
        cout << "5. Salir\n";
        cout << "Seleccione una opción: ";
        cin >> opcion;

        switch (opcion) {
            case 1: agregarEstudiante(); break;
            case 2: mostrarEstudiantes(); break;
            case 3: modificarEstudiante(); break;
            case 4: eliminarEstudiante(); break;
            case 5: cout << "Saliendo...\n"; break;
            default: cout << "Opción inválida.\n";
        }

    } while (opcion != 5);

    return 0;
```
📌 Tu tarea:
Completa la función eliminarEstudiante() para que:

Lea el carnet del estudiante a eliminar.
Elimine ese registro del archivo o de la lista en memoria.
Muestre un mensaje de confirmación o error.
}
