# Guía del Estudiante - Programación Orientada a Objetos

## Sesión 02: Componentes de una clase en Java

**Curso:** Programación Orientada a Objetos  
**Tema:** atributos/campos, variables locales, tipos de datos, miembros de clase e instancia, constructores, métodos de clase e instancia, métodos `void` y métodos con retorno  
**Práctica:** construcción progresiva de una clase `Producto`  
**Duración sugerida:** 180 minutos  
**Modalidad:** laboratorio guiado  
**Fecha de actualización técnica:** 09/09/2026

---

## 1. Propósito de la sesión

En esta práctica construirás, ejecutarás y modificarás ejemplos Java que muestran cómo se organiza una clase y cómo se comportan sus componentes. Al finalizar podrás diferenciar datos que pertenecen a cada objeto de datos compartidos por la clase, reconocer el alcance de una variable local, crear objetos mediante un constructor y decidir cuándo un método debe realizar una acción sin devolver valor o cuándo debe calcular y retornar un resultado.

El objetivo no es memorizar palabras reservadas. La meta es que puedas mirar una clase Java y explicar **qué pertenece al objeto, qué pertenece a la clase, qué existe solo dentro de un método y cómo se conectan constructor, atributos y métodos cuando el programa se ejecuta**.

## 2. Resultado observable

Al finalizar la sesión podrás:

- identificar campos de instancia, campos `static` y variables locales;
- seleccionar un tipo de dato coherente para cada valor del ejemplo;
- crear objetos usando `new` y un constructor;
- invocar métodos de instancia mediante un objeto;
- invocar métodos `static` mediante el nombre de la clase;
- diferenciar un método `void` de un método que retorna un valor;
- interpretar errores básicos de alcance y de contexto `static`;
- ejecutar una clase Java y comprobar el resultado en consola.

## 3. Herramientas recomendadas para esta práctica

### Java Development Kit

**Recomendación:** Eclipse Temurin JDK 25 LTS, usando la actualización 25.x disponible más reciente. Al 09/09/2026, Adoptium anunció Temurin 25.0.4.1 y mantiene Java 25 como línea LTS.

**Por qué usar una versión LTS:** esta sesión trabaja sintaxis fundamental de Java. Una versión LTS ofrece estabilidad y soporte prolongado sin obligarnos a introducir características experimentales que no forman parte del objetivo académico.

**Sitio oficial:** https://adoptium.net/temurin/releases/

**Instalación en Windows mediante Winget (opcional):**

```powershell
winget install EclipseAdoptium.Temurin.25.JDK
```

También puedes instalar el JDK desde IntelliJ IDEA usando **Download JDK** al crear o configurar el proyecto.

### IDE recomendado

**IntelliJ IDEA 2026.2.2** o una actualización compatible posterior de la misma línea estable.

**Sitio oficial:** https://www.jetbrains.com/idea/download/

Para esta sesión basta con crear un proyecto Java simple. No necesitamos Maven, Gradle, Spring, bases de datos ni librerías externas.

### Alternativa mínima

Puedes utilizar un editor de texto y las herramientas `javac` y `java` incluidas en el JDK. La práctica no depende de un IDE específico.

## 4. Precisión técnica importante antes de comenzar

En esta sesión utilizaremos algunos términos de la presentación y, a la vez, la terminología habitual de Java:

| En la sesión | Terminología Java más precisa | Qué significa |
|---|---|---|
| atributo global | campo (`field`) | variable declarada en el cuerpo de la clase, fuera de métodos |
| atributo de instancia | campo/variable de instancia | existe una copia por cada objeto |
| atributo de clase | campo/variable `static` | existe una sola variable asociada a la clase |
| atributo local | variable local | se declara dentro de un método o bloque y solo vive dentro de su alcance |

Además, recuerda estas correcciones técnicas:

- Java tiene **ocho tipos primitivos**: `byte`, `short`, `int`, `long`, `float`, `double`, `char` y `boolean`.
- No existe un tipo primitivo llamado `decimal` en Java; el tipo decimal de punto flotante de doble precisión es `double`.
- `String` es una clase, no un tipo primitivo.
- `byte`, `short`, `int` y `long` son enteros con signo. Java no define una variante sin signo general de esos tipos para declarar variables ordinarias.
- El lenguaje Java no fija un tamaño de almacenamiento en bytes para `boolean`; lo que sí define son sus dos valores: `true` y `false`.

