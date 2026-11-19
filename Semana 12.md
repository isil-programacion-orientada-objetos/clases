# Lideratec Academy — Guía del estudiante
## Programación Orientada a Objetos · Sesión 12 · Colecciones genéricas

## Propósito de la sesión
En un inventario o un registro de calificaciones no basta con guardar un único número: necesitamos varios valores que puedan crecer, consultarse y relacionarse con objetos. Java exige que los tipos genéricos de sus colecciones sean tipos de referencia. Por esa razón, comenzaremos distinguiendo `int` de `Integer`, y veremos cómo el autoboxing convierte automáticamente un valor primitivo en su clase envolvente. Después utilizaremos `ArrayList<Integer>` para preservar una secuencia de notas o ventas, y `HashSet<Character>` para mantener letras sin repetición. Finalmente, crearemos una clase `Producto` y la almacenaremos en `ArrayList<Producto>`, hasta integrar productos, existencias y familias en un pequeño inventario. El objetivo no es memorizar líneas de código: cada operación debe justificarse, predecirse y comprobarse mediante una salida observable. Al terminar podrás explicar cuándo conviene una lista, cuándo un conjunto y por qué los objetos permiten modelar artículos reales.

## Resultado observable
Al finalizar la sesión podrás construir y ejecutar proyectos Java 21 que utilicen clases envolventes, autoboxing y colecciones genéricas para resolver necesidades de almacenamiento. Podrás demostrar qué ocurre al agregar, sustituir y recorrer valores Integer; explicar por qué HashSet<Character> rechaza un elemento repetido; y representar un artículo con atributos propios para insertarlo en una colección de objetos. Demostrarás dominio si, sin copiar la solución, predices la salida, ejecutas, comparas el resultado y argumentas cuál instrucción explica cada cambio.

**Desempeños verificables:** utilizar wrappers; identificar autoboxing/unboxing; convertir cadenas numéricas; manipular ArrayList<Integer>; interpretar operaciones con Character; controlar duplicados con HashSet<Character>; modelar Producto; integrar colecciones.

## Preparación del entorno desde cero
1. Instala un JDK 21 si no está disponible. En una terminal ejecuta `java -version` y `javac -version`: ambos deben indicar versión 21.
2. Abre IntelliJ IDEA. Selecciona **New Project → Java**. Nombre: `ColeccionesGenericasS12`. Selecciona **JDK 21**; si ya tienes uno instalado, selecciónalo. No necesitas Maven, Gradle ni Tomcat para este laboratorio.
3. En el panel del proyecto, crea la carpeta `src` si tu configuración no la generó. Dentro crea **New → Java Class → Ej01**. El nombre de la clase pública debe coincidir con el nombre del archivo.
4. Copia el código de EJ01 y ejecuta con la flecha verde junto a `main`. Verifica que el panel Run muestre exactamente las líneas esperadas. Para los demás ejercicios crea `Ej02` ... `Ej08` en el mismo `src`.
5. Alternativa sin IDE: desde la carpeta `src`, ejecuta `javac Ej01.java` y luego `java Ej01` (reemplaza 01 por el ID).
**Error frecuente:** escribir `ArrayList<int>` provoca error de compilación porque los genéricos no admiten primitivos; utiliza `ArrayList<Integer>`.

## Plan de aula presencial/virtual: 120 minutos
- 0–10 min: apertura, preguntas sobre tipos primitivos y referencia.
- 10–25 min: EJ01 y EJ02 en demostración, predicción y contraste.
- 25–52 min: EJ03 y EJ04: lista, modificación y acumulación con práctica acompañada.
- 52–70 min: EJ05 y EJ06: Character y unicidad; T05/T06 rápidos.
- 70–108 min: EJ07 y EJ08: Producto e integración; T07 en parejas.
- 108–120 min: socialización, control de salida y cierre.
**Trabajo autónomo:** completar las ocho tareas espejo y las extensiones no concluidas durante el aula. No se presupone que los 16 ejercicios quepan completos en 120 minutos.

## EJ01 — Wrappers y autoboxing: convertir sin confundir tipos

**Objetivo técnico — qué haremos y qué aprenderemos**
En este ejemplo resolveremos una necesidad precisa: wrappers y autoboxing: convertir sin confundir tipos. Primero prepararemos las estructuras de Java que corresponden al tema «Integer y conversión explícita», después incorporaremos los datos y observaremos la operación que demuestra su funcionamiento. Antes de ejecutar, interpretaremos las instrucciones clave y anticiparemos el resultado. Finalmente contrastaremos la salida con la predicción y discutiremos qué cambiaría si modificamos un valor. El criterio de éxito es poder relacionar el comportamiento de la consola con la estructura utilizada, y no solamente obtener una ejecución sin errores.

**¿Qué problema concreto resolveremos?**
Necesitamos que Java maneje correctamente integer y conversión explícita en un caso pequeño y verificable. Una definición por sí sola no demuestra cómo varía el estado del programa; por ello construiremos y ejecutaremos el código.

**Archivo:** `src/Ej01.java` · **Punto de entrada:** `main` · **Duración de trabajo sugerida:** 8–15 minutos, según la complejidad.

