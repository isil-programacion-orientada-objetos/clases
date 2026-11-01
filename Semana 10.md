---
course_id: ISIL-POO
session_id: S10
version: 2.0-profunda
source_origin: PPT
java_version: 21
status: validated
---

# PROGRAMACIÓN ORIENTADA A OBJETOS · SESIÓN 10
## Operaciones en colecciones: ArrayList y Collections

**Lideratec Academy · ISIL · Java 21 · IntelliJ IDEA · Guía ampliada y reproducible**

> **El propósito de esta revisión es pasar de operaciones aisladas a casos con decisiones reales:** precondiciones, datos repetidos, índices, estados antes/después, auditoría de resultados, casos límite y una clase integradora que proteja sus datos.

## 1. Apertura docente: qué problema resuelve la sesión

En un sistema de inscripción no basta con declarar una lista y agregar tres nombres. Debemos decidir si hay capacidad para recibir nuevos participantes, distinguir entre corregir y desplazar posiciones, explicar por qué al retirar un registro pueden quedar duplicados y conocer los riesgos de buscar en una lista sin ordenar. Todas esas tareas parten de dos herramientas presentes en la sesión: `ArrayList`, que almacena elementos en una secuencia modificable, y `Collections`, que ofrece operaciones utilitarias para ordenar, buscar, contar, copiar, invertir y reemplazar.

El resultado de aprendizaje será observable: cada estudiante ejecutará programas que explican su estado inicial, justifican una transformación, muestran su salida y prueban al menos una situación límite. La clase no trata de memorizar métodos sueltos: busca comprender cuándo una operación modifica la lista, cuándo retorna información y qué condición debe cumplirse para que un resultado sea fiable.

## 2. Preparación desde cero: proyecto IntelliJ IDEA

1. Verifica que el JDK 21 esté disponible. En la terminal ejecuta `java -version` y `javac -version` y confirma la versión 21. En IntelliJ selecciona un **Project SDK** compatible con 21.
2. Abre IntelliJ IDEA, crea un proyecto nuevo de **Java**, selecciona **JDK 21** y nómbralo `S10_Colecciones_Profunda`. No necesitas Spring, Maven, Tomcat ni dependencias externas para estas prácticas.
3. En la carpeta de fuentes `src`, crea los archivos `EJ01.java` a `EJ09.java` y, para el integrador, `GestorInscripciones.java`. No añadas una declaración `package` salvo que reorganices todos los archivos del mismo modo.
4. Copia y ejecuta **un ejemplo por vez**. Usa el botón **Run** de la clase que contiene `main` y verifica la salida que aparece en esta guía.
5. Para ejecutar desde terminal, ubícate en la carpeta de los archivos y usa `javac -encoding UTF-8 EJ01.java` seguido de `java EJ01`. Para EJ09, compila `javac -encoding UTF-8 GestorInscripciones.java EJ09.java` y ejecuta `java EJ09`.
6. Si IntelliJ indica `release version 21 not supported`, revisa la selección real del JDK del proyecto y del compilador. Si aparece `Could not find or load main class`, comprueba el nombre exacto del archivo, la clase y las rutas de compilación.

**Nota docente:** se utilizan secuencias de números y nombres como datos pedagógicos; no se desarrolla un sistema de base de datos ni una interfaz web, porque aquí el foco son las dos clases de la PPT.

## 3. Plan realista para 120 minutos: dos bloques conceptuales

| Tiempo | Qué ocurre | Evidencia que exige el docente |
|---|---|---|
| 00–12 | Preparación y pregunta de diagnóstico | Proyecto y JDK listos; diferencia entre lista y arreglo |
| 12–31 | EJ01 + T01 dirigido | Registros vs cupo; regla de duplicados |
| 31–51 | EJ02 + predicciones | `set` no inserta; `add` desplaza índices |
| 51–67 | EJ04 + microreto | Primera, última y todas las posiciones |
| 67–91 | EJ05 completo | `sort` ANTES de `binarySearch`, Rosa índice 6 |
| 91–111 | EJ09: diseño, altas y copia ordenada | Estado encapsulado; búsqueda segura |
| 111–120 | Prueba de aceptación y cierre | Un dato válido, uno inválido y justificación oral |

**Trabajo autónomo con soluciones de consulta docente:** EJ03, EJ06, EJ07 y EJ08, y tareas T02–T09. Las nueve prácticas son completas y no se pretende fingir que todas sus ejecuciones exhaustivas caben en dos horas.

## 4. Cómo leer y usar cada práctica

Cada caso identifica una necesidad concreta, una secuencia de decisiones, el archivo completo para ejecutar, la salida obtenida realmente con Java 21, preguntas de comprensión, una falla frecuente y una tarea espejo en un contexto distinto. **La tarea espejo no es cambiar un nombre o un número:** pide combinar operaciones, comprobar límites y explicar invariantes. La solución completa aparece en la guía del docente, no en esta guía de estudiante.



---

# EJ01 — Controlar aforo y duplicados de un taller

**Área:** ArrayList · **Modalidad:** AULA · **Tarea espejo:** T01

### Situación y dificultad que resolveremos

El coordinador de un taller recibe inscripciones por etapas y necesita identificar si llegó al cupo de cinco lugares. La misma persona puede aparecer más de una vez si se registró dos veces: en esta fase lo detectamos, pero no borramos datos silenciosamente.

### Objetivo técnico y evidencia de aprendizaje

Construir un registro dinámico, medir cupos ocupados y distinguir capacidad disponible, lista vacía y presencia de inscripciones duplicadas. El estudiante debe poder identificar el estado anterior de la lista, la operación aplicada, su efecto y el resultado que confirma que funcionó.

### Descomposición antes de codificar

**1. Estado inicial.** La lista empieza vacía; `isEmpty()` describe el estado real, no el aforo disponible.

**2. Carga secuencial.** `add()` mantiene el orden de recepción; el nombre repetido no es eliminado por Java.

**3. Regla de negocio.** El control del cupo usa `size()` y una constante; es una decisión de la aplicación, no un límite de `ArrayList`.

**4. Verificación.** Mostrar lista, plazas y frecuencia de Rosa permite explicar cantidad de registros frente a cantidad de personas únicas.

### Construcción progresiva en IntelliJ

**Microacción 1.** Crear `ArrayList<String>` y verificar `isEmpty`.

**Fragmento relevante que escribirás o localizarás en el archivo:**

```java
final int CUPO = 5;
ArrayList<String> inscritos = new ArrayList<>();
System.out.println("Inicio vacio: " + inscritos.isEmpty());
```

**Qué ocurre y cómo verificarlo:** No hay inscritos todavía. CUPO define la regla del taller; no modifica la capacidad técnica de la colección.

**Microacción 2.** Registrar cuatro entradas en orden; demostrar el duplicado.

**Fragmento relevante que escribirás o localizarás en el archivo:**

```java
inscritos.add("Rosa");
inscritos.add("Luis");
inscritos.add("Ana");
inscritos.add("Rosa");
```

**Qué ocurre y cómo verificarlo:** Cada add coloca un dato al final. Tras el cuarto alta existen 4 registros pero solo 3 nombres diferentes.

**Microacción 3.** Evaluar `size()` frente a `CUPO` antes de un alta.

**Fragmento relevante que escribirás o localizarás en el archivo:**

```java
if (inscritos.size() < CUPO) {
    inscritos.add("Mario");
}
```

**Qué ocurre y cómo verificarlo:** Antes de añadir se compara size=4 con CUPO=5; se agrega Mario y size pasa a 5.

**Microacción 4.** Calcular frecuencia y auditar que el registro no se excedió.

**Fragmento relevante que escribirás o localizarás en el archivo:**

```java
Collections.frequency(inscritos, "Rosa");
boolean sePuedeInscribirOtraPersona = inscritos.size() < CUPO;
```

**Qué ocurre y cómo verificarlo:** Rosa figura 2 veces y el boolean es false porque el aforo alcanzó cinco registros.

### Rastreo del estado: antes, operación y consecuencia

| Hito | Estado o resultado | Interpretación |
|---|---|---|
| Lista recién creada | []; isEmpty = true | Todavía no se ha registrado nadie |
| Tras cuatro add | [Rosa, Luis, Ana, Rosa]; size = 4 | Duplicados permitidos, cupo disponible = 1 |
| Tras control de cupo | [Rosa, Luis, Ana, Rosa, Mario]; size = 5 | Se completa el aforo, próximo alta bloqueada |

### Programa completo que se construye

**Archivo ``**