## 5. Mapa de la práctica

```text
CLASE Producto
   |
   +--> campos de instancia
   |      nombre, precio, stock
   |
   +--> campo de clase
   |      static cantidadProductosRegistrados
   |
   +--> constructor
   |      Producto(...)
   |
   +--> métodos de instancia
   |      mostrarProducto()
   |      precioConDescuento(...)
   |
   +--> método de clase
          static mostrarDisponibilidad()

DENTRO DE UN MÉTODO
   |
   +--> variables locales
          nuevoStock, descuento
```

---

# Ejemplo 1. Campo de instancia vs. variable local

## 1. ¿Qué aprenderemos con este ejemplo?

Aprenderás por qué una variable declarada dentro de un método no puede utilizarse desde otro método, aunque ambos métodos pertenezcan a la misma clase.

## 2. Problema o situación

Un producto tiene un nombre y un stock. Queremos validar si una cantidad solicitada puede descontarse del stock. Para hacer el cálculo necesitamos una variable temporal llamada `nuevoStock`. Ese valor solo es útil mientras se ejecuta la validación.

## 3. Concepto que necesitamos

- `nombre` y `stock` serán campos de instancia: pertenecen al objeto.
- `nuevoStock` será variable local: se crea cuando entra al método y deja de estar disponible al salir de él.

## 4. Antes de comenzar

Crea un proyecto Java simple y dentro de `src` crea el archivo:

```text
ProductoAlcance.java
```

## 5. Estado inicial

No necesitas otros archivos. Copia el siguiente código completo:

```java
public class ProductoAlcance {
    String nombre = "Leche deslactosada";
    int stock = 10;

    public boolean validarStock(int cantidadSolicitada) {
        int nuevoStock = stock - cantidadSolicitada;
        return nuevoStock >= 0;
    }

    public void mostrarProducto() {
        System.out.println("Producto: " + nombre);
        System.out.println("Stock actual: " + stock);
        // System.out.println(nuevoStock); // ERROR CONTROLADO
    }

    public static void main(String[] args) {
        ProductoAlcance producto = new ProductoAlcance();
        producto.mostrarProducto();
        System.out.println("¿Puede vender 4 unidades? " + producto.validarStock(4));
    }
}
```

## 6. Paso 1 - Identifica qué está fuera y qué está dentro del método

**Qué hacemos:** observa la posición de `nombre`, `stock` y `nuevoStock`.

**Por qué lo hacemos:** el lugar donde una variable se declara determina su alcance.

**Qué significa cada parte importante:**

- `String nombre` está dentro de la clase y fuera de métodos: es un campo de instancia.
- `int stock` también es un campo de instancia.
- `int nuevoStock` está dentro de `validarStock(...)`: es local a ese método.

## 7. Paso 2 - Ejecuta el caso correcto

Ejecuta `ProductoAlcance.main()`.

**Resultado esperado:**

```text
Producto: Leche deslactosada
Stock actual: 10
¿Puede vender 4 unidades? true
```

**Cómo interpretarlo:** `validarStock(4)` calcula `10 - 4 = 6`. Como el resultado no es negativo, retorna `true`.

## 8. Paso 3 - Predice antes de modificar

Antes de cambiar nada responde:

1. ¿Qué ocurrirá con `validarStock(12)`?
2. ¿Se modifica realmente el campo `stock`?
3. ¿Por qué `nuevoStock` no necesita conservarse después del método?

Ahora cambia:

```java
producto.validarStock(4)
```

por:

```java
producto.validarStock(12)
```

**Resultado esperado:** `false`.

## 9. Error controlado

Descomenta temporalmente:

```java
System.out.println(nuevoStock);
```

Intenta compilar.

**Qué debe ocurrir:** el compilador indicará que `nuevoStock` no puede resolverse desde `mostrarProducto()` porque esa variable fue declarada dentro de otro método.

**Corrección:** vuelve a comentar la línea. No conviertas automáticamente `nuevoStock` en campo; primero pregúntate si el valor realmente necesita existir fuera de `validarStock()`.

## 10. Idea clave

Un campo describe estado que debe pertenecer al objeto o a la clase. Una variable local sirve para cálculos temporales dentro de un método o bloque.

