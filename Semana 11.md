# Sesión 11 — Colección de objetos en Java

**Curso:** Programación Orientada a Objetos (ISIL). **Sesión:** S11 / Tema 11. **Modalidad:** laboratorio guiado, 120 minutos en aula y práctica autónoma posterior. **Herramientas:** Java 21 (JDK) e IntelliJ IDEA; sin bibliotecas adicionales, Maven, Tomcat ni JSP.

**Objetivo:** registrar objetos `Estudiante` en `ArrayList`, recorrerlos con `for-each` e `Iterator`, buscar por nombre mediante `equals`, eliminar durante el recorrido usando `Iterator.remove` o aplicar `removeIf`, y controlar duplicados de `Producto` con `HashSet` definiendo `equals` y `hashCode` coherentes.

**Alcance:** la colección mantiene referencias a objetos de clases propias; no se enseñan bases de datos, interfaces gráficas, persistencia, API web ni algoritmos de ordenación.

## Apertura y resultado observable (lectura de inicio)

Al registrar estudiantes o administrar un catálogo de productos, el programa debe operar con grupos de objetos, no con variables individuales que se multipliquen cada vez que aparece una persona o un artículo nuevo. En esta sesión partiremos de dos clases sencillas, `Estudiante` y `Producto`, para comprender cómo las colecciones almacenan referencias a instancias creadas con `new`. Inicialmente construiremos una lista dinámica, agregaremos tres estudiantes y verificaremos el total. Después aprenderemos a recorrerla, localizar un nombre y eliminar elementos de dos maneras justificadas: con un iterador y con un criterio expresado mediante `removeIf`.

En la segunda parte cambiaremos la pregunta: si dos productos tienen el mismo nombre, ¿deben existir ambos dentro de un conjunto de productos únicos? Antes de usar `HashSet`, implementaremos `equals` y `hashCode` coherentes con una política explícita de identidad. Finalmente veremos cómo `HashSet` acepta o rechaza altas, comprueba pertenencia y elimina objetos. La evidencia será código Java que compila, salidas de consola que sabemos anticipar y la capacidad de explicar qué línea causa cada resultado, no una sucesión de ejemplos copiados sin interpretación.

**Al finalizar podrás** construir clases y colecciones de objetos; recorrerlas con dos técnicas; buscar por igualdad de texto; distinguir `Iterator.remove` de `removeIf`; definir igualdad lógica y su contrato hash; y comprobar unicidad mediante el retorno booleano de `HashSet.add` y el tamaño. El criterio de dominio es explicar por qué `new Producto("Impresora", 200)` no aumenta un `HashSet` que ya contiene una impresora identificada por nombre, aunque Java haya construido otra instancia.

## Agenda realista: 120 minutos

| Minutos | Trabajo | Modalidad |
|---|---|---|
| 0–10 | Comprobación de JDK, IntelliJ y proyecto | Inicio guiado |
| 10–23 | EJ01: clase Estudiante y registro | Docente + práctica |
| 23–33 | EJ02: for-each | Práctica acompañada |
| 33–43 | EJ03: Iterator | Demostración; T03 posterior |
| 43–55 | EJ04: búsqueda | Resolución y predicción |
| 55–67 | EJ05: eliminación con iterador | Resolución y corrección |
| 67–77 | EJ06: removeIf | Demostración; T06 posterior |
| 77–98 | EJ07: equals y hashCode | Explicación profunda + prueba |
| 98–114 | EJ08: HashSet y duplicados | Integración; T08 posterior |
| 114–120 | Repaso, comprobación de evidencias y dudas | Cierre |

Las ocho tareas `T01`–`T08` son **práctica espejo** que puede iniciarse en aula cuando avance el grupo y completarse posteriormente. No se presupone que el grupo termine las ocho tareas individuales y los ocho ejercicios guiados íntegramente en 120 minutos.

## Preparación reproducible del entorno y del proyecto desde cero

### Paso 0.1 — Comprobar Java 21

Abre la terminal del sistema (`cmd` o PowerShell en Windows) y escribe, una línea a la vez:

```text
java -version
javac -version
```

La primera respuesta debe identificar una instalación del runtime compatible con Java 21; la segunda debe mostrar un compilador `javac 21.x`. Si el comando `javac` no existe, puede faltar el JDK o su carpeta `bin` puede no estar en `PATH`. No basta con instalar únicamente un JRE.

### Paso 0.2 — Preparar IntelliJ IDEA

En la pantalla de bienvenida, selecciona **New Project**; si tienes un proyecto abierto, usa **File > New > Project**. Elige **Java**, escribe el nombre exacto `ISIL-POO-S11-Colecciones`, elige **Build system: IntelliJ**, selecciona **JDK: 21** y crea el proyecto sin incorporar plantillas de código adicionales. Si no aparece JDK 21, utiliza la opción **Download JDK** o **Add JDK from Disk** para enlazar una instalación autorizada de Java 21. La interfaz de IntelliJ puede variar ligeramente según versión; verifica las etiquetas disponibles.

En el panel **Project** localiza la carpeta `src`. Si no existe, créala mediante clic derecho al proyecto > **New > Directory** y márcala como carpeta de código fuente si el IDE lo pide (**Mark Directory as > Sources Root**). Para crear clases, haz clic derecho en `src` > **New > Java Class** y escribe exactamente `Estudiante`, `Producto` o `EJ01` según el ejercicio. No declares `package` en estas prácticas: todos los `.java` de la sesión permanecen en el paquete predeterminado. En cada archivo escribe el bloque desde `public class` hasta su llave de cierre; IntelliJ suele generar una estructura inicial que puedes completar.

### Paso 0.3 — Entender la estructura que iremos creando

```text
ISIL-POO-S11-Colecciones/
└── src/
    ├── Estudiante.java     ← se crea en EJ01
    ├── EJ01.java           ← registro
    ├── EJ02.java           ← for-each
    ├── EJ03.java           ← Iterator
    ├── EJ04.java           ← búsqueda equals
    ├── EJ05.java           ← eliminación Iterator.remove
    ├── EJ06.java           ← eliminación removeIf
    ├── Producto.java       ← se crea en EJ07
    ├── EJ07.java           ← identidad lógica
    └── EJ08.java           ← HashSet
```

No crees de golpe todos los archivos: sigue el orden EJ01 a EJ08. `Estudiante.java` se reutiliza sin modificaciones entre EJ02 y EJ06, y `Producto.java` se reutiliza de EJ07 a EJ08. La independencia de los métodos `main` permite ejecutar cada escenario sin que el estado de uno altere el siguiente.

### Paso 0.4 — Entender la plantilla Java mínima

Un archivo `EJxx.java` contiene una declaración `public class EJxx`, y dentro `public static void main(String[] args)`; el identificador `EJxx` debe coincidir exactamente con el nombre del archivo. `main` es el punto de entrada que Java ejecuta. Escribe los `import java.util...;` al inicio del archivo, **por encima** de `public class`. Las instrucciones del ejemplo van **dentro** de las llaves de `main`, no después del cierre de la clase. Las llaves muestran qué bloque contiene a otro; los puntos y coma finalizan las instrucciones.

Para ejecutar un escenario en IntelliJ, abre `EJ01.java`, haz clic en el triángulo de ejecución junto a `main` y selecciona **Run 'EJ01.main()'** (o la opción equivalente). Lee la pestaña **Run**: debe mostrar la salida prevista en el ejemplo y ningún error de compilación.

**Alternativa terminal:** dentro de la raíz del proyecto, crea la carpeta `out` si no existe (`mkdir out`) y compila con `javac -encoding UTF-8 -d out src/*.java` en una terminal de Bash, o `javac -encoding UTF-8 -d out src\*.java` en `cmd` de Windows. Ejecuta `java -cp out EJ01`. Reemplaza EJ01 por EJ02…EJ08. Si compilas antes de haber creado las clases que se utilizan, completa primero el archivo faltante y vuelve a intentar.

**Prueba inicial:** crea `src/EJ01.java` y `src/Estudiante.java` durante EJ01; compila y ejecuta. No necesitas instalar una base de datos, servidor de aplicaciones, Maven, extensiones externas ni conectividad permanente a internet una vez que el JDK y el IDE funcionan.


---

# EJ01 — Crear Estudiante y registrar objetos en ArrayList

## Objetivo técnico — lectura docente

Una aplicación académica debe registrar estudiantes sin crear una variable diferente para cada persona. Primero modelaremos los datos y el constructor de Estudiante; después escribiremos métodos de consulta y una representación textual. Por último crearemos una lista tipada y añadiremos tres objetos. No estudiaremos aún la búsqueda ni la eliminación: necesitamos comprobar que el almacenamiento inicial funciona y que el total registrado responde a las tres altas realizadas.

## Qué problema concreto resolveremos

¿Cómo guardar tres estudiantes en una sola estructura y saber cuántos fueron registrados?

**Archivos y punto de partida:** `src/EJ01.java` y `src/Estudiante.java` (se crean por primera vez). Los imports se escriben encima de la declaración de clase. Cada segmento debe quedar dentro del bloque indicado; la versión completa para cotejar aparece **solo después** de explicar las partes.

## Preparar el archivo ejecutable antes de los microbloques

Crea el archivo y escribe esta estructura inicial. El comentario marca el lugar donde sustituirás, en orden, los fragmentos siguientes. `main` es el punto de entrada y las importaciones habilitan los tipos de colección usados en el escenario. Los métodos de Estudiante y Producto se implementan en sus archivos propios.

```java
import java.util.ArrayList;
import java.util.List;

public class EJ01 {
    public static void main(String[] args) {
        // Escribir los microbloques indicados aquí.
    }
}
```

## Paso 1 — Plantear una hipótesis comprobable

Antes de editar, responde: ¿Cómo guardar tres estudiantes en una sola estructura y saber cuántos fueron registrados? Explica qué parte de la colección cambiará y qué salida permitirá demostrarlo; no valides únicamente que el programa no muestra errores.

### Paso 2 — Definir qué datos representa el estudiante

**Antes de escribir.** Una entidad estudiante tiene dos atributos: nombre identifica lo que mostraremos y edad permite practicar decisiones posteriores.

**Lugar exacto.** src/Estudiante.java, inmediatamente después de `public class Estudiante {`. Si ese archivo no existe, créalo en `src` mediante **New > Java Class**, conserva el nombre indicado y prepara las llaves de la clase y de `main` cuando corresponda.

**Escribe ahora:**

```java
    private String nombre;
    private int edad;
```

**Explicación técnica mientras lo escribimos.** Una entidad estudiante tiene dos atributos: nombre identifica lo que mostraremos y edad permite practicar decisiones posteriores. Los hacemos privados para que el estado se consulte mediante métodos, no accediendo a los campos desde cualquier clase.

**Estado o evidencia tras este microbloque.** El objeto dispone de dos campos, pero todavía no existe un mecanismo para recibir sus valores.

### Paso 3 — Construir la inicialización con un constructor

**Antes de escribir.** El constructor recibe los valores escritos cuando se ejecuta `new Estudiante(...)`.

**Lugar exacto.** src/Estudiante.java, debajo de los atributos y antes de la última llave. Si ese archivo no existe, créalo en `src` mediante **New > Java Class**, conserva el nombre indicado y prepara las llaves de la clase y de `main` cuando corresponda.

**Escribe ahora:**

```java
    public Estudiante(String nombre, int edad) {
        this.nombre = nombre;
        this.edad = edad;
    }
```