### Paso 1: elaboración progresiva
**Necesidad:** La variable unidades es un int primitivo: se usa para contar sin crear explícitamente un objeto.
**Lugar:** escribe estas líneas, en el orden indicado, en `src/Ej01.java` después del bloque anterior.
```java
public class Ej01 {
    public static void main(String[] args) {
        int unidades = 12;
        Integer caja = unidades;
```
**Interpretación:** La variable unidades es un int primitivo: se usa para contar sin crear explícitamente un objeto. Este paso forma parte de un archivo aún incompleto; termina los demás bloques antes de ejecutar.

### Paso 2: elaboración progresiva
**Necesidad:** La asignación a Integer activa autoboxing: Java envuelve 12 en una instancia que la referencia caja permite usar.
**Lugar:** escribe estas líneas, en el orden indicado, en `src/Ej01.java` después del bloque anterior.
```java
        int recuperadas = caja;
        System.out.println("Tipo envolvente: " + caja.getClass().getSimpleName());
        System.out.println("Valor: " + recuperadas);
        System.out.println("Máximo: " + Integer.max(recuperadas, 20));
```
**Interpretación:** La asignación a Integer activa autoboxing: Java envuelve 12 en una instancia que la referencia caja permite usar. Este paso forma parte de un archivo aún incompleto; termina los demás bloques antes de ejecutar.

### Paso 3: elaboración progresiva
**Necesidad:** La asignación de Integer a int recupera el valor mediante unboxing.
**Lugar:** escribe estas líneas, en el orden indicado, en `src/Ej01.java` después del bloque anterior.
```java
    }
}
```
**Interpretación:** La asignación de Integer a int recupera el valor mediante unboxing. Ahora el archivo puede compilarse y ejecutarse.

### Archivo completo para comprobación
```java
public class Ej01 {
    public static void main(String[] args) {
        int unidades = 12;
        Integer caja = unidades;
        int recuperadas = caja;
        System.out.println("Tipo envolvente: " + caja.getClass().getSimpleName());
        System.out.println("Valor: " + recuperadas);
        System.out.println("Máximo: " + Integer.max(recuperadas, 20));
    }
}
```

**Predice antes de ejecutar:** ¿Por qué `Integer caja = unidades` compila y `ArrayList<int>` no?
**Salida esperada:**
```text
Tipo envolvente: Integer
Valor: 12
Máximo: 20
```
**Extensión de razonamiento:** Cambiar 12 por 25 y predecir si cambiará el máximo.
**Tarea espejo T01:** Modificar la demostración para trabajar con `int unidades = 24`, convertirlo a `Integer` mediante autoboxing, recuperarlo y mostrar `Integer.min(recuperadas, 20)`.
**Entrega:** archivo `T01.java`, captura de ejecución y explicación causal de 3–5 líneas.

## EJ02 — Parsear cantidades recibidas como texto

**Objetivo técnico — qué haremos y qué aprenderemos**
En este ejemplo resolveremos una necesidad precisa: parsear cantidades recibidas como texto. Primero prepararemos las estructuras de Java que corresponden al tema «Integer.parseInt e Integer.compare», después incorporaremos los datos y observaremos la operación que demuestra su funcionamiento. Antes de ejecutar, interpretaremos las instrucciones clave y anticiparemos el resultado. Finalmente contrastaremos la salida con la predicción y discutiremos qué cambiaría si modificamos un valor. El criterio de éxito es poder relacionar el comportamiento de la consola con la estructura utilizada, y no solamente obtener una ejecución sin errores.

**¿Qué problema concreto resolveremos?**
Necesitamos que Java maneje correctamente integer.parseint e integer.compare en un caso pequeño y verificable. Una definición por sí sola no demuestra cómo varía el estado del programa; por ello construiremos y ejecutaremos el código.

**Archivo:** `src/Ej02.java` · **Punto de entrada:** `main` · **Duración de trabajo sugerida:** 8–15 minutos, según la complejidad.

### Paso 1: elaboración progresiva
**Necesidad:** La fuente externa está representada por una cadena, no por un número; no debe sumarse como texto.
**Lugar:** escribe estas líneas, en el orden indicado, en `src/Ej02.java` después del bloque anterior.
```java
public class Ej02 {
    public static void main(String[] args) {
        String dato = "18";
        int cantidad = Integer.parseInt(dato);
```
**Interpretación:** La fuente externa está representada por una cadena, no por un número; no debe sumarse como texto. Este paso forma parte de un archivo aún incompleto; termina los demás bloques antes de ejecutar.

### Paso 2: elaboración progresiva
**Necesidad:** Integer.parseInt interpreta los caracteres decimales y produce un int; si el texto es inválido lanzará NumberFormatException.
**Lugar:** escribe estas líneas, en el orden indicado, en `src/Ej02.java` después del bloque anterior.
```java
        int comparacion = Integer.compare(cantidad, 15);
        System.out.println("Cantidad: " + cantidad);
        System.out.println("Comparación con 15: " + comparacion);
    }
```
**Interpretación:** Integer.parseInt interpreta los caracteres decimales y produce un int; si el texto es inválido lanzará NumberFormatException. Este paso forma parte de un archivo aún incompleto; termina los demás bloques antes de ejecutar.

