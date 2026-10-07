---
course_id: JAVA-POO
session_id: S06
source_origin: PPT
status: validated
---

# Guía del Estudiante - Sesión 06
## Clases nativas: clase Math y operaciones con números

**Lideratec Academy - Programación Orientada a Objetos**

## 1. Propósito de la sesión

En esta sesión aprenderás a utilizar la clase nativa `Math` de Java como una caja de herramientas para resolver operaciones numéricas frecuentes sin reprogramarlas desde cero. Trabajarás primero con sus campos `Math.PI` y `Math.E`; después utilizarás métodos de valor absoluto, redondeo, comparación, potencias, raíces, logaritmos, conversiones angulares y generación de números aleatorios. Finalmente integrarás esas operaciones en una clase utilitaria que trabaja con los dígitos de un número entero.

La evidencia principal será un conjunto de programas Java que podrás compilar y ejecutar. El recorrido termina en una implementación equivalente al ejercicio `ProAritmetica`: generar un número aleatorio en un rango, contar sus dígitos, obtener la lista de dígitos y establecer si el número es capicúa.

**Herramientas:** JDK 21 e IntelliJ IDEA o, como alternativa, terminal con `javac` y `java`.

## 2. Resultado observable

### A. Lectura sugerida del docente

Al finalizar esta práctica no buscamos que memorices una lista de métodos. El objetivo es que puedas reconocer qué operación necesita un problema y seleccionar el método apropiado de `Math`. Primero observarás que `Math` pertenece a `java.lang`, por lo que sus miembros pueden utilizarse directamente. Después compararás métodos que suelen confundirse, como `floor`, `ceil` y `round`. Más adelante usarás `Math.random()` para generar enteros dentro de un intervalo y `Math.log10()` para determinar cuántos dígitos tiene un entero positivo. La sesión culmina cuando esas piezas dejan de estar aisladas y forman una clase utilitaria completa. En cada ejemplo tendrás que predecir la salida, ejecutar, interpretar, modificar y comprobar. Esa secuencia es importante: escribir código que compila no basta; debes poder explicar por qué cada operación produce el resultado observado.

### B. Desempeños observables

Al finalizar podrás:

1. identificar los campos `Math.PI` y `Math.E`;
2. seleccionar métodos de `Math` de acuerdo con una operación numérica;
3. diferenciar `floor`, `ceil` y `round` a partir de su salida;
4. generar enteros dentro de un rango usando `Math.random()`;
5. contar dígitos mediante `Math.log10()` para el dominio trabajado;
6. extraer los dígitos de un entero mediante `%` y `/`;
7. reconstruir un número y verificar si es capicúa;
8. integrar los métodos anteriores en una clase utilitaria.

### C. Criterio de dominio

Demuestras dominio cuando puedes modificar valores y rangos sin perder la lógica, anticipar qué debería ocurrir antes de ejecutar, interpretar la salida y explicar por qué un método de `Math` es adecuado para cada operación. Copiar el programa final sin explicar el flujo no constituye evidencia suficiente.

## 3. Antes de iniciar

### Debe saber

- crear y ejecutar una clase Java con método `main`;
- declarar variables primitivas;
- usar métodos `static`;
- usar `if`, `for` y `while`;
- usar operadores aritméticos `%`, `/`, `+`, `-`, `*`;
- leer valores con `Scanner`;
- reconocer una lista `List<Integer>` a nivel de uso básico.

### Debe tener disponible

- JDK 21;
- IntelliJ IDEA o terminal;
- una carpeta de trabajo, por ejemplo `S06_ClaseMath`.

### No se asumirá todavía

No se requiere crear librerías propias, usar Maven/Gradle, diseñar una arquitectura por capas ni emplear APIs externas. La sesión se concentra en `java.lang.Math` y en la clase utilitaria numérica del material.

## 4. Herramientas y recursos

### JDK 21

Es el entorno que contiene el compilador `javac` y la máquina virtual `java`. En esta sesión lo necesitamos para compilar y ejecutar los ejemplos.

**Validación en terminal:**

```bash
java -version
javac -version
```

Debes observar una versión 21.x. Si IntelliJ ya ejecuta proyectos con JDK 21, no necesitas reinstalar nada.

### IntelliJ IDEA

Es el IDE recomendado para trabajar cómodamente con los archivos Java. Para esta sesión basta con crear un proyecto Java sin dependencias externas y usar JDK 21 como SDK del proyecto.

**Alternativa:** puedes guardar cada archivo `.java` en una carpeta y usar:

```bash
javac NombreArchivo.java
java NombreArchivo
```

### Nota técnica importante sobre `min`

En la tabla del material aparece el nombre `mix(double n1, double n2)` para “retornar el valor menor”. Para la ejecución del laboratorio usaremos **`Math.min(...)`**, que es el nombre válido en Java. Esta corrección es operativa: no cambia el concepto enseñado, que es obtener el menor de dos valores.

## 5. Preparación del entorno

### Ruta A - Ya tienes IntelliJ + JDK 21

1. Abre IntelliJ IDEA.
2. Crea un proyecto Java llamado `S06_ClaseMath`.
3. Selecciona JDK 21 como SDK.
4. Crea una carpeta `src` si el IDE no la crea automáticamente.
5. Crea una clase `PruebaMath` con un `main`.
6. Escribe:

```java
public class PruebaMath {
    public static void main(String[] args) {
        System.out.println(Math.PI);
    }
}
```

7. Ejecuta.
8. Si observas un valor cercano a `3.141592653589793`, el entorno está listo.

### Ruta B - Terminal

1. Crea una carpeta `S06_ClaseMath`.
2. Abre una terminal en esa carpeta.
3. Crea `PruebaMath.java` con el código anterior.
4. Ejecuta:

```bash
javac PruebaMath.java
java PruebaMath
```

5. Si ves el valor de `PI`, puedes continuar.

---
# EJ01 - Campos Math.PI y Math.E

## Qué vamos a construir / resolver

Crear un programa mínimo que lea los dos campos constantes de `Math` y calcule su diferencia. Este ejemplo introduce la idea de acceder a miembros `static` mediante el nombre de la clase.

## Qué aprenderás aquí

- acceder a `Math.PI` y `Math.E` sin crear un objeto `Math`
- interpretar que ambos son valores `double` constantes
- comprobar que `Math` está disponible desde `java.lang`

## Archivos, recursos o artefactos involucrados

- `EJ01_CamposMath.java`

## Punto de partida

Ya puedes crear una clase Java con `main`. Aún no necesitamos importar ninguna clase para usar `Math`.

## Paso 1 - Crear la clase y el punto de entrada

### Estado antes

No existe todavía el archivo del ejemplo.

### ¿Por qué necesitamos este paso?

Necesitamos una clase ejecutable para observar los campos de `Math` en tiempo de ejecución.

### Escribe ahora

```java
public class EJ01_CamposMath {
    public static void main(String[] args) {
    }
}
```

### Explicación detallada

`EJ01_CamposMath` identifica el ejemplo. `main` es el punto de entrada que ejecutará la JVM. Todavía no hay comportamiento numérico.

### Elementos nuevos

- `EJ01_CamposMath`: nombre de la clase del ejemplo.
- `main`: método desde el que inicia la ejecución.

### Estado después

El programa compila, pero no muestra información.

### Por qué podemos avanzar

Ya existe el lugar donde agregaremos las lecturas de los campos de `Math`.

## Paso 2 - Mostrar PI y E

### Estado antes

La clase existe pero no usa todavía `Math`.

### ¿Por qué necesitamos este paso?

Queremos observar directamente los dos campos definidos por la clase nativa.

### Escribe ahora

```java
System.out.println("Math.PI = " + Math.PI);
System.out.println("Math.E  = " + Math.E);
```

### Explicación detallada

`Math.PI` y `Math.E` se acceden con `NombreClase.miembro` porque son miembros estáticos. No se crea `new Math()`. La concatenación convierte el valor en parte del texto mostrado.

### Elementos nuevos

- `Math.PI`: relación entre circunferencia y diámetro.
- `Math.E`: base del logaritmo natural.

### Estado después

El programa mostrará ambos valores.

### Por qué podemos avanzar

Con los valores disponibles podemos realizar una operación ordinaria entre ellos.

## Paso 3 - Calcular una diferencia

### Estado antes

PI y E solo se muestran.

### ¿Por qué necesitamos este paso?

Una constante de `Math` puede participar en expresiones como cualquier otro `double`.

### Escribe ahora

```java
System.out.println("Diferencia PI - E = " + (Math.PI - Math.E));
```

### Explicación detallada

Los paréntesis fuerzan a evaluar primero la resta. El resultado sigue siendo `double`.

### Elementos nuevos

- Expresión `Math.PI - Math.E`: combina dos campos estáticos.

### Estado después

Además de mostrar las constantes, el programa muestra una operación que las utiliza.

### Por qué podemos avanzar

El ejemplo ya demuestra acceso, lectura y uso de los campos.

## Traza / simulación manual

PI es aproximadamente 3.14159 y E aproximadamente 2.71828; por lo tanto, la diferencia `PI - E` será positiva.

## Auditoría del artefacto construido