**Explicación técnica mientras lo escribimos.** El constructor recibe los valores escritos cuando se ejecuta `new Estudiante(...)`. La palabra `this` distingue el campo del objeto del parámetro con igual nombre; sin asignación, los atributos conservarían valores por defecto.

**Estado o evidencia tras este microbloque.** Al crear `new Estudiante("Pedro",21)` el objeto retiene nombre y edad.

### Paso 4 — Ofrecer consulta y una presentación comprensible

**Antes de escribir.** Los getters devuelven un dato sin exponer el atributo.

**Lugar exacto.** src/Estudiante.java, debajo del constructor y dentro de la clase. Si ese archivo no existe, créalo en `src` mediante **New > Java Class**, conserva el nombre indicado y prepara las llaves de la clase y de `main` cuando corresponda.

**Escribe ahora:**

```java
    public String getNombre() {
        return nombre;
    }

    public int getEdad() {
        return edad;
    }

    @Override
    public String toString() {
        return "Nombre: " + nombre + " - Edad: " + edad;
    }
```

**Explicación técnica mientras lo escribimos.** Los getters devuelven un dato sin exponer el atributo. `toString()` devuelve una descripción en vez de mostrar una referencia técnica del objeto; `@Override` advierte al compilador que estamos redefiniendo un método heredado de Object.

**Estado o evidencia tras este microbloque.** `System.out.println(estudiante)` podrá imprimir nombre y edad de forma legible.

### Paso 5 — Crear la colección tipada

**Antes de escribir.** `List<Estudiante>` es el contrato que restringe los elementos a Estudiante y `new ArrayList<>()` construye la lista vacía.

**Lugar exacto.** src/EJ01.java, dentro de `main`, como primera instrucción. Si ese archivo no existe, créalo en `src` mediante **New > Java Class**, conserva el nombre indicado y prepara las llaves de la clase y de `main` cuando corresponda.

**Escribe ahora:**

```java
        List<Estudiante> estudiantes = new ArrayList<>();
```

**Explicación técnica mientras lo escribimos.** `List<Estudiante>` es el contrato que restringe los elementos a Estudiante y `new ArrayList<>()` construye la lista vacía. Los imports de List y ArrayList habilitan sus nombres, mientras que `estudiantes` es la variable que conserva la referencia a la colección.

**Estado o evidencia tras este microbloque.** La lista inicia vacía, con tamaño cero.

### Paso 6 — Registrar tres instancias y medir el resultado

**Antes de escribir.** Cada `new` construye un estudiante distinto y `add` incorpora su referencia a la lista.

**Lugar exacto.** src/EJ01.java, dentro de `main`, después de la declaración de la lista. Si ese archivo no existe, créalo en `src` mediante **New > Java Class**, conserva el nombre indicado y prepara las llaves de la clase y de `main` cuando corresponda.

**Escribe ahora:**

```java
        estudiantes.add(new Estudiante("Pedro", 21));
        estudiantes.add(new Estudiante("Rosa", 20));
        estudiantes.add(new Estudiante("Antonio", 23));
        System.out.println("Registrados: " + estudiantes.size());
```

**Explicación técnica mientras lo escribimos.** Cada `new` construye un estudiante distinto y `add` incorpora su referencia a la lista. `size()` mide cuántos elementos contiene. Las edades no se suman y los nombres no se convierten en claves; el resultado visible debe ser tres registros.

**Estado o evidencia tras este microbloque.** Tamaño antes=0; luego de tres llamadas a `add` el tamaño es 3 y se imprime «Registrados: 3».

## Auditoría del artefacto antes de ejecutar

- Confirma que el archivo se llama `EJ01.java` y la clase pública `EJ01`; los `import` preceden a la clase, `main` es el punto de entrada y sus llaves están equilibradas.
- Además, comprueba que `Estudiante.java` contiene campos, constructor, getters y `toString`. Los campos están declarados dentro de la clase y fuera de cualquier método.
- Contrasta cada bloque funcional de arriba con la versión completa; no debe haber una instrucción de comportamiento que aparezca por primera vez sin haberse explicado.

## Archivo `src/Estudiante.java` completo tras los microbloques

```java
public class Estudiante {
    private String nombre;
    private int edad;

    public Estudiante(String nombre, int edad) {
        this.nombre = nombre;
        this.edad = edad;
    }

    public String getNombre() {
        return nombre;
    }

    public int getEdad() {
        return edad;
    }

    @Override
    public String toString() {
        return "Nombre: " + nombre + " - Edad: " + edad;
    }
}
```

## Archivo `src/EJ01.java` completo al terminar

```java
import java.util.ArrayList;
import java.util.List;

public class EJ01 {
    public static void main(String[] args) {
List<Estudiante> estudiantes = new ArrayList<>();
estudiantes.add(new Estudiante("Pedro", 21));
estudiantes.add(new Estudiante("Rosa", 20));
estudiantes.add(new Estudiante("Antonio", 23));
System.out.println("Registrados: " + estudiantes.size());
    }
}
```

## Antes de ejecutar: predicción

1. ¿Cuántos elementos quedan o se recorren al terminar EJ01, y por qué?
2. ¿Qué instrucción precisa causa la salida visible y qué método o condición interviene?
3. Si cambias el dato de prueba indicado a continuación, ¿cuál será el primer resultado diferente?

## Ejecutar y validar

En IntelliJ, ejecuta `EJ01.main()` con el triángulo verde. Desde la terminal de la raíz del proyecto, tras compilar con `javac -encoding UTF-8 -d out src/*.java` (Bash) o `javac -encoding UTF-8 -d out src\*.java` (Windows), ejecuta `java -cp out EJ01`. Comprueba literalmente la salida o, en HashSet, comprueba el conjunto de productos sin imponer orden.

**Salida esperada:**

```text
Registrados: 3
```

**Interpretación.** Cada `new` construye un estudiante distinto y `add` incorpora su referencia a la lista. `size()` mide cuántos elementos contiene. Las edades no se suman y los nombres no se convierten en claves; el resultado visible debe ser tres registros. Tamaño antes=0; luego de tres llamadas a `add` el tamaño es 3 y se imprime «Registrados: 3». La prueba vale cuando puedes justificar el cambio de estado, no solamente repetir el texto de la consola.

**Variación A — prueba de transferencia.** Cambia el nombre de Antonio por Laura y verifica que el total permanece 3; añade un cuarto estudiante y confirma que pasa a 4.

**Variación B — comprobación negativa.** Construir Estudiante sin constructor de dos parámetros. Identifica la condición o llamada responsable, sin dejar una versión errónea como resultado final.

## Error o caso límite controlado y corrección

**Situación:** Construir Estudiante sin constructor de dos parámetros. **Causa:** El compilador no encuentra un constructor compatible con `new Estudiante("Pedro", 21)`. **Corrección:** Agrega el constructor mostrado y verifica que asigna los dos campos con `this`. Al ejecutar, el total será 3.

## Comprueba que puedes explicarlo

Explica la relación entre el dato inicial y el resultado; identifica la línea exacta que recorre, compara, elimina o impide un duplicado, según corresponda; y justifica por qué la validación propuesta detecta un error real.

## T01 — Tarea espejo: Comprobar que una lista permite registros repetidos

**Enunciado:** Crea cuatro estudiantes: Elena(22), Luis(19), Elena(22) y Nora(24). Regístralos en un ArrayList y muestra el total. Explica por qué el segundo registro de Elena permanece.

**Archivo a construir:** `src/T01.java`; conserva la clase `Estudiante` o `Producto` que ya desarrollaste. **Restricción:** Conserva la clase Estudiante; utiliza add y size, sin HashSet.

**Ruta de trabajo:** crea una clase Java con `main`, inicia los objetos indicados, añade el mecanismo específico aprendido en EJ01 y muestra una comprobación visible. **Pista:** Recuerda que ArrayList no impide objetos repetidos.

**Evidencia y criterio de aceptación:** Debe aparecer «Registros con repetición: 4». La solución debe compilar; el resultado se explica en una oración señalando qué método causó el comportamiento. Esta tarea es para que la resuelvas: la solución docente no se incluye en esta guía.


---

# EJ02 — Recorrer objetos de una lista con for-each

## Objetivo técnico — lectura docente

Tras crear estudiantes, necesitamos presentar sus datos para que alguien pueda verificar el contenido de la colección. Recuperaremos la lista con Pedro, Rosa y Antonio, añadiremos un for-each y utilizaremos la representación del objeto para imprimir cada registro. El valor de este ejemplo no es crear nuevos objetos, sino comprender por qué el recorrido entrega sucesivamente cada referencia y por qué no es necesario administrar un índice.

## Qué problema concreto resolveremos

¿Cómo visualizar todos los objetos sin crear manualmente posiciones 0, 1 y 2?

**Archivos y punto de partida:** `src/EJ02.java` y `src/Estudiante.java` existente. Los imports se escriben encima de la declaración de clase. Cada segmento debe quedar dentro del bloque indicado; la versión completa para cotejar aparece **solo después** de explicar las partes.

## Preparar el archivo ejecutable antes de los microbloques

Crea el archivo y escribe esta estructura inicial. El comentario marca el lugar donde sustituirás, en orden, los fragmentos siguientes. `main` es el punto de entrada y las importaciones habilitan los tipos de colección usados en el escenario. Los métodos de Estudiante y Producto se implementan en sus archivos propios.

```java
import java.util.ArrayList;
import java.util.List;

public class EJ02 {
    public static void main(String[] args) {
        // Escribir los microbloques indicados aquí.
    }
}
```

## Paso 1 — Plantear una hipótesis comprobable

Antes de editar, responde: ¿Cómo visualizar todos los objetos sin crear manualmente posiciones 0, 1 y 2? Explica qué parte de la colección cambiará y qué salida permitirá demostrarlo; no valides únicamente que el programa no muestra errores.

### Paso 2 — Preparar los objetos que vamos a visualizar

**Antes de escribir.** Recuperamos el patrón de creación anterior: existe una colección con tres referencias a Estudiante y cada instancia conserva sus atributos.

**Lugar exacto.** src/EJ02.java, dentro de `main`, declarar la lista y registrar las tres instancias. Si ese archivo no existe, créalo en `src` mediante **New > Java Class**, conserva el nombre indicado y prepara las llaves de la clase y de `main` cuando corresponda.

**Escribe ahora:**

```java
        List<Estudiante> estudiantes = new ArrayList<>();
        estudiantes.add(new Estudiante("Pedro", 21));
        estudiantes.add(new Estudiante("Rosa", 20));
        estudiantes.add(new Estudiante("Antonio", 23));
```

**Explicación técnica mientras lo escribimos.** Recuperamos el patrón de creación anterior: existe una colección con tres referencias a Estudiante y cada instancia conserva sus atributos. Este ejemplo no cambia los datos; cambia la forma de leerlos uno por uno.

**Estado o evidencia tras este microbloque.** El almacenamiento contiene tres elementos en orden de inserción.

### Paso 3 — Recorrer cada referencia sin controlar índices

**Antes de escribir.** En cada vuelta, `estudiante` representa el elemento actual de `estudiantes`.

**Lugar exacto.** src/EJ02.java, inmediatamente después del tercer `add` dentro de `main`. Si ese archivo no existe, créalo en `src` mediante **New > Java Class**, conserva el nombre indicado y prepara las llaves de la clase y de `main` cuando corresponda.

