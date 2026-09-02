---
title: "Guía del Estudiante - Sesión 01"
subtitle: "Programación Orientada a Objetos: Java, IDE, clases y objetos"
author: "Elaborado por el docente - Lideratec Academy"
date: ""
lang: es-PE
toc: true
toc-depth: 3
geometry: margin=2cm
fontsize: 10.5pt
mainfont: "DejaVu Sans"
monofont: "DejaVu Sans Mono"
header-includes:
  - |
    \usepackage{fancyhdr}
    \usepackage{xurl}
    \pagestyle{fancy}
    \fancyhf{}
    \fancyhead[L]{Lideratec Academy}
    \fancyhead[R]{POO - Sesión 01}
    \fancyfoot[C]{\thepage}
    \setlength{\headheight}{14pt}
---

# Programación Orientada a Objetos - Sesión 01

## Práctica guiada

**De un archivo Java a tus primeros objetos: clase `Felinos`, objetos, atributos, métodos y mensajes**

## Propósito

Esta guía está diseñada para acompañarte durante toda la sesión. No vas a recibir solamente un programa terminado para copiar. Construirás cada parte de forma progresiva, la ejecutarás, observarás qué ocurre, modificarás el código, provocarás errores controlados y comprobarás por qué una solución funciona.

Al finalizar debes poder explicar con tus propias palabras:

1. qué función cumplen JDK, JVM, archivo `.java`, archivo `.class` y método `main`;
2. para qué utilizamos un IDE;
3. qué diferencia existe entre Front End y Back End;
4. qué es una clase y qué es un objeto;
5. qué representan los atributos y los métodos;
6. cómo se crea una instancia mediante `new`;
7. cómo un objeto recibe una llamada a un método;
8. cómo varios objetos creados a partir de una misma clase pueden conservar datos diferentes;
9. cómo agrupar conceptualmente varios objetos;
10. cómo reconocer y corregir errores básicos de una aplicación Java inicial.

## Resultado de aprendizaje observable

Al terminar la práctica podrás crear y ejecutar una aplicación Java pequeña formada por dos o más clases, instanciar objetos, asignar valores a sus atributos, invocar métodos y explicar el resultado observado.

## Duración sugerida

**180 minutos de trabajo académico neto.**

Si tu equipo todavía no tiene Java o un IDE, la preparación puede requerir tiempo adicional. En un laboratorio institucional, utiliza siempre la instalación autorizada por el docente.

## Conocimientos previos

Solo se requiere:

- manejo básico de Windows;
- crear y localizar carpetas;
- descargar archivos desde sitios oficiales;
- escribir y guardar texto;
- seguir instrucciones en una consola o IDE.

No se asume experiencia previa con Programación Orientada a Objetos.

# 1. Ruta de aprendizaje

Durante la sesión avanzarás en esta secuencia:

```text
COMPRENDER EL ENTORNO JAVA
        ↓
COMPROBAR EL JDK
        ↓
VER .java → .class → JVM → main
        ↓
PREPARAR EL IDE
        ↓
RECONOCER CLASE Y OBJETO
        ↓
CONSTRUIR LA CLASE Felinos
        ↓
CREAR UN OBJETO
        ↓
ASIGNAR ATRIBUTOS
        ↓
INVOCAR MÉTODOS
        ↓
CREAR MÁS OBJETOS
        ↓
INTERPRETAR MENSAJES Y PARÁMETROS
        ↓
AGRUPAR OBJETOS
        ↓
INTEGRAR Y VALIDAR
```

# 2. Entorno tecnológico de referencia

Para esta práctica utilizaremos como ruta principal:

- **Java Development Kit:** JDK 25 LTS.
- **IDE principal:** IntelliJ IDEA 2026.2 o una versión 2026.2.x estable disponible en el laboratorio.
- **Sistema de referencia:** Windows de 64 bits.

## 2.1 ¿Por qué esta combinación?

El JDK es el entorno que necesitamos para desarrollar, compilar y ejecutar programas Java. Para una sesión académica inicial conviene trabajar con una versión LTS estable.

IntelliJ IDEA será el IDE principal porque proporciona un entorno integrado para crear proyectos Java, editar código, detectar errores y ejecutar aplicaciones. Sus funciones centrales para Java pueden utilizarse sin una suscripción de pago.

### Alternativas válidas

Si el docente o el laboratorio ya trabaja con otro entorno, el código de esta guía también puede desarrollarse con:

- Visual Studio Code + soporte Java;
- Apache NetBeans 31 o una versión vigente equivalente.

**Importante:** Java no depende conceptualmente de IntelliJ, VS Code o NetBeans. El IDE es una herramienta para escribir y ejecutar el código; los conceptos de clase, objeto, atributo y método son los mismos.

# 3. Reconoce los componentes antes de instalar