| Elemento | Qué hace | Por qué existe | Efecto |
|---|---|---|---|
| Crear la clase y el punto de entrada | `EJ01_CamposMath` identifica el ejemplo. `main` es el punto de entrada que ejecutará la JVM. Todavía no hay comportamiento numérico. | Necesitamos una clase ejecutable para observar los campos de `Math` en tiempo de ejecución. | El programa compila, pero no muestra información. |
| Mostrar PI y E | `Math.PI` y `Math.E` se acceden con `NombreClase.miembro` porque son miembros estáticos. No se crea `new Math()`. La concatenación convierte el valor en parte del texto mostrado. | Queremos observar directamente los dos campos definidos por la clase nativa. | El programa mostrará ambos valores. |
| Calcular una diferencia | Los paréntesis fuerzan a evaluar primero la resta. El resultado sigue siendo `double`. | Una constante de `Math` puede participar en expresiones como cualquier otro `double`. | Además de mostrar las constantes, el programa muestra una operación que las utiliza. |

## Archivo completo al terminar este ejemplo

```java
public class EJ01_CamposMath {
    public static void main(String[] args) {
        System.out.println("Math.PI = " + Math.PI);
        System.out.println("Math.E  = " + Math.E);
        System.out.println("Diferencia PI - E = " + (Math.PI - Math.E));
    }
}
```

## Antes de ejecutar: predicción

1. ¿Qué valor esperas que sea mayor: PI o E?
2. ¿La diferencia será positiva o negativa?

## Ejecuta / valida

En IntelliJ ejecuta el método `main`. En terminal:

```bash
javac EJ01_CamposMath.java
java EJ01_CamposMath
```

## Resultado esperado

Verás los valores de `Math.PI`, `Math.E` y una diferencia positiva cercana a `0.4233`.

## Cómo interpretarlo

El resultado confirma que los campos se utilizan directamente desde la clase. No hubo import explícito porque `Math` pertenece a `java.lang`.

## Variación A

Cambia la última expresión por `Math.E - Math.PI`. Predice primero el signo y luego verifica.

## Error o caso límite controlado

Intentar escribir `Math math = new Math();` no corresponde al uso de esta clase utilitaria.

## Por qué ocurre

Los métodos y campos que trabajamos son estáticos y se invocan mediante el nombre de la clase.

## Corrección razonada

Accede a ellos con `Math.PI`, `Math.E` o `Math.metodo(...)`.

## Qué debes poder explicar con tus palabras

- por qué no necesitas un objeto `Math`
- qué significa acceder a un miembro estático
- qué evidencia confirma que `Math` está disponible

## T01 - Tarea espejo

### Enunciado

Muestra `Math.PI`, `Math.E` y calcula la diferencia absoluta entre ambos valores. Antes de ejecutar, indica cuál constante esperas que sea mayor.

### Archivo a modificar

`T01_ConstantesMath.java`

### Restricción

La diferencia debe calcularse con `Math.abs(...)`; no escribas manualmente el valor de las constantes.

### Pista

La expresión interior puede ser `Math.PI - Math.E`.

### Evidencia que debes mostrar

Código y salida de consola con PI, E y la diferencia absoluta.

### Cómo saber si está correcta

La diferencia debe ser positiva y cercana a `0.4233`.

---

# EJ02 - Métodos básicos: abs, floor, ceil, round, max y min

## Qué vamos a construir / resolver

Comparar métodos que transforman o seleccionan valores numéricos para comprender qué problema resuelve cada uno.

## Qué aprenderás aquí

- usar `Math.abs`
- distinguir `floor`, `ceil` y `round`
- seleccionar mayor y menor con `max` y `min`

## Archivos, recursos o artefactos involucrados

- `EJ02_MetodosBasicos.java`

## Punto de partida

El ejemplo anterior confirmó que podemos llamar miembros estáticos de `Math`. Ahora aplicaremos métodos a valores concretos.

## Paso 1 - Declarar valores de prueba

### Estado antes

No tenemos entradas sobre las que comparar métodos.

### ¿Por qué necesitamos este paso?

Usaremos el mismo valor negativo para observar diferencias entre valor absoluto y redondeos.

### Escribe ahora

```java
double valor = -8.7;
double otro = 3.2;
```

### Explicación detallada

`valor` contiene un decimal negativo y `otro` un decimal positivo. Mantenerlos fijos permite atribuir cada cambio al método usado.

### Elementos nuevos

- `valor`: entrada principal.
- `otro`: segundo argumento para `max` y `min`.

### Estado después

Hay dos valores disponibles, pero todavía no se transforman.

### Por qué podemos avanzar

Ya podemos invocar métodos con entradas controladas.

## Paso 2 - Aplicar valor absoluto y redondeos

### Estado antes

`valor` conserva `-8.7`.

### ¿Por qué necesitamos este paso?

Queremos contrastar tres ideas diferentes: quitar signo, aproximar hacia abajo, aproximar hacia arriba y aproximar al entero más cercano.

### Escribe ahora

```java
System.out.println("abs: " + Math.abs(valor));
System.out.println("floor: " + Math.floor(valor));
System.out.println("ceil: " + Math.ceil(valor));
System.out.println("round: " + Math.round(valor));
```

### Explicación detallada

`abs` devuelve la magnitud positiva. `floor` busca el entero matemático menor o igual, por eso con negativos baja a `-9.0`. `ceil` busca el entero mayor o igual, por eso sube a `-8.0`. `round` elige el entero más cercano y retorna un tipo entero.

### Elementos nuevos

- `Math.abs(double)`
- `Math.floor(double)`
- `Math.ceil(double)`
- `Math.round(double)`

### Estado después

La consola permite comparar cuatro comportamientos sobre la misma entrada.

### Por qué podemos avanzar

Falta observar métodos que comparan dos argumentos.

## Paso 3 - Seleccionar mayor y menor

### Estado antes

Tenemos `valor=-8.7` y `otro=3.2`.

### ¿Por qué necesitamos este paso?

A veces el problema no pide transformar un número, sino elegir uno de dos.

### Escribe ahora

```java
System.out.println("max: " + Math.max(valor, otro));
System.out.println("min: " + Math.min(valor, otro));
```

### Explicación detallada

`max` retorna el mayor de los dos argumentos; `min` retorna el menor. En el material aparece `mix` en una tabla, pero para código ejecutable Java se utiliza `min`.

### Elementos nuevos

- `Math.max(a,b)`
- `Math.min(a,b)`

### Estado después

El ejemplo cubre transformación y comparación.

### Por qué podemos avanzar

Podemos ejecutar y verificar si cada salida coincide con la definición.

## Traza / simulación manual

Para `-8.7`: abs -> 8.7; floor -> -9.0; ceil -> -8.0; round -> -9. Entre -8.7 y 3.2, el máximo es 3.2 y el mínimo -8.7.

## Auditoría del artefacto construido

| Elemento | Qué hace | Por qué existe | Efecto |
|---|---|---|---|
| Declarar valores de prueba | `valor` contiene un decimal negativo y `otro` un decimal positivo. Mantenerlos fijos permite atribuir cada cambio al método usado. | Usaremos el mismo valor negativo para observar diferencias entre valor absoluto y redondeos. | Hay dos valores disponibles, pero todavía no se transforman. |
| Aplicar valor absoluto y redondeos | `abs` devuelve la magnitud positiva. `floor` busca el entero matemático menor o igual, por eso con negativos baja a `-9.0`. `ceil` busca el entero mayor o igual, por eso sube a `-8.0`. `round` elige el entero más cercano y retorna un tipo entero. | Queremos contrastar tres ideas diferentes: quitar signo, aproximar hacia abajo, aproximar hacia arriba y aproximar al entero más cercano. | La consola permite comparar cuatro comportamientos sobre la misma entrada. |
| Seleccionar mayor y menor | `max` retorna el mayor de los dos argumentos; `min` retorna el menor. En el material aparece `mix` en una tabla, pero para código ejecutable Java se utiliza `min`. | A veces el problema no pide transformar un número, sino elegir uno de dos. | El ejemplo cubre transformación y comparación. |

## Archivo completo al terminar este ejemplo

```java
public class EJ02_MetodosBasicos {
    public static void main(String[] args) {
        double valor = -8.7;
        double otro = 3.2;

        System.out.println("abs: " + Math.abs(valor));
        System.out.println("floor: " + Math.floor(valor));
        System.out.println("ceil: " + Math.ceil(valor));
        System.out.println("round: " + Math.round(valor));
        System.out.println("max: " + Math.max(valor, otro));
        System.out.println("min: " + Math.min(valor, otro));
    }
}
```

## Antes de ejecutar: predicción

1. Predice `floor(-8.7)` y `ceil(-8.7)` antes de ejecutar.
2. ¿`round(-8.7)` quedará más cerca de -8 o de -9?

## Ejecuta / valida

En IntelliJ ejecuta el método `main`. En terminal:

```bash
javac EJ02_MetodosBasicos.java
java EJ02_MetodosBasicos
```

## Resultado esperado

La salida debe mostrar `8.7`, `-9.0`, `-8.0`, `-9`, `3.2` y `-8.7` en el orden del programa.

## Cómo interpretarlo

La parte crítica es observar que `floor` y `ceil` se definen por orden matemático, no por 'quitar decimales'. En negativos, esa diferencia se vuelve evidente.

## Variación A

Cambia `valor` a `8.7` y vuelve a comparar `floor`, `ceil` y `round`.

## Error o caso límite controlado

Usar `Math.mix(valor, otro)` producirá error de compilación porque ese método no existe con ese nombre.

## Por qué ocurre

El nombre compilable para obtener el menor es `min`; la tabla fuente contiene una inconsistencia tipográfica.

## Corrección razonada

Usa `Math.min(valor, otro)` y conserva el concepto de seleccionar el menor.

## Qué debes poder explicar con tus palabras

