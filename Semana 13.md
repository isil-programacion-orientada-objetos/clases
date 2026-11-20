# FASE 13 — SESIÓN 13: HERENCIA EN JAVA

**Curso:** Programación Orientada a Objetos (ISIL) · **Duración:** 120 minutos · **Herramientas:** IntelliJ IDEA y JDK 21 · **Modalidad:** laboratorio de consola.

## Resultados de aprendizaje de la semana

Al finalizar, podrás reconocer superclase y subclase; diseñar herencia simple con `extends`; inicializar atributos heredados con `super()`; explicar visibilidad `public`, `protected`, acceso de paquete y `private`; sobrescribir métodos con `@Override` y `super.metodo()`; declarar clases abstractas e implementar sus métodos; implementar interfaces con `implements`; y justificar por qué una clase hereda de una sola clase, pero puede implementar contratos.

**Base académica:** presentación ISIL Tema 13: herencia; diapositivas 5–13 (jerarquías y constructores), 15–18 (abstract), 20–23 (interface) y 25–26 (sobrescritura). Ejemplos EJ01–EJ06 son adaptaciones y EJ07 integra los contenidos.

## Preparación completa desde cero en IntelliJ IDEA

1. Comprueba el JDK: en la terminal ejecuta `java -version` y `javac -version`. Deben indicar versión 21 para este laboratorio.
2. Abre IntelliJ IDEA → **New Project** → **Java**; elige JDK 21 y crea `S13_Herencia_Java` (sin framework ni dependencias externas). La interfaz puede variar entre versiones.
3. En la carpeta `src`, crea una clase Java nueva llamada `EJ01`. Al abrir el archivo, reemplaza su contenido por el código completo mostrado al final del ejemplo EJ01. El nombre de la clase pública debe coincidir con el archivo. En cada nuevo ejemplo crea el siguiente archivo `EJ02.java`, etc.
4. Para ejecutar, abre `EJ01.java` y utiliza el botón de ejecución junto a `main`, o abre una terminal en `src` y ejecuta `javac EJ01.java` seguido de `java EJ01`.
5. **Importante:** cada ejemplo va en una carpeta o proyecto independiente si usas las mismas clases auxiliares (`Empleado`, `Directivo`, etc.). En IntelliJ, crea un subproyecto o un módulo de Java por ejemplo; también puedes abrir directamente la carpeta `estudiante/ejemplos/EJxx` del laboratorio descargable. En consola, `cd` a esa carpeta antes de compilar.
6. Trabaja cada ejemplo en orden: predice primero, escribe por microbloques, compila, interpreta, introduce el error controlado y resuélvelo. Para las tareas espejo utiliza clases con sufijo Txx para evitar colisiones.

### Plan de clase de 120 minutos

| Tiempo | Bloque | Evidencia |
|---|---|---|
| 0–10 min | Objetivos, diagnóstico y entorno | JDK e IntelliJ listos |
| 10–25 min | EJ01 y T01 | Herencia sin duplicación |
| 25–40 min | EJ02 y T02 | `super()` ejecutado |
| 40–52 min | EJ03 y T03 | Jerarquía de tres niveles |
| 52–68 min | EJ04 y T04 | Método sobrescrito |
| 68–88 min | EJ05 y T05 | Clase abstracta funcional |
| 88–104 min | EJ06 y T06 | Interfaz compartida |
| 104–116 min | EJ07 y T07 | Integración comprobada |
| 116–120 min | Cierre y ticket de salida | Explicación de diferencias |

**Ritmo:** durante una clase de 120 minutos desarrolla EJ01, EJ02, EJ04, EJ05, EJ06 y EJ07 en vivo. EJ03 y las siete tareas espejo pueden trabajarse parcialmente en aula y completarse fuera de ella, sin reducir la explicación de la guía.


---

# EJ01 — Eliminar duplicación mediante extends

**Objetivo técnico y problema:** Un sistema mantiene el nombre y el sueldo tanto en Empleado como en Directivo. Si un dato común cambia, mantener dos copias del atributo incrementa el riesgo de inconsistencias. Extraeremos los miembros compartidos hacia Empleado y especializaremos Directivo con extends.

**Punto de partida:** carpeta independiente `EJ01`; crea `EJ01.java`. Antes de escribir, pregunta al compañero qué relación «es un» existe.

**Archivos:** `EJ01.java`; tarea espejo en `T01.java`. **Vínculo fuente:** Diapositivas 7–8.


## Paso 1 — Separar los datos comunes

**Estado previo:** aún no se ha introducido este bloque o comportamiento; trabaja en el mismo archivo antes de `public class EJ01`.

**Escribe este microbloque orientativo:**

```java
class Empleado {
    protected String nombre;
    protected double sueldo;
}
```

**Qué acabas de construir y por qué:** nombre y sueldo pertenecen a cualquier empleado. protected permite que la subclase acceda a esos miembros, aunque en aplicaciones reales conviene proteger el estado con métodos de acceso.

**Estado siguiente:** ya dispones de la pieza recién explicada. Al final del recorrido unirás los bloques en el código completo canónico indicado abajo; ese código es el que debes compilar.


## Paso 2 — Declarar la especialización

**Estado previo:** aún no se ha introducido este bloque o comportamiento; trabaja en el mismo archivo antes de `public class EJ01`.

**Escribe este microbloque orientativo:**

```java
class Directivo extends Empleado {
    private String departamento;
}
```