```java
import java.util.ArrayList;
import java.util.Collections;

public class EJ01 {
    public static void main(String[] args) {
        final int CUPO = 5;
        ArrayList<String> inscritos = new ArrayList<>();
        System.out.println("Inicio vacio: " + inscritos.isEmpty());

        inscritos.add("Rosa");
        inscritos.add("Luis");
        inscritos.add("Ana");
        inscritos.add("Rosa");
        System.out.println("Inscritos: " + inscritos);
        System.out.println("Registros: " + inscritos.size());
        System.out.println("Plazas disponibles: " + (CUPO - inscritos.size()));
        System.out.println("Rosa aparece: " + Collections.frequency(inscritos, "Rosa"));

        if (inscritos.size() < CUPO) {
            inscritos.add("Mario");
        }
        boolean sePuedeInscribirOtraPersona = inscritos.size() < CUPO;
        System.out.println("Final: " + inscritos);
        System.out.println("Queda cupo: " + sePuedeInscribirOtraPersona);
    }
}
```

### Predicción concreta antes de Run

1. Señala qué instrucciones cambian la lista y cuáles solo consultan o imprimen.
2. Anticipa la primera y la última línea de la salida y argumenta cómo se llegó a ellas.
3. Explica qué sucedería si la entrada tuviese un elemento repetido o faltante.

### Ejecución real, salida esperada e interpretación

```text
Inicio vacio: true
Inscritos: [Rosa, Luis, Ana, Rosa]
Registros: 4
Plazas disponibles: 1
Rosa aparece: 2
Final: [Rosa, Luis, Ana, Rosa, Mario]
Queda cupo: false
```

**Lectura de la salida:** Mostrar lista, plazas y frecuencia de Rosa permite explicar cantidad de registros frente a cantidad de personas únicas. Las líneas anteriores se obtuvieron ejecutando el código que aparece en esta misma sección; no son datos simulados.

### Error que debemos poder diagnosticar

**Síntoma / decisión equivocada:** Confundir número de registros con número de participantes únicos, o contar con un arreglo de longitud fija.

**Causa y corrección:** Explicar explícitamente la diferencia entre política de duplicados y características de ArrayList; para cupos comparar antes de añadir.

### Preguntas para defender el razonamiento

- ¿Cuándo el listado contiene dos registros pero no necesariamente dos personas distintas?
- ¿Por qué tener un `ArrayList` dinámico no elimina la necesidad de validar el cupo?

### Prueba de transferencia adicional

¿Qué cambia si el negocio prohíbe duplicados? Redacta una regla basada en `contains`, sin eliminar información de otras personas.

## T01 — Registro de seminario con cupo (tarea espejo evaluable)

Crea `T01.java` para un seminario con cupo 4. Registra `[Eva, Omar, Eva]`, imprime el estado inicial vacío, el listado y el número de duplicaciones de Eva. Agrega `Nora` solo si existe espacio. Intenta agregar `Leo` con la misma regla y reporta si su registro se produjo. La decisión debe depender de `size()`, nunca de una longitud supuesta.

**Archivos a crear:** `T01.java`.

**Secuencia de resolución sugerida:** reproduce el planteamiento, dibuja la lista inicial con índices, escribe las operaciones, anota las salidas antes de ejecutar, prueba un caso límite y documenta por qué la solución satisface cada criterio.

**Criterios de aceptación verificables:**

- Inicio vacío = true.
- Eva aparece 2 veces.
- Lista final [Eva, Omar, Eva, Nora].
- 4 registros, Leo no ingresó.

**Entrega:** código propio que compile y salida de consola; incluye una explicación de cinco a ocho líneas sobre las precondiciones, cambios de estado y resultados.



---

# EJ02 — Corregir registros sin perder posiciones

**Área:** ArrayList · **Modalidad:** AULA · **Tarea espejo:** T02

### Situación y dificultad que resolveremos

El coordinador digitó mal un nombre y necesita reemplazarlo. Después surge una inscripción que debe ocupar una posición intermedia en el orden de atención; ambos cambios tienen consecuencias distintas para los índices.

### Objetivo técnico y evidencia de aprendizaje

Distinguir `set` de `add(indice, dato)`, obtener un dato seguro y explicar por qué insertar desplaza posiciones sin sustituir elementos. El estudiante debe poder identificar el estado anterior de la lista, la operación aplicada, su efecto y el resultado que confirma que funcionó.

### Descomposición antes de codificar

**1. Control de límites.** `get()` y `set()` exigen índices desde 0 hasta `size()-1`; se valida antes de consultar.

**2. Corrección puntual.** `set(1, "Rocio")` modifica una posición sin incrementar `size()`.

**3. Reordenación.** `add(1, "Marta")` inserta y desplaza los elementos desde el índice 1.

**4. Estado final.** Las posiciones se vuelven a enumerar; las referencias a los elementos restantes se preservan.

### Construcción progresiva en IntelliJ

**Microacción 1.** Crear la lista y trazar posiciones 0,1,2.

**Fragmento relevante que escribirás o localizarás en el archivo:**

```java
cola.add("Ana");
cola.add("Rosa");
cola.add("Luis");
```

**Qué ocurre y cómo verificarlo:** Los índices iniciales son 0=Ana, 1=Rosa, 2=Luis.

**Microacción 2.** Verificar que el índice consultado sea válido.

**Fragmento relevante que escribirás o localizarás en el archivo:**

```java
if (consultado >= 0 && consultado < cola.size()) {
    System.out.println("Posicion 1: " + cola.get(consultado));
}
```

**Qué ocurre y cómo verificarlo:** La posición solicitada 1 cumple 0 <= 1 < 3; get devuelve Rosa sin alterar la lista.

**Microacción 3.** Corregir con set y comparar `size()`.

**Fragmento relevante que escribirás o localizarás en el archivo:**

```java
String anterior = cola.set(1, "Rocio");
```

**Qué ocurre y cómo verificarlo:** Se recupera Rosa como valor anterior y ahora el índice 1 contiene Rocio; siguen siendo 3 datos.

**Microacción 4.** Insertar con `add(indice, ...)` y volver a enumerar.

**Fragmento relevante que escribirás o localizarás en el archivo:**

```java
cola.add(1, "Marta");
for (int i = 0; i < cola.size(); i++) {
    System.out.println("Indice " + i + " -> " + cola.get(i));
}
```

**Qué ocurre y cómo verificarlo:** La inserción desplaza a Rocio hacia el índice 2 y a Luis hacia el 3; el tamaño pasa a 4.

### Rastreo del estado: antes, operación y consecuencia

| Hito | Estado o resultado | Interpretación |
|---|---|---|
| Carga original | [Ana, Rosa, Luis]; 3 | Rosa está en índice 1 |
| Tras set(1, Rocio) | [Ana, Rocio, Luis]; 3 | Sustitución no agrega elemento |
| Tras add(1, Marta) | [Ana, Marta, Rocio, Luis]; 4 | Rocio y Luis se desplazan |

### Programa completo que se construye

**Archivo ``**

```java
import java.util.ArrayList;

public class EJ02 {
    public static void main(String[] args) {
        ArrayList<String> cola = new ArrayList<>();
        cola.add("Ana");
        cola.add("Rosa");
        cola.add("Luis");
        System.out.println("Original: " + cola);

        int consultado = 1;
        if (consultado >= 0 && consultado < cola.size()) {
            System.out.println("Posicion 1: " + cola.get(consultado));
        }
        String anterior = cola.set(1, "Rocio");
        System.out.println("Reemplazado: " + anterior);
        System.out.println("Tras set: " + cola + " | total=" + cola.size());

        cola.add(1, "Marta");
        System.out.println("Tras insertar: " + cola + " | total=" + cola.size());
        for (int i = 0; i < cola.size(); i++) {
            System.out.println("Indice " + i + " -> " + cola.get(i));
        }
    }
}
```

### Predicción concreta antes de Run

1. Señala qué instrucciones cambian la lista y cuáles solo consultan o imprimen.
2. Anticipa la primera y la última línea de la salida y argumenta cómo se llegó a ellas.
3. Explica qué sucedería si la entrada tuviese un elemento repetido o faltante.

### Ejecución real, salida esperada e interpretación

```text
Original: [Ana, Rosa, Luis]
Posicion 1: Rosa
Reemplazado: Rosa
Tras set: [Ana, Rocio, Luis] | total=3
Tras insertar: [Ana, Marta, Rocio, Luis] | total=4
Indice 0 -> Ana
Indice 1 -> Marta
Indice 2 -> Rocio
Indice 3 -> Luis
```

**Lectura de la salida:** Las posiciones se vuelven a enumerar; las referencias a los elementos restantes se preservan. Las líneas anteriores se obtuvieron ejecutando el código que aparece en esta misma sección; no son datos simulados.

### Error que debemos poder diagnosticar

**Síntoma / decisión equivocada:** Utilizar `set(4, ...)` para insertar al final cuando la lista tiene tamaño 4, o consultar `get(size())`.

**Causa y corrección:** `set` solo reemplaza índices existentes; `add(size(), ...)` sí admite insertar al final. Validar `get` antes de acceder.

### Preguntas para defender el razonamiento

- ¿Qué devuelve `set` además de modificar la lista?
- ¿Qué intervalo de índices es válido para `add(indice, elemento)`?

### Prueba de transferencia adicional

Inserta un elemento en índice 0 y calcula todas las nuevas posiciones sin ejecutar.