- diferencia entre floor, ceil y round
- por qué `min` y `max` requieren dos argumentos
- qué corrección técnica se aplicó al nombre `mix`

## T02 - Tarea espejo

### Enunciado

Con `a=-12.4` y `b=6.8`, imprime `abs(a)`, `floor(a)`, `ceil(a)`, `round(a)`, `max(a,b)` y `min(a,b)`.

### Archivo a modificar

`T02_MetodosBasicos.java`

### Restricción

Debes invocar los seis métodos; no calcules las respuestas manualmente.

### Pista

Usa una línea `System.out.println` por resultado.

### Evidencia que debes mostrar

Código y salida ordenada con seis resultados.

### Cómo saber si está correcta

`abs` debe ser positivo; `max` debe devolver 6.8 y `min` -12.4.

---

# EJ03 - Potencias, raíz cúbica y exponencial

## Qué vamos a construir / resolver

Aplicar `pow`, `cbrt` y `exp` para reconocer cómo los parámetros cambian según la operación matemática.

## Qué aprenderás aquí

- usar base y exponente con `Math.pow`
- calcular una raíz cúbica con `Math.cbrt`
- observar `Math.exp(1)` como E elevado a 1

## Archivos, recursos o artefactos involucrados

- `EJ03_PotenciasRaices.java`

## Punto de partida

Ya sabes invocar métodos estáticos. Ahora el foco es entender cuántos argumentos recibe cada operación.

## Paso 1 - Preparar datos

### Estado antes

No existen todavía entradas.

### ¿Por qué necesitamos este paso?

Una potencia necesita base y exponente; la raíz cúbica necesita un número.

### Escribe ahora

```java
double base = 2;
double exponente = 5;
double cubo = 125;
```

### Explicación detallada

Usamos `double` porque los métodos de `Math` trabajan naturalmente con valores de punto flotante y retornan `double` en estas variantes.

### Elementos nuevos

- `base` y `exponente`: argumentos de `pow`.
- `cubo`: argumento de `cbrt`.

### Estado después

Tenemos entradas simples cuyo resultado puede anticiparse.

### Por qué podemos avanzar

Podemos aplicar cada función y comparar.

## Paso 2 - Calcular potencia y raíz cúbica

### Estado antes

Tenemos 2, 5 y 125 como datos.

### ¿Por qué necesitamos este paso?

Queremos comprobar dos operaciones con firmas distintas.

### Escribe ahora

```java
System.out.println("pow: " + Math.pow(base, exponente));
System.out.println("cbrt: " + Math.cbrt(cubo));
```

### Explicación detallada

`Math.pow(2,5)` representa 2 elevado a 5 y devuelve 32.0. `Math.cbrt(125)` devuelve la raíz cúbica, 5.0.

### Elementos nuevos

- `Math.pow(base, exponente)`
- `Math.cbrt(numero)`

### Estado después

La consola mostrará dos resultados predecibles.

### Por qué podemos avanzar

Falta conectar con el campo E mediante `exp`.

## Paso 3 - Observar exp

### Estado antes

Aún no usamos la función exponencial.

### ¿Por qué necesitamos este paso?

El material incluye `exp(n)`, que retorna E elevado a `n`. Usar 1 facilita validar el resultado contra `Math.E`.

### Escribe ahora

```java
System.out.println("exp(1): " + Math.exp(1));
```

### Explicación detallada

Con exponente 1, `Math.exp(1)` debe ser igual, dentro de la precisión `double`, al valor de `Math.E`.

### Elementos nuevos

- `Math.exp(n)`: E elevado a n.

### Estado después

El ejemplo reúne potencia general, raíz cúbica y exponencial.

### Por qué podemos avanzar

Ya podemos ejecutar y relacionar cada firma con su problema.

## Traza / simulación manual

2^5 = 32; raíz cúbica de 125 = 5; E^1 = E, aproximadamente 2.71828.

## Auditoría del artefacto construido

| Elemento | Qué hace | Por qué existe | Efecto |
|---|---|---|---|
| Preparar datos | Usamos `double` porque los métodos de `Math` trabajan naturalmente con valores de punto flotante y retornan `double` en estas variantes. | Una potencia necesita base y exponente; la raíz cúbica necesita un número. | Tenemos entradas simples cuyo resultado puede anticiparse. |
| Calcular potencia y raíz cúbica | `Math.pow(2,5)` representa 2 elevado a 5 y devuelve 32.0. `Math.cbrt(125)` devuelve la raíz cúbica, 5.0. | Queremos comprobar dos operaciones con firmas distintas. | La consola mostrará dos resultados predecibles. |
| Observar exp | Con exponente 1, `Math.exp(1)` debe ser igual, dentro de la precisión `double`, al valor de `Math.E`. | El material incluye `exp(n)`, que retorna E elevado a `n`. Usar 1 facilita validar el resultado contra `Math.E`. | El ejemplo reúne potencia general, raíz cúbica y exponencial. |

## Archivo completo al terminar este ejemplo

```java
public class EJ03_PotenciasRaices {
    public static void main(String[] args) {
        double base = 2;
        double exponente = 5;
        double cubo = 125;

        System.out.println("pow: " + Math.pow(base, exponente));
        System.out.println("cbrt: " + Math.cbrt(cubo));
        System.out.println("exp(1): " + Math.exp(1));
    }
}
```

## Antes de ejecutar: predicción

1. ¿Qué debe devolver `Math.pow(2,5)`?
2. ¿`Math.exp(1)` debería coincidir aproximadamente con qué campo de `Math`?

## Ejecuta / valida

En IntelliJ ejecuta el método `main`. En terminal:

```bash
javac EJ03_PotenciasRaices.java
java EJ03_PotenciasRaices
```

## Resultado esperado

`pow: 32.0`, `cbrt: 5.0` y `exp(1)` cercano a `2.718281828...`.

## Cómo interpretarlo

La firma del método refleja la operación: `pow` requiere dos argumentos; `cbrt` y `exp`, uno.

## Variación A

Cambia `base` a 10 y `exponente` a 3. Predice el resultado antes de ejecutar.

## Error o caso límite controlado

Intercambiar accidentalmente base y exponente cambia completamente el resultado de `pow`.

## Por qué ocurre

`pow(a,b)` interpreta el primer argumento como base y el segundo como exponente.

## Corrección razonada

Nombra variables con intención (`base`, `exponente`) y comprueba con un caso mental simple.

## Qué debes poder explicar con tus palabras

- firma conceptual de `pow`
- diferencia entre `pow` y `cbrt`
- relación entre `exp(1)` y `Math.E`

## T03 - Tarea espejo

### Enunciado

Con base 3, exponente 4 y número 216, calcula la potencia y la raíz cúbica.

### Archivo a modificar

`T03_PotenciasRaices.java`

### Restricción

Usa `Math.pow` y `Math.cbrt`; no escribas 81 ni 6 como constantes de resultado.

### Pista

`Math.pow(base, exponente)` y `Math.cbrt(numero)`.

### Evidencia que debes mostrar

Salida con potencia y raíz cúbica.

### Cómo saber si está correcta

La potencia debe ser 81.0 y la raíz cúbica 6.0.

---

# EJ04 - Logaritmos y conversiones angulares

## Qué vamos a construir / resolver

Usar `log`, `log10`, `toRadians` y `toDegrees` y reconocer que dos logaritmos con el mismo número pueden producir valores diferentes porque tienen bases distintas.

## Qué aprenderás aquí

- diferenciar logaritmo natural y decimal
- convertir grados a radianes
- convertir radianes a grados

## Archivos, recursos o artefactos involucrados

- `EJ04_LogaritmosAngulos.java`

## Punto de partida

El material presenta métodos de logaritmos y conversiones. Usaremos valores fáciles de validar: 1000 y 180 grados.

## Paso 1 - Definir número y ángulo

### Estado antes

No hay entradas.

### ¿Por qué necesitamos este paso?

Necesitamos un número positivo para los logaritmos y un ángulo en grados para la conversión.

### Escribe ahora

```java
double numero = 1000;
double grados = 180;
```

### Explicación detallada

1000 es útil porque su logaritmo base 10 es 3. 180 grados es útil porque equivale a PI radianes.

### Elementos nuevos

- `numero`: entrada de logaritmos.
- `grados`: entrada para conversión angular.

### Estado después

Las entradas permiten predicciones claras.

### Por qué podemos avanzar

Podemos calcular los dos tipos de logaritmos.

## Paso 2 - Comparar log y log10

### Estado antes

`numero` vale 1000.

### ¿Por qué necesitamos este paso?

El material incluye ambos métodos; compararlos evita asumir que “log” siempre significa base 10.

### Escribe ahora

```java
System.out.println("log10(1000): " + Math.log10(numero));
System.out.println("log(1000): " + Math.log(numero));
```

### Explicación detallada

`Math.log10` utiliza base 10. `Math.log` utiliza base E, es decir, logaritmo natural. Por eso las salidas son diferentes.

### Elementos nuevos

- `Math.log10`
- `Math.log`

### Estado después

Queda visible la diferencia de base.

### Por qué podemos avanzar

Ahora convertiremos unidades angulares.

## Paso 3 - Convertir grados y radianes

### Estado antes

Tenemos 180 grados.

### ¿Por qué necesitamos este paso?

Los métodos permiten convertir sin escribir manualmente factores de PI.

### Escribe ahora

```java
double radianes = Math.toRadians(grados);
System.out.println("180 grados en radianes: " + radianes);
System.out.println("PI radianes en grados: " + Math.toDegrees(Math.PI));
```