---

# Ejemplo 2. Tipos de datos de una clase

## 1. ¿Qué aprenderemos con este ejemplo?

Reconocerás los tipos primitivos de Java y la diferencia entre un valor primitivo y un `String`.

## 2. Problema o situación

Queremos representar diferentes datos de un producto sin usar un único tipo para todo.

## 3. Archivo

Crea:

```text
ProductoTipos.java
```

## 4. Código completo

```java
public class ProductoTipos {
    byte pasillo = 7;
    short unidadesPorLote = 1200;
    int stock = 50000;
    long codigoInterno = 10000000001L;
    float tasaImpuesto = 0.18F;
    double precio = 19.90;
    char categoria = 'A';
    boolean disponible = true;
    String nombre = "Aceite de oliva";

    public static void main(String[] args) {
        ProductoTipos producto = new ProductoTipos();

        System.out.println(producto.nombre);
        System.out.println("Precio: " + producto.precio);
        System.out.println("Disponible: " + producto.disponible);
        System.out.println("Categoría: " + producto.categoria);
    }
}
```

## 5. ¿Por qué cada literal se escribe así?

| Código | Interpretación |
|---|---|
| `7` | entero pequeño asignado a `byte` |
| `1200` | entero dentro del rango de `short` |
| `50000` | entero de uso general (`int`) |
| `10000000001L` | literal `long`; la `L` evita tratarlo como `int` |
| `0.18F` | literal `float`; la `F` indica precisión simple |
| `19.90` | literal decimal que por defecto es `double` |
| `'A'` | un solo carácter, entre comillas simples |
| `true` | valor lógico |
| `"Aceite de oliva"` | objeto `String`, entre comillas dobles |

## 6. Tabla de referencia mínima

| Tipo | Naturaleza | Tamaño definido por Java | Rango/uso básico |
|---|---|---:|---|
| `byte` | entero con signo | 8 bits | -128 a 127 |
| `short` | entero con signo | 16 bits | -32768 a 32767 |
| `int` | entero con signo | 32 bits | -2^31 a 2^31-1 |
| `long` | entero con signo | 64 bits | -2^63 a 2^63-1 |
| `float` | punto flotante | 32 bits | precisión simple IEEE 754 |
| `double` | punto flotante | 64 bits | precisión doble IEEE 754 |
| `char` | carácter/unidad UTF-16 | 16 bits | 0 a 65535 |
| `boolean` | lógico | no fijado en bytes por el lenguaje | `true` / `false` |

## 7. Modificación controlada

Cambia:

```java
float tasaImpuesto = 0.18F;
```

por:

```java
float tasaImpuesto = 0.18;
```

**Antes de compilar:** predice si funcionará.

**Qué ocurre:** `0.18` es un literal `double`. Java no permite asignarlo directamente a `float` sin una conversión explícita; por eso usamos `0.18F` en este ejemplo.

Vuelve a dejar el código correcto.

## 8. Idea clave

El tipo de una variable no es un adorno: determina qué clase de valores puede almacenar y cómo los interpreta Java.

---

# Ejemplo 3. Atributo/campo de clase vs. atributo/campo de instancia

## 1. ¿Qué aprenderemos con este ejemplo?

Comprobarás que un campo de instancia tiene una copia por objeto y que un campo `static` se comparte a nivel de clase.

## 2. Archivo

Crea:

```text
ProductoClaseInstancia.java
```

## 3. Código

```java
public class ProductoClaseInstancia {
    static int cantidadProductosRegistrados = 0;

    String nombre;

    public static void main(String[] args) {
        ProductoClaseInstancia producto1 = new ProductoClaseInstancia();
        ProductoClaseInstancia producto2 = new ProductoClaseInstancia();

        producto1.nombre = "Leche deslactosada";
        producto2.nombre = "Aceite de oliva";
        ProductoClaseInstancia.cantidadProductosRegistrados = 2;

        System.out.println("Producto 1: " + producto1.nombre);
        System.out.println("Producto 2: " + producto2.nombre);
        System.out.println("Cantidad compartida: "
                + ProductoClaseInstancia.cantidadProductosRegistrados);
    }
}
```

## 4. Flujo conceptual