## T02 — Actualizar la cola de asesorías (tarea espejo evaluable)

Construye `T02.java` con `[Sol, Luna, Mar, Cielo]`. Corrige `Luna` por `Nube` usando `set`, inserta `Rio` en el índice 2 y muestra la lista después de cada operación. Consulta una posición 8 solo si es válida; no permitas que el programa se interrumpa. Finalmente imprime todos los índices y sus nombres.

**Archivos a crear:** `T02.java`.

**Secuencia de resolución sugerida:** reproduce el planteamiento, dibuja la lista inicial con índices, escribe las operaciones, anota las salidas antes de ejecutar, prueba un caso límite y documenta por qué la solución satisface cada criterio.

**Criterios de aceptación verificables:**

- Después de `set`, la lista conserva 4 elementos.
- Después de insertar, hay 5 y Mar cambia de índice 2 a 3.
- La consulta índice 8 se rechaza sin excepción.

**Entrega:** código propio que compile y salida de consola; incluye una explicación de cinco a ocho líneas sobre las precondiciones, cambios de estado y resultados.



---

# EJ03 — Retirar inscripciones duplicadas con control

**Área:** ArrayList · **Modalidad:** AUTÓNOMO · **Tarea espejo:** T03

### Situación y dificultad que resolveremos

Una persona figura varias veces por error y solicita cancelar todas sus inscripciones. Hay que distinguir retirar una posición específica, retirar una ocurrencia y retirar todas las coincidencias sin saltarse datos.

### Objetivo técnico y evidencia de aprendizaje

Observar las dos variantes de `remove`, conservar el valor retirado y aplicar un ciclo de eliminación seguro para duplicados. El estudiante debe poder identificar el estado anterior de la lista, la operación aplicada, su efecto y el resultado que confirma que funcionó.

### Descomposición antes de codificar

**1. Por índice.** `remove(0)` devuelve el participante retirado y desplaza las posiciones posteriores.

**2. Por valor.** `remove("Luis")` devuelve boolean y elimina solo la primera coincidencia.

**3. Repetidos.** Un ciclo `while (lista.remove("Luis"))` continúa hasta no encontrar más coincidencias.

**4. Estado vacío.** `clear()` borra todos los elementos; `isEmpty()` confirma el cambio.

### Construcción progresiva en IntelliJ

**Microacción 1.** Mostrar lista con tres Luis y predecir desplazamientos.

**Fragmento relevante que escribirás o localizarás en el archivo:**

```java
inscritos.add("Ana"); inscritos.add("Luis");
inscritos.add("Eva"); inscritos.add("Luis"); inscritos.add("Luis");
```

**Qué ocurre y cómo verificarlo:** Lista inicial de 5 elementos; Luis ocupa posiciones 1, 3 y 4.

**Microacción 2.** Retirar por índice y guardar el valor retornado.

**Fragmento relevante que escribirás o localizarás en el archivo:**

```java
String eliminadoPorIndice = inscritos.remove(0);
```

**Qué ocurre y cómo verificarlo:** El resultado devuelto es Ana. Todos los demás nombres cambian de posición.

**Microacción 3.** Retirar solo primera coincidencia por valor.

**Fragmento relevante que escribirás o localizarás en el archivo:**

```java
boolean seRetiroUno = inscritos.remove("Luis");
```

**Qué ocurre y cómo verificarlo:** Se retira únicamente el primer Luis, no los tres; seRetiroUno vale true.

**Microacción 4.** Eliminar las restantes y verificar que no existe Luis.

**Fragmento relevante que escribirás o localizarás en el archivo:**

```java
while (inscritos.remove("Luis")) {
    retiradosAdicionales++;
}
```

**Qué ocurre y cómo verificarlo:** El ciclo retira otros dos Luis y termina cuando ya no existe ninguno; no salta coincidencias.

**Microacción 5.** Vaciar como operación distinta.

**Fragmento relevante que escribirás o localizarás en el archivo:**

```java
inscritos.clear();
System.out.println("Vacia al cerrar: " + inscritos.isEmpty());
```

**Qué ocurre y cómo verificarlo:** clear vacía por completo; no es el método adecuado si solo se desea retirar un nombre.

### Rastreo del estado: antes, operación y consecuencia

| Hito | Estado o resultado | Interpretación |
|---|---|---|
| Original | [Ana, Luis, Eva, Luis, Luis] | Cinco elementos; Luis repetido |
| remove(0) | [Luis, Eva, Luis, Luis] | El método retorna Ana |
| remove("Luis") | [Eva, Luis, Luis] | Solo desaparece el primero |
| while remove("Luis") | [Eva] | Elimina los dos restantes sin saltarlos |
| clear() | [] | Lista vacía por completo |

### Programa completo que se construye

**Archivo ``**

```java
import java.util.ArrayList;

public class EJ03 {
    public static void main(String[] args) {
        ArrayList<String> inscritos = new ArrayList<>();
        inscritos.add("Ana");
        inscritos.add("Luis");
        inscritos.add("Eva");
        inscritos.add("Luis");
        inscritos.add("Luis");
        System.out.println("Inicial: " + inscritos);

        String eliminadoPorIndice = inscritos.remove(0);
        System.out.println("Sale indice 0: " + eliminadoPorIndice);
        boolean seRetiroUno = inscritos.remove("Luis");
        System.out.println("Sale primer Luis: " + seRetiroUno);
        System.out.println("Restante: " + inscritos);

        int retiradosAdicionales = 0;
        while (inscritos.remove("Luis")) {
            retiradosAdicionales++;
        }
        System.out.println("Luis adicionales retirados: " + retiradosAdicionales);
        System.out.println("Resultado: " + inscritos);
        inscritos.clear();
        System.out.println("Vacia al cerrar: " + inscritos.isEmpty());
    }
}
```

### Predicción concreta antes de Run

1. Señala qué instrucciones cambian la lista y cuáles solo consultan o imprimen.
2. Anticipa la primera y la última línea de la salida y argumenta cómo se llegó a ellas.
3. Explica qué sucedería si la entrada tuviese un elemento repetido o faltante.

### Ejecución real, salida esperada e interpretación

```text
Inicial: [Ana, Luis, Eva, Luis, Luis]
Sale indice 0: Ana
Sale primer Luis: true
Restante: [Eva, Luis, Luis]
Luis adicionales retirados: 2
Resultado: [Eva]
Vacia al cerrar: true
```

**Lectura de la salida:** `clear()` borra todos los elementos; `isEmpty()` confirma el cambio. Las líneas anteriores se obtuvieron ejecutando el código que aparece en esta misma sección; no son datos simulados.

### Error que debemos poder diagnosticar

**Síntoma / decisión equivocada:** Recorrer con `for` y eliminar en cada posición sin reajustar el índice: se omiten elementos que se desplazan.

**Causa y corrección:** Eliminar por valor en un `while` condicionado a `remove` o adaptar el índice; no mezclar efectos de las sobrecargas.

### Preguntas para defender el razonamiento

- ¿Qué método `remove` devuelve un elemento y cuál devuelve boolean?
- ¿Por qué un ciclo ascendente que elimina índices puede saltar coincidencias consecutivas?

### Prueba de transferencia adicional

¿Qué sucede si nunca hubo B? Comprueba que el contador inicia y queda en cero.

## T03 — Depurar lista de entrega de certificados (tarea espejo evaluable)

Construye `T03.java`: parte de `[A, B, B, C, B, D]`, retira el elemento del índice 0 e informa cuál era. Luego elimina TODAS las apariciones de B usando un ciclo que no omita elementos. Muestra cuántos registros B fueron retirados, el estado final y el tamaño. No uses `clear` para eliminar únicamente las B.

**Archivos a crear:** `T03.java`.

**Secuencia de resolución sugerida:** reproduce el planteamiento, dibuja la lista inicial con índices, escribe las operaciones, anota las salidas antes de ejecutar, prueba un caso límite y documenta por qué la solución satisface cada criterio.

**Criterios de aceptación verificables:**

- Eliminado por índice: A.
- Se eliminan 3 letras B.
- Resultado [C, D], tamaño 2.

**Entrega:** código propio que compile y salida de consola; incluye una explicación de cinco a ocho líneas sobre las precondiciones, cambios de estado y resultados.



---

# EJ04 — Auditar presencias y localizar todas las coincidencias

**Área:** ArrayList · **Modalidad:** AULA · **Tarea espejo:** T04

### Situación y dificultad que resolveremos

La lista de asistencia contiene registros repetidos que deben analizarse. Un coordinador necesita no solo saber si alguien figura, sino conocer primera, última y todas sus posiciones, además de distinguir entre ausencia y posición cero.

### Objetivo técnico y evidencia de aprendizaje

Combinar recorrido, `contains`, `indexOf`, `lastIndexOf` y verificación explícita de `-1`, conservando las posiciones basadas en cero. El estudiante debe poder identificar el estado anterior de la lista, la operación aplicada, su efecto y el resultado que confirma que funcionó.