### Paso 3: elaboración progresiva
**Necesidad:** Integer.compare devuelve positivo, cero o negativo según la relación; 18 es mayor que 15.
**Lugar:** escribe estas líneas, en el orden indicado, en `src/Ej02.java` después del bloque anterior.
```java
}
```
**Interpretación:** Integer.compare devuelve positivo, cero o negativo según la relación; 18 es mayor que 15. Ahora el archivo puede compilarse y ejecutarse.

### Archivo completo para comprobación
```java
public class Ej02 {
    public static void main(String[] args) {
        String dato = "18";
        int cantidad = Integer.parseInt(dato);
        int comparacion = Integer.compare(cantidad, 15);
        System.out.println("Cantidad: " + cantidad);
        System.out.println("Comparación con 15: " + comparacion);
    }
}
```

**Predice antes de ejecutar:** ¿Qué ocurriría si el dato fuera `"dieciocho"`?
**Salida esperada:**
```text
Cantidad: 18
Comparación con 15: 1
```
**Extensión de razonamiento:** Cambiar el dato a `"12"` y justificar el signo de `compare`.
**Tarea espejo T02:** Convertir el texto `"9"` a int mediante `Integer.parseInt` y compararlo con 15 utilizando `Integer.compare`.
**Entrega:** archivo `T02.java`, captura de ejecución y explicación causal de 3–5 líneas.

## EJ03 — Almacenar calificaciones con ArrayList<Integer>

**Objetivo técnico — qué haremos y qué aprenderemos**
En este ejemplo resolveremos una necesidad precisa: almacenar calificaciones con arraylist<integer>. Primero prepararemos las estructuras de Java que corresponden al tema «ArrayList<Integer> y operaciones de lista», después incorporaremos los datos y observaremos la operación que demuestra su funcionamiento. Antes de ejecutar, interpretaremos las instrucciones clave y anticiparemos el resultado. Finalmente contrastaremos la salida con la predicción y discutiremos qué cambiaría si modificamos un valor. El criterio de éxito es poder relacionar el comportamiento de la consola con la estructura utilizada, y no solamente obtener una ejecución sin errores.

**¿Qué problema concreto resolveremos?**
Necesitamos que Java maneje correctamente arraylist<integer> y operaciones de lista en un caso pequeño y verificable. Una definición por sí sola no demuestra cómo varía el estado del programa; por ello construiremos y ejecutaremos el código.

**Archivo:** `src/Ej03.java` · **Punto de entrada:** `main` · **Duración de trabajo sugerida:** 8–15 minutos, según la complejidad.

### Paso 1: elaboración progresiva
**Necesidad:** El import permite escribir ArrayList sin nombre calificado.
**Lugar:** escribe estas líneas, en el orden indicado, en `src/Ej03.java` después del bloque anterior.
```java
import java.util.ArrayList;
public class Ej03 {
    public static void main(String[] args) {
        ArrayList<Integer> notas = new ArrayList<>();
```
**Interpretación:** El import permite escribir ArrayList sin nombre calificado. Este paso forma parte de un archivo aún incompleto; termina los demás bloques antes de ejecutar.

### Paso 2: elaboración progresiva
**Necesidad:** La colección declara Integer, nunca int: el argumento genérico exige una referencia.
**Lugar:** escribe estas líneas, en el orden indicado, en `src/Ej03.java` después del bloque anterior.
```java
        notas.add(14);
        notas.add(17);
        notas.add(12);
        notas.set(2, 16);
```
**Interpretación:** La colección declara Integer, nunca int: el argumento genérico exige una referencia. Este paso forma parte de un archivo aún incompleto; termina los demás bloques antes de ejecutar.

### Paso 3: elaboración progresiva
**Necesidad:** add incorpora elementos al final de la lista y realiza autoboxing de los literales.
**Lugar:** escribe estas líneas, en el orden indicado, en `src/Ej03.java` después del bloque anterior.
```java
        System.out.println("Notas: " + notas);
        System.out.println("Segunda nota: " + notas.get(1));
        System.out.println("Cantidad: " + notas.size());
    }
```
**Interpretación:** add incorpora elementos al final de la lista y realiza autoboxing de los literales. Este paso forma parte de un archivo aún incompleto; termina los demás bloques antes de ejecutar.

### Paso 4: elaboración progresiva
**Necesidad:** set reemplaza la tercera posición (índice 2), conservando el tamaño de la colección.
**Lugar:** escribe estas líneas, en el orden indicado, en `src/Ej03.java` después del bloque anterior.
```java
}
```
**Interpretación:** set reemplaza la tercera posición (índice 2), conservando el tamaño de la colección. Ahora el archivo puede compilarse y ejecutarse.

### Archivo completo para comprobación
```java
import java.util.ArrayList;
public class Ej03 {
    public static void main(String[] args) {
        ArrayList<Integer> notas = new ArrayList<>();
        notas.add(14);
        notas.add(17);
        notas.add(12);
        notas.set(2, 16);
        System.out.println("Notas: " + notas);
        System.out.println("Segunda nota: " + notas.get(1));
        System.out.println("Cantidad: " + notas.size());
    }
}
```

