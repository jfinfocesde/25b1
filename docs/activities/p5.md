# Semana 7 - Actividad Práctica: Implementación de Herencia

### Objetivo
Implementar un sistema de herencia en Java aplicando los conceptos aprendidos en clase, utilizando control de versiones con Git y GitHub.

### Instrucciones

#### Paso 1: Configuración del Repositorio

1. **Hacer Fork del Repositorio Base**
   - Accede al repositorio: `https://github.com/jfinfocesde/act_b1_s7.git`
   - Haz clic en el botón **"Fork"** en la esquina superior derecha
   - Selecciona tu cuenta personal como destino del fork
   - Espera a que se complete el proceso de fork

2. **Clonar tu Fork Localmente**
   ```bash
   git clone https://github.com/TU_USUARIO/act_b1_s7.git
   cd act_b1_s7
   ```

3. **Configurar Información Personal**
   - Abre el archivo `info.json` en la raíz del proyecto
   - Completa la información solicitada:

   ```json
   {
       "identificacion": "1234567890",
       "nombres": "Tu Nombre Completo",
       "apellidos": "Tus Apellidos Completos", 
       "grupo": "b1-martes"
   }
   ``` 

#### Paso 2: Desarrollo de la Actividad

**Implementar el Sistema de Tienda de Productos**

Basándote en el ejemplo de empleados visto en clase, debes crear un sistema de tienda con las siguientes características:

### 🏪 Lógica de Negocio Detallada

#### **Clase Padre: `Producto`**

**Atributos protegidos:**

- `String nombre` - Nombre del producto
- `double precioBase` - Precio base sin impuestos ni descuentos
- `String codigo` - Código único del producto (formato: "PROD-XXXX")
- `int cantidadStock` - Cantidad disponible en inventario
- `String categoria` - Categoría general del producto
- `boolean activo` - Si el producto está activo para venta

**Constructor:**
```java
public Producto(String nombre, double precioBase, String codigo, 
               int cantidadStock, String categoria)
```

**Métodos obligatorios:**

1. **Getters y Setters con validaciones:**

    - `setPrecioBase()`: Solo acepta valores > 0
    - `setCantidadStock()`: Solo acepta valores >= 0
    - `setCodigo()`: Debe seguir formato "PROD-XXXX"

2. **Lógica de negocio base:**
   ```java
   public double calcularPrecioFinal() {
       // TODO: Calcular precio base + IVA (19%)
       // Retornar el precio base multiplicado por 1.19
   }
   
   public boolean hayStock(int cantidad) {
       // TODO: Verificar si hay suficiente stock disponible
       // Comprobar que cantidadStock >= cantidad Y que el producto esté activo
       // Retornar true si ambas condiciones se cumplen, false en caso contrario
   }
   
   public void vender(int cantidad) {
       // TODO: Implementar lógica de venta
       // 1. Verificar si hay suficiente stock usando hayStock()
       // 2. Si hay stock: reducir cantidadStock en la cantidad vendida
       // 3. Mostrar mensaje "Venta exitosa: [cantidad] unidades de [nombre]"
       // 4. Si no hay stock: mostrar mensaje "Error: Stock insuficiente"
   }
   
   public void reabastecer(int cantidad) {
       // TODO: Aumentar el stock del producto
       // 1. Sumar la cantidad al cantidadStock actual
       // 2. Mostrar mensaje "Reabastecimiento exitoso: +[cantidad] unidades de [nombre]"
   }
   
   public double calcularDescuento() {
       // TODO: Retornar descuento base
       // La clase padre no tiene descuentos, retornar 0.0
   }
   ```

#### **Clase Hija: `ProductoElectronico`**

**Atributos adicionales:**

- `int garantiaMeses` - Meses de garantía
- `String marca` - Marca del producto
- `double voltaje` - Voltaje de operación
- `boolean esImportado` - Si es producto importado

**Lógica de negocio específica:**

1. **Método específico `calcularPrecioElectronico()`:**
   ```java
   public double calcularPrecioElectronico() {
       // TODO: Calcular precio final para productos electrónicos
       // 1. Obtener precio con IVA usando calcularPrecioFinal()
       // 2. Si esImportado es true: agregar impuesto adicional del 5% sobre precioBase
       // 3. Calcular descuento usando calcularDescuentoGarantia()
       // 4. Aplicar descuento: precio - (precio * descuento)
       // 5. Retornar el precio final calculado
   }
   ```

