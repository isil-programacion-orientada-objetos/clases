---
course_id: JAVA-POO
session_id: S07
source_origin: PPT
status: validated
technology: Java 21
---

# Guía del estudiante — Programación Orientada a Objetos · Sesión 07

**Lideratec Academy · Laboratorio guiado | Clase nativa `String` y utilitarios `ProCadenas`**

## 1. Propósito de la sesión

Muchas aplicaciones trabajan con nombres, mensajes, identificadores y frases. Para interpretarlos sin errores hay que saber dónde empieza un carácter, cómo se encuentran fragmentos, cómo se reconstruye una cadena y qué operaciones regresan un valor distinto del original. Construiremos ejemplos ejecutables en Java y después los unificaremos en una aplicación de consola llamada `ProCadenas`. El enfoque no es memorizar métodos: es anticipar una salida, escribir decisiones pequeñas, ejecutarlas y explicar por qué cada decisión produce exactamente ese resultado.

## 2. Resultado observable — lectura inicial del docente

En esta sesión aprenderás a manipular cadenas de texto en Java, una habilidad necesaria para procesar entradas y presentar información. Comenzaremos con expresiones que permiten medir una cadena y obtener sus caracteres mediante índices. Después compararemos textos bajo criterios distintos y buscaremos palabras dentro de frases. Veremos cómo limpiar espacios extremos, cambiar mayúsculas y minúsculas, reemplazar caracteres y concatenar resultados sin asumir que el String original cambia por sí solo. Con estos conocimientos construiremos métodos reutilizables: uno para invertir caracteres, otro para contar repeticiones, otro para localizar una subcadena y otro para extraerla. También comprobaremos si una frase es palíndroma eliminando sus espacios y comparando el resultado con el texto invertido. Finalmente, conectaremos esos métodos en una pequeña aplicación con entrada por teclado. En cada práctica tendrás un ejercicio modelo resuelto y una tarea similar para trabajar sin copiar una solución. El objetivo es que puedas justificar índices, condiciones, recorridos y resultados, y que detectes por qué aparecen errores cuando un índice se sale de la cadena.

### Desempeños observables

- Interpretar índices y límites de `String` sin confundirse con su longitud.
- Escoger entre comparación, búsqueda, transformación y extracción según el problema.
- Construir, invocar y explicar métodos utilitarios de la clase `ProCadenas`.
- Realizar trazas de iteraciones y estados intermedios.
- Predecir, ejecutar y contrastar salidas con casos positivos y negativos.
- Detectar y corregir accesos fuera de rango.
- Integrar lectura de teclado y cinco utilitarios en un programa Java.

**Criterio de dominio:** no basta con mostrar una consola correcta. Debes poder explicar el índice inicial, el criterio de término del ciclo, los parámetros de cada método y qué sucede con entradas vacías o una subcadena ausente.

## 3. Antes de iniciar

**Debes saber:** crear una clase Java y un método `main`; declarar variables; diferenciar `String`, `char`, `int` y `boolean`; utilizar `if`, `for`, métodos estáticos y `System.out.println`.

**Debes tener:** JDK 21 compatible con la instalación de tu equipo, una terminal y, opcionalmente, IntelliJ IDEA o cualquier IDE Java que ya utilices. No son necesarios Maven, Gradle, dependencias externas, servidores ni conexiones a bases de datos.

**No se asumirá:** expresiones regulares, Unicode avanzado, `StringBuilder`, programación funcional ni paquetes de terceros. Para esta sesión, el recorrido con `charAt` corresponde a los caracteres `char` de Java; se utilizan ejemplos textuales simples.

## 4. Preparación del entorno

**Ruta A — ya tienes Java instalado:** abre una terminal, escribe `java -version` y luego `javac -version`. Ambos comandos deben responder sin «comando no reconocido». En este laboratorio se comprobó la ejecución con OpenJDK 21. Si ambos comandos funcionan, no reinstales el JDK.