```text
ProductoClaseInstancia (CLASE)
       |
       +--> static cantidadProductosRegistrados = 2
       |
       +--> objeto producto1 -> nombre = "Leche deslactosada"
       |
       +--> objeto producto2 -> nombre = "Aceite de oliva"
```

## 5. Ejecución

**Resultado esperado:**

```text
Producto 1: Leche deslactosada
Producto 2: Aceite de oliva
Cantidad compartida: 2
```

## 6. Modificación con predicción

Cambia solo:

```java
producto1.nombre = "Arroz integral";
```

Pregunta: ¿debería cambiar `producto2.nombre`?

La respuesta correcta es **no**, porque `nombre` es de instancia.

Ahora cambia:

```java
ProductoClaseInstancia.cantidadProductosRegistrados = 5;
```

La cantidad será la misma sin importar desde qué parte del programa consultes ese campo de clase.

## 7. Buena forma de invocar un miembro `static`

Prefiere:

```java
ProductoClaseInstancia.cantidadProductosRegistrados
```

porque comunica que el dato pertenece a la clase. Java permite ciertas referencias estáticas mediante una instancia, pero hacerlo puede confundir al lector.

## 8. Idea clave

`static` cambia **a quién pertenece el miembro**: ya no pertenece a cada objeto por separado, sino a la clase.

---

# Ejemplo 4. Constructor y creación de objetos con `new`

## 1. ¿Qué aprenderemos con este ejemplo?

Construirás objetos con un estado inicial coherente y observarás cómo los parámetros del constructor alimentan los campos de instancia.

## 2. Archivo

Crea:

```text
ProductoConstructor.java
```

## 3. Código

```java
public class ProductoConstructor {
    String nombre;
    String presentacion;
    double precio;

    public ProductoConstructor(String nombre, String presentacion, double precio) {
        this.nombre = nombre;
        this.presentacion = presentacion;
        this.precio = precio;
    }

    public static void main(String[] args) {
        ProductoConstructor producto = new ProductoConstructor(
                "Leche deslactosada",
                "Paquete x 6 bolsas",
                20.00
        );

        System.out.println("Producto: " + producto.nombre);
        System.out.println("Presentación: " + producto.presentacion);
        System.out.println("Precio: " + producto.precio);
    }
}
```

## 4. Qué ocurre al ejecutar `new`

```text
new ProductoConstructor(...)
          |
          v
se crea una instancia
          |
          v
se ejecuta ProductoConstructor(...)
          |
          v
this.nombre       <- parámetro nombre
this.presentacion <- parámetro presentacion
this.precio       <- parámetro precio
          |
          v
la referencia se asigna a producto
```

## 5. ¿Por qué se usa `this`?

Dentro del constructor existen parámetros llamados `nombre`, `presentacion` y `precio`. Los campos tienen los mismos nombres. `this.nombre` significa **el campo `nombre` del objeto que se está construyendo**, mientras que `nombre` sin `this` representa el parámetro recibido.

## 6. Punto de control

Responde antes de continuar:

1. ¿El constructor tiene tipo de retorno?  
2. ¿Se escribe `void ProductoConstructor(...)`?  
3. ¿Qué palabra inicia la creación del objeto?  
4. ¿Qué pasa si cambias `20.00` por `24.50`?

El constructor no lleva tipo de retorno ni `void`. Se invoca como parte de una expresión con `new`.

## 7. Idea clave

El constructor define cómo empieza la vida de una instancia. Su nombre coincide con la clase y su función es inicializar el nuevo objeto.

---

# Ejemplo 5. Método de instancia vs. método de clase

## 1. ¿Qué aprenderemos con este ejemplo?

Diferenciarás un método que necesita un objeto específico de un método `static` que puede invocarse directamente mediante la clase.

## 2. Archivo

Crea:

```text
ProductoMetodos.java
```

## 3. Código

```java
public class ProductoMetodos {
    String nombre;
    String presentacion;
    double precio;

    static boolean disponible = true;

    public ProductoMetodos(String nombre, String presentacion, double precio) {
        this.nombre = nombre;
        this.presentacion = presentacion;
        this.precio = precio;
    }

    public void mostrarProducto() {
        System.out.println(nombre + " - " + presentacion + " - " + precio);
    }

    public static void mostrarDisponibilidad() {
        System.out.println("Disponible: " + disponible);
    }

    public static void main(String[] args) {
        ProductoMetodos producto = new ProductoMetodos(
                "Leche deslactosada",
                "Paquete x 6 bolsas",
                20.00
        );

        producto.mostrarProducto();
        ProductoMetodos.mostrarDisponibilidad();
    }
}
```