### Explicación detallada

`toRadians` recibe grados y retorna radianes. `toDegrees` realiza la operación inversa. Usar `Math.PI` permite comprobar que PI radianes equivalen a 180 grados.

### Elementos nuevos

- `Math.toRadians`
- `Math.toDegrees`

### Estado después

El ejemplo muestra conversión en ambas direcciones.

### Por qué podemos avanzar

Ya podemos ejecutar y comparar con referencias conocidas.

## Traza / simulación manual

`log10(1000)` debe ser 3. `toRadians(180)` debe acercarse a PI y `toDegrees(PI)` a 180.

## Auditoría del artefacto construido

| Elemento | Qué hace | Por qué existe | Efecto |
|---|---|---|---|
| Definir número y ángulo | 1000 es útil porque su logaritmo base 10 es 3. 180 grados es útil porque equivale a PI radianes. | Necesitamos un número positivo para los logaritmos y un ángulo en grados para la conversión. | Las entradas permiten predicciones claras. |
| Comparar log y log10 | `Math.log10` utiliza base 10. `Math.log` utiliza base E, es decir, logaritmo natural. Por eso las salidas son diferentes. | El material incluye ambos métodos; compararlos evita asumir que “log” siempre significa base 10. | Queda visible la diferencia de base. |
| Convertir grados y radianes | `toRadians` recibe grados y retorna radianes. `toDegrees` realiza la operación inversa. Usar `Math.PI` permite comprobar que PI radianes equivalen a 180 grados. | Los métodos permiten convertir sin escribir manualmente factores de PI. | El ejemplo muestra conversión en ambas direcciones. |

## Archivo completo al terminar este ejemplo

```java
public class EJ04_LogaritmosAngulos {
    public static void main(String[] args) {
        double numero = 1000;
        double grados = 180;
        double radianes = Math.toRadians(grados);

        System.out.println("log10(1000): " + Math.log10(numero));
        System.out.println("log(1000): " + Math.log(numero));
        System.out.println("180 grados en radianes: " + radianes);
        System.out.println("PI radianes en grados: " + Math.toDegrees(Math.PI));
    }
}
```

## Antes de ejecutar: predicción

1. ¿Por qué `log10(1000)` es fácil de anticipar?
2. ¿Qué valor aproximado esperas para 180 grados en radianes?

## Ejecuta / valida

En IntelliJ ejecuta el método `main`. En terminal:

```bash
javac EJ04_LogaritmosAngulos.java
java EJ04_LogaritmosAngulos
```

## Resultado esperado

`log10(1000): 3.0`; `log(1000)` cercano a 6.9077; 180 grados en radianes cercano a 3.14159; PI radianes en grados 180.0.

## Cómo interpretarlo

Los resultados confirman que la base del logaritmo forma parte de la definición del método y que las conversiones conservan el mismo ángulo expresado en otra unidad.

## Variación A

Cambia `grados` a 90 y comprueba que los radianes se aproximan a PI/2.

## Error o caso límite controlado

Llamar `Math.log` esperando base 10 produce un resultado numérico válido pero conceptualmente incorrecto para ese objetivo.

## Por qué ocurre

`Math.log` y `Math.log10` calculan funciones distintas.

## Corrección razonada

Selecciona el método según la base requerida y valida con un número de referencia.

## Qué debes poder explicar con tus palabras

- base usada por log y log10
- dirección de toRadians y toDegrees
- cómo validar con 180 grados y PI

## T04 - Tarea espejo

### Enunciado

Con `numero=100` y `grados=90`, calcula `log10`, `log` y la conversión a radianes.

### Archivo a modificar

`T04_LogaritmosAngulos.java`

### Restricción

Usa los métodos de `Math`; no escribas los resultados como constantes.

### Pista

Comprueba mentalmente que `log10(100)` debe ser 2.

### Evidencia que debes mostrar

Tres valores calculados y mostrados por consola.

### Cómo saber si está correcta

`log10` debe ser 2.0 y los radianes cercanos a 1.5708.

---

# EJ05 - Generar un entero aleatorio dentro de un rango

## Qué vamos a construir / resolver

Construir el método `numeroAleatorio(int min, int max)` presentado en el material y verificar que el valor generado siempre queda dentro del intervalo inclusivo.

## Qué aprenderás aquí

- interpretar la salida `[0,1)` de `Math.random()`
- escalar y desplazar el intervalo
- convertir el resultado a `int`
- validar el rango

## Archivos, recursos o artefactos involucrados

- `EJ05_NumeroAleatorio.java`

## Punto de partida

Hasta aquí has usado métodos con resultados deterministas. `Math.random()` introduce un valor que cambia entre ejecuciones.

## Paso 1 - Crear la firma del método

### Estado antes

El programa aún no encapsula la generación aleatoria.

### ¿Por qué necesitamos este paso?

Queremos reutilizar la lógica con cualquier límite inferior y superior.

### Escribe ahora

```java
public static int numeroAleatorio(int min, int max) {
    return 0;
}
```

### Explicación detallada

`min` y `max` representan los límites. El método retorna `int` porque el objetivo es producir un entero. El `0` es solo un estado temporal mientras construimos la fórmula.

### Elementos nuevos

- `min`: límite inferior.
- `max`: límite superior.
- retorno `int`: tipo del número generado.

### Estado después

Existe la estructura del método, pero su comportamiento aún es incorrecto.

### Por qué podemos avanzar

Ahora construiremos la transformación de intervalo.

## Paso 2 - Construir la fórmula

### Estado antes

`Math.random()` produciría un double desde 0 inclusive hasta 1 exclusivo.

### ¿Por qué necesitamos este paso?

Necesitamos transformar ese intervalo en `[min,max]` entero.

### Escribe ahora

```java
int aleatorio = (int) (Math.random() * (max - min + 1) + min);
return aleatorio;
```

### Explicación detallada

`max-min+1` es la cantidad de enteros posibles. Multiplicar escala el ancho. Sumar `min` desplaza el inicio. El cast a `int` elimina la parte decimal después del escalamiento.

### Elementos nuevos

- `Math.random()`
- `max - min + 1` como amplitud entera
- cast `(int)`

### Estado después

El método ya retorna un entero dentro del rango esperado cuando `min <= max`.

### Por qué podemos avanzar

Falta comprobarlo con una ejecución observable.

## Paso 3 - Agregar prueba y validación

### Estado antes

El método existe, pero no hay punto de entrada que lo use.

### ¿Por qué necesitamos este paso?

Un número aleatorio cambia; por eso además de mostrarlo conviene comprobar la condición de rango.

### Escribe ahora

```java
int min = 10;
int max = 20;
int numero = numeroAleatorio(min, max);
System.out.println("Aleatorio entre " + min + " y " + max + ": " + numero);
System.out.println("En rango: " + (numero >= min && numero <= max));
```

### Explicación detallada

La segunda línea de salida no depende del valor exacto generado: debe mostrar `true` si la fórmula respeta el intervalo.

### Elementos nuevos

- Validación booleana `numero >= min && numero <= max`.

### Estado después

Cada ejecución muestra un número y confirma si pertenece al rango.

### Por qué podemos avanzar

El comportamiento ya puede validarse aunque el número cambie.

## Traza / simulación manual

Si `min=10` y `max=20`, hay 11 enteros posibles. `Math.random()` nunca llega a 1, por lo que después de escalar y truncar el máximo índice posible es 10; al sumar 10 se llega como máximo a 20.

## Auditoría del artefacto construido

| Elemento | Qué hace | Por qué existe | Efecto |
|---|---|---|---|
| Crear la firma del método | `min` y `max` representan los límites. El método retorna `int` porque el objetivo es producir un entero. El `0` es solo un estado temporal mientras construimos la fórmula. | Queremos reutilizar la lógica con cualquier límite inferior y superior. | Existe la estructura del método, pero su comportamiento aún es incorrecto. |
| Construir la fórmula | `max-min+1` es la cantidad de enteros posibles. Multiplicar escala el ancho. Sumar `min` desplaza el inicio. El cast a `int` elimina la parte decimal después del escalamiento. | Necesitamos transformar ese intervalo en `[min,max]` entero. | El método ya retorna un entero dentro del rango esperado cuando `min <= max`. |
| Agregar prueba y validación | La segunda línea de salida no depende del valor exacto generado: debe mostrar `true` si la fórmula respeta el intervalo. | Un número aleatorio cambia; por eso además de mostrarlo conviene comprobar la condición de rango. | Cada ejecución muestra un número y confirma si pertenece al rango. |

## Archivo completo al terminar este ejemplo

```java
public class EJ05_NumeroAleatorio {
    public static int numeroAleatorio(int min, int max) {
        int aleatorio = (int) (Math.random() * (max - min + 1) + min);
        return aleatorio;
    }

    public static void main(String[] args) {
        int min = 10;
        int max = 20;
        int numero = numeroAleatorio(min, max);

        System.out.println("Aleatorio entre " + min + " y " + max + ": " + numero);
        System.out.println("En rango: " + (numero >= min && numero <= max));
    }
}
```

## Antes de ejecutar: predicción

1. ¿El número exacto puede predecirse?
2. ¿Qué condición sí debe cumplirse siempre?

## Ejecuta / valida

En IntelliJ ejecuta el método `main`. En terminal:

```bash
javac EJ05_NumeroAleatorio.java
java EJ05_NumeroAleatorio
```

## Resultado esperado

El número cambia entre ejecuciones, pero la línea `En rango:` debe mostrar siempre `true`.

