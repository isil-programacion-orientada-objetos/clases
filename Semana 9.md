---
course_id: JAVA-POO
session_id: S09
module_id: TEMA_09
source_origin: PPT
status: validated
---

# CREACIÓN DE COLECCIONES EN JAVA — GUÍA DEL ESTUDIANTE

**Lideratec Academy | Programación Orientada a Objetos | Sesión 09 | Java 21**

## 1. Propósito de la sesión

Durante una feria académica pueden llegar dos inscripciones de la misma persona, mientras que para el control de ingreso solo queremos contar asistentes diferentes. Al mismo tiempo, un coordinador consulta carreras escribiendo un código. Estos tres requisitos parecen semejantes porque todos almacenan datos, pero no se comportan igual: una lista guarda el orden y acepta repetidos, un conjunto impide duplicados y un mapa relaciona claves con valores. Elegir mal una estructura puede hacer perder registros, duplicar un conteo o dificultar una búsqueda.

En esta sesión construiremos pequeños programas de consola utilizando el Java Collections Framework. Partiremos de una lista `ArrayList`, practicaremos cancelaciones, diferenciaremos `HashSet` de `TreeSet`, consultaremos un `HashMap` y reuniremos `List`, `Set` y `Map` en un registro sencillo. Después contrastaremos una `LinkedList`, una cola de atención, un recorrido con `Iterator` y un criterio `Comparator`. Trabajaremos con Java 21 y archivos `.java` independientes; no necesitamos JSP, Tomcat, base de datos ni dependencias externas. Esta decisión facilita observar directamente qué hace cada operación.

Cada ejemplo tendrá una predicción, una construcción progresiva y una salida observable. La meta no es copiar clases completas: al finalizar podrás justificar por qué `List`, `Set` o `Map` es la opción coherente con un requisito concreto y demostrarlo en consola.

## 2. Resultado observable

Al concluir podrás crear colecciones tipadas mediante interfaces del JCF e implementaciones concretas, insertar y recuperar elementos, distinguir orden y duplicados, y seleccionar una estructura apropiada para una situación de registro. En particular, podrás explicar por qué `[Juana, Luis, Juana, Omar]` debe permanecer como lista cuando se cuentan inscripciones, mientras `[Juana, Luis, Omar]` expresa asistentes únicos. También podrás asociar el número 2 con Economía por medio de un mapa, sin confundir esa clave con una posición. Consideraremos logrado el resultado cuando compiles y ejecutes los ejemplos, predigas correctamente las salidas, corrijas al menos un error controlado y justifiques verbalmente la elección de cada colección.

### Desempeños verificables

- Crear una colección tipada con `List`, `Set` o `Map`.
- Predecir el efecto de `add`, `remove`, `get`, `size`, `contains` y `put`.
- Distinguir un valor duplicado de una clave actualizada.
- Ejecutar, contrastar y corregir salidas de consola.
- Justificar la estructura elegida en el integrador.

## 3. Antes de iniciar

**Debes saber:** declarar clases y `main`, utilizar variables, `println`, condicionales básicos y `for-each` (este último se recuerda dentro del ejemplo). **Necesitas:** JDK 21 e IntelliJ IDEA con soporte de Java, o una terminal y editor. **Todavía no asumimos:** persistencia, streams, genéricos avanzados, concurrencia, JSP, servlets, comparadores personalizados o base de datos.

## 4. Plan de clase presencial de 120 minutos — versión ampliada

Esta guía contiene **10 ejemplos completos y 10 tareas espejo**. En las dos horas se desarrollan **ocho ejemplos guiados** (EJ01, EJ02, EJ03, EJ04, EJ05, EJ07, EJ08 y EJ06). EJ09 y EJ10 quedan completamente explicados para el trabajo autónomo o la siguiente práctica; sus soluciones y validaciones también están preparadas. Las tareas espejo se trabajan como microverificaciones seleccionadas, no se simula que diez tareas completas caben en el aula. Si el grupo tiene dificultades con el entorno, prioriza EJ01, EJ03, EJ05 y EJ06 sin sacrificar la explicación.

| Minutos | Bloque | Modalidad y evidencia inmediata |
|---|---|---|
| 00–08 | Caso inicial | Decidir si contar registros, personas o claves |
| 08–15 | Entorno | Verificar JDK 21; ejecutar HolaColecciones |
| 15–28 | EJ01 | List mantiene duplicados; predicción T01 breve |
| 28–40 | EJ02 | remove + for-each; comprobar tamaño |
| 40–53 | EJ03 | HashSet y add repetido; evidencia booleana |
| 53–65 | EJ04 | TreeSet: unicidad + orden natural |
| 65–80 | EJ05 | HashMap: put reemplaza una clave; T05 breve |
| 80–91 | EJ07 | LinkedList: inserción en posición y cancelación |
| 91–102 | EJ08 | Queue FIFO: peek frente a poll |
| 102–114 | EJ06 | Integrador de List, Set y Map; predicción completa |
| 114–120 | Cierre | Ticket de salida y asignación de EJ09–EJ10 |
| **Total** | **120 minutos** | **8 demostraciones + 2 ejemplos de profundización** |

**Microtareas dentro de clase:** se proponen predicciones y una modificación mínima tras cada demostración. Las soluciones completas T01–T10 son trabajo individual; EJ09 (Iterator) y EJ10 (Comparator) funcionan como itinerario opcional de ampliación autónoma. El material permite impartir una clase de dos horas sin apresurar las explicaciones ni ocultar pasos.

## 5. Preparar el entorno desde cero

### Ruta A: ya tienes JDK e IntelliJ IDEA

1. Abre una terminal y ejecuta `java -version`; comprueba que aparece una versión 21. Ejecuta también `javac -version`; comprueba que se informa 21.
2. Abre IntelliJ IDEA. Elige **New Project** (o **File > New > Project** según versión). Selecciona **Java** y el JDK 21 instalado. Para este laboratorio no marques **Maven**, **Gradle** ni frameworks. Pon de nombre `ColeccionesS09`.
3. En el proyecto, localiza la carpeta `src`. Con clic derecho sobre ella elige **New > Java Class**, escribe `HolaColecciones` y confirma. Si tu IDE generó una línea `package`, puedes mantener una convención de paquetes de tu curso, pero los ejemplos de esta guía se presentan sin `package` para ejecutarse también desde terminal. Evita mezclar archivos empaquetados y sin empaquetar.
4. Reemplaza el contenido por el siguiente código y ejecútalo desde el triángulo junto a `main`. Debe imprimirse `Java 21 listo`. Si el proyecto no ve el JDK, abre **Project Structure > Project SDK** y selecciona el JDK 21 ya instalado.

```java
public class HolaColecciones {
    public static void main(String[] args) {
        System.out.println("Java 21 listo");
    }
}
```


### Ruta B: tu equipo no tiene JDK

1. Descarga un **JDK 21** de un distribuidor oficial compatible con tu sistema. Instálalo con los permisos institucionales correspondientes. Recuerda que un JRE por sí solo no incluye el compilador `javac`.
2. Vuelve a abrir la terminal y ejecuta `java -version` y `javac -version`; ambos deben indicar 21. Si `javac` no se reconoce, configura el JDK como SDK del proyecto y revisa la variable `PATH` del sistema según las políticas del equipo.
3. Instala o abre IntelliJ IDEA, crea `ColeccionesS09` como se indica en la ruta A y verifica `HolaColecciones`. No es necesario descargar Spring, Tomcat, bases de datos ni una librería adicional: `java.util` viene con el JDK.

### Alternativa por terminal: ejecutar sin IDE

Crea una carpeta llamada `ColeccionesS09`, y dentro guarda un archivo `EJ01.java` sin `package`. Desde esa carpeta ejecuta:

```bash
javac -encoding UTF-8 EJ01.java
java EJ01
```

En Windows PowerShell o CMD se usan los mismos comandos. El nombre del archivo debe coincidir exactamente con el nombre de la clase pública. Repite con EJ02.java...EJ10.java al avanzar. Si `java` señala `ClassNotFoundException`, revisa que la terminal esté ubicada en la carpeta que contiene el archivo `.class`.

**Advertencia de codificación:** conserva los archivos en UTF-8 para que las tildes de `Informática` y `Raúl` no se alteren.

## 6. Qué significa declarar por interfaz

`List<String> nombres = new ArrayList<>();` se lee así: necesito una **lista** de textos y elijo la implementación concreta **ArrayList**. `Set<String>` significa conjunto de textos únicos y `Map<Integer,String>` significa asociación de claves enteras con textos. `List` y `Set` pertenecen a la jerarquía `Collection`; `Map` pertenece a una jerarquía paralela del Java Collections Framework. El paquete de importación correcto es `java.util`, sin tilde.

**Importante:** no necesitas crear manualmente interfaces para utilizar las interfaces existentes `List`, `Set` y `Map` del JDK. En Java una interfaz define un contrato de operaciones y una clase como `ArrayList` implementa ese contrato.


---

# EJ01 — Conservar inscripciones repetidas con List y ArrayList

## Objetivo técnico — Qué vamos a hacer y qué aprenderemos

En una feria académica una misma persona puede inscribirse más de una vez. Necesitamos conservar cada anotación y respetar el orden en que llegó. Primero crearemos una lista vacía mediante la interfaz `List` y la implementación `ArrayList`; después agregaremos cuatro nombres, incluido uno repetido. Finalmente consultaremos la posición cero y el tamaño de la lista. Si la consola mantiene ambas apariciones de Juana y muestra cuatro inscripciones, habremos comprobado que `List` acepta repetidos y mantiene el orden de inserción.

## Qué problema concreto resolveremos

El registro no puede borrar una inscripción solo porque ya exista otra con el mismo nombre: cada ingreso cuenta.

## Archivos y punto de partida

Crea `src/EJ01.java` en IntelliJ, sin declaración `package`, o guárdalo como `EJ01.java` en la carpeta del laboratorio. Este ejemplo es independiente de los anteriores; se inicia con su archivo vacío. Los `import` se colocan **antes** de `public class`, y las instrucciones de los pasos siguientes van **dentro de `main`**, entre sus llaves. No compiles un archivo a medio construir.

### Paso 1 — Abrir una clase ejecutable y declarar las importaciones

**Antes de escribir:** necesitamos que Java encuentre las interfaces y clases estándar usadas en este ejemplo. En la parte superior del archivo escribe estas importaciones; debajo crea el envoltorio de clase. La clase pública tiene exactamente el mismo nombre que el archivo, condición indispensable para compilar sin errores.

```java
import java.util.List;
import java.util.ArrayList;

public class EJ01 {
    public static void main(String[] args) {
        // Aquí construiremos las instrucciones de los pasos 2 en adelante.
    }
}
```

**Mientras escribimos:** `import` permite utilizar el nombre corto de cada tipo; `public class` declara la clase; `main(String[] args)` es el punto de ejecución; `System.out.println` imprimirá mensajes cuando lo agreguemos. La línea de comentario es solo una marca temporal: elimínala antes de insertar el primer fragmento.

**Validación intermedia:** puedes compilar esta estructura vacía, pero todavía no muestra datos; las salidas aparecerán cuando agreguemos las operaciones.

### Paso 2 — Crear una lista tipada para registrar nombres

**Para comprender antes de escribir:** Todavía no existe ningún lugar donde guardar una cantidad variable de nombres. Declararemos una referencia de tipo `List<String>` para expresar que gestionamos una secuencia de textos, y usaremos `new ArrayList<>()` para obtener un objeto concreto. El símbolo `<>` permite inferir el tipo genérico que ya se declaró a la izquierda.

**Dónde y qué modificar:** en `src/EJ01.java`, dentro de `main`, inserta estas sentencias después del último bloque incorporado; la primera vez colócalas donde retiraste el comentario temporal. Mantén abiertos únicamente los delimitadores que muestre el fragmento, y conserva todas las sentencias anteriores.

```java
List<String> nombres = new ArrayList<>();
```

**Mientras lo construimos, comprendamos cada parte:** La interfaz `List` define operaciones de lista; `String` restringe el contenido a cadenas; `nombres` es la referencia; `new ArrayList<>()` crea la lista inicialmente vacía. No estamos creando cuatro variables sueltas: la colección crecerá al recibir cada `add`.

**Estado antes → después:** No hay elementos: `nombres.size()` sería 0.

**Por qué avanzamos:** Para evidenciar que puede almacenar entradas repetidas necesitamos insertar datos en su orden real.

### Paso 3 — Agregar las cuatro inscripciones sin eliminar duplicados

**Para comprender antes de escribir:** La lista ya existe, pero todavía está vacía. Insertaremos cada inscripción usando `add`, operación que agrega el elemento al final. Repetir Juana es deliberado: este dato nos permitirá distinguir una lista de un conjunto más adelante.

**Dónde y qué modificar:** en `src/EJ01.java`, dentro de `main`, inserta estas sentencias después del último bloque incorporado; la primera vez colócalas donde retiraste el comentario temporal. Mantén abiertos únicamente los delimitadores que muestre el fragmento, y conserva todas las sentencias anteriores.

```java
nombres.add("Juana");
nombres.add("Luis");
nombres.add("Juana");
nombres.add("Omar");
```

**Mientras lo construimos, comprendamos cada parte:** Cada llamada `add` añade una nueva posición. Los índices serán 0=Juana, 1=Luis, 2=Juana y 3=Omar. La tercera línea no modifica la primera: el valor se repite en otra posición porque la lista no exige unicidad.

**Estado antes → después:** Estado acumulado: `[Juana, Luis, Juana, Omar]`, con cuatro posiciones.

**Por qué avanzamos:** Ahora necesitamos mostrar la colección completa y realizar consultas puntuales sobre ella.

### Paso 4 — Observar lista completa, primer registro y tamaño