### Descomposición antes de codificar

**1. Buscar presencia.** `contains` responde una pregunta booleana, pero no indica posición.

**2. Primer y último.** `indexOf` y `lastIndexOf` ubican extremos en presencia de duplicados.

**3. Auditoría completa.** Recorrer con `for` permite capturar cada índice, no solo el primero.

**4. Ausentes.** La posición `-1` significa que el dato no está presente.

### Construcción progresiva en IntelliJ

**Microacción 1.** Cargar la lista con duplicados premeditados.

**Fragmento relevante que escribirás o localizarás en el archivo:**

```java
for (String nombre : new String[]{"Rosa", "Ana", "Luis", "Rosa", "Eva", "Rosa"}) {
    asistentes.add(nombre);
}
```

**Qué ocurre y cómo verificarlo:** Rosa aparece en índices 0, 3 y 5. La lista está en orden de llegada, no ordenada alfabéticamente.

**Microacción 2.** Comparar presencia vs primera/última posición.

**Fragmento relevante que escribirás o localizarás en el archivo:**

```java
asistentes.contains("Rosa");
asistentes.indexOf("Rosa");
asistentes.lastIndexOf("Rosa");
```

**Qué ocurre y cómo verificarlo:** contains devuelve true; primera posición 0, última posición 5.

**Microacción 3.** Recorrer todos los elementos y seleccionar cada coincidencia.

**Fragmento relevante que escribirás o localizarás en el archivo:**

```java
for (int i = 0; i < asistentes.size(); i++) {
    if (asistentes.get(i).equals("Rosa")) System.out.print(" " + i);
}
```

**Qué ocurre y cómo verificarlo:** El recorrido descubre todas las posiciones: 0 3 5; indexOf por sí solo no muestra todas.

**Microacción 4.** Verificar ausencia usando -1.

**Fragmento relevante que escribirás o localizarás en el archivo:**

```java
System.out.println("Posicion de Mario: " + asistentes.indexOf("Mario"));
```

**Qué ocurre y cómo verificarlo:** No hay Mario en la lista y la búsqueda devuelve -1. La posición 0 es un resultado válido, no ausencia.

### Rastreo del estado: antes, operación y consecuencia

| Hito | Estado o resultado | Interpretación |
|---|---|---|
| Registro original | [Rosa, Ana, Luis, Rosa, Eva, Rosa] | Rosa aparece 3 veces |
| contains/indexOf/lastIndexOf | true / 0 / 5 | Presencia, primera y última posición |
| Recorrido por índices | 0, 3, 5 | Todas las coincidencias |
| indexOf("Mario") | -1 | No presente |

### Programa completo que se construye

**Archivo ``**

```java
import java.util.ArrayList;

public class EJ04 {
    public static void main(String[] args) {
        ArrayList<String> asistentes = new ArrayList<>();
        for (String nombre : new String[]{"Rosa", "Ana", "Luis", "Rosa", "Eva", "Rosa"}) {
            asistentes.add(nombre);
        }
        System.out.println("Lista: " + asistentes);
        System.out.println("Contiene Rosa: " + asistentes.contains("Rosa"));
        System.out.println("Primera Rosa: " + asistentes.indexOf("Rosa"));
        System.out.println("Ultima Rosa: " + asistentes.lastIndexOf("Rosa"));
        System.out.print("Todas las posiciones de Rosa:");
        for (int i = 0; i < asistentes.size(); i++) {
            if (asistentes.get(i).equals("Rosa")) System.out.print(" " + i);
        }
        System.out.println();
        System.out.println("Posicion de Mario: " + asistentes.indexOf("Mario"));
    }
}
```

### Predicción concreta antes de Run

1. Señala qué instrucciones cambian la lista y cuáles solo consultan o imprimen.
2. Anticipa la primera y la última línea de la salida y argumenta cómo se llegó a ellas.
3. Explica qué sucedería si la entrada tuviese un elemento repetido o faltante.

### Ejecución real, salida esperada e interpretación

```text
Lista: [Rosa, Ana, Luis, Rosa, Eva, Rosa]
Contiene Rosa: true
Primera Rosa: 0
Ultima Rosa: 5
Todas las posiciones de Rosa: 0 3 5
Posicion de Mario: -1
```

**Lectura de la salida:** La posición `-1` significa que el dato no está presente. Las líneas anteriores se obtuvieron ejecutando el código que aparece en esta misma sección; no son datos simulados.

### Error que debemos poder diagnosticar

**Síntoma / decisión equivocada:** Evaluar presencia con `indexOf(...) > 0`: deja fuera a los datos del índice cero.

**Causa y corrección:** Usar `>= 0` o comparar con `-1`; para todas las ocurrencias recorrer los índices.

### Preguntas para defender el razonamiento

- ¿Por qué `indexOf(...) == 0` no significa ausencia?
- ¿Es posible recuperar TODAS las posiciones usando solo una llamada a `indexOf`?

### Prueba de transferencia adicional

Evalúa el comportamiento si Leo aparece una sola vez; ¿coinciden primero y último?

## T04 — Informe de asistencia con duplicados (tarea espejo evaluable)

Crea `T04.java` con `[Leo, Mia, Leo, Zoe, Leo, Ana]`. Debes mostrar si Leo está presente, primer índice, último índice y TODAS sus posiciones mediante un `for`. Consulta también a Luis y comunica `No inscrito` cuando `indexOf` devuelva -1. No confundas primera coincidencia con cantidad total.

**Archivos a crear:** `T04.java`.

**Secuencia de resolución sugerida:** reproduce el planteamiento, dibuja la lista inicial con índices, escribe las operaciones, anota las salidas antes de ejecutar, prueba un caso límite y documenta por qué la solución satisface cada criterio.

**Criterios de aceptación verificables:**

- Leo está presente; índices 0,2,4.
- Primera posición 0 y última 4.
- Luis no inscrito.

**Entrega:** código propio que compile y salida de consola; incluye una explicación de cinco a ocho líneas sobre las precondiciones, cambios de estado y resultados.



---

# EJ05 — Ordenar y buscar sin alterar el orden original

**Área:** Collections · **Modalidad:** AULA · **Tarea espejo:** T05

### Situación y dificultad que resolveremos

Antes de confirmar la inscripción, se necesita buscar rápidamente a Rosa en una lista alfabética. La búsqueda binaria depende de que el orden sea compatible. Para conservar el historial de recepción, se obtiene una copia de los nombres y se ordena la copia.

### Objetivo técnico y evidencia de aprendizaje

Ordenar una copia con `Collections.sort`, encontrar a Rosa con `binarySearch`, reconocer el índice basado en cero y detectar por qué no es válido buscar en un orden arbitrario. El estudiante debe poder identificar el estado anterior de la lista, la operación aplicada, su efecto y el resultado que confirma que funcionó.

### Descomposición antes de codificar

**1. Preservación.** `new ArrayList<>(original)` genera una lista distinta; ordenar la copia no reorganiza el registro de ingreso.

**2. Precondición.** `Collections.sort(ordenada)` se ejecuta ANTES de `binarySearch`.

**3. Evidencia.** La secuencia resultante contiene siete nombres; Rosa queda en índice 6 (contando desde cero).

**4. Caso ausente.** Si el valor no se encuentra, `binarySearch` devuelve un número negativo que no debe interpretarse como índice válido.

### Construcción progresiva en IntelliJ

**Microacción 1.** Cargar la lista en orden de llegada.

**Fragmento relevante que escribirás o localizarás en el archivo:**

```java
ArrayList<String> ordenada = new ArrayList<>(ingreso);
```

**Qué ocurre y cómo verificarlo:** La copia es independiente; la lista ingreso conserva exactamente el orden en que llegaron las siete inscripciones.

**Microacción 2.** Copiarla para preservar el historial.

**Fragmento relevante que escribirás o localizarás en el archivo:**

```java
Collections.sort(ordenada);
```

**Qué ocurre y cómo verificarlo:** La copia se convierte en [Andres, Diego, Juan, Marcos, Marcos, Maria, Rosa].

**Microacción 3.** Aplicar `Collections.sort` a la copia.

**Fragmento relevante que escribirás o localizarás en el archivo:**

```java
int indiceRosa = Collections.binarySearch(ordenada, "Rosa");
```

**Qué ocurre y cómo verificarlo:** Rosa queda en el índice 6; es el séptimo elemento porque los índices parten de cero.

**Microacción 4.** Ejecutar `binarySearch` y analizar resultados positivos/negativos.

**Fragmento relevante que escribirás o localizarás en el archivo:**

```java
int indiceZoe = Collections.binarySearch(ordenada, "Zoe");
```

**Qué ocurre y cómo verificarlo:** El valor obtenido es negativo y la condición indiceZoe >= 0 es false, por tanto no se accede a ese índice.

**Microacción 5.** Aplicar `reverse` solo después de las búsquedas.

**Fragmento relevante que escribirás o localizarás en el archivo:**