**Escribe ahora:**

```java
        for (Estudiante estudiante : estudiantes) {
            System.out.println(estudiante);
        }
```

**Explicación técnica mientras lo escribimos.** En cada vuelta, `estudiante` representa el elemento actual de `estudiantes`. Los dos puntos del for-each significan “tomar elementos de”; `println` invoca la representación `toString()` del objeto. La lista permanece intacta.

**Estado o evidencia tras este microbloque.** Se imprimen tres líneas: Pedro, Rosa, Antonio, con sus edades.

## Auditoría del artefacto antes de ejecutar

- Confirma que el archivo se llama `EJ02.java` y la clase pública `EJ02`; los `import` preceden a la clase, `main` es el punto de entrada y sus llaves están equilibradas.
- Contrasta cada bloque funcional de arriba con la versión completa; no debe haber una instrucción de comportamiento que aparezca por primera vez sin haberse explicado.

## Archivo `src/EJ02.java` completo al terminar

```java
import java.util.ArrayList;
import java.util.List;

public class EJ02 {
    public static void main(String[] args) {
List<Estudiante> estudiantes = new ArrayList<>();
estudiantes.add(new Estudiante("Pedro", 21));
estudiantes.add(new Estudiante("Rosa", 20));
estudiantes.add(new Estudiante("Antonio", 23));
for (Estudiante estudiante : estudiantes) {
    System.out.println(estudiante);
}
    }
}
```

## Antes de ejecutar: predicción

1. ¿Cuántos elementos quedan o se recorren al terminar EJ02, y por qué?
2. ¿Qué instrucción precisa causa la salida visible y qué método o condición interviene?
3. Si cambias el dato de prueba indicado a continuación, ¿cuál será el primer resultado diferente?

## Ejecutar y validar

En IntelliJ, ejecuta `EJ02.main()` con el triángulo verde. Desde la terminal de la raíz del proyecto, tras compilar con `javac -encoding UTF-8 -d out src/*.java` (Bash) o `javac -encoding UTF-8 -d out src\*.java` (Windows), ejecuta `java -cp out EJ02`. Comprueba literalmente la salida o, en HashSet, comprueba el conjunto de productos sin imponer orden.

**Salida esperada:**

```text
Nombre: Pedro - Edad: 21
Nombre: Rosa - Edad: 20
Nombre: Antonio - Edad: 23
```

**Interpretación.** En cada vuelta, `estudiante` representa el elemento actual de `estudiantes`. Los dos puntos del for-each significan “tomar elementos de”; `println` invoca la representación `toString()` del objeto. La lista permanece intacta. Se imprimen tres líneas: Pedro, Rosa, Antonio, con sus edades. La prueba vale cuando puedes justificar el cambio de estado, no solamente repetir el texto de la consola.

**Variación A — prueba de transferencia.** Cambia el orden de registro en la lista y anticipa el nuevo orden de impresión; no alteres el cuerpo del for-each.

**Variación B — comprobación negativa.** Imprimir el nombre de la clase o una referencia poco descriptiva. Identifica la condición o llamada responsable, sin dejar una versión errónea como resultado final.

## Error o caso límite controlado y corrección

**Situación:** Imprimir el nombre de la clase o una referencia poco descriptiva. **Causa:** Si toString no se sobrescribe, `println(objeto)` puede mostrar una descripción técnica que no sirve para inspeccionar el registro. **Corrección:** Revisa la implementación completa de toString en Estudiante y vuelve a ejecutar el mismo for-each.

## Comprueba que puedes explicarlo

Explica la relación entre el dato inicial y el resultado; identifica la línea exacta que recorre, compara, elimina o impide un duplicado, según corresponda; y justifica por qué la validación propuesta detecta un error real.

## T02 — Tarea espejo: Mostrar solo estudiantes de edad al menos 21

**Enunciado:** Recorre Elena(22), Luis(19) y Nora(24) con for-each; imprime únicamente los que cumplen edad >= 21. Justifica por qué Luis no aparece.

**Archivo a construir:** `src/T02.java`; conserva la clase `Estudiante` o `Producto` que ya desarrollaste. **Restricción:** No modifiques la colección mientras usas for-each.

**Ruta de trabajo:** crea una clase Java con `main`, inicia los objetos indicados, añade el mecanismo específico aprendido en EJ02 y muestra una comprobación visible. **Pista:** La condición va dentro del bloque for-each.

**Evidencia y criterio de aceptación:** Aparecen Elena y Nora; Luis no aparece. La solución debe compilar; el resultado se explica en una oración señalando qué método causó el comportamiento. Esta tarea es para que la resuelvas: la solución docente no se incluye en esta guía.


---

# EJ03 — Recorrer secuencialmente con Iterator

## Objetivo técnico — lectura docente

El recorrido anterior era breve, pero algunas operaciones requieren controlar explícitamente cuándo hay un elemento disponible y cuándo se avanza. Vamos a obtener un Iterator de la misma lista, verificar hasNext y recibir cada Estudiante con next. Al final comprobaremos que las tres referencias aparecen exactamente una vez y distinguiremos preguntar por la disponibilidad de consumir realmente el objeto.

## Qué problema concreto resolveremos

¿Cómo sabemos si existe otro objeto antes de avanzar un cursor de recorrido?

**Archivos y punto de partida:** `src/EJ03.java` y `src/Estudiante.java` existente. Los imports se escriben encima de la declaración de clase. Cada segmento debe quedar dentro del bloque indicado; la versión completa para cotejar aparece **solo después** de explicar las partes.

## Preparar el archivo ejecutable antes de los microbloques

Crea el archivo y escribe esta estructura inicial. El comentario marca el lugar donde sustituirás, en orden, los fragmentos siguientes. `main` es el punto de entrada y las importaciones habilitan los tipos de colección usados en el escenario. Los métodos de Estudiante y Producto se implementan en sus archivos propios.

```java
import java.util.ArrayList;
import java.util.List;
import java.util.Iterator;

public class EJ03 {
    public static void main(String[] args) {
        // Escribir los microbloques indicados aquí.
    }
}
```

## Paso 1 — Plantear una hipótesis comprobable

Antes de editar, responde: ¿Cómo sabemos si existe otro objeto antes de avanzar un cursor de recorrido? Explica qué parte de la colección cambiará y qué salida permitirá demostrarlo; no valides únicamente que el programa no muestra errores.

### Paso 2 — Preparar el estado inicial de recorrido

**Antes de escribir.** Volvemos a usar la misma colección para aislar la diferencia entre for-each e Iterator: no cambia qué se guarda, solo quién controla el avance al siguiente elemento.

**Lugar exacto.** src/EJ03.java, primeras instrucciones de `main`. Si ese archivo no existe, créalo en `src` mediante **New > Java Class**, conserva el nombre indicado y prepara las llaves de la clase y de `main` cuando corresponda.

**Escribe ahora:**

```java
        List<Estudiante> estudiantes = new ArrayList<>();
        estudiantes.add(new Estudiante("Pedro", 21));
        estudiantes.add(new Estudiante("Rosa", 20));
        estudiantes.add(new Estudiante("Antonio", 23));
```

**Explicación técnica mientras lo escribimos.** Volvemos a usar la misma colección para aislar la diferencia entre for-each e Iterator: no cambia qué se guarda, solo quién controla el avance al siguiente elemento.

**Estado o evidencia tras este microbloque.** La colección contiene tres estudiantes.

### Paso 3 — Solicitar un iterador posicionado antes del primer objeto

**Antes de escribir.** La variable `iterador` contiene un cursor lógico de recorrido.

**Lugar exacto.** src/EJ03.java, después de los tres `add` dentro de `main`. Si ese archivo no existe, créalo en `src` mediante **New > Java Class**, conserva el nombre indicado y prepara las llaves de la clase y de `main` cuando corresponda.

**Escribe ahora:**

```java
        Iterator<Estudiante> iterador = estudiantes.iterator();
```

**Explicación técnica mientras lo escribimos.** La variable `iterador` contiene un cursor lógico de recorrido. La llamada `iterator()` lo obtiene de esta colección; aún no se ha entregado ningún estudiante mediante `next()`. Importar `java.util.Iterator` permite utilizar el tipo.

**Estado o evidencia tras este microbloque.** Estado de recorrido: 0 objetos entregados.

### Paso 4 — Preguntar y avanzar de forma segura

**Antes de escribir.** `hasNext()` es la condición que evita solicitar un elemento inexistente; cada `next()` devuelve uno y avanza el iterador.

**Lugar exacto.** src/EJ03.java, después de declarar `iterador` dentro de `main`. Si ese archivo no existe, créalo en `src` mediante **New > Java Class**, conserva el nombre indicado y prepara las llaves de la clase y de `main` cuando corresponda.

**Escribe ahora:**

```java
        while (iterador.hasNext()) {
            Estudiante actual = iterador.next();
            System.out.println(actual);
        }
```

**Explicación técnica mientras lo escribimos.** `hasNext()` es la condición que evita solicitar un elemento inexistente; cada `next()` devuelve uno y avanza el iterador. La variable `actual` solo existe dentro del ciclo. Si llamamos a `next()` sin comprobar disponibilidad podemos producir NoSuchElementException.

**Estado o evidencia tras este microbloque.** Se visitan los tres objetos una sola vez; al terminar, `hasNext()` ya es false.

## Auditoría del artefacto antes de ejecutar

- Confirma que el archivo se llama `EJ03.java` y la clase pública `EJ03`; los `import` preceden a la clase, `main` es el punto de entrada y sus llaves están equilibradas.
- Contrasta cada bloque funcional de arriba con la versión completa; no debe haber una instrucción de comportamiento que aparezca por primera vez sin haberse explicado.

## Archivo `src/EJ03.java` completo al terminar

```java
import java.util.ArrayList;
import java.util.List;
import java.util.Iterator;

public class EJ03 {
    public static void main(String[] args) {
List<Estudiante> estudiantes = new ArrayList<>();
estudiantes.add(new Estudiante("Pedro", 21));
estudiantes.add(new Estudiante("Rosa", 20));
estudiantes.add(new Estudiante("Antonio", 23));
Iterator<Estudiante> iterador = estudiantes.iterator();
while (iterador.hasNext()) {
    Estudiante actual = iterador.next();
    System.out.println(actual);
}
    }
}
```

## Antes de ejecutar: predicción

1. ¿Cuántos elementos quedan o se recorren al terminar EJ03, y por qué?
2. ¿Qué instrucción precisa causa la salida visible y qué método o condición interviene?
3. Si cambias el dato de prueba indicado a continuación, ¿cuál será el primer resultado diferente?

## Ejecutar y validar

En IntelliJ, ejecuta `EJ03.main()` con el triángulo verde. Desde la terminal de la raíz del proyecto, tras compilar con `javac -encoding UTF-8 -d out src/*.java` (Bash) o `javac -encoding UTF-8 -d out src\*.java` (Windows), ejecuta `java -cp out EJ03`. Comprueba literalmente la salida o, en HashSet, comprueba el conjunto de productos sin imponer orden.

**Salida esperada:**

```text
Nombre: Pedro - Edad: 21
Nombre: Rosa - Edad: 20
Nombre: Antonio - Edad: 23
```

