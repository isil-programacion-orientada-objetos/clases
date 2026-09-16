---
course_id: POO-JAVA-ISIL
session_id: S03
module_id: TEMA-03
course_version: provisional
source_origin: PPT
status: validated
---

# Guía del Estudiante - FASE 13
## Programación Orientada a Objetos - Tema 03: Constructores y métodos

## 1. Propósito de la sesión

En esta clase-laboratorio construirás clases Java desde archivos vacíos para observar cómo cambia la creación e inicialización de objetos según el constructor disponible y cómo elegir entre métodos de instancia, métodos de clase (`static`), métodos `void` y métodos que devuelven un valor. El objetivo no es memorizar sintaxis aislada: cada ejemplo termina con una predicción, una ejecución, una interpretación, una variación y una tarea espejo.

**Producto observable:** ocho mini-laboratorios ejecutables (`EJ01` a `EJ08`) y ocho tareas espejo (`T01` a `T08`) que terminan en un caso integrador.

## 2. Resultado observable

### A. Lectura sugerida del docente

Al finalizar la sesión podrás mirar una necesidad de programación y decidir qué mecanismo de la clase corresponde. Si el objeto necesita nacer con un estado determinado, podrás escoger entre un constructor sin argumentos, parametrizado o de copia. Si una operación necesita datos propios de un objeto, reconocerás que debe invocarse desde una instancia; si la operación no depende del estado de un objeto concreto, podrás justificar un método de clase. También distinguirás entre una acción que termina sin devolver un dato y una operación cuyo resultado debe regresar al código que la llamó. La evidencia de dominio no será únicamente que el programa compile: deberás poder anticipar la salida, explicar por qué ocurre, modificar el ejemplo sin romper su intención y resolver una variante con otra clase.

### B. Desempeños observables

- Crear objetos mediante `new`.
- Diferenciar constructor por defecto y constructor escrito explícitamente.
- Implementar constructor sin argumentos, parametrizado y de copia.
- Invocar correctamente métodos de instancia y métodos `static`.
- Usar `void` cuando la operación es una acción sin valor de retorno.
- Usar un tipo de retorno y `return` cuando el resultado debe reutilizarse.
- Predecir, ejecutar, interpretar y corregir errores sencillos de estos conceptos.

### C. Criterio de dominio

Dominas la sesión cuando puedes resolver `T08` sin copiar el integrador de `Producto` y puedes justificar verbalmente cada uso de `new`, `static`, `void` y `return`.

## 3. Antes de iniciar

### Debe saber

- Qué es una clase y qué es un objeto.
- Cómo declarar atributos simples en Java.
- Cómo escribir un método `main`.
- Cómo compilar y ejecutar un programa Java básico o seguir una guía para hacerlo.

### Debe tener disponible

- JDK instalado y el comando `java`/`javac` accesible.
- Un editor o IDE. Para una instalación nueva se recomienda JDK 25 LTS e IntelliJ IDEA estable actual.
- Permiso para crear carpetas y archivos en una ubicación de trabajo.

### No se asumirá todavía

Esta guía no necesita herencia, polimorfismo, interfaces, colecciones, excepciones, persistencia, frameworks ni patrones de diseño.

## 4. Herramientas y recursos

### JDK

**Qué es:** el kit de desarrollo que contiene el compilador y la máquina virtual necesaria para trabajar con Java.

**Recomendación de instalación nueva:** JDK 25 LTS. La sesión utiliza sintaxis básica compatible con versiones LTS anteriores, por lo que si tu institución ya definió JDK 21 no necesitas cambiarlo solo para esta práctica.

**Sitio oficial:** https://www.oracle.com/java/technologies/downloads/

**Validación:** abre una terminal y ejecuta:

```bash
java -version
javac -version
```

Si ambos comandos muestran una versión, el entorno está disponible.

### IntelliJ IDEA

**Qué es:** un IDE orientado al desarrollo Java.

**Recomendación:** versión estable actual de IntelliJ IDEA; las funciones principales de Java están disponibles gratuitamente.

**Sitio oficial:** https://www.jetbrains.com/idea/download/

**Qué necesitas para esta sesión:** crear un proyecto Java sencillo, crear archivos `.java`, ejecutar `Main` y leer la consola. No necesitas herramientas Ultimate específicas, servidor, base de datos ni framework.

## 5. Preparación del entorno desde cero

### Ruta A - Ya tienes Java

1. Abre una terminal.
2. Ejecuta `java -version`.
3. Ejecuta `javac -version`.
4. Crea una carpeta de trabajo llamada `POO_S03`.
5. Dentro de ella crearás una carpeta independiente por ejemplo (`EJ01`, `EJ02`, etc.).
6. En cada carpeta habrá, como máximo, `Producto.java` y `Main.java`.

### Ruta B - Equipo sin preparar

1. Descarga un JDK 25 LTS desde el sitio oficial o utiliza la distribución aprobada por tu institución.
2. Instálalo siguiendo el instalador de tu sistema operativo.
3. Cierra y vuelve a abrir la terminal.
4. Comprueba `java -version` y `javac -version`.
5. Instala IntelliJ IDEA desde el sitio oficial si deseas trabajar con IDE.
6. Crea un proyecto Java sin framework y selecciona el JDK instalado.
7. Crea una clase `Main` y ejecuta un `System.out.println("Entorno listo");`.
8. Si ves `Entorno listo` en consola, continúa con EJ01.

### Ejecución por terminal usada en la guía

En la carpeta de cada ejemplo:

```bash
javac Producto.java Main.java
java Main
```

En las tareas espejo se sustituye `Producto.java` por `Libro.java`.


---

# EJ01 - Constructor por defecto: observar qué ocurre al crear un objeto

## Qué vamos a construir

Un programa mínimo con `Producto.java` y `Main.java` para practicar **Constructor por defecto + palabra reservada new**.

## Qué aprenderás aquí