## Cómo interpretarlo

En funciones aleatorias validamos propiedades invariantes -en este caso pertenencia al intervalo- en lugar de esperar un único valor exacto.

## Variación A

Ejecuta cinco veces y registra los resultados. Todos deben permanecer entre 10 y 20 inclusive.

## Error o caso límite controlado

Usar `min > max` rompe la interpretación del intervalo y la fórmula deja de representar el problema esperado.

## Por qué ocurre

La fórmula presupone que el límite inferior no supera al superior.

## Corrección razonada

Para esta sesión usa rangos válidos con `min <= max`. En una versión robusta futura podrías validar la entrada antes de generar.

## Qué debes poder explicar con tus palabras

- qué devuelve Math.random
- por qué aparece +1
- por qué se suma min
- qué propiedad se valida

## T05 - Tarea espejo

### Enunciado

Implementa `numeroAleatorio(25,30)` y comprueba con una expresión booleana que el resultado pertenece al rango.

### Archivo a modificar

`T05_NumeroAleatorio.java`

### Restricción

Usa la fórmula basada en `Math.random()` del ejemplo; no uses otras APIs de aleatoriedad.

### Pista

Reutiliza `(int)(Math.random() * (max-min+1) + min)`.

### Evidencia que debes mostrar

Número generado y `En rango = true`.

### Cómo saber si está correcta

Tras varias ejecuciones nunca debe aparecer un valor menor que 25 ni mayor que 30.

---

# EJ06 - Contar dígitos con Math.log10

## Qué vamos a construir / resolver

Construir `cuentaDigitos(int num)` para el dominio de enteros distintos de cero y comprender por qué `log10` permite obtener la cantidad de dígitos.

## Qué aprenderás aquí

- combinar `Math.abs` y `Math.log10`
- convertir el resultado a entero
- identificar el caso límite de cero

## Archivos, recursos o artefactos involucrados

- `EJ06_CuentaDigitos.java`

## Punto de partida

El material propone la expresión `(int) Math.log10(Math.abs(num)) + 1`. Primero la estudiaremos en un entero positivo como 2091.

## Paso 1 - Crear la firma

### Estado antes

No existe un método para contar dígitos.

### ¿Por qué necesitamos este paso?

Queremos aislar la operación y recibir cualquier entero como argumento.

### Escribe ahora

```java
public static int cuentaDigitos(int num) {
    return 0;
}
```

### Explicación detallada

El parámetro `num` representa el entero analizado y el retorno `int` representa una cantidad.

### Elementos nuevos

- `num`: número a analizar.
- retorno `int`: cantidad de dígitos.

### Estado después

Existe un método incompleto.

### Por qué podemos avanzar

Podemos introducir la fórmula del material.

## Paso 2 - Aplicar abs, log10 y +1

### Estado antes

El método retorna 0 sin analizar el número.

### ¿Por qué necesitamos este paso?

Para números positivos, el piso implícito al convertir `log10` a `int`, más 1, coincide con el número de posiciones decimales. `abs` evita que el signo negativo invalide el logaritmo.

### Escribe ahora

```java
int canDigitos = (int) Math.log10(Math.abs(num)) + 1;
return canDigitos;
```

### Explicación detallada

`Math.abs(num)` toma la magnitud. `Math.log10` ubica el orden de magnitud decimal. El cast `(int)` descarta la fracción positiva y `+1` convierte el exponente en cantidad de dígitos.

### Elementos nuevos

- `canDigitos`: resultado calculado.
- Composición `abs -> log10 -> cast -> +1`.

### Estado después

El método funciona para enteros distintos de cero dentro del dominio habitual del ejercicio.

### Por qué podemos avanzar

Ahora comprobaremos con 2091.

## Paso 3 - Ejecutar con 2091

### Estado antes

El método está construido.

### ¿Por qué necesitamos este paso?

2091 tiene cuatro dígitos y permite validar la fórmula sin ambigüedad.

### Escribe ahora

```java
int numero = 2091;
System.out.println("El numero " + numero + " tiene " + cuentaDigitos(numero) + " digitos");
```

### Explicación detallada

`log10(2091)` está entre 3 y 4; el cast produce 3 y al sumar 1 obtenemos 4.

### Elementos nuevos

- Prueba concreta del método.

### Estado después

La salida debe indicar 4 dígitos.

### Por qué podemos avanzar

Podemos estudiar ahora un caso límite importante.

## Traza / simulación manual

Para 2091: `log10(2091)` es aproximadamente 3.32; `(int)` lo convierte en 3; `+1` produce 4.

## Auditoría del artefacto construido

| Elemento | Qué hace | Por qué existe | Efecto |
|---|---|---|---|
| Crear la firma | El parámetro `num` representa el entero analizado y el retorno `int` representa una cantidad. | Queremos aislar la operación y recibir cualquier entero como argumento. | Existe un método incompleto. |
| Aplicar abs, log10 y +1 | `Math.abs(num)` toma la magnitud. `Math.log10` ubica el orden de magnitud decimal. El cast `(int)` descarta la fracción positiva y `+1` convierte el exponente en cantidad de dígitos. | Para números positivos, el piso implícito al convertir `log10` a `int`, más 1, coincide con el número de posiciones decimales. `abs` evita que el signo negativo invalide el logaritmo. | El método funciona para enteros distintos de cero dentro del dominio habitual del ejercicio. |
| Ejecutar con 2091 | `log10(2091)` está entre 3 y 4; el cast produce 3 y al sumar 1 obtenemos 4. | 2091 tiene cuatro dígitos y permite validar la fórmula sin ambigüedad. | La salida debe indicar 4 dígitos. |

## Archivo completo al terminar este ejemplo

```java
public class EJ06_CuentaDigitos {
    public static int cuentaDigitos(int num) {
        int canDigitos = (int) Math.log10(Math.abs(num)) + 1;
        return canDigitos;
    }

    public static void main(String[] args) {
        int numero = 2091;
        System.out.println("El numero " + numero + " tiene " + cuentaDigitos(numero) + " digitos");
    }
}
```

## Antes de ejecutar: predicción

1. ¿Entre qué dos enteros estará `log10(2091)`?
2. ¿Qué cantidad de dígitos esperas?

## Ejecuta / valida

En IntelliJ ejecuta el método `main`. En terminal:

```bash
javac EJ06_CuentaDigitos.java
java EJ06_CuentaDigitos
```

## Resultado esperado

`El numero 2091 tiene 4 digitos`.

## Cómo interpretarlo

La expresión no 'cuenta' caracteres: deduce la cantidad mediante el orden de magnitud decimal.

## Variación A

Prueba con `-2091`. Gracias a `Math.abs`, debe seguir devolviendo 4.

## Error o caso límite controlado

Con `num=0`, `Math.log10(0)` no representa un logaritmo finito y la fórmula del material no produce el resultado conceptual esperado de 1 dígito.

## Por qué ocurre

Cero es un caso límite porque el logaritmo decimal no está definido como un número real finito en 0.

## Corrección razonada

En la tarea espejo agregarás `if (num == 0) return 1;` antes de aplicar la fórmula. Esa ampliación controla un caso límite sin cambiar la técnica principal.

## Qué debes poder explicar con tus palabras

- por qué se usa abs
- por qué se suma 1
- qué ocurre con 0
- cómo controlar el caso límite

## T06 - Tarea espejo

### Enunciado

Implementa `cuentaDigitos` para `987654` y añade el caso límite `0`, que debe devolver 1.

### Archivo a modificar

`T06_CuentaDigitos.java`

### Restricción

Para números distintos de cero conserva la fórmula con `Math.log10(Math.abs(num)) + 1`.

### Pista

Evalúa primero `if (num == 0)`.

### Evidencia que debes mostrar

Salida para 987654 y para 0.

### Cómo saber si está correcta

Debe mostrar 6 dígitos para 987654 y 1 para 0.

---

# EJ07 - Obtener la lista de dígitos de un número

## Qué vamos a construir / resolver

Construir `digitosNumero(int num)` usando división entera y residuo, y corregir el orden con `Collections.reverse`.

## Qué aprenderás aquí

- extraer el último dígito con `% 10`
- reducir el número con `/=10`
- trazar un ciclo `while`
- invertir la lista resultante

## Archivos, recursos o artefactos involucrados

- `EJ07_DigitosNumero.java`

## Punto de partida

El material usa `List<Integer>`, `ArrayList` y `Collections.reverse`. Aquí sí necesitamos imports porque esas clases pertenecen a `java.util`, no a `java.lang`.

## Paso 1 - Agregar imports y estructura

### Estado antes

La clase aún no conoce los tipos de colección.

### ¿Por qué necesitamos este paso?

El resultado debe ser una lista ordenada de dígitos y necesitaremos una lista dinámica más la operación `reverse`.

### Escribe ahora

```java
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;
```

### Explicación detallada

`List` define el tipo de referencia; `ArrayList` crea la implementación concreta; `Collections.reverse` invierte el orden de una lista existente.

### Elementos nuevos

- `List<Integer>`
- `ArrayList`
- `Collections`

### Estado después

El compilador puede resolver los tipos utilizados en el método.

### Por qué podemos avanzar

Podemos crear la lista y conservar una copia temporal del número.

## Paso 2 - Crear lista y temporal

### Estado antes

Tenemos imports, pero ningún estado para el proceso.

### ¿Por qué necesitamos este paso?

Necesitamos una colección donde guardar dígitos y una variable que podamos reducir sin perder el argumento original.

### Escribe ahora

