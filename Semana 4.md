---
course_id: ISIL-POO-JAVA
session_id: S04
source_origin: PPT
status: draft
---

# Guía del Estudiante - S04: Estructuras de control en Java

## 1. Propósito de la sesión

Hasta este punto del curso has trabajado con clases, objetos, atributos, constructores y métodos. En esta sesión el foco cambia hacia una pregunta esencial: **¿cómo decide un programa qué instrucciones ejecutar y cuántas veces repetirlas?**

Construirás una colección progresiva de programas Java pequeños para observar el flujo de ejecución. Empezarás con decisiones simples (`if`), pasarás por alternativas (`if-else`, ternario y condicionales anidados), seleccionarás casos con `switch`, y después trabajarás repeticiones mediante `while`, `do-while` y `for`. Finalmente usarás contador, acumulador, `break` y `continue`.

El producto observable será una carpeta `src` con diez ejemplos funcionales y diez tareas espejo. Cada ejemplo se escribe, predice, compila, ejecuta, interpreta, modifica y corrige antes de avanzar.

## 2. Resultado observable

### Lectura sugerida del docente

Al finalizar la práctica no será suficiente decir "mi código ejecutó". Deberás poder explicar qué condición controla cada decisión, qué variable controla cada repetición, por qué un bucle termina, qué diferencia existe entre contar y acumular, y cómo `break` o `continue` cambian el recorrido. La sesión se construye de manera incremental: primero escribes una parte pequeña, luego explicas qué estado introduce, predices el resultado y recién entonces ejecutas. Cuando aparezca una salida distinta de la esperada, utilizarás esa diferencia como evidencia para diagnosticar el problema. El objetivo es que puedas mirar un bloque de Java y reconstruir mentalmente el camino que seguirá el programa. Ese criterio es más importante que copiar una sintaxis que compila una sola vez.

### Desempeños observables

Al finalizar podrás:

1. construir decisiones con `if`, `if-else` y `switch`;
2. interpretar una expresión ternaria simple;
3. seguir el flujo de un condicional anidado;
4. ejecutar y trazar `while`, `do-while` y `for`;
5. diferenciar contador de acumulador;
6. predecir preincremento y posincremento;
7. usar `break` y `continue` con intención explícita;
8. diagnosticar y corregir errores lógicos sencillos de control de flujo.

### Criterio de dominio

Dominas la sesión cuando puedes modificar datos o condiciones sin copiar una solución y, antes de ejecutar, explicar qué rama o iteraciones deberían ocurrir. La consola debe confirmar tu razonamiento.

## 3. Antes de iniciar

### Debe saber

- crear una clase Java;
- declarar atributos y variables;
- crear objetos con `new`;
- asignar valores;
- declarar y llamar métodos simples;
- usar `System.out.println`;
- reconocer tipos `int`, `double`, `char`, `String` y `boolean` a nivel básico.

### Debe tener disponible

- un JDK instalado;
- una terminal o consola;
- un editor/IDE para Java;
- permisos para crear carpetas y archivos.

### No se asumirá todavía

No necesitas colecciones, arreglos, excepciones, streams, lambdas, concurrencia, archivos, bases de datos ni frameworks. No los incorporaremos para resolver esta práctica.

# 4. Herramientas y recursos

## JDK

### Qué es y para qué se usa

El JDK contiene las herramientas necesarias para compilar y ejecutar programas Java. En esta guía utilizaremos principalmente `javac` para compilar y `java` para ejecutar.

### Recomendación

Para un entorno nuevo, utiliza **JDK 25 LTS**. Si el laboratorio institucional ya está estandarizado en **JDK 21 LTS**, puedes conservarlo: los ejemplos de esta sesión emplean sintaxis clásica compatible con ambos.

Sitio oficial de Oracle para descargas y versiones:

- https://www.oracle.com/java/technologies/downloads/

### Validación

Abre una terminal y ejecuta:

```bash
java -version
javac -version
```

Debes obtener una versión en ambos comandos. Si `java` funciona pero `javac` no, probablemente tienes un runtime disponible pero el compilador no está correctamente instalado o configurado en `PATH`.

## IntelliJ IDEA

### Qué es y por qué se recomienda

IntelliJ IDEA es un IDE para Java y Kotlin. Actualmente JetBrains distribuye un único IntelliJ IDEA; las funciones centrales para Java siguen disponibles sin costo. Para esta sesión no necesitas funciones Ultimate.

- Descarga oficial: https://www.jetbrains.com/idea/download/

### Instalación mínima

1. Abre la página oficial.
2. Selecciona el instalador de tu sistema operativo.
3. Descarga e instala IntelliJ IDEA.
4. Inicia el IDE.
5. Crea un proyecto Java sencillo seleccionando el JDK disponible.
6. No agregues Maven, Gradle ni frameworks para esta sesión: no son necesarios para los ejemplos.

### Qué NO necesitas instalar

- servidor de aplicaciones;
- base de datos;
- Spring Boot;
- librerías externas;
- plugins de terceros para ejecutar Java básico.

# 5. Preparación del entorno desde cero

## Ruta A - Ya tienes Java

En la terminal:

```bash
java -version
javac -version
```

Luego crea una carpeta de trabajo:

```bash
mkdir S04_EstructurasControl
cd S04_EstructurasControl
mkdir src
cd src
```

En Windows PowerShell, esos comandos funcionan de forma equivalente. Si la carpeta ya existe, no vuelvas a crearla; entra en ella.

Crea un archivo de prueba:

```java
public class PruebaEntorno {
    public static void main(String[] args) {
        System.out.println("Entorno Java listo");
    }
}
```

Guárdalo como `PruebaEntorno.java` y ejecuta:

```bash
javac PruebaEntorno.java
java PruebaEntorno
```

Resultado esperado:

```text
Entorno Java listo
```

Después puedes borrar `PruebaEntorno.class`; es un archivo generado por la compilación y no forma parte de los entregables.

## Ruta B - Equipo sin preparar

1. Descarga un JDK desde una fuente oficial o técnicamente confiable.
2. Instálalo siguiendo el instalador de tu sistema.
3. Cierra y vuelve a abrir la terminal.
4. Ejecuta `java -version` y `javac -version`.
5. Instala IntelliJ IDEA si deseas trabajar con IDE.
6. Crea el proyecto `S04_EstructurasControl`.
7. Dentro del proyecto crea una carpeta `src`.
8. Realiza la prueba mínima anterior antes de empezar EJ01.

> Si el equipo institucional ya tiene una versión de JDK definida por el curso, conserva esa versión para evitar diferencias entre máquinas. Esta guía no necesita características exclusivas de JDK 25.

# 6. Mapa de la práctica

| Ejemplo | Habilidad principal | Tarea espejo |
|---|---|---|
| EJ01 | if | T01 |
| EJ02 | if-else + ternario | T02 |
| EJ03 | if-else anidado | T03 |
| EJ04 | switch-case | T04 |
| EJ05 | ++, -- y asignación compuesta | T05 |
| EJ06 | while | T06 |
| EJ07 | contador + acumulador | T07 |
| EJ08 | do-while | T08 |
| EJ09 | for | T09 |
| EJ10 | break + continue | T10 |

Cada ejemplo es independiente. No es necesario ejecutar todos a la vez.


# EJ01 - Decidir con if: aprobar solo cuando la condición es verdadera

## Qué vamos a construir

Un programa que crea un estudiante, asigna una nota y ejecuta un mensaje únicamente cuando la expresión `nota >= 13` es verdadera.

## Qué aprenderás aquí

Relacionar una expresión booleana con la ejecución condicional de un bloque de código.

## Archivos que vamos a crear o modificar

- `src/EJ01_IfSimple.java`
- Después resolverás `src/T01_IfSimple.java` como T01.

## Punto de partida

Proyecto `S04_EstructurasControl` abierto, carpeta `src` disponible y los ejemplos anteriores cerrados o sin ejecutar. Cada archivo de esta guía es independiente y puede compilarse por separado.

## Paso 1 - Escribir el bloque 1

### Escribe

```java
public class EJ01_IfSimple {
    String nombre;
    int nota;
```

### Qué significa

Se declaran los atributos `nombre` y `nota`. La clase conserva el contexto de objetos trabajado previamente; la novedad de esta sesión será la decisión.

### Por qué lo hacemos ahora

Este bloque añade únicamente la responsabilidad necesaria para avanzar al siguiente estado sin ocultar lógica nueva dentro de un archivo ya terminado.

## Paso 2 - Escribir el bloque 2

### Escribe

```java

    public static void main(String[] args) {
        EJ01_IfSimple e1 = new EJ01_IfSimple();
        e1.nombre = "Rosa Aliaga";
```

### Qué significa

Se crea `e1`, se asignan datos concretos y se deja el estado listo para evaluar. La condición todavía no modifica el objeto: solo consulta su nota.

### Por qué lo hacemos ahora

Este bloque añade únicamente la responsabilidad necesaria para avanzar al siguiente estado sin ocultar lógica nueva dentro de un archivo ya terminado.

## Paso 3 - Escribir el bloque 3

### Escribe

```java
        e1.nota = 17;

        if (e1.nota >= 13) {
```

### Qué significa

`if (e1.nota >= 13)` produce un valor booleano. El bloque entre llaves se ejecuta únicamente si ese valor es `true`.

### Por qué lo hacemos ahora

Este bloque añade únicamente la responsabilidad necesaria para avanzar al siguiente estado sin ocultar lógica nueva dentro de un archivo ya terminado.