Crear una instancia sin constructor explícito y reconocer los valores predeterminados de sus atributos.

## Archivos que vamos a crear o modificar

- `Producto.java`
- `Main.java`

## Punto de partida

Crea una carpeta `EJ01` dentro de `POO_S03`. Comienza con los dos archivos vacíos indicados. No reutilices el archivo final del ejemplo anterior: queremos observar qué aporta exactamente esta habilidad.

## Paso 1 - Crear la clase Producto

Abre `Producto.java` y escribe el estado final de la clase para este ejemplo. Después lo leeremos por partes.

```java
public class Producto {
    String nombre;
    double precio;
    int stock;
}
```

### Qué significa

La clase solo declara atributos. Como no existe un constructor explícito, Java puede proporcionar el constructor por defecto que usaremos desde `Main`.

### Por qué lo hacemos ahora

Este ejemplo aísla **Constructor por defecto + palabra reservada new** para que puedas predecir su efecto antes de mezclarlo con los demás componentes de la clase.

## Paso 2 - Crear el punto de entrada

Abre `Main.java` y escribe:

```java
public class Main {
    public static void main(String[] args) {
        Producto producto = new Producto();

        System.out.println("nombre = " + producto.nombre);
        System.out.println("precio = " + producto.precio);
        System.out.println("stock = " + producto.stock);
    }
}
```

### Lectura pedagógica del código

La expresión `new Producto()` crea la instancia. Después leemos los atributos sin haberles asignado valores manualmente para observar la inicialización predeterminada.

## Flujo mental

`entrada -> operación -> cambio/resultado -> salida`

Java proporciona un constructor por defecto cuando la clase no declara ningún constructor. Al crear el objeto con `new Producto()`, los atributos de instancia quedan con sus valores predeterminados: `null` para referencias, `0.0` para `double` y `0` para `int`.

## Archivo completo al terminar este ejemplo

### Producto.java

```java
public class Producto {
    String nombre;
    double precio;
    int stock;
}
```

### Main.java

```java
public class Main {
    public static void main(String[] args) {
        Producto producto = new Producto();

        System.out.println("nombre = " + producto.nombre);
        System.out.println("precio = " + producto.precio);
        System.out.println("stock = " + producto.stock);
    }
}
```

## Antes de ejecutar: predicción

1. ¿Se puede crear el objeto aunque no hayas escrito un constructor?
2. ¿Qué valores tendrán nombre, precio y stock antes de asignarlos?

## Ejecuta

```bash
javac Producto.java Main.java
java Main
```

## Resultado esperado

```text
nombre = null
precio = 0.0
stock = 0
```

## Cómo interpretarlo

Java proporciona un constructor por defecto cuando la clase no declara ningún constructor. Al crear el objeto con `new Producto()`, los atributos de instancia quedan con sus valores predeterminados: `null` para referencias, `0.0` para `double` y `0` para `int`.

## Variación A

Después de crear el objeto, asigna `producto.nombre = "Teclado";` y vuelve a imprimir. Observa que la creación y la asignación son pasos distintos.

## Variación B

Crea un segundo objeto `Producto otro = new Producto();` y compara sus valores iniciales con los del primero.

## Error controlado

Escribe `Producto producto = Producto();` sin `new`. Java no interpreta el nombre de la clase como una función invocable.

## Por qué ocurre

La creación de una instancia requiere la expresión `new NombreClase(...)`. El constructor se invoca como parte de esa expresión.

## Corrección razonada

Restituye `Producto producto = new Producto();`.

## Qué debes poder explicar con tus palabras

- ¿Por qué el constructor por defecto no aparece escrito en la clase?
- ¿Qué papel cumple `new` en la creación del objeto?
- ¿Qué valores observaste antes de asignar datos?

## T01 - Tarea espejo: Observar el constructor por defecto en Libro

**Enunciado.** Observar el constructor por defecto en Libro. Trabaja con la clase `Libro` para transferir la habilidad del ejemplo sin copiar literalmente el caso `Producto`.

**Archivos a modificar:** `Libro.java` y `Main.java`.

**Restricción:** No declares un constructor explícito. El objetivo es observar el constructor por defecto que Java proporciona.

**Pista:** La creación debe usar `new Libro()` y luego acceder a los atributos desde la referencia creada.

**Evidencia que debes mostrar:** Captura o copia de la salida mostrando los tres valores predeterminados.

**Cómo saber si está correcta:** La salida debe mostrar `null`, `0.0` y `0` para título, precio y stock.


---

# EJ02 - Constructor sin argumentos: inicialización personalizada

## Qué vamos a construir

Un programa mínimo con `Producto.java` y `Main.java` para practicar **Constructor sin argumentos**.

## Qué aprenderás aquí

Definir explícitamente un constructor sin parámetros para establecer un estado inicial propio.

## Archivos que vamos a crear o modificar

- `Producto.java`
- `Main.java`

## Punto de partida

Crea una carpeta `EJ02` dentro de `POO_S03`. Comienza con los dos archivos vacíos indicados. No reutilices el archivo final del ejemplo anterior: queremos observar qué aporta exactamente esta habilidad.

## Paso 1 - Crear la clase Producto

Abre `Producto.java` y escribe el estado final de la clase para este ejemplo. Después lo leeremos por partes.

```java
public class Producto {
    String nombre;
    double precio;
    int stock;

    public Producto() {
        nombre = "Sin nombre";
        precio = 0.0;
        stock = 1;
    }
}
```

### Qué significa

La declaración `public Producto()` tiene el mismo nombre de la clase y no tiene tipo de retorno. Sus instrucciones establecen un estado inicial personalizado.

### Por qué lo hacemos ahora

Este ejemplo aísla **Constructor sin argumentos** para que puedas predecir su efecto antes de mezclarlo con los demás componentes de la clase.

## Paso 2 - Crear el punto de entrada

Abre `Main.java` y escribe:

```java
public class Main {
    public static void main(String[] args) {
        Producto producto = new Producto();

        System.out.println("nombre = " + producto.nombre);
        System.out.println("precio = " + producto.precio);
        System.out.println("stock = " + producto.stock);
    }
}
```

### Lectura pedagógica del código

La misma expresión `new Producto()` ahora invoca el constructor sin argumentos que escribiste. La diferencia se aprecia en los valores impresos.

## Flujo mental

`entrada -> operación -> cambio/resultado -> salida`

El constructor sigue sin recibir argumentos, pero ahora sí existe código de inicialización escrito por nosotros. Por eso el objeto nace con los valores definidos dentro de `Producto()`.

## Archivo completo al terminar este ejemplo

### Producto.java

```java
public class Producto {
    String nombre;
    double precio;
    int stock;

    public Producto() {
        nombre = "Sin nombre";
        precio = 0.0;
        stock = 1;
    }
}
```

### Main.java

```java
public class Main {
    public static void main(String[] args) {
        Producto producto = new Producto();

        System.out.println("nombre = " + producto.nombre);
        System.out.println("precio = " + producto.precio);
        System.out.println("stock = " + producto.stock);
    }
}
```

## Antes de ejecutar: predicción

1. ¿Seguirá apareciendo `null` en nombre?
2. ¿Qué valor tendrá stock inmediatamente después de `new Producto()`?

## Ejecuta

```bash
javac Producto.java Main.java
java Main
```

## Resultado esperado

```text
nombre = Sin nombre
precio = 0.0
stock = 1
```

## Cómo interpretarlo

El constructor sigue sin recibir argumentos, pero ahora sí existe código de inicialización escrito por nosotros. Por eso el objeto nace con los valores definidos dentro de `Producto()`.

## Variación A

Cambia el valor inicial de `stock` de `1` a `5` y predice la nueva salida.

## Variación B

Cambia `nombre` a `"Producto pendiente"` y verifica que cada nueva instancia usa ese estado inicial.

## Error controlado

Cambia la cabecera a `public void Producto()`. El programa compilará, pero esa declaración será un método ordinario, no un constructor; `new Producto()` usará nuevamente el constructor por defecto implícito.

## Por qué ocurre

Un constructor no declara tipo de retorno. Escribir `void` cambia la naturaleza de la declaración.

## Corrección razonada

Usa exactamente `public Producto()` sin `void` ni otro tipo de retorno.

## Qué debes poder explicar con tus palabras

- ¿Qué diferencia práctica observas entre el constructor por defecto y el constructor sin argumentos escrito por ti?
- ¿Por qué `void Producto()` no es un constructor?

## T02 - Tarea espejo: Inicializar Libro con un constructor sin argumentos

**Enunciado.** Inicializar Libro con un constructor sin argumentos. Trabaja con la clase `Libro` para transferir la habilidad del ejemplo sin copiar literalmente el caso `Producto`.

**Archivos a modificar:** `Libro.java` y `Main.java`.

**Restricción:** El constructor no debe recibir parámetros y no debe declarar `void`.

**Pista:** La cabecera comienza con `public Libro()`.

**Evidencia que debes mostrar:** Código del constructor y salida de una nueva instancia.

**Cómo saber si está correcta:** Al crear `new Libro()`, el título debe ser `Sin titulo` y el stock debe ser 1.


---

# EJ03 - Constructor parametrizado: crear objetos con datos específicos

## Qué vamos a construir

Un programa mínimo con `Producto.java` y `Main.java` para practicar **Constructor con argumentos / parametrizado**.

## Qué aprenderás aquí

Recibir valores al crear el objeto y utilizarlos para inicializar sus atributos.

## Archivos que vamos a crear o modificar

- `Producto.java`
- `Main.java`

## Punto de partida

Crea una carpeta `EJ03` dentro de `POO_S03`. Comienza con los dos archivos vacíos indicados. No reutilices el archivo final del ejemplo anterior: queremos observar qué aporta exactamente esta habilidad.

## Paso 1 - Crear la clase Producto

Abre `Producto.java` y escribe el estado final de la clase para este ejemplo. Después lo leeremos por partes.

```java
public class Producto {
    String nombre;
    double precio;
    int stock;

    public Producto(String nombreInicial, double precioInicial, int stockInicial) {
        nombre = nombreInicial;
        precio = precioInicial;
        stock = stockInicial;
    }
}
```

### Qué significa

El constructor recibe tres parámetros. Cada parámetro transporta un dato desde la llamada con `new` hacia los atributos del nuevo objeto.

### Por qué lo hacemos ahora

Este ejemplo aísla **Constructor con argumentos / parametrizado** para que puedas predecir su efecto antes de mezclarlo con los demás componentes de la clase.

## Paso 2 - Crear el punto de entrada

Abre `Main.java` y escribe:

```java
public class Main {
    public static void main(String[] args) {
        Producto producto = new Producto("Mouse", 79.90, 12);

        System.out.println("nombre = " + producto.nombre);
        System.out.println("precio = " + producto.precio);
        System.out.println("stock = " + producto.stock);
    }
}
```

### Lectura pedagógica del código

Los tres argumentos de `new Producto(...)` se conectan con los tres parámetros del constructor y construyen un objeto con datos específicos desde el inicio.

## Flujo mental

`entrada -> operación -> cambio/resultado -> salida`

Los argumentos de `new Producto("Mouse", 79.90, 12)` se entregan al constructor en el mismo orden de sus parámetros. El constructor usa esos valores para establecer el estado inicial del nuevo objeto.

## Archivo completo al terminar este ejemplo

### Producto.java

```java
public class Producto {
    String nombre;
    double precio;
    int stock;

    public Producto(String nombreInicial, double precioInicial, int stockInicial) {
        nombre = nombreInicial;
        precio = precioInicial;
        stock = stockInicial;
    }
}
```

### Main.java