**Para comprender antes de escribir:** Con la lista cargada comprobaremos tres aspectos diferentes. Imprimir el objeto mostrará los valores en orden; `get(0)` identificará el primer registro; `size()` devolverá cuántos elementos se conservaron, contando también la repetición.

**Dónde y qué modificar:** en `src/EJ01.java`, dentro de `main`, inserta estas sentencias después del último bloque incorporado; la primera vez colócalas donde retiraste el comentario temporal. Mantén abiertos únicamente los delimitadores que muestre el fragmento, y conserva todas las sentencias anteriores.

```java
System.out.println("Lista: " + nombres);
System.out.println("Primero: " + nombres.get(0));
System.out.println("Total: " + nombres.size());
```

**Mientras lo construimos, comprendamos cada parte:** `println` escribe texto en la consola. La concatenación con `+` incorpora el resultado de la colección o del método. `get(0)` usa un índice basado en cero y devuelve Juana; `size()` informa 4, no 3, porque estamos contando inscripciones y no personas únicas.

**Estado antes → después:** Ahora la consola permitirá cotejar la secuencia `[Juana, Luis, Juana, Omar]`, la primera posición y el total 4.

**Por qué avanzamos:** La siguiente actividad probará la misma relación entre orden, repetición e índices con ciudades.

## Auditoría del archivo construido

Comprueba que las importaciones están fuera de la clase, que existe una única clase pública con nombre igual al archivo, que las operaciones aparecen dentro de `main` y que los fragmentos de los pasos 2 en adelante conservan el orden mostrado. El listado siguiente es la **versión acumulada** de esos pasos, no una segunda implementación con código adicional.

## Archivo completo al terminar el ejemplo

```java
import java.util.List;
import java.util.ArrayList;

public class EJ01 {
    public static void main(String[] args) {
        List<String> nombres = new ArrayList<>();
        nombres.add("Juana");
        nombres.add("Luis");
        nombres.add("Juana");
        nombres.add("Omar");
        System.out.println("Lista: " + nombres);
        System.out.println("Primero: " + nombres.get(0));
        System.out.println("Total: " + nombres.size());
    }
}
```


## Antes de ejecutar: predicción

1. ¿Se conservará Juana dos veces o solo una?
2. ¿Qué nombre recuperará `get(0)`?
3. ¿`size()` contará nombres distintos o inscripciones?

## Ejecutar y validar

En IntelliJ abre `src/EJ01.java` y ejecuta el botón junto a `main`. En terminal, desde la carpeta donde guardaste el archivo, ejecuta:

```bash
javac -encoding UTF-8 EJ01.java
java EJ01
```

**Salida esperada:**

```text
Lista: [Juana, Luis, Juana, Omar]
Primero: Juana
Total: 4
```


## Interpretación del resultado

No confundas número de inscripciones con cantidad de participantes únicos; son necesidades distintas. Compara tu predicción con las líneas concretas de la consola; si no coinciden, revisa primero el orden de las llamadas que cambian los datos.

## Variación controlada

Inserta `nombres.add("Ana");` antes de los `println`. Predice la nueva lista y verifica que su tamaño pasa a 5. Explica cuál cambió el estado y qué elemento siguió conservándose.

## Error o caso límite y corrección razonada

Cambiar `get(0)` por `get(4)` en una lista de cuatro valores provoca `IndexOutOfBoundsException`: el último índice válido es 3. Restituye `get(0)` o elige un índice entre 0 y 3. Haz la prueba únicamente en una copia de tu archivo o revierte el cambio antes de seguir.


### Laboratorio de razonamiento adicional — Índices y duplicados

**Antes de pasar a la tarea espejo, reconstruye esta traza sin abrir la consola.**

| Acción | Estado observable | Consecuencia |
|---|---|---|
| Antes de add | [] | size=0 |
| Tras primera Juana | [Juana] | size=1 |
| Tras Luis y segunda Juana | [Juana, Luis, Juana] | size=3 |
| Tras Omar | [Juana, Luis, Juana, Omar] | size=4 |

**Pregunta de transferencia:** ¿Por qué size vale 4 aunque solamente hay tres nombres diferentes?

**Verificación:** formula una explicación con tus palabras y contrástala con el estado anterior/después. Identifica qué operación sería incorrecta si el requisito cambiara.

**Prueba adicional:** predice qué cambiaría al repetir la operación decisiva una vez más; ejecuta después y vuelve al archivo original para evitar confundir los resultados posteriores.

## T01 — Tarea espejo: Registrar ciudades sin perder repeticiones

**Enunciado:** Una encuesta registra las visitas Lima, Cusco y Lima. Conserva los tres registros en el orden recibido, imprime la lista, consulta la segunda posición y muestra el total.

**Archivo a crear:** `src/T01.java`, con clase pública `T01` y su propio `main`, tomando como referencia la estructura de clase que ya aprendiste.

**Restricción:** Mantén las dos apariciones de Lima; no uses `Set`.

**Pista:** Utiliza `List<String>`, `new ArrayList<>()`, tres `add`, `get(1)` y `size()`.

**Evidencia:** entrega código fuente y captura legible de la consola que coincida con estas líneas:

```text
Ciudades: [Lima, Cusco, Lima]
Segunda: Cusco
Total: 3
```

**Cómo sabes que está correcta:** compila sin errores, reproduce la salida en el orden indicado y puedes explicar qué operación genera cada resultado. La solución completa de la tarea la reconstruirás tú.


---

# EJ02 — Retirar un turno y recorrer una List sin perder el orden

## Objetivo técnico — Qué vamos a hacer y qué aprenderemos

Una sala de atención recibe turnos y, cuando una persona cancela, debe retirar solo su registro. En este ejercicio aprovecharemos una lista para conservar el orden de llegada, eliminaremos el turno de Luis mediante `remove` y recorreremos los turnos restantes con un ciclo `for-each`. Comprobaremos que la cancelación reduce el tamaño sin desordenar las otras inscripciones. El resultado será una salida por persona y un contador de turnos pendientes; esta operación es diferente de la consulta por índice del ejercicio anterior.

## Qué problema concreto resolveremos

Imprimir únicamente la lista no resuelve la necesidad de atender nombre por nombre; tampoco permite reflejar la cancelación de un turno.

## Archivos y punto de partida

Crea `src/EJ02.java` en IntelliJ, sin declaración `package`, o guárdalo como `EJ02.java` en la carpeta del laboratorio. Este ejemplo es independiente de los anteriores; se inicia con su archivo vacío. Los `import` se colocan **antes** de `public class`, y las instrucciones de los pasos siguientes van **dentro de `main`**, entre sus llaves. No compiles un archivo a medio construir.

### Paso 1 — Abrir una clase ejecutable y declarar las importaciones

**Antes de escribir:** necesitamos que Java encuentre las interfaces y clases estándar usadas en este ejemplo. En la parte superior del archivo escribe estas importaciones; debajo crea el envoltorio de clase. La clase pública tiene exactamente el mismo nombre que el archivo, condición indispensable para compilar sin errores.

```java
import java.util.List;
import java.util.ArrayList;

public class EJ02 {
    public static void main(String[] args) {
        // Aquí construiremos las instrucciones de los pasos 2 en adelante.
    }
}
```

**Mientras escribimos:** `import` permite utilizar el nombre corto de cada tipo; `public class` declara la clase; `main(String[] args)` es el punto de ejecución; `System.out.println` imprimirá mensajes cuando lo agreguemos. La línea de comentario es solo una marca temporal: elimínala antes de insertar el primer fragmento.

**Validación intermedia:** puedes compilar esta estructura vacía, pero todavía no muestra datos; las salidas aparecerán cuando agreguemos las operaciones.

### Paso 2 — Preparar la cola de turnos en orden de llegada

**Para comprender antes de escribir:** Crearemos una lista de textos porque el orden de inscripción sigue siendo relevante. El código agrega tres nombres explícitos para que sea visible qué estado existe antes de producir una cancelación. Al terminar estas sentencias, aún no se ha retirado ningún elemento.

**Dónde y qué modificar:** en `src/EJ02.java`, dentro de `main`, inserta estas sentencias después del último bloque incorporado; la primera vez colócalas donde retiraste el comentario temporal. Mantén abiertos únicamente los delimitadores que muestre el fragmento, y conserva todas las sentencias anteriores.

```java
List<String> turnos = new ArrayList<>();
turnos.add("Ana");
turnos.add("Luis");
turnos.add("Marta");
```

**Mientras lo construimos, comprendamos cada parte:** `turnos` es la referencia a una lista nueva. `add` agrega Ana en 0, Luis en 1 y Marta en 2. Mantener estas posiciones nos permitirá comprobar que el retiro no invierte ni reordena las entradas restantes.

**Estado antes → después:** Estado: `[Ana, Luis, Marta]`, tamaño 3.

**Por qué avanzamos:** Para representar la cancelación debemos remover el nombre que ya no tendrá atención.

### Paso 3 — Cancelar únicamente el turno de Luis

**Para comprender antes de escribir:** El registro contiene a Luis, pero ya no debe aparecer cuando se llame a las personas. Utilizaremos `remove("Luis")` para quitar una ocurrencia del valor indicado. Como el argumento es una cadena, esta sobrecarga busca el objeto y no un índice numérico.

**Dónde y qué modificar:** en `src/EJ02.java`, dentro de `main`, inserta estas sentencias después del último bloque incorporado; la primera vez colócalas donde retiraste el comentario temporal. Mantén abiertos únicamente los delimitadores que muestre el fragmento, y conserva todas las sentencias anteriores.

```java
turnos.remove("Luis");
```

**Mientras lo construimos, comprendamos cada parte:** La operación busca una aparición igual a `"Luis"` y la elimina. Ana permanece primero y Marta segundo. Si hubiera dos registros de Luis, esta llamada eliminaría solo la primera coincidencia, no todas.

**Estado antes → después:** Estado nuevo: `[Ana, Marta]`, tamaño 2.

**Por qué avanzamos:** Nos falta mostrar cómo recorrer secuencialmente los turnos aún activos.

### Paso 4 — Mostrar cada turno con for-each y contar pendientes

**Para comprender antes de escribir:** No queremos escribir manualmente `get(0)` y `get(1)` cada vez que cambie el número de turnos. El `for-each` visita cada elemento de la lista. Dentro de su bloque imprimiremos el nombre actual y, al final del recorrido, consultaremos `size()` para saber cuántos turnos quedan.

**Dónde y qué modificar:** en `src/EJ02.java`, dentro de `main`, inserta estas sentencias después del último bloque incorporado; la primera vez colócalas donde retiraste el comentario temporal. Mantén abiertos únicamente los delimitadores que muestre el fragmento, y conserva todas las sentencias anteriores.

```java
for (String nombre : turnos) {
    System.out.println("Atención: " + nombre);
}
System.out.println("Pendientes: " + turnos.size());
```

**Mientras lo construimos, comprendamos cada parte:** `String nombre` representa temporalmente cada entrada; el signo `:` se interpreta como «para cada elemento de `turnos`». La primera vuelta muestra Ana y la segunda muestra Marta. Las llaves agrupan el cuerpo del bucle. `size()` devuelve 2 después de eliminar Luis.

**Estado antes → después:** Se imprimen dos líneas de atención y el total de pendientes 2.

**Por qué avanzamos:** El siguiente ejemplo cambiará la necesidad: ignorar inscripciones repetidas en vez de conservarlas.

## Auditoría del archivo construido

Comprueba que las importaciones están fuera de la clase, que existe una única clase pública con nombre igual al archivo, que las operaciones aparecen dentro de `main` y que los fragmentos de los pasos 2 en adelante conservan el orden mostrado. El listado siguiente es la **versión acumulada** de esos pasos, no una segunda implementación con código adicional.

## Archivo completo al terminar el ejemplo

```java
import java.util.List;
import java.util.ArrayList;

public class EJ02 {
    public static void main(String[] args) {
        List<String> turnos = new ArrayList<>();
        turnos.add("Ana");
        turnos.add("Luis");
        turnos.add("Marta");
        turnos.remove("Luis");
        for (String nombre : turnos) {
            System.out.println("Atención: " + nombre);
        }
        System.out.println("Pendientes: " + turnos.size());
    }
}
```


## Antes de ejecutar: predicción

1. ¿Quién aparece en la primera línea de atención después de `remove`?
2. ¿Cuántas veces se repite el cuerpo del ciclo?
3. ¿Qué cambia si intentas quitar un nombre inexistente?

## Ejecutar y validar

En IntelliJ abre `src/EJ02.java` y ejecuta el botón junto a `main`. En terminal, desde la carpeta donde guardaste el archivo, ejecuta:

```bash
javac -encoding UTF-8 EJ02.java
java EJ02
```

**Salida esperada:**

```text
Atención: Ana
Atención: Marta
Pendientes: 2
```


## Interpretación del resultado

`remove` gestiona cancelaciones; `for-each` adapta la salida a una lista de longitud variable. Compara tu predicción con las líneas concretas de la consola; si no coinciden, revisa primero el orden de las llamadas que cambian los datos.

## Variación controlada

Agrega `turnos.add("Elena");` antes de la cancelación y verifica que el recorrido respeta la posición final de Elena. Explica cuál cambió el estado y qué elemento siguió conservándose.

## Error o caso límite y corrección razonada

Si escribes `turnos.remove("Pedro")`, no existe coincidencia: no se elimina ningún valor y el tamaño permanece en 3. Corrige el argumento a `"Luis"`. Haz la prueba únicamente en una copia de tu archivo o revierte el cambio antes de seguir.


### Laboratorio de razonamiento adicional — Eliminar por valor no equivale a eliminar por índice

**Antes de pasar a la tarea espejo, reconstruye esta traza sin abrir la consola.**

| Acción | Estado observable | Consecuencia |
|---|---|---|
| Antes de retirar | [Ana, Luis, Marta] | 3 turnos |
| Después de remove("Luis") | [Ana, Marta] | 2 turnos |
| Después de for-each | [Ana, Marta] | sin cambios |