## 4. Lectura guiada

### Método de instancia

```java
producto.mostrarProducto();
```

Necesitamos `producto` porque `mostrarProducto()` utiliza `nombre`, `presentacion` y `precio`, que son datos del objeto.

### Método de clase

```java
ProductoMetodos.mostrarDisponibilidad();
```

No necesitamos crear un objeto para consultar `disponible`, porque ese campo también es `static`.

## 5. Error controlado de contexto `static`

Dentro de `mostrarDisponibilidad()` agrega temporalmente:

```java
System.out.println(nombre);
```

Intenta compilar.

**Qué debe ocurrir:** un método `static` no tiene una instancia actual de `ProductoMetodos`; por eso no puede acceder directamente al campo de instancia `nombre`.

Elimina esa línea y vuelve a compilar.

## 6. Idea clave

Un método de instancia trabaja respecto de un objeto concreto. Un método de clase (`static`) trabaja en contexto de clase y accede directamente a miembros estáticos, no a miembros de instancia sin una referencia de objeto.

---

# Ejemplo 6. Método `void` vs. método con retorno

## 1. ¿Qué aprenderemos con este ejemplo?

Compararás una acción que imprime información con un cálculo que devuelve un valor utilizable por otra parte del programa.

## 2. Archivo

Crea:

```text
ProductoRetorno.java
```

## 3. Código

```java
public class ProductoRetorno {
    String nombre;
    double precio;

    public ProductoRetorno(String nombre, double precio) {
        this.nombre = nombre;
        this.precio = precio;
    }

    public void mostrarProducto() {
        System.out.println("Producto: " + nombre + " - Precio: " + precio);
    }

    public double precioConDescuento(double porcentaje) {
        double descuento = precio * porcentaje / 100.0;
        return precio - descuento;
    }

    public static void main(String[] args) {
        ProductoRetorno producto = new ProductoRetorno("Agua gasificada", 3.50);

        producto.mostrarProducto();

        double precioFinal = producto.precioConDescuento(10);
        System.out.println("Precio con descuento: " + precioFinal);
    }
}
```

## 4. Comparación

| Método | Declaración | Qué hace | Qué recibe el llamador |
|---|---|---|---|
| acción sin retorno | `void mostrarProducto()` | imprime datos | ningún valor |
| cálculo con retorno | `double precioConDescuento(...)` | calcula un precio | un `double` |

## 5. ¿Por qué guardamos el resultado?

```java
double precioFinal = producto.precioConDescuento(10);
```

El método no solo hace algo; **produce un dato**. Ese dato puede almacenarse, imprimirse o usarse después.

## 6. Predicción

Antes de ejecutar cambia el descuento de `10` a `20` y calcula manualmente el resultado.

Para `3.50`:

```text
descuento = 3.50 * 20 / 100 = 0.70
precio final = 3.50 - 0.70 = 2.80
```

Comprueba después en consola.

## 7. Idea clave

Usa `void` cuando el propósito del método sea realizar una acción sin entregar un resultado al llamador. Usa un tipo de retorno cuando el método debe producir un valor que otra parte del programa necesita.

---

# Ejemplo 7. Integrador - Clase `Producto`

## 1. Objetivo

Integrar en una sola clase los componentes trabajados: campos de instancia, campo de clase, variable local, constructor, método de instancia, método `static`, método `void` y método con retorno.

## 2. Archivo

Crea:

```text
Producto.java
```

## 3. Código completo

