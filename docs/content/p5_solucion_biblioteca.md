# Implementación completa del sistema de gestión de biblioteca 

---

### **Código Fuente**

#### 1. Clase `Libro`

```java
public class Libro {
    private String titulo;
    private String autor;
    private String ISBN;
    private int anioPublicacion;
    private boolean disponible;

    // Constructor
    public Libro(String titulo, String autor, String ISBN, int anioPublicacion) {
        this.titulo = titulo;
        this.autor = autor;
        this.ISBN = ISBN;
        this.anioPublicacion = anioPublicacion;
        this.disponible = true; // Por defecto, el libro está disponible
    }

    // Getters y Setters
    public String getTitulo() {
        return titulo;
    }

    public void setTitulo(String titulo) {
        this.titulo = titulo;
    }

    public String getAutor() {
        return autor;
    }

    public void setAutor(String autor) {
        this.autor = autor;
    }

    public String getISBN() {
        return ISBN;
    }

    public void setISBN(String ISBN) {
        this.ISBN = ISBN;
    }

    public int getAnioPublicacion() {
        return anioPublicacion;
    }

    public void setAnioPublicacion(int anioPublicacion) {
        this.anioPublicacion = anioPublicacion;
    }

    public boolean isDisponible() {
        return disponible;
    }

    // Métodos específicos
    public void marcarComoPrestado() {
        this.disponible = false;
    }

    public void marcarComoDisponible() {
        this.disponible = true;
    }

    @Override
    public String toString() {
        return "Libro{" +
                "titulo='" + titulo + '\'' +
                ", autor='" + autor + '\'' +
                ", ISBN='" + ISBN + '\'' +
                ", añoPublicacion=" + anioPublicacion +
                ", disponible=" + disponible +
                '}';
    }
}
```

---

#### 2. Clase `Usuario`

```java
import java.util.ArrayList;
import java.util.List;

public class Usuario {
    private int id;
    private String nombre;
    private String email;
    private List<Prestamo> prestamosActuales;

    // Constructor
    public Usuario(int id, String nombre, String email) {
        this.id = id;
        this.nombre = nombre;
        this.email = email;
        this.prestamosActuales = new ArrayList<>();
    }

    // Getters y Setters
    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    public String getNombre() {
        return nombre;
    }

    public void setNombre(String nombre) {
        this.nombre = nombre;
    }

    public String getEmail() {
        return email;
    }

    public void setEmail(String email) {
        this.email = email;
    }

    public List<Prestamo> getPrestamosActuales() {
        return prestamosActuales;
    }

    // Métodos específicos
    public void agregarPrestamo(Prestamo prestamo) {
        if (prestamosActuales.size() < 3) { // Regla: Máximo 3 préstamos por usuario
            prestamosActuales.add(prestamo);
        } else {
            System.out.println("El usuario ya tiene el máximo de préstamos permitidos.");
        }
    }

    public void eliminarPrestamo(Prestamo prestamo) {
        prestamosActuales.remove(prestamo);
    }

    @Override
    public String toString() {
        return "Usuario{" +
                "id=" + id +
                ", nombre='" + nombre + '\'' +
                ", email='" + email + '\'' +
                ", prestamosActuales=" + prestamosActuales +
                '}';
    }
}
```

---

#### 3. Clase `Prestamo`

```java
import java.time.LocalDate;

public class Prestamo {
    private Libro libro;
    private Usuario usuario;
    private LocalDate fechaPrestamo;
    private LocalDate fechaDevolucionPrevista;

    // Constructor
    public Prestamo(Libro libro, Usuario usuario) {
        this.libro = libro;
        this.usuario = usuario;
        this.fechaPrestamo = LocalDate.now();
        this.fechaDevolucionPrevista = fechaPrestamo.plusDays(15); // Regla: Máximo 15 días
    }

    // Getters y Setters
    public Libro getLibro() {
        return libro;
    }

    public void setLibro(Libro libro) {
        this.libro = libro;
    }

    public Usuario getUsuario() {
        return usuario;
    }

    public void setUsuario(Usuario usuario) {
        this.usuario = usuario;
    }

    public LocalDate getFechaPrestamo() {
        return fechaPrestamo;
    }

    public void setFechaPrestamo(LocalDate fechaPrestamo) {
        this.fechaPrestamo = fechaPrestamo;
    }

    public LocalDate getFechaDevolucionPrevista() {
        return fechaDevolucionPrevista;
    }

    public void setFechaDevolucionPrevista(LocalDate fechaDevolucionPrevista) {
        this.fechaDevolucionPrevista = fechaDevolucionPrevista;
    }

    // Método específico
    public int calcularDiasRetraso() {
        LocalDate hoy = LocalDate.now();
        if (hoy.isAfter(fechaDevolucionPrevista)) {
            return (int) fechaDevolucionPrevista.until(hoy).getDays();
        }
        return 0; // No hay retraso
    }

    @Override
    public String toString() {
        return "Préstamo{" +
                "libro=" + libro.getTitulo() +
                ", usuario=" + usuario.getNombre() +
                ", fechaPrestamo=" + fechaPrestamo +
                ", fechaDevolucionPrevista=" + fechaDevolucionPrevista +
                '}';
    }
}
```