**Pregunta de transferencia:** ¿El for-each modifica el contenido?

**Verificación:** formula una explicación con tus palabras y contrástala con el estado anterior/después. Identifica qué operación sería incorrecta si el requisito cambiara.

**Prueba adicional:** predice qué cambiaría al repetir la operación decisiva una vez más; ejecuta después y vuelve al archivo original para evitar confundir los resultados posteriores.

## T02 — Tarea espejo: Actualizar una lista de atención

**Enunciado:** Registra a Rosa, Pedro y Sonia; Pedro cancela. Muestra los turnos restantes con una línea `Atención: ...` por persona y al final imprime el número de pendientes.

**Archivo a crear:** `src/T02.java`, con clase pública `T02` y su propio `main`, tomando como referencia la estructura de clase que ya aprendiste.

**Restricción:** No reemplaces la lista por un arreglo ni uses un índice fijo para mostrar turnos.

**Pista:** Elimina `"Pedro"` con `remove`; recorre con `for (String persona : turnos)`.

**Evidencia:** entrega código fuente y captura legible de la consola que coincida con estas líneas:

```text
Atención: Rosa
Atención: Sonia
Pendientes: 2
```

**Cómo sabes que está correcta:** compila sin errores, reproduce la salida en el orden indicado y puedes explicar qué operación genera cada resultado. La solución completa de la tarea la reconstruirás tú.


---

# EJ03 — Evitar códigos duplicados mediante Set y HashSet

## Objetivo técnico — Qué vamos a hacer y qué aprenderemos

En el control de acceso de una actividad un código no debe contarse dos veces, aunque alguien intente registrarlo nuevamente. A diferencia de la lista, ahora necesitamos una colección de elementos únicos. Declararemos `Set<String>` e instanciaremos `HashSet`, insertaremos dos códigos y repetiremos uno para observar el valor booleano devuelto por `add`. Después verificaremos si un código está presente con `contains` y mostraremos el número de elementos únicos. No utilizaremos la posición ni supondremos un orden de salida porque `HashSet` no garantiza orden.

## Qué problema concreto resolveremos

Si una persona ingresa dos veces el mismo código, el total de asistentes únicos no debe incrementarse.

## Archivos y punto de partida

Crea `src/EJ03.java` en IntelliJ, sin declaración `package`, o guárdalo como `EJ03.java` en la carpeta del laboratorio. Este ejemplo es independiente de los anteriores; se inicia con su archivo vacío. Los `import` se colocan **antes** de `public class`, y las instrucciones de los pasos siguientes van **dentro de `main`**, entre sus llaves. No compiles un archivo a medio construir.

### Paso 1 — Abrir una clase ejecutable y declarar las importaciones

**Antes de escribir:** necesitamos que Java encuentre las interfaces y clases estándar usadas en este ejemplo. En la parte superior del archivo escribe estas importaciones; debajo crea el envoltorio de clase. La clase pública tiene exactamente el mismo nombre que el archivo, condición indispensable para compilar sin errores.

```java
import java.util.Set;
import java.util.HashSet;

public class EJ03 {
    public static void main(String[] args) {
        // Aquí construiremos las instrucciones de los pasos 2 en adelante.
    }
}
```

**Mientras escribimos:** `import` permite utilizar el nombre corto de cada tipo; `public class` declara la clase; `main(String[] args)` es el punto de ejecución; `System.out.println` imprimirá mensajes cuando lo agreguemos. La línea de comentario es solo una marca temporal: elimínala antes de insertar el primer fragmento.

**Validación intermedia:** puedes compilar esta estructura vacía, pero todavía no muestra datos; las salidas aparecerán cuando agreguemos las operaciones.

### Paso 2 — Crear una colección que exige unicidad

**Para comprender antes de escribir:** Hasta ahora una lista conservaba incluso registros duplicados. Esta vez necesitamos que cada código esté una sola vez. `Set` expresa esa regla de unicidad y `HashSet` la implementa sin ofrecer índices de posición ni un orden de iteración garantizado.

**Dónde y qué modificar:** en `src/EJ03.java`, dentro de `main`, inserta estas sentencias después del último bloque incorporado; la primera vez colócalas donde retiraste el comentario temporal. Mantén abiertos únicamente los delimitadores que muestre el fragmento, y conserva todas las sentencias anteriores.

```java
Set<String> codigos = new HashSet<>();
```

**Mientras lo construimos, comprendamos cada parte:** `Set<String>` es la interfaz de conjunto de cadenas, `codigos` la referencia y `new HashSet<>()` construye un conjunto vacío. A diferencia de `List`, aquí la pregunta importante no será «¿en qué posición?», sino «¿ya existe este elemento?».

**Estado antes → después:** Estado inicial: conjunto vacío, tamaño 0.

**Por qué avanzamos:** Ahora comprobaremos qué sucede al intentar introducir un duplicado.

### Paso 3 — Insertar códigos y capturar el rechazo del duplicado

**Para comprender antes de escribir:** Introduciremos dos códigos distintos y repetiremos el primero. El método `add` devuelve `true` si la colección cambió porque el elemento era nuevo, o `false` si ya existía. Guardaremos el tercer resultado para contrastar la predicción con la consola.

**Dónde y qué modificar:** en `src/EJ03.java`, dentro de `main`, inserta estas sentencias después del último bloque incorporado; la primera vez colócalas donde retiraste el comentario temporal. Mantén abiertos únicamente los delimitadores que muestre el fragmento, y conserva todas las sentencias anteriores.

```java
codigos.add("DNI100");
codigos.add("DNI200");
boolean repetido = codigos.add("DNI100");
```

**Mientras lo construimos, comprendamos cada parte:** Las primeras llamadas incorporan DNI100 y DNI200. En la tercera, `HashSet` detecta que DNI100 ya pertenece al conjunto. `boolean repetido` recibe `false`: el nombre de la variable describe el intento de repetición, no el éxito. El tamaño sigue siendo 2.

**Estado antes → después:** Estado: dos códigos únicos; `repetido == false`.

**Por qué avanzamos:** Falta consultar existencia y total sin depender del orden de los elementos.

### Paso 4 — Comprobar pertenencia y tamaño

**Para comprender antes de escribir:** Una lista de acceso necesita saber si una credencial está registrada. Usaremos `contains("DNI200")` para consultar presencia y `size()` para contar códigos únicos. También mostraremos el resultado de intentar repetir DNI100.

**Dónde y qué modificar:** en `src/EJ03.java`, dentro de `main`, inserta estas sentencias después del último bloque incorporado; la primera vez colócalas donde retiraste el comentario temporal. Mantén abiertos únicamente los delimitadores que muestre el fragmento, y conserva todas las sentencias anteriores.

```java
System.out.println("¿Se agregó repetido?: " + repetido);
System.out.println("Existe DNI200: " + codigos.contains("DNI200"));
System.out.println("Únicos: " + codigos.size());
```

**Mientras lo construimos, comprendamos cada parte:** `contains` devuelve `true` cuando el valor buscado está presente. La consulta no agrega ni elimina códigos. `size()` permanece en 2; ninguna línea imprime el conjunto entero, de manera que la comprobación no depende del orden no especificado de `HashSet`.

**Estado antes → después:** La consola mostrará `false`, `true` y 2 en tres líneas.

**Por qué avanzamos:** En el próximo ejercicio seguiremos evitando duplicados, pero exigiremos ver los valores ordenados.

## Auditoría del archivo construido

Comprueba que las importaciones están fuera de la clase, que existe una única clase pública con nombre igual al archivo, que las operaciones aparecen dentro de `main` y que los fragmentos de los pasos 2 en adelante conservan el orden mostrado. El listado siguiente es la **versión acumulada** de esos pasos, no una segunda implementación con código adicional.

## Archivo completo al terminar el ejemplo

```java
import java.util.Set;
import java.util.HashSet;

public class EJ03 {
    public static void main(String[] args) {
        Set<String> codigos = new HashSet<>();
        codigos.add("DNI100");
        codigos.add("DNI200");
        boolean repetido = codigos.add("DNI100");
        System.out.println("¿Se agregó repetido?: " + repetido);
        System.out.println("Existe DNI200: " + codigos.contains("DNI200"));
        System.out.println("Únicos: " + codigos.size());
    }
}
```


## Antes de ejecutar: predicción

1. ¿Qué devuelve la tercera llamada a `add`?
2. ¿`contains("DNI200")` cambiará el conjunto?
3. ¿Cuál será el total de códigos únicos?

## Ejecutar y validar

En IntelliJ abre `src/EJ03.java` y ejecuta el botón junto a `main`. En terminal, desde la carpeta donde guardaste el archivo, ejecuta:

```bash
javac -encoding UTF-8 EJ03.java
java EJ03
```

**Salida esperada:**

```text
¿Se agregó repetido?: false
Existe DNI200: true
Únicos: 2
```


## Interpretación del resultado

El `Set` evita doble conteo de códigos únicos; el orden de sus elementos no forma parte de la promesa de `HashSet`. Compara tu predicción con las líneas concretas de la consola; si no coinciden, revisa primero el orden de las llamadas que cambian los datos.

## Variación controlada

Añade `codigos.add("DNI300");` y comprueba que el total pasa a 3. Explica cuál cambió el estado y qué elemento siguió conservándose.

## Error o caso límite y corrección razonada

Intentar `codigos.get(0)` no compila: `Set` no ofrece acceso por índice. Para verificar presencia, usa `contains`; para recorrido, `for-each` sin asumir un orden. Haz la prueba únicamente en una copia de tu archivo o revierte el cambio antes de seguir.


### Laboratorio de razonamiento adicional — add informa si el Set ha cambiado

**Antes de pasar a la tarea espejo, reconstruye esta traza sin abrir la consola.**

| Acción | Estado observable | Consecuencia |
|---|---|---|
| add("DNI100") | {DNI100} | true |
| add("DNI200") | {DNI100, DNI200} | true |
| add("DNI100") repetido | mismos dos valores | false |

**Pregunta de transferencia:** ¿Se puede justificar el rechazo del repetido sin fiarse del orden de impresión?

**Verificación:** formula una explicación con tus palabras y contrástala con el estado anterior/después. Identifica qué operación sería incorrecta si el requisito cambiara.

**Prueba adicional:** predice qué cambiaría al repetir la operación decisiva una vez más; ejecuta después y vuelve al archivo original para evitar confundir los resultados posteriores.

## T03 — Tarea espejo: Controlar identificadores de inventario

**Enunciado:** Inserta P01, P02 y otra vez P01 en un conjunto. Muestra si la última inserción fue aceptada, si existe P02 y cuántos identificadores únicos quedaron.

**Archivo a crear:** `src/T03.java`, con clase pública `T03` y su propio `main`, tomando como referencia la estructura de clase que ya aprendiste.

**Restricción:** Usa `Set<String>` y `HashSet`; no imprimas el conjunto entero para comprobar orden.

**Pista:** Declara `boolean aceptado = productos.add("P01")` en el tercer intento; comprueba `contains` y `size`.

**Evidencia:** entrega código fuente y captura legible de la consola que coincida con estas líneas:

```text
Nuevo duplicado: false
Existe P02: true
Únicos: 2
```

**Cómo sabes que está correcta:** compila sin errores, reproduce la salida en el orden indicado y puedes explicar qué operación genera cada resultado. La solución completa de la tarea la reconstruirás tú.


---

# EJ04 — Ordenar automáticamente valores únicos con TreeSet

## Objetivo técnico — Qué vamos a hacer y qué aprenderemos

En un ejercicio numérico queremos registrar números primos sin duplicados y obtenerlos de menor a mayor aunque hayan llegado desordenados. Necesitaremos una implementación diferente de `Set`: `TreeSet`, que mantiene los elementos conforme a su orden natural. Declararemos el conjunto, agregaremos cinco valores, incluidos dos treces, e imprimiremos el resultado. La salida mostrará únicamente cuatro números ordenados. Así podremos comparar `HashSet`, usado para verificar unicidad sin prometer orden, con `TreeSet`, elegido cuando la ordenación forma parte de la necesidad.

## Qué problema concreto resolveremos

Una lista mantendría el 13 repetido y el orden de llegada; aquí se pide una secuencia única y ordenada.

## Archivos y punto de partida

Crea `src/EJ04.java` en IntelliJ, sin declaración `package`, o guárdalo como `EJ04.java` en la carpeta del laboratorio. Este ejemplo es independiente de los anteriores; se inicia con su archivo vacío. Los `import` se colocan **antes** de `public class`, y las instrucciones de los pasos siguientes van **dentro de `main`**, entre sus llaves. No compiles un archivo a medio construir.

### Paso 1 — Abrir una clase ejecutable y declarar las importaciones

**Antes de escribir:** necesitamos que Java encuentre las interfaces y clases estándar usadas en este ejemplo. En la parte superior del archivo escribe estas importaciones; debajo crea el envoltorio de clase. La clase pública tiene exactamente el mismo nombre que el archivo, condición indispensable para compilar sin errores.

```java
import java.util.Set;
import java.util.TreeSet;

public class EJ04 {
    public static void main(String[] args) {
        // Aquí construiremos las instrucciones de los pasos 2 en adelante.
    }
}
```

**Mientras escribimos:** `import` permite utilizar el nombre corto de cada tipo; `public class` declara la clase; `main(String[] args)` es el punto de ejecución; `System.out.println` imprimirá mensajes cuando lo agreguemos. La línea de comentario es solo una marca temporal: elimínala antes de insertar el primer fragmento.

**Validación intermedia:** puedes compilar esta estructura vacía, pero todavía no muestra datos; las salidas aparecerán cuando agreguemos las operaciones.

### Paso 2 — Elegir TreeSet porque ahora importa el orden