**Predice antes de ejecutar:** ¿Por qué los índices comienzan en cero?
**Salida esperada:**
```text
Notas: [14, 17, 16]
Segunda nota: 17
Cantidad: 3
```
**Extensión de razonamiento:** Insertar 19 al final y actualizar la cantidad esperada.
**Tarea espejo T03:** Crear un ArrayList<Integer> con 11, 13 y 18; reemplazar el primer valor por 15 e imprimir la lista y su tamaño.
**Entrega:** archivo `T03.java`, captura de ejecución y explicación causal de 3–5 líneas.

## EJ04 — Calcular un promedio desde una colección

**Objetivo técnico — qué haremos y qué aprenderemos**
En este ejemplo resolveremos una necesidad precisa: calcular un promedio desde una colección. Primero prepararemos las estructuras de Java que corresponden al tema «Recorrido, unboxing y agregación», después incorporaremos los datos y observaremos la operación que demuestra su funcionamiento. Antes de ejecutar, interpretaremos las instrucciones clave y anticiparemos el resultado. Finalmente contrastaremos la salida con la predicción y discutiremos qué cambiaría si modificamos un valor. El criterio de éxito es poder relacionar el comportamiento de la consola con la estructura utilizada, y no solamente obtener una ejecución sin errores.

**¿Qué problema concreto resolveremos?**
Necesitamos que Java maneje correctamente recorrido, unboxing y agregación en un caso pequeño y verificable. Una definición por sí sola no demuestra cómo varía el estado del programa; por ello construiremos y ejecutaremos el código.

**Archivo:** `src/Ej04.java` · **Punto de entrada:** `main` · **Duración de trabajo sugerida:** 8–15 minutos, según la complejidad.

### Paso 1: elaboración progresiva
**Necesidad:** El ArrayList almacena las ventas como Integer y permite ampliarlas sin crear arreglos fijos.
**Lugar:** escribe estas líneas, en el orden indicado, en `src/Ej04.java` después del bloque anterior.
```java
import java.util.ArrayList;
public class Ej04 {
    public static void main(String[] args) {
        ArrayList<Integer> ventas = new ArrayList<>();
```
**Interpretación:** El ArrayList almacena las ventas como Integer y permite ampliarlas sin crear arreglos fijos. Este paso forma parte de un archivo aún incompleto; termina los demás bloques antes de ejecutar.

### Paso 2: elaboración progresiva
**Necesidad:** La variable total comienza en cero: es el acumulador que recibe cada valor.
**Lugar:** escribe estas líneas, en el orden indicado, en `src/Ej04.java` después del bloque anterior.
```java
        ventas.add(10);
        ventas.add(20);
        ventas.add(30);
        int total = 0;
```
**Interpretación:** La variable total comienza en cero: es el acumulador que recibe cada valor. Este paso forma parte de un archivo aún incompleto; termina los demás bloques antes de ejecutar.

### Paso 3: elaboración progresiva
**Necesidad:** El for-each visita cada referencia Integer; al sumarla a total Java aplica unboxing.
**Lugar:** escribe estas líneas, en el orden indicado, en `src/Ej04.java` después del bloque anterior.
```java
        for (Integer venta : ventas) {
            total += venta;
        }
        double promedio = (double) total / ventas.size();
```
**Interpretación:** El for-each visita cada referencia Integer; al sumarla a total Java aplica unboxing. Este paso forma parte de un archivo aún incompleto; termina los demás bloques antes de ejecutar.

### Paso 4: elaboración progresiva
**Necesidad:** La conversión a double antes de dividir evita una división entera.
**Lugar:** escribe estas líneas, en el orden indicado, en `src/Ej04.java` después del bloque anterior.
```java
        System.out.println("Total: " + total);
        System.out.println("Promedio: " + promedio);
    }
}
```
**Interpretación:** La conversión a double antes de dividir evita una división entera. Ahora el archivo puede compilarse y ejecutarse.

### Archivo completo para comprobación
```java
import java.util.ArrayList;
public class Ej04 {
    public static void main(String[] args) {
        ArrayList<Integer> ventas = new ArrayList<>();
        ventas.add(10);
        ventas.add(20);
        ventas.add(30);
        int total = 0;
        for (Integer venta : ventas) {
            total += venta;
        }
        double promedio = (double) total / ventas.size();
        System.out.println("Total: " + total);
        System.out.println("Promedio: " + promedio);
    }
}
```

**Predice antes de ejecutar:** ¿Qué cambia si se omite `(double)` cuando total no es divisible entre tres?
**Salida esperada:**
```text
Total: 60
Promedio: 20.0
```
**Extensión de razonamiento:** Agregar la venta 40 y recalcular total y promedio.
**Tarea espejo T04:** Calcular el total y el promedio de los valores 5, 10 y 15 almacenados en ArrayList<Integer>.
**Entrega:** archivo `T04.java`, captura de ejecución y explicación causal de 3–5 líneas.

## EJ05 — Distinguir letras y dígitos con Character