| Componente | Qué es | Para qué lo necesitas hoy |
|---|---|---|
| JDK | Entorno de desarrollo Java | Compilar y ejecutar los programas de la sesión |
| `javac` | Compilador incluido en el JDK | Convertir un archivo `.java` en bytecode `.class` |
| JVM | Máquina virtual de Java | Ejecutar el bytecode generado |
| Entorno de ejecución | Componentes necesarios para ejecutar Java | Se utilizan cuando ejecutas el programa |
| IDE | Entorno integrado de desarrollo | Crear proyectos, editar, detectar errores y ejecutar |
| Java API | Conjunto de clases y paquetes de Java | Proporciona funcionalidades reutilizables |

## Precisión importante sobre JRE

En el estudio conceptual de Java encontrarás el término **JRE (Java Runtime Environment)** para referirte al entorno de ejecución. En un entorno moderno de desarrollo no necesitas instalar necesariamente un JRE independiente: al instalar un JDK dispones de los componentes de ejecución necesarios para desarrollar y probar tus programas.

# 4. Preparación del JDK paso a paso

## Paso 1. Abrir una consola

**Objetivo:** comprobar si tu equipo ya tiene un JDK disponible.

**Dónde hacerlo:** Símbolo del sistema o PowerShell.

1. Presiona la tecla **Windows**.
2. Escribe `cmd` o `PowerShell`.
3. Abre la aplicación.
4. Escribe:

```text
java -version
```

5. Presiona Enter.
6. Luego escribe:

```text
javac -version
```

7. Presiona Enter.

### Qué debes observar

Si el JDK está correctamente disponible, ambos comandos mostrarán una versión.

### ¿Qué significa cada comando?

- `java -version` comprueba el lanzador utilizado para ejecutar Java.
- `javac -version` comprueba el compilador Java.

### Punto de control

Completa:

- Versión mostrada por `java -version`: __________________________
- Versión mostrada por `javac -version`: _________________________

### Si `java` funciona pero `javac` no

No continúes suponiendo que todo está listo. Puede existir un entorno de ejecución o una configuración incompleta del JDK. Si estás en un laboratorio institucional, consulta al docente antes de modificar variables del sistema.

## Paso 2. Revisar la carpeta del JDK

En Windows una instalación de Oracle JDK suele encontrarse bajo:

```text
C:\Program Files\Java\
```

Dentro puedes encontrar una carpeta parecida a:

```text
jdk-25
```

El número exacto puede variar por actualización.

**No borres otras versiones instaladas.** Solo estamos identificando el entorno disponible.

## Paso 3. Descargar JDK 25 LTS si hace falta

**Sitio oficial:**

<https://www.oracle.com/java/technologies/downloads/>

### Ruta recomendada en Windows

1. Abre el sitio oficial.
2. Ubica **JDK 25**.
3. Selecciona **Windows**.
4. Identifica la opción para **x64 Installer** si tu equipo es Windows x64.
5. Descarga el instalador `.exe`.

No elijas ARM64 salvo que tu equipo realmente utilice arquitectura ARM64.

## Paso 4. Instalar el JDK

1. Abre tu carpeta **Descargas**.
2. Localiza el instalador descargado.
3. Ejecútalo.
4. Si Windows solicita permisos administrativos, confirma solo si tienes autorización.
5. Mantén la ubicación predeterminada salvo indicación del laboratorio.
6. Finaliza el asistente.
7. Cierra la consola que utilizaste antes.
8. Abre una consola nueva.
9. Ejecuta otra vez:

```text
java -version
javac -version
```

### Resultado esperado

Ambos comandos deben responder con una versión Java disponible.

### Si falla

Antes de modificar `PATH` manualmente:

1. confirma que el JDK terminó de instalarse;
2. abre una consola nueva;
3. verifica la carpeta de instalación;
4. si es un equipo institucional, consulta al docente.

# 5. Microejemplo 1 - Ver realmente `.java → .class → JVM`

## Qué aprenderás

Comprobarás de manera visible que un archivo fuente `.java` puede compilarse y producir un archivo `.class`, y que después la JVM puede ejecutar ese bytecode.

## Situación

Antes de utilizar el IDE vamos a ejecutar un programa mínimo desde consola. Esto te permitirá entender qué automatiza después el IDE.

## Paso 1. Crear una carpeta de práctica

1. Crea una carpeta llamada:

```text
POO_S01
```

2. Dentro crea otra carpeta:

```text
microejemplo_java
```

## Paso 2. Crear `HolaJava.java`

Abre un editor de texto y escribe:

```java
public class HolaJava {
    public static void main(String[] args) {
        System.out.println("Hola desde Java");
    }
}
```

Guarda el archivo con el nombre exacto:

```text
HolaJava.java
```

### ¿Qué debes reconocer por ahora?