**Qué acabas de construir y por qué:** extends indica una relación «es un». El Directivo es un Empleado con una responsabilidad adicional: el departamento. No volvemos a declarar nombre ni sueldo.

**Estado siguiente:** ya dispones de la pieza recién explicada. Al final del recorrido unirás los bloques en el código completo canónico indicado abajo; ese código es el que debes compilar.


## Paso 3 — Comprobar la herencia con un objeto

**Estado previo:** aún no se ha introducido este bloque o comportamiento; trabaja en el mismo archivo antes de `public class EJ01`.

**Escribe este microbloque orientativo:**

```java
Directivo d = new Directivo();
d.nombre = "Ana";
d.sueldo = 2500;
d.departamento = "TI";
```

**Qué acabas de construir y por qué:** Se crea un único objeto Directivo. El objeto contiene estado heredado de Empleado y el campo adicional de su propia clase.

**Estado siguiente:** ya dispones de la pieza recién explicada. Al final del recorrido unirás los bloques en el código completo canónico indicado abajo; ese código es el que debes compilar.


## Auditoría y archivo completo al terminar EJ01

Verifica que estén presentes las declaraciones de clases, las relaciones `extends`/`implements` aplicables, constructores o métodos y una clase pública `EJ01` con `main`. Los microbloques anteriores muestran las decisiones sucesivas; el siguiente archivo reúne el estado final coherente y ejecutable, incluidos los detalles de prueba y salida que se ejecutan en `main`.

```java
class Empleado {
    protected String nombre;
    protected double sueldo;
    public String leerRegistro() { return nombre + " | S/ " + sueldo; }
}
class Directivo extends Empleado {
    String departamento;
    @Override public String leerRegistro() { return super.leerRegistro() + " | " + departamento; }
}
public class EJ01 {
    public static void main(String[] args) {
        Directivo d = new Directivo();
        d.nombre = "Ana";
        d.sueldo = 2500;
        d.departamento = "TI";
        System.out.println(d.leerRegistro());
    }
}
```

### Predice, ejecuta e interpreta

**Predicción:** ¿Cuántos objetos se crean y de qué clase? ¿Por qué Directivo puede utilizar nombre?

```bash
javac EJ01.java
java EJ01
```

**Salida esperada:**

```text
Ana | S/ 2500.0 | TI
```

**Interpretación:** Superclase y subclase. Relaciona cada parte de la salida con el método que la origina; explica qué elemento heredado o implementado intervino. Comprueba la predicción con la consola.

**Variación controlada:** Cambia el sueldo a 3100 y observa que leerRegistro() reutiliza el dato heredado.

**Error frecuente:** Si escribes class Directivo sin extends Empleado, d.nombre deja de estar disponible.

**Corrección razonada:** Restituye extends Empleado para establecer la jerarquía.

## T01 — Tarea espejo

**Enunciado:** Crear una subclase Practicante de Empleado con atributo instituto; reutilizar nombre y sueldo; imprimir una ficha extendida.

**Archivo:** `T01.java` en carpeta separada. **Restricción:** no elimines la estructura de jerarquía ni sustituir la relación por código duplicado. **Pista:** identifica primero el miembro compartido y después la responsabilidad específica. **Evidencia:** captura del código, compilación y consola, más explicación de las decisiones. **Criterio:** el proyecto compila, produce el resultado propuesto y usa el concepto nuevo de EJ01 correctamente. **No copies la solución docente:** adapta la estructura trabajando las clases por separado.


---

# EJ02 — Inicializar la subclase mediante super()

**Objetivo técnico y problema:** Heredar campos no garantiza que estén inicializados. Construiremos una superclase Persona con constructor obligatorio y una subclase Cliente que delega la inicialización de nombre y edad usando super(nombre, edad).

**Punto de partida:** carpeta independiente `EJ02`; crea `EJ02.java`. Antes de escribir, pregunta al compañero qué relación «es un» existe.

**Archivos:** `EJ02.java`; tarea espejo en `T02.java`. **Vínculo fuente:** Diapositivas 10–13.


## Paso 1 — Crear Persona y exigir datos válidos

**Estado previo:** aún no se ha introducido este bloque o comportamiento; trabaja en el mismo archivo antes de `public class EJ02`.

**Escribe este microbloque orientativo:**

```java
class Persona {
    protected String nombre;
    protected int edad;
    Persona(String nombre, int edad) {
        this.nombre = nombre;
        this.edad = edad;
    }
}
```

**Qué acabas de construir y por qué:** El constructor recibe los datos comunes. this distingue el atributo del parámetro homónimo; crear Persona exige enviar ambos argumentos.

**Estado siguiente:** ya dispones de la pieza recién explicada. Al final del recorrido unirás los bloques en el código completo canónico indicado abajo; ese código es el que debes compilar.


## Paso 2 — Crear Cliente como especialización

**Estado previo:** aún no se ha introducido este bloque o comportamiento; trabaja en el mismo archivo antes de `public class EJ02`.

**Escribe este microbloque orientativo:**

```java
class Cliente extends Persona {
    private double credito;
    Cliente(String nombre, int edad, double credito) {
        super(nombre, edad);
        this.credito = credito;
    }
}
```

**Qué acabas de construir y por qué:** super(nombre, edad) se dirige al constructor de Persona; aquí ocupa la primera sentencia del constructor de Cliente. Solo después se inicializa el dato propio credito.