## Paso 4 - Escribir el bloque 4

### Escribe

```java
            System.out.println(e1.nombre + ": curso aprobado");
        }
    }
}
```

### Qué significa

Al cerrar el método y la clase, el programa queda listo para compilar. La evidencia será que el mensaje aparece para 17 y desaparece si la nota baja de 13.

### Por qué lo hacemos ahora

Este bloque añade únicamente la responsabilidad necesaria para avanzar al siguiente estado sin ocultar lógica nueva dentro de un archivo ya terminado.

## Archivo completo al terminar este ejemplo

```java
public class EJ01_IfSimple {
    String nombre;
    int nota;

    public static void main(String[] args) {
        EJ01_IfSimple e1 = new EJ01_IfSimple();
        e1.nombre = "Rosa Aliaga";
        e1.nota = 17;

        if (e1.nota >= 13) {
            System.out.println(e1.nombre + ": curso aprobado");
        }
    }
}
```

## Flujo mental

```text
objeto creado -> nota = 17 -> evaluar nota >= 13 -> true -> imprimir mensaje
```

## Traza manual antes de ejecutar

| Estado | nota | `nota >= 13` | Acción |
|---|---:|---|---|
| Inicial | 17 | true | entra al if e imprime aprobación |
| Variación | 11 | false | omite el bloque if |

## Antes de ejecutar: predicción

1. Responde: Con nota 13, ¿la condición `nota >= 13` es verdadera o falsa? ¿Por qué?
2. Escribe cuál será la primera línea visible en consola.
3. Indica qué condición o actualización provoca ese resultado.

## Ejecuta

Desde la carpeta `src`:

```bash
javac EJ01_IfSimple.java
java EJ01_IfSimple
```

## Resultado esperado

```text
Rosa Aliaga: curso aprobado
```

## Cómo interpretarlo

Verdadera, porque el operador `>=` incluye el límite 13. La salida no solo confirma que el archivo compila: evidencia el camino que siguió el flujo de ejecución. Relaciona siempre la salida con la condición, la actualización o la sentencia de control que la produjo.

## Variación A

Cambia `e1.nota` de 17 a 11. Predice qué ocurrirá: el programa no entra al bloque `if`, por lo que no imprime el mensaje de aprobación.

Vuelve a compilar y ejecutar después del cambio. No confíes en la ejecución anterior: el archivo fuente cambió y debe producir una nueva evidencia.

## Error controlado

Cambiar `>=` por `>` y probar con nota 13. El estudiante observará que 13 deja de aprobar, mostrando cómo un operador relacional cambia la regla.

### Por qué ocurre

`>` excluye el valor 13, mientras `>=` lo incluye. No es un error de compilación; es un error lógico respecto de la regla.

### Corrección razonada

Restaura el código del archivo completo del ejemplo y vuelve a ejecutar hasta recuperar la salida esperada. El objetivo no es memorizar la corrección, sino relacionar el cambio realizado con su efecto observable.

## Qué debes poder explicar con tus palabras

- Con nota 13, ¿la condición `nota >= 13` es verdadera o falsa? ¿Por qué?
- ¿Qué parte del programa controla el flujo?
- ¿Qué variable cambia o se consulta?
- ¿Qué evidencia en consola confirma tu explicación?

# T01 - Tarea espejo de EJ01

## Enunciado

Con `nota = 19`, mostrar `Rendimiento destacado` solo si la nota es 18 o mayor.

## Archivo a modificar

`src/T01_IfSimple.java`

## Restricción

Usar una sola sentencia `if`; no usar `else` ni operador ternario.

## Punto de partida

Crea el archivo con esta estructura inicial. Debe compilar aun antes de completar el TODO:

```java
public class T01_IfSimple {
    public static void main(String[] args) {
        String nombre = "Andrea";
        int nota = 19;

        // T01 - TODO
        // Objetivo: mostrar "Rendimiento destacado" solo cuando nota sea 18 o mayor.
        // Prediccion: con nota = 19, debe mostrarse el mensaje una sola vez.
        // Pista: utiliza una sentencia if con una expresion booleana.
        // Escribe tu if debajo de este comentario.
    }
}
```

## Pista

La condición puede escribirse como `nota >= 18`.

## Evidencia que debes mostrar

Captura o copia de la consola con el mensaje para nota 19 y ausencia del mensaje para nota 17.

## Cómo saber si está correcta

Debe compilar. Con 19 muestra el mensaje; con 17 no lo muestra. No compares solo texto: explica qué condición o actualización conduce al resultado.


# EJ02 - Dos caminos con if-else y la misma decisión con operador ternario

## Qué vamos a construir

Un programa que siempre produce una clasificación - aprobado o desaprobado - y después expresa la misma decisión como una expresión ternaria.

## Qué aprenderás aquí

Diferenciar un bloque de decisión `if-else` de una expresión que selecciona uno de dos valores.

## Archivos que vamos a crear o modificar

- `src/EJ02_IfElseTernario.java`
- Después resolverás `src/T02_IfElseTernario.java` como T02.

## Punto de partida

Proyecto `S04_EstructurasControl` abierto, carpeta `src` disponible y los ejemplos anteriores cerrados o sin ejecutar. Cada archivo de esta guía es independiente y puede compilarse por separado.

## Paso 1 - Escribir el bloque 1

### Escribe

```java
public class EJ02_IfElseTernario {
    String nombre;
    int nota;

    public static void main(String[] args) {
```

### Qué significa

La clase conserva dos atributos y un objeto estudiante para comparar dos formas de expresar la misma regla.

### Por qué lo hacemos ahora

Este bloque añade únicamente la responsabilidad necesaria para avanzar al siguiente estado sin ocultar lógica nueva dentro de un archivo ya terminado.

## Paso 2 - Escribir el bloque 2

### Escribe

```java
        EJ02_IfElseTernario e2 = new EJ02_IfElseTernario();
        e2.nombre = "Carlos Canales";
        e2.nota = 10;

        if (e2.nota >= 13) {
```

### Qué significa

El `if-else` obliga a elegir una de dos ramas. Para cualquier nota, exactamente una de esas ramas se ejecutará.

### Por qué lo hacemos ahora

Este bloque añade únicamente la responsabilidad necesaria para avanzar al siguiente estado sin ocultar lógica nueva dentro de un archivo ya terminado.

## Paso 3 - Escribir el bloque 3

### Escribe

```java
            System.out.println("if-else: curso aprobado");
        } else {
            System.out.println("if-else: curso desaprobado");
        }
```

### Qué significa

El operador ternario evalúa la misma condición, pero produce un valor que se asigna a `mensaje`. No es un bloque de sentencias equivalente a `if-else`; aquí se usa porque solo necesitamos seleccionar un texto.

### Por qué lo hacemos ahora

Este bloque añade únicamente la responsabilidad necesaria para avanzar al siguiente estado sin ocultar lógica nueva dentro de un archivo ya terminado.

## Paso 4 - Escribir el bloque 4

### Escribe

```java
        String mensaje = (e2.nota >= 13)
                ? "curso aprobado"
                : "curso desaprobado";
        System.out.println("ternario: " + mensaje);
    }
}
```

### Qué significa

Imprimir ambas respuestas permite validar que, con la misma entrada, la regla de negocio permanece equivalente.

### Por qué lo hacemos ahora

Este bloque añade únicamente la responsabilidad necesaria para avanzar al siguiente estado sin ocultar lógica nueva dentro de un archivo ya terminado.

## Archivo completo al terminar este ejemplo

```java
public class EJ02_IfElseTernario {
    String nombre;
    int nota;

    public static void main(String[] args) {
        EJ02_IfElseTernario e2 = new EJ02_IfElseTernario();
        e2.nombre = "Carlos Canales";
        e2.nota = 10;

        if (e2.nota >= 13) {
            System.out.println("if-else: curso aprobado");
        } else {
            System.out.println("if-else: curso desaprobado");
        }

        String mensaje = (e2.nota >= 13)
                ? "curso aprobado"
                : "curso desaprobado";
        System.out.println("ternario: " + mensaje);
    }
}
```

## Flujo mental

```text
nota = 10 -> evaluar >= 13 -> false -> ejecutar else -> construir mensaje ternario -> imprimir ambas salidas
```

## Traza manual antes de ejecutar

| nota | condición | rama if-else | valor ternario |
|---:|---|---|---|
| 10 | false | else | curso desaprobado |
| 15 | true | if | curso aprobado |

## Antes de ejecutar: predicción

1. Responde: ¿Por qué en este ejemplo `if-else` y ternario producen el mismo texto aunque no sean la misma estructura sintáctica?
2. Escribe cuál será la primera línea visible en consola.
3. Indica qué condición o actualización provoca ese resultado.

## Ejecuta

Desde la carpeta `src`:

```bash
javac EJ02_IfElseTernario.java
java EJ02_IfElseTernario
```

## Resultado esperado

```text
if-else: curso desaprobado
ternario: curso desaprobado
```

## Cómo interpretarlo

Porque ambos evalúan la misma condición y asocian los mismos resultados a verdadero y falso. La salida no solo confirma que el archivo compila: evidencia el camino que siguió el flujo de ejecución. Relaciona siempre la salida con la condición, la actualización o la sentencia de control que la produjo.

## Variación A

Cambia la nota a 15. Ambas salidas deben cambiar a `curso aprobado`.