**Objetivo técnico — qué haremos y qué aprenderemos**
En este ejemplo resolveremos una necesidad precisa: distinguir letras y dígitos con character. Primero prepararemos las estructuras de Java que corresponden al tema «Character.isLetter/isDigit/toUpperCase», después incorporaremos los datos y observaremos la operación que demuestra su funcionamiento. Antes de ejecutar, interpretaremos las instrucciones clave y anticiparemos el resultado. Finalmente contrastaremos la salida con la predicción y discutiremos qué cambiaría si modificamos un valor. El criterio de éxito es poder relacionar el comportamiento de la consola con la estructura utilizada, y no solamente obtener una ejecución sin errores.

**¿Qué problema concreto resolveremos?**
Necesitamos que Java maneje correctamente character.isletter/isdigit/touppercase en un caso pequeño y verificable. Una definición por sí sola no demuestra cómo varía el estado del programa; por ello construiremos y ejecutaremos el código.

**Archivo:** `src/Ej05.java` · **Punto de entrada:** `main` · **Duración de trabajo sugerida:** 8–15 minutos, según la complejidad.

### Paso 1: elaboración progresiva
**Necesidad:** El dato char representa exactamente un carácter que analizaremos.
**Lugar:** escribe estas líneas, en el orden indicado, en `src/Ej05.java` después del bloque anterior.
```java
public class Ej05 {
    public static void main(String[] args) {
        char dato = 'a';
        System.out.println("Es letra: " + Character.isLetter(dato));
```
**Interpretación:** El dato char representa exactamente un carácter que analizaremos. Este paso forma parte de un archivo aún incompleto; termina los demás bloques antes de ejecutar.

### Paso 2: elaboración progresiva
**Necesidad:** isLetter devuelve un booleano que indica si el carácter es una letra.
**Lugar:** escribe estas líneas, en el orden indicado, en `src/Ej05.java` después del bloque anterior.
```java
        System.out.println("Es dígito: " + Character.isDigit(dato));
        System.out.println("Mayúscula: " + Character.toUpperCase(dato));
    }
}
```
**Interpretación:** isLetter devuelve un booleano que indica si el carácter es una letra. Ahora el archivo puede compilarse y ejecutarse.

### Archivo completo para comprobación
```java
public class Ej05 {
    public static void main(String[] args) {
        char dato = 'a';
        System.out.println("Es letra: " + Character.isLetter(dato));
        System.out.println("Es dígito: " + Character.isDigit(dato));
        System.out.println("Mayúscula: " + Character.toUpperCase(dato));
    }
}
```

**Predice antes de ejecutar:** ¿Qué distingue el método `isDigit` de `isLetter`?
**Salida esperada:**
```text
Es letra: true
Es dígito: false
Mayúscula: A
```
**Extensión de razonamiento:** Reemplazar `a` por `7` y predecir las tres líneas.
**Tarea espejo T05:** Aplicar Character.isLetter, Character.isDigit y Character.toUpperCase al carácter `'7'`.
**Entrega:** archivo `T05.java`, captura de ejecución y explicación causal de 3–5 líneas.

## EJ06 — Evitar caracteres repetidos con HashSet<Character>

**Objetivo técnico — qué haremos y qué aprenderemos**
En este ejemplo resolveremos una necesidad precisa: evitar caracteres repetidos con hashset<character>. Primero prepararemos las estructuras de Java que corresponden al tema «HashSet, autoboxing y unicidad», después incorporaremos los datos y observaremos la operación que demuestra su funcionamiento. Antes de ejecutar, interpretaremos las instrucciones clave y anticiparemos el resultado. Finalmente contrastaremos la salida con la predicción y discutiremos qué cambiaría si modificamos un valor. El criterio de éxito es poder relacionar el comportamiento de la consola con la estructura utilizada, y no solamente obtener una ejecución sin errores.

**¿Qué problema concreto resolveremos?**
Necesitamos que Java maneje correctamente hashset, autoboxing y unicidad en un caso pequeño y verificable. Una definición por sí sola no demuestra cómo varía el estado del programa; por ello construiremos y ejecutaremos el código.

**Archivo:** `src/Ej06.java` · **Punto de entrada:** `main` · **Duración de trabajo sugerida:** 8–15 minutos, según la complejidad.

### Paso 1: elaboración progresiva
**Necesidad:** Un HashSet almacena valores únicos y no promete orden de iteración.
**Lugar:** escribe estas líneas, en el orden indicado, en `src/Ej06.java` después del bloque anterior.
```java
import java.util.HashSet;
public class Ej06 {
    public static void main(String[] args) {
        HashSet<Character> letras = new HashSet<>();
```
**Interpretación:** Un HashSet almacena valores únicos y no promete orden de iteración. Este paso forma parte de un archivo aún incompleto; termina los demás bloques antes de ejecutar.

### Paso 2: elaboración progresiva
**Necesidad:** La primera inserción de A devuelve true: el conjunto cambia.
**Lugar:** escribe estas líneas, en el orden indicado, en `src/Ej06.java` después del bloque anterior.
```java
        System.out.println("Primera A: " + letras.add('A'));
        System.out.println("Segunda A: " + letras.add('A'));
        System.out.println("Agregar B: " + letras.add('B'));
        System.out.println("Contiene B: " + letras.contains('B'));
```
**Interpretación:** La primera inserción de A devuelve true: el conjunto cambia. Este paso forma parte de un archivo aún incompleto; termina los demás bloques antes de ejecutar.