```java
public class Main {
    public static void main(String[] args) {
        Producto producto = new Producto("Mouse", 79.90, 12);

        System.out.println("nombre = " + producto.nombre);
        System.out.println("precio = " + producto.precio);
        System.out.println("stock = " + producto.stock);
    }
}
```

## Antes de ejecutar: predicción

1. ¿Qué valores viajarán desde `new Producto(...)` hasta el constructor?
2. ¿Qué atributo recibe cada parámetro?

## Ejecuta

```bash
javac Producto.java Main.java
java Main
```

## Resultado esperado

```text
nombre = Mouse
precio = 79.9
stock = 12
```

## Cómo interpretarlo

Los argumentos de `new Producto("Mouse", 79.90, 12)` se entregan al constructor en el mismo orden de sus parámetros. El constructor usa esos valores para establecer el estado inicial del nuevo objeto.

## Variación A

Crea `Producto teclado = new Producto("Teclado", 120.0, 7);` e imprime sus datos.

## Variación B

Cambia solo el tercer argumento y observa que el resto del estado inicial permanece igual.

## Error controlado

Intenta `new Producto("Mouse", 79.90)` omitiendo `stockInicial`.

## Por qué ocurre

La llamada no coincide con la firma disponible: el constructor declarado requiere tres argumentos compatibles.

## Corrección razonada

Proporciona los tres argumentos en el orden esperado.

## Qué debes poder explicar con tus palabras

- ¿Qué relación existe entre los argumentos de `new` y los parámetros del constructor?
- ¿Por qué este constructor permite crear objetos con estados iniciales distintos?

## T03 - Tarea espejo: Crear Libro con un constructor parametrizado

**Enunciado.** Crear Libro con un constructor parametrizado. Trabaja con la clase `Libro` para transferir la habilidad del ejemplo sin copiar literalmente el caso `Producto`.

**Archivos a modificar:** `Libro.java` y `Main.java`.

**Restricción:** Los tres valores deben ingresar durante la creación del objeto, no mediante asignaciones posteriores en `Main`.

**Pista:** La firma necesita parámetros compatibles con `String`, `double` e `int`.

**Evidencia que debes mostrar:** Llamada a `new Libro(...)` y salida con los datos recibidos.

**Cómo saber si está correcta:** Los valores impresos deben coincidir con los argumentos usados al crear el objeto.


---

# EJ04 - Constructor de copia: crear una nueva instancia a partir de otra

## Qué vamos a construir

Un programa mínimo con `Producto.java` y `Main.java` para practicar **Constructor de copia**.

## Qué aprenderás aquí

Definir un constructor que reciba un objeto existente y copie sus atributos a una nueva instancia.

## Archivos que vamos a crear o modificar

- `Producto.java`
- `Main.java`

## Punto de partida

Crea una carpeta `EJ04` dentro de `POO_S03`. Comienza con los dos archivos vacíos indicados. No reutilices el archivo final del ejemplo anterior: queremos observar qué aporta exactamente esta habilidad.

## Paso 1 - Crear la clase Producto

Abre `Producto.java` y escribe el estado final de la clase para este ejemplo. Después lo leeremos por partes.

```java
public class Producto {
    String nombre;
    double precio;
    int stock;

    public Producto(String nombreInicial, double precioInicial, int stockInicial) {
        nombre = nombreInicial;
        precio = precioInicial;
        stock = stockInicial;
    }

    public Producto(Producto original) {
        nombre = original.nombre;
        precio = original.precio;
        stock = original.stock;
    }
}
```

### Qué significa

La clase conserva el constructor parametrizado y agrega otro constructor cuyo parámetro es un `Producto`. Dentro de él se copian los valores del objeto recibido.

### Por qué lo hacemos ahora

Este ejemplo aísla **Constructor de copia** para que puedas predecir su efecto antes de mezclarlo con los demás componentes de la clase.

## Paso 2 - Crear el punto de entrada

Abre `Main.java` y escribe:

```java
public class Main {
    public static void main(String[] args) {
        Producto original = new Producto("Monitor", 899.0, 4);
        Producto copia = new Producto(original);

        copia.nombre = "Monitor - copia";

        System.out.println("original = " + original.nombre);
        System.out.println("copia = " + copia.nombre);
        System.out.println("precio copia = " + copia.precio);
        System.out.println("stock copia = " + copia.stock);
    }
}
```

### Lectura pedagógica del código

Primero se crea `original`; luego `new Producto(original)` crea otra instancia usando el constructor de copia. Cambiamos solo el nombre de la copia para comprobar que es una instancia distinta.

## Flujo mental

`entrada -> operación -> cambio/resultado -> salida`

`new Producto(original)` invoca un constructor que crea otra instancia y copia los valores. Por eso podemos modificar el atributo `nombre` de la nueva instancia sin cambiar el valor mostrado por el objeto original.

## Archivo completo al terminar este ejemplo

### Producto.java

```java
public class Producto {
    String nombre;
    double precio;
    int stock;

    public Producto(String nombreInicial, double precioInicial, int stockInicial) {
        nombre = nombreInicial;
        precio = precioInicial;
        stock = stockInicial;
    }

    public Producto(Producto original) {
        nombre = original.nombre;
        precio = original.precio;
        stock = original.stock;
    }
}
```

### Main.java

```java
public class Main {
    public static void main(String[] args) {
        Producto original = new Producto("Monitor", 899.0, 4);
        Producto copia = new Producto(original);

        copia.nombre = "Monitor - copia";

        System.out.println("original = " + original.nombre);
        System.out.println("copia = " + copia.nombre);
        System.out.println("precio copia = " + copia.precio);
        System.out.println("stock copia = " + copia.stock);
    }
}
```

## Antes de ejecutar: predicción

1. ¿La copia tendrá los mismos valores iniciales que el original?
2. Después de cambiar `copia.nombre`, ¿debería cambiar `original.nombre`?

## Ejecuta

```bash
javac Producto.java Main.java
java Main
```

## Resultado esperado