**Interpretación.** `hasNext()` es la condición que evita solicitar un elemento inexistente; cada `next()` devuelve uno y avanza el iterador. La variable `actual` solo existe dentro del ciclo. Si llamamos a `next()` sin comprobar disponibilidad podemos producir NoSuchElementException. Se visitan los tres objetos una sola vez; al terminar, `hasNext()` ya es false. La prueba vale cuando puedes justificar el cambio de estado, no solamente repetir el texto de la consola.

**Variación A — prueba de transferencia.** Agrega un cuarto estudiante y explica cuántas veces será true hasNext y cuántas veces se ejecutará next.

**Variación B — comprobación negativa.** Llamar a next una vez adicional sin comprobar hasNext. Identifica la condición o llamada responsable, sin dejar una versión errónea como resultado final.

## Error o caso límite controlado y corrección

**Situación:** Llamar a next una vez adicional sin comprobar hasNext. **Causa:** El iterador no dispone de otro elemento y `next` puede lanzar NoSuchElementException. **Corrección:** Conserva `while(iterador.hasNext())` como guardia de cada llamada a `next`. No dejes el error en el artefacto final.

## Comprueba que puedes explicarlo

Explica la relación entre el dato inicial y el resultado; identifica la línea exacta que recorre, compara, elimina o impide un duplicado, según corresponda; y justifica por qué la validación propuesta detecta un error real.

## T03 — Tarea espejo: Contar visitas reales con Iterator

**Enunciado:** Recorre Elena(22), Luis(19) y Nora(24) mediante iterator(), hasNext() y next(), imprime nombres y lleva un contador de objetos visitados.

**Archivo a construir:** `src/T03.java`; conserva la clase `Estudiante` o `Producto` que ya desarrollaste. **Restricción:** No utilices índices ni conviertas la lista en arreglo.

**Ruta de trabajo:** crea una clase Java con `main`, inicia los objetos indicados, añade el mecanismo específico aprendido en EJ03 y muestra una comprobación visible. **Pista:** Incrementa el contador una vez después de cada next().

**Evidencia y criterio de aceptación:** Se ven tres nombres y «Total visitados: 3». La solución debe compilar; el resultado se explica en una oración señalando qué método causó el comportamiento. Esta tarea es para que la resuelvas: la solución docente no se incluye en esta guía.


---

# EJ04 — Buscar un estudiante mediante String.equals

## Objetivo técnico — lectura docente

Una lista de estudiantes solo es útil si podemos localizar un registro concreto. Construiremos una búsqueda por el texto del nombre, diferenciando el valor a buscar de la señal booleana que indica un hallazgo. Revisaremos cada estudiante hasta encontrar Rosa y demostraremos también qué debe ocurrir cuando el nombre solicitado no exista. El criterio de éxito será una respuesta de consola correcta para ambos escenarios, sin confundir la identidad del objeto con igualdad de texto.

## Qué problema concreto resolveremos

¿Cómo distinguir un nombre hallado de uno inexistente usando igualdad textual?

**Archivos y punto de partida:** `src/EJ04.java` y `src/Estudiante.java` existente. Los imports se escriben encima de la declaración de clase. Cada segmento debe quedar dentro del bloque indicado; la versión completa para cotejar aparece **solo después** de explicar las partes.

## Preparar el archivo ejecutable antes de los microbloques

Crea el archivo y escribe esta estructura inicial. El comentario marca el lugar donde sustituirás, en orden, los fragmentos siguientes. `main` es el punto de entrada y las importaciones habilitan los tipos de colección usados en el escenario. Los métodos de Estudiante y Producto se implementan en sus archivos propios.

```java
import java.util.ArrayList;
import java.util.List;

public class EJ04 {
    public static void main(String[] args) {
        // Escribir los microbloques indicados aquí.
    }
}
```

## Paso 1 — Plantear una hipótesis comprobable

Antes de editar, responde: ¿Cómo distinguir un nombre hallado de uno inexistente usando igualdad textual? Explica qué parte de la colección cambiará y qué salida permitirá demostrarlo; no valides únicamente que el programa no muestra errores.

### Paso 2 — Preparar la colección que contiene al candidato

**Antes de escribir.** Necesitamos buscar un nombre entre estudiantes que ya están registrados; la lista contiene nombres diferentes y uno coincide exactamente con el valor objetivo.

**Lugar exacto.** src/EJ04.java, primeras instrucciones de `main`. Si ese archivo no existe, créalo en `src` mediante **New > Java Class**, conserva el nombre indicado y prepara las llaves de la clase y de `main` cuando corresponda.

**Escribe ahora:**

```java
        List<Estudiante> estudiantes = new ArrayList<>();
        estudiantes.add(new Estudiante("Pedro", 21));
        estudiantes.add(new Estudiante("Rosa", 20));
        estudiantes.add(new Estudiante("Antonio", 23));
```

**Explicación técnica mientras lo escribimos.** Necesitamos buscar un nombre entre estudiantes que ya están registrados; la lista contiene nombres diferentes y uno coincide exactamente con el valor objetivo.

**Estado o evidencia tras este microbloque.** Tenemos tres registros, pero aún no sabemos en qué elemento se encuentra Rosa.

### Paso 3 — Separar el nombre buscado del indicador de éxito

**Antes de escribir.** `buscado` almacena el criterio textual.

**Lugar exacto.** src/EJ04.java, después del tercer `add`. Si ese archivo no existe, créalo en `src` mediante **New > Java Class**, conserva el nombre indicado y prepara las llaves de la clase y de `main` cuando corresponda.

**Escribe ahora:**

```java
        String buscado = "Rosa";
        boolean encontrado = false;
```

**Explicación técnica mientras lo escribimos.** `buscado` almacena el criterio textual. `encontrado` registra una decisión que todavía no ocurrió, por eso empieza en false. Esta separación nos permite informar claramente cuando no exista coincidencia.

**Estado o evidencia tras este microbloque.** Antes del recorrido, no hay hallazgo confirmado.

### Paso 4 — Comparar contenido textual y terminar al encontrar

**Antes de escribir.** `getNombre()` devuelve el texto del objeto actual y `equals(buscado)` compara contenido de caracteres.

**Lugar exacto.** src/EJ04.java, debajo de `boolean encontrado = false;`. Si ese archivo no existe, créalo en `src` mediante **New > Java Class**, conserva el nombre indicado y prepara las llaves de la clase y de `main` cuando corresponda.

**Escribe ahora:**

```java
        for (Estudiante estudiante : estudiantes) {
            if (estudiante.getNombre().equals(buscado)) {
                System.out.println("Encontrado: " + estudiante);
                encontrado = true;
                break;
            }
        }
```

**Explicación técnica mientras lo escribimos.** `getNombre()` devuelve el texto del objeto actual y `equals(buscado)` compara contenido de caracteres. `==` no expresa esta intención para String. Si coincide, imprimimos el registro, marcamos éxito y `break` detiene búsquedas innecesarias.

**Estado o evidencia tras este microbloque.** Para los datos del ejemplo se encuentra a Rosa y se fija encontrado=true.

### Paso 5 — Cubrir la búsqueda sin resultados

**Antes de escribir.** El signo `!` niega el valor booleano; si ninguna comparación cambió el indicador, mostramos una salida verificable.

**Lugar exacto.** src/EJ04.java, después del cierre del `for` dentro de `main`. Si ese archivo no existe, créalo en `src` mediante **New > Java Class**, conserva el nombre indicado y prepara las llaves de la clase y de `main` cuando corresponda.

**Escribe ahora:**

```java
        if (!encontrado) {
            System.out.println("No encontrado: " + buscado);
        }
```

**Explicación técnica mientras lo escribimos.** El signo `!` niega el valor booleano; si ninguna comparación cambió el indicador, mostramos una salida verificable. Este bloque no imprime nada cuando Rosa sí fue localizada.

**Estado o evidencia tras este microbloque.** Con buscado=Rosa hay una sola línea; con buscado=Mario aparece No encontrado: Mario.

## Auditoría del artefacto antes de ejecutar

- Confirma que el archivo se llama `EJ04.java` y la clase pública `EJ04`; los `import` preceden a la clase, `main` es el punto de entrada y sus llaves están equilibradas.
- Contrasta cada bloque funcional de arriba con la versión completa; no debe haber una instrucción de comportamiento que aparezca por primera vez sin haberse explicado.

## Archivo `src/EJ04.java` completo al terminar

```java
import java.util.ArrayList;
import java.util.List;

public class EJ04 {
    public static void main(String[] args) {
List<Estudiante> estudiantes = new ArrayList<>();
estudiantes.add(new Estudiante("Pedro", 21));
estudiantes.add(new Estudiante("Rosa", 20));
estudiantes.add(new Estudiante("Antonio", 23));
String buscado = "Rosa";
boolean encontrado = false;
for (Estudiante estudiante : estudiantes) {
    if (estudiante.getNombre().equals(buscado)) {
        System.out.println("Encontrado: " + estudiante);
        encontrado = true;
        break;
    }
}
if (!encontrado) {
    System.out.println("No encontrado: " + buscado);
}
    }
}
```

## Antes de ejecutar: predicción

1. ¿Cuántos elementos quedan o se recorren al terminar EJ04, y por qué?
2. ¿Qué instrucción precisa causa la salida visible y qué método o condición interviene?
3. Si cambias el dato de prueba indicado a continuación, ¿cuál será el primer resultado diferente?

## Ejecutar y validar

En IntelliJ, ejecuta `EJ04.main()` con el triángulo verde. Desde la terminal de la raíz del proyecto, tras compilar con `javac -encoding UTF-8 -d out src/*.java` (Bash) o `javac -encoding UTF-8 -d out src\*.java` (Windows), ejecuta `java -cp out EJ04`. Comprueba literalmente la salida o, en HashSet, comprueba el conjunto de productos sin imponer orden.

**Salida esperada:**

```text
Encontrado: Nombre: Rosa - Edad: 20
```

**Interpretación.** El signo `!` niega el valor booleano; si ninguna comparación cambió el indicador, mostramos una salida verificable. Este bloque no imprime nada cuando Rosa sí fue localizada. Con buscado=Rosa hay una sola línea; con buscado=Mario aparece No encontrado: Mario. La prueba vale cuando puedes justificar el cambio de estado, no solamente repetir el texto de la consola.

**Variación A — prueba de transferencia.** Sustituye Rosa por Mario. Debe imprimirse No encontrado: Mario, no una excepción ni un resultado vacío.

**Variación B — comprobación negativa.** Comparar String con ==. Identifica la condición o llamada responsable, sin dejar una versión errónea como resultado final.

## Error o caso límite controlado y corrección

**Situación:** Comparar String con ==. **Causa:** La comparación `==` contrasta referencias; no expresa la comparación de contenido que solicita el ejercicio. **Corrección:** Utiliza `estudiante.getNombre().equals(buscado)` y prueba un nombre presente y uno ausente.

## Comprueba que puedes explicarlo

Explica la relación entre el dato inicial y el resultado; identifica la línea exacta que recorre, compara, elimina o impide un duplicado, según corresponda; y justifica por qué la validación propuesta detecta un error real.

## T04 — Tarea espejo: Comprobar el caso de búsqueda sin coincidencia

**Enunciado:** Busca «Mario» en una lista de Elena, Luis y Nora. Usa String.equals y muestra un mensaje explícito cuando no existe el registro.

**Archivo a construir:** `src/T04.java`; conserva la clase `Estudiante` o `Producto` que ya desarrollaste. **Restricción:** La comparación es por nombre; no llames a == para Strings.