```java
Collections.reverse(ordenada);
```

**Qué ocurre y cómo verificarlo:** Se invierte solamente DESPUÉS de buscar; una búsqueda natural sobre este orden ya no tendría la precondición de orden ascendente.

### Rastreo del estado: antes, operación y consecuencia

| Hito | Estado o resultado | Interpretación |
|---|---|---|
| Ingreso | [Maria, Juan, Andres, Rosa, Marcos, Diego, Marcos] | Orden cronológico |
| Copia + sort | [Andres, Diego, Juan, Marcos, Marcos, Maria, Rosa] | Orden natural ascendente |
| binarySearch Rosa | 6 | Séptimo elemento, índice cero-based |
| binarySearch Zoe | negativo | No se debe acceder como índice |
| reverse final | [Rosa, Maria, Marcos, Marcos, Juan, Diego, Andres] | No repetir binarySearch natural ahora |

### Programa completo que se construye

**Archivo ``**

```java
import java.util.ArrayList;
import java.util.Collections;

public class EJ05 {
    public static void main(String[] args) {
        ArrayList<String> ingreso = new ArrayList<>();
        for (String nombre : new String[]{"Maria", "Juan", "Andres", "Rosa", "Marcos", "Diego", "Marcos"}) {
            ingreso.add(nombre);
        }
        ArrayList<String> ordenada = new ArrayList<>(ingreso);
        Collections.sort(ordenada);
        System.out.println("Ingreso: " + ingreso);
        System.out.println("Ordenada: " + ordenada);

        int indiceRosa = Collections.binarySearch(ordenada, "Rosa");
        System.out.println("Indice Rosa: " + indiceRosa);
        int indiceZoe = Collections.binarySearch(ordenada, "Zoe");
        System.out.println("Zoe encontrada: " + (indiceZoe >= 0));
        System.out.println("Ingreso intacto: " + ingreso);
        Collections.reverse(ordenada);
        System.out.println("Invertida al final: " + ordenada);
    }
}
```

### Predicción concreta antes de Run

1. Señala qué instrucciones cambian la lista y cuáles solo consultan o imprimen.
2. Anticipa la primera y la última línea de la salida y argumenta cómo se llegó a ellas.
3. Explica qué sucedería si la entrada tuviese un elemento repetido o faltante.

### Ejecución real, salida esperada e interpretación

```text
Ingreso: [Maria, Juan, Andres, Rosa, Marcos, Diego, Marcos]
Ordenada: [Andres, Diego, Juan, Marcos, Marcos, Maria, Rosa]
Indice Rosa: 6
Zoe encontrada: false
Ingreso intacto: [Maria, Juan, Andres, Rosa, Marcos, Diego, Marcos]
Invertida al final: [Rosa, Maria, Marcos, Marcos, Juan, Diego, Andres]
```

**Lectura de la salida:** Si el valor no se encuentra, `binarySearch` devuelve un número negativo que no debe interpretarse como índice válido. Las líneas anteriores se obtuvieron ejecutando el código que aparece en esta misma sección; no son datos simulados.

### Error que debemos poder diagnosticar

**Síntoma / decisión equivocada:** Usar búsqueda binaria sobre lista desordenada o leer el resultado negativo como posición.

**Causa y corrección:** Ordenar con criterio coherente, buscar antes de invertir y tratar resultado >=0 como encontrado.

### Preguntas para defender el razonamiento

- ¿Por qué es incorrecto utilizar `Collections.binarySearch` natural sobre la lista invertida?
- ¿Qué hace `new ArrayList<>(ingreso)` que no hace `ArrayList<String> copia = ingreso`?

### Prueba de transferencia adicional

Inscribe un nombre nuevo a la lista original; ¿por qué la copia ordenada no lo reflejará automáticamente?

## T05 — Búsqueda en nómina de ponentes (tarea espejo evaluable)

Construye `T05.java` con el ingreso `[Zoe, Ana, Luis, Eva, Mario]`: realiza una COPIA, ordénala con `Collections.sort`, busca a `Luis` con `binarySearch`, comprueba si `Nora` existe y demuestra que el ingreso conserva el orden original. Invierte la copia SOLO después de terminar todas las búsquedas. Explica en un comentario por qué no se recomienda buscar binariamente después de `reverse` sin criterio compatible.

**Archivos a crear:** `T05.java`.

**Secuencia de resolución sugerida:** reproduce el planteamiento, dibuja la lista inicial con índices, escribe las operaciones, anota las salidas antes de ejecutar, prueba un caso límite y documenta por qué la solución satisface cada criterio.

**Criterios de aceptación verificables:**

- Copia alfabética [Ana, Eva, Luis, Mario, Zoe].
- Luis localizado en índice 2.
- Nora ausente sin interpretar el valor negativo como índice.
- La lista de ingreso no cambió.

**Entrega:** código propio que compile y salida de consola; incluye una explicación de cinco a ocho líneas sobre las precondiciones, cambios de estado y resultados.



---

# EJ06 — Preparar listados descendentes y un sorteo verificable

**Área:** Collections · **Modalidad:** AUTÓNOMO · **Tarea espejo:** T06

### Situación y dificultad que resolveremos

Los mismos inscritos deben ordenarse en orden alfabético inverso para un informe, y después mezclarse para un sorteo. Se requiere comprobar que la mezcla no cambió ni la cantidad ni las frecuencias de nombres, aunque el orden resultante varíe.

### Objetivo técnico y evidencia de aprendizaje

Aplicar un comparador de orden inverso, usar `Collections.shuffle` y validar invariantes después de una operación aleatoria. El estudiante debe poder identificar el estado anterior de la lista, la operación aplicada, su efecto y el resultado que confirma que funcionó.

### Descomposición antes de codificar

**1. Criterio inverso.** `Collections.sort(lista, Collections.reverseOrder())` ordena con criterio explícito.

**2. Registro de referencia.** Se crea una copia antes de mezclar para comparar cantidades y contenido.

**3. Mezcla.** `shuffle` altera posiciones; su salida no es fija y no debe evaluarse contra una secuencia exacta.

**4. Verificación.** Tras ordenar ambas listas de comparación, se confirma que conservan los mismos elementos, incluso repetidos.

### Construcción progresiva en IntelliJ

**Microacción 1.** Ordenar usando `Collections.reverseOrder`.

**Fragmento relevante que escribirás o localizarás en el archivo:**

```java
Collections.sort(turnos, Collections.reverseOrder());
```

**Qué ocurre y cómo verificarlo:** El orden descendente es [Rosa, Mario, Luis, Ana, Ana]. reverseOrder es el criterio usado por sort.

**Microacción 2.** Guardar lista de control antes de la mezcla.

**Fragmento relevante que escribirás o localizarás en el archivo:**

```java
ArrayList<String> control = new ArrayList<>(turnos);
```

**Qué ocurre y cómo verificarlo:** control captura exactamente el mismo multiconjunto antes de mezclar.

**Microacción 3.** Mezclar y NO asumir secuencia fija.

**Fragmento relevante que escribirás o localizarás en el archivo:**

```java
Collections.shuffle(turnos);
```

**Qué ocurre y cómo verificarlo:** El orden es variable; incluso podría coincidir casualmente con el original. No existe resultado único.

**Microacción 4.** Ordenar copias para comparar contenido y frecuencia.

**Fragmento relevante que escribirás o localizarás en el archivo:**

```java
Collections.sort(turnos);
Collections.sort(control);
System.out.println("Mismos participantes: " + control.equals(turnos));
```

**Qué ocurre y cómo verificarlo:** Al ordenar ambos y compararlos se verifica el contenido sin depender del azar; Ana permanece repetida dos veces.

### Rastreo del estado: antes, operación y consecuencia

| Hito | Estado o resultado | Interpretación |
|---|---|---|
| sort inverso | [Rosa, Mario, Luis, Ana, Ana] | Criterio descendente |
| shuffle | Orden variable | No esperar una cadena fija |
| ordenar y comparar | Mismos participantes = true | La mezcla cambió posiciones, no contenido |

### Programa completo que se construye

**Archivo ``**

```java
import java.util.ArrayList;
import java.util.Collections;

public class EJ06 {
    public static void main(String[] args) {
        ArrayList<String> turnos = new ArrayList<>();
        for (String nombre : new String[]{"Rosa", "Ana", "Luis", "Ana", "Mario"}) turnos.add(nombre);
        Collections.sort(turnos, Collections.reverseOrder());
        System.out.println("Descendente: " + turnos);
        ArrayList<String> control = new ArrayList<>(turnos);
        Collections.shuffle(turnos);
        System.out.println("Mezcla: " + turnos);
        System.out.println("Mismo tamano: " + (control.size() == turnos.size()));
        Collections.sort(turnos);
        Collections.sort(control);
        System.out.println("Mismos participantes: " + control.equals(turnos));
        System.out.println("Frecuencia Ana: " + Collections.frequency(turnos, "Ana"));
    }
}
```

### Predicción concreta antes de Run