```text
original = Monitor
copia = Monitor - copia
precio copia = 899.0
stock copia = 4
```

## Cómo interpretarlo

`new Producto(original)` invoca un constructor que crea otra instancia y copia los valores. Por eso podemos modificar el atributo `nombre` de la nueva instancia sin cambiar el valor mostrado por el objeto original.

## Variación A

Cambia `copia.stock = 1;` y compara ambos objetos.

## Variación B

Crea una segunda copia usando `new Producto(copia)` y observa qué valores hereda en ese momento.

## Error controlado

Sustituye `Producto copia = new Producto(original);` por `Producto copia = original;` y luego cambia `copia.nombre`.

## Por qué ocurre

Esa asignación no invoca el constructor de copia ni crea una nueva instancia; ambas variables quedan asociadas al mismo objeto.

## Corrección razonada

Vuelve a usar `Producto copia = new Producto(original);` para crear una instancia nueva mediante el constructor de copia.

## Qué debes poder explicar con tus palabras

- ¿Qué recibe el constructor de copia?
- ¿Qué diferencia observable existe entre usar `new Producto(original)` y usar `copia = original`?

## T04 - Tarea espejo: Crear una copia independiente de Libro

**Enunciado.** Crear una copia independiente de Libro. Trabaja con la clase `Libro` para transferir la habilidad del ejemplo sin copiar literalmente el caso `Producto`.

**Archivos a modificar:** `Libro.java` y `Main.java`.

**Restricción:** La copia debe construirse con `new Libro(original)`. No uses `Libro copia = original` como solución.

**Pista:** El parámetro del constructor de copia es otro objeto `Libro`.

**Evidencia que debes mostrar:** Salida donde el título original permanece sin cambios después de modificar la copia.

**Cómo saber si está correcta:** Original y copia deben empezar con los mismos valores; luego solo el título de la copia debe cambiar.


---

# EJ05 - Método de instancia: operar con el estado de un objeto

## Qué vamos a construir

Un programa mínimo con `Producto.java` y `Main.java` para practicar **Método de instancia**.

## Qué aprenderás aquí

Definir e invocar un método que trabaja con atributos propios de cada instancia.

## Archivos que vamos a crear o modificar

- `Producto.java`
- `Main.java`

## Punto de partida

Crea una carpeta `EJ05` dentro de `POO_S03`. Comienza con los dos archivos vacíos indicados. No reutilices el archivo final del ejemplo anterior: queremos observar qué aporta exactamente esta habilidad.

## Paso 1 - Crear la clase Producto

Abre `Producto.java` y escribe el estado final de la clase para este ejemplo. Después lo leeremos por partes.

```java
public class Producto {
    String nombre;
    int stock;

    public Producto(String nombreInicial, int stockInicial) {
        nombre = nombreInicial;
        stock = stockInicial;
    }

    public void aumentarStock(int cantidad) {
        stock = stock + cantidad;
    }
}
```

### Qué significa

El método `aumentarStock` no es `static`; por tanto, trabaja dentro del contexto de una instancia y modifica su atributo `stock`.

### Por qué lo hacemos ahora

Este ejemplo aísla **Método de instancia** para que puedas predecir su efecto antes de mezclarlo con los demás componentes de la clase.

## Paso 2 - Crear el punto de entrada

Abre `Main.java` y escribe:

```java
public class Main {
    public static void main(String[] args) {
        Producto producto = new Producto("Webcam", 5);

        producto.aumentarStock(3);

        System.out.println("producto = " + producto.nombre);
        System.out.println("stock = " + producto.stock);
    }
}
```

### Lectura pedagógica del código

La llamada comienza con `producto.` porque `aumentarStock` es un método de instancia. Dentro del método se usa el `stock` de ese objeto concreto.

## Flujo mental

`entrada -> operación -> cambio/resultado -> salida`

`aumentarStock` es un método de instancia: se invoca desde `producto` y puede acceder directamente al atributo `stock` de ese objeto. La operación afecta al estado de esa instancia.

## Archivo completo al terminar este ejemplo

### Producto.java

```java
public class Producto {
    String nombre;
    int stock;

    public Producto(String nombreInicial, int stockInicial) {
        nombre = nombreInicial;
        stock = stockInicial;
    }

    public void aumentarStock(int cantidad) {
        stock = stock + cantidad;
    }
}
```

### Main.java

```java
public class Main {
    public static void main(String[] args) {
        Producto producto = new Producto("Webcam", 5);

        producto.aumentarStock(3);

        System.out.println("producto = " + producto.nombre);
        System.out.println("stock = " + producto.stock);
    }
}
```

## Antes de ejecutar: predicción

1. ¿Qué valor de `stock` leerá el método antes de modificarlo?
2. ¿Cuál será el stock después de sumar 3?

## Ejecuta

```bash
javac Producto.java Main.java
java Main
```

## Resultado esperado

```text
producto = Webcam
stock = 8
```

## Cómo interpretarlo

`aumentarStock` es un método de instancia: se invoca desde `producto` y puede acceder directamente al atributo `stock` de ese objeto. La operación afecta al estado de esa instancia.

## Variación A

Crea dos productos con stocks diferentes e invoca `aumentarStock` solo en uno.

## Variación B

Llama dos veces a `aumentarStock(2)` y sigue la evolución del atributo.

## Error controlado

Intenta invocar `Producto.aumentarStock(3);` desde `Main`.

## Por qué ocurre

El método no es `static`; necesita una instancia concreta porque opera sobre el `stock` de un objeto.

## Corrección razonada

Invoca `producto.aumentarStock(3);` usando la referencia de la instancia.

## Qué debes poder explicar con tus palabras

- ¿Por qué el método necesita una instancia concreta?
- ¿Qué dato del objeto utiliza y modifica?
- ¿Qué pasaría si existen dos objetos con stocks distintos?

## T05 - Tarea espejo: Modificar el stock mediante un método de instancia