**Ruta de trabajo:** crea una clase Java con `main`, inicia los objetos indicados, añade el mecanismo específico aprendido en EJ04 y muestra una comprobación visible. **Pista:** Inicia encontrado=false; cambia a true solo si coincide.

**Evidencia y criterio de aceptación:** Se imprime «No encontrado: Mario». La solución debe compilar; el resultado se explica en una oración señalando qué método causó el comportamiento. Esta tarea es para que la resuelvas: la solución docente no se incluye en esta guía.


---

# EJ05 — Eliminar un estudiante con Iterator.remove

## Objetivo técnico — lectura docente

El área administrativa necesita retirar un estudiante de la lista durante el mismo recorrido que lo localiza. Partiremos de tres registros, construiremos un Iterator y buscaremos a Rosa por nombre. Al encontrarla llamaremos al método remove del iterador que entregó ese objeto, y después volveremos a imprimir el estado de la colección. El ejercicio demostrará por qué el mecanismo de eliminación importa, no solo qué elemento se desea borrar.

## Qué problema concreto resolveremos

¿Cómo eliminar durante un recorrido sin provocar modificaciones inconsistentes?

**Archivos y punto de partida:** `src/EJ05.java` y `src/Estudiante.java` existente. Los imports se escriben encima de la declaración de clase. Cada segmento debe quedar dentro del bloque indicado; la versión completa para cotejar aparece **solo después** de explicar las partes.

## Preparar el archivo ejecutable antes de los microbloques

Crea el archivo y escribe esta estructura inicial. El comentario marca el lugar donde sustituirás, en orden, los fragmentos siguientes. `main` es el punto de entrada y las importaciones habilitan los tipos de colección usados en el escenario. Los métodos de Estudiante y Producto se implementan en sus archivos propios.

```java
import java.util.ArrayList;
import java.util.List;
import java.util.Iterator;

public class EJ05 {
    public static void main(String[] args) {
        // Escribir los microbloques indicados aquí.
    }
}
```

## Paso 1 — Plantear una hipótesis comprobable

Antes de editar, responde: ¿Cómo eliminar durante un recorrido sin provocar modificaciones inconsistentes? Explica qué parte de la colección cambiará y qué salida permitirá demostrarlo; no valides únicamente que el programa no muestra errores.

### Paso 2 — Preparar la colección que debe cambiar

**Antes de escribir.** El objetivo ya no es únicamente observar estudiantes: debemos quitar uno durante el recorrido, manteniendo a los otros dos.

**Lugar exacto.** src/EJ05.java, primeras instrucciones de `main`. Si ese archivo no existe, créalo en `src` mediante **New > Java Class**, conserva el nombre indicado y prepara las llaves de la clase y de `main` cuando corresponda.

**Escribe ahora:**

```java
        List<Estudiante> estudiantes = new ArrayList<>();
        estudiantes.add(new Estudiante("Pedro", 21));
        estudiantes.add(new Estudiante("Rosa", 20));
        estudiantes.add(new Estudiante("Antonio", 23));
```

**Explicación técnica mientras lo escribimos.** El objetivo ya no es únicamente observar estudiantes: debemos quitar uno durante el recorrido, manteniendo a los otros dos. Conviene empezar por un estado estable que conozcamos y cuantificar el cambio al final.

**Estado o evidencia tras este microbloque.** Antes de la operación hay 3 objetos.

### Paso 3 — Obtener el iterador para un recorrido con eliminación

**Antes de escribir.** Para eliminar mientras recorremos elegimos el mecanismo enseñado por la sesión: el propio Iterator.

**Lugar exacto.** src/EJ05.java, después de registrar Antonio. Si ese archivo no existe, créalo en `src` mediante **New > Java Class**, conserva el nombre indicado y prepara las llaves de la clase y de `main` cuando corresponda.

**Escribe ahora:**

```java
        Iterator<Estudiante> iterador = estudiantes.iterator();
```

**Explicación técnica mientras lo escribimos.** Para eliminar mientras recorremos elegimos el mecanismo enseñado por la sesión: el propio Iterator. Evitamos modificar directamente la lista desde un for-each, una práctica propensa a ConcurrentModificationException.

**Estado o evidencia tras este microbloque.** El iterador está preparado, pero la lista conserva tres objetos.

### Paso 4 — Eliminar mediante el mismo cursor que visitó el objeto

**Antes de escribir.** Se avanza con `next()` y se compara el nombre de la instancia actual.

**Lugar exacto.** src/EJ05.java, después de declarar `iterador`. Si ese archivo no existe, créalo en `src` mediante **New > Java Class**, conserva el nombre indicado y prepara las llaves de la clase y de `main` cuando corresponda.

**Escribe ahora:**

```java
        while (iterador.hasNext()) {
            Estudiante actual = iterador.next();
            if (actual.getNombre().equals("Rosa")) {
                iterador.remove();
                break;
            }
        }
```

**Explicación técnica mientras lo escribimos.** Se avanza con `next()` y se compara el nombre de la instancia actual. `iterador.remove()` elimina el último elemento que devolvió ese iterador; `break` es adecuado aquí porque solo queremos borrar una primera coincidencia. Llamar a `remove` antes de `next()` es inválido.

**Estado o evidencia tras este microbloque.** Luego de encontrar Rosa, quedan Pedro y Antonio.

### Paso 5 — Hacer visible el cambio de la colección

**Antes de escribir.** Mostrar únicamente un mensaje de “eliminado” no prueba el estado de la estructura.

**Lugar exacto.** src/EJ05.java, después del `while` dentro de `main`. Si ese archivo no existe, créalo en `src` mediante **New > Java Class**, conserva el nombre indicado y prepara las llaves de la clase y de `main` cuando corresponda.

**Escribe ahora:**

```java
        System.out.println("Restantes: " + estudiantes.size());
        for (Estudiante estudiante : estudiantes) {
            System.out.println(estudiante);
        }
```

**Explicación técnica mientras lo escribimos.** Mostrar únicamente un mensaje de “eliminado” no prueba el estado de la estructura. Medimos el tamaño y recorremos lo que queda, para corroborar que desapareció solo Rosa.

**Estado o evidencia tras este microbloque.** Tamaño pasa de 3 a 2 y no se imprime Rosa.

## Auditoría del artefacto antes de ejecutar

- Confirma que el archivo se llama `EJ05.java` y la clase pública `EJ05`; los `import` preceden a la clase, `main` es el punto de entrada y sus llaves están equilibradas.
- Contrasta cada bloque funcional de arriba con la versión completa; no debe haber una instrucción de comportamiento que aparezca por primera vez sin haberse explicado.

## Archivo `src/EJ05.java` completo al terminar

```java
import java.util.ArrayList;
import java.util.List;
import java.util.Iterator;

public class EJ05 {
    public static void main(String[] args) {
List<Estudiante> estudiantes = new ArrayList<>();
estudiantes.add(new Estudiante("Pedro", 21));
estudiantes.add(new Estudiante("Rosa", 20));
estudiantes.add(new Estudiante("Antonio", 23));
Iterator<Estudiante> iterador = estudiantes.iterator();
while (iterador.hasNext()) {
    Estudiante actual = iterador.next();
    if (actual.getNombre().equals("Rosa")) {
        iterador.remove();
        break;
    }
}
System.out.println("Restantes: " + estudiantes.size());
for (Estudiante estudiante : estudiantes) {
    System.out.println(estudiante);
}
    }
}
```

## Antes de ejecutar: predicción

1. ¿Cuántos elementos quedan o se recorren al terminar EJ05, y por qué?
2. ¿Qué instrucción precisa causa la salida visible y qué método o condición interviene?
3. Si cambias el dato de prueba indicado a continuación, ¿cuál será el primer resultado diferente?

## Ejecutar y validar

En IntelliJ, ejecuta `EJ05.main()` con el triángulo verde. Desde la terminal de la raíz del proyecto, tras compilar con `javac -encoding UTF-8 -d out src/*.java` (Bash) o `javac -encoding UTF-8 -d out src\*.java` (Windows), ejecuta `java -cp out EJ05`. Comprueba literalmente la salida o, en HashSet, comprueba el conjunto de productos sin imponer orden.

**Salida esperada:**

```text
Restantes: 2
Nombre: Pedro - Edad: 21
Nombre: Antonio - Edad: 23
```

**Interpretación.** Mostrar únicamente un mensaje de “eliminado” no prueba el estado de la estructura. Medimos el tamaño y recorremos lo que queda, para corroborar que desapareció solo Rosa. Tamaño pasa de 3 a 2 y no se imprime Rosa. La prueba vale cuando puedes justificar el cambio de estado, no solamente repetir el texto de la consola.

**Variación A — prueba de transferencia.** Cambia la búsqueda a Pedro y comprueba que el primer elemento puede eliminarse con el mismo procedimiento.

**Variación B — comprobación negativa.** Usar estudiantes.remove(actual) dentro del while sobre la misma lista. Identifica la condición o llamada responsable, sin dejar una versión errónea como resultado final.

## Error o caso límite controlado y corrección

**Situación:** Usar estudiantes.remove(actual) dentro del while sobre la misma lista. **Causa:** La modificación estructural externa al iterador puede provocar ConcurrentModificationException al continuar el recorrido. **Corrección:** Usa `iterador.remove()` después de `next()` y sobre el mismo iterador.

## Comprueba que puedes explicarlo

Explica la relación entre el dato inicial y el resultado; identifica la línea exacta que recorre, compara, elimina o impide un duplicado, según corresponda; y justifica por qué la validación propuesta detecta un error real.

## T05 — Tarea espejo: Eliminar varias coincidencias sin saltar elementos

**Enunciado:** Usa un Iterator para quitar todos los estudiantes menores de 21 años de Elena(22), Luis(19) y Nora(24); luego muestra los restantes.

**Archivo a construir:** `src/T05.java`; conserva la clase `Estudiante` o `Producto` que ya desarrollaste. **Restricción:** Elimina exclusivamente con iterador.remove() dentro del recorrido.

**Ruta de trabajo:** crea una clase Java con `main`, inicia los objetos indicados, añade el mecanismo específico aprendido en EJ05 y muestra una comprobación visible. **Pista:** A diferencia del ejemplo, no hagas break: pueden existir varias coincidencias.

**Evidencia y criterio de aceptación:** Quedan Elena y Nora; total 2. La solución debe compilar; el resultado se explica en una oración señalando qué método causó el comportamiento. Esta tarea es para que la resuelvas: la solución docente no se incluye en esta guía.


---

# EJ06 — Eliminar por condición usando removeIf

## Objetivo técnico — lectura docente

En algunas situaciones la condición de eliminación es más importante que un nombre exacto. Sobre la lista de estudiantes aplicaremos removeIf para retirar a quienes tienen menos de 21 años, recuperaremos el booleano que informa un cambio y verificaremos los objetos que permanecen. Contrastaremos el operador menor estricto con la condición menor o igual: una sola diferencia en el límite puede borrar registros que deberían conservarse.

## Qué problema concreto resolveremos

¿Cómo retirar todos los objetos que satisfacen una misma condición?

**Archivos y punto de partida:** `src/EJ06.java` y `src/Estudiante.java` existente. Los imports se escriben encima de la declaración de clase. Cada segmento debe quedar dentro del bloque indicado; la versión completa para cotejar aparece **solo después** de explicar las partes.

## Preparar el archivo ejecutable antes de los microbloques