```java
public class HolaJava
```

Define una clase llamada `HolaJava`.

```java
public static void main(String[] args)
```

Es el método que utilizaremos como punto de entrada de esta aplicación.

```java
System.out.println("Hola desde Java");
```

Imprime un texto para que podamos observar que el programa se ejecutó.

No necesitas memorizar todavía el significado profundo de todos los modificadores de `main`. En esta sesión debes reconocer la firma completa y su función como punto de inicio.

## Paso 3. Abrir la consola en la carpeta

Ubícate mediante consola en la carpeta donde guardaste `HolaJava.java`.

Puedes comprobar el contenido con:

```text
dir
```

Debes observar `HolaJava.java`.

## Paso 4. Compilar

Escribe:

```text
javac HolaJava.java
```

### Qué debería ocurrir

Si no existen errores de sintaxis, el comando termina sin mostrar un mensaje de error.

Ahora ejecuta:

```text
dir
```

Debes observar al menos:

```text
HolaJava.java
HolaJava.class
```

### Qué acaba de ocurrir

```text
HolaJava.java
      ↓ javac
HolaJava.class
```

El compilador convirtió el código fuente en bytecode.

## Paso 5. Ejecutar

Escribe:

```text
java HolaJava
```

Observa que **no escribimos `.class`** al ejecutar.

### Resultado esperado

```text
Hola desde Java
```

### ¿Qué participó?

```text
Código fuente
HolaJava.java
      ↓
Compilador javac
      ↓
Bytecode
HolaJava.class
      ↓
JVM / entorno Java
      ↓
main
      ↓
Salida en consola
```

## Ahora modifica

Cambia:

```java
System.out.println("Hola desde Java");
```

por:

```java
System.out.println("Mi primera ejecución Java");
```

Guarda el archivo y ejecuta directamente:

```text
java HolaJava
```

### Pregunta

¿Cambió el texto?

Respuesta: ________________________________________________

### Explicación

Si no recompilaste, el archivo `.class` continúa conteniendo la versión anterior.

Ahora ejecuta:

```text
javac HolaJava.java
java HolaJava
```

### ¿Qué aprendiste?

Modificar `.java` no modifica automáticamente el `.class` compilado cuando trabajas manualmente desde consola. El IDE suele automatizar este proceso por ti.

## Probemos un error controlado

Cambia temporalmente:

```java
System.out.println("Mi primera ejecución Java");
```

por:

```java
System.out.println("Mi primera ejecución Java")
```

Elimina el `;`.

Compila:

```text
javac HolaJava.java
```

### Qué observar

El compilador señalará un error de sintaxis.

### Corrige

Vuelve a colocar `;`, guarda y recompila.

### Punto de control

- [ ] Sé qué archivo escribo: `.java`.
- [ ] Sé qué archivo genera `javac`: `.class`.
- [ ] Pude ejecutar con `java NombreClase`.
- [ ] Entiendo que `main` inicia esta aplicación.
- [ ] Vi un error de compilación y lo corregí.

# 6. Preparación de IntelliJ IDEA

## Paso 1. Descargar IntelliJ IDEA

**Sitio oficial:**

<https://www.jetbrains.com/idea/download/>

En la distribución actual IntelliJ IDEA se ofrece como un producto unificado. Las funciones centrales para desarrollo Java continúan disponibles sin costo después del periodo de prueba de las funciones avanzadas.

### Qué debes hacer

1. Abre la página oficial.
2. Selecciona Windows.
3. Descarga el instalador correspondiente a la arquitectura de tu equipo.
4. Ejecuta el instalador.
5. Mantén las opciones predeterminadas salvo que el laboratorio indique otra configuración.
6. Abre IntelliJ IDEA.

## Paso 2. Crear un proyecto Java vacío

1. En la pantalla inicial selecciona **New Project**.
2. Elige **Java**.
3. Nombre del proyecto:

```text
GestionZooApp
```

4. En **JDK**, selecciona JDK 25 si ya está detectado.
5. Si no aparece, utiliza **Add JDK from Disk** y apunta a la carpeta del JDK instalado.
6. Si el equipo no tiene un JDK y el laboratorio permite descargarlo desde el IDE, IntelliJ también ofrece **Download JDK**.
7. Para esta sesión utiliza el sistema de construcción simple del propio IDE si aparece como **IntelliJ**.
8. No agregues frameworks.
9. Desactiva código de ejemplo automático si aparece.
10. Crea el proyecto.

### Qué debes observar

Aparecerá una ventana con:

- panel de proyecto;
- carpeta `src`;
- editor central;
- controles para ejecutar;
- ventana de salida cuando ejecutes una clase.

### Punto de control

- [ ] IntelliJ abre correctamente.
- [ ] El proyecto `GestionZooApp` fue creado.
- [ ] El proyecto utiliza un JDK.
- [ ] Veo la carpeta `src`.