**Enunciado.** Modificar el stock mediante un método de instancia. Trabaja con la clase `Libro` para transferir la habilidad del ejemplo sin copiar literalmente el caso `Producto`.

**Archivos a modificar:** `Libro.java` y `Main.java`.

**Restricción:** El método no debe ser `static`; debe modificar el atributo `stock` de la instancia que recibe la llamada.

**Pista:** La invocación debe comenzar con la variable `libro.`.

**Evidencia que debes mostrar:** Stock antes/después o salida final igual a 7.

**Cómo saber si está correcta:** Con stock inicial 3 y aumento 4, el resultado debe ser 7.


---

# EJ06 - Método de clase: una operación que no depende de una instancia

## Qué vamos a construir

Un programa mínimo con `Producto.java` y `Main.java` para practicar **Método de clase static**.

## Qué aprenderás aquí

Definir e invocar un método static desde el nombre de la clase sin crear un objeto para esa operación.

## Archivos que vamos a crear o modificar

- `Producto.java`
- `Main.java`

## Punto de partida

Crea una carpeta `EJ06` dentro de `POO_S03`. Comienza con los dos archivos vacíos indicados. No reutilices el archivo final del ejemplo anterior: queremos observar qué aporta exactamente esta habilidad.

## Paso 1 - Crear la clase Producto

Abre `Producto.java` y escribe el estado final de la clase para este ejemplo. Después lo leeremos por partes.

```java
public class Producto {
    String nombre;
    double precio;

    public Producto(String nombreInicial, double precioInicial) {
        nombre = nombreInicial;
        precio = precioInicial;
    }

    public static double calcularDescuento(double monto, double porcentaje) {
        return monto - (monto * porcentaje / 100.0);
    }
}
```

### Qué significa

`calcularDescuento` está marcado `static`. La operación usa sus parámetros y devuelve un `double`; no necesita los atributos de un objeto concreto.

### Por qué lo hacemos ahora

Este ejemplo aísla **Método de clase static** para que puedas predecir su efecto antes de mezclarlo con los demás componentes de la clase.

## Paso 2 - Crear el punto de entrada

Abre `Main.java` y escribe:

```java
public class Main {
    public static void main(String[] args) {
        double precioFinal = Producto.calcularDescuento(200.0, 10.0);

        System.out.println("precio final = " + precioFinal);
    }
}
```

### Lectura pedagógica del código

La llamada comienza con `Producto.` porque el método es `static`. El resultado se guarda en una variable porque el método devuelve un `double`.

## Flujo mental

`entrada -> operación -> cambio/resultado -> salida`

`calcularDescuento` está declarado con `static`, por eso pertenece a la clase y puede invocarse como `Producto.calcularDescuento(...)`. La operación usa únicamente los parámetros recibidos y no necesita el estado de una instancia.

## Archivo completo al terminar este ejemplo

### Producto.java

```java
public class Producto {
    String nombre;
    double precio;

    public Producto(String nombreInicial, double precioInicial) {
        nombre = nombreInicial;
        precio = precioInicial;
    }

    public static double calcularDescuento(double monto, double porcentaje) {
        return monto - (monto * porcentaje / 100.0);
    }
}
```

### Main.java

```java
public class Main {
    public static void main(String[] args) {
        double precioFinal = Producto.calcularDescuento(200.0, 10.0);

        System.out.println("precio final = " + precioFinal);
    }
}
```

## Antes de ejecutar: predicción

1. ¿Es necesario crear `new Producto(...)` para ejecutar `calcularDescuento`?
2. ¿Cuál será el resultado de aplicar 10% a 200?

## Ejecuta

```bash
javac Producto.java Main.java
java Main
```

## Resultado esperado

```text
precio final = 180.0
```

## Cómo interpretarlo

`calcularDescuento` está declarado con `static`, por eso pertenece a la clase y puede invocarse como `Producto.calcularDescuento(...)`. La operación usa únicamente los parámetros recibidos y no necesita el estado de una instancia.

## Variación A

Prueba `Producto.calcularDescuento(500.0, 15.0)` y calcula primero el resultado a mano.

## Variación B

Guarda el resultado en otra variable y úsalo en una segunda operación.

## Error controlado

Dentro del método `static`, agrega temporalmente `System.out.println(nombre);`.

## Por qué ocurre

`nombre` es un atributo de instancia. Un método `static` no tiene una instancia específica desde la cual obtener ese atributo.

## Corrección razonada

Elimina el acceso directo a `nombre`; usa solo datos recibidos por parámetros o miembros `static` cuando corresponda.

## Qué debes poder explicar con tus palabras

- ¿Por qué se invoca el método desde `Producto` y no desde un objeto?
- ¿Qué condición hace que esta operación sea adecuada como `static`?

## T06 - Tarea espejo: Calcular un descuento mediante un método static

**Enunciado.** Calcular un descuento mediante un método static. Trabaja con la clase `Libro` para transferir la habilidad del ejemplo sin copiar literalmente el caso `Producto`.

**Archivos a modificar:** `Libro.java` y `Main.java`.

**Restricción:** La operación debe ser `static` y recibir por parámetros toda la información necesaria.

**Pista:** La llamada esperada tiene la forma `Libro.nombreDelMetodo(...)`.

**Evidencia que debes mostrar:** Código del método y salida de una llamada hecha desde la clase.

**Cómo saber si está correcta:** Con monto 100 y porcentaje 20, el resultado debe ser 80.0.


---

# EJ07 - Método void: ejecutar una acción sin devolver un valor

## Qué vamos a construir

Un programa mínimo con `Producto.java` y `Main.java` para practicar **Método void**.

## Qué aprenderás aquí

Definir un método que realiza una acción observable y no entrega un valor para reutilizar.

## Archivos que vamos a crear o modificar

- `Producto.java`
- `Main.java`

## Punto de partida