1. Señala qué instrucciones cambian la lista y cuáles solo consultan o imprimen.
2. Anticipa la primera y la última línea de la salida y argumenta cómo se llegó a ellas.
3. Explica qué sucedería si la entrada tuviese un elemento repetido o faltante.

### Ejecución real, salida esperada e interpretación

```text
Descendente: [Rosa, Mario, Luis, Ana, Ana]
Mezcla: [Mario, Rosa, Ana, Luis, Ana]
Mismo tamano: true
Mismos participantes: true
Frecuencia Ana: 2
```

**Lectura de la salida:** Tras ordenar ambas listas de comparación, se confirma que conservan los mismos elementos, incluso repetidos. Las líneas anteriores se obtuvieron ejecutando el código que aparece en esta misma sección; no son datos simulados.

### Error que debemos poder diagnosticar

**Síntoma / decisión equivocada:** Afirmar que siempre se obtiene un orden específico después de `shuffle`.

**Causa y corrección:** Comparar invariantes (tamaño y multiconjunto de elementos), no una salida aleatoria exacta.

### Preguntas para defender el razonamiento

- ¿Por qué una mezcla correcta puede volver a producir accidentalmente el mismo orden?
- ¿Por qué no basta comparar las dos listas sin ordenarlas si queremos comprobar sus elementos?

### Prueba de transferencia adicional

Justifica por qué `Collections.reverse` no es igual a un nuevo ordenamiento descendente si la lista no estaba previamente ordenada.

## T06 — Organizar sorteos sin perder asistentes (tarea espejo evaluable)

Crea `T06.java` con `[Pia, Omar, Ana, Pia, Zoe]`. Ordena con `Collections.reverseOrder`, muestra el resultado descendente, guarda copia, mezcla con `shuffle`, y valida que el total y los elementos son los mismos (después de ordenar ambos listados para comparar). Debe permanecer dos veces Pia y el programa no debe suponer un orden fijo después de mezclar.

**Archivos a crear:** `T06.java`.

**Secuencia de resolución sugerida:** reproduce el planteamiento, dibuja la lista inicial con índices, escribe las operaciones, anota las salidas antes de ejecutar, prueba un caso límite y documenta por qué la solución satisface cada criterio.

**Criterios de aceptación verificables:**

- Orden descendente [Zoe, Pia, Pia, Omar, Ana].
- Los 5 nombres persisten tras mezclar.
- Pia sigue apareciendo 2 veces.

**Entrega:** código propio que compile y salida de consola; incluye una explicación de cinco a ocho líneas sobre las precondiciones, cambios de estado y resultados.



---

# EJ07 — Construir un resumen de calificaciones y frecuencias

**Área:** Collections · **Modalidad:** AUTÓNOMO · **Tarea espejo:** T07

### Situación y dificultad que resolveremos

El docente recibe calificaciones discretas y debe informar valor mayor, menor y cuántas veces se repite una nota específica. La información se mantiene como números enteros; la lista no se clasifica como aprobado/desaprobado porque el objetivo es operar con colecciones.

### Objetivo técnico y evidencia de aprendizaje

Utilizar `Collections.max`, `min`, `frequency` con una lista numérica, validar la precondición de lista no vacía y calcular el rango de valores. El estudiante debe poder identificar el estado anterior de la lista, la operación aplicada, su efecto y el resultado que confirma que funcionó.

### Descomposición antes de codificar

**1. Datos.** `ArrayList<Integer>` guarda valores enteros en una lista dinámica.

**2. Datos antes del cálculo.** `max` y `min` requieren que exista al menos un elemento.

**3. Interpretación.** `frequency(lista, 15)` cuenta apariciones, no posiciones ni porcentajes.

**4. Resultado.** El rango es la diferencia entre el máximo y mínimo, un dato derivado de los dos extremos.

### Construcción progresiva en IntelliJ

**Microacción 1.** Cargar las siete notas sin perder repeticiones.

**Fragmento relevante que escribirás o localizarás en el archivo:**

```java
ArrayList<Integer> notas = new ArrayList<>();
for (int n : new int[]{12, 15, 18, 15, 10, 15, 20}) notas.add(n);
```

**Qué ocurre y cómo verificarlo:** Se conservan siete calificaciones, tres de ellas con valor 15.

**Microacción 2.** Validar la lista antes de obtener max y min.

**Fragmento relevante que escribirás o localizarás en el archivo:**

```java
if (!notas.isEmpty()) {
    int mayor = Collections.max(notas);
    int menor = Collections.min(notas);
}
```

**Qué ocurre y cómo verificarlo:** Solo se consultan extremos cuando hay al menos una nota: max=20, min=10.

**Microacción 3.** Calcular la frecuencia y derivar el rango.

**Fragmento relevante que escribirás o localizarás en el archivo:**

```java
Collections.frequency(notas, 15);
int rango = mayor - menor;
```

**Qué ocurre y cómo verificarlo:** La nota 15 aparece 3 veces; el rango 20-10 es 10.

**Microacción 4.** Preparar el escenario de lista vacía.

**Fragmento relevante que escribirás o localizarás en el archivo:**

```java
ArrayList<Integer> vacia = new ArrayList<>();
System.out.println(vacia.isEmpty());
```

**Qué ocurre y cómo verificarlo:** La lista está vacía. En ese estado llamar a max/min no tendría un elemento extremo.

**Microacción 5.** Confirmar el caso límite sin solicitar extremos.

**Fragmento relevante que escribirás o localizarás en el archivo:**

```java
System.out.println("Extremos vacia: no aplica = " + vacia.isEmpty());
```

**Qué ocurre y cómo verificarlo:** Esta línea confirma que el caso límite se trató sin consultar extremos y permite distinguir ausencia de datos de calificación mínima.

### Rastreo del estado: antes, operación y consecuencia

| Hito | Estado o resultado | Interpretación |
|---|---|---|
| Carga | [12, 15, 18, 15, 10, 15, 20] | 7 registros |
| max y min | 20 y 10 | Rango = 10 |
| frequency 15 | 3 | Tres notas iguales |
| lista sin elementos | [] | No ejecutar max/min |

### Programa completo que se construye

**Archivo ``**

```java
import java.util.ArrayList;
import java.util.Collections;

public class EJ07 {
    public static void main(String[] args) {
        ArrayList<Integer> notas = new ArrayList<>();
        for (int n : new int[]{12, 15, 18, 15, 10, 15, 20}) notas.add(n);
        System.out.println("Notas: " + notas);
        if (!notas.isEmpty()) {
            int mayor = Collections.max(notas);
            int menor = Collections.min(notas);
            System.out.println("Mayor: " + mayor);
            System.out.println("Menor: " + menor);
            System.out.println("Rango: " + (mayor - menor));
            System.out.println("Frecuencia 15: " + Collections.frequency(notas, 15));
        }
        ArrayList<Integer> vacia = new ArrayList<>();
        System.out.println("Extremos vacia: no aplica = " + vacia.isEmpty());
    }
}
```

### Predicción concreta antes de Run

1. Señala qué instrucciones cambian la lista y cuáles solo consultan o imprimen.
2. Anticipa la primera y la última línea de la salida y argumenta cómo se llegó a ellas.
3. Explica qué sucedería si la entrada tuviese un elemento repetido o faltante.

### Ejecución real, salida esperada e interpretación

```text
Notas: [12, 15, 18, 15, 10, 15, 20]
Mayor: 20
Menor: 10
Rango: 10
Frecuencia 15: 3
Extremos vacia: no aplica = true
```

**Lectura de la salida:** El rango es la diferencia entre el máximo y mínimo, un dato derivado de los dos extremos. Las líneas anteriores se obtuvieron ejecutando el código que aparece en esta misma sección; no son datos simulados.

### Error que debemos poder diagnosticar

**Síntoma / decisión equivocada:** Ejecutar `max` sobre una lista vacía y provocar `NoSuchElementException`.

**Causa y corrección:** Comprobar `isEmpty()` antes de calcular extremos y explicar qué significa una frecuencia cero.

### Preguntas para defender el razonamiento

- ¿Cuándo `frequency` devuelve 0?
- ¿Qué condición debe cumplirse antes de usar `max/min`?

### Prueba de transferencia adicional

Agrega otra nota 20 y predice qué resultados cambian y cuáles quedan iguales.

## T07 — Auditoría de notas de prácticas (tarea espejo evaluable)

Escribe `T07.java` con las notas `[11, 17, 14, 17, 20, 11]`. Informa nota mínima, máxima, rango, frecuencia de 17 y frecuencia de 9. Antes de llamar a `max` o `min`, verifica que la lista no esté vacía; añade al final una lista vacía y comunica que allí no se deben buscar extremos.

**Archivos a crear:** `T07.java`.

**Secuencia de resolución sugerida:** reproduce el planteamiento, dibuja la lista inicial con índices, escribe las operaciones, anota las salidas antes de ejecutar, prueba un caso límite y documenta por qué la solución satisface cada criterio.