**Para comprender antes de escribir:** La regla de unicidad sigue vigente, pero agregamos una necesidad que el ejemplo anterior no tenía: mostrar los números en orden ascendente. Mantenemos la interfaz `Set<Integer>` y cambiamos la implementación concreta a `TreeSet`. `Integer` es el tipo objeto usado para números enteros.

**Dónde y qué modificar:** en `src/EJ04.java`, dentro de `main`, inserta estas sentencias después del último bloque incorporado; la primera vez colócalas donde retiraste el comentario temporal. Mantén abiertos únicamente los delimitadores que muestre el fragmento, y conserva todas las sentencias anteriores.

```java
Set<Integer> numerosPrimos = new TreeSet<>();
```

**Mientras lo construimos, comprendamos cada parte:** `Set<Integer>` indica un conjunto cuyos valores son enteros; `TreeSet` ordena dichos enteros por su orden natural de menor a mayor. Declarar contra la interfaz conserva el sentido de «conjunto» aunque cambiemos la implementación.

**Estado antes → después:** Estado inicial: `{}` sin números.

**Por qué avanzamos:** Probaremos que el orden final no depende del orden en que llamemos `add`.

### Paso 3 — Insertar valores desordenados y repetir el trece

**Para comprender antes de escribir:** Los primos llegan 17, 5, 13, 7 y nuevamente 13. Cada `add` ofrece un candidato; el segundo 13 no crea una nueva entrada. El conjunto reorganiza internamente sus elementos de acuerdo con la ordenación natural de `Integer`.

**Dónde y qué modificar:** en `src/EJ04.java`, dentro de `main`, inserta estas sentencias después del último bloque incorporado; la primera vez colócalas donde retiraste el comentario temporal. Mantén abiertos únicamente los delimitadores que muestre el fragmento, y conserva todas las sentencias anteriores.

```java
numerosPrimos.add(17);
numerosPrimos.add(5);
numerosPrimos.add(13);
numerosPrimos.add(7);
numerosPrimos.add(13);
```

**Mientras lo construimos, comprendamos cada parte:** El conjunto no conserva cinco registros: conserva solo los valores distintos 5, 7, 13 y 17. La palabra «primos» describe estos datos de prueba; la colección no calcula primalidad ni verifica matemáticamente que cada valor sea primo.

**Estado antes → después:** Estado lógico ordenado: `[5, 7, 13, 17]`.

**Por qué avanzamos:** Necesitamos imprimir el conjunto para comprobar simultáneamente la unicidad y el orden.

### Paso 4 — Mostrar los números ordenados

**Para comprender antes de escribir:** La prueba decisiva es imprimir la colección completa, no consultar un índice. La salida debe reflejar el orden que mantiene `TreeSet` sin necesidad de invocar un método de ordenamiento adicional.

**Dónde y qué modificar:** en `src/EJ04.java`, dentro de `main`, inserta estas sentencias después del último bloque incorporado; la primera vez colócalas donde retiraste el comentario temporal. Mantén abiertos únicamente los delimitadores que muestre el fragmento, y conserva todas las sentencias anteriores.

```java
System.out.println("Primos ordenados: " + numerosPrimos);
```

**Mientras lo construimos, comprendamos cada parte:** Cuando concatenamos el conjunto con el texto, Java construye su representación textual. En este caso muestra 5 antes que 7, 13 y 17. El 13 duplicado no aparece porque `Set` conserva valores únicos.

**Estado antes → después:** Salida exacta: `Primos ordenados: [5, 7, 13, 17]`.

**Por qué avanzamos:** Después pasaremos a una necesidad distinta: recuperar un valor a partir de una clave, en lugar de solo guardar elementos.

## Auditoría del archivo construido

Comprueba que las importaciones están fuera de la clase, que existe una única clase pública con nombre igual al archivo, que las operaciones aparecen dentro de `main` y que los fragmentos de los pasos 2 en adelante conservan el orden mostrado. El listado siguiente es la **versión acumulada** de esos pasos, no una segunda implementación con código adicional.

## Archivo completo al terminar el ejemplo

```java
import java.util.Set;
import java.util.TreeSet;

public class EJ04 {
    public static void main(String[] args) {
        Set<Integer> numerosPrimos = new TreeSet<>();
        numerosPrimos.add(17);
        numerosPrimos.add(5);
        numerosPrimos.add(13);
        numerosPrimos.add(7);
        numerosPrimos.add(13);
        System.out.println("Primos ordenados: " + numerosPrimos);
    }
}
```


## Antes de ejecutar: predicción

1. ¿El primer valor que se imprime será 17 o 5?
2. ¿Cuántas veces aparecerá 13?
3. ¿Qué diferencia a `TreeSet` de `HashSet` en esta demostración?

## Ejecutar y validar

En IntelliJ abre `src/EJ04.java` y ejecuta el botón junto a `main`. En terminal, desde la carpeta donde guardaste el archivo, ejecuta:

```bash
javac -encoding UTF-8 EJ04.java
java EJ04
```

**Salida esperada:**

```text
Primos ordenados: [5, 7, 13, 17]
```


## Interpretación del resultado

`TreeSet` resuelve dos requisitos simultáneos: unicidad y orden natural. Compara tu predicción con las líneas concretas de la consola; si no coinciden, revisa primero el orden de las llamadas que cambian los datos.

## Variación controlada

Añade `numerosPrimos.add(3);` y comprueba que el resultado comienza con 3. Explica cuál cambió el estado y qué elemento siguió conservándose.

## Error o caso límite y corrección razonada

Si cambias `Integer` por un tipo no compatible con el orden natural sin definir un comparador, `TreeSet` no puede ordenarlo adecuadamente. En esta sesión utiliza `Integer` o `String` y deja los comparadores para otro tema. Haz la prueba únicamente en una copia de tu archivo o revierte el cambio antes de seguir.


### Laboratorio de razonamiento adicional — Orden de inserción frente a orden natural

**Antes de pasar a la tarea espejo, reconstruye esta traza sin abrir la consola.**

| Acción | Estado observable | Consecuencia |
|---|---|---|
| Insertar 17,5,13,7 | valores únicos | 4 |
| Insertar 13 otra vez | mismos valores | 4 |
| Mostrar TreeSet | [5, 7, 13, 17] | ascendente |

**Pregunta de transferencia:** ¿Ordena TreeSet porque Java ejecutó una llamada sort?

**Verificación:** formula una explicación con tus palabras y contrástala con el estado anterior/después. Identifica qué operación sería incorrecta si el requisito cambiara.

**Prueba adicional:** predice qué cambiaría al repetir la operación decisiva una vez más; ejecuta después y vuelve al archivo original para evitar confundir los resultados posteriores.

## T04 — Tarea espejo: Mantener edades únicas ordenadas

**Enunciado:** Registra las edades 22, 18, 20 y nuevamente 18. Imprime la colección de edades únicas en orden natural ascendente.

**Archivo a crear:** `src/T04.java`, con clase pública `T04` y su propio `main`, tomando como referencia la estructura de clase que ya aprendiste.

**Restricción:** No apliques `sort` ni cambies a una lista.

**Pista:** Usa `Set<Integer>` implementado con `TreeSet<Integer>`; inserta los cuatro valores y muestra el conjunto.

**Evidencia:** entrega código fuente y captura legible de la consola que coincida con estas líneas:

```text
Edades: [18, 20, 22]
```

**Cómo sabes que está correcta:** compila sin errores, reproduce la salida en el orden indicado y puedes explicar qué operación genera cada resultado. La solución completa de la tarea la reconstruirás tú.


---

# EJ05 — Consultar y actualizar carreras mediante Map y HashMap

## Objetivo técnico — Qué vamos a hacer y qué aprenderemos

Un catálogo académico utiliza códigos numéricos: al ingresar un código, el sistema debe devolver el nombre de la carrera. En esta situación no buscamos la posición de un nombre dentro de una lista, sino la asociación entre una clave y un valor. Crearemos `Map<Integer,String>` mediante `HashMap`, registraremos tres carreras y corregiremos el nombre asociado al código 3 usando nuevamente `put`. Luego mostraremos la carrera 3, verificaremos si existe la clave 4 y contaremos las claves almacenadas. La salida comprobará que volver a utilizar una clave reemplaza su valor, no agrega una segunda entrada con la misma clave.

## Qué problema concreto resolveremos

Para recuperar la carrera número 3 necesitamos una relación explícita entre el código y su descripción.

## Archivos y punto de partida

Crea `src/EJ05.java` en IntelliJ, sin declaración `package`, o guárdalo como `EJ05.java` en la carpeta del laboratorio. Este ejemplo es independiente de los anteriores; se inicia con su archivo vacío. Los `import` se colocan **antes** de `public class`, y las instrucciones de los pasos siguientes van **dentro de `main`**, entre sus llaves. No compiles un archivo a medio construir.

### Paso 1 — Abrir una clase ejecutable y declarar las importaciones

**Antes de escribir:** necesitamos que Java encuentre las interfaces y clases estándar usadas en este ejemplo. En la parte superior del archivo escribe estas importaciones; debajo crea el envoltorio de clase. La clase pública tiene exactamente el mismo nombre que el archivo, condición indispensable para compilar sin errores.

```java
import java.util.Map;
import java.util.HashMap;

public class EJ05 {
    public static void main(String[] args) {
        // Aquí construiremos las instrucciones de los pasos 2 en adelante.
    }
}
```

**Mientras escribimos:** `import` permite utilizar el nombre corto de cada tipo; `public class` declara la clase; `main(String[] args)` es el punto de ejecución; `System.out.println` imprimirá mensajes cuando lo agreguemos. La línea de comentario es solo una marca temporal: elimínala antes de insertar el primer fragmento.

**Validación intermedia:** puedes compilar esta estructura vacía, pero todavía no muestra datos; las salidas aparecerán cuando agreguemos las operaciones.

### Paso 2 — Crear un diccionario de códigos y carreras

**Para comprender antes de escribir:** No basta con saber que existen nombres de carreras; necesitamos asociarlos con códigos para consultarlos después. La interfaz `Map<K,V>` modela pares clave-valor y `HashMap` es la implementación concreta elegida. `Map` pertenece al JCF, pero no extiende `Collection`.

**Dónde y qué modificar:** en `src/EJ05.java`, dentro de `main`, inserta estas sentencias después del último bloque incorporado; la primera vez colócalas donde retiraste el comentario temporal. Mantén abiertos únicamente los delimitadores que muestre el fragmento, y conserva todas las sentencias anteriores.

```java
Map<Integer, String> carreras = new HashMap<>();
```

**Mientras lo construimos, comprendamos cada parte:** `Integer` especifica el tipo de clave, `String` el tipo del valor. `carreras` identifica el mapa vacío. A diferencia de `List` y `Set`, para insertar utilizaremos `put(clave, valor)` en lugar de `add`.

**Estado antes → después:** Estado inicial: ninguna clave asociada.

**Por qué avanzamos:** Ahora crearemos tres asociaciones con códigos distintos.

### Paso 3 — Relacionar códigos con nombres

**Para comprender antes de escribir:** Cada llamada a `put` incorpora una pareja. Guardaremos Informática bajo 1, Economía bajo 2 y Arquitectura bajo 3. Las claves identifican los registros; sus valores son los textos que el usuario necesita recuperar.

**Dónde y qué modificar:** en `src/EJ05.java`, dentro de `main`, inserta estas sentencias después del último bloque incorporado; la primera vez colócalas donde retiraste el comentario temporal. Mantén abiertos únicamente los delimitadores que muestre el fragmento, y conserva todas las sentencias anteriores.

```java
carreras.put(1, "Informática");
carreras.put(2, "Economía");
carreras.put(3, "Arquitectura");
```

**Mientras lo construimos, comprendamos cada parte:** `put(1, "Informática")` crea la asociación 1→Informática, y las otras dos llamadas hacen lo mismo con 2 y 3. No estamos determinando posiciones; no debe asumirse que la iteración de un `HashMap` respeta el orden de inserción.

**Estado antes → después:** Estado: tres claves únicas, cada una con una carrera.

**Por qué avanzamos:** A continuación simularemos una corrección de nombre sin cambiar el código.

### Paso 4 — Actualizar el valor de una clave existente

**Para comprender antes de escribir:** La carrera correspondiente al código 3 ha sido renombrada. Usaremos `put` con la misma clave para modificar la asociación ya existente. El mapa no duplica claves: reemplaza el valor anterior de esa clave.

**Dónde y qué modificar:** en `src/EJ05.java`, dentro de `main`, inserta estas sentencias después del último bloque incorporado; la primera vez colócalas donde retiraste el comentario temporal. Mantén abiertos únicamente los delimitadores que muestre el fragmento, y conserva todas las sentencias anteriores.

```java
carreras.put(3, "Diseño");
```

**Mientras lo construimos, comprendamos cada parte:** El entero 3 ya está presente, por lo que `put` actualiza su valor desde Arquitectura hasta Diseño. `carreras.size()` continuará devolviendo 3, porque siguen existiendo los códigos 1, 2 y 3, aunque uno de sus valores cambió.

**Estado antes → después:** Estado: 1→Informática, 2→Economía y 3→Diseño; tres claves.

**Por qué avanzamos:** Falta consultar la carrera actualizada y comprobar si existe otra clave.

### Paso 5 — Consultar por clave y confirmar su ausencia

**Para comprender antes de escribir:** El sistema debe mostrar el nombre asociado al código solicitado y distinguir una clave que no fue registrada. `get(3)` recupera el valor actual; `containsKey(4)` devuelve si existe el código 4; `size()` cuenta pares almacenados.

**Dónde y qué modificar:** en `src/EJ05.java`, dentro de `main`, inserta estas sentencias después del último bloque incorporado; la primera vez colócalas donde retiraste el comentario temporal. Mantén abiertos únicamente los delimitadores que muestre el fragmento, y conserva todas las sentencias anteriores.