Vuelve a compilar y ejecutar después del cambio. No confíes en la ejecución anterior: el archivo fuente cambió y debe producir una nueva evidencia.

## Error controlado

Escribir el ternario sin asignarlo ni imprimirlo, por ejemplo solo `(e2.nota >= 13) ? ...`. Java no acepta esa expresión como sentencia independiente en ese contexto.

### Por qué ocurre

El operador ternario produce un valor. Ese valor debe utilizarse, por ejemplo asignándolo a `mensaje`.

### Corrección razonada

Restaura el código del archivo completo del ejemplo y vuelve a ejecutar hasta recuperar la salida esperada. El objetivo no es memorizar la corrección, sino relacionar el cambio realizado con su efecto observable.

## Qué debes poder explicar con tus palabras

- ¿Por qué en este ejemplo `if-else` y ternario producen el mismo texto aunque no sean la misma estructura sintáctica?
- ¿Qué parte del programa controla el flujo?
- ¿Qué variable cambia o se consulta?
- ¿Qué evidencia en consola confirma tu explicación?

# T02 - Tarea espejo de EJ02

## Enunciado

Con `nota = 15`, producir `Aprobado`/`Desaprobado` primero con if-else y luego con ternario.

## Archivo a modificar

`src/T02_IfElseTernario.java`

## Restricción

Ambas soluciones deben coexistir y producir el mismo resultado para la misma nota.

## Punto de partida

Crea el archivo con esta estructura inicial. Debe compilar aun antes de completar el TODO:

```java
public class T02_IfElseTernario {
    public static void main(String[] args) {
        int nota = 15;

        // T02 - TODO A
        // Objetivo: usar if-else para imprimir "Aprobado" si nota >= 13; en caso contrario, "Desaprobado".

        // T02 - TODO B
        // Objetivo: producir el mismo resultado mediante operador ternario y guardarlo en String mensaje.
        // Pista: condicion ? valorVerdadero : valorFalso
    }
}
```

## Pista

Primero resuelve la rama verdadera/falsa; después reutiliza exactamente la misma condición en el ternario.

## Evidencia que debes mostrar

Consola mostrando dos líneas equivalentes para nota 15 y luego para nota 10.

## Cómo saber si está correcta

Para 15 ambas dicen Aprobado; para 10 ambas dicen Desaprobado. No compares solo texto: explica qué condición o actualización conduce al resultado.


# EJ03 - Evaluar más de una condición con if-else anidado

## Qué vamos a construir

Un método que compara dos enteros y distingue tres resultados: x mayor, y mayor o igualdad.

## Qué aprenderás aquí

Encadenar una segunda decisión únicamente cuando la primera no resolvió el escenario.

## Archivos que vamos a crear o modificar

- `src/EJ03_IfAnidado.java`
- Después resolverás `src/T03_IfAnidado.java` como T03.

## Punto de partida

Proyecto `S04_EstructurasControl` abierto, carpeta `src` disponible y los ejemplos anteriores cerrados o sin ejecutar. Cada archivo de esta guía es independiente y puede compilarse por separado.

## Paso 1 - Escribir el bloque 1

### Escribe

```java
public class EJ03_IfAnidado {
    public static void main(String[] args) {
        identificarMayor(19, 20);
    }
```

### Qué significa

`main` delega la comparación a `identificarMayor`. Esto mantiene el ejemplo cercano al enfoque de métodos ya trabajado.

### Por qué lo hacemos ahora

Este bloque añade únicamente la responsabilidad necesaria para avanzar al siguiente estado sin ocultar lógica nueva dentro de un archivo ya terminado.

## Paso 2 - Escribir el bloque 2

### Escribe

```java
    public static void identificarMayor(int x, int y) {
        String mensaje;

        if (x > y) {
            mensaje = x + " es el mayor";
        } else {
```

### Qué significa

Primero se pregunta si `x > y`. Si esa condición resuelve el caso, no se necesita comparar nada más.

### Por qué lo hacemos ahora

Este bloque añade únicamente la responsabilidad necesaria para avanzar al siguiente estado sin ocultar lógica nueva dentro de un archivo ya terminado.

## Paso 3 - Escribir el bloque 3

### Escribe

```java
            if (y > x) {
                mensaje = y + " es el mayor";
            } else {
                mensaje = "Los valores son iguales";
            }
```

### Qué significa

Solo cuando la primera condición es falsa se evalúa `y > x`. Si también es falsa, queda un único caso posible: igualdad.

### Por qué lo hacemos ahora

Este bloque añade únicamente la responsabilidad necesaria para avanzar al siguiente estado sin ocultar lógica nueva dentro de un archivo ya terminado.

## Paso 4 - Escribir el bloque 4

### Escribe

```java
        }

        System.out.println("x: " + x + ", y: " + y);
        System.out.println(mensaje);
    }
}
```

### Qué significa

Las dos impresiones permiten observar entrada y decisión final, facilitando la traza manual.

### Por qué lo hacemos ahora

Este bloque añade únicamente la responsabilidad necesaria para avanzar al siguiente estado sin ocultar lógica nueva dentro de un archivo ya terminado.

## Archivo completo al terminar este ejemplo

```java
public class EJ03_IfAnidado {
    public static void main(String[] args) {
        identificarMayor(19, 20);
    }

    public static void identificarMayor(int x, int y) {
        String mensaje;

        if (x > y) {
            mensaje = x + " es el mayor";
        } else {
            if (y > x) {
                mensaje = y + " es el mayor";
            } else {
                mensaje = "Los valores son iguales";
            }
        }

        System.out.println("x: " + x + ", y: " + y);
        System.out.println(mensaje);
    }
}
```

## Flujo mental

```text
comparar x > y -> false -> comparar y > x -> true -> seleccionar mensaje -> imprimir
```

## Traza manual antes de ejecutar

| x | y | x>y | y>x (solo si hace falta) | Resultado |
|---:|---:|---|---|---|
|19|20|false|true|20 es el mayor|
|20|20|false|false|iguales|

## Antes de ejecutar: predicción

1. Responde: ¿Qué condición solo se evalúa si `x > y` resulta falsa?
2. Escribe cuál será la primera línea visible en consola.
3. Indica qué condición o actualización provoca ese resultado.

## Ejecuta

Desde la carpeta `src`:

```bash
javac EJ03_IfAnidado.java
java EJ03_IfAnidado
```

## Resultado esperado

```text
x: 19, y: 20
20 es el mayor
```

## Cómo interpretarlo

La condición `y > x` que está dentro del `else`. La salida no solo confirma que el archivo compila: evidencia el camino que siguió el flujo de ejecución. Relaciona siempre la salida con la condición, la actualización o la sentencia de control que la produjo.

## Variación A

Ejecuta `identificarMayor(20, 20)`. Debe recorrer la primera condición, entrar al `else`, fallar la segunda y llegar a igualdad.

Vuelve a compilar y ejecutar después del cambio. No confíes en la ejecución anterior: el archivo fuente cambió y debe producir una nueva evidencia.

## Error controlado

Cambiar la segunda condición a `y >= x`. Con valores iguales, el programa dirá que y es el mayor, lo que contradice el caso de igualdad.

### Por qué ocurre

Al incluir igualdad en la segunda rama, el tercer caso queda inalcanzable para valores iguales.

### Corrección razonada

Restaura el código del archivo completo del ejemplo y vuelve a ejecutar hasta recuperar la salida esperada. El objetivo no es memorizar la corrección, sino relacionar el cambio realizado con su efecto observable.

## Qué debes poder explicar con tus palabras

- ¿Qué condición solo se evalúa si `x > y` resulta falsa?
- ¿Qué parte del programa controla el flujo?
- ¿Qué variable cambia o se consulta?
- ¿Qué evidencia en consola confirma tu explicación?

# T03 - Tarea espejo de EJ03

## Enunciado

Crear la lógica espejo para identificar el menor entre dos valores o informar igualdad.

## Archivo a modificar

`src/T03_IfAnidado.java`

## Restricción

Usar if-else anidado; no usar `Math.min`.

## Punto de partida

Crea el archivo con esta estructura inicial. Debe compilar aun antes de completar el TODO:

```java
public class T03_IfAnidado {
    public static void main(String[] args) {
        identificarMenor(8, 8);
    }

    public static void identificarMenor(int x, int y) {
        // T03 - TODO
        // Objetivo: indicar cual valor es menor o informar que ambos son iguales.
        // Restriccion: utiliza if-else anidado; no uses Math.min.
        // Prediccion para 8 y 8: debe informar que los valores son iguales.
    }
}
```

## Pista

Invierte los operadores `>` por `<`, conservando el tercer caso de igualdad.

## Evidencia que debes mostrar

Probar 5 y 9; 9 y 5; 8 y 8.

## Cómo saber si está correcta

Debe responder 5 es el menor, 5 es el menor y valores iguales, respectivamente. No compares solo texto: explica qué condición o actualización conduce al resultado.


# EJ04 - Seleccionar una operación con switch-case

## Qué vamos a construir

Una calculadora mínima que evalúa un operador y ejecuta el bloque correspondiente.

## Qué aprenderás aquí

Usar `switch` cuando una misma variable puede conducir a varios casos explícitos.

## Archivos que vamos a crear o modificar

- `src/EJ04_SwitchCalculadora.java`
- Después resolverás `src/T04_SwitchCalculadora.java` como T04.

## Punto de partida