```java
public class Producto {
    static int cantidadProductosRegistrados = 0;
    static boolean disponible = true;

    String nombre;
    String presentacion;
    double precio;
    int stock;

    public Producto(String nombre, String presentacion, double precio, int stock) {
        this.nombre = nombre;
        this.presentacion = presentacion;
        this.precio = precio;
        this.stock = stock;
        cantidadProductosRegistrados++;
    }

    public void mostrarProducto() {
        System.out.println(nombre + " - " + presentacion);
        System.out.println("Precio: " + precio + " | Stock: " + stock);
    }

    public boolean validarStock(int cantidadSolicitada) {
        int nuevoStock = stock - cantidadSolicitada;
        return nuevoStock >= 0;
    }

    public double precioConDescuento(double porcentaje) {
        double descuento = precio * porcentaje / 100.0;
        return precio - descuento;
    }

    public static void mostrarDisponibilidad() {
        System.out.println("Disponibilidad general: " + disponible);
    }

    public static void main(String[] args) {
        Producto producto1 = new Producto(
                "Leche deslactosada",
                "Paquete x 6 bolsas",
                20.00,
                10
        );

        Producto producto2 = new Producto(
                "Aceite de oliva",
                "Botella 500 ml",
                28.50,
                5
        );

        producto1.mostrarProducto();
        System.out.println("¿Stock suficiente para 4? " + producto1.validarStock(4));
        System.out.println("Precio con 10%: " + producto1.precioConDescuento(10));

        System.out.println();

        producto2.mostrarProducto();
        System.out.println("¿Stock suficiente para 8? " + producto2.validarStock(8));
        System.out.println("Precio con 15%: " + producto2.precioConDescuento(15));

        System.out.println();
        System.out.println("Registrados: " + Producto.cantidadProductosRegistrados);
        Producto.mostrarDisponibilidad();
    }
}
```

## 4. Antes de ejecutar, predice

Completa mentalmente:

1. `cantidadProductosRegistrados` después de crear `producto1`: ______  
2. después de crear `producto2`: ______  
3. `producto1.validarStock(4)`: ______  
4. `producto2.validarStock(8)`: ______  
5. precio de `producto1` con 10% de descuento: ______

## 5. Resultado esperado aproximado

```text
Leche deslactosada - Paquete x 6 bolsas
Precio: 20.0 | Stock: 10
¿Stock suficiente para 4? true
Precio con 10%: 18.0

Aceite de oliva - Botella 500 ml
Precio: 28.5 | Stock: 5
¿Stock suficiente para 8? false
Precio con 15%: 24.225

Registrados: 2
Disponibilidad general: true
```

## 6. Lectura causa -> efecto

```text
new Producto(...)
     ↓
ejecuta constructor
     ↓
inicializa campos del objeto
     ↓
incrementa campo static compartido
     ↓
el objeto puede invocar métodos de instancia
     ↓
los métodos pueden usar variables locales temporales
     ↓
los métodos con retorno entregan un valor al llamador
```

## 7. Modificación controlada

Realiza tres cambios, uno por uno:

1. cambia `stock` de `producto2` de `5` a `12`;
2. cambia el descuento de `15` a `20`;
3. cambia `Producto.disponible = false;` antes de llamar a `mostrarDisponibilidad()`.

Después de cada cambio:

- predice el resultado;
- ejecuta;
- compara;
- explica qué miembro cambió: ¿instancia o clase?

---

# Actividades espejo

## Actividad 1 - Identificación

En el integrador clasifica cada identificador:

| Identificador | Campo de instancia | Campo de clase | Variable local | Parámetro |
|---|:---:|:---:|:---:|:---:|
| `nombre` | | | | |
| `cantidadProductosRegistrados` | | | | |
| `cantidadSolicitada` | | | | |
| `nuevoStock` | | | | |
| `descuento` | | | | |

## Actividad 2 - Método correcto

Indica cuál llamada es coherente y explica por qué:

```java
producto1.mostrarProducto();
Producto.mostrarDisponibilidad();
```

Luego responde por qué sería menos claro escribir una llamada estática mediante una instancia.

## Actividad 3 - Diseña una modificación

Agrega un campo de instancia `String categoria` y haz que el constructor lo reciba. No agregues nuevos conceptos: limita el cambio a campo, parámetro, asignación del constructor y visualización.

## Actividad 4 - Nuevo método de retorno

Crea dentro de `Producto`:

```java
public double calcularValorStock() {
    return precio * stock;
}
```

Antes de ejecutar predice el resultado para cada producto.

---

# Tabla de errores frecuentes