```java
System.out.println("Carrera 3: " + carreras.get(3));
System.out.println("Existe 4: " + carreras.containsKey(4));
System.out.println("Total claves: " + carreras.size());
```

**Mientras lo construimos, comprendamos cada parte:** `get(3)` devuelve Diseño después de la actualización. `containsKey(4)` es `false` porque solo registramos 1, 2 y 3. `size()` devuelve 3. Evitamos imprimir el mapa completo: el orden de las claves en `HashMap` no está garantizado.

**Estado antes → después:** La consola confirma el valor corregido, la ausencia de la clave 4 y el total 3.

**Por qué avanzamos:** Integraremos ahora estas tres estructuras en un registro académico que tiene necesidades diferentes.

## Auditoría del archivo construido

Comprueba que las importaciones están fuera de la clase, que existe una única clase pública con nombre igual al archivo, que las operaciones aparecen dentro de `main` y que los fragmentos de los pasos 2 en adelante conservan el orden mostrado. El listado siguiente es la **versión acumulada** de esos pasos, no una segunda implementación con código adicional.

## Archivo completo al terminar el ejemplo

```java
import java.util.Map;
import java.util.HashMap;

public class EJ05 {
    public static void main(String[] args) {
        Map<Integer, String> carreras = new HashMap<>();
        carreras.put(1, "Informática");
        carreras.put(2, "Economía");
        carreras.put(3, "Arquitectura");
        carreras.put(3, "Diseño");
        System.out.println("Carrera 3: " + carreras.get(3));
        System.out.println("Existe 4: " + carreras.containsKey(4));
        System.out.println("Total claves: " + carreras.size());
    }
}
```


## Antes de ejecutar: predicción

1. Después del segundo `put(3, ...)`, ¿qué devuelve `get(3)`?
2. ¿El tamaño será 3 o 4?
3. ¿Qué responde `containsKey(4)`?

## Ejecutar y validar

En IntelliJ abre `src/EJ05.java` y ejecuta el botón junto a `main`. En terminal, desde la carpeta donde guardaste el archivo, ejecuta:

```bash
javac -encoding UTF-8 EJ05.java
java EJ05
```

**Salida esperada:**

```text
Carrera 3: Diseño
Existe 4: false
Total claves: 3
```


## Interpretación del resultado

La unicidad en un `Map` corresponde a las claves; varias claves sí pueden apuntar a valores iguales. Compara tu predicción con las líneas concretas de la consola; si no coinciden, revisa primero el orden de las llamadas que cambian los datos.

## Variación controlada

Agrega `carreras.put(4, "Medicina");` y comprueba que `containsKey(4)` cambia a `true` y el tamaño a 4. Explica cuál cambió el estado y qué elemento siguió conservándose.

## Error o caso límite y corrección razonada

Escribir `carreras.add(4, "Medicina")` no compila: `Map` usa `put`, no `add`. Corrige a `carreras.put(4, "Medicina")`. `get` de una clave ausente devuelve `null` cuando el mapa no contiene dicha clave. Haz la prueba únicamente en una copia de tu archivo o revierte el cambio antes de seguir.


### Laboratorio de razonamiento adicional — Claves únicas, valores sustituibles

**Antes de pasar a la tarea espejo, reconstruye esta traza sin abrir la consola.**

| Acción | Estado observable | Consecuencia |
|---|---|---|
| put(1, Informática) | 1→Informática | 1 clave |
| put(2, Economía), put(3, Arquitectura) | tres asociaciones | 3 claves |
| put(3, Diseño) | 3→Diseño | sigue habiendo 3 claves |

**Pregunta de transferencia:** ¿Por qué get(3) imprime Diseño y no Arquitectura?

**Verificación:** formula una explicación con tus palabras y contrástala con el estado anterior/después. Identifica qué operación sería incorrecta si el requisito cambiara.

**Prueba adicional:** predice qué cambiaría al repetir la operación decisiva una vez más; ejecuta después y vuelve al archivo original para evitar confundir los resultados posteriores.

## T05 — Tarea espejo: Mantener un catálogo de cursos por código

**Enunciado:** Crea un mapa con 10→Computación y 20→Diseño. Actualiza la clave 20 a Diseño Digital. Imprime su valor, el número total de claves y si existe la clave 99.

**Archivo a crear:** `src/T05.java`, con clase pública `T05` y su propio `main`, tomando como referencia la estructura de clase que ya aprendiste.

**Restricción:** No crees dos claves 20 ni uses `List` para simular un mapa.

**Pista:** Declara `Map<Integer,String>`, usa `put` tres veces, y consulta `get(20)`, `size()` y `containsKey(99)`.

**Evidencia:** entrega código fuente y captura legible de la consola que coincida con estas líneas:

```text
Curso 20: Diseño Digital
Claves: 2
Existe 99: false
```

**Cómo sabes que está correcta:** compila sin errores, reproduce la salida en el orden indicado y puedes explicar qué operación genera cada resultado. La solución completa de la tarea la reconstruirás tú.


---

# EJ06 — Integrar List, TreeSet y HashMap en un registro académico

## Objetivo técnico — Qué vamos a hacer y qué aprenderemos

La feria académica necesita responder tres preguntas que no se resuelven igual: cuántas inscripciones hubo aunque alguna persona se repita, qué participantes distintos asistieron y cómo consultar una carrera mediante su código. Construiremos una lista de inscripciones, un `TreeSet` que reúna participantes sin duplicados y un `HashMap` de carreras. Después usaremos un `for-each` para copiar los nombres de la lista al conjunto y ejecutaremos tres consultas. Si vemos cuatro inscripciones, tres personas únicas ordenadas y la carrera correspondiente al código 2, habremos elegido cada colección según el requisito, no por preferencia de sintaxis.

## Qué problema concreto resolveremos

Intentar usar una sola colección para todas las necesidades provocaría pérdida de inscripciones, falta de orden alfabético o consultas por clave innecesariamente complejas.

## Archivos y punto de partida

Crea `src/EJ06.java` en IntelliJ, sin declaración `package`, o guárdalo como `EJ06.java` en la carpeta del laboratorio. Este ejemplo es independiente de los anteriores; se inicia con su archivo vacío. Los `import` se colocan **antes** de `public class`, y las instrucciones de los pasos siguientes van **dentro de `main`**, entre sus llaves. No compiles un archivo a medio construir.

### Paso 1 — Abrir una clase ejecutable y declarar las importaciones

**Antes de escribir:** necesitamos que Java encuentre las interfaces y clases estándar usadas en este ejemplo. En la parte superior del archivo escribe estas importaciones; debajo crea el envoltorio de clase. La clase pública tiene exactamente el mismo nombre que el archivo, condición indispensable para compilar sin errores.

```java
import java.util.List;
import java.util.ArrayList;
import java.util.Set;
import java.util.TreeSet;
import java.util.Map;
import java.util.HashMap;

public class EJ06 {
    public static void main(String[] args) {
        // Aquí construiremos las instrucciones de los pasos 2 en adelante.
    }
}
```

**Mientras escribimos:** `import` permite utilizar el nombre corto de cada tipo; `public class` declara la clase; `main(String[] args)` es el punto de ejecución; `System.out.println` imprimirá mensajes cuando lo agreguemos. La línea de comentario es solo una marca temporal: elimínala antes de insertar el primer fragmento.

**Validación intermedia:** puedes compilar esta estructura vacía, pero todavía no muestra datos; las salidas aparecerán cuando agreguemos las operaciones.

### Paso 2 — Guardar inscripciones sin perder la repetición

**Para comprender antes de escribir:** La feria recibe cuatro registros. Juana aparece dos veces y no debemos borrarla porque cada entrada es una inscripción válida. Por eso comenzamos con `List<String>` y `ArrayList`, la combinación que ya comprobamos para conservar el orden y los repetidos.

**Dónde y qué modificar:** en `src/EJ06.java`, dentro de `main`, inserta estas sentencias después del último bloque incorporado; la primera vez colócalas donde retiraste el comentario temporal. Mantén abiertos únicamente los delimitadores que muestre el fragmento, y conserva todas las sentencias anteriores.

```java
List<String> inscripciones = new ArrayList<>();
inscripciones.add("Juana");
inscripciones.add("Luis");
inscripciones.add("Juana");
inscripciones.add("Omar");
```

**Mientras lo construimos, comprendamos cada parte:** Las cuatro llamadas a `add` agregan cuatro posiciones: Juana, Luis, Juana y Omar. La lista representa eventos de registro, no un censo único de personas. Su `size()` sería 4 aunque Juana se repita.

**Estado antes → después:** Estado: `[Juana, Luis, Juana, Omar]`.

**Por qué avanzamos:** Para obtener asistentes distintos necesitamos una segunda colección con otra regla.

### Paso 3 — Construir el conjunto de participantes únicos

**Para comprender antes de escribir:** La lista conserva datos que deben permanecer intactos; no la convertiremos en un conjunto porque perderíamos información sobre duplicados. En su lugar, declaramos un `TreeSet<String>` y recorremos las inscripciones. Cada nombre intentará entrar en el conjunto y los repetidos no crearán nuevas entradas.

**Dónde y qué modificar:** en `src/EJ06.java`, dentro de `main`, inserta estas sentencias después del último bloque incorporado; la primera vez colócalas donde retiraste el comentario temporal. Mantén abiertos únicamente los delimitadores que muestre el fragmento, y conserva todas las sentencias anteriores.

```java
Set<String> participantes = new TreeSet<>();
for (String nombre : inscripciones) {
    participantes.add(nombre);
}
```

**Mientras lo construimos, comprendamos cada parte:** `for-each` entrega cada elemento de `inscripciones` en el orden de la lista. `participantes.add(nombre)` agrega Juana, luego Luis; la segunda Juana es ignorada por unicidad, y Omar se incorpora. `TreeSet` mantiene al final los tres nombres ordenados alfabéticamente según el orden natural de `String`.

**Estado antes → después:** Estado: `[Juana, Luis, Omar]` sin borrar ninguno de los cuatro registros originales.

**Por qué avanzamos:** Ya podemos responder a las dos primeras necesidades, pero falta consultar carreras mediante un código.

### Paso 4 — Registrar las carreras por su identificador

**Para comprender antes de escribir:** Para una consulta directa por código no necesitamos recorrer nombres. Usaremos `Map<Integer,String>` para asociar cada código académico con su carrera. El ejemplo incluye tres códigos, suficientes para demostrar recuperación del código 2.

**Dónde y qué modificar:** en `src/EJ06.java`, dentro de `main`, inserta estas sentencias después del último bloque incorporado; la primera vez colócalas donde retiraste el comentario temporal. Mantén abiertos únicamente los delimitadores que muestre el fragmento, y conserva todas las sentencias anteriores.

```java
Map<Integer, String> carreras = new HashMap<>();
carreras.put(1, "Informática");
carreras.put(2, "Economía");
carreras.put(3, "Arquitectura");
```

**Mientras lo construimos, comprendamos cada parte:** Los enteros 1, 2 y 3 son claves únicas; los textos son sus carreras. `put` añade asociaciones independientes de la lista y el conjunto. `get(2)` permitirá obtener Economía sin referirse a la posición 2 de ninguna lista.

**Estado antes → después:** Estado del mapa: 1→Informática, 2→Economía, 3→Arquitectura.

**Por qué avanzamos:** Solo falta escribir una salida que haga visibles las tres responsabilidades.

### Paso 5 — Comprobar las tres respuestas del sistema

**Para comprender antes de escribir:** Para demostrar que el diseño no mezcla responsabilidades imprimiremos la lista, el conjunto y el nombre de la carrera con código 2. Observa que cada impresión representa una pregunta distinta: entradas recibidas, participantes distintos y dato recuperado mediante clave.

**Dónde y qué modificar:** en `src/EJ06.java`, dentro de `main`, inserta estas sentencias después del último bloque incorporado; la primera vez colócalas donde retiraste el comentario temporal. Mantén abiertos únicamente los delimitadores que muestre el fragmento, y conserva todas las sentencias anteriores.

```java
System.out.println("Inscripciones: " + inscripciones);
System.out.println("Participantes: " + participantes);
System.out.println("Carrera 2: " + carreras.get(2));
```

**Mientras lo construimos, comprendamos cada parte:** `inscripciones` muestra cuatro entradas con Juana repetida. `participantes` muestra tres nombres únicos ordenados por `TreeSet`. `carreras.get(2)` devuelve Economía porque 2 es la clave del mapa, no un índice de la lista.

**Estado antes → después:** Resultado integrado: cuatro inscripciones, tres participantes y carrera 2 Economía.

**Por qué avanzamos:** Al terminar, justificaremos en voz alta por qué cada estructura era la adecuada para su necesidad.

## Auditoría del archivo construido

Comprueba que las importaciones están fuera de la clase, que existe una única clase pública con nombre igual al archivo, que las operaciones aparecen dentro de `main` y que los fragmentos de los pasos 2 en adelante conservan el orden mostrado. El listado siguiente es la **versión acumulada** de esos pasos, no una segunda implementación con código adicional.

## Archivo completo al terminar el ejemplo

```java
import java.util.List;
import java.util.ArrayList;
import java.util.Set;
import java.util.TreeSet;
import java.util.Map;
import java.util.HashMap;

public class EJ06 {
    public static void main(String[] args) {
        List<String> inscripciones = new ArrayList<>();
        inscripciones.add("Juana");
        inscripciones.add("Luis");
        inscripciones.add("Juana");
        inscripciones.add("Omar");
        Set<String> participantes = new TreeSet<>();
        for (String nombre : inscripciones) {
            participantes.add(nombre);
        }
        Map<Integer, String> carreras = new HashMap<>();
        carreras.put(1, "Informática");
        carreras.put(2, "Economía");
        carreras.put(3, "Arquitectura");
        System.out.println("Inscripciones: " + inscripciones);
        System.out.println("Participantes: " + participantes);
        System.out.println("Carrera 2: " + carreras.get(2));
    }
}
```