### Paso 3: elaboración progresiva
**Necesidad:** La segunda inserción de A devuelve false: el elemento ya estaba.
**Lugar:** escribe estas líneas, en el orden indicado, en `src/Ej06.java` después del bloque anterior.
```java
        System.out.println("Únicos: " + letras.size());
    }
}
```
**Interpretación:** La segunda inserción de A devuelve false: el elemento ya estaba. Ahora el archivo puede compilarse y ejecutarse.

### Archivo completo para comprobación
```java
import java.util.HashSet;
public class Ej06 {
    public static void main(String[] args) {
        HashSet<Character> letras = new HashSet<>();
        System.out.println("Primera A: " + letras.add('A'));
        System.out.println("Segunda A: " + letras.add('A'));
        System.out.println("Agregar B: " + letras.add('B'));
        System.out.println("Contiene B: " + letras.contains('B'));
        System.out.println("Únicos: " + letras.size());
    }
}
```

**Predice antes de ejecutar:** ¿Por qué `add` devuelve false en el segundo intento?
**Salida esperada:**
```text
Primera A: true
Segunda A: false
Agregar B: true
Contiene B: true
Únicos: 2
```
**Extensión de razonamiento:** Agregar nuevamente B y comprobar que el tamaño sigue siendo 2.
**Tarea espejo T06:** Crear un HashSet<Character>, insertar C, D y nuevamente C. Imprimir los tres booleanos retornados por add y el tamaño final, sin depender del orden.
**Entrega:** archivo `T06.java`, captura de ejecución y explicación causal de 3–5 líneas.

## EJ07 — Representar productos como objetos dentro de ArrayList

**Objetivo técnico — qué haremos y qué aprenderemos**
En este ejemplo resolveremos una necesidad precisa: representar productos como objetos dentro de arraylist. Primero prepararemos las estructuras de Java que corresponden al tema «Clase Producto y colección de objetos», después incorporaremos los datos y observaremos la operación que demuestra su funcionamiento. Antes de ejecutar, interpretaremos las instrucciones clave y anticiparemos el resultado. Finalmente contrastaremos la salida con la predicción y discutiremos qué cambiaría si modificamos un valor. El criterio de éxito es poder relacionar el comportamiento de la consola con la estructura utilizada, y no solamente obtener una ejecución sin errores.

**¿Qué problema concreto resolveremos?**
Necesitamos que Java maneje correctamente clase producto y colección de objetos en un caso pequeño y verificable. Una definición por sí sola no demuestra cómo varía el estado del programa; por ello construiremos y ejecutaremos el código.

**Archivo:** `src/Ej07.java` · **Punto de entrada:** `main` · **Duración de trabajo sugerida:** 8–15 minutos, según la complejidad.

### Paso 1: elaboración progresiva
**Necesidad:** La clase interna Producto agrupa atributos relacionados que describen un artículo.
**Lugar:** escribe estas líneas, en el orden indicado, en `src/Ej07.java` después del bloque anterior.
```java
import java.util.ArrayList;
public class Ej07 {
    static class Producto {
        String codigo;
```
**Interpretación:** La clase interna Producto agrupa atributos relacionados que describen un artículo. Este paso forma parte de un archivo aún incompleto; termina los demás bloques antes de ejecutar.

### Paso 2: elaboración progresiva
**Necesidad:** El constructor recibe datos y usa this para asignarlos al objeto actual.
**Lugar:** escribe estas líneas, en el orden indicado, en `src/Ej07.java` después del bloque anterior.
```java
        String descripcion;
        double precio;
        Producto(String codigo, String descripcion, double precio) {
            this.codigo = codigo;
```
**Interpretación:** El constructor recibe datos y usa this para asignarlos al objeto actual. Este paso forma parte de un archivo aún incompleto; termina los demás bloques antes de ejecutar.

### Paso 3: elaboración progresiva
**Necesidad:** ArrayList<Producto> guarda referencias a instancias Producto, no filas aisladas.
**Lugar:** escribe estas líneas, en el orden indicado, en `src/Ej07.java` después del bloque anterior.
```java
            this.descripcion = descripcion;
            this.precio = precio;
        }
    }
```
**Interpretación:** ArrayList<Producto> guarda referencias a instancias Producto, no filas aisladas. Este paso forma parte de un archivo aún incompleto; termina los demás bloques antes de ejecutar.

### Paso 4: elaboración progresiva
**Necesidad:** Cada new crea una instancia diferente y add la incorpora en orden de inserción.
**Lugar:** escribe estas líneas, en el orden indicado, en `src/Ej07.java` después del bloque anterior.
```java
    public static void main(String[] args) {
        ArrayList<Producto> productos = new ArrayList<>();
        productos.add(new Producto("P01", "Teclado", 85.0));
        productos.add(new Producto("P02", "Mouse", 45.0));
```
**Interpretación:** Cada new crea una instancia diferente y add la incorpora en orden de inserción. Este paso forma parte de un archivo aún incompleto; termina los demás bloques antes de ejecutar.