Proyecto `S04_EstructurasControl` abierto, carpeta `src` disponible y los ejemplos anteriores cerrados o sin ejecutar. Cada archivo de esta guía es independiente y puede compilarse por separado.

## Paso 1 - Escribir el bloque 1

### Escribe

```java
public class EJ04_SwitchCalculadora {
    public static void main(String[] args) {
        double resultado = operarNumeros(12, 11, '+');
        System.out.println("Resultado: " + resultado);
    }

    public static double operarNumeros(int x, int y, char operador) {
```

### Qué significa

`main` llama a un método que recibe dos números y un operador. La selección se basa en un único valor: `operador`.

### Por qué lo hacemos ahora

Este bloque añade únicamente la responsabilidad necesaria para avanzar al siguiente estado sin ocultar lógica nueva dentro de un archivo ya terminado.

## Paso 2 - Escribir el bloque 2

### Escribe

```java
        double resultado = 0;

        switch (operador) {
            case '+':
                resultado = x + y;
                break;
            case '-':
```

### Qué significa

`switch` compara el operador con cada `case`. Cada caso asigna un resultado y `break` evita continuar hacia el siguiente caso.

### Por qué lo hacemos ahora

Este bloque añade únicamente la responsabilidad necesaria para avanzar al siguiente estado sin ocultar lógica nueva dentro de un archivo ya terminado.

## Paso 3 - Escribir el bloque 3

### Escribe

```java
                resultado = x - y;
                break;
            case '*':
                resultado = x * y;
                break;
            case '/':
                resultado = (double) x / y;
```

### Qué significa

La conversión `(double) x / y` evita que una división entre enteros pierda la parte decimal. Se conserva la estructura clásica de `switch` del material.

### Por qué lo hacemos ahora

Este bloque añade únicamente la responsabilidad necesaria para avanzar al siguiente estado sin ocultar lógica nueva dentro de un archivo ya terminado.

## Paso 4 - Escribir el bloque 4

### Escribe

```java
                break;
            default:
                System.out.println("Operador no reconocido");
        }

        return resultado;
    }
}
```

### Qué significa

El método retorna el resultado y `main` lo imprime. Si no coincide ningún caso, se utiliza `default`.

### Por qué lo hacemos ahora

Este bloque añade únicamente la responsabilidad necesaria para avanzar al siguiente estado sin ocultar lógica nueva dentro de un archivo ya terminado.

## Archivo completo al terminar este ejemplo

```java
public class EJ04_SwitchCalculadora {
    public static void main(String[] args) {
        double resultado = operarNumeros(12, 11, '+');
        System.out.println("Resultado: " + resultado);
    }

    public static double operarNumeros(int x, int y, char operador) {
        double resultado = 0;

        switch (operador) {
            case '+':
                resultado = x + y;
                break;
            case '-':
                resultado = x - y;
                break;
            case '*':
                resultado = x * y;
                break;
            case '/':
                resultado = (double) x / y;
                break;
            default:
                System.out.println("Operador no reconocido");
        }

        return resultado;
    }
}
```

## Flujo mental

```text
operador = + -> switch -> case + -> sumar -> break -> return -> imprimir
```

## Traza manual antes de ejecutar

| operador | case seleccionado | resultado | break |
|---|---|---:|---|
| + | `case '+'` | 23.0 | sale del switch |
| * | `case '*'` | 132.0 | sale del switch |

## Antes de ejecutar: predicción

1. Responde: ¿Qué función cumple `break` dentro de cada `case` en esta sintaxis clásica?
2. Escribe cuál será la primera línea visible en consola.
3. Indica qué condición o actualización provoca ese resultado.

## Ejecuta

Desde la carpeta `src`:

```bash
javac EJ04_SwitchCalculadora.java
java EJ04_SwitchCalculadora
```

## Resultado esperado

```text
Resultado: 23.0
```

## Cómo interpretarlo

Evita que, después de ejecutar el caso elegido, la ejecución continúe en los casos siguientes. La salida no solo confirma que el archivo compila: evidencia el camino que siguió el flujo de ejecución. Relaciona siempre la salida con la condición, la actualización o la sentencia de control que la produjo.

## Variación A

Cambia el operador a `*`; con 12 y 11 el resultado debe ser 132.0.

Vuelve a compilar y ejecutar después del cambio. No confíes en la ejecución anterior: el archivo fuente cambió y debe producir una nueva evidencia.

## Error controlado

Comenta el `break` del caso `+` y ejecuta de nuevo. Observarás que también se ejecuta el caso siguiente y el resultado termina siendo el de la resta.

### Por qué ocurre

En el `switch` clásico, si no aparece `break`, la ejecución continúa en los casos siguientes hasta encontrar una salida del switch.

### Corrección razonada

Restaura el código del archivo completo del ejemplo y vuelve a ejecutar hasta recuperar la salida esperada. El objetivo no es memorizar la corrección, sino relacionar el cambio realizado con su efecto observable.

## Qué debes poder explicar con tus palabras

- ¿Qué función cumple `break` dentro de cada `case` en esta sintaxis clásica?
- ¿Qué parte del programa controla el flujo?
- ¿Qué variable cambia o se consulta?
- ¿Qué evidencia en consola confirma tu explicación?

# T04 - Tarea espejo de EJ04

## Enunciado

Completar un switch que soporte +, -, *, / y `%`; para 20 % 6 debe producir 2.

## Archivo a modificar

`src/T04_SwitchCalculadora.java`

## Restricción

Utilizar switch clásico y `break` en los casos que no deben caer al siguiente.

## Punto de partida

Crea el archivo con esta estructura inicial. Debe compilar aun antes de completar el TODO:

```java
public class T04_SwitchCalculadora {
    public static void main(String[] args) {
        int x = 20;
        int y = 6;
        char operador = '%';

        // T04 - TODO
        // Objetivo: usar switch para calcular +, -, *, / y %.
        // Para los datos actuales, debe mostrarse 2 como residuo de 20 % 6.
        // Pista: cada case clasico debe terminar con break cuando no deseas continuar al siguiente case.
    }
}
```

## Pista

El residuo se calcula con `x % y`.

## Evidencia que debes mostrar

Mostrar al menos dos pruebas: `%` y otra operación.

## Cómo saber si está correcta

Con 20, 6 y `%`, el resultado es 2.0; otra operación también debe coincidir con el cálculo esperado. No compares solo texto: explica qué condición o actualización conduce al resultado.


# EJ05 - Actualizar variables: incremento, decremento y asignación compuesta

## Qué vamos a construir

Un programa que permite observar la diferencia entre usar el valor incrementado antes o después de asignarlo, y luego aplica operadores de asignación compuesta.

## Qué aprenderás aquí

Interpretar el momento en que cambia una variable y reconocer formas compactas de actualizarla.

## Archivos que vamos a crear o modificar

- `src/EJ05_OperadoresActualizacion.java`
- Después resolverás `src/T05_OperadoresActualizacion.java` como T05.

## Punto de partida

Proyecto `S04_EstructurasControl` abierto, carpeta `src` disponible y los ejemplos anteriores cerrados o sin ejecutar. Cada archivo de esta guía es independiente y puede compilarse por separado.

## Paso 1 - Escribir el bloque 1

### Escribe

```java
public class EJ05_OperadoresActualizacion {
    public static void main(String[] args) {
        int a = 10;
        int b = ++a;
        System.out.println("Preincremento -> a: " + a + ", b: " + b);
```

### Qué significa

El primer bloque permite observar preincremento: la variable cambia antes de que su valor sea entregado a `b`.

### Por qué lo hacemos ahora

Este bloque añade únicamente la responsabilidad necesaria para avanzar al siguiente estado sin ocultar lógica nueva dentro de un archivo ya terminado.

## Paso 2 - Escribir el bloque 2

### Escribe

```java

        int x = 10;
        int y = x++;
        System.out.println("Posincremento -> x: " + x + ", y: " + y);

        int c = 10;
```

### Qué significa

El segundo bloque muestra posincremento: `y` recibe el valor anterior y luego `x` aumenta.

### Por qué lo hacemos ahora

Este bloque añade únicamente la responsabilidad necesaria para avanzar al siguiente estado sin ocultar lógica nueva dentro de un archivo ya terminado.

## Paso 3 - Escribir el bloque 3

### Escribe

```java
        c += 5;
        System.out.println("Luego de += 5: " + c);
        c -= 3;
        System.out.println("Luego de -= 3: " + c);
        c *= 4;
        System.out.println("Luego de *= 4: " + c);
```

### Qué significa

Las asignaciones compuestas actualizan `c` reutilizando su valor actual. Cada línea equivale a una operación seguida de asignación.

### Por qué lo hacemos ahora

Este bloque añade únicamente la responsabilidad necesaria para avanzar al siguiente estado sin ocultar lógica nueva dentro de un archivo ya terminado.

## Paso 4 - Escribir el bloque 4

### Escribe

```java
        c /= 2;
        System.out.println("Luego de /= 2: " + c);
        c %= 5;
        System.out.println("Luego de %= 5: " + c);
    }
}
```

### Qué significa

La salida después de cada cambio convierte el estado interno en evidencia observable; por eso no ejecutaremos todo sin detenernos a predecir.

### Por qué lo hacemos ahora

Este bloque añade únicamente la responsabilidad necesaria para avanzar al siguiente estado sin ocultar lógica nueva dentro de un archivo ya terminado.

## Archivo completo al terminar este ejemplo