Crea el archivo y escribe esta estructura inicial. El comentario marca el lugar donde sustituirás, en orden, los fragmentos siguientes. `main` es el punto de entrada y las importaciones habilitan los tipos de colección usados en el escenario. Los métodos de Estudiante y Producto se implementan en sus archivos propios.

```java
import java.util.ArrayList;
import java.util.List;

public class EJ06 {
    public static void main(String[] args) {
        // Escribir los microbloques indicados aquí.
    }
}
```

## Paso 1 — Plantear una hipótesis comprobable

Antes de editar, responde: ¿Cómo retirar todos los objetos que satisfacen una misma condición? Explica qué parte de la colección cambiará y qué salida permitirá demostrarlo; no valides únicamente que el programa no muestra errores.

### Paso 2 — Iniciar con datos suficientes para probar el filtro

**Antes de escribir.** La diferencia de este caso consiste en eliminar mediante una condición declarada en una sola llamada, no mediante el cursor explícito.

**Lugar exacto.** src/EJ06.java, primeras instrucciones de `main`. Si ese archivo no existe, créalo en `src` mediante **New > Java Class**, conserva el nombre indicado y prepara las llaves de la clase y de `main` cuando corresponda.

**Escribe ahora:**

```java
        List<Estudiante> estudiantes = new ArrayList<>();
        estudiantes.add(new Estudiante("Pedro", 21));
        estudiantes.add(new Estudiante("Rosa", 20));
        estudiantes.add(new Estudiante("Antonio", 23));
```

**Explicación técnica mientras lo escribimos.** La diferencia de este caso consiste en eliminar mediante una condición declarada en una sola llamada, no mediante el cursor explícito. Las edades distintas permitirán comprobar el criterio de corte.

**Estado o evidencia tras este microbloque.** La lista contiene edades 21, 20 y 23.

### Paso 3 — Eliminar por predicado con removeIf

**Antes de escribir.** `removeIf` evalúa el predicado para cada elemento.

**Lugar exacto.** src/EJ06.java, después del último `add`. Si ese archivo no existe, créalo en `src` mediante **New > Java Class**, conserva el nombre indicado y prepara las llaves de la clase y de `main` cuando corresponda.

**Escribe ahora:**

```java
        boolean seElimino = estudiantes.removeIf(e -> e.getEdad() < 21);
```

**Explicación técnica mientras lo escribimos.** `removeIf` evalúa el predicado para cada elemento. `e` es cada Estudiante y la flecha introduce la condición; los objetos con edad menor de 21 se eliminan. El booleano informa si la colección cambió, no cuántos objetos se borraron.

**Estado o evidencia tras este microbloque.** Rosa (20) cumple la condición y se elimina; Pedro (21) permanece.

### Paso 4 — Comprobar la modificación sin confiar en suposiciones

**Antes de escribir.** Imprimimos el booleano, el tamaño y las instancias conservadas.

**Lugar exacto.** src/EJ06.java, después de la llamada `removeIf`. Si ese archivo no existe, créalo en `src` mediante **New > Java Class**, conserva el nombre indicado y prepara las llaves de la clase y de `main` cuando corresponda.

**Escribe ahora:**

```java
        System.out.println("Se eliminó alguno: " + seElimino);
        System.out.println("Restantes: " + estudiantes.size());
        for (Estudiante estudiante : estudiantes) {
            System.out.println(estudiante);
        }
```

**Explicación técnica mientras lo escribimos.** Imprimimos el booleano, el tamaño y las instancias conservadas. Así contrastamos el efecto con los valores anteriores: la condición `edad < 21` no equivale a `edad <= 21`.

**Estado o evidencia tras este microbloque.** Se imprime true, Restantes: 2, Pedro y Antonio.

## Auditoría del artefacto antes de ejecutar

- Confirma que el archivo se llama `EJ06.java` y la clase pública `EJ06`; los `import` preceden a la clase, `main` es el punto de entrada y sus llaves están equilibradas.
- Contrasta cada bloque funcional de arriba con la versión completa; no debe haber una instrucción de comportamiento que aparezca por primera vez sin haberse explicado.

## Archivo `src/EJ06.java` completo al terminar

```java
import java.util.ArrayList;
import java.util.List;

public class EJ06 {
    public static void main(String[] args) {
List<Estudiante> estudiantes = new ArrayList<>();
estudiantes.add(new Estudiante("Pedro", 21));
estudiantes.add(new Estudiante("Rosa", 20));
estudiantes.add(new Estudiante("Antonio", 23));
boolean seElimino = estudiantes.removeIf(e -> e.getEdad() < 21);
System.out.println("Se eliminó alguno: " + seElimino);
System.out.println("Restantes: " + estudiantes.size());
for (Estudiante estudiante : estudiantes) {
    System.out.println(estudiante);
}
    }
}
```

## Antes de ejecutar: predicción

1. ¿Cuántos elementos quedan o se recorren al terminar EJ06, y por qué?
2. ¿Qué instrucción precisa causa la salida visible y qué método o condición interviene?
3. Si cambias el dato de prueba indicado a continuación, ¿cuál será el primer resultado diferente?

## Ejecutar y validar

En IntelliJ, ejecuta `EJ06.main()` con el triángulo verde. Desde la terminal de la raíz del proyecto, tras compilar con `javac -encoding UTF-8 -d out src/*.java` (Bash) o `javac -encoding UTF-8 -d out src\*.java` (Windows), ejecuta `java -cp out EJ06`. Comprueba literalmente la salida o, en HashSet, comprueba el conjunto de productos sin imponer orden.

**Salida esperada:**

```text
Se eliminó alguno: true
Restantes: 2
Nombre: Pedro - Edad: 21
Nombre: Antonio - Edad: 23
```

**Interpretación.** Imprimimos el booleano, el tamaño y las instancias conservadas. Así contrastamos el efecto con los valores anteriores: la condición `edad < 21` no equivale a `edad <= 21`. Se imprime true, Restantes: 2, Pedro y Antonio. La prueba vale cuando puedes justificar el cambio de estado, no solamente repetir el texto de la consola.

**Variación A — prueba de transferencia.** Cambia el límite de < 21 a <= 21 y observa que Pedro también desaparece; devuelve el código al caso original.

**Variación B — comprobación negativa.** Cambiar < 21 por <= 21 sin revisar el límite. Identifica la condición o llamada responsable, sin dejar una versión errónea como resultado final.

## Error o caso límite controlado y corrección

**Situación:** Cambiar < 21 por <= 21 sin revisar el límite. **Causa:** Se elimina también Pedro, que tiene exactamente 21 años; la salida deja de cumplir la regla de “menores de 21”. **Corrección:** Restablece `e.getEdad() < 21`; repite la ejecución y confirma que quedan dos.

## Comprueba que puedes explicarlo

Explica la relación entre el dato inicial y el resultado; identifica la línea exacta que recorre, compara, elimina o impide un duplicado, según corresponda; y justifica por qué la validación propuesta detecta un error real.

## T06 — Tarea espejo: Eliminar por condición inversa con removeIf

**Enunciado:** Sobre Elena(22), Luis(19) y Nora(24), elimina a quienes tengan 22 años o más usando removeIf; muestra si cambió la lista y qué quedó.

**Archivo a construir:** `src/T06.java`; conserva la clase `Estudiante` o `Producto` que ya desarrollaste. **Restricción:** Usa una sola invocación a removeIf con un predicado por edad.

**Ruta de trabajo:** crea una clase Java con `main`, inicia los objetos indicados, añade el mecanismo específico aprendido en EJ06 y muestra una comprobación visible. **Pista:** El predicado debe ser >= 22, no < 22.

**Evidencia y criterio de aceptación:** Queda únicamente Luis; total 1; resultado boolean true. La solución debe compilar; el resultado se explica en una oración señalando qué método causó el comportamiento. Esta tarea es para que la resuelvas: la solución docente no se incluye en esta guía.


---

# EJ07 — Definir la igualdad de Producto con equals y hashCode

## Objetivo técnico — lectura docente

Para pasar de una lista a un conjunto necesitamos decidir qué significa que dos productos sean equivalentes. Crearemos la clase Producto con nombre y precio, pero fijaremos una regla de identidad específica: el nombre determina igualdad, aunque el precio difiera. Implementaremos equals y hashCode de manera coherente y ensayaremos casos positivos y negativos antes de utilizar HashSet. Así podremos justificar por qué dos instancias distintas no siempre deben contarse como dos productos distintos.

## Qué problema concreto resolveremos

¿Cómo garantizar que dos productos del mismo nombre sean tratados como iguales?

**Archivos y punto de partida:** `src/EJ07.java` y `src/Producto.java` (se crea por primera vez). Los imports se escriben encima de la declaración de clase. Cada segmento debe quedar dentro del bloque indicado; la versión completa para cotejar aparece **solo después** de explicar las partes.

## Preparar el archivo ejecutable antes de los microbloques

Crea el archivo y escribe esta estructura inicial. El comentario marca el lugar donde sustituirás, en orden, los fragmentos siguientes. `main` es el punto de entrada y las importaciones habilitan los tipos de colección usados en el escenario. Los métodos de Estudiante y Producto se implementan en sus archivos propios.

```java
public class EJ07 {
    public static void main(String[] args) {
        // Escribir los microbloques indicados aquí.
    }
}
```

## Paso 1 — Plantear una hipótesis comprobable

Antes de editar, responde: ¿Cómo garantizar que dos productos del mismo nombre sean tratados como iguales? Explica qué parte de la colección cambiará y qué salida permitirá demostrarlo; no valides únicamente que el programa no muestra errores.

### Paso 2 — Declarar la identidad y la información mostrada

**Antes de escribir.** Un producto necesita nombre y precio para el caso de catálogo.

**Lugar exacto.** src/Producto.java, debajo de `public class Producto {`. Si ese archivo no existe, créalo en `src` mediante **New > Java Class**, conserva el nombre indicado y prepara las llaves de la clase y de `main` cuando corresponda.

**Escribe ahora:**

```java
    private String nombre;
    private double precio;
```

**Explicación técnica mientras lo escribimos.** Un producto necesita nombre y precio para el caso de catálogo. En esta práctica definimos que dos productos se consideran el mismo elemento del conjunto cuando coincide su nombre, aunque tengan precios distintos; es una regla de identidad de este ejercicio, no una regla universal de todos los comercios.

**Estado o evidencia tras este microbloque.** Todavía falta establecer cómo reciben valores y cómo se comparan.

### Paso 3 — Recibir valores y permitir consultas

**Antes de escribir.** El constructor asigna los dos atributos recibidos.

**Lugar exacto.** src/Producto.java, después de los campos y antes de la llave final. Si ese archivo no existe, créalo en `src` mediante **New > Java Class**, conserva el nombre indicado y prepara las llaves de la clase y de `main` cuando corresponda.

**Escribe ahora:**

```java
    public Producto(String nombre, double precio) {
        this.nombre = nombre;
        this.precio = precio;
    }

    public String getNombre() {
        return nombre;
    }

    public double getPrecio() {
        return precio;
    }
```

**Explicación técnica mientras lo escribimos.** El constructor asigna los dos atributos recibidos. Los getters permiten comparar el nombre o mostrar el precio; por ejemplo, dos objetos Impresora con distintos precios siguen teniendo distinto estado de precio aunque nuestra igualdad futura dependa solo de nombre.