**Estado siguiente:** ya dispones de la pieza recién explicada. Al final del recorrido unirás los bloques en el código completo canónico indicado abajo; ese código es el que debes compilar.


## Paso 3 — Probar la construcción

**Estado previo:** aún no se ha introducido este bloque o comportamiento; trabaja en el mismo archivo antes de `public class EJ02`.

**Escribe este microbloque orientativo:**

```java
Cliente c = new Cliente("Rosa", 22, 500);
System.out.println(c.ficha());
```

**Qué acabas de construir y por qué:** El objeto tiene nombre y edad inicializados por Persona y crédito asignado por Cliente.

**Estado siguiente:** ya dispones de la pieza recién explicada. Al final del recorrido unirás los bloques en el código completo canónico indicado abajo; ese código es el que debes compilar.


## Auditoría y archivo completo al terminar EJ02

Verifica que estén presentes las declaraciones de clases, las relaciones `extends`/`implements` aplicables, constructores o métodos y una clase pública `EJ02` con `main`. Los microbloques anteriores muestran las decisiones sucesivas; el siguiente archivo reúne el estado final coherente y ejecutable, incluidos los detalles de prueba y salida que se ejecutan en `main`.

```java
class Persona {
    protected String nombre;
    protected int edad;
    Persona(String nombre, int edad) { this.nombre = nombre; this.edad = edad; }
}
class Cliente extends Persona {
    private double credito;
    Cliente(String nombre, int edad, double credito) {
        super(nombre, edad);
        this.credito = credito;
    }
    public String ficha() { return nombre + " (" + edad + ") crédito: " + credito; }
}
public class EJ02 {
    public static void main(String[] args) {
        Cliente c = new Cliente("Rosa", 22, 500);
        System.out.println(c.ficha());
    }
}
```

### Predice, ejecuta e interpreta

**Predicción:** ¿Cuál constructor se ejecuta antes: Persona o Cliente? ¿Qué ocurriría si no llamamos al constructor disponible de Persona?

```bash
javac EJ02.java
java EJ02
```

**Salida esperada:**

```text
Rosa (22) crédito: 500.0
```

**Interpretación:** Constructores y modificadores de acceso. Relaciona cada parte de la salida con el método que la origina; explica qué elemento heredado o implementado intervino. Comprueba la predicción con la consola.

**Variación controlada:** Construye un segundo Cliente con edad 30 y crédito 1200 y compáralos.

**Error frecuente:** Omitir super(nombre, edad) intenta llamar implícitamente Persona(), que no existe.

**Corrección razonada:** Invoca explícitamente super(nombre, edad) antes de inicializar credito.

## T02 — Tarea espejo

**Enunciado:** Crear Estudiante extends PersonaT02; inicializar carrera mediante constructor y mostrar ficha, usando super().

**Archivo:** `T02.java` en carpeta separada. **Restricción:** no elimines la estructura de jerarquía ni sustituir la relación por código duplicado. **Pista:** identifica primero el miembro compartido y después la responsabilidad específica. **Evidencia:** captura del código, compilación y consola, más explicación de las decisiones. **Criterio:** el proyecto compila, produce el resultado propuesto y usa el concepto nuevo de EJ02 correctamente. **No copies la solución docente:** adapta la estructura trabajando las clases por separado.


---

# EJ03 — Extender una jerarquía en tres niveles

**Objetivo técnico y problema:** La jerarquía Empleado → Directivo → JefeArea es un caso de herencia simple en cadena: cada clase tiene como máximo una superclase directa. Construiremos niveles y verificaremos qué capacidades están disponibles en el último.

**Punto de partida:** carpeta independiente `EJ03`; crea `EJ03.java`. Antes de escribir, pregunta al compañero qué relación «es un» existe.

**Archivos:** `EJ03.java`; tarea espejo en `T03.java`. **Vínculo fuente:** Diapositivas 9–10.


## Paso 1 — Definir la base Empleado

**Estado previo:** aún no se ha introducido este bloque o comportamiento; trabaja en el mismo archivo antes de `public class EJ03`.

**Escribe este microbloque orientativo:**

```java
class Empleado {
    protected String nombre;
    Empleado(String nombre) { this.nombre = nombre; }
}
```

**Qué acabas de construir y por qué:** El nivel base concentra identidad compartida.

**Estado siguiente:** ya dispones de la pieza recién explicada. Al final del recorrido unirás los bloques en el código completo canónico indicado abajo; ese código es el que debes compilar.


## Paso 2 — Especializar Directivo

**Estado previo:** aún no se ha introducido este bloque o comportamiento; trabaja en el mismo archivo antes de `public class EJ03`.

**Escribe este microbloque orientativo:**

```java
class Directivo extends Empleado {
    protected String departamento;
    Directivo(String n, String d) {
        super(n); departamento = d;
    }
}
```

**Qué acabas de construir y por qué:** Directivo reutiliza el constructor de Empleado y agrega departamento.

**Estado siguiente:** ya dispones de la pieza recién explicada. Al final del recorrido unirás los bloques en el código completo canónico indicado abajo; ese código es el que debes compilar.


## Paso 3 — Especializar JefeArea

**Estado previo:** aún no se ha introducido este bloque o comportamiento; trabaja en el mismo archivo antes de `public class EJ03`.

**Escribe este microbloque orientativo:**