```java
public class EJ05_OperadoresActualizacion {
    public static void main(String[] args) {
        int a = 10;
        int b = ++a;
        System.out.println("Preincremento -> a: " + a + ", b: " + b);

        int x = 10;
        int y = x++;
        System.out.println("Posincremento -> x: " + x + ", y: " + y);

        int c = 10;
        c += 5;
        System.out.println("Luego de += 5: " + c);
        c -= 3;
        System.out.println("Luego de -= 3: " + c);
        c *= 4;
        System.out.println("Luego de *= 4: " + c);
        c /= 2;
        System.out.println("Luego de /= 2: " + c);
        c %= 5;
        System.out.println("Luego de %= 5: " + c);
    }
}
```

## Flujo mental

```text
a=10 -> ++a produce 11 -> b recibe 11; x=10 -> y recibe 10 -> x++ deja x=11; c cambia secuencialmente
```

## Traza manual antes de ejecutar

| Instrucción | valor original | valor asignado | valor final original |
|---|---:|---:|---:|
| `b = ++a` | 10 | 11 | 11 |
| `y = x++` | 10 | 10 | 11 |

## Antes de ejecutar: predicción

1. Responde: Después de `int x=10; int y=x++;`, ¿cuáles son los valores de x e y?
2. Escribe cuál será la primera línea visible en consola.
3. Indica qué condición o actualización provoca ese resultado.

## Ejecuta

Desde la carpeta `src`:

```bash
javac EJ05_OperadoresActualizacion.java
java EJ05_OperadoresActualizacion
```

## Resultado esperado

```text
Preincremento -> a: 11, b: 11
Posincremento -> x: 11, y: 10
Luego de += 5: 15
Luego de -= 3: 12
Luego de *= 4: 48
Luego de /= 2: 24
Luego de %= 5: 4
```

## Cómo interpretarlo

x vale 11 e y vale 10. La salida no solo confirma que el archivo compila: evidencia el camino que siguió el flujo de ejecución. Relaciona siempre la salida con la condición, la actualización o la sentencia de control que la produjo.

## Variación A

Repite el ejercicio sustituyendo incremento por decremento: `--a` y `x--`. Predice primero los pares de valores.

Vuelve a compilar y ejecutar después del cambio. No confíes en la ejecución anterior: el archivo fuente cambió y debe producir una nueva evidencia.

## Error controlado

Suponer que `int y = x++;` deja `y` en 11. La ejecución mostrará y=10 mientras x termina en 11.

### Por qué ocurre

El posincremento entrega primero el valor actual para la asignación y después incrementa la variable original.

### Corrección razonada

Restaura el código del archivo completo del ejemplo y vuelve a ejecutar hasta recuperar la salida esperada. El objetivo no es memorizar la corrección, sino relacionar el cambio realizado con su efecto observable.

## Qué debes poder explicar con tus palabras

- Después de `int x=10; int y=x++;`, ¿cuáles son los valores de x e y?
- ¿Qué parte del programa controla el flujo?
- ¿Qué variable cambia o se consulta?
- ¿Qué evidencia en consola confirma tu explicación?

# T05 - Tarea espejo de EJ05

## Enunciado

Partir de valor=8, comparar preincremento y posincremento y después aplicar `+=4`, `*=2`, `-=3`.

## Archivo a modificar

`src/T05_OperadoresActualizacion.java`

## Restricción

Reiniciar `valor` antes de cada comparación para no mezclar estados.

## Punto de partida

Crea el archivo con esta estructura inicial. Debe compilar aun antes de completar el TODO:

```java
public class T05_OperadoresActualizacion {
    public static void main(String[] args) {
        int valor = 8;

        // T05 - TODO A
        // Guarda en otra variable el resultado de ++valor y muestra ambas variables.

        // T05 - TODO B
        // Reinicia valor en 8. Guarda valor++ en otra variable y muestra ambas variables.

        // T05 - TODO C
        // Reinicia valor en 8 y aplica, en orden: += 4, *= 2, -= 3.
        // Predice el valor final antes de ejecutar.
    }
}
```

## Pista

Predice por separado el valor de la variable original y el valor asignado.

## Evidencia que debes mostrar

Consola con los estados de pre, post y valor final de asignaciones compuestas.

## Cómo saber si está correcta

Pre: valor 9/pre 9; Post: valor 9/post 8; valor final compuesto: 21. No compares solo texto: explica qué condición o actualización conduce al resultado.


# EJ06 - Repetir mientras una condición sea verdadera con while

## Qué vamos a construir

Un recorrido desde un límite inferior hasta uno superior que imprime únicamente los valores pares.

## Qué aprenderás aquí

Controlar una repetición con una condición evaluada al inicio y actualizar manualmente la variable de control.

## Archivos que vamos a crear o modificar

- `src/EJ06_WhilePares.java`
- Después resolverás `src/T06_WhileImpares.java` como T06.

## Punto de partida

Proyecto `S04_EstructurasControl` abierto, carpeta `src` disponible y los ejemplos anteriores cerrados o sin ejecutar. Cada archivo de esta guía es independiente y puede compilarse por separado.

## Paso 1 - Escribir el bloque 1

### Escribe

```java
public class EJ06_WhilePares {
    public static void main(String[] args) {
        identificarPares(13, 20);
```

### Qué significa

`main` entrega un rango al método. La variable `a` actuará como control del bucle.

### Por qué lo hacemos ahora

Este bloque añade únicamente la responsabilidad necesaria para avanzar al siguiente estado sin ocultar lógica nueva dentro de un archivo ya terminado.

## Paso 2 - Escribir el bloque 2

### Escribe

```java
    }

    public static void identificarPares(int a, int b) {
        while (a <= b) {
```

### Qué significa

`while (a <= b)` evalúa la condición antes de cada vuelta. Si es falsa desde el inicio, el cuerpo no se ejecuta.

### Por qué lo hacemos ahora

Este bloque añade únicamente la responsabilidad necesaria para avanzar al siguiente estado sin ocultar lógica nueva dentro de un archivo ya terminado.

## Paso 3 - Escribir el bloque 3

### Escribe

```java
            if (a % 2 == 0) {
                System.out.println(a + " es par");
            }
```

### Qué significa

Dentro del bucle, `% 2 == 0` filtra los pares. `a++` es esencial porque cambia la variable que participa en la condición.

### Por qué lo hacemos ahora

Este bloque añade únicamente la responsabilidad necesaria para avanzar al siguiente estado sin ocultar lógica nueva dentro de un archivo ya terminado.

## Paso 4 - Escribir el bloque 4

### Escribe

```java
            a++;
        }
    }
}
```

### Qué significa

Cuando `a` llega a 21, `a <= b` es falsa y el bucle termina.

### Por qué lo hacemos ahora

Este bloque añade únicamente la responsabilidad necesaria para avanzar al siguiente estado sin ocultar lógica nueva dentro de un archivo ya terminado.

## Archivo completo al terminar este ejemplo

```java
public class EJ06_WhilePares {
    public static void main(String[] args) {
        identificarPares(13, 20);
    }

    public static void identificarPares(int a, int b) {
        while (a <= b) {
            if (a % 2 == 0) {
                System.out.println(a + " es par");
            }
            a++;
        }
    }
}
```

## Flujo mental

```text
a=13 -> evaluar a<=20 -> comprobar paridad -> a++ -> volver a condición -> terminar cuando a=21
```

## Traza manual antes de ejecutar

| a al entrar | a<=20 | a%2==0 | imprime | a después |
|---:|---|---|---|---:|
|13|true|false|-|14|
|14|true|true|14 es par|15|
|15|true|false|-|16|
|16|true|true|16 es par|17|

## Antes de ejecutar: predicción

1. Responde: ¿Qué línea garantiza que el while avance hacia su condición de término?
2. Escribe cuál será la primera línea visible en consola.
3. Indica qué condición o actualización provoca ese resultado.

## Ejecuta

Desde la carpeta `src`:

```bash
javac EJ06_WhilePares.java
java EJ06_WhilePares
```

## Resultado esperado

```text
14 es par
16 es par
18 es par
20 es par
```

## Cómo interpretarlo

`a++;`, porque incrementa la variable usada en `a <= b`. La salida no solo confirma que el archivo compila: evidencia el camino que siguió el flujo de ejecución. Relaciona siempre la salida con la condición, la actualización o la sentencia de control que la produjo.

## Variación A

Cambia el límite inicial a 21 y el final a 20. Como la condición se evalúa antes, el cuerpo no se ejecuta ninguna vez.

Vuelve a compilar y ejecutar después del cambio. No confíes en la ejecución anterior: el archivo fuente cambió y debe producir una nueva evidencia.

## Error controlado

Comenta temporalmente `a++`. El valor de a nunca cambia y la condición permanece verdadera, produciendo un bucle que no termina por sí solo.

### Por qué ocurre

La condición depende de `a`, por lo que alguna sentencia del cuerpo debe acercarla al estado de salida.

### Corrección razonada

Restaura el código del archivo completo del ejemplo y vuelve a ejecutar hasta recuperar la salida esperada. El objetivo no es memorizar la corrección, sino relacionar el cambio realizado con su efecto observable.

## Qué debes poder explicar con tus palabras

- ¿Qué línea garantiza que el while avance hacia su condición de término?
- ¿Qué parte del programa controla el flujo?
- ¿Qué variable cambia o se consulta?
- ¿Qué evidencia en consola confirma tu explicación?

# T06 - Tarea espejo de EJ06

## Enunciado

Recorrer del 13 al 20 con while e imprimir solo los impares.