```java
List<Integer> digitos = new ArrayList<>();
int temporal = num;
```

### Explicación detallada

`digitos` empieza vacía. `temporal` recibe el valor de `num` y será modificado en cada iteración.

### Elementos nuevos

- `digitos`: lista acumuladora.
- `temporal`: copia de trabajo.

### Estado después

El estado inicial está preparado para el ciclo.

### Por qué podemos avanzar

Ya podemos extraer un dígito por iteración.

## Paso 3 - Recorrer con while

### Estado antes

`temporal` contiene el número completo y `digitos` está vacía.

### ¿Por qué necesitamos este paso?

Cada iteración debe separar el último dígito y reducir el número restante.

### Escribe ahora

```java
while (temporal > 0) {
    digitos.add(temporal % 10);
    temporal /= 10;
}
```

### Explicación detallada

`temporal % 10` obtiene el último dígito. `digitos.add` lo almacena. `temporal /= 10` elimina ese último dígito mediante división entera. El ciclo termina cuando no queda ningún dígito por procesar.

### Elementos nuevos

- Condición `temporal > 0`.
- Residuo `% 10`.
- Actualización `temporal /= 10`.

### Estado después

La lista contiene los dígitos, pero en orden inverso de extracción.

### Por qué podemos avanzar

Debemos restaurar el orden original.

## Paso 4 - Invertir y retornar

### Estado antes

Para 2091 la lista temporal sería `[1,9,0,2]`.

### ¿Por qué necesitamos este paso?

El objetivo del material es retornar los dígitos en el mismo orden en que aparecen en el número.

### Escribe ahora

```java
Collections.reverse(digitos);
return digitos;
```

### Explicación detallada

`reverse` modifica la lista actual y la deja como `[2,0,9,1]`. Luego el método retorna la misma lista.

### Elementos nuevos

- Mutación de orden con `Collections.reverse`.

### Estado después

La lista final coincide con la escritura decimal del número.

### Por qué podemos avanzar

Podemos ejecutar y comparar con una traza manual.

## Traza / simulación manual

Para 2091, sigue el cambio de estado en cada iteración:

```text
Iteración 1: temporal=2091 -> dígito=1 -> lista=[1]          -> temporal=209
Iteración 2: temporal=209  -> dígito=9 -> lista=[1, 9]       -> temporal=20
Iteración 3: temporal=20   -> dígito=0 -> lista=[1, 9, 0]    -> temporal=2
Iteración 4: temporal=2    -> dígito=2 -> lista=[1, 9, 0, 2] -> temporal=0
```

Al terminar el ciclo, `temporal` vale `0`, por lo que la condición `temporal > 0` deja de cumplirse. La lista todavía está en el orden de extracción, `[1, 9, 0, 2]`. Después de `Collections.reverse(digitos)` queda `[2, 0, 9, 1]`, que coincide con el orden visual del número original.

## Auditoría del artefacto construido

| Elemento | Qué hace | Por qué existe | Efecto |
|---|---|---|---|
| Agregar imports y estructura | `List` define el tipo de referencia; `ArrayList` crea la implementación concreta; `Collections.reverse` invierte el orden de una lista existente. | El resultado debe ser una lista ordenada de dígitos y necesitaremos una lista dinámica más la operación `reverse`. | El compilador puede resolver los tipos utilizados en el método. |
| Crear lista y temporal | `digitos` empieza vacía. `temporal` recibe el valor de `num` y será modificado en cada iteración. | Necesitamos una colección donde guardar dígitos y una variable que podamos reducir sin perder el argumento original. | El estado inicial está preparado para el ciclo. |
| Recorrer con while | `temporal % 10` obtiene el último dígito. `digitos.add` lo almacena. `temporal /= 10` elimina ese último dígito mediante división entera. El ciclo termina cuando no queda ningún dígito por procesar. | Cada iteración debe separar el último dígito y reducir el número restante. | La lista contiene los dígitos, pero en orden inverso de extracción. |
| Invertir y retornar | `reverse` modifica la lista actual y la deja como `[2,0,9,1]`. Luego el método retorna la misma lista. | El objetivo del material es retornar los dígitos en el mismo orden en que aparecen en el número. | La lista final coincide con la escritura decimal del número. |

## Archivo completo al terminar este ejemplo

```java
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;

public class EJ07_DigitosNumero {
    public static List<Integer> digitosNumero(int num) {
        List<Integer> digitos = new ArrayList<>();
        int temporal = num;

        while (temporal > 0) {
            digitos.add(temporal % 10);
            temporal /= 10;
        }

        Collections.reverse(digitos);
        return digitos;
    }

    public static void main(String[] args) {
        int numero = 2091;
        System.out.println("Digitos de " + numero + ": " + digitosNumero(numero));
    }
}
```

## Antes de ejecutar: predicción

1. ¿Qué dígito se extrae primero de 2091?
2. ¿Por qué necesitaremos invertir la lista al final?

## Ejecuta / valida

En IntelliJ ejecuta el método `main`. En terminal:

```bash
javac EJ07_DigitosNumero.java
java EJ07_DigitosNumero
```

## Resultado esperado

`Digitos de 2091: [2, 0, 9, 1]`.

## Cómo interpretarlo

El ciclo procesa de derecha a izquierda; `reverse` transforma esa secuencia en el orden natural de lectura.

## Variación A

Cambia el número a 53081 y realiza primero dos iteraciones manuales antes de ejecutar.

## Error o caso límite controlado

Con `num=0`, la condición `temporal > 0` no entra al ciclo y la lista queda vacía. En el ejercicio original el número proviene de un rango positivo, por eso ese caso no aparece en el flujo principal.

## Por qué ocurre

El algoritmo está diseñado para enteros positivos en el contexto del ejercicio fuente.

## Corrección razonada

Mantén entradas positivas en el ejemplo principal. Si la especificación futura exigiera 0, habría que definir explícitamente si debe retornar `[0]`.

## Qué debes poder explicar con tus palabras

- función de temporal
- por qué %10 extrae el último dígito
- por qué /=10 reduce el número
- por qué se usa reverse

## T07 - Tarea espejo

### Enunciado

Completa `digitosNumero` y prueba con 53081.

### Archivo a modificar

`T07_DigitosNumero.java`

### Restricción

Debes usar el patrón `%10`, `/=10` y `Collections.reverse`; no conviertas el número a String.

### Pista

La lista se llena en orden inverso y se corrige al final.

### Evidencia que debes mostrar

Salida `[5, 3, 0, 8, 1]`.

### Cómo saber si está correcta

La lista debe conservar el cero intermedio y el orden original.

---

# EJ08 - Determinar si un número es capicúa

## Qué vamos a construir / resolver

Reconstruir un número invertido a partir de sus dígitos y compararlo con el original, siguiendo la lógica del material.

## Qué aprenderás aquí

- extraer dígitos
- usar un ciclo `for` con posiciones
- aplicar `Math.pow` para valor posicional
- retornar una condición booleana

## Archivos, recursos o artefactos involucrados

- `EJ08_EsCapicua.java`

## Punto de partida

Ya dominaste la extracción de dígitos. Ahora reutilizaremos ese patrón y añadiremos reconstrucción posicional para comparar el número original con su inverso.

## Paso 1 - Preparar lista, temporal y acumulador

### Estado antes

No existe estado para invertir el número.

### ¿Por qué necesitamos este paso?

Necesitamos almacenar los dígitos extraídos, modificar una copia y acumular el número reconstruido.

### Escribe ahora

```java
List<Integer> digitos = new ArrayList<>();
int temporal = num;
int numInvertido = 0;
```

### Explicación detallada

`numInvertido` comienza en 0 porque iremos sumando cada dígito multiplicado por su potencia de 10 correspondiente.

### Elementos nuevos

- `numInvertido`: acumulador del número reconstruido.

### Estado después

Hay tres piezas de estado: lista, copia y acumulador.

### Por qué podemos avanzar

Podemos extraer los dígitos como en EJ07.

## Paso 2 - Extraer dígitos

### Estado antes

`digitos` está vacía y `temporal` conserva el número.

### ¿Por qué necesitamos este paso?

La reconstrucción posterior necesita cada dígito como elemento individual.

### Escribe ahora

```java
while (temporal > 0) {
    digitos.add(temporal % 10);
    temporal /= 10;
}
```

### Explicación detallada

Este bloque repite el patrón ya explicado en EJ07. La diferencia es que aquí NO invertimos la lista: el orden de extracción ya corresponde al orden que necesitamos para reconstruir el número invertido.

### Elementos nuevos

- Reutilización deliberada del patrón de extracción.

### Estado después

Para 1221 la lista queda `[1,2,2,1]`; para 1234 quedaría `[4,3,2,1]`.

### Por qué podemos avanzar

Ahora asignaremos valor posicional a cada elemento.

## Paso 3 - Reconstruir con Math.pow

### Estado antes

Tenemos los dígitos en orden de extracción.

### ¿Por qué necesitamos este paso?

Cada dígito debe ocupar una potencia de 10 según su posición en el número invertido.

### Escribe ahora

```java
for (int pos = 0; pos <= digitos.size() - 1; pos++) {
    numInvertido += digitos.get(pos)
            * (int) Math.pow(10, digitos.size() - pos - 1);
}
```

### Explicación detallada

`pos` recorre índices. `digitos.get(pos)` obtiene el dígito. `digitos.size()-pos-1` calcula el exponente: empieza alto y disminuye. `Math.pow(10, exponente)` produce 1000, 100, 10, 1, etc. La multiplicación ubica el dígito en su posición y `+=` acumula el número.