```java
class JefeArea extends Directivo {
    private double movilidad;
    JefeArea(String n, String d, double m) {
        super(n, d); movilidad = m;
    }
}
```

**Qué acabas de construir y por qué:** JefeArea hereda datos de ambos niveles anteriores y añade movilidad; cada constructor delega en su padre directo.

**Estado siguiente:** ya dispones de la pieza recién explicada. Al final del recorrido unirás los bloques en el código completo canónico indicado abajo; ese código es el que debes compilar.


## Auditoría y archivo completo al terminar EJ03

Verifica que estén presentes las declaraciones de clases, las relaciones `extends`/`implements` aplicables, constructores o métodos y una clase pública `EJ03` con `main`. Los microbloques anteriores muestran las decisiones sucesivas; el siguiente archivo reúne el estado final coherente y ejecutable, incluidos los detalles de prueba y salida que se ejecutan en `main`.

```java
class Empleado {
    protected String nombre;
    Empleado(String nombre) { this.nombre = nombre; }
}
class Directivo extends Empleado {
    protected String departamento;
    Directivo(String nombre, String departamento) {
        super(nombre); this.departamento = departamento;
    }
}
class JefeArea extends Directivo {
    private double movilidad;
    JefeArea(String nombre, String departamento, double movilidad) {
        super(nombre, departamento); this.movilidad = movilidad;
    }
    public String resumen() { return nombre + " - " + departamento + " - S/ " + movilidad; }
}
public class EJ03 {
    public static void main(String[] args) {
        JefeArea jefe = new JefeArea("Carlos", "Soporte", 150);
        System.out.println(jefe.resumen());
    }
}
```

### Predice, ejecuta e interpreta

**Predicción:** ¿Puede JefeArea acceder a nombre si lo declaró Empleado? ¿Qué constructor se ejecuta primero?

```bash
javac EJ03.java
java EJ03
```

**Salida esperada:**

```text
Carlos - Soporte - S/ 150.0
```

**Interpretación:** Herencia simple y encadenada. Relaciona cada parte de la salida con el método que la origina; explica qué elemento heredado o implementado intervino. Comprueba la predicción con la consola.

**Variación controlada:** Agrega un segundo JefeArea con otro departamento y compara los resultados.

**Error frecuente:** Intentar que JefeArea extienda simultáneamente Directivo y otra clase con extends no compila en Java.

**Corrección razonada:** Conserva una sola superclase directa y modela responsabilidades diferentes con interfaces cuando corresponda.

## T03 — Tarea espejo

**Enunciado:** Extender la cadena PersonaBase → Trabajador → Supervisor y agregar un bono; imprimir datos heredados y propios.

**Archivo:** `T03.java` en carpeta separada. **Restricción:** no elimines la estructura de jerarquía ni sustituir la relación por código duplicado. **Pista:** identifica primero el miembro compartido y después la responsabilidad específica. **Evidencia:** captura del código, compilación y consola, más explicación de las decisiones. **Criterio:** el proyecto compila, produce el resultado propuesto y usa el concepto nuevo de EJ03 correctamente. **No copies la solución docente:** adapta la estructura trabajando las clases por separado.


---

# EJ04 — Sobrescribir un método y reutilizar super.metodo()

**Objetivo técnico y problema:** Un Directivo necesita mostrar información común más su departamento. En lugar de duplicar el texto de la superclase, sobrescribiremos leerRegistro() y llamaremos a super.leerRegistro() para añadir información.

**Punto de partida:** carpeta independiente `EJ04`; crea `EJ04.java`. Antes de escribir, pregunta al compañero qué relación «es un» existe.

**Archivos:** `EJ04.java`; tarea espejo en `T04.java`. **Vínculo fuente:** Diapositivas 24–26.


## Paso 1 — Definir el comportamiento común

**Estado previo:** aún no se ha introducido este bloque o comportamiento; trabaja en el mismo archivo antes de `public class EJ04`.

**Escribe este microbloque orientativo:**

```java
class Empleado {
    String leerRegistro() { return "Empleado registrado"; }
}
```

**Qué acabas de construir y por qué:** La clase base tiene una implementación concreta reutilizable.

**Estado siguiente:** ya dispones de la pieza recién explicada. Al final del recorrido unirás los bloques en el código completo canónico indicado abajo; ese código es el que debes compilar.


## Paso 2 — Añadir un comportamiento especializado

**Estado previo:** aún no se ha introducido este bloque o comportamiento; trabaja en el mismo archivo antes de `public class EJ04`.

**Escribe este microbloque orientativo:**

```java
class Directivo extends Empleado {
    @Override String leerRegistro() {
        return super.leerRegistro() + " | Área: TI";
    }
}
```

**Qué acabas de construir y por qué:** @Override solicita al compilador que compruebe la sobrescritura; super.leerRegistro() utiliza la implementación heredada en vez de recursar.

**Estado siguiente:** ya dispones de la pieza recién explicada. Al final del recorrido unirás los bloques en el código completo canónico indicado abajo; ese código es el que debes compilar.


## Paso 3 — Invocar a través del tipo padre

**Estado previo:** aún no se ha introducido este bloque o comportamiento; trabaja en el mismo archivo antes de `public class EJ04`.

**Escribe este microbloque orientativo:**

```java
Empleado e = new Directivo();
System.out.println(e.leerRegistro());
```

**Qué acabas de construir y por qué:** La variable está declarada como Empleado, pero el objeto real es Directivo; se ejecuta el método sobrescrito.