Crea una carpeta `EJ07` dentro de `POO_S03`. Comienza con los dos archivos vacíos indicados. No reutilices el archivo final del ejemplo anterior: queremos observar qué aporta exactamente esta habilidad.

## Paso 1 - Crear la clase Producto

Abre `Producto.java` y escribe el estado final de la clase para este ejemplo. Después lo leeremos por partes.

```java
public class Producto {
    String nombre;
    double precio;

    public Producto(String nombreInicial, double precioInicial) {
        nombre = nombreInicial;
        precio = precioInicial;
    }

    public void mostrarResumen() {
        System.out.println("Producto: " + nombre);
        System.out.println("Precio: " + precio);
    }
}
```

### Qué significa

`mostrarResumen` está declarado `void`. Su responsabilidad es producir una acción observable en consola, no entregar un valor al código llamador.

### Por qué lo hacemos ahora

Este ejemplo aísla **Método void** para que puedas predecir su efecto antes de mezclarlo con los demás componentes de la clase.

## Paso 2 - Crear el punto de entrada

Abre `Main.java` y escribe:

```java
public class Main {
    public static void main(String[] args) {
        Producto producto = new Producto("Audifonos", 149.90);

        producto.mostrarResumen();
    }
}
```

### Lectura pedagógica del código

La llamada `producto.mostrarResumen();` se usa como una acción completa. No hay una variable a la izquierda porque no existe un valor de retorno.

## Flujo mental

`entrada -> operación -> cambio/resultado -> salida`

El método tiene tipo de retorno `void`: ejecuta la acción de mostrar información y finaliza sin entregar un valor al código que lo invocó.

## Archivo completo al terminar este ejemplo

### Producto.java

```java
public class Producto {
    String nombre;
    double precio;

    public Producto(String nombreInicial, double precioInicial) {
        nombre = nombreInicial;
        precio = precioInicial;
    }

    public void mostrarResumen() {
        System.out.println("Producto: " + nombre);
        System.out.println("Precio: " + precio);
    }
}
```

### Main.java

```java
public class Main {
    public static void main(String[] args) {
        Producto producto = new Producto("Audifonos", 149.90);

        producto.mostrarResumen();
    }
}
```

## Antes de ejecutar: predicción

1. ¿Qué acción realizará `mostrarResumen()`?
2. ¿Quedará un valor de retorno disponible para guardarlo en una variable?

## Ejecuta

```bash
javac Producto.java Main.java
java Main
```

## Resultado esperado

```text
Producto: Audifonos
Precio: 149.9
```

## Cómo interpretarlo

El método tiene tipo de retorno `void`: ejecuta la acción de mostrar información y finaliza sin entregar un valor al código que lo invocó.

## Variación A

Agrega una tercera línea que muestre un mensaje fijo y comprueba que el método sigue siendo `void`.

## Variación B

Invoca `mostrarResumen()` dos veces y distingue ejecutar una acción de devolver un dato.

## Error controlado

Intenta escribir `String texto = producto.mostrarResumen();`.

## Por qué ocurre

Un método `void` no devuelve un valor compatible con `String` ni con otro tipo de variable.

## Corrección razonada

Invoca `producto.mostrarResumen();` como una acción independiente.

## Qué debes poder explicar con tus palabras

- ¿Qué hace el método y qué no hace?
- ¿Por qué no podemos almacenar el resultado de un método `void`?

## T07 - Tarea espejo: Mostrar una ficha mediante un método void

**Enunciado.** Mostrar una ficha mediante un método void. Trabaja con la clase `Libro` para transferir la habilidad del ejemplo sin copiar literalmente el caso `Producto`.

**Archivos a modificar:** `Libro.java` y `Main.java`.

**Restricción:** `mostrarFicha` debe ser `void`; no devuelvas un `String` ni intentes guardar su resultado.

**Pista:** El propósito es ejecutar una acción observable: imprimir la ficha.

**Evidencia que debes mostrar:** Salida con título y precio generada al llamar al método.

**Cómo saber si está correcta:** El método se invoca con `libro.mostrarFicha();` y no requiere variable receptora.


---

# EJ08 - Método con retorno e integración: producir un valor y reutilizarlo

## Qué vamos a construir

Un programa mínimo con `Producto.java` y `Main.java` para practicar **Método no void + return + integración de la sesión**.

## Qué aprenderás aquí

Devolver un valor, almacenarlo y combinarlo con una operación static en un flujo completo.

## Archivos que vamos a crear o modificar

- `Producto.java`
- `Main.java`

## Punto de partida

Crea una carpeta `EJ08` dentro de `POO_S03`. Comienza con los dos archivos vacíos indicados. No reutilices el archivo final del ejemplo anterior: queremos observar qué aporta exactamente esta habilidad.

## Paso 1 - Crear la clase Producto

Abre `Producto.java` y escribe el estado final de la clase para este ejemplo. Después lo leeremos por partes.

```java
public class Producto {
    String nombre;
    double precio;
    int stock;

    public Producto(String nombreInicial, double precioInicial, int stockInicial) {
        nombre = nombreInicial;
        precio = precioInicial;
        stock = stockInicial;
    }

    public void mostrarResumen() {
        System.out.println(nombre + " | precio=" + precio + " | stock=" + stock);
    }

    public double calcularSubtotal(int cantidad) {
        return precio * cantidad;
    }

    public static double aplicarImpuesto(double subtotal, double tasa) {
        return subtotal + (subtotal * tasa / 100.0);
    }
}
```

### Qué significa

La clase reúne un constructor parametrizado, un método de instancia `void`, un método de instancia con retorno y un método `static` con retorno. Cada uno responde a una necesidad distinta.

### Por qué lo hacemos ahora

Este ejemplo aísla **Método no void + return + integración de la sesión** para que puedas predecir su efecto antes de mezclarlo con los demás componentes de la clase.

## Paso 2 - Crear el punto de entrada

Abre `Main.java` y escribe:

```java
public class Main {
    public static void main(String[] args) {
        Producto producto = new Producto("Laptop", 2500.0, 10);

        producto.mostrarResumen();

        double subtotal = producto.calcularSubtotal(2);
        double total = Producto.aplicarImpuesto(subtotal, 18.0);

        System.out.println("subtotal = " + subtotal);
        System.out.println("total con impuesto = " + total);
    }
}
```

### Lectura pedagógica del código

El flujo separa responsabilidades: el objeto ejecuta acciones y cálculos relacionados con su estado; la clase ejecuta la operación común `aplicarImpuesto` a partir de valores recibidos.

## Flujo mental

`entrada -> operación -> cambio/resultado -> salida`

El flujo integra las decisiones de la sesión. El constructor parametrizado crea el objeto con datos específicos. `mostrarResumen()` es de instancia y `void`: ejecuta una acción. `calcularSubtotal()` es de instancia y devuelve un `double` que se almacena. `aplicarImpuesto()` es `static`: trabaja con valores recibidos y se invoca desde la clase.

## Archivo completo al terminar este ejemplo

### Producto.java

```java
public class Producto {
    String nombre;
    double precio;
    int stock;

    public Producto(String nombreInicial, double precioInicial, int stockInicial) {
        nombre = nombreInicial;
        precio = precioInicial;
        stock = stockInicial;
    }

    public void mostrarResumen() {
        System.out.println(nombre + " | precio=" + precio + " | stock=" + stock);
    }

    public double calcularSubtotal(int cantidad) {
        return precio * cantidad;
    }

    public static double aplicarImpuesto(double subtotal, double tasa) {
        return subtotal + (subtotal * tasa / 100.0);
    }
}
```

### Main.java

```java
public class Main {
    public static void main(String[] args) {
        Producto producto = new Producto("Laptop", 2500.0, 10);

        producto.mostrarResumen();

        double subtotal = producto.calcularSubtotal(2);
        double total = Producto.aplicarImpuesto(subtotal, 18.0);

        System.out.println("subtotal = " + subtotal);
        System.out.println("total con impuesto = " + total);
    }
}
```

## Antes de ejecutar: predicción

1. ¿Qué valor devolverá `calcularSubtotal(2)`?
2. ¿Por qué `aplicarImpuesto` se invoca desde la clase?
3. ¿Qué diferencia existe entre `mostrarResumen()` y `calcularSubtotal(...)`?

## Ejecuta

```bash
javac Producto.java Main.java
java Main
```

## Resultado esperado

```text
Laptop | precio=2500.0 | stock=10
subtotal = 5000.0
total con impuesto = 5900.0
```

## Cómo interpretarlo

El flujo integra las decisiones de la sesión. El constructor parametrizado crea el objeto con datos específicos. `mostrarResumen()` es de instancia y `void`: ejecuta una acción. `calcularSubtotal()` es de instancia y devuelve un `double` que se almacena. `aplicarImpuesto()` es `static`: trabaja con valores recibidos y se invoca desde la clase.

## Variación A

Cambia la cantidad de 2 a 3 y predice subtotal y total antes de ejecutar.

## Variación B

Cambia la tasa de 18 a 10 y compara qué parte del flujo cambia y cuál permanece igual.

## Error controlado

Elimina temporalmente `return precio * cantidad;` del método `calcularSubtotal`.

## Por qué ocurre

El método declara que devolverá `double`; por tanto, debe producir un valor compatible en su flujo de ejecución.

## Corrección razonada

Restaura `return precio * cantidad;`.

## Qué debes poder explicar con tus palabras

- ¿Qué métodos dependen del objeto `producto`?
- ¿Qué método pertenece a la clase?
- ¿Cuál acción no devuelve valor y cuáles sí producen un dato reutilizable?

## T08 - Tarea espejo: Integrar constructor, instancia, static, void y return en Libro

**Enunciado.** Integrar constructor, instancia, static, void y return en Libro. Trabaja con la clase `Libro` para transferir la habilidad del ejemplo sin copiar literalmente el caso `Producto`.

**Archivos a modificar:** `Libro.java` y `Main.java`.

**Restricción:** Debes justificar cada invocación: objeto para métodos de instancia y clase para el método `static`. `mostrarFicha` debe ser `void`; los cálculos deben devolver `double`.

**Pista:** Separa mentalmente acción (`void`) de cálculo reutilizable (`return`).

**Evidencia que debes mostrar:** Código final y salida con ficha, subtotal y total con descuento.

**Cómo saber si está correcta:** Con 2 unidades a 120 y 10% de descuento, subtotal=240.0 y total=216.0.


---

# Cierre de sesión

Hoy construiste una progresión completa: primero observaste qué ocurre cuando Java aporta un constructor por defecto; después escribiste constructores sin argumentos, parametrizados y de copia. Luego pasaste del nacimiento del objeto a su comportamiento, diferenciando llamadas que necesitan una instancia de aquellas que pueden ejecutarse desde la clase mediante `static`. Finalmente separaste las operaciones `void`, que realizan una acción sin entregar un valor, de los métodos que declaran un tipo de retorno y utilizan `return` para producir un dato reutilizable.

La parte más importante no es recordar una lista de reglas, sino justificar la decisión: **¿necesito inicializar?, ¿esta operación depende de un objeto concreto?, ¿el resultado debe regresar al código que llama?** Si puedes responder esas tres preguntas y resolver `T08`, ya tienes una base sólida para continuar.

Repasa los errores controlados porque muestran confusiones reales: agregar `void` a un constructor, invocar un método de instancia desde la clase, acceder a datos de instancia desde un contexto `static` o intentar guardar el resultado de un método `void`.

Como refuerzo puedes consultar Lideratec Academy: https://lideratecacademy.com/blog/ y el canal https://www.youtube.com/@LideratecAcademy. El laboratorio de FASE 15 queda disponible como proyecto completo para validar o recuperar tu implementación, pero no es necesario para completar esta guía.
