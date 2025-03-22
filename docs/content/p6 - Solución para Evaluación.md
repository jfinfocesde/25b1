### Solución para Evaluación

#### 1. Clase Estudiante
```java
public class Estudiante {
    private String nombre;
    private int edad;

    // Constructor
    public Estudiante(String nombre, int edad) {
        this.nombre = nombre; // Uso de this para diferenciar
        this.edad = edad;     // Uso de this para diferenciar
    }

    // Getters
    public String getNombre() {
        return nombre;
    }

    public int getEdad() {
        return edad;
    }

    @Override
    public String toString() {
        return "Estudiante{nombre='" + nombre + "', edad=" + edad + "}";
    }
}
```

#### 2. Clase Escuela
```java
import java.util.ArrayList;
import java.util.List;

public class Escuela {
    private List<Estudiante> estudiantes;

    // Constructor
    public Escuela() {
        this.estudiantes = new ArrayList<>();
    }

    // Agregar estudiante
    public void agregarEstudiante(Estudiante estudiante) {
        estudiantes.add(estudiante);
        System.out.println("Estudiante agregado: " + estudiante.getNombre());
    }

    // Mostrar lista de estudiantes
    public void mostrarEstudiantes() {
        if (estudiantes.isEmpty()) {
            System.out.println("No hay estudiantes registrados.");
        } else {
            System.out.println("Lista de estudiantes:");
            for (Estudiante estudiante : estudiantes) {
                System.out.println(estudiante);
            }
        }
    }
}
```

#### 3. Programa Principal
```java
public class Main {
    public static void main(String[] args) {
        // Crear una escuela
        Escuela escuela = new Escuela();

        // Agregar estudiantes
        escuela.agregarEstudiante(new Estudiante("Ana", 15));
        escuela.agregarEstudiante(new Estudiante("Luis", 16));

        // Mostrar lista de estudiantes
        escuela.mostrarEstudiantes();
    }
}
```

#### Salida Esperada
```
Estudiante agregado: Ana
Estudiante agregado: Luis
Lista de estudiantes:
Estudiante{nombre='Ana', edad=15}
Estudiante{nombre='Luis', edad=16}
```

---