**Criterios de aceptación verificables:**

- Valor mínimo 11, máximo 20, rango 9.
- Frecuencia 17 = 2, frecuencia 9 = 0.
- No se intenta max/min de una lista vacía.

**Entrega:** código propio que compile y salida de consola; incluye una explicación de cinco a ocho líneas sobre las precondiciones, cambios de estado y resultados.



---

# EJ08 — Normalizar estados y proteger una copia de respaldo

**Área:** Collections · **Modalidad:** AUTÓNOMO · **Tarea espejo:** T08

### Situación y dificultad que resolveremos

Una lista de estados fue registrada con códigos no uniformes y debe transformarse. El equipo desea una versión normalizada y otra copia para ensayar operaciones sin destruir el registro original.

### Objetivo técnico y evidencia de aprendizaje

Aplicar `replaceAll`, preparar un destino de capacidad lógica suficiente para `copy`, usar `fill` solo sobre una lista separada y comparar original/copia. El estudiante debe poder identificar el estado anterior de la lista, la operación aplicada, su efecto y el resultado que confirma que funcionó.

### Descomposición antes de codificar

**1. Reemplazar coincidencias.** `Collections.replaceAll` sustituye todas las apariciones del valor elegido.

**2. Copia real.** `Collections.copy` exige destino con `size >= origen.size`; la capacidad inicial reservada no es suficiente.

**3. Rellenar.** `Collections.fill` reemplaza elementos existentes sin crear posiciones nuevas.

**4. Protección.** La copia de trabajo puede ser alterada sin modificar el listado normalizado.

### Construcción progresiva en IntelliJ

**Microacción 1.** Crear el registro inicial de estados.

**Fragmento relevante que escribirás o localizarás en el archivo:**

```java
ArrayList<String> estados = new ArrayList<>();
```

**Qué ocurre y cómo verificarlo:** Se crea una lista para mantener el registro de estados previo a normalizar, sin sustituir su contenido por un texto fijo.

**Microacción 2.** Normalizar todas las apariciones del código pendiente.

**Fragmento relevante que escribirás o localizarás en el archivo:**

```java
boolean modifico = Collections.replaceAll(estados, "PEND", "PENDIENTE");
```

**Qué ocurre y cómo verificarlo:** Las dos apariciones de PEND cambian a PENDIENTE; el boolean indica que existieron reemplazos.

**Microacción 3.** Preparar destino con posiciones reales para copy.

**Fragmento relevante que escribirás o localizarás en el archivo:**

```java
ArrayList<String> respaldo = new ArrayList<>();
for (int i = 0; i < estados.size(); i++) respaldo.add("SIN_DATO");
```

**Qué ocurre y cómo verificarlo:** El respaldo ya tiene cuatro ELEMENTOS reales; no se confunde la capacidad reservada con tamaño de lista.

**Microacción 4.** Copiar el origen al destino correctamente.

**Fragmento relevante que escribirás o localizarás en el archivo:**

```java
Collections.copy(respaldo, estados);
```

**Qué ocurre y cómo verificarlo:** El respaldo toma los cuatro elementos del origen en las mismas posiciones.

**Microacción 5.** Rellenar solo la copia de trabajo y comprobar que el origen se preservó.

**Fragmento relevante que escribirás o localizarás en el archivo:**

```java
Collections.fill(respaldo, "REVISAR");
```

**Qué ocurre y cómo verificarlo:** Se reemplazan los cuatro valores del respaldo. Estados permanece normalizada e independiente.

### Rastreo del estado: antes, operación y consecuencia

| Hito | Estado o resultado | Interpretación |
|---|---|---|
| Original | [PEND, OK, PEND, OBS] | Dos registros PEND |
| replaceAll | [PENDIENTE, OK, PENDIENTE, OBS] | Ambos cambiaron |
| copy | Destino igual al origen | Mismo número de elementos |
| fill solo destino | [REVISAR, REVISAR, REVISAR, REVISAR] | La fuente no se altera |

### Programa completo que se construye

**Archivo ``**

```java
import java.util.ArrayList;
import java.util.Collections;

public class EJ08 {
    public static void main(String[] args) {
        ArrayList<String> estados = new ArrayList<>();
        for (String s : new String[]{"PEND", "OK", "PEND", "OBS"}) estados.add(s);
        System.out.println("Original: " + estados);
        boolean modifico = Collections.replaceAll(estados, "PEND", "PENDIENTE");
        System.out.println("Hubo cambio: " + modifico);
        System.out.println("Normalizada: " + estados);

        ArrayList<String> respaldo = new ArrayList<>();
        for (int i = 0; i < estados.size(); i++) respaldo.add("SIN_DATO");
        Collections.copy(respaldo, estados);
        System.out.println("Respaldo: " + respaldo);
        Collections.fill(respaldo, "REVISAR");
        System.out.println("Copia para pruebas: " + respaldo);
        System.out.println("Fuente preservada: " + estados);
    }
}
```

### Predicción concreta antes de Run

1. Señala qué instrucciones cambian la lista y cuáles solo consultan o imprimen.
2. Anticipa la primera y la última línea de la salida y argumenta cómo se llegó a ellas.
3. Explica qué sucedería si la entrada tuviese un elemento repetido o faltante.

### Ejecución real, salida esperada e interpretación

```text
Original: [PEND, OK, PEND, OBS]
Hubo cambio: true
Normalizada: [PENDIENTE, OK, PENDIENTE, OBS]
Respaldo: [PENDIENTE, OK, PENDIENTE, OBS]
Copia para pruebas: [REVISAR, REVISAR, REVISAR, REVISAR]
Fuente preservada: [PENDIENTE, OK, PENDIENTE, OBS]
```

**Lectura de la salida:** La copia de trabajo puede ser alterada sin modificar el listado normalizado. Las líneas anteriores se obtuvieron ejecutando el código que aparece en esta misma sección; no son datos simulados.

### Error que debemos poder diagnosticar

**Síntoma / decisión equivocada:** Crear `new ArrayList<>(origen.size())` y llamar a `Collections.copy`: la capacidad puede ser suficiente, pero el tamaño lógico sigue siendo cero.

**Causa y corrección:** Inicializar el destino con `Collections.nCopies` u otros elementos reales antes de copiar.

### Preguntas para defender el razonamiento

- ¿Cuál es la diferencia entre `ArrayList` con capacidad 5 y lista con 5 elementos?
- ¿`fill` agrega nuevos elementos?

### Prueba de transferencia adicional

Intenta reemplazar un código inexistente y explica el resultado boolean de `replaceAll`.

## T08 — Preparar copia de seguridad de estados (tarea espejo evaluable)

Construye `T08.java` con `[P, A, P, B, P]`. Reemplaza TODOS los códigos P por PENDIENTE y muestra si `replaceAll` efectuó cambios. Copia la lista a un destino que ya contenga cinco posiciones, usa `fill` para poner `VERIFICAR` solo en la copia, e imprime ambos listados. Documenta por qué un `new ArrayList<>(5)` vacío NO es destino suficiente para `Collections.copy`.

**Archivos a crear:** `T08.java`.

**Secuencia de resolución sugerida:** reproduce el planteamiento, dibuja la lista inicial con índices, escribe las operaciones, anota las salidas antes de ejecutar, prueba un caso límite y documenta por qué la solución satisface cada criterio.

**Criterios de aceptación verificables:**

- P se reemplaza tres veces.
- El respaldo contiene el mismo orden y longitud.
- fill modifica la copia, no el origen.
- No se usa un destino vacío para copy.

**Entrega:** código propio que compile y salida de consola; incluye una explicación de cinco a ocho líneas sobre las precondiciones, cambios de estado y resultados.



---

# EJ09 — Integrar un gestor de inscripciones con reglas y búsquedas seguras

**Área:** ArrayList + Collections · **Modalidad:** AULA: vista completa + cierre autónomo · **Tarea espejo:** T09

### Situación y dificultad que resolveremos

Un centro de formación necesita una clase que registre participantes, rechace nombres vacíos, evite inscripciones duplicadas y permita obtener una nómina alfabética SIN modificar el orden de llegada. También debe manejar búsquedas de datos presentes y ausentes y demostrar que devuelve copias seguras.

### Objetivo técnico y evidencia de aprendizaje

Diseñar `GestorInscripciones` con encapsulamiento, métodos que reportan éxito o fracaso, ordenamiento de una copia, búsqueda binaria correctamente preparada y comprobación de invariantes en un caso de ejecución completo. El estudiante debe poder identificar el estado anterior de la lista, la operación aplicada, su efecto y el resultado que confirma que funcionó.

### Descomposición antes de codificar

**1. Responsabilidad.** El campo `private ArrayList<String>` mantiene la lista de llegada bajo control de un solo objeto.

**2. Validación.** `registrar` rechaza null, cadenas vacías y nombres repetidos; el retorno explica la decisión.

**3. Ordenamiento seguro.** `ordenados()` crea copia y la ordena; no rompe el historial de recepción.