## Archivo a modificar

`src/T06_WhileImpares.java`

## Restricción

Actualizar la variable de control dentro del while.

## Punto de partida

Crea el archivo con esta estructura inicial. Debe compilar aun antes de completar el TODO:

```java
public class T06_WhileImpares {
    public static void main(String[] args) {
        int actual = 13;
        int limite = 20;

        // T06 - TODO
        // Objetivo: recorrer desde actual hasta limite con while e imprimir solo numeros impares.
        // Restriccion: actualiza la variable de control dentro del bucle.
        // Pista: un numero impar deja residuo distinto de cero al dividirse entre 2.
    }
}
```

## Pista

Puedes comprobar `actual % 2 != 0`.

## Evidencia que debes mostrar

Consola con 13, 15, 17 y 19; además, explicar qué ocurre si se elimina el incremento.

## Cómo saber si está correcta

Debe terminar y mostrar exactamente los impares del rango. No compares solo texto: explica qué condición o actualización conduce al resultado.


# EJ07 - Contar y acumular dentro de un bucle

## Qué vamos a construir

Un while que identifica múltiplos de 6; una variable cuenta coincidencias y otra suma los valores encontrados.

## Qué aprenderás aquí

Distinguir una variable que registra cuántas veces ocurre algo de otra que conserva una suma progresiva.

## Archivos que vamos a crear o modificar

- `src/EJ07_ContadorAcumulador.java`
- Después resolverás `src/T07_ContadorAcumulador.java` como T07.

## Punto de partida

Proyecto `S04_EstructurasControl` abierto, carpeta `src` disponible y los ejemplos anteriores cerrados o sin ejecutar. Cada archivo de esta guía es independiente y puede compilarse por separado.

## Paso 1 - Escribir el bloque 1

### Escribe

```java
public class EJ07_ContadorAcumulador {
    public static void main(String[] args) {
        int cantidadMultiplos = 0;
        int sumaMultiplos = 0;
```

### Qué significa

Se inicializan cuatro roles distintos: contador, acumulador y dos límites. Separar roles facilita interpretar el algoritmo.

### Por qué lo hacemos ahora

Este bloque añade únicamente la responsabilidad necesaria para avanzar al siguiente estado sin ocultar lógica nueva dentro de un archivo ya terminado.

## Paso 2 - Escribir el bloque 2

### Escribe

```java
        int limiteInferior = 1;
        int limiteSuperior = 50;

        while (limiteInferior <= limiteSuperior) {
            if (limiteInferior % 6 == 0) {
```

### Qué significa

El `while` recorre todo el intervalo. El `if` decide si el valor actual es múltiplo de 6.

### Por qué lo hacemos ahora

Este bloque añade únicamente la responsabilidad necesaria para avanzar al siguiente estado sin ocultar lógica nueva dentro de un archivo ya terminado.

## Paso 3 - Escribir el bloque 3

### Escribe

```java
                cantidadMultiplos++;
                sumaMultiplos += limiteInferior;
            }
            limiteInferior++;
        }
```

### Qué significa

Cuando hay coincidencia, `cantidadMultiplos++` registra una ocurrencia y `sumaMultiplos += limiteInferior` agrega el valor encontrado.

### Por qué lo hacemos ahora

Este bloque añade únicamente la responsabilidad necesaria para avanzar al siguiente estado sin ocultar lógica nueva dentro de un archivo ya terminado.

## Paso 4 - Escribir el bloque 4

### Escribe

```java

        System.out.println("Cantidad de multiplos de 6: " + cantidadMultiplos);
        System.out.println("Suma de los multiplos de 6: " + sumaMultiplos);
    }
}
```

### Qué significa

Al finalizar se muestran dos evidencias diferentes: cuántos valores cumplieron y cuánto suman en total.

### Por qué lo hacemos ahora

Este bloque añade únicamente la responsabilidad necesaria para avanzar al siguiente estado sin ocultar lógica nueva dentro de un archivo ya terminado.

## Archivo completo al terminar este ejemplo

```java
public class EJ07_ContadorAcumulador {
    public static void main(String[] args) {
        int cantidadMultiplos = 0;
        int sumaMultiplos = 0;
        int limiteInferior = 1;
        int limiteSuperior = 50;

        while (limiteInferior <= limiteSuperior) {
            if (limiteInferior % 6 == 0) {
                cantidadMultiplos++;
                sumaMultiplos += limiteInferior;
            }
            limiteInferior++;
        }

        System.out.println("Cantidad de multiplos de 6: " + cantidadMultiplos);
        System.out.println("Suma de los multiplos de 6: " + sumaMultiplos);
    }
}
```

## Flujo mental

```text
recorrer 1..50 -> si es múltiplo de 6 -> cantidad++ y suma += valor -> avanzar -> mostrar ambos resultados
```

## Traza manual antes de ejecutar

| actual | múltiplo de 6 | cantidad | suma |
|---:|---|---:|---:|
|5|no|0|0|
|6|sí|1|6|
|12|sí|2|18|
|18|sí|3|36|

## Antes de ejecutar: predicción

1. Responde: ¿Por qué `cantidadMultiplos++` y `sumaMultiplos += limiteInferior` no son equivalentes?
2. Escribe cuál será la primera línea visible en consola.
3. Indica qué condición o actualización provoca ese resultado.

## Ejecuta

Desde la carpeta `src`:

```bash
javac EJ07_ContadorAcumulador.java
java EJ07_ContadorAcumulador
```

## Resultado esperado

```text
Cantidad de multiplos de 6: 8
Suma de los multiplos de 6: 216
```

## Cómo interpretarlo

El contador aumenta en una unidad por coincidencia; el acumulador agrega el valor encontrado. La salida no solo confirma que el archivo compila: evidencia el camino que siguió el flujo de ejecución. Relaciona siempre la salida con la condición, la actualización o la sentencia de control que la produjo.

## Variación A

Cambia el divisor de 6 a 5 y predice cuántos múltiplos habrá entre 1 y 50 antes de ejecutar.

Vuelve a compilar y ejecutar después del cambio. No confíes en la ejecución anterior: el archivo fuente cambió y debe producir una nueva evidencia.

## Error controlado

Inicializa `sumaMultiplos` en 1. La cantidad seguirá siendo correcta, pero la suma quedará desplazada en una unidad.

### Por qué ocurre

Un acumulador debe iniciar en el elemento neutro de la operación que representa; para suma, ese valor es 0.

### Corrección razonada

Restaura el código del archivo completo del ejemplo y vuelve a ejecutar hasta recuperar la salida esperada. El objetivo no es memorizar la corrección, sino relacionar el cambio realizado con su efecto observable.

## Qué debes poder explicar con tus palabras

- ¿Por qué `cantidadMultiplos++` y `sumaMultiplos += limiteInferior` no son equivalentes?
- ¿Qué parte del programa controla el flujo?
- ¿Qué variable cambia o se consulta?
- ¿Qué evidencia en consola confirma tu explicación?

# T07 - Tarea espejo de EJ07

## Enunciado

Contar y sumar múltiplos de 4 entre 1 y 40.

## Archivo a modificar

`src/T07_ContadorAcumulador.java`

## Restricción

Usar un contador y un acumulador separados.

## Punto de partida

Crea el archivo con esta estructura inicial. Debe compilar aun antes de completar el TODO:

```java
public class T07_ContadorAcumulador {
    public static void main(String[] args) {
        int actual = 1;
        int limite = 40;
        int cantidad = 0;
        int suma = 0;

        // T07 - TODO
        // Objetivo: contar y sumar los multiplos de 4 entre 1 y 40, inclusive.
        // Evidencia esperada: cantidad = 10 y suma = 220.
        // Pista: actual % 4 == 0 identifica un multiplo de 4.
    }
}
```

## Pista

El contador aumenta en 1; el acumulador aumenta en `actual`.

## Evidencia que debes mostrar

Consola con cantidad=10 y suma=220.

## Cómo saber si está correcta

Los resultados esperados son 10 y 220; además el bucle debe terminar en 41. No compares solo texto: explica qué condición o actualización conduce al resultado.


# EJ08 - Garantizar al menos una ejecución con do-while: Fibonacci

## Qué vamos a construir

Una generación de diez términos de Fibonacci que actualiza dos valores de estado y controla la cantidad de términos con `k`.

## Qué aprenderás aquí

Reconocer que el cuerpo de `do-while` se ejecuta antes de evaluar la condición y seguir el cambio de estado entre iteraciones.

## Archivos que vamos a crear o modificar

- `src/EJ08_DoWhileFibonacci.java`
- Después resolverás `src/T08_DoWhileFibonacci.java` como T08.

## Punto de partida

Proyecto `S04_EstructurasControl` abierto, carpeta `src` disponible y los ejemplos anteriores cerrados o sin ejecutar. Cada archivo de esta guía es independiente y puede compilarse por separado.

## Paso 1 - Escribir el bloque 1

### Escribe

```java
public class EJ08_DoWhileFibonacci {
    public static void main(String[] args) {
        generarFibonacci(10);
    }
```

### Qué significa

Se crean los dos valores base de Fibonacci y una variable `k` que indica cuántos términos ya están representados.

### Por qué lo hacemos ahora

Este bloque añade únicamente la responsabilidad necesaria para avanzar al siguiente estado sin ocultar lógica nueva dentro de un archivo ya terminado.

## Paso 2 - Escribir el bloque 2

### Escribe