## Antes de ejecutar: predicción

1. ¿En qué salida aparecerá Juana dos veces?
2. ¿Por qué los participantes se verán alfabéticamente?
3. ¿Qué estructura responde directamente la consulta del código 2?

## Ejecutar y validar

En IntelliJ abre `src/EJ06.java` y ejecuta el botón junto a `main`. En terminal, desde la carpeta donde guardaste el archivo, ejecuta:

```bash
javac -encoding UTF-8 EJ06.java
java EJ06
```

**Salida esperada:**

```text
Inscripciones: [Juana, Luis, Juana, Omar]
Participantes: [Juana, Luis, Omar]
Carrera 2: Economía
```


## Interpretación del resultado

Cuando el requisito cambia, puede cambiar también la colección; en este diseño las tres estructuras no son redundantes. Compara tu predicción con las líneas concretas de la consola; si no coinciden, revisa primero el orden de las llamadas que cambian los datos.

## Variación controlada

Agrega `inscripciones.add("Ana");` antes del ciclo y observa que la lista crece y el conjunto incorpora un participante distinto al inicio del orden natural. Explica cuál cambió el estado y qué elemento siguió conservándose.

## Error o caso límite y corrección razonada

Si intentas consultar `inscripciones.get(2)` para recuperar la carrera 2, obtendrás Juana: una posición en List no equivale a una clave en Map. La consulta correcta es `carreras.get(2)`. Haz la prueba únicamente en una copia de tu archivo o revierte el cambio antes de seguir.


### Laboratorio de razonamiento adicional — Tres preguntas, tres contratos de datos

**Antes de pasar a la tarea espejo, reconstruye esta traza sin abrir la consola.**

| Acción | Estado observable | Consecuencia |
|---|---|---|
| Registro recibido | [Juana, Luis, Juana, Omar] | List registra 4 |
| Participantes distintos | [Juana, Luis, Omar] | TreeSet reúne 3 |
| Consultar carrera por clave | 2→Economía | Map resuelve 1 búsqueda |

**Pregunta de transferencia:** ¿Podemos reemplazar las tres colecciones por un único Set sin perder información?

**Verificación:** formula una explicación con tus palabras y contrástala con el estado anterior/después. Identifica qué operación sería incorrecta si el requisito cambiara.

**Prueba adicional:** predice qué cambiaría al repetir la operación decisiva una vez más; ejecuta después y vuelve al archivo original para evitar confundir los resultados posteriores.

## T06 — Tarea espejo: Integrar inscripciones, participantes y cursos

**Enunciado:** Crea una lista de inscripciones Eva, Raúl y Eva. Construye un TreeSet con las personas únicas y un HashMap con 100→Java y 200→Base de Datos. Muestra la lista, el conjunto y el nombre del curso 200.

**Archivo a crear:** `src/T06.java`, con clase pública `T06` y su propio `main`, tomando como referencia la estructura de clase que ya aprendiste.

**Restricción:** Mantén una sola clase y tres colecciones con responsabilidades distintas.

**Pista:** Recorre la lista con `for-each` para cargar el `TreeSet`; consulta el mapa mediante `get(200)`.

**Evidencia:** entrega código fuente y captura legible de la consola que coincida con estas líneas:

```text
Inscripciones: [Eva, Raúl, Eva]
Participantes: [Eva, Raúl]
Curso 200: Base de Datos
```

**Cómo sabes que está correcta:** compila sin errores, reproduce la salida en el orden indicado y puedes explicar qué operación genera cada resultado. La solución completa de la tarea la reconstruirás tú.

---


---

# EJ07 — Insertar en medio de una LinkedList y retirar un turno

## Objetivo técnico — qué vamos a hacer y qué aprenderemos

En una ventanilla se respeta una secuencia de atención, pero puede aparecer una reserva que debe ubicarse entre dos registros. Construiremos una lista vinculada mediante la interfaz List y la implementación LinkedList. Primero registraremos tres turnos, después insertaremos a Sara en la posición 1 y finalmente retiraremos a Luis por su nombre. El caso permite interpretar con precisión los índices en el momento de insertar y comprobar que las otras personas conservan su posición relativa. No afirmaremos que una LinkedList sea siempre mejor: aquí se utiliza para conocer otra implementación válida de List.

## Qué problema concreto resolveremos

Una reserva nueva debe aparecer en una posición exacta; concatenarla al final no responde al orden de atención definido.

## Archivos y punto de partida

Crea `src/EJ07.java` y escribe la clase pública `EJ07`. Parte de un archivo nuevo, no del resultado del ejemplo anterior: así los cambios serán independientes. Primero se añaden los imports y la clase; después cada microbloque dentro de `main`.

## Paso 1 — Preparar importaciones y punto de entrada

En esta demostración necesitamos tipos específicos de `java.util`, no dependencias externas. Escribe la estructura siguiente al inicio de la clase. Dentro de `main` iremos agregando los bloques por orden.

```java
import java.util.List;
import java.util.LinkedList;

public class EJ07 {
    public static void main(String[] args) {
        // Inserta aquí los próximos bloques.
    }
}
```
**Comprobación inicial:** el archivo todavía no tiene resultados. `main` define dónde comienza la ejecución; el nombre público debe coincidir con el del archivo.

## Paso 2 — Elegir la interfaz List y la implementación vinculada

**Por qué lo hacemos ahora:** La referencia List expresa las operaciones disponibles, mientras LinkedList determina la representación concreta. Antes de escribir, señala en qué estado está la colección y qué cambio esperamos observar.

**Acción:** dentro de `main`, después del último fragmento ya creado, agrega exactamente este bloque (sin duplicar las llaves externas de la clase):

```java
List<String> turnos = new LinkedList<>();
```
**Qué hace y por qué:** La referencia List expresa las operaciones disponibles, mientras LinkedList determina la representación concreta. El tipo String impide añadir accidentalmente números.

**Traza antes/después:** Antes: no existe una lista. Después: turnos=[]

**Predicción parcial:** ¿Para imprimir tres turnos, necesitamos tres variables? **Comprueba tu razonamiento:** No; una colección permite almacenar varios textos y crecer.

## Paso 3 — Cargar los turnos iniciales

**Por qué lo hacemos ahora:** Las llamadas add sin índice anexan por el final. Antes de escribir, señala en qué estado está la colección y qué cambio esperamos observar.

**Acción:** dentro de `main`, después del último fragmento ya creado, agrega exactamente este bloque (sin duplicar las llaves externas de la clase):

```java
turnos.add("Marta");
turnos.add("Luis");
turnos.add("Ana");
```
**Qué hace y por qué:** Las llamadas add sin índice anexan por el final. Los índices temporales son 0=Marta, 1=Luis, 2=Ana. Esta correspondencia es necesaria para decidir dónde incorporar la reserva.

**Traza antes/después:** Antes: []. Después: [Marta, Luis, Ana]

**Predicción parcial:** ¿Qué nombre está en el índice 1 ahora? **Comprueba tu razonamiento:** Luis, porque las posiciones comienzan en 0.

## Paso 4 — Insertar en una posición concreta

**Por qué lo hacemos ahora:** La sobrecarga add(indice, elemento) inserta sin sustituir. Antes de escribir, señala en qué estado está la colección y qué cambio esperamos observar.

**Acción:** dentro de `main`, después del último fragmento ya creado, agrega exactamente este bloque (sin duplicar las llaves externas de la clase):

```java
turnos.add(1, "Sara");
```
**Qué hace y por qué:** La sobrecarga add(indice, elemento) inserta sin sustituir. Sara ocupa ahora la posición 1, y Luis y Ana se desplazan un lugar a la derecha. Se debe usar un índice entre 0 y size() inclusive para insertar.

**Traza antes/después:** Antes: [Marta, Luis, Ana]. Después: [Marta, Sara, Luis, Ana]

**Predicción parcial:** ¿Qué ocurre con Luis: desaparece o se mueve? **Comprueba tu razonamiento:** Se mueve al índice 2; no se pierde ningún registro.

## Paso 5 — Cancelar por valor y comprobar el orden

**Por qué lo hacemos ahora:** remove("Luis") busca el texto y elimina su primera coincidencia; no es remove(1), que elimina por índice. Antes de escribir, señala en qué estado está la colección y qué cambio esperamos observar.

**Acción:** dentro de `main`, después del último fragmento ya creado, agrega exactamente este bloque (sin duplicar las llaves externas de la clase):

```java
turnos.remove("Luis");
System.out.println("Turnos: " + turnos);
System.out.println("Primero: " + turnos.get(0));
```
**Qué hace y por qué:** remove("Luis") busca el texto y elimina su primera coincidencia; no es remove(1), que elimina por índice. La lista resultante conserva a Marta, Sara y Ana. get(0) solamente consulta.

**Traza antes/después:** Antes: [Marta, Sara, Luis, Ana]. Después: [Marta, Sara, Ana]

**Predicción parcial:** ¿Cuál sería el efecto de remove(1) en vez de remove("Luis")? **Comprueba tu razonamiento:** Eliminaría Sara, que ahora ocupa la posición 1.

## Auditoría del archivo terminado

| Elemento | Qué significa y qué aporta |
|---|---|
| `java.util.List` | Tipo estándar que necesita el ejemplo; su import permite utilizar el nombre corto. |
| `java.util.LinkedList` | Tipo estándar que necesita el ejemplo; su import permite utilizar el nombre corto. |
| `EJ07.main` | Ejecuta los bloques en el orden escrito. |
| Operaciones de colección | Cambian o inspeccionan el estado según se describe en cada microbloque. |

## Archivo completo al terminar el ejemplo

```java
import java.util.List;
import java.util.LinkedList;

public class EJ07 {
    public static void main(String[] args) {
        List<String> turnos = new LinkedList<>();
        turnos.add("Marta");
        turnos.add("Luis");
        turnos.add("Ana");
        turnos.add(1, "Sara");
        turnos.remove("Luis");
        System.out.println("Turnos: " + turnos);
        System.out.println("Primero: " + turnos.get(0));
    }
}
```
## Antes de ejecutar — predicción obligatoria

1. ¿Sara reemplaza a Luis o lo desplaza?
2. ¿Qué elemento se elimina al usar remove("Luis")?
3. ¿Qué nombre devuelve get(0) al final?

## Ejecución y resultado esperado

En IntelliJ utiliza **Run** en el `main` de `EJ07`. Si usas terminal, entra en la carpeta del `.java` y ejecuta:

```bash
javac -encoding UTF-8 EJ07.java
java EJ07
```

**Salida de referencia:**

```text
Turnos: [Marta, Sara, Ana]
Primero: Marta
```
**Interpretación:** lee la salida de izquierda a derecha y explica qué dato se conservó, cuál cambió y qué operación solo consultó. No generalices garantías de orden a HashSet o HashMap.

## Variación controlada

Agrega turnos.add(0, "Rosa") antes de eliminar a Luis. Describe el desplazamiento de los índices y predice la primera persona.

## Error frecuente y corrección

Si usas turnos.add(8, "Sara") cuando existen tres registros, Java lanza IndexOutOfBoundsException. Inserta entre 0 y size() (3 en ese momento) y vuelve a ejecutar.

## Demuestra que comprendiste

Sin consultar el código, explica por qué elegiste esta interfaz, qué clase instancia el objeto y cuál es la diferencia entre una operación que consulta y una que modifica la colección.

## T07 — Tarea espejo: Reordenar estaciones de una ruta

**Enunciado:** Registra Centro, Parque y Terminal en una LinkedList. Inserta Museo en la posición 1 y retira Parque por valor. Muestra la secuencia final y su primer elemento.

**Archivo:** `src/T07.java`, con `main` independiente. **Restricción:** no reemplaces la estructura por arreglos ni uses una operación ajena al contrato trabajado.

**Pista:** List<String> con LinkedList<>(); tres add; add(1, "Museo"); remove("Parque"); get(0).

**Antes de ejecutar:** escribe una predicción de cada línea. Debes mostrar exactamente lo siguiente:

```text
Estaciones: [Centro, Museo, Terminal]
Primera: Centro
```
**Evidencia:** archivo compilable, consola y una explicación de qué sentencia provocó cada cambio. **Criterio:** salida correcta + razonamiento del estado antes/después; el resultado no debe copiarse de la guía docente.


---

# EJ08 — Atender una fila con Queue y LinkedList

## Objetivo técnico — qué vamos a hacer y qué aprenderemos

Una mesa de ayuda registra solicitudes según su llegada. El requisito cambia: no basta con conservar nombres, ahora necesitamos identificar cuál será atendido y retirar ese primero. Usaremos la interfaz Queue y una LinkedList, que para este ejemplo permite un comportamiento de primero en entrar, primero en salir (FIFO). Insertaremos tres solicitudes con offer, examinaremos la primera con peek y retiraremos solo una mediante poll. La salida permitirá comprobar que mirar una solicitud no es lo mismo que atenderla.

## Qué problema concreto resolveremos

Una lista de usuarios no especifica por sí sola que la operación habitual debe atender siempre al primero.

## Archivos y punto de partida

Crea `src/EJ08.java` y escribe la clase pública `EJ08`. Parte de un archivo nuevo, no del resultado del ejemplo anterior: así los cambios serán independientes. Primero se añaden los imports y la clase; después cada microbloque dentro de `main`.

## Paso 1 — Preparar importaciones y punto de entrada

En esta demostración necesitamos tipos específicos de `java.util`, no dependencias externas. Escribe la estructura siguiente al inicio de la clase. Dentro de `main` iremos agregando los bloques por orden.