### Paso 5: elaboración progresiva
**Necesidad:** El for-each lee cada objeto y muestra sus atributos con un formato comprensible.
**Lugar:** escribe estas líneas, en el orden indicado, en `src/Ej07.java` después del bloque anterior.
```java
        for (Producto p : productos) {
            System.out.println(p.codigo + " - " + p.descripcion + ": " + p.precio);
        }
    }
```
**Interpretación:** El for-each lee cada objeto y muestra sus atributos con un formato comprensible. Este paso forma parte de un archivo aún incompleto; termina los demás bloques antes de ejecutar.

### Paso 6: elaboración progresiva
**Necesidad:** El for-each lee cada objeto y muestra sus atributos con un formato comprensible.
**Lugar:** escribe estas líneas, en el orden indicado, en `src/Ej07.java` después del bloque anterior.
```java
}
```
**Interpretación:** El for-each lee cada objeto y muestra sus atributos con un formato comprensible. Ahora el archivo puede compilarse y ejecutarse.

### Archivo completo para comprobación
```java
import java.util.ArrayList;
public class Ej07 {
    static class Producto {
        String codigo;
        String descripcion;
        double precio;
        Producto(String codigo, String descripcion, double precio) {
            this.codigo = codigo;
            this.descripcion = descripcion;
            this.precio = precio;
        }
    }
    public static void main(String[] args) {
        ArrayList<Producto> productos = new ArrayList<>();
        productos.add(new Producto("P01", "Teclado", 85.0));
        productos.add(new Producto("P02", "Mouse", 45.0));
        for (Producto p : productos) {
            System.out.println(p.codigo + " - " + p.descripcion + ": " + p.precio);
        }
    }
}
```

**Predice antes de ejecutar:** ¿Por qué se necesita `new Producto(...)` en cada inserción?
**Salida esperada:**
```text
P01 - Teclado: 85.0
P02 - Mouse: 45.0
```
**Extensión de razonamiento:** Agregar un producto P03 / Monitor / 650.0 e imprimirlo.
**Tarea espejo T07:** Crear la clase Producto con código, descripción y precio; insertar P10/Laptop/2500.0 y P11/Cámara/350.0 en ArrayList<Producto>; recorrer e imprimir.
**Entrega:** archivo `T07.java`, captura de ejecución y explicación causal de 3–5 líneas.

## EJ08 — Integrar inventario, precios y códigos distintos

**Objetivo técnico — qué haremos y qué aprenderemos**
En este ejemplo resolveremos una necesidad precisa: integrar inventario, precios y códigos distintos. Primero prepararemos las estructuras de Java que corresponden al tema «ArrayList<Producto>, ArrayList<Integer> y HashSet<Character>», después incorporaremos los datos y observaremos la operación que demuestra su funcionamiento. Antes de ejecutar, interpretaremos las instrucciones clave y anticiparemos el resultado. Finalmente contrastaremos la salida con la predicción y discutiremos qué cambiaría si modificamos un valor. El criterio de éxito es poder relacionar el comportamiento de la consola con la estructura utilizada, y no solamente obtener una ejecución sin errores.

**¿Qué problema concreto resolveremos?**
Necesitamos que Java maneje correctamente arraylist<producto>, arraylist<integer> y hashset<character> en un caso pequeño y verificable. Una definición por sí sola no demuestra cómo varía el estado del programa; por ello construiremos y ejecutaremos el código.

**Archivo:** `src/Ej08.java` · **Punto de entrada:** `main` · **Duración de trabajo sugerida:** 8–15 minutos, según la complejidad.

### Paso 1: elaboración progresiva
**Necesidad:** La clase Producto representa cada existencia mediante código, descripción y stock.
**Lugar:** escribe estas líneas, en el orden indicado, en `src/Ej08.java` después del bloque anterior.
```java
import java.util.ArrayList;
import java.util.HashSet;
public class Ej08 {
    static class Producto {
```
**Interpretación:** La clase Producto representa cada existencia mediante código, descripción y stock. Este paso forma parte de un archivo aún incompleto; termina los demás bloques antes de ejecutar.

### Paso 2: elaboración progresiva
**Necesidad:** La lista inventario conserva los objetos de negocio completos.
**Lugar:** escribe estas líneas, en el orden indicado, en `src/Ej08.java` después del bloque anterior.
```java
        String codigo;
        String descripcion;
        int stock;
        Producto(String codigo, String descripcion, int stock) {
```
**Interpretación:** La lista inventario conserva los objetos de negocio completos. Este paso forma parte de un archivo aún incompleto; termina los demás bloques antes de ejecutar.

### Paso 3: elaboración progresiva
**Necesidad:** La lista existencias separa cantidades Integer para operar y sumar; el conjunto familias guarda letras únicas.
**Lugar:** escribe estas líneas, en el orden indicado, en `src/Ej08.java` después del bloque anterior.
```java
            this.codigo = codigo;
            this.descripcion = descripcion;
            this.stock = stock;
        }
```
**Interpretación:** La lista existencias separa cantidades Integer para operar y sumar; el conjunto familias guarda letras únicas. Este paso forma parte de un archivo aún incompleto; termina los demás bloques antes de ejecutar.