**Ruta B — equipo sin preparar:** obtén un JDK 21 de un distribuidor oficial (por ejemplo, [Eclipse Temurin](https://adoptium.net/temurin/releases/?version=21)); elige tu sistema operativo y arquitectura, instala el JDK y abre una terminal nueva. Comprueba de nuevo `java -version` y `javac -version`. Si solo funciona `java`, revisa que instalaste un **JDK** y que la carpeta `bin` figura correctamente en el `PATH` o que tu IDE usa la ruta del JDK. No descargues bibliotecas adicionales.

**Crear la carpeta:** en tu equipo crea `S07_String_Java`; dentro guardarás los archivos `.java` con el nombre exacto de cada clase pública. En una terminal ubicada en la misma carpeta, ejecuta para cada ejemplo:

```bash
javac -encoding UTF-8 EJ01Basicos.java
java EJ01Basicos
```

Reemplaza los dos nombres por el archivo y la clase que correspondan a cada ejemplo. En Windows puedes abrir **Terminal** o la terminal integrada de IntelliJ IDEA; en el IDE crea un proyecto Java con JDK 21, una clase Java por archivo y usa la opción de ejecutar su `main`. Para EJ08 se compilan **dos** archivos juntos, como se indica allí. `-encoding UTF-8` permite que las cadenas acentuadas del material sean leídas correctamente.

**Primera prueba del entorno:** crea un archivo `Comprobacion.java` con `public class Comprobacion { public static void main(String[] args) { System.out.println("Java listo"); } }`, ejecútalo con `javac -encoding UTF-8 Comprobacion.java` y `java Comprobacion`. Debe imprimir `Java listo`. Si aparece «class ... is public, should be declared in a file named ...», iguala los nombres de clase y archivo; si aparece `ClassNotFoundException`, ejecuta desde la carpeta donde está el `.class`.

## 5. Convención de trabajo

Los ejemplos resueltos `EJ01`–`EJ08` desarrollan habilidades progresivas. Cada uno tiene una tarea `T01`–`T08`. Escribe primero los microbloques, revisa la explicación y **solo entonces** consulta el archivo completo situado al final del ejemplo. Las tareas deben resolverse sin pegar una solución; la guía entrega todos los requisitos, pistas y resultados que necesitas. Guarda evidencias de ejecución y una breve explicación del procedimiento.


---

# EJ01 — Índices, longitud y acceso a caracteres

**Fuente temática:** FUENTE (diapositivas 5–10).

**Qué vamos a construir:** Necesitamos leer un carácter de una cadena sin confundir su posición con su longitud.

**Qué aprenderás:** Distinguir un índice válido de uno inexistente y explicar el cálculo de la última posición.

**Archivo principal:** `EJ01Basicos.java`.

**Punto de partida:** crea un archivo con ese nombre en la carpeta de trabajo. Parte de la estructura de clase y `main` conocida; las partes funcionales se agregan progresivamente.


## Paso 1 — Abrir una clase y su punto de entrada

### Estado antes

No existe archivo fuente para este ejercicio.

### ¿Por qué necesitamos este paso?

Java ejecuta las instrucciones contenidas en main; el nombre público debe coincidir con el archivo.

### Escribe ahora


```java
public class EJ01Basicos {
    public static void main(String[] args) {
```

### Explicación detallada

La clase pública EJ01Basicos agrupa el ejercicio. `main` es el punto de entrada: `public` permite el acceso, `static` evita crear un objeto para ejecutarlo, `void` indica que no devuelve valor y `String[] args` representa argumentos opcionales.

**Elementos nuevos o recuperados:** EJ01Basicos, main, String[] args.

**Estado después:** Tenemos un contenedor compilable donde incorporar instrucciones; aún no produce salida.

**Por qué podemos avanzar:** Necesitamos una cadena concreta para medirla.


## Paso 2 — Guardar la cadena y medirla

### Estado antes

La clase no contiene aún datos.

### ¿Por qué necesitamos este paso?

Se requiere un objeto String y un entero donde conservar la longitud.

### Escribe ahora


```java
String texto = "Java";
int longitud = texto.length();
```

### Explicación detallada

Las comillas dobles crean un literal String. `texto` es la referencia a esa cadena. `length()` cuenta cuatro unidades `char` en este ejemplo; el resultado `int` se conserva en `longitud`. No confundir método `length()` con la propiedad de un arreglo.

**Elementos nuevos o recuperados:** texto (String), longitud (int), length().

**Estado después:** texto="Java"; longitud=4.

**Por qué podemos avanzar:** Conociendo el tamaño podemos calcular índices válidos.


## Paso 3 — Localizar el primer y último carácter

### Estado antes

Conocemos texto="Java" y longitud=4.

### ¿Por qué necesitamos este paso?

Los índices empiezan en cero y el último se encuentra en longitud menos uno.

### Escribe ahora


```java
char primero = texto.charAt(0);
char ultimo = texto.charAt(longitud - 1);
```

### Explicación detallada

`charAt(0)` devuelve J. `charAt(longitud - 1)` usa el índice 3 y devuelve a. `char` guarda una unidad de carácter individual; `charAt(4)` lanzaría `StringIndexOutOfBoundsException`.

**Elementos nuevos o recuperados:** primero, ultimo (char), charAt(int).

**Estado después:** primero=J; ultimo=a.

**Por qué podemos avanzar:** Debemos hacer observable el resultado mediante la consola.


## Paso 4 — Presentar los resultados

### Estado antes

Los tres valores ya están calculados.

### ¿Por qué necesitamos este paso?

La impresión confirma nuestras predicciones y permite detectar errores de índice.

### Escribe ahora


```java
System.out.println("Longitud: " + longitud);
System.out.println("Primero: " + primero);
System.out.println("Último: " + ultimo);
```

### Explicación detallada

`System.out.println` escribe una línea en consola; `+` concatena la etiqueta String con el valor de la variable. Los tres mensajes evidencian que los índices 0 y 3 son válidos. Finalmente se cierran los bloques con dos llaves `}`.

**Elementos nuevos o recuperados:** println, concatenación con +.

**Estado después:** La consola muestra longitud 4, J y a.

**Por qué podemos avanzar:** La salida permitirá contrastar predicción y ejecución.


## Traza manual o simulación

Índices de "Java": J→0, a→1, v→2, a→3. `length()`=4. El último índice válido es 4-1=3.

## Auditoría del artefacto construido

| Elemento | Qué hace / estado | Por qué existe |
|---|---|---|
| String texto | referencia a "Java" | tener una secuencia examinable |
| length() | retorna 4 | determinar la frontera de índices |
| charAt(0) | retorna J | acceder al inicio |
| charAt(longitud-1) | retorna a | acceder sin desbordarse |
| println | muestra la salida | verificar ejecución |


## Archivo completo al terminar el ejemplo


```java
public class EJ01Basicos {
    public static void main(String[] args) {
        String texto = "Java";
        int longitud = texto.length();
        char primero = texto.charAt(0);
        char ultimo = texto.charAt(longitud - 1);
        System.out.println("Longitud: " + longitud);
        System.out.println("Primero: " + primero);
        System.out.println("Último: " + ultimo);
    }
}
```


## Antes de ejecutar: predicción

1. ¿Qué número devuelve `length()`?
2. ¿Qué devuelve `charAt(3)`?
3. ¿Por qué `charAt(4)` es inválido?


## Ejecuta y valida


```bash
javac -encoding UTF-8 EJ01Basicos.java
java EJ01Basicos
```

**Resultado esperado:**


```text
Longitud: 4
Primero: J
Último: a
```

**Cómo interpretarlo:** Distinguir un índice válido de uno inexistente y explicar el cálculo de la última posición. El resultado demuestra las decisiones de los microbloques y debe coincidir con la predicción cuando los datos sean iguales.

**Variación A:** Cambia `"Java"` por `"POO"`; explica por qué la última posición cambia a 2.

**Error o caso límite controlado:** Sustituye temporalmente `longitud - 1` por `longitud` al acceder al último carácter; solo como prueba de depuración.

**Por qué ocurre:** El mayor índice legal es siempre uno menor que `length()` para una cadena no vacía.

**Corrección razonada:** Restaura `longitud - 1`; antes de llamar `charAt` con entrada libre, comprueba `texto.length() > 0`.

**Qué debes poder explicar con tus palabras:** la responsabilidad de cada variable, el criterio de inicio y término de cada ciclo, el significado del retorno y por qué el caso límite no debe sorprenderte.

## T01 — Tarea espejo: Último carácter de una palabra

**Enunciado:** Con `texto = "Código"`, muestra su longitud y último `char` mediante `length()` y `charAt()`. Antes de ejecutar, predice la última letra.

**Archivo que debes crear o modificar:** `T01UltimoCaracter.java`.

**Restricción:** Asegurar índice correcto con longitud-1; sin usar números mágicos.

**Pista:** `length()` de "Código" es 6.

**Evidencia:** captura o transcripción de la consola, archivo `.java` y explicación de dos decisiones técnicas.

**Cómo saber si está correcta:** Longitud: 6; Último: o

**Punto de partida sugerido (código completo de trabajo con TODO):**


```java
public class T01UltimoCaracter {
    public static void main(String[] args) {
        String texto = "Código";
        // TODO T01: calcula longitud y último carácter con String.
        System.out.println("PENDIENTE T01");
    }
}
```


**Cómo ejecutar tu tarea:** `javac -encoding UTF-8 T01UltimoCaracter.java` y `java T01UltimoCaracter`. Sustituye los TODO; el texto PENDIENTE es solo un marcador inicial.


---

# EJ02 — Comparación y búsqueda en cadenas

**Fuente temática:** FUENTE (diapositivas 7–9).

**Qué vamos a construir:** Comparar referencias y buscar fragmentos requiere distinguir igualdad exacta, igualdad sin distinguir mayúsculas y posición.

**Qué aprenderás:** Elegir métodos apropiados para comparación y búsqueda sin utilizar `==` para comparar contenido.

**Archivo principal:** `EJ02Comparacion.java`.

**Punto de partida:** crea un archivo con ese nombre en la carpeta de trabajo. Parte de la estructura de clase y `main` conocida; las partes funcionales se agregan progresivamente.


## Paso 1 — Definir las dos entradas

### Estado antes

Aún no hay cadenas comparables.

### ¿Por qué necesitamos este paso?

Para comparar contenido se necesitan dos Strings cuyas letras solo difieran por mayúsculas.

### Escribe ahora


```java
public class EJ02Comparacion {
    public static void main(String[] args) {
        String nombre = "Ana";
        String entrada = "ana";
```

### Explicación detallada

`nombre` y `entrada` son variables String. Mantienen las mismas letras, pero A/a difiere. Abrimos una clase y `main` con el mismo patrón conocido en EJ01.

**Elementos nuevos o recuperados:** nombre, entrada (String).

**Estado después:** nombre="Ana", entrada="ana".

**Por qué podemos avanzar:** La comparación debe elegir si distingue la capitalización.


## Paso 2 — Comparar con dos criterios

### Estado antes

Hay dos Strings disponibles.

### ¿Por qué necesitamos este paso?

Una verificación estricta y otra flexible responden a necesidades distintas.

### Escribe ahora


```java
boolean exacto = nombre.equals(entrada);
boolean flexible = nombre.equalsIgnoreCase(entrada);
```

### Explicación detallada

`equals` compara secuencias respetando mayúsculas: false. `equalsIgnoreCase` ignora diferencias de mayúsculas/minúsculas: true. `boolean` solo puede ser verdadero o falso; `==` no es la operación de comparación textual buscada.

**Elementos nuevos o recuperados:** boolean, equals(Object), equalsIgnoreCase(String).

**Estado después:** exacto=false y flexible=true.

**Por qué podemos avanzar:** Ahora queremos localizar partes de una cadena.


## Paso 3 — Buscar presencia y posición

### Estado antes

Se conoce nombre="Ana".

### ¿Por qué necesitamos este paso?

Presencia y ubicación no son la misma pregunta.

### Escribe ahora


```java
boolean contiene = nombre.contains("n");
int posicion = nombre.indexOf("na");
```

### Explicación detallada

`contains("n")` devuelve true porque la n existe. `indexOf("na")` devuelve la posición inicial 1; si la subcadena no existe, retorna -1. `contiene` es boolean mientras `posicion` es int.

**Elementos nuevos o recuperados:** contains(CharSequence), indexOf(String), posicion (int).

**Estado después:** contiene=true, posicion=1.

**Por qué podemos avanzar:** La consola permitirá comparar cuatro operaciones diferentes.


## Paso 4 — Imprimir y leer el diagnóstico

### Estado antes

Hay cuatro resultados en memoria.

### ¿Por qué necesitamos este paso?

Las etiquetas separan igualdad, presencia y posición.

### Escribe ahora


```java
System.out.println("Exacto: " + exacto);
System.out.println("Sin distinguir mayúsculas: " + flexible);
System.out.println("Contiene n: " + contiene);
System.out.println("Posición de na: " + posicion);
```

### Explicación detallada

Cada `println` muestra una variable previamente calculada. Los resultados `false`, `true`, `true`, `1` proceden de decisiones diferentes; cierra los dos bloques abiertos.

**Elementos nuevos o recuperados:** etiquetas de salida.

**Estado después:** Aparecen cuatro líneas con resultados diferenciados.

**Por qué podemos avanzar:** La distinción guiará las tareas de búsqueda del estudiante.


## Traza manual o simulación

En "Ana", `n` ocupa el índice 1 y `na` comienza en 1. "Ana" no es igual exactamente a "ana", aunque sí lo es ignorando mayúsculas.

## Auditoría del artefacto construido

| Elemento | Qué hace / estado | Por qué existe |
|---|---|---|
| equals | false | distingue capitalización |
| equalsIgnoreCase | true | comparación flexible |
| contains | true | prueba presencia |
| indexOf | 1 | ubica inicio o -1 |


## Archivo completo al terminar el ejemplo


```java
public class EJ02Comparacion {
    public static void main(String[] args) {
        String nombre = "Ana";
        String entrada = "ana";
        boolean exacto = nombre.equals(entrada);
        boolean flexible = nombre.equalsIgnoreCase(entrada);
        boolean contiene = nombre.contains("n");
        int posicion = nombre.indexOf("na");
        System.out.println("Exacto: " + exacto);
        System.out.println("Sin distinguir mayúsculas: " + flexible);
        System.out.println("Contiene n: " + contiene);
        System.out.println("Posición de na: " + posicion);
    }
}
```


## Antes de ejecutar: predicción

1. ¿`equals` devuelve true o false?
2. ¿Cuál método devuelve -1 cuando no encuentra una secuencia?


## Ejecuta y valida


```bash
javac -encoding UTF-8 EJ02Comparacion.java
java EJ02Comparacion
```

**Resultado esperado:**


```text
Exacto: false
Sin distinguir mayúsculas: true
Contiene n: true
Posición de na: 1
```

**Cómo interpretarlo:** Elegir métodos apropiados para comparación y búsqueda sin utilizar `==` para comparar contenido. El resultado demuestra las decisiones de los microbloques y debe coincidir con la predicción cuando los datos sean iguales.

**Variación A:** Reemplaza la búsqueda `"na"` por `"xy"`; `indexOf` debe ser -1 sin ocasionar excepción.

**Error o caso límite controlado:** Confundir `indexOf` con `contains` y usar su entero como si fuese boolean.

**Por qué ocurre:** El primero retorna int y el segundo boolean; responden preguntas diferentes.

**Corrección razonada:** Usar `indexOf(...) >= 0` si necesitas una condición, o `contains` si solo necesitas presencia.

**Qué debes poder explicar con tus palabras:** la responsabilidad de cada variable, el criterio de inicio y término de cada ciclo, el significado del retorno y por qué el caso límite no debe sorprenderte.

## T02 — Tarea espejo: Validación de un texto de curso

**Enunciado:** Con `"Curso Java"` demuestra igualdad ignorando mayúsculas frente a `"curso java"`, presencia de `"Java"` y posición de `"SQL"`.

**Archivo que debes crear o modificar:** `T02ValidacionTexto.java`.

**Restricción:** No reemplazar `indexOf` por una búsqueda de texto exacta; explicar el caso -1.

**Pista:** Una subcadena inexistente produce -1, no cero.

**Evidencia:** captura o transcripción de la consola, archivo `.java` y explicación de dos decisiones técnicas.

**Cómo saber si está correcta:** Coincide: true; Contiene Java: true; Posición SQL: -1

**Punto de partida sugerido (código completo de trabajo con TODO):**


```java
public class T02ValidacionTexto {
    public static void main(String[] args) {
        String nombre = "Curso Java";
        // TODO T02: compara, busca presencia y localiza una subcadena ausente.
        System.out.println("PENDIENTE T02");
    }
}
```


**Cómo ejecutar tu tarea:** `javac -encoding UTF-8 T02ValidacionTexto.java` y `java T02ValidacionTexto`. Sustituye los TODO; el texto PENDIENTE es solo un marcador inicial.


---

# EJ03 — Limpieza y transformación de texto

**Fuente temática:** FUENTE (diapositivas 9–10).

**Qué vamos a construir:** Una entrada de usuario puede contener espacios exteriores o un formato inconsistente; necesitamos generar una etiqueta sin alterar el valor original.

**Qué aprenderás:** Encadenar transformaciones de String comprendiendo que cada operación retorna una nueva cadena.

**Archivo principal:** `EJ03Transformacion.java`.

**Punto de partida:** crea un archivo con ese nombre en la carpeta de trabajo. Parte de la estructura de clase y `main` conocida; las partes funcionales se agregan progresivamente.


## Paso 1 — Conservar la fuente de datos

### Estado antes

No existe texto de entrada.

### ¿Por qué necesitamos este paso?

La evidencia debe permitir comparar el antes y el después.

### Escribe ahora


```java
public class EJ03Transformacion {
    public static void main(String[] args) {
        String original = "  Java Basico  ";
```

### Explicación detallada

`original` contiene dos espacios al inicio y dos al final. Al conservarlo sin modificar, podemos verificar que cada operación crea otro resultado: String es inmutable.

**Elementos nuevos o recuperados:** original (String), inmutabilidad.

**Estado después:** original guarda exactamente los blancos y letras.

**Por qué podemos avanzar:** Antes de transformar necesitamos eliminar espacios externos.


## Paso 2 — Eliminar espacios externos y normalizar caja

### Estado antes

original="  Java Basico  ".

### ¿Por qué necesitamos este paso?

Limpiar exteriores y normalizar mayúsculas son operaciones distintas.

### Escribe ahora


```java
String limpio = original.trim();
String mayusculas = limpio.toUpperCase();
```

### Explicación detallada

`trim()` retira los espacios iniciales y finales, no los interiores. `toUpperCase()` genera "JAVA BASICO". La variable `original` sigue con sus espacios: reasignamos resultados a nuevas referencias en lugar de modificar el objeto original.

**Elementos nuevos o recuperados:** limpio, mayusculas, trim(), toUpperCase().

**Estado después:** limpio="Java Basico", mayusculas="JAVA BASICO".

**Por qué podemos avanzar:** Para usar la cadena como identificador debemos tratar el espacio interno.


## Paso 3 — Reemplazar el separador y añadir sufijo

### Estado antes

mayusculas="JAVA BASICO".

### ¿Por qué necesitamos este paso?

Ahora el espacio del medio debe convertirse en guion bajo y se agregará un sufijo.

### Escribe ahora


```java
String codigo = mayusculas.replace(' ', '_');
String etiqueta = codigo.concat("_21");
```

### Explicación detallada

`replace(char,char)` cambia todas las apariciones del carácter espacio por `_`. Las comillas simples indican `char` y las dobles delimitan un String. `concat("_21")` añade el sufijo al final y devuelve la etiqueta final.

**Elementos nuevos o recuperados:** codigo, etiqueta, replace(char,char), concat(String).

**Estado después:** codigo="JAVA_BASICO" y etiqueta="JAVA_BASICO_21".

**Por qué podemos avanzar:** La salida comparativa evidencia que el original no cambió.


## Paso 4 — Contrastar estado original y final

### Estado antes

Existe original sin tocar y etiqueta transformada.

### ¿Por qué necesitamos este paso?

Imprimir dos valores permite verificar inmutabilidad.

### Escribe ahora


```java
System.out.println("Original: [" + original + "]");
System.out.println("Resultado: " + etiqueta);
```

### Explicación detallada

Los corchetes visualizan espacios que serían difíciles de detectar. La etiqueta final muestra solo la transformación deseada. Cerramos `main` y la clase con `}`.

**Elementos nuevos o recuperados:** corchetes de diagnóstico.

**Estado después:** La consola evidencia dos estados diferentes.

**Por qué podemos avanzar:** Podemos interpretar por qué la secuencia de operaciones importa.


## Traza manual o simulación

Antes: [··Java·Basico··] (·=espacio). Después de trim: [Java·Basico]. Después de mayúsculas: [JAVA·BASICO]. Después de replace: [JAVA_BASICO]. Después de concat: [JAVA_BASICO_21].

## Auditoría del artefacto construido

| Elemento | Qué hace / estado | Por qué existe |
|---|---|---|
| trim | retira espacios extremos | normaliza entrada |
| toUpperCase | normaliza capitalización | formato consistente |
| replace | cambia separador interior | crear etiqueta |
| concat | añade sufijo | identificación |
| original | sin cambios | demostrar inmutabilidad |


## Archivo completo al terminar el ejemplo


```java
public class EJ03Transformacion {
    public static void main(String[] args) {
        String original = "  Java Basico  ";
        String limpio = original.trim();
        String mayusculas = limpio.toUpperCase();
        String codigo = mayusculas.replace(' ', '_');
        String etiqueta = codigo.concat("_21");
        System.out.println("Original: [" + original + "]");
        System.out.println("Resultado: " + etiqueta);
    }
}
```


## Antes de ejecutar: predicción

1. ¿Qué espacios elimina trim?
2. ¿Qué valor tiene original al final?
3. ¿Qué cambia al invertir el orden de trim y replace?


## Ejecuta y valida


```bash
javac -encoding UTF-8 EJ03Transformacion.java
java EJ03Transformacion
```

**Resultado esperado:**


```text
Original: [  Java Basico  ]
Resultado: JAVA_BASICO_21
```

**Cómo interpretarlo:** Encadenar transformaciones de String comprendiendo que cada operación retorna una nueva cadena. El resultado demuestra las decisiones de los microbloques y debe coincidir con la predicción cuando los datos sean iguales.

**Variación A:** Sustituye `toUpperCase()` por `toLowerCase()` y predice `java_basico_21`.

**Error o caso límite controlado:** Suponer que `original.trim();` modifica `original` sin capturar el retorno.

**Por qué ocurre:** `String` no es mutable; se necesita asignar el String devuelto.

**Corrección razonada:** Usa `String limpio = original.trim();` (como en el ejemplo), o `original = original.trim();` si decidiste reemplazar la referencia.

**Qué debes poder explicar con tus palabras:** la responsabilidad de cada variable, el criterio de inicio y término de cada ciclo, el significado del retorno y por qué el caso límite no debe sorprenderte.

## T03 — Tarea espejo: Código normalizado de un curso

**Enunciado:** Dado `"  Curso de Java  "`, elimina espacios extremos, pasa a minúsculas, cambia espacios internos por guiones y agrega `"-poo"`. Imprime original y etiqueta.

**Archivo que debes crear o modificar:** `T03Normalizar.java`.

**Restricción:** Usar métodos de la sesión, sin modificar el literal original.

**Pista:** La etiqueta queda en minúsculas y sin espacios internos.

**Evidencia:** captura o transcripción de la consola, archivo `.java` y explicación de dos decisiones técnicas.

**Cómo saber si está correcta:** Etiqueta: curso-de-java-poo

**Punto de partida sugerido (código completo de trabajo con TODO):**


```java
public class T03Normalizar {
    public static void main(String[] args) {
        String original = "  Curso de Java  ";
        // TODO T03: realiza cuatro transformaciones conservando original.
        System.out.println("PENDIENTE T03");
    }
}
```


**Cómo ejecutar tu tarea:** `javac -encoding UTF-8 T03Normalizar.java` y `java T03Normalizar`. Sustituye los TODO; el texto PENDIENTE es solo un marcador inicial.


---

# EJ04 — Invertir una cadena mediante índices

**Fuente temática:** FUENTE (diapositiva 13).

**Qué vamos a construir:** Invertir un texto exige leer los caracteres de derecha a izquierda y conservar cada avance en un acumulador.

**Qué aprenderás:** Crear un método utilitario con un bucle descendente, retorno String y traza verificable.

**Archivo principal:** `EJ04Invertir.java`.

**Punto de partida:** crea un archivo con ese nombre en la carpeta de trabajo. Parte de la estructura de clase y `main` conocida; las partes funcionales se agregan progresivamente.


## Paso 1 — Definir responsabilidad y firma del método

### Estado antes

No existe función para invertir la cadena.

### ¿Por qué necesitamos este paso?

Una clase contiene el utilitario que recibirá un String y devolverá otro String invertido.

### Escribe ahora


```java
public class EJ04Invertir {
    public static String invierteCadena(String cadena) {
```

### Explicación detallada

`invierteCadena` es un método estático: se llama sin construir un objeto. Retorna `String`, acepta un parámetro String `cadena` y su firma delimita qué operación ofrece.

**Elementos nuevos o recuperados:** método invierteCadena(String), parámetro cadena, static.

**Estado después:** Queda declarada la operación que debe devolver un String.

**Por qué podemos avanzar:** Necesitamos una variable donde reunir caracteres invertidos.


## Paso 2 — Inicializar acumulador y recorrido descendente

### Estado antes

cadena="POO Java" (8 caracteres).

### ¿Por qué necesitamos este paso?

El carácter final debe copiarse primero.

### Escribe ahora


```java
String invertida = "";
for (int indice = cadena.length() - 1; indice >= 0; indice--) {
```

### Explicación detallada

`invertida` comienza vacía. `indice` inicia en `length()-1`, continúa mientras `indice >= 0` y disminuye con `indice--`; así cubre índices válidos en orden inverso y finaliza cuando vale -1. `for` controla el recorrido y evita perder el primer carácter.

**Elementos nuevos o recuperados:** invertida (String), indice (int), for, --.

**Estado después:** invertida="" e indice inicial 7.

**Por qué podemos avanzar:** Cada iteración debe añadir el carácter actual.


## Paso 3 — Acumular y devolver

### Estado antes

invertida="".

### ¿Por qué necesitamos este paso?

Sin acumular no tendríamos una secuencia invertida.

### Escribe ahora


```java
invertida += cadena.charAt(indice);
}
return invertida;
}
```

### Explicación detallada

`charAt(indice)` recupera el carácter actual. `+=` equivale a concatenar el contenido previo con ese carácter. La llave cierra el `for`; `return invertida` entrega el valor al llamador y la última llave cierra el método. Este patrón es didáctico para cadenas cortas.

**Elementos nuevos o recuperados:** +=, return.

**Estado después:** Al terminar, invertida="avaJ OOP".

**Por qué podemos avanzar:** Para observar el valor debemos invocar el utilitario desde main.


## Paso 4 — Llamar al método desde main

### Estado antes

El método existe pero no ha sido invocado.

### ¿Por qué necesitamos este paso?

La invocación confirma que la firma y el algoritmo funcionan juntos.

### Escribe ahora


```java
public static void main(String[] args) {
    System.out.println(invierteCadena("POO Java"));
```

### Explicación detallada

`main` realiza una llamada al método estático y pasa el literal como argumento. `println` muestra el String devuelto. Se cierran las llaves de main y de la clase.

**Elementos nuevos o recuperados:** llamada con argumento, valor de retorno.

**Estado después:** Aparece avaJ OOP en consola.

**Por qué podemos avanzar:** La traza prueba que el orden de índices fue correcto.


## Traza manual o simulación

Traza corta con "SOL": indice 2→L, acumulado "L"; indice 1→O, acumulado "LO"; indice 0→S, acumulado "LOS"; siguiente indice=-1 termina.

## Auditoría del artefacto construido

| Elemento | Qué hace / estado | Por qué existe |
|---|---|---|
| firma y parámetro | recibe la cadena | permitir reutilización |
| acumulador vacío | guarda el resultado parcial | preservar caracteres |
| for descendente | visita 7...0 | invertir orden |
| charAt + += | anexa carácter actual | producir salida |
| return | entrega String | hacer observable el método |
| main | llama al utilitario | ejecutar demostración |


## Archivo completo al terminar el ejemplo


```java
public class EJ04Invertir {
    public static String invierteCadena(String cadena) {
        String invertida = "";
        for (int indice = cadena.length() - 1; indice >= 0; indice--) {
            invertida += cadena.charAt(indice);
        }
        return invertida;
    }
    public static void main(String[] args) {
        System.out.println(invierteCadena("POO Java"));
    }
}
```


## Antes de ejecutar: predicción

1. ¿En qué índice comienza el for?
2. ¿Qué contiene invertida después de dos iteraciones?
3. ¿Qué sucede si la cadena es vacía?


## Ejecuta y valida


```bash
javac -encoding UTF-8 EJ04Invertir.java
java EJ04Invertir
```

**Resultado esperado:**


```text
avaJ OOP
```

**Cómo interpretarlo:** Crear un método utilitario con un bucle descendente, retorno String y traza verificable. El resultado demuestra las decisiones de los microbloques y debe coincidir con la predicción cuando los datos sean iguales.

**Variación A:** Usa `"RADAR"`; el resultado coincide con la entrada, aunque se haya recorrido inversamente.

**Error o caso límite controlado:** Modificar la condición `indice >= 0` por `indice > 0`.

**Por qué ocurre:** El índice cero ya no se visita y se pierde el primer carácter.

**Corrección razonada:** Restaurar `indice >= 0`; comprobar la traza con "SOL".

**Qué debes poder explicar con tus palabras:** la responsabilidad de cada variable, el criterio de inicio y término de cada ciclo, el significado del retorno y por qué el caso límite no debe sorprenderte.

## T04 — Tarea espejo: Invertir una cadena con números y espacios

**Enunciado:** Implementa `invierteCadena(String cadena)` para invertir `"Java 21"`; llama al método desde `main`.

**Archivo que debes crear o modificar:** `T04InvertirTexto.java`.

**Restricción:** El recorrido debe incluir el índice cero; no usar métodos externos de inversión.

**Pista:** Cadena invertida correcta con el espacio preservado.

**Evidencia:** captura o transcripción de la consola, archivo `.java` y explicación de dos decisiones técnicas.

**Cómo saber si está correcta:** 12 avaJ

**Punto de partida sugerido (código completo de trabajo con TODO):**


```java
public class T04InvertirTexto {
    public static String invierteCadena(String cadena) {
        // TODO T04: crea acumulador, for descendente y return.
        return "PENDIENTE T04";
    }
    public static void main(String[] args) {
        System.out.println(invierteCadena("Java 21"));
    }
}
```


**Cómo ejecutar tu tarea:** `javac -encoding UTF-8 T04InvertirTexto.java` y `java T04InvertirTexto`. Sustituye los TODO; el texto PENDIENTE es solo un marcador inicial.


---

# EJ05 — Contar ocurrencias de un carácter

**Fuente temática:** FUENTE (diapositiva 14).

**Qué vamos a construir:** Necesitamos conocer cuántas veces aparece un carácter específico y evitar contar otros parecidos.

**Qué aprenderás:** Construir un contador con `for`, `if`, comparación `char` y resultado `int`.

**Archivo principal:** `EJ05Contar.java`.

**Punto de partida:** crea un archivo con ese nombre en la carpeta de trabajo. Parte de la estructura de clase y `main` conocida; las partes funcionales se agregan progresivamente.


## Paso 1 — Declarar una operación que devuelve un entero

### Estado antes

No existe procedimiento de conteo.

### ¿Por qué necesitamos este paso?

El conteo necesita la cadena y el carácter buscado.

### Escribe ahora


```java
public class EJ05Contar {
    public static int cuentaOcurrenciasCaracter(String cadena, char caracter) {
```

### Explicación detallada

La firma devuelve `int`, porque el número de coincidencias es un entero. `String cadena` es la secuencia observada y `char caracter` es el objetivo, escrito con comillas simples al invocar.

**Elementos nuevos o recuperados:** cuentaOcurrenciasCaracter, caracter (char).

**Estado después:** Se define contrato de entrada y retorno.

**Por qué podemos avanzar:** Necesitamos iniciar un contador y visitar cada posición.


## Paso 2 — Preparar contador y recorrido ascendente

### Estado antes

total no existe y no se han visitado caracteres.

### ¿Por qué necesitamos este paso?

La operación debe inspeccionar desde el índice cero hasta el anterior a length.

### Escribe ahora


```java
int total = 0;
for (int i = 0; i < cadena.length(); i++) {
```

### Explicación detallada

`total=0` evita un resultado indeterminado; `i=0` comienza en la primera posición, `i < length()` impide desbordes e `i++` avanza uno. Si la cadena está vacía, el bucle no inicia y el resultado queda cero.

**Elementos nuevos o recuperados:** total (int), i (int), ++.

**Estado después:** total=0 e i inicial=0.

**Por qué podemos avanzar:** Cada posición debe compararse con el carácter buscado.


## Paso 3 — Incrementar únicamente cuando coincide

### Estado antes

El contador comienza en 0.

### ¿Por qué necesitamos este paso?

Un carácter diferente no debe sumarse.

### Escribe ahora


```java
if (cadena.charAt(i) == caracter) {
    total++;
}
}
return total;
}
```

### Explicación detallada

`charAt(i)` obtiene el `char` actual y `==` compara dos `char`; si coinciden, `total++` suma uno. Las llaves cierran primero el if y luego el for. `return total` entrega el conteo. El método finaliza cuando el índice alcanza la longitud.

**Elementos nuevos o recuperados:** if, == para char, total++.

**Estado después:** Al revisar 13 posiciones, total=5.

**Por qué podemos avanzar:** La llamada externa debe mostrar el conteo.


## Paso 4 — Invocar el contador

### Estado antes

La operación está definida.

### ¿Por qué necesitamos este paso?

La salida permite contrastar el número previsto.

### Escribe ahora


```java
public static void main(String[] args) {
    System.out.println(cuentaOcurrenciasCaracter("casa amarilla", 'a'));
```

### Explicación detallada

Se pasa una cadena y el literal `char` a. La consola recibe un `int` que representa coincidencias exactas; A mayúscula no contaría como a minúscula.

**Elementos nuevos o recuperados:** argumentos String y char.

**Estado después:** Con la entrada de ejemplo imprime 5.

**Por qué podemos avanzar:** Ahora podemos discutir si debe distinguir mayúsculas.


## Traza manual o simulación

Traza de "casa": índices 0(c) total0, 1(a) total1, 2(s) total1, 3(a) total2. En " amarilla" se suman otras tres a; resultado global 5.

## Auditoría del artefacto construido

| Elemento | Qué hace / estado | Por qué existe |
|---|---|---|
| int total=0 | inicia conteo | base correcta |
| for | visita cada índice | inspección completa |
| if/== | filtra coincidencias exactas | no contar caracteres ajenos |
| total++ | suma una coincidencia | estado acumulado |
| return | devuelve entero | usar salida en main |


## Archivo completo al terminar el ejemplo


```java
public class EJ05Contar {
    public static int cuentaOcurrenciasCaracter(String cadena, char caracter) {
        int total = 0;
        for (int i = 0; i < cadena.length(); i++) {
            if (cadena.charAt(i) == caracter) {
                total++;
            }
        }
        return total;
    }
    public static void main(String[] args) {
        System.out.println(cuentaOcurrenciasCaracter("casa amarilla", 'a'));
    }
}
```


## Antes de ejecutar: predicción

1. ¿El espacio suma al buscar a?
2. ¿El resultado se afecta por una A mayúscula?
3. ¿Qué ocurre con cadena vacía?


## Ejecuta y valida


```bash
javac -encoding UTF-8 EJ05Contar.java
java EJ05Contar
```

**Resultado esperado:**


```text
5
```

**Cómo interpretarlo:** Construir un contador con `for`, `if`, comparación `char` y resultado `int`. El resultado demuestra las decisiones de los microbloques y debe coincidir con la predicción cuando los datos sean iguales.

**Variación A:** Cambia el carácter buscado por `"l"` y predice 2.

**Error o caso límite controlado:** Escribir `i <= cadena.length()` en el encabezado del for.

**Por qué ocurre:** Al igualar la longitud se solicita un índice fuera del rango.

**Corrección razonada:** Usar `i < cadena.length()` y verificar que el primer índice es 0.

**Qué debes poder explicar con tus palabras:** la responsabilidad de cada variable, el criterio de inicio y término de cada ciclo, el significado del retorno y por qué el caso límite no debe sorprenderte.

## T05 — Tarea espejo: Contar letras en un término

**Enunciado:** Implementa `cuentaOcurrenciasCaracter` para contar `a` en `"programacion"`. Explica por qué el resultado es 2.

**Archivo que debes crear o modificar:** `T05ContarLetras.java`.

**Restricción:** No usar `indexOf` como contador único: solo devuelve una posición.

**Pista:** Conteo exacto de a en la cadena.

**Evidencia:** captura o transcripción de la consola, archivo `.java` y explicación de dos decisiones técnicas.

**Cómo saber si está correcta:** 2

**Punto de partida sugerido (código completo de trabajo con TODO):**


```java
public class T05ContarLetras {
    public static int cuentaOcurrenciasCaracter(String cadena, char caracter) {
        // TODO T05: for, if, contador y return.
        return -1;
    }
    public static void main(String[] args) {
        System.out.println(cuentaOcurrenciasCaracter("programacion", 'a'));
    }
}
```


**Cómo ejecutar tu tarea:** `javac -encoding UTF-8 T05ContarLetras.java` y `java T05ContarLetras`. Sustituye los TODO; el texto PENDIENTE es solo un marcador inicial.


---

# EJ06 — Buscar y extraer una subcadena

**Fuente temática:** FUENTE (diapositivas 15–16).

**Qué vamos a construir:** Para extraer un fragmento primero debemos conocer dónde comienza y cuántos caracteres necesitamos.

**Qué aprenderás:** Combinar `indexOf` con `substring(inicio, finExclusivo)` y comprobar la búsqueda antes de extraer.

**Archivo principal:** `EJ06BuscarExtraer.java`.

**Punto de partida:** crea un archivo con ese nombre en la carpeta de trabajo. Parte de la estructura de clase y `main` conocida; las partes funcionales se agregan progresivamente.


## Paso 1 — Crear el método de búsqueda

### Estado antes

No existe búsqueda reutilizable.

### ¿Por qué necesitamos este paso?

Se requiere recuperar la posición inicial de una palabra buscada.

### Escribe ahora


```java
public class EJ06BuscarExtraer {
    public static int posicionSubcadena(String cadena, String subcadena) {
        return cadena.indexOf(subcadena);
    }
```

### Explicación detallada

`posicionSubcadena` recibe cadena principal y subcadena, ambas String. `indexOf` retorna el índice de la primera coincidencia o -1. El `return` entrega ese entero; no modificamos la entrada.

**Elementos nuevos o recuperados:** posicionSubcadena, subcadena (String).

**Estado después:** Hay una operación que entrega índices o -1.

**Por qué podemos avanzar:** Para recuperar una parte necesitamos también una función de extracción.


## Paso 2 — Crear extracción con longitud

### Estado antes

Solo sabemos ubicar una subcadena.

### ¿Por qué necesitamos este paso?

`substring` pide una frontera final exclusiva, no una cantidad.

### Escribe ahora


```java
public static String extraeSubcadena(String cadena, int inicio, int cantidad) {
    return cadena.substring(inicio, inicio + cantidad);
}
```

### Explicación detallada

`inicio` es el índice inicial y `cantidad` es el número de caracteres deseado. El segundo argumento `inicio + cantidad` es exclusivo: substring(6,10) contiene índices 6,7,8,9. Si se supera `length()` lanza una excepción.

**Elementos nuevos o recuperados:** extraeSubcadena, inicio, cantidad, substring(int,int).

**Estado después:** También podemos extraer un String de longitud determinada.

**Por qué podemos avanzar:** Necesitamos un caso real y una condición que descarte búsquedas fallidas.


## Paso 3 — Buscar antes de extraer

### Estado antes

Los dos métodos existen pero no se han invocado.

### ¿Por qué necesitamos este paso?

Sin verificar -1 podríamos intentar iniciar substring en un índice inválido.

### Escribe ahora


```java
public static void main(String[] args) {
    String frase = "Anita lava la tina";
    int posicion = posicionSubcadena(frase, "lava");
    if (posicion >= 0) {
```

### Explicación detallada

`main` define la frase y busca "lava". La primera coincidencia empieza en el índice 6. La condición `>=0` protege contra el caso donde `indexOf` retorna -1.

**Elementos nuevos o recuperados:** frase, posicion, if >= 0.

**Estado después:** frase disponible, posicion=6 y condición verdadera.

**Por qué podemos avanzar:** Ahora el índice es seguro para extraer cuatro caracteres.


## Paso 4 — Mostrar la posición y el fragmento

### Estado antes

La búsqueda encontró posición 6.

### ¿Por qué necesitamos este paso?

Un caso completo necesita mostrar tanto índice como texto extraído.

### Escribe ahora


```java
System.out.println("Posición: " + posicion);
System.out.println("Extraída: " + extraeSubcadena(frase, posicion, 4));
}
```

### Explicación detallada

El primer println confirma el índice y el segundo muestra `substring(6,10)` que retorna lava. La última llave del fragmento cierra if; después se cierran main y la clase.

**Elementos nuevos o recuperados:** invocación combinada.

**Estado después:** Se muestran posición=6 y Extraída=lava.

**Por qué podemos avanzar:** Podemos verificar límites y la diferencia entre fin exclusivo y cantidad.


## Traza manual o simulación

"Anita lava la tina": A0 n1 i2 t3 a4 espacio5 l6 a7 v8 a9. 

`indexOf("lava")=6`; `substring(6,6+4)=substring(6,10)="lava"`. El índice 10 NO se incluye.

## Auditoría del artefacto construido

| Elemento | Qué hace / estado | Por qué existe |
|---|---|---|
| indexOf | 6 | localizar comienzo |
| inicio+cantidad | 10 | calcular límite final exclusivo |
| substring | lava | extraer exactamente 4 caracteres |
| if >=0 | evita -1 | prevenir extracción imposible |


## Archivo completo al terminar el ejemplo


```java
public class EJ06BuscarExtraer {
    public static int posicionSubcadena(String cadena, String subcadena) {
        return cadena.indexOf(subcadena);
    }
    public static String extraeSubcadena(String cadena, int inicio, int cantidad) {
        return cadena.substring(inicio, inicio + cantidad);
    }
    public static void main(String[] args) {
        String frase = "Anita lava la tina";
        int posicion = posicionSubcadena(frase, "lava");
        if (posicion >= 0) {
            System.out.println("Posición: " + posicion);
            System.out.println("Extraída: " + extraeSubcadena(frase, posicion, 4));
        }
    }
}
```


## Antes de ejecutar: predicción

1. ¿Qué devuelve indexOf de una palabra ausente?
2. ¿substring(6,10) incluye índice 10?
3. ¿Por qué la comprobación es previa?


## Ejecuta y valida


```bash
javac -encoding UTF-8 EJ06BuscarExtraer.java
java EJ06BuscarExtraer
```

**Resultado esperado:**


```text
Posición: 6
Extraída: lava
```

**Cómo interpretarlo:** Combinar `indexOf` con `substring(inicio, finExclusivo)` y comprobar la búsqueda antes de extraer. El resultado demuestra las decisiones de los microbloques y debe coincidir con la predicción cuando los datos sean iguales.

**Variación A:** Cambia el texto buscado a `"tina"` (posición 14) y la cantidad a 4.

**Error o caso límite controlado:** Buscar `"SQL"` y pasar -1 directamente a substring.

**Por qué ocurre:** La búsqueda fallida no es índice válido; substring produciría una excepción.

**Corrección razonada:** Conservar la guarda de `posicion>=0`; comprobar además `inicio>=0` y `inicio+cantidad<=length()` ante cantidades variables.

**Qué debes poder explicar con tus palabras:** la responsabilidad de cada variable, el criterio de inicio y término de cada ciclo, el significado del retorno y por qué el caso límite no debe sorprenderte.

## T06 — Tarea espejo: Extracción segura de una palabra

**Enunciado:** En `"Aprender Java es util"`, busca `"Java"`, muestra posición y extrae exactamente 4 caracteres. Si no aparece, muestra `"No encontrado"` en lugar de extraer.

**Archivo que debes crear o modificar:** `T06ExtraerSeguro.java`.

**Restricción:** No escribir el índice a mano; deducirlo mediante indexOf.

**Pista:** Posición e intervalo calculados por el programa.

**Evidencia:** captura o transcripción de la consola, archivo `.java` y explicación de dos decisiones técnicas.

**Cómo saber si está correcta:** Posición: 9; Texto: Java

**Punto de partida sugerido (código completo de trabajo con TODO):**


```java
public class T06ExtraerSeguro {
    public static void main(String[] args) {
        String frase = "Aprender Java es util";
        String buscada = "Java";
        // TODO T06: indexOf, guardia >=0, substring y salida.
        System.out.println("PENDIENTE T06");
    }
}
```


**Cómo ejecutar tu tarea:** `javac -encoding UTF-8 T06ExtraerSeguro.java` y `java T06ExtraerSeguro`. Sustituye los TODO; el texto PENDIENTE es solo un marcador inicial.


---

# EJ07 — Identificar palíndromos ignorando espacios

**Fuente temática:** FUENTE (diapositiva 17).

**Qué vamos a construir:** Para evaluar un palíndromo con espacios primero debemos compararlo consigo mismo invertido bajo reglas equivalentes.

**Qué aprenderás:** Eliminar únicamente el espacio ordinario, invertir y comparar sin distinguir mayúsculas.

**Archivo principal:** `EJ07Palindromo.java`.

**Punto de partida:** crea un archivo con ese nombre en la carpeta de trabajo. Parte de la estructura de clase y `main` conocida; las partes funcionales se agregan progresivamente.


## Paso 1 — Reutilizar inversión ya aprendida

### Estado antes

El ejemplo necesita inversión, disponible como habilidad previa.

### ¿Por qué necesitamos este paso?

Para comparar las direcciones necesitamos el mismo método de inversión del EJ04.

### Escribe ahora


```java
public class EJ07Palindromo {
    public static String invierteCadena(String cadena) {
        String invertida = "";
        for (int i = cadena.length() - 1; i >= 0; i--) {
            invertida += cadena.charAt(i);
        }
        return invertida;
    }
```

### Explicación detallada

Es exactamente el patrón del EJ04: acumulador String vacío, recorrido descendente desde length()-1 hasta cero, concatenación y return. La diferencia es únicamente que usamos `i` como variable de control. No se crea lógica nueva.

**Elementos nuevos o recuperados:** reutilización de método conocido.

**Estado después:** Hay un método invierteCadena reutilizable.

**Por qué podemos avanzar:** Aún necesitamos normalizar los espacios antes de comparar.


## Paso 2 — Definir regla y acumulador de limpieza

### Estado antes

cadena aún incluye espacios.

### ¿Por qué necesitamos este paso?

La PPT pide ignorar los espacios contenidos en una frase.

### Escribe ahora


```java
public static boolean esPalindromo(String cadena) {
    String sinBlancos = "";
    for (int i = 0; i < cadena.length(); i++) {
```

### Explicación detallada

`esPalindromo` devuelve boolean, recibe String y crea `sinBlancos`. Recorre de izquierda a derecha, iniciando en 0, para preservar el orden normal del texto al quitar espacios. El valor de `sinBlancos` cambia en cada coincidencia admitida.

**Elementos nuevos o recuperados:** esPalindromo, sinBlancos (String).

**Estado después:** sinBlancos comienza vacío y se inspecciona cada char.

**Por qué podemos avanzar:** Tenemos que descartar solo los espacios.


## Paso 3 — Descartar el espacio normal

### Estado antes

sinBlancos="".

### ¿Por qué necesitamos este paso?

No queremos añadir el carácter espacio al acumulador.

### Escribe ahora


```java
if (cadena.charAt(i) != ' ') {
    sinBlancos += cadena.charAt(i);
}
}
```

### Explicación detallada

`!=` compara desigualdad de dos `char`: si la posición actual no es espacio `` se concatena; si es espacio no se añade. La primera llave cierra if y la siguiente el for. Este ejercicio no elimina signos ni acentos, solamente espacios ordinarios.

**Elementos nuevos o recuperados:** != para char, filtro de espacios.

**Estado después:** sinBlancos="Anitalavalatina" en el caso de estudio.

**Por qué podemos avanzar:** Al quitar espacios podemos invertir y comparar.


## Paso 4 — Invertir y comparar

### Estado antes

sinBlancos depurado.

### ¿Por qué necesitamos este paso?

La frase depurada debe ser igual a su reverso sin importar las mayúsculas.

### Escribe ahora


```java
String invertida = invierteCadena(sinBlancos);
return sinBlancos.equalsIgnoreCase(invertida);
}
```

### Explicación detallada

Se invoca un método previamente construido; la igualdad sin mayúsculas entrega true o false. La comparación se hace sobre cadenas sin espacios y no sobre la original. El método devuelve inmediatamente un boolean.

**Elementos nuevos o recuperados:** invocación anidada, equalsIgnoreCase.

**Estado después:** invertida calculada; retorno boolean.

**Por qué podemos avanzar:** La consola validará un caso positivo y otro negativo.


## Paso 5 — Probar dos casos

### Estado antes

El método ya está completo.

### ¿Por qué necesitamos este paso?

Una única prueba positiva podría ocultar un método que siempre retorna true.

### Escribe ahora


```java
public static void main(String[] args) {
    System.out.println(esPalindromo("Anita lava la tina"));
    System.out.println(esPalindromo("Hola mundo"));
```

### Explicación detallada

La primera salida debe ser true porque la frase es simétrica al ignorar espacios y caja. La segunda debe ser false; se cierran main y la clase.

**Elementos nuevos o recuperados:** prueba positiva/negativa.

**Estado después:** Se imprimen true y false en líneas separadas.

**Por qué podemos avanzar:** Las variaciones mostrarán límites de esta definición de palíndromo.


## Traza manual o simulación

"Anita lava la tina" → quitar espacios: "Anitalavalatina" → invertir: "anitalavalatinA" → equalsIgnoreCase: true. "Hola mundo" → "Holamundo" ≠ "odnumaloH" → false.

## Auditoría del artefacto construido

| Elemento | Qué hace / estado | Por qué existe |
|---|---|---|
| invierteCadena | inversión previa | reutilizar habilidad EJ04 |
| for ascendente | revisa posiciones en orden | preservar orden del texto |
| charAt(i) != ' ' | descarta espacios | aplicar regla de fuente |
| equalsIgnoreCase | compara sin capitalización | palíndromo sensible a letras pero no a caja |
| true/false | resultado boolean | verificar ambos casos |


## Archivo completo al terminar el ejemplo


```java
public class EJ07Palindromo {
    public static String invierteCadena(String cadena) {
        String invertida = "";
        for (int i = cadena.length() - 1; i >= 0; i--) {
            invertida += cadena.charAt(i);
        }
        return invertida;
    }
    public static boolean esPalindromo(String cadena) {
        String sinBlancos = "";
        for (int i = 0; i < cadena.length(); i++) {
            if (cadena.charAt(i) != ' ') {
                sinBlancos += cadena.charAt(i);
            }
        }
        String invertida = invierteCadena(sinBlancos);
        return sinBlancos.equalsIgnoreCase(invertida);
    }
    public static void main(String[] args) {
        System.out.println(esPalindromo("Anita lava la tina"));
        System.out.println(esPalindromo("Hola mundo"));
    }
}
```


## Antes de ejecutar: predicción

1. ¿Se consideran los espacios de "Anita lava la tina"?
2. ¿Cuál método evita que Ana y ana se consideren diferentes por caja?
3. ¿Se eliminan tildes o comas?


## Ejecuta y valida


```bash
javac -encoding UTF-8 EJ07Palindromo.java
java EJ07Palindromo
```

**Resultado esperado:**


```text
true
false
```

**Cómo interpretarlo:** Eliminar únicamente el espacio ordinario, invertir y comparar sin distinguir mayúsculas. El resultado demuestra las decisiones de los microbloques y debe coincidir con la predicción cuando los datos sean iguales.

**Variación A:** Prueba `"Somos"` y `"Java"`; predice true y false respectivamente.

**Error o caso límite controlado:** Suponer que la frase `"Anita, lava la tina"` será verdadera con la lógica actual.

**Por qué ocurre:** El signo coma no está excluido, por eso no se debe prometer que se ignora puntuación.

**Corrección razonada:** Definir correctamente el alcance de la práctica: eliminar espacios ordinarios; no añadir normalización de puntuación.

**Qué debes poder explicar con tus palabras:** la responsabilidad de cada variable, el criterio de inicio y término de cada ciclo, el significado del retorno y por qué el caso límite no debe sorprenderte.

## T07 — Tarea espejo: Palíndromos con y sin espacios

**Enunciado:** Implementa `esPalindromo` usando `invierteCadena` y evalúa `"Luz azul"` y `"Java"` con la misma regla de espacios y mayúsculas.

**Archivo que debes crear o modificar:** `T07Palindromos.java`.

**Restricción:** No eliminar comas/tildes mediante librerías adicionales; mantener definición del material.

**Pista:** True para Luz azul y false para Java.

**Evidencia:** captura o transcripción de la consola, archivo `.java` y explicación de dos decisiones técnicas.

**Cómo saber si está correcta:** true; false

**Punto de partida sugerido (código completo de trabajo con TODO):**


```java
public class T07Palindromos {
    public static String invierteCadena(String cadena) {
        String invertida = "";
        for (int i = cadena.length() - 1; i >= 0; i--) {
            invertida += cadena.charAt(i);
        }
        return invertida;
    }
    public static boolean esPalindromo(String cadena) {
        // TODO T07: descarta ' ', invierte y compara con equalsIgnoreCase.
        return false;
    }
    public static void main(String[] args) {
        System.out.println(esPalindromo("Luz azul"));
        System.out.println(esPalindromo("Java"));
    }
}
```


**Cómo ejecutar tu tarea:** `javac -encoding UTF-8 T07Palindromos.java` y `java T07Palindromos`. Sustituye los TODO; el texto PENDIENTE es solo un marcador inicial.


---

# EJ08 — Aplicación integradora de consola ProCadenas

**Fuente temática:** INTEGRADOR (diapositivas 18–22).

**Qué vamos a construir:** Los cinco métodos aislados deben poder utilizarse desde una aplicación que recoja entradas y muestre resultados sin fallar al introducir posiciones imposibles.

**Qué aprenderás:** Integrar los cinco métodos de ProCadenas, Scanner y comprobaciones para entradas de consola.

**Archivo principal:** `EJ08App.java` y `ProCadenas.java` en la misma carpeta.

**Punto de partida:** crea un archivo con ese nombre en la carpeta de trabajo. Parte de la estructura de clase y `main` conocida; las partes funcionales se agregan progresivamente.


## Paso 1 — Reunir los cinco utilitarios

### Estado antes

Los métodos viven en clases de demostración independientes.

### ¿Por qué necesitamos este paso?

`ProCadenas.java` centraliza cinco responsabilidades que ya enseñamos en EJ04–EJ07.

### Escribe ahora


```java
public class ProCadenas {
    public static String invierteCadena(String cadena) {
        String invertida = "";
        for (int i = cadena.length() - 1; i >= 0; i--) {
            invertida += cadena.charAt(i);
        }
        return invertida;
    }
    public static int cuentaOcurrenciasCaracter(String cadena, char caracter) {
        int total = 0;
        for (int i = 0; i < cadena.length(); i++) {
            if (cadena.charAt(i) == caracter) {
                total++;
            }
        }
        return total;
    }
    public static int posicionSubcadena(String cadena, String subcadena) {
        return cadena.indexOf(subcadena);
    }
    public static String extraeSubcadena(String cadena, int inicio, int cantidad) {
        return cadena.substring(inicio, inicio + cantidad);
    }
    public static boolean esPalindromo(String cadena) {
        String sinBlancos = "";
        for (int i = 0; i < cadena.length(); i++) {
            if (cadena.charAt(i) != ' ') {
                sinBlancos += cadena.charAt(i);
            }
        }
        return sinBlancos.equalsIgnoreCase(invierteCadena(sinBlancos));
    }
}
```

### Explicación detallada

Este archivo usa cinco cuerpos completos ya desarrollados: invierteCadena conserva el for descendente de EJ04; cuentaOcurrenciasCaracter tiene el contador y el if de EJ05; posicionSubcadena y extraeSubcadena reutilizan indexOf y substring de EJ06; esPalindromo filtra los espacios, invierte y compara como en EJ07. La diferencia es únicamente la clase contenedora ProCadenas y la llamada estática entre sus métodos; el lector verá inmediatamente el código Java completo, sin puntos suspensivos ni dependencias.

**Elementos nuevos o recuperados:** ProCadenas, reutilización static.

**Estado después:** Se reúnen en una clase utilitaria para llamarlos desde otra clase.

**Por qué podemos avanzar:** La app debe leer las entradas antes de llamar los métodos.


## Paso 2 — Preparar la lectura de consola

### Estado antes

ProCadenas ya está disponible.

### ¿Por qué necesitamos este paso?

`Scanner` permite que el usuario ingrese la frase y el carácter buscado.

### Escribe ahora


```java
import java.util.Scanner;
public class EJ08App {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Cadena: ");
        String cadena = sc.nextLine();
        System.out.print("Carácter: ");
        String auxiliar = sc.nextLine();
```

### Explicación detallada

`import java.util.Scanner` permite usar Scanner de la biblioteca estándar. `new Scanner(System.in)` crea el lector. `System.out.print` deja el cursor en la misma línea y `nextLine` consume la línea ingresada. `auxiliar` sigue siendo un String, aunque represente un carácter.

**Elementos nuevos o recuperados:** import, Scanner, new, nextLine(), print().

**Estado después:** Existen sc, cadena y auxiliar.

**Por qué podemos avanzar:** Antes de extraer charAt(0) hay que garantizar que el texto no esté vacío.


## Paso 3 — Validar el carácter y leer los otros parámetros

### Estado antes

auxiliar posiblemente vacío.

### ¿Por qué necesitamos este paso?

Un auxiliar vacío no permite recuperar la posición 0.

### Escribe ahora


```java
if (auxiliar.length() == 0) {
    System.out.println("Error: ingresa un carácter.");
    sc.close();
    return;
}
char caracter = auxiliar.charAt(0);
System.out.print("Subcadena buscada: ");
String subcadena = sc.nextLine();
System.out.print("Posición inicial: ");
int inicio = sc.nextInt();
System.out.print("Cantidad de caracteres: ");
int cantidad = sc.nextInt();
```

### Explicación detallada

`length()==0` detecta línea vacía, `return` finaliza main sin provocar `charAt(0)` inválido y `close` libera Scanner. Con entrada válida, `charAt(0)` toma el primer carácter. `nextInt` lee enteros para posición y cantidad; una entrada no numérica no está contemplada en este ejercicio básico.

**Elementos nuevos o recuperados:** close(), return temprano, nextInt().

**Estado después:** caracter válido, subcadena, inicio y cantidad leídos.

**Por qué podemos avanzar:** Podemos invocar las funciones que ya conocemos.


## Paso 4 — Mostrar inversión, conteo y búsqueda

### Estado antes

Todos los datos de entrada ya existen.

### ¿Por qué necesitamos este paso?

Los métodos estáticos se invocan con `ProCadenas.nombreMetodo`.

### Escribe ahora


```java
System.out.println("Invertida: " + ProCadenas.invierteCadena(cadena));
System.out.println("Ocurrencias: " + ProCadenas.cuentaOcurrenciasCaracter(cadena, caracter));
System.out.println("Posición: " + ProCadenas.posicionSubcadena(cadena, subcadena));
```

### Explicación detallada

Cada llamada usa argumentos del tipo adecuado y produce el valor demostrado anteriormente: String, int e int. No hay instancias de ProCadenas porque sus operaciones son static. La búsqueda podría dar -1 sin impedir las demás operaciones.

**Elementos nuevos o recuperados:** llamada estática Clase.metodo.

**Estado después:** La consola muestra tres resultados independientes.

**Por qué podemos avanzar:** La extracción merece una validación especial de intervalos.


## Paso 5 — Proteger el intervalo de extracción

### Estado antes

inicio y cantidad pueden ser inválidos.

### ¿Por qué necesitamos este paso?

El usuario puede escribir una posición negativa o una cantidad mayor que el texto.

### Escribe ahora


```java
if (inicio >= 0 && cantidad >= 0 && inicio <= cadena.length()
        && cantidad <= cadena.length() - inicio) {
    System.out.println("Extraída: " + ProCadenas.extraeSubcadena(cadena, inicio, cantidad));
} else {
    System.out.println("Extracción no válida.");
}
```

### Explicación detallada

Las cuatro condiciones evitan iniciar fuera de rango o exceder la longitud. La resta length-inicio evita construir un límite superior incorrecto y comprueba la cantidad disponible. `&&` exige cumplir todas las condiciones. La rama else informa en vez de terminar por excepción.

**Elementos nuevos o recuperados:** &&, else, límites de substring.

**Estado después:** Se extrae un texto válido o se informa el problema.

**Por qué podemos avanzar:** Falta mostrar palíndromo y cerrar el lector.


## Paso 6 — Comprobar palíndromo y cerrar recursos

### Estado antes

Los demás resultados se mostraron.

### ¿Por qué necesitamos este paso?

La última operación usa el mismo texto original y entrega boolean.

### Escribe ahora


```java
System.out.println("Palíndromo: " + ProCadenas.esPalindromo(cadena));
sc.close();
```

### Explicación detallada

`esPalindromo` devuelve true/false tras quitar espacios, invertir y comparar. `sc.close()` libera el lector después de consumir todas las entradas. Luego se cierran main y clase con las llaves correspondientes.

**Elementos nuevos o recuperados:** cierre de recurso.

**Estado después:** La app está completa y el lector se cierra.

**Por qué podemos avanzar:** Es momento de validar con un caso integrado real.


### Construcción completa de `ProCadenas.java`

Este archivo contiene los cinco métodos ya construidos individualmente. Se escriben sus cuerpos exactamente aquí: los recorridos y retornos son los de EJ04–EJ07, y los dos métodos de búsqueda y extracción mantienen los parámetros de EJ06. Ninguna operación tiene que adivinarse.


```java
public class ProCadenas {
    public static String invierteCadena(String cadena) {
        String invertida = "";
        for (int i = cadena.length() - 1; i >= 0; i--) {
            invertida += cadena.charAt(i);
        }
        return invertida;
    }
    public static int cuentaOcurrenciasCaracter(String cadena, char caracter) {
        int total = 0;
        for (int i = 0; i < cadena.length(); i++) {
            if (cadena.charAt(i) == caracter) {
                total++;
            }
        }
        return total;
    }
    public static int posicionSubcadena(String cadena, String subcadena) {
        return cadena.indexOf(subcadena);
    }
    public static String extraeSubcadena(String cadena, int inicio, int cantidad) {
        return cadena.substring(inicio, inicio + cantidad);
    }
    public static boolean esPalindromo(String cadena) {
        String sinBlancos = "";
        for (int i = 0; i < cadena.length(); i++) {
            if (cadena.charAt(i) != ' ') {
                sinBlancos += cadena.charAt(i);
            }
        }
        return sinBlancos.equalsIgnoreCase(invierteCadena(sinBlancos));
    }
}
```


## Traza manual o simulación

Secuencia de ejemplo: cadena="Anita lava la tina", carácter=`a`, subcadena="lava", inicio=6, cantidad=4. Resultados: invertida="anit al aval atinA", ocurrencias=5, posición=6, extraída="lava", palíndromo=true.

## Auditoría del artefacto construido

| Elemento | Qué hace / estado | Por qué existe |
|---|---|---|
| ProCadenas.java | 5 métodos reutilizables | separar operaciones |
| Scanner | lee entradas | hacer aplicación interactiva |
| validación auxiliar | rechaza carácter ausente | evitar charAt inválido |
| llamadas estáticas | produce inversión/conteo/búsqueda | integración |
| condición múltiple | verifica intervalo | evitar substring inválido |
| close | libera entrada | cierre de recursos |


## Archivo completo al terminar el ejemplo


```java
import java.util.Scanner;

public class EJ08App {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Cadena: ");
        String cadena = sc.nextLine();
        System.out.print("Carácter: ");
        String auxiliar = sc.nextLine();
        if (auxiliar.length() == 0) {
            System.out.println("Error: ingresa un carácter.");
            sc.close();
            return;
        }
        char caracter = auxiliar.charAt(0);
        System.out.print("Subcadena buscada: ");
        String subcadena = sc.nextLine();
        System.out.print("Posición inicial: ");
        int inicio = sc.nextInt();
        System.out.print("Cantidad de caracteres: ");
        int cantidad = sc.nextInt();
        System.out.println("Invertida: " + ProCadenas.invierteCadena(cadena));
        System.out.println("Ocurrencias: " + ProCadenas.cuentaOcurrenciasCaracter(cadena, caracter));
        System.out.println("Posición: " + ProCadenas.posicionSubcadena(cadena, subcadena));
        if (inicio >= 0 && cantidad >= 0 && inicio <= cadena.length()
                && cantidad <= cadena.length() - inicio) {
            System.out.println("Extraída: " + ProCadenas.extraeSubcadena(cadena, inicio, cantidad));
        } else {
            System.out.println("Extracción no válida.");
        }
        System.out.println("Palíndromo: " + ProCadenas.esPalindromo(cadena));
        sc.close();
    }
}
```


## Antes de ejecutar: predicción

1. ¿Por qué `auxiliar` se lee primero como String?
2. ¿Qué pasa si se pide extraer 40 caracteres?
3. ¿Qué clase conserva los métodos utilitarios?


## Ejecuta y valida

Coloca `EJ08App.java` y `ProCadenas.java` en la misma carpeta. En la terminal de esa carpeta ejecuta:

```bash
javac -encoding UTF-8 ProCadenas.java EJ08App.java
java EJ08App
```

Ingresa las cinco líneas, en este orden: `Anita lava la tina`, `a`, `lava`, `6`, `4`. Si usas un IDE, ejecuta `main` de `EJ08App` y escribe los datos en la consola del IDE.

**Resultado esperado:**


```text
Cadena: Anita lava la tina
Carácter: a
Subcadena buscada: lava
Posición inicial: 6
Cantidad de caracteres: 4
Invertida: anit al aval atinA
Ocurrencias: 5
Posición: 6
Extraída: lava
Palíndromo: true
```

**Cómo interpretarlo:** Integrar los cinco métodos de ProCadenas, Scanner y comprobaciones para entradas de consola. El resultado demuestra las decisiones de los microbloques y debe coincidir con la predicción cuando los datos sean iguales.

**Variación A:** Prueba con la cadena `"Hola mundo"`, subcadena `"mundo"`, índice 5 y cantidad 5: muestra false para palíndromo.

**Error o caso límite controlado:** Ingresar cantidad=100 para una cadena de 18 caracteres.

**Por qué ocurre:** La solicitud excede el texto, por tanto es inválida para substring.

**Corrección razonada:** Conservar las comprobaciones; confirmar que se imprime "Extracción no válida." sin fallar.

**Qué debes poder explicar con tus palabras:** la responsabilidad de cada variable, el criterio de inicio y término de cada ciclo, el significado del retorno y por qué el caso límite no debe sorprenderte.

## T08 — Tarea espejo: Consulta integrada con la clase ProCadenas

**Enunciado:** Conservando `ProCadenas.java`, escribe una app que lea `texto` y `fragmento` e imprima: inversión, posición del fragmento, número de letras `a` y estado de palíndromo. Prueba texto "Anita lava la tina" y fragmento "lava".

**Archivo que debes crear o modificar:** `T08App.java` junto a `ProCadenas.java`, cuyo código completo se mostró arriba.

**Restricción:** No copiar los métodos dentro de T08App; invocarlos desde ProCadenas.

**Pista:** La app debe imprimir cuatro resultados y seguir funcionando con "Hola mundo".

**Evidencia:** captura o transcripción de la consola, archivo `.java` y explicación de dos decisiones técnicas.

**Cómo saber si está correcta:** Invertida: anit al aval atinA; Posición: 6; Cantidad de a: 5; Palíndromo: true

**Punto de partida sugerido (código completo de trabajo con TODO):**


```java
import java.util.Scanner;

public class T08App {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Texto: ");
        String texto = sc.nextLine();
        System.out.print("Fragmento: ");
        String fragmento = sc.nextLine();
        // TODO T08: imprimir inversión, posición de fragmento,
        //          cantidad de letras 'a' y evaluación de palíndromo.
        System.out.println("PENDIENTE T08");
        sc.close();
    }
}
```


**Cómo ejecutar tu tarea:** compila `ProCadenas.java` y `T08App.java` juntos; después ejecuta `java T08App`. Sustituye los TODO; el texto PENDIENTE es solo un marcador inicial.


---

## 6. Cierre de sesión: lo que sabes construir y comprobar

Durante esta sesión construiste una ruta completa desde una cadena sencilla hasta una aplicación de consola que utiliza métodos especializados. Empezaste por los índices: aprendiste a no confundir `length()` con el último índice y a usar `charAt` solo cuando el intervalo lo permite. Comparaste cadenas con criterios distintos, buscaste fragmentos y comprobaste que operaciones como `trim`, `toUpperCase` o `replace` devuelven resultados nuevos. Luego recorriste caracteres con ciclos descendentes y ascendentes, construiste acumuladores y contadores, y entendiste por qué sus valores iniciales afectan la salida. La búsqueda y extracción de subcadenas te obligó a traducir un índice de inicio y una cantidad a un límite final exclusivo. Por último, la comprobación de palíndromos integró limpieza de espacios, inversión y comparación sin diferencias de mayúsculas.

No basta con que el programa imprima valores correctos: ahora debes poder justificar qué devuelve cada método, qué hace cada condición y por qué algunas entradas producen errores si no se validan. Repasa especialmente el índice `length()-1`, la condición `i < length()`, el valor `-1` de `indexOf` y el segundo índice exclusivo de `substring`. Como práctica final, ejecuta todas las tareas T01–T08 e identifica qué decisión es reutilizable entre ellas. Si necesitas reforzar los conceptos, consulta la documentación de `String` y los recursos de **Lideratec Academy** en https://lideratecacademy.com/blog/ y https://www.youtube.com/@LideratecAcademy. En sesiones posteriores podrás aplicar estos mismos criterios de lectura, validación e integración a otros objetos y métodos.

**Entregables del estudiante:** ocho archivos de tarea T01–T08, salidas de consola y explicación breve por tarea. La evidencia final demuestra comprensión, no una copia de los ejemplos.