```java
import java.util.Queue;
import java.util.LinkedList;

public class EJ08 {
    public static void main(String[] args) {
        // Inserta aquí los próximos bloques.
    }
}
```
**Comprobación inicial:** el archivo todavía no tiene resultados. `main` define dónde comienza la ejecución; el nombre público debe coincidir con el del archivo.

## Paso 2 — Declarar una cola de solicitudes

**Por qué lo hacemos ahora:** Queue expresa el contrato de cola y LinkedList lo implementa. Antes de escribir, señala en qué estado está la colección y qué cambio esperamos observar.

**Acción:** dentro de `main`, después del último fragmento ya creado, agrega exactamente este bloque (sin duplicar las llaves externas de la clase):

```java
Queue<String> fila = new LinkedList<>();
```
**Qué hace y por qué:** Queue expresa el contrato de cola y LinkedList lo implementa. Los elementos de esta demostración son Strings. No usamos PriorityQueue: aquí no existen prioridades especiales; se necesita orden de llegada.

**Traza antes/después:** Antes: no existe fila. Después: cola vacía.

**Predicción parcial:** ¿La palabra Queue obliga a usar prioridades numéricas? **Comprueba tu razonamiento:** No. Esta implementación procesa primero al que llegó primero.

## Paso 3 — Registrar el orden de llegada

**Por qué lo hacemos ahora:** offer introduce elementos en la cola. Antes de escribir, señala en qué estado está la colección y qué cambio esperamos observar.

**Acción:** dentro de `main`, después del último fragmento ya creado, agrega exactamente este bloque (sin duplicar las llaves externas de la clase):

```java
fila.offer("Sara");
fila.offer("Luis");
fila.offer("Ana");
```
**Qué hace y por qué:** offer introduce elementos en la cola. Después de estas llamadas, Sara está al frente y Ana al final. Este estado es el que debemos imaginar antes de consultar o retirar.

**Traza antes/después:** Antes: []. Después: [Sara, Luis, Ana]

**Predicción parcial:** ¿Quién debe salir antes, Sara o Ana? **Comprueba tu razonamiento:** Sara, porque llegó primero.

## Paso 4 — Consultar sin retirar

**Por qué lo hacemos ahora:** peek consulta la cabeza y no la retira. Antes de escribir, señala en qué estado está la colección y qué cambio esperamos observar.

**Acción:** dentro de `main`, después del último fragmento ya creado, agrega exactamente este bloque (sin duplicar las llaves externas de la clase):

```java
System.out.println("Siguiente: " + fila.peek());
```
**Qué hace y por qué:** peek consulta la cabeza y no la retira. Aunque el mensaje muestra Sara, la cola todavía contiene a las tres personas. En una cola vacía, peek devuelve null; no lanza una excepción en este caso.

**Traza antes/después:** Antes y después: [Sara, Luis, Ana].

**Predicción parcial:** ¿Disminuye el tamaño por imprimir peek? **Comprueba tu razonamiento:** No; solo consulta.

## Paso 5 — Atender y mostrar los pendientes

**Por qué lo hacemos ahora:** poll devuelve y retira la cabeza. Antes de escribir, señala en qué estado está la colección y qué cambio esperamos observar.

**Acción:** dentro de `main`, después del último fragmento ya creado, agrega exactamente este bloque (sin duplicar las llaves externas de la clase):

```java
System.out.println("Atendido: " + fila.poll());
System.out.println("Pendientes: " + fila);
```
**Qué hace y por qué:** poll devuelve y retira la cabeza. Después de atender a Sara, permanecen Luis y Ana, en ese orden. En cola vacía, poll devuelve null; contrasta con peek, que observa sin quitar.

**Traza antes/después:** Antes: [Sara, Luis, Ana]. Después: [Luis, Ana]

**Predicción parcial:** ¿Qué imprimirá un segundo poll inmediatamente después? **Comprueba tu razonamiento:** Luis; la primera solicitud ya salió.

## Auditoría del archivo terminado

| Elemento | Qué significa y qué aporta |
|---|---|
| `java.util.Queue` | Tipo estándar que necesita el ejemplo; su import permite utilizar el nombre corto. |
| `java.util.LinkedList` | Tipo estándar que necesita el ejemplo; su import permite utilizar el nombre corto. |
| `EJ08.main` | Ejecuta los bloques en el orden escrito. |
| Operaciones de colección | Cambian o inspeccionan el estado según se describe en cada microbloque. |

## Archivo completo al terminar el ejemplo

```java
import java.util.Queue;
import java.util.LinkedList;

public class EJ08 {
    public static void main(String[] args) {
        Queue<String> fila = new LinkedList<>();
        fila.offer("Sara");
        fila.offer("Luis");
        fila.offer("Ana");
        System.out.println("Siguiente: " + fila.peek());
        System.out.println("Atendido: " + fila.poll());
        System.out.println("Pendientes: " + fila);
    }
}
```
## Antes de ejecutar — predicción obligatoria

1. ¿Qué devuelve peek sin modificar la cola?
2. ¿Quién sale con poll?
3. ¿Quiénes permanecen y en qué orden?

## Ejecución y resultado esperado

En IntelliJ utiliza **Run** en el `main` de `EJ08`. Si usas terminal, entra en la carpeta del `.java` y ejecuta:

```bash
javac -encoding UTF-8 EJ08.java
java EJ08
```

**Salida de referencia:**

```text
Siguiente: Sara
Atendido: Sara
Pendientes: [Luis, Ana]
```
**Interpretación:** lee la salida de izquierda a derecha y explica qué dato se conservó, cuál cambió y qué operación solo consultó. No generalices garantías de orden a HashSet o HashMap.

## Variación controlada

Agrega una llamada más a fila.poll() antes de imprimir Pendientes. Predice qué dos personas fueron atendidas y cuál queda.

## Error frecuente y corrección

Es incorrecto afirmar que peek y poll producen el mismo efecto. Después de peek la cola está intacta; poll elimina un registro. Corrige la línea según necesites consultar o atender.

## Demuestra que comprendiste

Sin consultar el código, explica por qué elegiste esta interfaz, qué clase instancia el objeto y cuál es la diferencia entre una operación que consulta y una que modifica la colección.

## T08 — Tarea espejo: Procesar tickets por orden de llegada

**Enunciado:** Registra T100, T200 y T300. Muestra el próximo ticket, atiende dos solicitudes con poll y presenta los tickets que todavía esperan.

**Archivo:** `src/T08.java`, con `main` independiente. **Restricción:** no reemplaces la estructura por arreglos ni uses una operación ajena al contrato trabajado.

**Pista:** Queue<String> tickets = new LinkedList<>(); offer, peek y dos poll consecutivos.

**Antes de ejecutar:** escribe una predicción de cada línea. Debes mostrar exactamente lo siguiente:

```text
Próximo: T100
Atendido 1: T100
Atendido 2: T200
Pendientes: [T300]
```
**Evidencia:** archivo compilable, consola y una explicación de qué sentencia provocó cada cambio. **Criterio:** salida correcta + razonamiento del estado antes/después; el resultado no debe copiarse de la guía docente.


---

# EJ09 — Eliminar valores durante el recorrido con Iterator

## Objetivo técnico — qué vamos a hacer y qué aprenderemos

Una lista de estados de inscripción contiene registros anulados que no deben aparecer en el informe final. Para retirarlos mientras recorremos la colección sin alterar indebidamente el ciclo, usaremos un Iterator. Partiremos de una ArrayList con cuatro estados, crearemos el iterador y recorreremos uno por uno con hasNext y next. Cuando el estado sea ANULADO, llamaremos remove sobre ese mismo iterador. Es un caso diferente de eliminar un único nombre conocido: aquí la decisión se toma mientras inspeccionamos cada registro.

## Qué problema concreto resolveremos

Es necesario eliminar todos los estados ANULADO durante una revisión, sin saltarse posiciones ni modificar estructuralmente la lista desde un for-each.

## Archivos y punto de partida

Crea `src/EJ09.java` y escribe la clase pública `EJ09`. Parte de un archivo nuevo, no del resultado del ejemplo anterior: así los cambios serán independientes. Primero se añaden los imports y la clase; después cada microbloque dentro de `main`.

## Paso 1 — Preparar importaciones y punto de entrada

En esta demostración necesitamos tipos específicos de `java.util`, no dependencias externas. Escribe la estructura siguiente al inicio de la clase. Dentro de `main` iremos agregando los bloques por orden.

```java
import java.util.List;
import java.util.ArrayList;
import java.util.Iterator;

public class EJ09 {
    public static void main(String[] args) {
        // Inserta aquí los próximos bloques.
    }
}
```
**Comprobación inicial:** el archivo todavía no tiene resultados. `main` define dónde comienza la ejecución; el nombre público debe coincidir con el del archivo.

## Paso 2 — Preparar la lista con dos anulaciones

**Por qué lo hacemos ahora:** La lista conserva los cuatro registros. Antes de escribir, señala en qué estado está la colección y qué cambio esperamos observar.

**Acción:** dentro de `main`, después del último fragmento ya creado, agrega exactamente este bloque (sin duplicar las llaves externas de la clase):

```java
List<String> estados = new ArrayList<>();
estados.add("PENDIENTE");
estados.add("ANULADO");
estados.add("CONFIRMADO");
estados.add("ANULADO");
```
**Qué hace y por qué:** La lista conserva los cuatro registros. Los dos ANULADO son intencionales para verificar que una sola revisión los quite a ambos. La lista inicialmente está en orden de ingreso.

**Traza antes/después:** Antes: []. Después: [PENDIENTE, ANULADO, CONFIRMADO, ANULADO]

**Predicción parcial:** ¿Cuántos elementos queremos eliminar? **Comprueba tu razonamiento:** Dos, ambos iguales a ANULADO.

## Paso 3 — Obtener un iterador

**Por qué lo hacemos ahora:** Iterator<String> permite avanzar por los elementos de la lista en forma controlada. Antes de escribir, señala en qué estado está la colección y qué cambio esperamos observar.

**Acción:** dentro de `main`, después del último fragmento ya creado, agrega exactamente este bloque (sin duplicar las llaves externas de la clase):

```java
Iterator<String> cursor = estados.iterator();
```
**Qué hace y por qué:** Iterator<String> permite avanzar por los elementos de la lista en forma controlada. cursor es un nombre elegido para representar el objeto que recorre estados. No altera la lista por el simple hecho de crearlo.

**Traza antes/después:** Antes y después: cuatro elementos; cursor preparado.

**Predicción parcial:** ¿El iterator() elimina algún valor? **Comprueba tu razonamiento:** No, solo prepara el recorrido.

## Paso 4 — Recorrer y decidir si retirar

**Por qué lo hacemos ahora:** hasNext comprueba si falta algún elemento por visitar. Antes de escribir, señala en qué estado está la colección y qué cambio esperamos observar.

**Acción:** dentro de `main`, después del último fragmento ya creado, agrega exactamente este bloque (sin duplicar las llaves externas de la clase):

```java
while (cursor.hasNext()) {
    String estado = cursor.next();
    if (estado.equals("ANULADO")) {
        cursor.remove();
    }
}
```
**Qué hace y por qué:** hasNext comprueba si falta algún elemento por visitar. next recupera el actual y avanza el cursor. equals compara el texto; cuando encuentra ANULADO, remove() del iterador elimina el último elemento visitado. No se llama remove sobre estados dentro del recorrido, porque mezclar modificaciones estructurales podría invalidar el iterador.

**Traza antes/después:** Inicio: [PENDIENTE, ANULADO, CONFIRMADO, ANULADO]. Al finalizar: [PENDIENTE, CONFIRMADO]

**Predicción parcial:** ¿Por qué no usamos estados.remove(estado) dentro de este recorrido? **Comprueba tu razonamiento:** Porque modificar directamente la lista mientras se usa el iterador puede provocar una modificación concurrente y romper el recorrido.

## Paso 5 — Mostrar el resultado depurado

**Por qué lo hacemos ahora:** La salida es una evidencia del filtro realizado: queda una lista de dos elementos en el orden original relativo. Antes de escribir, señala en qué estado está la colección y qué cambio esperamos observar.

**Acción:** dentro de `main`, después del último fragmento ya creado, agrega exactamente este bloque (sin duplicar las llaves externas de la clase):

```java
System.out.println("Estados vigentes: " + estados);
System.out.println("Cantidad: " + estados.size());
```
**Qué hace y por qué:** La salida es una evidencia del filtro realizado: queda una lista de dos elementos en el orden original relativo. El conteo confirma que se eliminaron exactamente dos registros, no todos.

**Traza antes/después:** Después: [PENDIENTE, CONFIRMADO], size=2.

**Predicción parcial:** ¿El programa reconstruye una lista nueva? **Comprueba tu razonamiento:** No: modifica la lista original mediante el iterador.

## Auditoría del archivo terminado

| Elemento | Qué significa y qué aporta |
|---|---|
| `java.util.List` | Tipo estándar que necesita el ejemplo; su import permite utilizar el nombre corto. |
| `java.util.ArrayList` | Tipo estándar que necesita el ejemplo; su import permite utilizar el nombre corto. |
| `java.util.Iterator` | Tipo estándar que necesita el ejemplo; su import permite utilizar el nombre corto. |
| `EJ09.main` | Ejecuta los bloques en el orden escrito. |
| Operaciones de colección | Cambian o inspeccionan el estado según se describe en cada microbloque. |

## Archivo completo al terminar el ejemplo

```java
import java.util.List;
import java.util.ArrayList;
import java.util.Iterator;

public class EJ09 {
    public static void main(String[] args) {
        List<String> estados = new ArrayList<>();
        estados.add("PENDIENTE");
        estados.add("ANULADO");
        estados.add("CONFIRMADO");
        estados.add("ANULADO");
        Iterator<String> cursor = estados.iterator();
        while (cursor.hasNext()) {
            String estado = cursor.next();
            if (estado.equals("ANULADO")) {
                cursor.remove();
            }
        }
        System.out.println("Estados vigentes: " + estados);
        System.out.println("Cantidad: " + estados.size());
    }
}
```
## Antes de ejecutar — predicción obligatoria