# 7. IDE y Java API - qué debes reconocer

## 7.1 ¿Qué hace el IDE?

Un IDE integra herramientas que facilitan el desarrollo. En esta sesión lo usaremos para:

- crear clases;
- escribir código;
- detectar errores;
- compilar;
- ejecutar;
- leer la salida.

El IDE no reemplaza los conceptos de Java. Cuando pulsas **Run**, el IDE está coordinando operaciones que anteriormente realizaste manualmente.

## 7.2 Java API

La Java API proporciona clases organizadas para reutilizar funcionalidades.

Debes reconocer estos términos mencionados en la sesión:

- **JAR:** archivo que puede empaquetar clases compiladas y otros recursos;
- **package:** permite agrupar clases;
- **class:** plantilla a partir de la cual se pueden crear objetos.

También reconocerás nombres de paquetes como:

- `java.lang`;
- `java.util`;
- `java.io`;
- `java.sql`;
- `javax.swing`.

No necesitas memorizar sus clases internas en esta sesión.

# 8. Front End y Back End - actividad breve

## Idea clave

En una arquitectura de aplicaciones:

- **Front End:** lado del cliente o usuario.
- **Back End:** lado del servidor.

## Clasifica

| Elemento | ¿Front End o Back End? | ¿Por qué? |
|---|---|---|
| Navegador web del usuario |  |  |
| Aplicación cliente instalada |  |  |
| Servidor web |  |  |
| Servidor de datos |  |  |

## Mini caso

Un estudiante abre un navegador, ingresa a una aplicación web y consulta información guardada en un servidor de datos.

Responde:

1. ¿Qué elemento está del lado del usuario? __________________________
2. ¿Qué elementos están del lado servidor? __________________________
3. ¿Dónde se encuentran los datos? __________________________________

# 9. Programación Orientada a Objetos - de la realidad al programa

## Idea clave

La POO busca representar elementos relevantes de un problema mediante objetos y sus interacciones.

Un objeto posee:

- **atributos:** características;
- **métodos:** comportamientos u operaciones.

## Ejemplo conceptual - Felinos

Piensa en varios felinos:

- Nube;
- Micifuz;
- un tigre;
- un león.

Pueden compartir características generales, pero cada objeto concreto puede tener valores propios.

### Clase como plantilla

```text
Felinos
├── nombreEspecie
├── nombrePropio
├── color
├── edad
├── cazar()
├── comer()
├── saltar()
└── dormir()
```

### Objetos concretos

```text
Objeto 1
nombrePropio = Nube
nombreEspecie = gato

Objeto 2
nombrePropio = Micifuz
nombreEspecie = gato
```

**La clase describe. El objeto representa una instancia concreta.**

# 10. Microejemplo 2 - Crear la clase `Felinos` desde cero

## Qué construiremos

Primero crearemos solamente la estructura de la clase. Después la iremos ampliando.

## Paso 1. Crear el archivo

1. En IntelliJ, abre `src`.
2. Clic derecho.
3. Selecciona **New > Java Class**.
4. Nombre:

```text
Felinos
```

Debe crearse:

```text
Felinos.java
```

## Versión 1 - Clase vacía

```java
public class Felinos {

}
```

### Qué significa

- `class` indica que estamos definiendo una clase.
- `Felinos` es el nombre elegido para la clase.
- `{ }` delimitan su contenido.

### Punto de control

Antes de avanzar, confirma que el archivo se llama `Felinos.java` y la clase pública `Felinos`.

# 11. Microejemplo 3 - Agregar atributos uno por uno

## Versión 2 - Primer atributo

Dentro de la clase escribe:

```java
public class Felinos {
    String nombrePropio;
}
```

## ¿Qué representa?

`nombrePropio` describe una característica que cada objeto podrá almacenar.

Ahora agrega:

```java
String nombreEspecie;
```

La clase queda:

```java
public class Felinos {
    String nombrePropio;
    String nombreEspecie;
}
```

Agrega también:

```java
String color;
int edad;
```

Resultado:

```java
public class Felinos {
    String nombrePropio;
    String nombreEspecie;
    String color;
    int edad;
}
```

## Analicemos

`String` será utilizado para texto.

`int` será utilizado en este ejercicio para un número entero como la edad.

Lo importante hoy es reconocer que los atributos pertenecen a la estructura de la clase y cada objeto podrá conservar sus propios valores.

## Ahora hazlo tú

Señala qué atributo utilizarías para:

- guardar `"Nube"`: __________________
- guardar `"gato"`: ___________________
- guardar `"pardo"`: __________________
- guardar `7`: _________________________

# 12. Microejemplo 4 - Agregar un comportamiento

## Versión 3 - Primer método

Agrega debajo de los atributos:

```java
public void chequeoSalud() {
    System.out.println("Chequeo de salud de " + nombrePropio);
}
```

La clase completa queda:

```java
public class Felinos {
    String nombrePropio;
    String nombreEspecie;
    String color;
    int edad;

    public void chequeoSalud() {
        System.out.println("Chequeo de salud de " + nombrePropio);
    }
}
```

## ¿Qué hace el método?

Representa un comportamiento llamado `chequeoSalud`.

Dentro utilizamos una salida en consola para observar cuándo se ejecuta.

## Lectura natural

```java
public void chequeoSalud()
```

Puedes leerlo hoy como:

> La clase define una operación llamada `chequeoSalud` que podrá ejecutarse sobre un objeto `Felinos`.

## Agrega un segundo método

```java
public void alimentacion() {
    System.out.println("Alimentación de " + nombrePropio);
}
```

## Punto de control

Tu clase debe contener:

- [ ] `nombrePropio`;
- [ ] `nombreEspecie`;
- [ ] `color`;
- [ ] `edad`;
- [ ] `chequeoSalud()`;
- [ ] `alimentacion()`.

# 13. Microejemplo 5 - Crear la clase de arranque `GestionZoo`

## Paso 1. Crear una segunda clase

Dentro de `src`, crea:

```text
GestionZoo
```

Escribe:

```java
public class GestionZoo {
    public static void main(String[] args) {

    }
}
```

## ¿Qué representa `main`?

En esta aplicación `main` será el punto desde el que comenzaremos a ejecutar instrucciones.

No necesitas profundizar todavía en `public`, `static`, `void` o `String[] args`. Debes reconocer la firma completa y saber que el código que coloquemos dentro de sus llaves será parte de la secuencia inicial.

## Ejecuta por primera vez

Pulsa el botón de ejecución asociado a `GestionZoo.main()`.

### Qué debería ocurrir

La aplicación termina sin imprimir nada porque todavía no colocamos instrucciones visibles.

### ¿Por qué es útil este paso?

Acabas de comprobar que:

- la clase compila;
- el IDE reconoce `main`;
- el proyecto puede ejecutarse.

# 14. Microejemplo 6 - Crear el primer objeto

Dentro de `main` escribe:

```java
Felinos miFelino = new Felinos();
```

La clase queda:

```java
public class GestionZoo {
    public static void main(String[] args) {
        Felinos miFelino = new Felinos();
    }
}
```

## Descomposición de la línea

### `Felinos`

Es el tipo del objeto que queremos utilizar.

### `miFelino`

Es el nombre de la variable mediante la que accederemos al objeto.

### `=`

Asocia la variable con la nueva instancia creada.

### `new`

Solicita la creación de una nueva instancia.

### `Felinos()`

Construye un objeto basado en la clase `Felinos`.

## Lectura natural completa

> Crea un nuevo objeto de tipo `Felinos` y permite acceder a ese objeto mediante la variable `miFelino`.

## Pregunta de predicción

¿Crear el objeto ya le asigna automáticamente el nombre `Nube`?

Respuesta: ______________________________________________________

# 15. Microejemplo 7 - Asignar valores al objeto

Agrega:

```java
miFelino.nombrePropio = "Nube";
miFelino.nombreEspecie = "gato";
miFelino.color = "pardo";
miFelino.edad = 3;
```

## Analicemos una línea

```java
miFelino.nombrePropio = "Nube";
```

### `miFelino`

Indica sobre qué objeto estamos trabajando.

### `.`

Permite acceder a un miembro del objeto.

### `nombrePropio`

Es el atributo que vamos a modificar.

### `=`

Asigna un valor.

### `"Nube"`

Es el valor que guardaremos.

## Antes y después

Antes de la asignación:

```text
miFelino.nombrePropio → sin valor asignado explícitamente
```

Después:

```text
miFelino.nombrePropio → "Nube"
```

# 16. Microejemplo 8 - Invocar métodos del objeto

Agrega:

```java
miFelino.chequeoSalud();
miFelino.alimentacion();
```

Tu `main` queda:

```java
public class GestionZoo {
    public static void main(String[] args) {
        Felinos miFelino = new Felinos();

        miFelino.nombrePropio = "Nube";
        miFelino.nombreEspecie = "gato";
        miFelino.color = "pardo";
        miFelino.edad = 3;

        miFelino.chequeoSalud();
        miFelino.alimentacion();
    }
}
```

## Ejecuta

### Resultado esperado

```text
Chequeo de salud de Nube
Alimentación de Nube
```

## ¿Qué ocurrió?

En:

```java
miFelino.chequeoSalud();
```

- objeto destinatario: `miFelino`;
- método solicitado: `chequeoSalud`;
- parámetros: ninguno en este ejemplo.

## Predice antes de cambiar

¿Qué salida esperas si reemplazas:

