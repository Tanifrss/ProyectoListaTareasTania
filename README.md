#include <iostream>
#include <vector>
#include <string>

using namespace std;

// Estructura que representa una tarea
struct Tarea {
    string descripcion;
    bool completada;
};

// Prototipos de funciones
void agregarTarea(vector<Tarea>& tareas);
void mostrarTareas(const vector<Tarea>& tareas);
void completarTarea(vector<Tarea>& tareas);

int main() {
    vector<Tarea> tareas;
    int opcion = 0; // Inicializada para evitar valores basura

    while (opcion != 4) {
        cout << "\nLISTA DE TAREAS\n\n";
        cout << "1. Agregar tarea\n";
        cout << "2. Mostrar tareas\n";
        cout << "3. Marcar tarea como completada\n";
        cout << "4. Salir\n\n";
        cout << "Seleccione una opción: ";

        cin >> opcion;
        cin.ignore(); // Limpia el búfer para el getline posterior

        switch (opcion) {
            case 1:
                agregarTarea(tareas);
                break;
            case 2:
                mostrarTareas(tareas);
                break;
            case 3:
                completarTarea(tareas);
                break;
            case 4:
                cout << "Saliendo del programa...\n";
                break;
            default:
                cout << "Opción no válida.\n";
                break;
        }
    }

    return 0;
}

// Agrega una nueva tarea al vector
void agregarTarea(vector<Tarea>& tareas) {
    Tarea nueva;
    
    cout << "Ingrese la tarea: ";
    getline(cin, nueva.descripcion);
    
    if (nueva.descripcion == "") {
        cout << "La tarea no puede estar vacía.\n";
        return;
    }
    
    nueva.completada = false;
    tareas.push_back(nueva);
    cout << "Nueva tarea añadida correctamente.\n";
}

// Muestra todas las tareas
void mostrarTareas(const vector<Tarea>& tareas) {
    if (tareas.empty()) {
        cout << "No hay tareas registradas.\n";
        return;
    }

    cout << "\n--- TAREAS ---\n";
    for (size_t i = 0; i < tareas.size(); i++) { // Sintaxis del for corregida
        cout << i + 1 << ". ";
        
        if (tareas[i].completada) {
            cout << "[Completada] ";
        } else {
            cout << "[Pendiente]  ";
        }
        
        cout << tareas[i].descripcion << endl; 
    }
}

// Marca una tarea como completada
void completarTarea(vector<Tarea>& tareas) {
    if (tareas.empty()) {
        cout << "No hay tareas para marcar como completadas.\n";
        return;
    }

    mostrarTareas(tareas);
    int numeroTarea;
    cout << "\nIngrese el número de la tarea a completar: ";
    cin >> numeroTarea;

    if (numeroTarea < 1 || numeroTarea > static_cast<int>(tareas.size())) {
        cout << "Número de tarea inválido.\n";
    } else {
        tareas[numeroTarea - 1].completada = true;
        cout << "Tarea marcada como completada con éxito.\n";
    }
}