**Estado siguiente:** ya dispones de la pieza recién explicada. Al final del recorrido unirás los bloques en el código completo canónico indicado abajo; ese código es el que debes compilar.


## Auditoría y archivo completo al terminar EJ04

Verifica que estén presentes las declaraciones de clases, las relaciones `extends`/`implements` aplicables, constructores o métodos y una clase pública `EJ04` con `main`. Los microbloques anteriores muestran las decisiones sucesivas; el siguiente archivo reúne el estado final coherente y ejecutable, incluidos los detalles de prueba y salida que se ejecutan en `main`.

```java
class Empleado {
    String leerRegistro() { return "Empleado registrado"; }
}
class Directivo extends Empleado {
    @Override String leerRegistro() {
        return super.leerRegistro() + " | Área: TI";
    }
}
public class EJ04 {
    public static void main(String[] args) {
        Empleado e = new Directivo();
        System.out.println(e.leerRegistro());
    }
}
```

### Predice, ejecuta e interpreta

**Predicción:** ¿Se imprimirá únicamente «Empleado registrado» o también «Área: TI»? Justifica utilizando el objeto real.

```bash
javac EJ04.java
java EJ04
```

**Salida esperada:**

```text
Empleado registrado | Área: TI
```

**Interpretación:** Sobrescritura de métodos. Relaciona cada parte de la salida con el método que la origina; explica qué elemento heredado o implementado intervino. Comprueba la predicción con la consola.

**Variación controlada:** Reemplaza temporalmente super.leerRegistro() por "Registro propio" y compara la salida.

**Error frecuente:** Usar leerRegistro() sin super dentro de su propio override provoca recursión infinita.

**Corrección razonada:** Invoca super.leerRegistro() para delegar en la implementación de la superclase.

## T04 — Tarea espejo

**Enunciado:** Crear VehiculoT04 y Moto, sobrescribir descripcion() y agregar cilindrada llamando a super.descripcion().

**Archivo:** `T04.java` en carpeta separada. **Restricción:** no elimines la estructura de jerarquía ni sustituir la relación por código duplicado. **Pista:** identifica primero el miembro compartido y después la responsabilidad específica. **Evidencia:** captura del código, compilación y consola, más explicación de las decisiones. **Criterio:** el proyecto compila, produce el resultado propuesto y usa el concepto nuevo de EJ04 correctamente. **No copies la solución docente:** adapta la estructura trabajando las clases por separado.


---

# EJ05 — Implementar una clase abstracta de figuras

**Objetivo técnico y problema:** Un cálculo de área no es idéntico para todas las figuras. Estableceremos un contrato parcial mediante Figura, que contiene métodos abstractos calcularArea() y calcularPerimetro(). Implementaremos un Cuadrado y un Triangulo usando cálculos adecuados a cada figura.

**Punto de partida:** carpeta independiente `EJ05`; crea `EJ05.java`. Antes de escribir, pregunta al compañero qué relación «es un» existe.

**Archivos:** `EJ05.java`; tarea espejo en `T05.java`. **Vínculo fuente:** Diapositivas 15–18.


## Paso 1 — Declarar la clase base incompleta

**Estado previo:** aún no se ha introducido este bloque o comportamiento; trabaja en el mismo archivo antes de `public class EJ05`.

**Escribe este microbloque orientativo:**

```java
abstract class Figura {
    public abstract double calcularArea();
    public abstract double calcularPerimetro();
}
```

**Qué acabas de construir y por qué:** abstract impide crear directamente new Figura(). Cada método abstracto carece de cuerpo y obliga a las subclases concretas a completarlo.

**Estado siguiente:** ya dispones de la pieza recién explicada. Al final del recorrido unirás los bloques en el código completo canónico indicado abajo; ese código es el que debes compilar.


## Paso 2 — Resolver las operaciones del cuadrado

**Estado previo:** aún no se ha introducido este bloque o comportamiento; trabaja en el mismo archivo antes de `public class EJ05`.

**Escribe este microbloque orientativo:**

```java
class Cuadrado extends Figura {
    private double lado;
    Cuadrado(double lado) { this.lado = lado; }
    @Override public double calcularArea() { return lado * lado; }
    @Override public double calcularPerimetro() { return 4 * lado; }
}
```

**Qué acabas de construir y por qué:** Cuadrado aporta lado y dos fórmulas específicas. @Override verifica la implementación de cada contrato.

**Estado siguiente:** ya dispones de la pieza recién explicada. Al final del recorrido unirás los bloques en el código completo canónico indicado abajo; ese código es el que debes compilar.


## Paso 3 — Resolver las del triángulo

**Estado previo:** aún no se ha introducido este bloque o comportamiento; trabaja en el mismo archivo antes de `public class EJ05`.

**Escribe este microbloque orientativo:**

```java
class TrianguloEquilatero extends Figura {
    private double lado;
    TrianguloEquilatero(double lado) { this.lado = lado; }
    @Override public double calcularArea() { return Math.sqrt(3) * lado * lado / 4; }
    @Override public double calcularPerimetro() { return 3 * lado; }
}
```

**Qué acabas de construir y por qué:** Un triángulo equilátero tiene tres lados iguales y área √3 × lado² / 4. No es correcto usar base×altura/2 si no hemos proporcionado una altura real.

**Estado siguiente:** ya dispones de la pieza recién explicada. Al final del recorrido unirás los bloques en el código completo canónico indicado abajo; ese código es el que debes compilar.