| Síntoma | Causa probable | Cómo verificar | Corrección |
|---|---|---|---|
| `cannot find symbol` con variable local | se intenta usar fuera de su alcance | revisa dónde fue declarada | úsala dentro del método o devuelve el valor si realmente se necesita fuera |
| error al usar campo de instancia desde método `static` | falta un objeto actual | identifica si el miembro tiene `static` | usa una instancia o mantén el método en contexto de instancia |
| error al asignar decimal a `float` | el literal decimal es `double` por defecto | observa si falta `F` | usa `0.18F` si realmente necesitas `float` |
| constructor no reconocido | nombre diferente al de la clase o firma distinta | compara nombre y argumentos | iguala nombre de constructor y argumentos de `new` |
| se espera valor y el método es `void` | el método no retorna nada | mira el tipo antes del nombre | no lo asignes o cambia el diseño si el propósito real es devolver un dato |
| método con tipo de retorno no retorna valor | falta `return` compatible | revisa todos los caminos relevantes | retorna un valor del tipo declarado |

---

# Preguntas de comprobación

1. ¿Qué diferencia existe entre una variable local y un campo de instancia?
2. ¿Qué palabra identifica un miembro de clase?
3. ¿Por qué `String` no aparece entre los ocho tipos primitivos?
4. ¿Qué función cumple un constructor?
5. ¿Por qué un constructor no se declara con `void`?
6. ¿Cómo invocas un método de instancia?
7. ¿Cómo conviene invocar un método `static`?
8. ¿Qué diferencia funcional existe entre `void` y `double` como tipo de retorno?
9. ¿Qué ocurre con una variable local cuando finaliza el método?
10. ¿Qué valor comparte `cantidadProductosRegistrados` entre los objetos?

# Evidencias sugeridas

Entrega o conserva como evidencia:

- los siete archivos `.java` ejecutables;
- una captura de la salida del ejemplo integrador;
- una captura del error controlado de alcance o de contexto `static`;
- respuestas breves a las preguntas de comprobación;
- la modificación final de `Producto` con el campo `categoria`.

# Checklist final

- [ ] Tengo un JDK instalado y `java -version` funciona.
- [ ] Distingo campo de instancia, campo `static` y variable local.
- [ ] Sé que `double`, no `decimal`, es tipo primitivo Java.
- [ ] Sé que `String` es una clase.
- [ ] Puedo crear un objeto con `new`.
- [ ] Puedo explicar qué hace el constructor.
- [ ] Puedo diferenciar método de instancia y método de clase.
- [ ] Puedo diferenciar `void` y un método con retorno.
- [ ] Puedo interpretar un error de alcance.
- [ ] Ejecuté el integrador y comparé la salida con mi predicción.

# Mapa final de la sesión

```text
CLASE
 |
 +-- campos
 |    +-- instancia -> una copia por objeto
 |    +-- static    -> una copia por clase
 |
 +-- constructor -> inicializa nuevas instancias
 |
 +-- métodos
      +-- instancia -> requieren objeto
      +-- static    -> contexto de clase
      +-- void      -> acción sin valor de retorno
      +-- no void   -> retorna un valor

MÉTODO / BLOQUE
 |
 +-- variables locales -> alcance temporal
```

# Cierre

En esta sesión aprendiste a leer una clase Java como una estructura coherente: **los campos almacenan estado, el constructor crea el estado inicial, los métodos expresan comportamiento y el alcance determina dónde existe cada variable**. También comprobaste que `static` separa aquello que pertenece a la clase de aquello que pertenece a cada objeto.

Repasa especialmente los dos errores controlados: variable local fuera de alcance y acceso directo a un campo de instancia desde un método `static`. Son errores muy útiles porque revelan si realmente entendiste el contexto de ejecución.

Como siguiente paso, conserva el ejemplo integrador y úsalo como base para continuar trabajando con clases y objetos.

**Blog:** https://lideratecacademy.com/  
**Canal YouTube:** https://www.youtube.com/@LideratecAcademy

## Recursos oficiales

- Java SE Support Roadmap: https://www.oracle.com/java/technologies/java-se-support-roadmap.html
- Java Language Specification SE 25 - Classes: https://docs.oracle.com/javase/specs/jls/se25/html/jls-8.html
- Java Language Specification SE 25 - Types: https://docs.oracle.com/javase/specs/jls/se25/html/jls-4.html
- Eclipse Temurin: https://adoptium.net/temurin/releases/
- Instalación Temurin: https://adoptium.net/installation
- IntelliJ IDEA: https://www.jetbrains.com/idea/download/
- Configurar JDK en IntelliJ IDEA: https://www.jetbrains.com/help/idea/sdk.html