**4. Búsqueda.** `buscarEnOrdenados` construye una lista ordenada antes de llamar a `binarySearch`.

**5. Verificación.** main prueba altas válidas/inválidas, orden, búsqueda y retiro; cada resultado es comprobable.

### Construcción progresiva en IntelliJ

**Microacción 1.** Crear `GestorInscripciones` con atributo privado.

**Fragmento relevante que escribirás o localizarás en el archivo:**

```java
private final ArrayList<String> nombres = new ArrayList<>();
```

**Qué ocurre y cómo verificarlo:** La lista pertenece al gestor y no se expone directamente; final impide sustituir la referencia del campo.

**Microacción 2.** Implementar altas con validación de datos y duplicados.

**Fragmento relevante que escribirás o localizarás en el archivo:**

```java
if (nombre == null || nombre.isBlank()) return false;
String limpio = nombre.trim();
if (nombres.contains(limpio)) return false;
```

**Qué ocurre y cómo verificarlo:** Se valida antes de insertar: se rechaza null/blanco y un nombre existente. ArrayList permite duplicados; esta es una regla específica del gestor.

**Microacción 3.** Crear `ordenados` sin mutar la lista interna.

**Fragmento relevante que escribirás o localizarás en el archivo:**

```java
ArrayList<String> copia = new ArrayList<>(nombres);
Collections.sort(copia);
return copia;
```

**Qué ocurre y cómo verificarlo:** El historial de llegada queda intacto porque se ordena una lista nueva.

**Microacción 4.** Buscar binariamente solo sobre copia ordenada.

**Fragmento relevante que escribirás o localizarás en el archivo:**

```java
ArrayList<String> copia = ordenados();
return Collections.binarySearch(copia, nombre.trim());
```

**Qué ocurre y cómo verificarlo:** El método de búsqueda recibe una copia ya ordenada; no depende de que el ingreso original tenga orden alfabético.

**Microacción 5.** Crear clase principal con 11 pruebas de aceptación.

**Fragmento relevante que escribirás o localizarás en el archivo:**

```java
System.out.println("Duplicado Rosa: " + g.registrar("Rosa"));
System.out.println("Existe Zoe: " + (g.buscarEnOrdenados("Zoe") >= 0));
```

**Qué ocurre y cómo verificarlo:** Main debe demostrar no solo éxito: duplicado devuelve false y nombre ausente también aparece como no encontrado.

### Rastreo del estado: antes, operación y consecuencia

| Hito | Estado o resultado | Interpretación |
|---|---|---|
| Registrar tres | [Rosa, Ana, Luis] | Llegada |
| Intentar Rosa y blanco | false, false | Reglas de negocio |
| ordenados() | [Ana, Luis, Rosa] | Copia ordenada; llegada original intacta |
| buscar Rosa | 2 | Índice en copia ordenada, no en llegada |
| retirar Luis dos veces | true, false | Segundo intento no encontró al participante |

### Programa completo que se construye

**Archivo `GestorInscripciones.java`**

```java
import java.util.ArrayList;
import java.util.Collections;

public class GestorInscripciones {
    private final ArrayList<String> nombres = new ArrayList<>();

    public boolean registrar(String nombre) {
        if (nombre == null || nombre.isBlank()) return false;
        String limpio = nombre.trim();
        if (nombres.contains(limpio)) return false;
        nombres.add(limpio);
        return true;
    }

    public boolean retirar(String nombre) {
        if (nombre == null) return false;
        return nombres.remove(nombre.trim());
    }

    public ArrayList<String> ordenados() {
        ArrayList<String> copia = new ArrayList<>(nombres);
        Collections.sort(copia);
        return copia;
    }

    public int buscarEnOrdenados(String nombre) {
        if (nombre == null) return -1;
        ArrayList<String> copia = ordenados();
        return Collections.binarySearch(copia, nombre.trim());
    }

    public int cantidad() { return nombres.size(); }
    public ArrayList<String> llegada() { return new ArrayList<>(nombres); }
}
```


**Archivo `EJ09.java`**

```java
public class EJ09 {
    public static void main(String[] args) {
        GestorInscripciones g = new GestorInscripciones();
        System.out.println("Alta Rosa: " + g.registrar("Rosa"));
        System.out.println("Alta Ana: " + g.registrar("Ana"));
        System.out.println("Alta Luis: " + g.registrar("Luis"));
        System.out.println("Duplicado Rosa: " + g.registrar("Rosa"));
        System.out.println("Nombre vacio: " + g.registrar(" "));
        System.out.println("Orden llegada: " + g.llegada());
        System.out.println("Orden alfabetico: " + g.ordenados());
        System.out.println("Indice Rosa ordenado: " + g.buscarEnOrdenados("Rosa"));
        System.out.println("Existe Zoe: " + (g.buscarEnOrdenados("Zoe") >= 0));
        System.out.println("Sale Luis: " + g.retirar("Luis"));
        System.out.println("Sale Luis otra vez: " + g.retirar("Luis"));
        System.out.println("Quedan: " + g.llegada() + " | total=" + g.cantidad());
    }
}
```

### Predicción concreta antes de Run

1. Señala qué instrucciones cambian la lista y cuáles solo consultan o imprimen.
2. Anticipa la primera y la última línea de la salida y argumenta cómo se llegó a ellas.
3. Explica qué sucedería si la entrada tuviese un elemento repetido o faltante.

### Ejecución real, salida esperada e interpretación

```text
Alta Rosa: true
Alta Ana: true
Alta Luis: true
Duplicado Rosa: false
Nombre vacio: false
Orden llegada: [Rosa, Ana, Luis]
Orden alfabetico: [Ana, Luis, Rosa]
Indice Rosa ordenado: 2
Existe Zoe: false
Sale Luis: true
Sale Luis otra vez: false
Quedan: [Rosa, Ana] | total=2
```

**Lectura de la salida:** main prueba altas válidas/inválidas, orden, búsqueda y retiro; cada resultado es comprobable. Las líneas anteriores se obtuvieron ejecutando el código que aparece en esta misma sección; no son datos simulados.

### Error que debemos poder diagnosticar

**Síntoma / decisión equivocada:** Ordenar directamente el atributo interno y cambiar sin querer la cronología de inscripciones, o devolver la referencia interna.

**Causa y corrección:** Separar responsabilidades: alta/retiro mutan estado; consulta/ordenados devuelven datos o copias. Validar nombre antes de operar.

### Preguntas para defender el razonamiento

- ¿Por qué el atributo es privado y el método llegada retorna copia?
- ¿Por qué buscarEnOrdenados es seguro aunque el orden de llegada sea arbitrario?
- ¿Qué diferencia hay entre permitir duplicados a nivel ArrayList y rechazarlos como regla del negocio?

### Prueba de transferencia adicional

Introduce una prueba donde el cliente modifica la lista devuelta por `llegada()`: la lista interna debe conservarse.

## T09 — Gestor de turnos con reglas verificables (tarea espejo evaluable)

Crea `GestorTurnos.java` y `T09.java`. El gestor guarda una lista privada y expone `registrar`, `retirar`, `ordenados`, `buscarOrdenado`, `cantidad` y `llegada`. Prohíbe vacíos y duplicados, y `ordenados` debe devolver copia. En main registra `[Zoe, Ana, Luis]`, intenta repetir `Ana`, ordena una copia, busca a `Luis`, busca `Pia` (ausente), retira Zoe dos veces y verifica que la lista de llegada no se reordenó. Incluye un caso vacío.

**Archivos a crear:** `GestorTurnos.java`, `T09.java`.

**Secuencia de resolución sugerida:** reproduce el planteamiento, dibuja la lista inicial con índices, escribe las operaciones, anota las salidas antes de ejecutar, prueba un caso límite y documenta por qué la solución satisface cada criterio.

**Criterios de aceptación verificables:**

- Se aceptan tres altas, se rechazan duplicado y blanco.
- La lista de llegada mantiene [Zoe, Ana, Luis] después de ordenar la copia.
- Luis tiene índice 1 en la lista alfabética.
- Pia no existe; segundo retiro Zoe devuelve false.
- Quedan [Ana, Luis] y nuevo gestor tiene cero elementos.

**Entrega:** código propio que compile y salida de consola; incluye una explicación de cinco a ocho líneas sobre las precondiciones, cambios de estado y resultados.


---

# 5. Cierre y evaluación de salida

Explica con un ejemplo propio por qué `set` no equivale a `add(indice, elemento)`, por qué `Collections.copy` no funciona con una lista destino de tamaño cero y por qué `binarySearch` exige un criterio de orden previo. Presenta una salida válida y una invalidación controlada: una inscripción duplicada rechazada, un índice fuera de rango tratado o una búsqueda ausente. La evidencia no es solo que el código ejecute, sino que puedas justificar la consecuencia de cada operación.

**Próxima práctica:** profundiza en el integrador `GestorInscripciones` y contrasta las diferencias entre una lista que almacena datos y los métodos de la clase que la administra.