## Auditoría y archivo completo al terminar EJ05

Verifica que estén presentes las declaraciones de clases, las relaciones `extends`/`implements` aplicables, constructores o métodos y una clase pública `EJ05` con `main`. Los microbloques anteriores muestran las decisiones sucesivas; el siguiente archivo reúne el estado final coherente y ejecutable, incluidos los detalles de prueba y salida que se ejecutan en `main`.

```java
abstract class Figura {
    public abstract double calcularArea();
    public abstract double calcularPerimetro();
}
class Cuadrado extends Figura {
    private double lado;
    Cuadrado(double lado) { this.lado = lado; }
    @Override public double calcularArea() { return lado * lado; }
    @Override public double calcularPerimetro() { return 4 * lado; }
}
class TrianguloEquilatero extends Figura {
    private double lado;
    TrianguloEquilatero(double lado) { this.lado = lado; }
    @Override public double calcularArea() { return Math.sqrt(3) * lado * lado / 4; }
    @Override public double calcularPerimetro() { return 3 * lado; }
}
public class EJ05 {
    public static void main(String[] args) {
        Figura cuadrado = new Cuadrado(3);
        Figura triangulo = new TrianguloEquilatero(2);
        System.out.printf("Cuadrado: área %.2f, perímetro %.2f%n", cuadrado.calcularArea(), cuadrado.calcularPerimetro());
        System.out.printf("Triángulo: área %.2f, perímetro %.2f%n", triangulo.calcularArea(), triangulo.calcularPerimetro());
    }
}
```

### Predice, ejecuta e interpreta

**Predicción:** ¿Por qué new Figura() no compila? ¿Qué área produce un cuadrado de lado 3?

```bash
javac EJ05.java
java EJ05
```

**Salida esperada:**

```text
Cuadrado: área 9.00, perímetro 12.00
Triángulo: área 1.73, perímetro 6.00
```

**Interpretación:** Clase y métodos abstractos. Relaciona cada parte de la salida con el método que la origina; explica qué elemento heredado o implementado intervino. Comprueba la predicción con la consola.

**Variación controlada:** Cambia lado del triángulo a 4: ¿cómo varía su área?, ¿cómo varía su perímetro?

**Error frecuente:** Omitir calcularPerimetro() en una subclase concreta produce error de compilación.

**Corrección razonada:** Implementa todos los métodos abstractos o declara la subclase abstracta si no se va a instanciar.

## T05 — Tarea espejo

**Enunciado:** Crear FiguraT05 abstracta y Rectangulo con ancho y alto; implementar calcularArea y calcularPerimetro.

**Archivo:** `T05.java` en carpeta separada. **Restricción:** no elimines la estructura de jerarquía ni sustituir la relación por código duplicado. **Pista:** identifica primero el miembro compartido y después la responsabilidad específica. **Evidencia:** captura del código, compilación y consola, más explicación de las decisiones. **Criterio:** el proyecto compila, produce el resultado propuesto y usa el concepto nuevo de EJ05 correctamente. **No copies la solución docente:** adapta la estructura trabajando las clases por separado.


---

# EJ06 — Implementar una interfaz en clases diferentes

**Objetivo técnico y problema:** Un automóvil, un atleta y una pieza de juego pueden avanzar, aunque no pertenezcan a una misma jerarquía de clases. Definiremos la interfaz IntMovil con avanzar() y mostraremos implementaciones independientes.

**Punto de partida:** carpeta independiente `EJ06`; crea `EJ06.java`. Antes de escribir, pregunta al compañero qué relación «es un» existe.

**Archivos:** `EJ06.java`; tarea espejo en `T06.java`. **Vínculo fuente:** Diapositivas 20–22.


## Paso 1 — Declarar el contrato común

**Estado previo:** aún no se ha introducido este bloque o comportamiento; trabaja en el mismo archivo antes de `public class EJ06`.

**Escribe este microbloque orientativo:**

```java
interface IntMovil {
    void avanzar();
}
```

**Qué acabas de construir y por qué:** En una interfaz básica, avanzar() es público y abstracto implícitamente. La interfaz describe una capacidad sin determinar cómo se realiza.

**Estado siguiente:** ya dispones de la pieza recién explicada. Al final del recorrido unirás los bloques en el código completo canónico indicado abajo; ese código es el que debes compilar.


## Paso 2 — Implementar dos comportamientos distintos

**Estado previo:** aún no se ha introducido este bloque o comportamiento; trabaja en el mismo archivo antes de `public class EJ06`.

**Escribe este microbloque orientativo:**

```java
class Automovil implements IntMovil {
    @Override public void avanzar() { System.out.println("Auto: rueda"); }
}
class Atleta implements IntMovil {
    @Override public void avanzar() { System.out.println("Atleta: corre"); }
}
```

**Qué acabas de construir y por qué:** implements obliga a proporcionar la operación pública; cada clase interpreta avanzar de acuerdo con su naturaleza.

**Estado siguiente:** ya dispones de la pieza recién explicada. Al final del recorrido unirás los bloques en el código completo canónico indicado abajo; ese código es el que debes compilar.


## Paso 3 — Agregar una tercera implementación y ejecutarlas

**Estado previo:** aún no se ha introducido este bloque o comportamiento; trabaja en el mismo archivo antes de `public class EJ06`.

**Escribe este microbloque orientativo:**