```java
miFelino.nombrePropio = "Nube";
```

por:

```java
miFelino.nombrePropio = "Luna";
```

Predicción: ______________________________________________________

Haz el cambio, ejecuta y compara.

# 17. Error controlado 1 - Comillas incorrectas

Copia temporalmente esta línea:

```java
miFelino.nombrePropio = “Nube”;
```

Observa que las comillas son tipográficas.

## Qué ocurre

El compilador o el IDE marcará un problema porque Java espera comillas válidas para delimitar el texto.

## Corrige

```java
miFelino.nombrePropio = "Nube";
```

## Aprendizaje

Cuando copies código desde un procesador de texto, verifica que las comillas no hayan sido reemplazadas por comillas tipográficas.

# 18. Error controlado 2 - Ejecutar antes de asignar el nombre

Mueve temporalmente:

```java
miFelino.chequeoSalud();
```

antes de:

```java
miFelino.nombrePropio = "Nube";
```

Ejemplo:

```java
Felinos miFelino = new Felinos();
miFelino.chequeoSalud();
miFelino.nombrePropio = "Nube";
```

## Predice

¿Qué crees que aparecerá en la salida?

Predicción: ______________________________________________________

## Ejecuta

Probablemente observarás:

```text
Chequeo de salud de null
```

## ¿Qué significa `null` aquí?

Para esta práctica basta con interpretar que el atributo de texto todavía no tenía un valor asignado explícitamente cuando el método intentó utilizarlo.

## Corrige

Asigna primero el nombre y llama después al método.

# 19. Microejemplo 9 - Dos objetos de una misma clase

Ahora crea un segundo objeto debajo del primero:

```java
Felinos segundoFelino = new Felinos();
segundoFelino.nombrePropio = "Micifuz";
segundoFelino.nombreEspecie = "gato";
segundoFelino.color = "pardo atigrado";
segundoFelino.edad = 7;
segundoFelino.chequeoSalud();
```

## Ejecuta

Debes observar salidas asociadas a dos objetos diferentes.

## Compara

| Elemento | `miFelino` | `segundoFelino` |
|---|---|---|
| Clase | `Felinos` | `Felinos` |
| `nombrePropio` | Nube | Micifuz |
| `nombreEspecie` | gato | gato |
| `color` | pardo | pardo atigrado |
| `edad` | 3 | 7 |

## Idea central

La clase es una plantilla común. Cada objeto conserva su propio estado.

## Ahora hazlo tú - tercer objeto

Crea:

```text
tercerFelino
```

Condiciones:

- debe ser una nueva instancia de `Felinos`;
- debe tener un nombre diferente;
- debe tener especie, color y edad;
- debe ejecutar `chequeoSalud()`;
- no copies exactamente los valores de Nube ni Micifuz.

### Evidencia

Escribe la salida obtenida:

__________________________________________________________________

# 20. Microejemplo 10 - Mensaje con parámetro usando una bicicleta

El ejemplo de interacción entre objetos incluye tres elementos:

1. objeto destinatario;
2. método;
3. datos o parámetros.

Para verlo en código construiremos una clase pequeña.

## Paso 1. Crear `Bicicleta`

```java
public class Bicicleta {
    int marchaActual;

    public void cambiarDeMarcha(int marcha) {
        marchaActual = marcha;
        System.out.println("Marcha actual: " + marchaActual);
    }
}
```

## Paso 2. Crear `PruebaBicicleta`

```java
public class PruebaBicicleta {
    public static void main(String[] args) {
        Bicicleta tuBicicleta = new Bicicleta();
        tuBicicleta.cambiarDeMarcha(3);
    }
}
```

## Analiza la llamada

```java
tuBicicleta.cambiarDeMarcha(3);
```

### Objeto destinatario

```text
tuBicicleta
```

### Método

```text
cambiarDeMarcha
```

### Parámetro enviado

```text
3
```

## Ejecuta

Resultado esperado:

```text
Marcha actual: 3
```

## Ahora modifica

Cambia `3` por `5`.

Antes de ejecutar, escribe tu predicción:

__________________________________________________________________

Después ejecuta y compara.

# 21. Contenedor - agrupar objetos

## Idea conceptual

Un contenedor permite agrupar varios objetos y acceder a ellos para gestionarlos.

En esta sesión no necesitamos estudiar todavía toda la API de colecciones. Para visualizar la idea utilizaremos un arreglo sencillo de objetos `Felinos`.

## Microejemplo 11 - Arreglo de felinos

Después de crear tres objetos, puedes agruparlos así:

```java
Felinos[] misFelinos = {miFelino, segundoFelino, tercerFelino};
```

## Qué representa

```text
misFelinos
├── miFelino
├── segundoFelino
└── tercerFelino
```

## Acceso uno por uno