```java
    public static void generarFibonacci(int n) {
        int a = 0;
        int b = 1;
        int k = 2;

        System.out.print(a + " " + b);
```

### Qué significa

Los valores base se imprimen antes del `do`. Luego, dentro del bucle, `c` se calcula a partir de `a + b`.

### Por qué lo hacemos ahora

Este bloque añade únicamente la responsabilidad necesaria para avanzar al siguiente estado sin ocultar lógica nueva dentro de un archivo ya terminado.

## Paso 3 - Escribir el bloque 3

### Escribe

```java

        do {
            int c = a + b;
            System.out.print(" " + c);
            a = b;
            b = c;
```

### Qué significa

El orden `a = b; b = c;` desplaza el estado para preparar la siguiente iteración. `k++` registra un término adicional.

### Por qué lo hacemos ahora

Este bloque añade únicamente la responsabilidad necesaria para avanzar al siguiente estado sin ocultar lógica nueva dentro de un archivo ya terminado.

## Paso 4 - Escribir el bloque 4

### Escribe

```java
            k++;
        } while (k < n);

        System.out.println();
    }
}
```

### Qué significa

La condición se evalúa al final, característica central de `do-while`. Con n=10 la secuencia contiene diez términos.

### Por qué lo hacemos ahora

Este bloque añade únicamente la responsabilidad necesaria para avanzar al siguiente estado sin ocultar lógica nueva dentro de un archivo ya terminado.

## Archivo completo al terminar este ejemplo

```java
public class EJ08_DoWhileFibonacci {
    public static void main(String[] args) {
        generarFibonacci(10);
    }

    public static void generarFibonacci(int n) {
        int a = 0;
        int b = 1;
        int k = 2;

        System.out.print(a + " " + b);

        do {
            int c = a + b;
            System.out.print(" " + c);
            a = b;
            b = c;
            k++;
        } while (k < n);

        System.out.println();
    }
}
```

## Flujo mental

```text
a=0,b=1 -> imprimir base -> do: c=a+b -> imprimir c -> a=b -> b=c -> k++ -> evaluar k<n
```

## Traza manual antes de ejecutar

| iteración | a antes | b antes | c=a+b | a después | b después |
|---:|---:|---:|---:|---:|---:|
|1|0|1|1|1|1|
|2|1|1|2|1|2|
|3|1|2|3|2|3|

## Antes de ejecutar: predicción

1. Responde: ¿Qué representan a y b justo antes de calcular un nuevo término c?
2. Escribe cuál será la primera línea visible en consola.
3. Indica qué condición o actualización provoca ese resultado.

## Ejecuta

Desde la carpeta `src`:

```bash
javac EJ08_DoWhileFibonacci.java
java EJ08_DoWhileFibonacci
```

## Resultado esperado

```text
0 1 1 2 3 5 8 13 21 34
```

## Cómo interpretarlo

Los dos términos anteriores necesarios para calcular el siguiente término. La salida no solo confirma que el archivo compila: evidencia el camino que siguió el flujo de ejecución. Relaciona siempre la salida con la condición, la actualización o la sentencia de control que la produjo.

## Variación A

Cambia n de 10 a 8. La secuencia debe terminar en 13.

Vuelve a compilar y ejecutar después del cambio. No confíes en la ejecución anterior: el archivo fuente cambió y debe producir una nueva evidencia.

## Error controlado

Intercambia el orden de las asignaciones `a = b; b = c;` por `b = c; a = b;`. La secuencia deja de representar correctamente el estado anterior.

### Por qué ocurre

La siguiente iteración necesita conservar el antiguo valor de b en a antes de reemplazar b por c.

### Corrección razonada

Restaura el código del archivo completo del ejemplo y vuelve a ejecutar hasta recuperar la salida esperada. El objetivo no es memorizar la corrección, sino relacionar el cambio realizado con su efecto observable.

## Qué debes poder explicar con tus palabras

- ¿Qué representan a y b justo antes de calcular un nuevo término c?
- ¿Qué parte del programa controla el flujo?
- ¿Qué variable cambia o se consulta?
- ¿Qué evidencia en consola confirma tu explicación?

# T08 - Tarea espejo de EJ08

## Enunciado

Generar exactamente los primeros 8 términos de Fibonacci con do-while.

## Archivo a modificar

`src/T08_DoWhileFibonacci.java`

## Restricción

Usar do-while y conservar variables de estado equivalentes a a, b y un contador.

## Punto de partida

Crea el archivo con esta estructura inicial. Debe compilar aun antes de completar el TODO:

```java
public class T08_DoWhileFibonacci {
    public static void main(String[] args) {
        int n = 8;

        // T08 - TODO
        // Objetivo: generar los primeros 8 terminos de Fibonacci con do-while.
        // Salida esperada: 0 1 1 2 3 5 8 13
        // Conserva las variables a, b y una variable de control para la cantidad de terminos.
    }
}
```

## Pista

La base 0 y 1 ya representa dos términos; el contador puede iniciar en 2.

## Evidencia que debes mostrar

Salida `0 1 1 2 3 5 8 13` y una traza manual de al menos tres iteraciones.

## Cómo saber si está correcta

Debe imprimir ocho términos y terminar en 13. No compares solo texto: explica qué condición o actualización conduce al resultado.


# EJ09 - Repetición controlada con for: calcular un factorial

## Qué vamos a construir

Un cálculo factorial donde la inicialización, condición y actualización del contador se concentran en el encabezado del `for`.

## Qué aprenderás aquí

Usar `for` cuando el patrón de iteración puede expresarse claramente mediante inicio, condición y actualización.

## Archivos que vamos a crear o modificar

- `src/EJ09_ForFactorial.java`
- Después resolverás `src/T09_ForFactorial.java` como T09.

## Punto de partida

Proyecto `S04_EstructurasControl` abierto, carpeta `src` disponible y los ejemplos anteriores cerrados o sin ejecutar. Cada archivo de esta guía es independiente y puede compilarse por separado.

## Paso 1 - Escribir el bloque 1

### Escribe

```java
public class EJ09_ForFactorial {
    public static void main(String[] args) {
        calcularFactorial(10);
    }
```

### Qué significa

`main` envía n=10 al método. `factor` comienza en 1 porque almacenará un producto acumulativo.

### Por qué lo hacemos ahora

Este bloque añade únicamente la responsabilidad necesaria para avanzar al siguiente estado sin ocultar lógica nueva dentro de un archivo ya terminado.

## Paso 2 - Escribir el bloque 2

### Escribe

```java

    public static void calcularFactorial(int n) {
        int factor = 1;
```

### Qué significa

El encabezado del `for` concentra inicialización (`k=2`), condición (`k<=n`) y actualización (`k++`).

### Por qué lo hacemos ahora

Este bloque añade únicamente la responsabilidad necesaria para avanzar al siguiente estado sin ocultar lógica nueva dentro de un archivo ya terminado.

## Paso 3 - Escribir el bloque 3

### Escribe

```java
        for (int k = 2; k <= n; k++) {
            factor *= k;
        }
```

### Qué significa

En cada iteración, `factor *= k` multiplica el acumulador por el siguiente factor. El resultado conserva todo el trabajo previo.

### Por qué lo hacemos ahora

Este bloque añade únicamente la responsabilidad necesaria para avanzar al siguiente estado sin ocultar lógica nueva dentro de un archivo ya terminado.

## Paso 4 - Escribir el bloque 4

### Escribe

```java
        System.out.println("n: " + n);
        System.out.println("Factorial: " + factor);
    }
}
```

### Qué significa

Al terminar el for se imprimen n y el factorial, que para 10 debe ser 3628800.

### Por qué lo hacemos ahora

Este bloque añade únicamente la responsabilidad necesaria para avanzar al siguiente estado sin ocultar lógica nueva dentro de un archivo ya terminado.

## Archivo completo al terminar este ejemplo

```java
public class EJ09_ForFactorial {
    public static void main(String[] args) {
        calcularFactorial(10);
    }

    public static void calcularFactorial(int n) {
        int factor = 1;

        for (int k = 2; k <= n; k++) {
            factor *= k;
        }

        System.out.println("n: " + n);
        System.out.println("Factorial: " + factor);
    }
}
```

## Flujo mental

```text
factor=1 -> k=2 -> mientras k<=10 -> factor*=k -> k++ -> imprimir 3628800
```

## Traza manual antes de ejecutar

| k | factor antes | operación | factor después |
|---:|---:|---|---:|
|2|1|1*2|2|
|3|2|2*3|6|
|4|6|6*4|24|
|5|24|24*5|120|

## Antes de ejecutar: predicción

1. Responde: ¿Por qué el acumulador del factorial comienza en 1 y no en 0?
2. Escribe cuál será la primera línea visible en consola.
3. Indica qué condición o actualización provoca ese resultado.

## Ejecuta

Desde la carpeta `src`:

```bash
javac EJ09_ForFactorial.java
java EJ09_ForFactorial
```

## Resultado esperado

```text
n: 10
Factorial: 3628800
```

## Cómo interpretarlo

Porque 1 es el elemento neutro de la multiplicación; multiplicar por 1 conserva el producto. La salida no solo confirma que el archivo compila: evidencia el camino que siguió el flujo de ejecución. Relaciona siempre la salida con la condición, la actualización o la sentencia de control que la produjo.

## Variación A

Cambia n a 5 y predice 120 antes de ejecutar.