### Elementos nuevos

- `pos` como índice de control.
- `digitos.get(pos)`.
- `Math.pow(10, exponente)` para valor posicional.

### Estado después

`numInvertido` contiene la representación invertida del número original.

### Por qué podemos avanzar

Solo falta comparar ambos enteros.

## Paso 4 - Retornar la comparación

### Estado antes

Tenemos `num` y `numInvertido`.

### ¿Por qué necesitamos este paso?

La definición operacional del ejercicio es verdadera cuando ambos valores coinciden.

### Escribe ahora

```java
return num == numInvertido;
```

### Explicación detallada

La comparación `==` entre enteros produce `true` o `false`, exactamente el tipo de retorno del método.

### Elementos nuevos

- Resultado booleano directo.

### Estado después

El método queda completo.

### Por qué podemos avanzar

Podemos ejecutar con un caso capicúa y otro no capicúa.

## Traza / simulación manual

Para 1234, los dígitos extraídos son `[4,3,2,1]`. Se reconstruye `4*1000 + 3*100 + 2*10 + 1 = 4321`; como 1234 != 4321, el resultado es `false`. Para 1221, el reconstruido vuelve a ser 1221.

## Auditoría del artefacto construido

| Elemento | Qué hace | Por qué existe | Efecto |
|---|---|---|---|
| Preparar lista, temporal y acumulador | `numInvertido` comienza en 0 porque iremos sumando cada dígito multiplicado por su potencia de 10 correspondiente. | Necesitamos almacenar los dígitos extraídos, modificar una copia y acumular el número reconstruido. | Hay tres piezas de estado: lista, copia y acumulador. |
| Extraer dígitos | Este bloque repite el patrón ya explicado en EJ07. La diferencia es que aquí NO invertimos la lista: el orden de extracción ya corresponde al orden que necesitamos para reconstruir el número invertido. | La reconstrucción posterior necesita cada dígito como elemento individual. | Para 1221 la lista queda `[1,2,2,1]`; para 1234 quedaría `[4,3,2,1]`. |
| Reconstruir con Math.pow | `pos` recorre índices. `digitos.get(pos)` obtiene el dígito. `digitos.size()-pos-1` calcula el exponente: empieza alto y disminuye. `Math.pow(10, exponente)` produce 1000, 100, 10, 1, etc. La multiplicación ubica el dígito en su posición y `+=` acumula el número. | Cada dígito debe ocupar una potencia de 10 según su posición en el número invertido. | `numInvertido` contiene la representación invertida del número original. |
| Retornar la comparación | La comparación `==` entre enteros produce `true` o `false`, exactamente el tipo de retorno del método. | La definición operacional del ejercicio es verdadera cuando ambos valores coinciden. | El método queda completo. |

## Archivo completo al terminar este ejemplo

```java
import java.util.ArrayList;
import java.util.List;

public class EJ08_EsCapicua {
    public static boolean esCapicua(int num) {
        List<Integer> digitos = new ArrayList<>();
        int temporal = num;
        int numInvertido = 0;

        while (temporal > 0) {
            digitos.add(temporal % 10);
            temporal /= 10;
        }

        for (int pos = 0; pos <= digitos.size() - 1; pos++) {
            numInvertido += digitos.get(pos)
                    * (int) Math.pow(10, digitos.size() - pos - 1);
        }

        return num == numInvertido;
    }

    public static void main(String[] args) {
        int numero = 1221;
        System.out.println("El numero " + numero + " es capicua: " + esCapicua(numero));
    }
}
```

## Antes de ejecutar: predicción

1. ¿Qué lista se forma al extraer los dígitos de 1221?
2. ¿Qué condición final determinará el booleano?

## Ejecuta / valida

En IntelliJ ejecuta el método `main`. En terminal:

```bash
javac EJ08_EsCapicua.java
java EJ08_EsCapicua
```

## Resultado esperado

Para 1221 debe mostrar `true`. Si cambias a 1234 debe mostrar `false`.

## Cómo interpretarlo

El método no busca texto simétrico: reconstruye numéricamente el valor invertido y realiza una comparación entera.

## Variación A

Cambia el número a 12321 y traza solo la primera y la última iteración del `for`.

## Error o caso límite controlado

Un error frecuente es usar un exponente desplazado, por ejemplo `digitos.size()-pos`, lo que multiplica todas las posiciones por 10 de más.

## Por qué ocurre

El exponente de la primera posición para una lista de n dígitos debe ser n-1.

## Corrección razonada

Usa `digitos.size() - pos - 1` y verifica los extremos: primera posición -> n-1; última -> 0.

## Qué debes poder explicar con tus palabras

- por qué la lista no se invierte aquí
- cómo se calcula el exponente
- cómo se construye numInvertido
- por qué el retorno es booleano

## T08 - Tarea espejo

### Enunciado

Completa el método y valida `12321 -> true` y `12345 -> false`.

### Archivo a modificar

`T08_EsCapicua.java`

### Restricción

Reconstruye numInvertido con la lista y `Math.pow`; no conviertas a String.

### Pista

El exponente es `digitos.size() - pos - 1`.

### Evidencia que debes mostrar

Dos líneas de salida, una verdadera y una falsa.

### Cómo saber si está correcta

12321 debe ser true y 12345 false.

---

# EJ09 - Integración: clase ProAritmetica

## Qué vamos a construir / resolver

Integrar los cuatro métodos utilitarios del material en un único programa que recibe un rango, genera un número y analiza sus dígitos.

## Qué aprenderás aquí

- integrar `numeroAleatorio`, `cuentaDigitos`, `digitosNumero` y `esCapicua`
- leer límites con `Scanner`
- interpretar una salida completa
- verificar que cada método conserva una responsabilidad específica

## Archivos, recursos o artefactos involucrados

- `EJ09_ProAritmetica.java`

## Punto de partida

Los métodos ya fueron estudiados por separado. El objetivo ahora no es introducir nueva lógica, sino conectarlos en el orden del ejercicio fuente.

## Paso 1 - Preparar imports

### Estado antes

El archivo integrador todavía no conoce listas, Collections ni Scanner.

### ¿Por qué necesitamos este paso?

La clase utiliza colecciones en dos métodos y entrada de teclado en `main`.

### Escribe ahora

```java
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;
import java.util.Scanner;
```

### Explicación detallada

Estos imports provienen de `java.util`. `Math` no requiere import porque está en `java.lang`.

### Elementos nuevos

- `Scanner` para entrada de usuario en el integrador.

### Estado después

El archivo puede resolver los tipos auxiliares.

### Por qué podemos avanzar

Podemos colocar los métodos ya construidos.

## Paso 2 - Incorporar numeroAleatorio y cuentaDigitos

### Estado antes

La clase no tiene operaciones utilitarias.

### ¿Por qué necesitamos este paso?

El flujo del main primero genera un número y después necesita conocer su cantidad de dígitos.

### Escribe ahora

```java
public static int numeroAleatorio(int min, int max) {
    int aleatorio = (int) (Math.random() * (max - min + 1) + min);
    return aleatorio;
}

public static int cuentaDigitos(int num) {
    int canDigitos = (int) Math.log10(Math.abs(num)) + 1;
    return canDigitos;
}
```

### Explicación detallada

Ambos bloques reutilizan exactamente los patrones ya estudiados. No hay una dependencia interna entre ellos: cada método resuelve una responsabilidad.

### Elementos nuevos

- Integración de métodos previamente explicados.

### Estado después

La clase puede generar y contar.

### Por qué podemos avanzar

Faltan lista de dígitos y capicúa.

## Paso 3 - Incorporar digitosNumero y esCapicua

### Estado antes

Aún no podemos listar dígitos ni validar simetría.

### ¿Por qué necesitamos este paso?

Son las dos operaciones restantes del ejercicio.

### Escribe ahora

```java
public static List<Integer> digitosNumero(int num) {
    List<Integer> digitos = new ArrayList<>();
    int temporal = num;
    while (temporal > 0) {
        digitos.add(temporal % 10);
        temporal /= 10;
    }
    Collections.reverse(digitos);
    return digitos;
}

public static boolean esCapicua(int num) {
    List<Integer> digitos = new ArrayList<>();
    int temporal = num;
    int numInvertido = 0;
    while (temporal > 0) {
        digitos.add(temporal % 10);
        temporal /= 10;
    }
    for (int pos = 0; pos <= digitos.size() - 1; pos++) {
        numInvertido += digitos.get(pos)
                * (int) Math.pow(10, digitos.size() - pos - 1);
    }
    return num == numInvertido;
}
```

### Explicación detallada

`digitosNumero` invierte la lista para devolver el orden original. `esCapicua` no la invierte porque aprovecha el orden de extracción para reconstruir el número invertido. Esa diferencia es intencional.

### Elementos nuevos

- Convivencia de dos recorridos similares con resultados distintos.

### Estado después

La clase ya contiene las cuatro operaciones del material.

### Por qué podemos avanzar

Falta orquestarlas desde `main`.

## Paso 4 - Leer rango y generar número

### Estado antes

Los métodos existen, pero ninguno se invoca.

### ¿Por qué necesitamos este paso?

El ejercicio solicita límites N1 y N2 definidos por el usuario.

### Escribe ahora

```java
Scanner sc = new Scanner(System.in);
System.out.print("Ingresa el limite inferior: ");
int n1 = sc.nextInt();
System.out.print("Ingresa el limite superior: ");
int n2 = sc.nextInt();
int n3 = numeroAleatorio(n1, n2);
```