### Paso 4: elaboración progresiva
**Necesidad:** charAt(0) toma la inicial del código; el HashSet evita duplicar familias.
**Lugar:** escribe estas líneas, en el orden indicado, en `src/Ej08.java` después del bloque anterior.
```java
    }
    public static void main(String[] args) {
        ArrayList<Producto> inventario = new ArrayList<>();
        inventario.add(new Producto("A1", "Audífonos", 5));
```
**Interpretación:** charAt(0) toma la inicial del código; el HashSet evita duplicar familias. Este paso forma parte de un archivo aún incompleto; termina los demás bloques antes de ejecutar.

### Paso 5: elaboración progresiva
**Necesidad:** El acumulador suma existencias y las tres salidas permiten verificar dos artículos, ocho unidades y dos familias.
**Lugar:** escribe estas líneas, en el orden indicado, en `src/Ej08.java` después del bloque anterior.
```java
        inventario.add(new Producto("B2", "Parlante", 3));
        ArrayList<Integer> existencias = new ArrayList<>();
        HashSet<Character> familias = new HashSet<>();
        for (Producto p : inventario) {
```
**Interpretación:** El acumulador suma existencias y las tres salidas permiten verificar dos artículos, ocho unidades y dos familias. Este paso forma parte de un archivo aún incompleto; termina los demás bloques antes de ejecutar.

### Paso 6: elaboración progresiva
**Necesidad:** El acumulador suma existencias y las tres salidas permiten verificar dos artículos, ocho unidades y dos familias.
**Lugar:** escribe estas líneas, en el orden indicado, en `src/Ej08.java` después del bloque anterior.
```java
            existencias.add(p.stock);
            familias.add(p.codigo.charAt(0));
        }
        int total = 0;
```
**Interpretación:** El acumulador suma existencias y las tres salidas permiten verificar dos artículos, ocho unidades y dos familias. Este paso forma parte de un archivo aún incompleto; termina los demás bloques antes de ejecutar.

### Paso 7: elaboración progresiva
**Necesidad:** El acumulador suma existencias y las tres salidas permiten verificar dos artículos, ocho unidades y dos familias.
**Lugar:** escribe estas líneas, en el orden indicado, en `src/Ej08.java` después del bloque anterior.
```java
        for (Integer n : existencias) {
            total += n;
        }
        System.out.println("Productos: " + inventario.size());
```
**Interpretación:** El acumulador suma existencias y las tres salidas permiten verificar dos artículos, ocho unidades y dos familias. Este paso forma parte de un archivo aún incompleto; termina los demás bloques antes de ejecutar.

### Paso 8: elaboración progresiva
**Necesidad:** El acumulador suma existencias y las tres salidas permiten verificar dos artículos, ocho unidades y dos familias.
**Lugar:** escribe estas líneas, en el orden indicado, en `src/Ej08.java` después del bloque anterior.
```java
        System.out.println("Unidades: " + total);
        System.out.println("Familias: " + familias.size());
    }
}
```
**Interpretación:** El acumulador suma existencias y las tres salidas permiten verificar dos artículos, ocho unidades y dos familias. Ahora el archivo puede compilarse y ejecutarse.

### Archivo completo para comprobación
```java
import java.util.ArrayList;
import java.util.HashSet;
public class Ej08 {
    static class Producto {
        String codigo;
        String descripcion;
        int stock;
        Producto(String codigo, String descripcion, int stock) {
            this.codigo = codigo;
            this.descripcion = descripcion;
            this.stock = stock;
        }
    }
    public static void main(String[] args) {
        ArrayList<Producto> inventario = new ArrayList<>();
        inventario.add(new Producto("A1", "Audífonos", 5));
        inventario.add(new Producto("B2", "Parlante", 3));
        ArrayList<Integer> existencias = new ArrayList<>();
        HashSet<Character> familias = new HashSet<>();
        for (Producto p : inventario) {
            existencias.add(p.stock);
            familias.add(p.codigo.charAt(0));
        }
        int total = 0;
        for (Integer n : existencias) {
            total += n;
        }
        System.out.println("Productos: " + inventario.size());
        System.out.println("Unidades: " + total);
        System.out.println("Familias: " + familias.size());
    }
}
```

**Predice antes de ejecutar:** ¿Por qué no es necesario conocer el orden de iteración del HashSet?
**Salida esperada:**
```text
Productos: 2
Unidades: 8
Familias: 2
```
**Extensión de razonamiento:** Agregar A3 / Webcam / 4 y justificar por qué familias sigue siendo 2.
**Tarea espejo T08:** Crear un inventario con productos A1/5, A2/7 y B1/3; usar una lista de existencias y un conjunto de letras de familia; mostrar productos, unidades y familias.
**Entrega:** archivo `T08.java`, captura de ejecución y explicación causal de 3–5 líneas.

## Cierre de la sesión
Explica por qué no se escribe ArrayList<int>, por qué HashSet.add puede devolver false y cómo una clase Producto se incorpora a ArrayList<Producto>.
## Rúbrica para cada tarea / 20 puntos
- Compilación y estructura: 4.
- Tipo y colección apropiados: 5.
- Operaciones y resultados: 6.
- Evidencia de prueba: 3.
- Explicación: 2.