1. ¿Cuántos estados ANULADO desaparecerán?
2. ¿Qué conserva su orden relativo?
3. ¿Cuánto devuelve size al finalizar?

## Ejecución y resultado esperado

En IntelliJ utiliza **Run** en el `main` de `EJ09`. Si usas terminal, entra en la carpeta del `.java` y ejecuta:

```bash
javac -encoding UTF-8 EJ09.java
java EJ09
```

**Salida de referencia:**

```text
Estados vigentes: [PENDIENTE, CONFIRMADO]
Cantidad: 2
```
**Interpretación:** lee la salida de izquierda a derecha y explica qué dato se conservó, cuál cambió y qué operación solo consultó. No generalices garantías de orden a HashSet o HashMap.

## Variación controlada

Añade un segundo PENDIENTE al final. Comprueba que quedan tres estados y que la lista conserva los repetidos no anulados.

## Error frecuente y corrección

No invoques cursor.remove() antes de cursor.next(), ni dos veces seguidas sin otro next: se produce IllegalStateException. Lee el elemento con next y decide solo entonces si lo eliminas.

## Demuestra que comprendiste

Sin consultar el código, explica por qué elegiste esta interfaz, qué clase instancia el objeto y cuál es la diferencia entre una operación que consulta y una que modifica la colección.

## T09 — Tarea espejo: Depurar etiquetas descartadas

**Enunciado:** Crea una lista con ACTIVA, DESCARTAR, REVISAR y DESCARTAR. Recorre con Iterator y elimina todas las etiquetas DESCARTAR. Imprime la lista final y su cantidad.

**Archivo:** `src/T09.java`, con `main` independiente. **Restricción:** no reemplaces la estructura por arreglos ni uses una operación ajena al contrato trabajado.

**Pista:** Declara Iterator<String>; repite while(hasNext), lee next y usa cursor.remove en la condición.

**Antes de ejecutar:** escribe una predicción de cada línea. Debes mostrar exactamente lo siguiente:

```text
Etiquetas finales: [ACTIVA, REVISAR]
Total: 2
```
**Evidencia:** archivo compilable, consola y una explicación de qué sentencia provocó cada cambio. **Criterio:** salida correcta + razonamiento del estado antes/después; el resultado no debe copiarse de la guía docente.


---

# EJ10 — Cambiar el criterio de orden usando Comparator y TreeSet

## Objetivo técnico — qué vamos a hacer y qué aprenderemos

Un informe necesita mostrar valores únicos ascendentes y después descendentes. Hasta ahora vimos que TreeSet organiza elementos en su orden natural, pero la presentación puede requerir otro criterio de comparación. Partiremos de un TreeSet de enteros con un dato repetido y crearemos un segundo TreeSet que recibe Comparator.reverseOrder(). Copiaremos los números con addAll y comprobaremos que ambos mantienen unicidad, pero los exponen con distinto orden. No escribiremos un comparador personalizado ni saldremos del nivel de introducción a las interfaces del JCF.

## Qué problema concreto resolveremos

Un mismo conjunto de valores debe visualizarse en sentido contrario sin utilizar índices ni cambiar el significado de los datos.

## Archivos y punto de partida

Crea `src/EJ10.java` y escribe la clase pública `EJ10`. Parte de un archivo nuevo, no del resultado del ejemplo anterior: así los cambios serán independientes. Primero se añaden los imports y la clase; después cada microbloque dentro de `main`.

## Paso 1 — Preparar importaciones y punto de entrada

En esta demostración necesitamos tipos específicos de `java.util`, no dependencias externas. Escribe la estructura siguiente al inicio de la clase. Dentro de `main` iremos agregando los bloques por orden.

```java
import java.util.Set;
import java.util.TreeSet;
import java.util.Comparator;

public class EJ10 {
    public static void main(String[] args) {
        // Inserta aquí los próximos bloques.
    }
}
```
**Comprobación inicial:** el archivo todavía no tiene resultados. `main` define dónde comienza la ejecución; el nombre público debe coincidir con el del archivo.

## Paso 2 — Crear el conjunto con orden natural

**Por qué lo hacemos ahora:** Integer indica valores enteros. Antes de escribir, señala en qué estado está la colección y qué cambio esperamos observar.

**Acción:** dentro de `main`, después del último fragmento ya creado, agrega exactamente este bloque (sin duplicar las llaves externas de la clase):

```java
Set<Integer> natural = new TreeSet<>();
natural.add(12);
natural.add(5);
natural.add(8);
natural.add(8);
```
**Qué hace y por qué:** Integer indica valores enteros. TreeSet elimina el segundo 8 y mantiene el orden natural ascendente. El orden de los add no determina la visualización final en este caso.

**Traza antes/después:** Antes: []. Después: [5, 8, 12]

**Predicción parcial:** ¿Por qué aparecen solo tres números? **Comprueba tu razonamiento:** La operación add de Set no agrega el 8 duplicado.

## Paso 3 — Declarar un criterio inverso

**Por qué lo hacemos ahora:** Comparator.reverseOrder() devuelve un criterio para invertir el orden natural de enteros. Antes de escribir, señala en qué estado está la colección y qué cambio esperamos observar.

**Acción:** dentro de `main`, después del último fragmento ya creado, agrega exactamente este bloque (sin duplicar las llaves externas de la clase):

```java
Set<Integer> inverso = new TreeSet<>(Comparator.reverseOrder());
```
**Qué hace y por qué:** Comparator.reverseOrder() devuelve un criterio para invertir el orden natural de enteros. La instancia inverso inicia vacía; crearla no copia automáticamente el primer conjunto. Al colocar un Comparator en el constructor cambiamos la relación de orden del nuevo TreeSet.

**Traza antes/después:** Antes: natural=[5, 8, 12]. Después: inverso=[]

**Predicción parcial:** ¿Cambió el orden de natural al crear inverso? **Comprueba tu razonamiento:** No; son dos conjuntos separados.

## Paso 4 — Transferir los elementos sin duplicar

**Por qué lo hacemos ahora:** addAll agrega a inverso cada dato de natural. Antes de escribir, señala en qué estado está la colección y qué cambio esperamos observar.

**Acción:** dentro de `main`, después del último fragmento ya creado, agrega exactamente este bloque (sin duplicar las llaves externas de la clase):

```java
inverso.addAll(natural);
```
**Qué hace y por qué:** addAll agrega a inverso cada dato de natural. No se altera natural y no se crean números nuevos. Como destino es TreeSet con criterio inverso, los mismos tres números aparecen en orden descendente.

**Traza antes/después:** Antes: inverso=[]. Después: inverso=[12, 8, 5]

**Predicción parcial:** ¿Debemos invocar add tres veces manualmente? **Comprueba tu razonamiento:** No; addAll transfiere los elementos existentes.

## Paso 5 — Comparar resultados visibles

**Por qué lo hacemos ahora:** Al mostrar los conjuntos visualizamos la diferencia entre contenido y criterio de ordenación. Antes de escribir, señala en qué estado está la colección y qué cambio esperamos observar.

**Acción:** dentro de `main`, después del último fragmento ya creado, agrega exactamente este bloque (sin duplicar las llaves externas de la clase):

```java
System.out.println("Natural: " + natural);
System.out.println("Inverso: " + inverso);
```
**Qué hace y por qué:** Al mostrar los conjuntos visualizamos la diferencia entre contenido y criterio de ordenación. La unicidad se mantiene y el orden cambia. La demostración conecta SortedSet/TreeSet y Comparator sin construir clases adicionales.

**Traza antes/después:** Al final: natural=[5, 8, 12]; inverso=[12, 8, 5]

**Predicción parcial:** ¿Cuál conjunto tiene más elementos? **Comprueba tu razonamiento:** Ninguno; cada uno contiene tres valores únicos.

## Auditoría del archivo terminado

| Elemento | Qué significa y qué aporta |
|---|---|
| `java.util.Set` | Tipo estándar que necesita el ejemplo; su import permite utilizar el nombre corto. |
| `java.util.TreeSet` | Tipo estándar que necesita el ejemplo; su import permite utilizar el nombre corto. |
| `java.util.Comparator` | Tipo estándar que necesita el ejemplo; su import permite utilizar el nombre corto. |
| `EJ10.main` | Ejecuta los bloques en el orden escrito. |
| Operaciones de colección | Cambian o inspeccionan el estado según se describe en cada microbloque. |

## Archivo completo al terminar el ejemplo

```java
import java.util.Set;
import java.util.TreeSet;
import java.util.Comparator;

public class EJ10 {
    public static void main(String[] args) {
        Set<Integer> natural = new TreeSet<>();
        natural.add(12);
        natural.add(5);
        natural.add(8);
        natural.add(8);
        Set<Integer> inverso = new TreeSet<>(Comparator.reverseOrder());
        inverso.addAll(natural);
        System.out.println("Natural: " + natural);
        System.out.println("Inverso: " + inverso);
    }
}
```
## Antes de ejecutar — predicción obligatoria

1. ¿Cuántos valores únicos tendrá cada conjunto?
2. ¿En qué orden se mostrará el segundo?
3. ¿Se modifica natural después de addAll?

## Ejecución y resultado esperado

En IntelliJ utiliza **Run** en el `main` de `EJ10`. Si usas terminal, entra en la carpeta del `.java` y ejecuta:

```bash
javac -encoding UTF-8 EJ10.java
java EJ10
```

**Salida de referencia:**

```text
Natural: [5, 8, 12]
Inverso: [12, 8, 5]
```
**Interpretación:** lee la salida de izquierda a derecha y explica qué dato se conservó, cuál cambió y qué operación solo consultó. No generalices garantías de orden a HashSet o HashMap.

## Variación controlada

Agrega natural.add(20) después de addAll. Comprueba que inverso todavía no incorpora el 20 hasta que vuelvas a llamar a inverso.addAll(natural).

## Error frecuente y corrección

Es incorrecto esperar que HashSet respete el mismo orden de esta demostración; utiliza TreeSet para exigirlo. Verifica que importas java.util.Comparator y no una clase inexistente.

## Demuestra que comprendiste

Sin consultar el código, explica por qué elegiste esta interfaz, qué clase instancia el objeto y cuál es la diferencia entre una operación que consulta y una que modifica la colección.

## T10 — Tarea espejo: Mostrar nombres únicos alfabéticamente y al revés

**Enunciado:** Carga Ana, Rosa, Luis y Ana en TreeSet. Crea otro TreeSet con Comparator.reverseOrder y copia los valores. Imprime ambos órdenes.

**Archivo:** `src/T10.java`, con `main` independiente. **Restricción:** no reemplaces la estructura por arreglos ni uses una operación ajena al contrato trabajado.

**Pista:** Set<String> con TreeSet y otro TreeSet<>(Comparator.reverseOrder()); usa addAll.

**Antes de ejecutar:** escribe una predicción de cada línea. Debes mostrar exactamente lo siguiente:

```text
Natural: [Ana, Luis, Rosa]
Inverso: [Rosa, Luis, Ana]
```
**Evidencia:** archivo compilable, consola y una explicación de qué sentencia provocó cada cambio. **Criterio:** salida correcta + razonamiento del estado antes/después; el resultado no debe copiarse de la guía docente.

---

## 7. Cierre y mapa de elección de colecciones

La elección depende del contrato que necesita el problema. Si cada inscripción debe permanecer, `List` es adecuada, aunque existan nombres repetidos. Si únicamente se deben contar códigos diferentes, utiliza `Set`; cuando además se necesita orden natural, `TreeSet` lo proporciona. Si la pregunta contiene una clave, `Map` relaciona dicha clave con un valor y permite sustituir la asociación anterior. Si las solicitudes deben procesarse en orden de llegada, `Queue` con `LinkedList` permite observar al primero con `peek` o retirarlo con `poll`. Si necesitas quitar ciertos elementos durante un recorrido, `Iterator` permite decidirlo sobre el elemento actual. `Comparator` cambia el criterio de orden de un `TreeSet` sin cambiar el tipo de los datos.

En una situación nueva, identifica primero qué podría perderse si seleccionas otra estructura: registros duplicados, orden significativo, asociaciones por código o turnos pendientes. La evidencia de dominio no es memorizar una clase, sino predecir una salida, explicar por qué ocurre y corregir un error concreto.

## 8. Cuestionario de salida — 6 minutos

1. Una persona aparece dos veces en una hoja de inscripción. ¿Cómo conserva ambas entradas una `List`?
2. ¿Por qué la tercera inserción de un DNI repetido en `HashSet` devuelve `false`?
3. ¿Qué cambia si pasas de `HashSet` a `TreeSet` con textos comparables?
4. ¿Por qué actualizar la clave 3 con `put` no aumenta el tamaño de `HashMap`?
5. ¿En qué se diferencian `peek` y `poll` en la fila de atención?
6. ¿Qué responsabilidad cubre cada colección del integrador EJ06?

## 9. Checklist de estudio y entrega

- [ ] Identifiqué los **10 ejemplos** EJ01–EJ10 y tengo **10 tareas espejo** T01–T10.
- [ ] Distinguí **8 ejemplos del itinerario presencial** de **EJ09–EJ10 autónomos**.
- [ ] Ejecuté ejemplos con Java 21 o verifiqué el JDK institucional aprobado.
- [ ] Antes de ejecutar cada ejemplo, escribí al menos una predicción.
- [ ] Registré los cambios de estado después de cada operación nueva.
- [ ] Puedo explicar por qué no debe suponerse orden en HashSet ni HashMap.
- [ ] Entrego mis soluciones personales, consola y justificación de selección de estructura.

**Recursos de continuidad:** https://lideratecacademy.com/blog/ · https://www.youtube.com/@LideratecAcademy