2. **Método específico `calcularDescuentoGarantia()`:**
   ```java
   public double calcularDescuentoGarantia() {
       // TODO: Calcular descuento basado en meses de garantía
       // Si garantiaMeses >= 24: retornar 0.10 (10% descuento)
       // Si garantiaMeses >= 12: retornar 0.05 (5% descuento)
       // En otros casos: retornar 0.0 (sin descuento)
   }
   ```

3. **Métodos específicos:**
   ```java
   public boolean esGarantiaExtendida() {
       // TODO: Verificar si la garantía es extendida
       // Retornar true si garantiaMeses > 12, false en caso contrario
   }
   
   public double calcularCostoGarantia() {
       // TODO: Calcular costo de la garantía
       // Fórmula: precioBase * 0.02 * garantiaMeses
       // (2% del precio base por cada mes de garantía)
   }
   
   public boolean esCompatibleVoltaje(double voltajeLocal) {
       // TODO: Verificar compatibilidad de voltaje
       // Calcular diferencia absoluta entre voltaje y voltajeLocal
       // Retornar true si la diferencia es <= 10% del voltajeLocal
       // Usar Math.abs() para valor absoluto
   }
   ```

#### **Clase Hija: `ProductoAlimenticio`**

**Atributos adicionales:**

- `boolean refrigerado` - Si requiere refrigeración
- `String lote` - Número de lote de producción
- `int diasParaVencer` - Días restantes para vencimiento

**Lógica de negocio específica:**

1. **Método específico `calcularPrecioAlimenticio()`:**
   ```java
   public double calcularPrecioAlimenticio() {
       // TODO: Calcular precio final para productos alimenticios
       // 1. Obtener precio con IVA usando calcularPrecioFinal()
       // 2. Si refrigerado es true: agregar costo adicional del 8% sobre precioBase
       // 3. Calcular descuento usando calcularDescuentoVencimiento()
       // 4. Aplicar descuento: precio - (precio * descuento)
       // 5. Retornar el precio final calculado
   }
   ```

2. **Método específico `calcularDescuentoVencimiento()`:**
   ```java
   public double calcularDescuentoVencimiento() {
       // TODO: Calcular descuento basado en días para vencer
       // Si diasParaVencer <= 3: retornar 0.50 (50% descuento)
       // Si diasParaVencer <= 7: retornar 0.30 (30% descuento)
       // Si diasParaVencer <= 15: retornar 0.15 (15% descuento)
       // En otros casos: retornar 0.0 (sin descuento)
   }
   ```

3. **Métodos específicos:**
   ```java
   public boolean estaProximoAVencer() {
       // TODO: Verificar si el producto está próximo a vencer
       // Retornar true si diasParaVencer <= 7, false en caso contrario
   }
   
   public boolean estaVencido() {
       // TODO: Verificar si el producto está vencido
       // Retornar true si diasParaVencer <= 0, false en caso contrario
   }
   
   public String obtenerEstadoFrescura() {
       // TODO: Determinar el estado de frescura del producto
       // Si estaVencido(): retornar "VENCIDO"
       // Si diasParaVencer <= 3: retornar "URGENTE"
       // Si diasParaVencer <= 7: retornar "PRÓXIMO A VENCER"
       // Si diasParaVencer <= 15: retornar "CONSUMIR PRONTO"
       // En otros casos: retornar "FRESCO"
   }
   
   public double calcularPerdidaPorVencimiento() {
       // TODO: Calcular pérdida económica por vencimiento
       // Si estaVencido(): retornar precioBase * cantidadStock
       // En otros casos: retornar 0.0
   }
   ```

#### **Clase de Prueba: `SistemaTienda`**

**Funcionalidades a implementar:**

1. **Crear inventario diverso:**
   ```java
   // Crear productos electrónicos
   ProductoElectronico laptop = new ProductoElectronico(...);
   ProductoElectronico celular = new ProductoElectronico(...);
   
   // Crear productos alimenticios
   ProductoAlimenticio leche = new ProductoAlimenticio(...);
   ProductoAlimenticio pan = new ProductoAlimenticio(...);
   ```
### 📋 Casos de Prueba Obligatorios

1. **Producto Electrónico:**

    - Laptop importada, 24 meses garantía, 110V
    - Precio base: $2,500,000
    - Stock: 5 unidades

2. **Producto Alimenticio:**

    - Leche refrigerada, 5 días para vencer
    - Precio base: $4,500
    - Stock: 20 unidades

3. **Operaciones a probar:**

    - Crear objetos de cada tipo por separado
    - Venta exitosa y fallida por falta de stock
    - Cálculo de precios usando métodos específicos de cada clase
    - Reabastecimiento de inventario
    - Verificación de compatibilidad de voltaje
    - Comparación entre precio base y precios específicos
    - Demostrar funcionalidades únicas de cada tipo