**Estado o evidencia tras este microbloque.** Ahora pueden construirse productos y consultarse sus atributos.

### Paso 4 — Dar una descripción útil al presentar un producto

**Antes de escribir.** `toString` devuelve texto representativo para la salida de consola.

**Lugar exacto.** src/Producto.java, después de `getPrecio()`. Si ese archivo no existe, créalo en `src` mediante **New > Java Class**, conserva el nombre indicado y prepara las llaves de la clase y de `main` cuando corresponda.

**Escribe ahora:**

```java
    @Override
    public String toString() {
        return nombre + " - " + precio;
    }
```

**Explicación técnica mientras lo escribimos.** `toString` devuelve texto representativo para la salida de consola. No forma parte de la regla de igualdad: sirve para comprobar qué objeto estamos mostrando y su precio actual.

**Estado o evidencia tras este microbloque.** Un producto Impresora con precio 187.0 se imprime Impresora - 187.0.

### Paso 5 — Definir la igualdad según el nombre

**Antes de escribir.** El parámetro Object acepta cualquier referencia que se deba comparar.

**Lugar exacto.** src/Producto.java, después de `toString()`. Si ese archivo no existe, créalo en `src` mediante **New > Java Class**, conserva el nombre indicado y prepara las llaves de la clase y de `main` cuando corresponda.

**Escribe ahora:**

```java
    @Override
    public boolean equals(Object obj) {
        if (obj == null) {
            return false;
        }
        if (obj instanceof Producto) {
            Producto otro = (Producto) obj;
            return this.nombre.equals(otro.getNombre());
        }
        return false;
    }
```

**Explicación técnica mientras lo escribimos.** El parámetro Object acepta cualquier referencia que se deba comparar. Primero descartamos null, después verificamos con `instanceof` que sea Producto, convertimos el tipo y comparamos únicamente nombres con String.equals. Dos objetos distintos pueden ser lógicamente iguales; el precio no participa en esta decisión.

**Estado o evidencia tras este microbloque.** Impresora(187) y Impresora(199) dan true; Impresora y Televisor dan false.

### Paso 6 — Hacer que la dispersión respete la misma igualdad

**Antes de escribir.** Si dos productos son iguales por nombre, deben producir el mismo código hash.

**Lugar exacto.** src/Producto.java, después del método `equals` y antes del cierre de clase. Si ese archivo no existe, créalo en `src` mediante **New > Java Class**, conserva el nombre indicado y prepara las llaves de la clase y de `main` cuando corresponda.

**Escribe ahora:**

```java
    @Override
    public int hashCode() {
        return nombre.hashCode();
    }
```

**Explicación técnica mientras lo escribimos.** Si dos productos son iguales por nombre, deben producir el mismo código hash. Por ello calculamos hash a partir del mismo atributo que usa equals. Hash no es un identificador único garantizado: dos objetos diferentes pueden coincidir en código; Java comprueba igualdad además de ubicar elementos en la estructura.

**Estado o evidencia tras este microbloque.** Dos productos de nombre Impresora tienen el mismo hash; no se garantiza hash distinto para cada nombre.

### Paso 7 — Ejecutar contrastes de identidad con objetos independientes

**Antes de escribir.** Cada llamada a new produce una referencia distinta, pero a y b comparten el nombre lógico.

**Lugar exacto.** src/EJ07.java, dentro de `main`, colocar el bloque completo de pruebas. Si ese archivo no existe, créalo en `src` mediante **New > Java Class**, conserva el nombre indicado y prepara las llaves de la clase y de `main` cuando corresponda.

**Escribe ahora:**

```java
        Producto a = new Producto("Impresora", 187.0);
        Producto b = new Producto("Impresora", 199.0);
        Producto c = new Producto("Televisor", 650.0);
        System.out.println("a.equals(b): " + a.equals(b));
        System.out.println("Mismo hash si iguales: " + (a.hashCode() == b.hashCode()));
        System.out.println("a.equals(c): " + a.equals(c));
```

**Explicación técnica mientras lo escribimos.** Cada llamada a new produce una referencia distinta, pero a y b comparten el nombre lógico. La primera salida confirma equals, la segunda verifica el requisito del contrato hash y la tercera sirve de control negativo. Se han construido estos criterios antes de incorporarlos a HashSet para evitar una “caja negra”.

**Estado o evidencia tras este microbloque.** La consola muestra true, true y false en ese orden.

## Auditoría del artefacto antes de ejecutar

- Confirma que el archivo se llama `EJ07.java` y la clase pública `EJ07`; los `import` preceden a la clase, `main` es el punto de entrada y sus llaves están equilibradas.
- Además, verifica que `Producto.java` contiene `equals(Object)` y `hashCode()`, que ambos usan el nombre como regla de identidad, y que el precio permanece fuera de ella.
- Contrasta cada bloque funcional de arriba con la versión completa; no debe haber una instrucción de comportamiento que aparezca por primera vez sin haberse explicado.

## Archivo `src/Producto.java` completo tras los microbloques

```java
public class Producto {
    private String nombre;
    private double precio;

    public Producto(String nombre, double precio) {
        this.nombre = nombre;
        this.precio = precio;
    }

    public String getNombre() {
        return nombre;
    }

    public double getPrecio() {
        return precio;
    }

    @Override
    public String toString() {
        return nombre + " - " + precio;
    }

    @Override
    public boolean equals(Object obj) {
        if (obj == null) {
            return false;
        }
        if (obj instanceof Producto) {
            Producto otro = (Producto) obj;
            return this.nombre.equals(otro.getNombre());
        }
        return false;
    }

    @Override
    public int hashCode() {
        return nombre.hashCode();
    }
}
```

## Archivo `src/EJ07.java` completo al terminar

```java

public class EJ07 {
    public static void main(String[] args) {
Producto a = new Producto("Impresora", 187.0);
Producto b = new Producto("Impresora", 199.0);
Producto c = new Producto("Televisor", 650.0);
System.out.println("a.equals(b): " + a.equals(b));
System.out.println("Mismo hash si iguales: " + (a.hashCode() == b.hashCode()));
System.out.println("a.equals(c): " + a.equals(c));
    }
}
```

## Antes de ejecutar: predicción

1. ¿Cuántos elementos quedan o se recorren al terminar EJ07, y por qué?
2. ¿Qué instrucción precisa causa la salida visible y qué método o condición interviene?
3. Si cambias el dato de prueba indicado a continuación, ¿cuál será el primer resultado diferente?

## Ejecutar y validar

En IntelliJ, ejecuta `EJ07.main()` con el triángulo verde. Desde la terminal de la raíz del proyecto, tras compilar con `javac -encoding UTF-8 -d out src/*.java` (Bash) o `javac -encoding UTF-8 -d out src\*.java` (Windows), ejecuta `java -cp out EJ07`. Comprueba literalmente la salida o, en HashSet, comprueba el conjunto de productos sin imponer orden.

**Salida esperada:**

```text
a.equals(b): true
Mismo hash si iguales: true
a.equals(c): false
```

**Interpretación.** Cada llamada a new produce una referencia distinta, pero a y b comparten el nombre lógico. La primera salida confirma equals, la segunda verifica el requisito del contrato hash y la tercera sirve de control negativo. Se han construido estos criterios antes de incorporarlos a HashSet para evitar una “caja negra”. La consola muestra true, true y false en ese orden. La prueba vale cuando puedes justificar el cambio de estado, no solamente repetir el texto de la consola.

**Variación A — prueba de transferencia.** Cambia solamente el precio de b y confirma que equals y hashCode siguen siendo iguales; después cambia su nombre.

**Variación B — comprobación negativa.** Sobrescribir equals pero no hashCode. Identifica la condición o llamada responsable, sin dejar una versión errónea como resultado final.

## Error o caso límite controlado y corrección

**Situación:** Sobrescribir equals pero no hashCode. **Causa:** Dos productos considerados iguales podrían tener hashes diferentes, rompiendo la obligación del contrato al utilizarlos como claves de hash. **Corrección:** Implementa hashCode a partir del nombre, el mismo dato que decide equals. No presupongas hashes únicos.

## Comprueba que puedes explicarlo

Explica la relación entre el dato inicial y el resultado; identifica la línea exacta que recorre, compara, elimina o impide un duplicado, según corresponda; y justifica por qué la validación propuesta detecta un error real.

## T07 — Tarea espejo: Probar igualdad lógica aunque cambie el precio

**Enunciado:** Crea dos productos Mouse con precios 35.0 y 50.0, y uno Teclado. Comprueba equals para los dos Mouse, compara sus hashes y contrasta con Teclado.

**Archivo a construir:** `src/T07.java`; conserva la clase `Estudiante` o `Producto` que ya desarrollaste. **Restricción:** La identidad lógica sigue siendo el nombre definido en Producto.

**Ruta de trabajo:** crea una clase Java con `main`, inicia los objetos indicados, añade el mecanismo específico aprendido en EJ07 y muestra una comprobación visible. **Pista:** No cambies equals/hashCode: analiza la política de identidad ya construida.

**Evidencia y criterio de aceptación:** Mouse/Mouse = true; hashes iguales; Mouse/Teclado = false. La solución debe compilar; el resultado se explica en una oración señalando qué método causó el comportamiento. Esta tarea es para que la resuelvas: la solución docente no se incluye en esta guía.


---

# EJ08 — Construir un HashSet de productos sin duplicados

## Objetivo técnico — lectura docente

Una lista puede aceptar elementos repetidos, mientras que un HashSet está diseñado para conservar elementos únicos según la igualdad de sus objetos. Con la clase Producto ya preparada, registraremos tres nombres distintos e intentaremos agregar una segunda Impresora con precio diferente. Interpretaremos las respuestas de add y la cantidad almacenada, comprobaremos contains y remove y presentaremos los productos restantes sin exigir ningún orden. El resultado verificable será un conjunto de dos productos después de la eliminación.

## Qué problema concreto resolveremos

¿Cómo impedir duplicados, comprobar pertenencia y eliminar por identidad lógica?

**Archivos y punto de partida:** `src/EJ08.java` y `src/Producto.java` existente. Los imports se escriben encima de la declaración de clase. Cada segmento debe quedar dentro del bloque indicado; la versión completa para cotejar aparece **solo después** de explicar las partes.

## Preparar el archivo ejecutable antes de los microbloques

Crea el archivo y escribe esta estructura inicial. El comentario marca el lugar donde sustituirás, en orden, los fragmentos siguientes. `main` es el punto de entrada y las importaciones habilitan los tipos de colección usados en el escenario. Los métodos de Estudiante y Producto se implementan en sus archivos propios.

```java
import java.util.HashSet;

public class EJ08 {
    public static void main(String[] args) {
        // Escribir los microbloques indicados aquí.
    }
}
```

## Paso 1 — Plantear una hipótesis comprobable

Antes de editar, responde: ¿Cómo impedir duplicados, comprobar pertenencia y eliminar por identidad lógica? Explica qué parte de la colección cambiará y qué salida permitirá demostrarlo; no valides únicamente que el programa no muestra errores.

### Paso 2 — Crear una colección que represente un catálogo sin duplicados

**Antes de escribir.** `HashSet<Producto>` declara un conjunto de productos sin duplicados lógicos.

**Lugar exacto.** src/EJ08.java, primera instrucción de `main`. Si ese archivo no existe, créalo en `src` mediante **New > Java Class**, conserva el nombre indicado y prepara las llaves de la clase y de `main` cuando corresponda.