```java
class JuegoLudo implements IntMovil {
    @Override public void avanzar() { System.out.println("Ludo: mueve ficha"); }
}
```

**Qué acabas de construir y por qué:** La misma capacidad puede encontrarse en clases sin relación de herencia entre sí.

**Estado siguiente:** ya dispones de la pieza recién explicada. Al final del recorrido unirás los bloques en el código completo canónico indicado abajo; ese código es el que debes compilar.


## Auditoría y archivo completo al terminar EJ06

Verifica que estén presentes las declaraciones de clases, las relaciones `extends`/`implements` aplicables, constructores o métodos y una clase pública `EJ06` con `main`. Los microbloques anteriores muestran las decisiones sucesivas; el siguiente archivo reúne el estado final coherente y ejecutable, incluidos los detalles de prueba y salida que se ejecutan en `main`.

```java
interface IntMovil { void avanzar(); }
class Automovil implements IntMovil {
    @Override public void avanzar() { System.out.println("Auto: rueda"); }
}
class Atleta implements IntMovil {
    @Override public void avanzar() { System.out.println("Atleta: corre"); }
}
class JuegoLudo implements IntMovil {
    @Override public void avanzar() { System.out.println("Ludo: mueve ficha"); }
}
public class EJ06 {
    public static void main(String[] args) {
        IntMovil a = new Automovil();
        IntMovil b = new Atleta();
        IntMovil c = new JuegoLudo();
        a.avanzar(); b.avanzar(); c.avanzar();
    }
}
```

### Predice, ejecuta e interpreta

**Predicción:** ¿Comparten Automovil y Atleta una clase padre declarada aquí? ¿Por qué pueden exponerse como IntMovil?

```bash
javac EJ06.java
java EJ06
```

**Salida esperada:**

```text
Auto: rueda
Atleta: corre
Ludo: mueve ficha
```

**Interpretación:** Interfaces e implements. Relaciona cada parte de la salida con el método que la origina; explica qué elemento heredado o implementado intervino. Comprueba la predicción con la consola.

**Variación controlada:** Cambia el mensaje de Atleta y comprueba que solo cambia esa implementación.

**Error frecuente:** Implementar avanzar() sin public reduce visibilidad e incumple el contrato.

**Corrección razonada:** Escribe public void avanzar() en toda clase concreta que implemente IntMovil.

## T06 — Tarea espejo

**Enunciado:** Diseñar interfaz SaludableT06 con cuidar(); implementarla en PersonaSana y MascotaSana con respuestas diferentes.

**Archivo:** `T06.java` en carpeta separada. **Restricción:** no elimines la estructura de jerarquía ni sustituir la relación por código duplicado. **Pista:** identifica primero el miembro compartido y después la responsabilidad específica. **Evidencia:** captura del código, compilación y consola, más explicación de las decisiones. **Criterio:** el proyecto compila, produce el resultado propuesto y usa el concepto nuevo de EJ06 correctamente. **No copies la solución docente:** adapta la estructura trabajando las clases por separado.


---

# EJ07 — Integrar extends, implements y @Override en un caso único

**Objetivo técnico y problema:** Un sistema de personal debe mostrar fichas de empleados y permitir que un directivo envíe reportes. Respetaremos las responsabilidades: Directivo extiende Empleado, implementa Reportable y sobrescribe leerRegistro() sin duplicar la información básica.

**Punto de partida:** carpeta independiente `EJ07`; crea `EJ07.java`. Antes de escribir, pregunta al compañero qué relación «es un» existe.

**Archivos:** `EJ07.java`; tarea espejo en `T07.java`. **Vínculo fuente:** Derivado controlado de diapositivas 23–26.


## Paso 1 — Crear el contrato para emitir reportes

**Estado previo:** aún no se ha introducido este bloque o comportamiento; trabaja en el mismo archivo antes de `public class EJ07`.

**Escribe este microbloque orientativo:**

```java
interface Reportable {
    String generarReporte();
}
```

**Qué acabas de construir y por qué:** Reportable representa una capacidad adicional, no una superclase. Un Empleado genérico no tiene por qué generar reportes.

**Estado siguiente:** ya dispones de la pieza recién explicada. Al final del recorrido unirás los bloques en el código completo canónico indicado abajo; ese código es el que debes compilar.


## Paso 2 — Construir Empleado con un registro común

**Estado previo:** aún no se ha introducido este bloque o comportamiento; trabaja en el mismo archivo antes de `public class EJ07`.

**Escribe este microbloque orientativo:**

```java
class Empleado {
    protected String nombre;
    Empleado(String nombre) { this.nombre = nombre; }
    String leerRegistro() { return "Empleado: " + nombre; }
}
```

**Qué acabas de construir y por qué:** Se define estado común y un método concreto heredable.

**Estado siguiente:** ya dispones de la pieza recién explicada. Al final del recorrido unirás los bloques en el código completo canónico indicado abajo; ese código es el que debes compilar.


## Paso 3 — Especializar Directivo y agregar el contrato

**Estado previo:** aún no se ha introducido este bloque o comportamiento; trabaja en el mismo archivo antes de `public class EJ07`.

**Escribe este microbloque orientativo:**

```java
class Directivo extends Empleado implements Reportable {
    private String departamento;
    Directivo(String nombre, String departamento) {
        super(nombre); this.departamento = departamento;
    }
    @Override String leerRegistro() {
        return super.leerRegistro() + " | " + departamento;
    }
    @Override public String generarReporte() {
        return "Reporte de " + departamento;
    }
}
```