### Explicación detallada

`Scanner` lee los dos enteros. `n3` recibe el valor generado y se convierte en la entrada común de los demás métodos.

### Elementos nuevos

- `n1`, `n2`: límites.
- `n3`: número generado y objeto de análisis.

### Estado después

Existe un número aleatorio concreto para analizar durante esa ejecución.

### Por qué podemos avanzar

Podemos pasar n3 a cada método y mostrar resultados.

## Paso 5 - Mostrar análisis completo

### Estado antes

`n3` ya fue generado.

### ¿Por qué necesitamos este paso?

La salida debe hacer visible cada resultado del proceso.

### Escribe ahora

```java
System.out.println("Numero aleatorio entre " + n1 + " y " + n2 + ": " + n3);
System.out.println("El numero " + n3 + " tiene " + cuentaDigitos(n3) + " digitos");
List<Integer> digitos = digitosNumero(n3);
System.out.println("El numero " + n3 + " esta formado por los digitos " + digitos);
boolean capicua = esCapicua(n3);
System.out.println("El numero " + n3 + " es capicua: " + capicua);
sc.close();
```

### Explicación detallada

El mismo `n3` alimenta todas las operaciones. Guardar `digitos` y `capicua` hace explícito qué devuelve cada método. `sc.close()` cierra el recurso al terminar.

### Elementos nuevos

- Orquestación de resultados en `main`.

### Estado después

El programa cumple el flujo completo del ejercicio.

### Por qué podemos avanzar

Podemos validarlo con un rango positivo.

## Traza / simulación manual

Si ingresas 1500 y 3000, `n3` quedará dentro de ese rango. Por ello tendrá 4 dígitos. La lista debe contener exactamente esos cuatro dígitos en orden. `esCapicua` dependerá del valor aleatorio concreto.

## Auditoría del artefacto construido

| Elemento | Qué hace | Por qué existe | Efecto |
|---|---|---|---|
| Preparar imports | Estos imports provienen de `java.util`. `Math` no requiere import porque está en `java.lang`. | La clase utiliza colecciones en dos métodos y entrada de teclado en `main`. | El archivo puede resolver los tipos auxiliares. |
| Incorporar numeroAleatorio y cuentaDigitos | Ambos bloques reutilizan exactamente los patrones ya estudiados. No hay una dependencia interna entre ellos: cada método resuelve una responsabilidad. | El flujo del main primero genera un número y después necesita conocer su cantidad de dígitos. | La clase puede generar y contar. |
| Incorporar digitosNumero y esCapicua | `digitosNumero` invierte la lista para devolver el orden original. `esCapicua` no la invierte porque aprovecha el orden de extracción para reconstruir el número invertido. Esa diferencia es intencional. | Son las dos operaciones restantes del ejercicio. | La clase ya contiene las cuatro operaciones del material. |
| Leer rango y generar número | `Scanner` lee los dos enteros. `n3` recibe el valor generado y se convierte en la entrada común de los demás métodos. | El ejercicio solicita límites N1 y N2 definidos por el usuario. | Existe un número aleatorio concreto para analizar durante esa ejecución. |
| Mostrar análisis completo | El mismo `n3` alimenta todas las operaciones. Guardar `digitos` y `capicua` hace explícito qué devuelve cada método. `sc.close()` cierra el recurso al terminar. | La salida debe hacer visible cada resultado del proceso. | El programa cumple el flujo completo del ejercicio. |

## Archivo completo al terminar este ejemplo

```java
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;
import java.util.Scanner;

public class EJ09_ProAritmetica {
    public static int numeroAleatorio(int min, int max) {
        int aleatorio = (int) (Math.random() * (max - min + 1) + min);
        return aleatorio;
    }

    public static int cuentaDigitos(int num) {
        int canDigitos = (int) Math.log10(Math.abs(num)) + 1;
        return canDigitos;
    }

    public static List<Integer> digitosNumero(int num) {
        List<Integer> digitos = new ArrayList<>();
        int temporal = num;

        while (temporal > 0) {
            digitos.add(temporal % 10);
            temporal /= 10;
        }

        Collections.reverse(digitos);
        return digitos;
    }

    public static boolean esCapicua(int num) {
        List<Integer> digitos = new ArrayList<>();
        int temporal = num;
        int numInvertido = 0;

        while (temporal > 0) {
            digitos.add(temporal % 10);
            temporal /= 10;
        }

        for (int pos = 0; pos <= digitos.size() - 1; pos++) {
            numInvertido += digitos.get(pos)
                    * (int) Math.pow(10, digitos.size() - pos - 1);
        }

        return num == numInvertido;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.println("Numero aleatorio entre N1 y N2");
        System.out.print("Ingresa el limite inferior: ");
        int n1 = sc.nextInt();
        System.out.print("Ingresa el limite superior: ");
        int n2 = sc.nextInt();

        int n3 = numeroAleatorio(n1, n2);
        System.out.println("Numero aleatorio entre " + n1 + " y " + n2 + ": " + n3);

        System.out.println("\nCantidad de digitos de un numero entero");
        System.out.println("El numero " + n3 + " tiene " + cuentaDigitos(n3) + " digitos");

        System.out.println("\nDigitos de un numero entero");
        List<Integer> digitos = digitosNumero(n3);
        System.out.println("El numero " + n3 + " esta formado por los digitos " + digitos);

        System.out.println("\nValidar si un numero es capicua");
        boolean capicua = esCapicua(n3);
        System.out.println("El numero " + n3 + " es capicua: " + capicua);

        sc.close();
    }
}
```

## Antes de ejecutar: predicción

1. Si el rango es 1500-3000, ¿cuántos dígitos esperas para cualquier valor generado?
2. ¿Puedes predecir con certeza si será capicúa? Explica por qué.

## Ejecuta / valida

En IntelliJ ejecuta el método `main`. En terminal:

```bash
javac EJ09_ProAritmetica.java
java EJ09_ProAritmetica
```

## Resultado esperado

La salida exacta cambia por el aleatorio, pero el número debe estar entre los límites, `cuentaDigitos` debe ser coherente con el número, la lista debe reproducir sus dígitos y el booleano debe corresponder a su simetría.

## Cómo interpretarlo

Cada método tiene una responsabilidad y `main` coordina el flujo. Esa separación permite probar los métodos de manera independiente antes de integrarlos.

## Variación A

Ejecuta con rango 1221-1221. El número generado será 1221, la cantidad 4, la lista `[1,2,2,1]` y capicúa `true`. Esta variación convierte la parte aleatoria en un caso determinista para validar todo el flujo.

## Error o caso límite controlado

Si usas un rango que incluye 0, la versión fuente de `cuentaDigitos` presenta el caso límite estudiado en EJ06. El flujo original usa rangos positivos como 1500-3000.

## Por qué ocurre

El método fuente de conteo presupone números distintos de cero y el ejercicio principal trabaja con enteros positivos.

## Corrección razonada

Para reproducir estrictamente la sesión usa rangos positivos. En T09 integrarás la versión controlada de T06 para que el programa también trate 0 correctamente.

## Qué debes poder explicar con tus palabras

- responsabilidad de cada método
- por qué n3 conecta todo el flujo
- diferencia entre salida aleatoria y propiedades verificables
- cómo usar un rango de un solo valor para validar

## T09 - Tarea espejo

### Enunciado

Construye el integrador usando las soluciones T05-T08. Debe leer un rango, generar un número y mostrar cantidad de dígitos, lista y capicúa. Incluye el caso `num==0` en `cuentaDigitos`.

### Archivo a modificar

`T09_ProAritmetica.java`

### Restricción

Reutiliza las técnicas de la sesión; no conviertas el número a String ni uses otra API de aleatoriedad.

### Pista

Resuelve primero los cuatro métodos y recién después completa `main`.

### Evidencia que debes mostrar

Código completo y una ejecución con un rango elegido.

### Cómo saber si está correcta

Prueba adicional con rango 1221-1221: debe producir 1221, 4, `[1, 2, 2, 1]` y `true`.

---
# 6. Cierre de la sesión

En esta sesión construiste una ruta completa desde operaciones aisladas de `Math` hasta una clase utilitaria integrada. Empezaste verificando los campos `PI` y `E`, después comparaste métodos de redondeo y selección, y utilizaste funciones de potencia, raíz, logaritmos y conversión angular. A continuación aplicaste `Math.random()` para transformar un valor de `[0,1)` en un entero dentro de un rango y usaste `Math.log10()` para deducir la cantidad de dígitos de un número.

La parte más importante no fue memorizar nombres, sino aprender a relacionar una necesidad con una operación: `abs` para magnitud, `floor/ceil/round` para aproximaciones distintas, `pow` para potencia, `log10` para orden de magnitud y `random` para generación pseudoaleatoria. También trazaste el ciclo que extrae dígitos y observaste por qué `digitosNumero` invierte una lista mientras `esCapicua` conserva el orden de extracción para reconstruir el número invertido.

Antes de cerrar, repasa especialmente tres puntos: la diferencia entre `floor`, `ceil` y `round`; la fórmula inclusiva de `numeroAleatorio`; y la traza `%10` / `/=10`. Son las zonas donde un pequeño error cambia el resultado completo.

Puedes continuar reforzando programación Java en **Lideratec Academy**, consultar material en https://lideratecacademy.com/blog/ y revisar el canal https://www.youtube.com/@LideratecAcademy.

El laboratorio materializado de FASE 15 puede utilizarse después como recurso opcional para comparar tu implementación con los archivos ejecutables.