Puedes observar el primer nombre con:

```java
System.out.println(misFelinos[0].nombrePropio);
```

Luego:

```java
System.out.println(misFelinos[1].nombrePropio);
System.out.println(misFelinos[2].nombrePropio);
```

## Resultado esperado

Aparecerán los nombres de los tres objetos.

## Precisión de la sesión

El objetivo de este bloque es comprender la idea de **agrupar objetos**. La sintaxis completa de listas, conjuntos y mapas puede estudiarse en una sesión posterior.

# 22. Integración - proyecto final de la sesión

## Objetivo

Integrar clase, atributos, métodos, objetos, mensajes y agrupación básica.

## Requisitos

Tu proyecto debe contener:

### Clase `Felinos`

- `nombrePropio`;
- `nombreEspecie`;
- `color`;
- `edad`;
- `chequeoSalud()`;
- `alimentacion()`.

### Clase `GestionZoo`

Debe:

1. contener `main`;
2. crear al menos tres objetos `Felinos`;
3. asignar valores diferentes;
4. invocar métodos;
5. agrupar los objetos en un arreglo;
6. mostrar al menos los nombres almacenados.

## Versión de referencia estructural

No copies valores necesariamente. Utiliza tus propios datos.

```java
public class Felinos {
    String nombrePropio;
    String nombreEspecie;
    String color;
    int edad;

    public void chequeoSalud() {
        System.out.println("Chequeo de salud de " + nombrePropio);
    }

    public void alimentacion() {
        System.out.println("Alimentación de " + nombrePropio);
    }
}
```

```java
public class GestionZoo {
    public static void main(String[] args) {
        Felinos felino1 = new Felinos();
        felino1.nombrePropio = "Nube";
        felino1.nombreEspecie = "gato";
        felino1.color = "pardo";
        felino1.edad = 3;

        Felinos felino2 = new Felinos();
        felino2.nombrePropio = "Micifuz";
        felino2.nombreEspecie = "gato";
        felino2.color = "pardo atigrado";
        felino2.edad = 7;

        Felinos felino3 = new Felinos();
        felino3.nombrePropio = "Luna";
        felino3.nombreEspecie = "gato";
        felino3.color = "gris";
        felino3.edad = 2;

        felino1.chequeoSalud();
        felino2.chequeoSalud();
        felino3.chequeoSalud();

        Felinos[] misFelinos = {felino1, felino2, felino3};

        System.out.println("Felinos registrados:");
        System.out.println(misFelinos[0].nombrePropio);
        System.out.println(misFelinos[1].nombrePropio);
        System.out.println(misFelinos[2].nombrePropio);
    }
}
```

# 23. Actividades progresivas

## Actividad 1 - Reconocimiento

Completa:

| Elemento | Tipo |
|---|---|
| `Felinos` | clase / objeto |
| `miFelino` | clase / objeto-referencia usada para acceder a una instancia |
| `nombrePropio` | atributo / método |
| `chequeoSalud()` | atributo / método |
| `new Felinos()` | creación de instancia / asignación de texto |

## Actividad 2 - Lectura de código

Observa:

```java
Felinos miFelino = new Felinos();
miFelino.nombrePropio = "Nube";
miFelino.chequeoSalud();
```

Responde:

1. ¿Qué instrucción crea la instancia?
2. ¿Qué instrucción asigna un valor?
3. ¿Cuál es el objeto destinatario de la llamada?
4. ¿Cuál es el método?
5. ¿Recibe parámetros?

## Actividad 3 - Modificación controlada

Agrega un método a `Felinos`:

```java
public void dormir() {
    System.out.println(nombrePropio + " está durmiendo");
}
```

Después llama al método desde uno de tus objetos.

### Antes de ejecutar

Predice la salida:

__________________________________________________________________

### Después de ejecutar

Salida real:

__________________________________________________________________

## Actividad 4 - Mensaje con parámetro

En el ejemplo:

```java
tuBicicleta.cambiarDeMarcha(4);
```

Completa:

- destinatario: ______________________
- método: ____________________________
- parámetro: _________________________

## Actividad 5 - Integración

Crea un cuarto felino y agrégalo al arreglo.

Comprueba que el programa muestra también su nombre.

# 24. Errores frecuentes y diagnóstico