**Qué acabas de construir y por qué:** extends aplica a una sola clase; implements incorpora la capacidad Reportable. El override del método heredado usa super, y el del contrato es public.

**Estado siguiente:** ya dispones de la pieza recién explicada. Al final del recorrido unirás los bloques en el código completo canónico indicado abajo; ese código es el que debes compilar.


## Paso 4 — Validar ambas responsabilidades

**Estado previo:** aún no se ha introducido este bloque o comportamiento; trabaja en el mismo archivo antes de `public class EJ07`.

**Escribe este microbloque orientativo:**

```java
Directivo d = new Directivo("Ana", "TI");
System.out.println(d.leerRegistro());
System.out.println(d.generarReporte());
```

**Qué acabas de construir y por qué:** Comprobamos dos efectos: herencia reutilizada en la ficha y cumplimiento del contrato en el reporte.

**Estado siguiente:** ya dispones de la pieza recién explicada. Al final del recorrido unirás los bloques en el código completo canónico indicado abajo; ese código es el que debes compilar.


## Auditoría y archivo completo al terminar EJ07

Verifica que estén presentes las declaraciones de clases, las relaciones `extends`/`implements` aplicables, constructores o métodos y una clase pública `EJ07` con `main`. Los microbloques anteriores muestran las decisiones sucesivas; el siguiente archivo reúne el estado final coherente y ejecutable, incluidos los detalles de prueba y salida que se ejecutan en `main`.

```java
interface Reportable { String generarReporte(); }
class Empleado {
    protected String nombre;
    Empleado(String nombre) { this.nombre = nombre; }
    String leerRegistro() { return "Empleado: " + nombre; }
}
class Directivo extends Empleado implements Reportable {
    private String departamento;
    Directivo(String nombre, String departamento) {
        super(nombre); this.departamento = departamento;
    }
    @Override String leerRegistro() { return super.leerRegistro() + " | " + departamento; }
    @Override public String generarReporte() { return "Reporte de " + departamento; }
}
public class EJ07 {
    public static void main(String[] args) {
        Directivo d = new Directivo("Ana", "TI");
        System.out.println(d.leerRegistro());
        System.out.println(d.generarReporte());
    }
}
```

### Predice, ejecuta e interpreta

**Predicción:** ¿Qué palabra une Directivo con Empleado y cuál con Reportable? ¿Qué imprime el método sobrescrito?

```bash
javac EJ07.java
java EJ07
```

**Salida esperada:**

```text
Empleado: Ana | TI
Reporte de TI
```

**Interpretación:** Jerarquía + interfaces + sobrescritura. Relaciona cada parte de la salida con el método que la origina; explica qué elemento heredado o implementado intervino. Comprueba la predicción con la consola.

**Variación controlada:** Cambia el departamento a Finanzas y verifica que cambia tanto la ficha como el reporte.

**Error frecuente:** Definir generarReporte() sin public impide implementar correctamente el método público de la interfaz.

**Corrección razonada:** Declara public String generarReporte() y mantén @Override para detectar inconsistencias.

## T07 — Tarea espejo

**Enunciado:** Crear PersonaT07, Docente extends PersonaT07 implements EvaluadorT07; sobrescribir ficha con super.ficha() y definir evaluar().

**Archivo:** `T07.java` en carpeta separada. **Restricción:** no elimines la estructura de jerarquía ni sustituir la relación por código duplicado. **Pista:** identifica primero el miembro compartido y después la responsabilidad específica. **Evidencia:** captura del código, compilación y consola, más explicación de las decisiones. **Criterio:** el proyecto compila, produce el resultado propuesto y usa el concepto nuevo de EJ07 correctamente. **No copies la solución docente:** adapta la estructura trabajando las clases por separado.


---

## Cierre de la sesión

Hoy convertiste una necesidad de reutilización en una jerarquía real de clases y comprobaste que una subclase puede aprovechar estado y comportamiento ya definido. Empezaste con `Empleado` y `Directivo`; después aprendiste a inicializar correctamente la base con `super()` y a organizar una jerarquía encadenada. Cuando aparecieron necesidades diferentes, decidiste dónde correspondía usar sobrescritura y por qué `@Override` permite detectar errores en la firma del método.

También construiste una clase abstracta para exigir operaciones comunes sin inventar una implementación universal. En el ejemplo de figuras verificaste que cada cálculo corresponde a la figura concreta, y que una superclase abstracta no se instancia. Luego trabajaste con una interfaz para expresar un comportamiento que pueden compartir clases no relacionadas por herencia. En el ejercicio integrador combinaste `extends`, `implements`, `super()` y `@Override` de forma consciente, sin convertirlos en sinónimos.

Al repasar, practica tres preguntas: ¿qué comparten todas las clases de una familia?, ¿qué comportamiento necesita implementación diferente?, ¿qué capacidad pueden ofrecer clases de familias distintas? Si obtienes una salida inesperada, analiza primero el tipo real del objeto, la firma de cada método y el orden de construcción. Esas comprobaciones te ayudarán en sesiones posteriores de programación orientada a objetos.

Puedes reforzar el tema con las prácticas de **Lideratec Academy**, el blog `https://lideratecacademy.com/blog/` y el canal `https://www.youtube.com/@LideratecAcademy`.