**Escribe ahora:**

```java
        HashSet<Producto> productos = new HashSet<>();
```

**Explicación técnica mientras lo escribimos.** `HashSet<Producto>` declara un conjunto de productos sin duplicados lógicos. Su regla de duplicidad invoca equals y hashCode ya definidos en Producto. El import HashSet permite usar la clase de Java Collections Framework.

**Estado o evidencia tras este microbloque.** El conjunto inicia con tamaño 0; su recorrido no tiene orden garantizado.

### Paso 3 — Registrar tres nombres distintos y una repetición

**Antes de escribir.** Las primeras tres altas tienen nombres distintos, por lo que cada add devuelve true.

**Lugar exacto.** src/EJ08.java, después de declarar `productos`. Si ese archivo no existe, créalo en `src` mediante **New > Java Class**, conserva el nombre indicado y prepara las llaves de la clase y de `main` cuando corresponda.

**Escribe ahora:**

```java
        boolean a1 = productos.add(new Producto("Impresora", 187.0));
        boolean a2 = productos.add(new Producto("Computadora", 2356.0));
        boolean a3 = productos.add(new Producto("Televisor", 650.0));
        boolean duplicado = productos.add(new Producto("Impresora", 200.0));
```

**Explicación técnica mientras lo escribimos.** Las primeras tres altas tienen nombres distintos, por lo que cada add devuelve true. La cuarta crea otra instancia de Impresora, pero equals la considera equivalente a la primera; el conjunto no reemplaza el precio existente, sino que rechaza la inserción.

**Estado o evidencia tras este microbloque.** Los cuatro intentos dejan tres objetos y `duplicado` queda false.

### Paso 4 — Medir la condición de unicidad

**Antes de escribir.** Observamos por separado las respuestas de add y la cantidad real.

**Lugar exacto.** src/EJ08.java, después del cuarto `add`. Si ese archivo no existe, créalo en `src` mediante **New > Java Class**, conserva el nombre indicado y prepara las llaves de la clase y de `main` cuando corresponda.

**Escribe ahora:**

```java
        System.out.println("Altas: " + a1 + "," + a2 + "," + a3);
        System.out.println("Duplicado agregado: " + duplicado);
        System.out.println("Únicos: " + productos.size());
```

**Explicación técnica mientras lo escribimos.** Observamos por separado las respuestas de add y la cantidad real. De esta forma no confundimos cuatro solicitudes de alta con cuatro elementos almacenados: el cuarto objeto no fue insertado.

**Estado o evidencia tras este microbloque.** Se imprime Altas: true,true,true; Duplicado agregado: false; Únicos: 3.

### Paso 5 — Consultar y retirar por la identidad lógica

**Antes de escribir.** `contains` y `remove` crean objetos de consulta con nombres coincidentes; el precio 0 es un dato de prueba y no participa en la identidad.

**Lugar exacto.** src/EJ08.java, después de las comprobaciones de tamaño. Si ese archivo no existe, créalo en `src` mediante **New > Java Class**, conserva el nombre indicado y prepara las llaves de la clase y de `main` cuando corresponda.

**Escribe ahora:**

```java
        boolean existe = productos.contains(new Producto("Impresora", 0));
        System.out.println("Existe Impresora: " + existe);
        boolean borrado = productos.remove(new Producto("Televisor", 0));
        System.out.println("Eliminado Televisor: " + borrado);
        System.out.println("Restantes: " + productos.size());
```

**Explicación técnica mientras lo escribimos.** `contains` y `remove` crean objetos de consulta con nombres coincidentes; el precio 0 es un dato de prueba y no participa en la identidad. contains devuelve true si está Impresora. remove devuelve true si retiró Televisor. La cantidad baja a dos.

**Estado o evidencia tras este microbloque.** Existe Impresora=true; Eliminado Televisor=true; Restantes=2.

### Paso 6 — Visualizar elementos sin asumir su orden

**Antes de escribir.** La impresión permite inspeccionar qué productos sobrevivieron, pero HashSet no garantiza ni el orden de inserción ni el orden lexicográfico.

**Lugar exacto.** src/EJ08.java, después de imprimir `Restantes`. Si ese archivo no existe, créalo en `src` mediante **New > Java Class**, conserva el nombre indicado y prepara las llaves de la clase y de `main` cuando corresponda.

**Escribe ahora:**

```java
        for (Producto producto : productos) {
            System.out.println(producto);
        }
```

**Explicación técnica mientras lo escribimos.** La impresión permite inspeccionar qué productos sobrevivieron, pero HashSet no garantiza ni el orden de inserción ni el orden lexicográfico. La evaluación correcta compara pertenencia y cantidad, no posiciones ni orden de salida.

**Estado o evidencia tras este microbloque.** Aparecen Impresora y Computadora en algún orden; Televisor no aparece.

## Auditoría del artefacto antes de ejecutar

- Confirma que el archivo se llama `EJ08.java` y la clase pública `EJ08`; los `import` preceden a la clase, `main` es el punto de entrada y sus llaves están equilibradas.
- Confirma que `Producto.java` proviene de EJ07 sin modificar la igualdad lógica; el resultado no debe depender del orden en que HashSet imprime los productos.
- Contrasta cada bloque funcional de arriba con la versión completa; no debe haber una instrucción de comportamiento que aparezca por primera vez sin haberse explicado.

## Archivo `src/EJ08.java` completo al terminar

```java
import java.util.HashSet;

public class EJ08 {
    public static void main(String[] args) {
HashSet<Producto> productos = new HashSet<>();
boolean a1 = productos.add(new Producto("Impresora", 187.0));
boolean a2 = productos.add(new Producto("Computadora", 2356.0));
boolean a3 = productos.add(new Producto("Televisor", 650.0));
boolean duplicado = productos.add(new Producto("Impresora", 200.0));
System.out.println("Altas: " + a1 + "," + a2 + "," + a3);
System.out.println("Duplicado agregado: " + duplicado);
System.out.println("Únicos: " + productos.size());
boolean existe = productos.contains(new Producto("Impresora", 0));
System.out.println("Existe Impresora: " + existe);
boolean borrado = productos.remove(new Producto("Televisor", 0));
System.out.println("Eliminado Televisor: " + borrado);
System.out.println("Restantes: " + productos.size());
for (Producto producto : productos) {
    System.out.println(producto);
}
    }
}
```

## Antes de ejecutar: predicción

1. ¿Cuántos elementos quedan o se recorren al terminar EJ08, y por qué?
2. ¿Qué instrucción precisa causa la salida visible y qué método o condición interviene?
3. Si cambias el dato de prueba indicado a continuación, ¿cuál será el primer resultado diferente?

## Ejecutar y validar

En IntelliJ, ejecuta `EJ08.main()` con el triángulo verde. Desde la terminal de la raíz del proyecto, tras compilar con `javac -encoding UTF-8 -d out src/*.java` (Bash) o `javac -encoding UTF-8 -d out src\*.java` (Windows), ejecuta `java -cp out EJ08`. Comprueba literalmente la salida o, en HashSet, comprueba el conjunto de productos sin imponer orden.

**Salida esperada:**

```text
Altas: true,true,true
Duplicado agregado: false
Únicos: 3
Existe Impresora: true
Eliminado Televisor: true
Restantes: 2
Impresora - 187.0
Computadora - 2356.0
(El orden de las dos últimas líneas puede variar.)
```

**Interpretación.** La impresión permite inspeccionar qué productos sobrevivieron, pero HashSet no garantiza ni el orden de inserción ni el orden lexicográfico. La evaluación correcta compara pertenencia y cantidad, no posiciones ni orden de salida. Aparecen Impresora y Computadora en algún orden; Televisor no aparece. La prueba vale cuando puedes justificar el cambio de estado, no solamente repetir el texto de la consola.

**Variación A — prueba de transferencia.** Prueba `contains(new Producto("NoExiste", 0))`; debe devolver false. Restaura el código original antes de comparar.

**Variación B — comprobación negativa.** Exigir un orden específico al imprimir HashSet. Identifica la condición o llamada responsable, sin dejar una versión errónea como resultado final.

## Error o caso límite controlado y corrección

**Situación:** Exigir un orden específico al imprimir HashSet. **Causa:** El conjunto no garantiza orden de iteración, por lo que una prueba posicional puede fallar aunque los datos sean correctos. **Corrección:** Verifica size, add, contains y remove; acepta cualquiera de los órdenes de los dos productos que quedan.

## Comprueba que puedes explicarlo

Explica la relación entre el dato inicial y el resultado; identifica la línea exacta que recorre, compara, elimina o impide un duplicado, según corresponda; y justifica por qué la validación propuesta detecta un error real.

## T08 — Tarea espejo: Evitar duplicados y retirar un producto por identidad

**Enunciado:** Crea un HashSet con Mouse(35), Teclado(80) y Mouse(50); indica qué add falla, verifica contains de Mouse por nombre, retira Teclado y muestra la cardinalidad final.

**Archivo a construir:** `src/T08.java`; conserva la clase `Estudiante` o `Producto` que ya desarrollaste. **Restricción:** No afirmes un orden fijo al recorrer HashSet; usa objetos de consulta con mismo nombre.

**Ruta de trabajo:** crea una clase Java con `main`, inicia los objetos indicados, añade el mecanismo específico aprendido en EJ08 y muestra una comprobación visible. **Pista:** El precio del objeto usado para consultar no afecta equals si solo se compara el nombre.

**Evidencia y criterio de aceptación:** Repetido=false; únicos=2; contiene Mouse=true; elimina Teclado=true; restantes=1. La solución debe compilar; el resultado se explica en una oración señalando qué método causó el comportamiento. Esta tarea es para que la resuelvas: la solución docente no se incluye en esta guía.


---

## Cierre docente y transferencia a la siguiente clase

Hoy construimos objetos reales antes de colocarlos dentro de colecciones. En lugar de tratar la lista como un contenedor misterioso, aprendimos que cada llamada a `new Estudiante(...)` produce una instancia y que `ArrayList` conserva esas referencias. Primero verificamos las altas; luego contrastamos dos formas de recorrido: `for-each`, útil para presentar información, e `Iterator`, que incorpora métodos explícitos para saber si existe otro elemento y avanzar. La búsqueda mostró por qué `String.equals` comunica igualdad de contenido y por qué necesitamos una respuesta alternativa si el nombre consultado no aparece. También retiramos un objeto durante el recorrido de manera correcta con `Iterator.remove` y después aplicamos una condición de eliminación mediante `removeIf`.

En el catálogo de productos apareció una decisión distinta: la igualdad no se decide por el hecho de tener dos instancias creadas con `new`, sino por un criterio que escribimos en `Producto.equals`. Mantuvimos el mismo criterio en `hashCode` y verificamos el contrato con casos positivos y negativos. Finalmente comprobamos que `HashSet.add` puede rechazar un duplicado, que `contains` y `remove` actúan según esa igualdad, y que el orden de impresión del conjunto no es una condición de éxito. Para repasar, revisa especialmente los límites de las condiciones, el estado antes/después de borrar y la relación entre los dos métodos de identidad. La continuación natural es aplicar este criterio a otras colecciones y problemas de la programación orientada a objetos, sin añadir hoy tecnologías que no son necesarias. Puedes consultar materiales complementarios en Lideratec Academy, su blog https://lideratecacademy.com/blog/ y su canal https://www.youtube.com/@LideratecAcademy.