Vuelve a compilar y ejecutar después del cambio. No confíes en la ejecución anterior: el archivo fuente cambió y debe producir una nueva evidencia.

## Error controlado

Inicializa `factor` en 0. Todas las multiplicaciones posteriores conservarán el resultado en 0.

### Por qué ocurre

Para un producto acumulativo, el valor inicial correcto es 1; 0 anula cualquier multiplicación.

### Corrección razonada

Restaura el código del archivo completo del ejemplo y vuelve a ejecutar hasta recuperar la salida esperada. El objetivo no es memorizar la corrección, sino relacionar el cambio realizado con su efecto observable.

## Qué debes poder explicar con tus palabras

- ¿Por qué el acumulador del factorial comienza en 1 y no en 0?
- ¿Qué parte del programa controla el flujo?
- ¿Qué variable cambia o se consulta?
- ¿Qué evidencia en consola confirma tu explicación?

# T09 - Tarea espejo de EJ09

## Enunciado

Calcular 6! mediante for.

## Archivo a modificar

`src/T09_ForFactorial.java`

## Restricción

No escribir la multiplicación completa de forma manual.

## Punto de partida

Crea el archivo con esta estructura inicial. Debe compilar aun antes de completar el TODO:

```java
public class T09_ForFactorial {
    public static void main(String[] args) {
        int n = 6;
        int factor = 1;

        // T09 - TODO
        // Objetivo: calcular 6! con un bucle for.
        // Prediccion: 720.
        // Restriccion: no escribas la multiplicacion 1*2*3*4*5*6 directamente.
    }
}
```

## Pista

Usa un acumulador iniciado en 1 y recorre desde 2 hasta n.

## Evidencia que debes mostrar

Consola mostrando 720 y explicación de las seis etapas del producto.

## Cómo saber si está correcta

El resultado final debe ser 720. No compares solo texto: explica qué condición o actualización conduce al resultado.


# EJ10 - Modificar una repetición con continue y break

## Qué vamos a construir

Un for en el que `continue` omite una iteración concreta y `break` termina por completo la repetición.

## Qué aprenderás aquí

Distinguir entre saltar el resto de la iteración actual y abandonar definitivamente el bucle.

## Archivos que vamos a crear o modificar

- `src/EJ10_BreakContinue.java`
- Después resolverás `src/T10_BreakContinue.java` como T10.

## Punto de partida

Proyecto `S04_EstructurasControl` abierto, carpeta `src` disponible y los ejemplos anteriores cerrados o sin ejecutar. Cada archivo de esta guía es independiente y puede compilarse por separado.

## Paso 1 - Escribir el bloque 1

### Escribe

```java
public class EJ10_BreakContinue {
    public static void main(String[] args) {
        for (int numero = 1; numero <= 10; numero++) {
```

### Qué significa

El `for` genera una secuencia de números del 1 al 10. A partir de aquí se aplican dos decisiones que alteran el recorrido.

### Por qué lo hacemos ahora

Este bloque añade únicamente la responsabilidad necesaria para avanzar al siguiente estado sin ocultar lógica nueva dentro de un archivo ya terminado.

## Paso 2 - Escribir el bloque 2

### Escribe

```java
            if (numero == 3) {
                continue;
            }
```

### Qué significa

Cuando `numero == 3`, `continue` omite el resto de esa iteración. Por eso 3 no se imprime.

### Por qué lo hacemos ahora

Este bloque añade únicamente la responsabilidad necesaria para avanzar al siguiente estado sin ocultar lógica nueva dentro de un archivo ya terminado.

## Paso 3 - Escribir el bloque 3

### Escribe

```java
            if (numero == 8) {
                break;
            }
```

### Qué significa

Cuando `numero == 8`, `break` abandona el bucle completo. Por eso 8 y los valores posteriores no llegan a imprimirse.

### Por qué lo hacemos ahora

Este bloque añade únicamente la responsabilidad necesaria para avanzar al siguiente estado sin ocultar lógica nueva dentro de un archivo ya terminado.

## Paso 4 - Escribir el bloque 4

### Escribe

```java
            System.out.println(numero);
        }
    }
}
```

### Qué significa

La salida final permite distinguir físicamente 'saltar una vuelta' de 'terminar el ciclo'.

### Por qué lo hacemos ahora

Este bloque añade únicamente la responsabilidad necesaria para avanzar al siguiente estado sin ocultar lógica nueva dentro de un archivo ya terminado.

## Archivo completo al terminar este ejemplo

```java
public class EJ10_BreakContinue {
    public static void main(String[] args) {
        for (int numero = 1; numero <= 10; numero++) {
            if (numero == 3) {
                continue;
            }

            if (numero == 8) {
                break;
            }

            System.out.println(numero);
        }
    }
}
```

## Flujo mental

```text
numero 1..10 -> si 3: continue -> si 8: break -> imprimir solo valores que superan ambas decisiones
```

## Traza manual antes de ejecutar

| numero | condición continue | condición break | acción |
|---:|---|---|---|
|1|false|false|imprime 1|
|2|false|false|imprime 2|
|3|true|no se evalúa|salta a 4|
|4|false|false|imprime 4|
|8|false|true|termina bucle|

## Antes de ejecutar: predicción

1. Responde: Cuando numero vale 3, ¿se evalúa después el if que contiene break?
2. Escribe cuál será la primera línea visible en consola.
3. Indica qué condición o actualización provoca ese resultado.

## Ejecuta

Desde la carpeta `src`:

```bash
javac EJ10_BreakContinue.java
java EJ10_BreakContinue
```

## Resultado esperado

```text
1
2
4
5
6
7
```

## Cómo interpretarlo

No. `continue` transfiere el control a la siguiente iteración del for. La salida no solo confirma que el archivo compila: evidencia el camino que siguió el flujo de ejecución. Relaciona siempre la salida con la condición, la actualización o la sentencia de control que la produjo.

## Variación A

Mueve el `break` antes del `continue` y cambia ambos valores para observar cómo el orden de las condiciones afecta el comportamiento.

Vuelve a compilar y ejecutar después del cambio. No confíes en la ejecución anterior: el archivo fuente cambió y debe producir una nueva evidencia.

## Error controlado

Sustituye `continue` por `break` cuando numero==3. La salida terminará en 2 en lugar de continuar con 4,5,6,7.

### Por qué ocurre

`break` abandona todo el bucle; `continue` solo omite lo que queda de la iteración actual.

### Corrección razonada

Restaura el código del archivo completo del ejemplo y vuelve a ejecutar hasta recuperar la salida esperada. El objetivo no es memorizar la corrección, sino relacionar el cambio realizado con su efecto observable.

## Qué debes poder explicar con tus palabras

- Cuando numero vale 3, ¿se evalúa después el if que contiene break?
- ¿Qué parte del programa controla el flujo?
- ¿Qué variable cambia o se consulta?
- ¿Qué evidencia en consola confirma tu explicación?

# T10 - Tarea espejo de EJ10

## Enunciado

Recorrer 1..12, omitir múltiplos de 3 con continue y terminar cuando el número llegue a 10 con break.

## Archivo a modificar

`src/T10_BreakContinue.java`

## Restricción

Utilizar ambos controles; no resolverlo cambiando el límite del for a 9.

## Punto de partida

Crea el archivo con esta estructura inicial. Debe compilar aun antes de completar el TODO:

```java
public class T10_BreakContinue {
    public static void main(String[] args) {
        // T10 - TODO
        // Recorre los numeros del 1 al 12.
        // 1) Usa continue para no imprimir multiplos de 3.
        // 2) Usa break para terminar completamente cuando numero llegue a 10.
        // Predice la secuencia final antes de ejecutar.
    }
}
```

## Pista

Evalúa `numero == 10` para break y `numero % 3 == 0` para continue.

## Evidencia que debes mostrar

Predicción escrita y consola final: 1, 2, 4, 5, 7, 8.

## Cómo saber si está correcta

No debe aparecer 3, 6 ni 9; tampoco debe imprimirse 10 ni valores posteriores. No compares solo texto: explica qué condición o actualización conduce al resultado.



# 7. Cierre de sesión

Hoy construiste una secuencia completa de programas para controlar el flujo en Java. Empezaste con una condición `if` que puede ejecutar o no un bloque; después agregaste un camino alternativo con `if-else`, comparaste esa decisión con el operador ternario y seguiste decisiones anidadas. Con `switch` observaste cómo un único valor puede seleccionar distintos casos. Luego pasaste de decidir a repetir: analizaste cómo `while` valida antes de entrar, cómo un contador y un acumulador cumplen funciones distintas, cómo `do-while` valida al final y cómo `for` concentra el control de una repetición conocida.

También observaste que operadores pequeños como `++`, `--` o `+=` modifican el estado y deben leerse con precisión. Finalmente, `continue` y `break` mostraron dos formas diferentes de alterar una repetición: saltar una iteración o terminarla completamente.

Antes de continuar, repasa especialmente las trazas manuales. Si puedes anticipar la salida antes de ejecutar, estás comprendiendo el flujo. Si solo reconoces la respuesta después de verla en consola, todavía necesitas practicar la lectura paso a paso.

Puedes complementar la práctica con los recursos de **Lideratec Academy**:

- Blog: https://lideratecacademy.com/blog/
- YouTube: https://www.youtube.com/@LideratecAcademy

Si deseas validar tu implementación o trabajar con una versión completa del proyecto, puedes utilizar el laboratorio ejecutable de la FASE 15 como recurso opcional. No es necesario para completar esta guía.