| Problema observado | Causa probable | Qué revisar | Corrección inicial |
|---|---|---|---|
| `java` no se reconoce | JDK ausente o configuración de terminal | `java -version` | Verificar JDK y abrir una consola nueva |
| `javac` no se reconoce | Compilador no disponible en la ruta | `javac -version` | Revisar instalación del JDK o consultar al docente |
| IntelliJ no reconoce JDK | Proyecto sin SDK/JDK configurado | Configuración del proyecto | Seleccionar JDK 25 instalado |
| `cannot find symbol` | Nombre incorrecto o clase no accesible | Ortografía de clase/atributo/método | Comparar nombre exacto |
| Nombre de archivo y clase pública no coinciden | Clase pública guardada con otro nombre | Archivo `.java` | Igualar nombre de clase y archivo |
| Error cerca de `“Nube”` | Comillas tipográficas | Delimitadores | Reemplazar por `"Nube"` |
| Falta `;` | Instrucción incompleta | Final de línea | Agregar `;` |
| No aparece salida | Método no fue invocado o clase incorrecta | `main` y Run | Ejecutar clase correcta |
| Aparece `null` | Atributo de texto usado antes de asignación | Orden de instrucciones | Asignar antes de ejecutar el método |
| Cambié `.java` pero consola manual muestra versión anterior | No recompilaste | `.class` | Ejecutar `javac` otra vez |

# 25. Preguntas de comprobación

1. ¿Cuál es la diferencia entre `.java` y `.class`?
2. ¿Qué hace `javac`?
3. ¿Qué función cumple la JVM?
4. ¿Qué función cumple `main` en esta práctica?
5. ¿Por qué utilizamos un JDK para desarrollar?
6. ¿Qué aporta un IDE?
7. ¿Cuál es la diferencia entre clase y objeto?
8. ¿Qué es un atributo?
9. ¿Qué es un método?
10. ¿Qué significa `new Felinos()`?
11. En `miFelino.chequeoSalud()`, ¿quién es el destinatario?
12. En `tuBicicleta.cambiarDeMarcha(3)`, ¿qué dato es el parámetro?
13. ¿Por qué dos objetos de `Felinos` pueden tener nombres diferentes?
14. ¿Para qué sirve agrupar objetos en un contenedor?
15. ¿Cómo diferenciarías Front End y Back End?

# 26. Evidencias de aprendizaje

Prepara:

1. `Felinos.java`;
2. `GestionZoo.java`;
3. `Bicicleta.java` y `PruebaBicicleta.java`, si el docente solicita el microejemplo;
4. captura de `java -version` o `javac -version`;
5. captura de ejecución de `GestionZoo`;
6. evidencia del tercer o cuarto objeto creado por ti;
7. respuestas a las preguntas indicadas por el docente.

No se define aquí una fecha o plataforma de entrega porque debe utilizarse la indicada en el aula virtual.

# 27. Checklist final

- [ ] Identifico JDK, JVM, `.java`, `.class` y `main`.
- [ ] Ejecuté `java -version` y `javac -version`.
- [ ] Compilé manualmente un ejemplo con `javac`.
- [ ] Vi aparecer un archivo `.class`.
- [ ] Ejecuté una clase con `java`.
- [ ] Abrí IntelliJ IDEA y configuré un JDK.
- [ ] Distingo Front End y Back End.
- [ ] Distingo clase y objeto.
- [ ] Reconozco atributos y métodos.
- [ ] Construí `Felinos` progresivamente.
- [ ] Creé una instancia con `new`.
- [ ] Asigné valores a atributos.
- [ ] Invoqué métodos.
- [ ] Creé varios objetos de la misma clase.
- [ ] Interpreté una llamada con parámetro.
- [ ] Agrupé objetos en un arreglo.
- [ ] Analicé al menos dos errores controlados.
- [ ] Completé una modificación propia.
- [ ] Preparé las evidencias solicitadas.

# 28. Cierre de aprendizaje

Al completar la sesión no solo escribiste una clase Java. Observaste el recorrido del código fuente hasta su ejecución, comprobaste qué automatiza un IDE y construiste progresivamente una solución orientada a objetos.

Debes conservar especialmente estas ideas:

- el archivo `.java` contiene el código fuente;
- el compilador produce bytecode `.class`;
- la JVM participa en la ejecución;
- `main` es el punto de entrada de la aplicación trabajada;
- una clase define una plantilla;
- un objeto es una instancia concreta;
- los atributos conservan información;
- los métodos representan comportamiento;
- `new` permite crear una nueva instancia;
- los objetos pueden recibir llamadas a métodos;
- varios objetos creados con la misma clase pueden tener datos diferentes;
- un contenedor permite agrupar objetos.

## Qué debes repasar antes de la siguiente sesión

1. clase versus objeto;
2. atributo versus método;
3. `new` e instanciación;
4. `objeto.metodo()`;
5. objeto, método y parámetro en una interacción;
6. `main` y flujo de ejecución;
7. `.java → .class → JVM`.

## Recursos de refuerzo

- Blog Lideratec Academy: <https://lideratecacademy.com/>
- Canal YouTube Lideratec Academy: <https://www.youtube.com/@LideratecAcademy>

Vuelve a ejecutar los ejemplos cambiando valores. La comprensión mejora cuando puedes predecir qué ocurrirá antes de pulsar **Run**.
