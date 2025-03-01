# Flujo de Trabajo en GitHub: Guía Completa y Tutorial Práctico

## Parte 1: Entendiendo el Flujo de Trabajo en GitHub

### Estructura de Ramas

1. **Ramas Principales**:
   - `main` (o `master`): Contiene el código de producción estable
   - `develop`: Rama principal de desarrollo

2. **Ramas de Soporte**:
   - `feature/*`: Para nuevas funcionalidades
   - `hotfix/*`: Para correcciones urgentes
   - `release/*`: Para preparar nuevas versiones

### Proceso de Desarrollo

1. **Inicio del Desarrollo**:
   - Clonar el repositorio
   - Crear rama develop desde main
   - Crear ramas feature desde develop

2. **Desarrollo de Características**:
   - Trabajar en ramas feature
   - Realizar commits frecuentes
   - Mantener sincronización con develop

3. **Integración de Cambios**:
   - Crear Pull Requests
   - Realizar Code Reviews
   - Resolver conflictos
   - Merge a develop

4. **Preparación de Releases**:
   - Crear rama release desde develop
   - Realizar pruebas finales
   - Merge a main y develop

## Parte 2: Tutorial Práctico - Calculadora Colaborativa

### Configuración Inicial

**Desarrollador 1 (Líder del Proyecto)**:

1. Crear el repositorio en GitHub:
   ```bash
   # Crear y configurar el repositorio local
   mkdir calculadora-colaborativa
   cd calculadora-colaborativa
   git init
   
   # Crear estructura inicial del proyecto
   touch README.md
   mkdir src
   
   # Commit inicial
   git add .
   git commit -m "feat: inicialización del proyecto"
   
   # Conectar con GitHub y subir código
   git remote add origin [URL_DEL_REPOSITORIO]
   git push -u origin main
   
   # Crear y configurar rama develop
   git checkout -b develop
   git push -u origin develop
   ```

**Desarrollador 2 (Colaborador)**:

1. Clonar el repositorio:
   ```bash
   git clone [URL_DEL_REPOSITORIO]
   cd calculadora-colaborativa
   git checkout develop
   ```

### Desarrollo de Funcionalidades

**Desarrollador 1 - Implementar Suma y Resta**:

1. Crear rama de característica:
   ```bash
   git checkout develop
   git pull origin develop
   git checkout -b feature/operaciones-basicas
   ```

2. Implementar código:
   ```java
   // Calculadora.java
   public class Calculadora {
       public double sumar(double a, double b) {
           return a + b;
       }
       
       public double restar(double a, double b) {
           return a - b;
       }
   }
   ```

3. Commit y push:
   ```bash
   git add .
   git commit -m "feat: implementa operaciones de suma y resta"
   git push origin feature/operaciones-basicas
   ```

**Desarrollador 2 - Implementar Multiplicación y División**:

1. Crear rama de característica:
   ```bash
   git checkout develop
   git pull origin develop
   git checkout -b feature/operaciones-avanzadas
   ```

2. Implementar código:
   ```java
   // Calculadora.java
   public class Calculadora {
       public double multiplicar(double a, double b) {
           return a * b;
       }
       
       public double dividir(double a, double b) {
           if (b == 0) {
               throw new IllegalArgumentException("No se puede dividir por cero");
           }
           return a / b;
       }
   }
   ```

### Manejo de Conflictos

1. **Desarrollador 2** - Crear Pull Request:
   - Ir a GitHub
   - Crear PR de `feature/operaciones-avanzadas` a `develop`
   - Asignar a Desarrollador 1 como reviewer

2. **Desarrollador 1** - Resolver Conflictos:
   ```bash
   git checkout develop
   git pull origin develop
   git checkout feature/operaciones-basicas
   git merge develop
   ```

3. **Resolver conflictos en Calculadora.java**:
   ```java
   public class Calculadora {
       public double sumar(double a, double b) {
           return a + b;
       }
       
       public double restar(double a, double b) {
           return a - b;
       }
       
       public double multiplicar(double a, double b) {
           return a * b;
       }
       
       public double dividir(double a, double b) {
           if (b == 0) {
               throw new IllegalArgumentException("No se puede dividir por cero");
           }
           return a / b;
       }
   }
   ```

### Preparación del Release

1. **Desarrollador 1** - Crear rama release:
   ```bash
   git checkout develop
   git pull origin develop
   git checkout -b release/v1.0.0
   ```

2. **Ambos Desarrolladores** - Pruebas finales

3. **Desarrollador 1** - Merge a main:
   ```bash
   git checkout main
   git merge release/v1.0.0
   git tag -a v1.0.0 -m "Primera versión estable"
   git push origin main --tags
   
   git checkout develop
   git merge release/v1.0.0
   git push origin develop
   ```

### Buenas Prácticas Implementadas

1. **Comunicación**:
   - Usar mensajes de commit descriptivos
   - Documentar cambios en PRs
   - Mantener discusiones en los PRs

2. **Gestión de Código**:
   - Revisiones de código obligatorias
   - No hacer push directo a main/develop
   - Mantener ramas actualizadas

3. **Resolución de Conflictos**:
   - Resolver conflictos localmente
   - Probar después de resolver conflictos
   - Comunicar cambios significativos

Este tutorial práctico demuestra un flujo de trabajo real en GitHub, incluyendo todas las interacciones posibles entre dos desarrolladores, desde la configuración inicial hasta el lanzamiento de una versión estable.