---

#### 4. Clase `Biblioteca`

```java
import java.util.ArrayList;
import java.util.List;

public class Biblioteca {
    private List<Libro> libros;
    private List<Usuario> usuarios;
    private List<Prestamo> prestamos;

    // Constructor
    public Biblioteca() {
        this.libros = new ArrayList<>();
        this.usuarios = new ArrayList<>();
        this.prestamos = new ArrayList<>();
    }

    // Métodos sobrecargados para agregar libros
    public void agregarLibro(Libro libro) {
        libros.add(libro);
    }

    public void agregarLibro(String titulo, String autor, String ISBN, int anioPublicacion) {
        Libro libro = new Libro(titulo, autor, ISBN, anioPublicacion);
        libros.add(libro);
    }

    // Métodos sobrecargados para registrar usuarios
    public void registrarUsuario(Usuario usuario) {
        usuarios.add(usuario);
    }

    public void registrarUsuario(int id, String nombre, String email) {
        Usuario usuario = new Usuario(id, nombre, email);
        usuarios.add(usuario);
    }

    // Realizar préstamo
    public void realizarPrestamo(Libro libro, Usuario usuario) {
        if (!libro.isDisponible()) {
            System.out.println("El libro no está disponible.");
            return;
        }
        if (usuario.getPrestamosActuales().size() >= 3) {
            System.out.println("El usuario ya tiene el máximo de préstamos permitidos.");
            return;
        }
        libro.marcarComoPrestado();
        Prestamo prestamo = new Prestamo(libro, usuario);
        prestamos.add(prestamo);
        usuario.agregarPrestamo(prestamo);
        System.out.println("Préstamo realizado con éxito.");
    }

    // Registrar devolución
    public void registrarDevolucion(Libro libro, Usuario usuario) {
        for (Prestamo prestamo : prestamos) {
            if (prestamo.getLibro().equals(libro) && prestamo.getUsuario().equals(usuario)) {
                libro.marcarComoDisponible();
                usuario.eliminarPrestamo(prestamo);
                prestamos.remove(prestamo);
                System.out.println("Devolución registrada con éxito.");
                return;
            }
        }
        System.out.println("No se encontró el préstamo correspondiente.");
    }

    // Buscar libros (sobrecarga)
    public List<Libro> buscarLibrosPorTitulo(String titulo) {
        List<Libro> resultados = new ArrayList<>();
        for (Libro libro : libros) {
            if (libro.getTitulo().toLowerCase().contains(titulo.toLowerCase())) {
                resultados.add(libro);
            }
        }
        return resultados;
    }

    public List<Libro> buscarLibrosPorAutor(String autor) {
        List<Libro> resultados = new ArrayList<>();
        for (Libro libro : libros) {
            if (libro.getAutor().toLowerCase().contains(autor.toLowerCase())) {
                resultados.add(libro);
            }
        }
        return resultados;
    }

    // Consultar historial de préstamos de un usuario
    public List<Prestamo> consultarHistorialPrestamos(Usuario usuario) {
        List<Prestamo> historial = new ArrayList<>();
        for (Prestamo prestamo : prestamos) {
            if (prestamo.getUsuario().equals(usuario)) {
                historial.add(prestamo);
            }
        }
        return historial;
    }

    // Generar informes
    public void generarInforme() {
        System.out.println("=== Informe de la Biblioteca ===");
        System.out.println("Libros disponibles: " + libros.size());
        System.out.println("Usuarios registrados: " + usuarios.size());
        System.out.println("Préstamos activos: " + prestamos.size());
    }
}
```

---

#### 5. Programa Principal

```java
public class Main {
    public static void main(String[] args) {
        Biblioteca biblioteca = new Biblioteca();

        // Registrar libros
        biblioteca.agregarLibro(new Libro("El Quijote", "Miguel de Cervantes", "1234567890", 1605));
        biblioteca.agregarLibro("Cien años de soledad", "Gabriel García Márquez", "0987654321", 1967);

        // Registrar usuarios
        biblioteca.registrarUsuario(new Usuario(1, "Juan Pérez", "juan@example.com"));
        biblioteca.registrarUsuario(2, "María López", "maria@example.com");

        // Obtener referencias a libros y usuarios
        Libro libro1 = biblioteca.buscarLibrosPorTitulo("Quijote").get(0);
        Usuario usuario1 = biblioteca.consultarHistorialPrestamos(new Usuario(1, "", "")).get(0).getUsuario();

        // Realizar préstamo
        biblioteca.realizarPrestamo(libro1, usuario1);

        // Consultar disponibilidad
        System.out.println("Disponibilidad de 'El Quijote': " + libro1.isDisponible());

        // Registrar devolución
        biblioteca.registrarDevolucion(libro1, usuario1);

        // Generar informe
        biblioteca.generarInforme();
    }
}
```

---
