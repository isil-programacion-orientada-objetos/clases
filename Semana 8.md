# SESIÓN 08 — RETO SIMETRÍA WEB · V5
## FASE 13 · GUÍA DEL ESTUDIANTE · DESDE CERO EN INTELLIJ IDEA
**ISIL · Programación Orientada a Objetos · Java 21 + Maven + JSP + Apache Tomcat · 120 minutos**

> **Importante: en esta versión NO se parte de un proyecto ya creado.** Aprenderás qué opción elegir en IntelliJ, cómo configurar Maven, qué carpetas y archivos crear, dónde escribir cada bloque y cómo ejecutar primero en consola y luego en el navegador. El resultado será el mismo tanto en consola como en navegador.

## 1. Producto final y límites de la sesión

Crearás **un único proyecto** llamado `RetoSimetriaWeb` con un formulario que pide **código numérico** y **frase**; en el servidor Java se evalúan tres condiciones: capicúa, primo y palíndromo. El sitio devuelve un puntaje **0 a 3** y un nivel: AÚN SIN PUNTOS, INICIAL, AVANZADO o EXPERTO.

La clase aborda únicamente **dos temas**:

- **TEMA 1 · Java:** construir una clase que usa métodos, bucles, `Math.sqrt()` y operaciones sobre `String` (repaso integrado de POO).
- **TEMA 2 · JSP/Tomcat:** construir la entrada web y mostrar el resultado procesado por Java.

**Producto a entregar:** carpeta Maven completa con `pom.xml`, tres archivos `.java`, dos `.jsp` y un `.css`; prueba de consola y dos capturas del navegador.

```text
NAVEGADOR index.jsp (codigo=131, frase=somos)
           │  Enviar POST
           ▼
SERVIDOR resultado.jsp  -->  new ValidadorReto(131, "somos")
                                       │
                        capicúa=true · primo=true · palíndromo=true
                                       │
                             PUNTAJE 3/3 · EXPERTO
                                       │
           ◄──────────── HTML de respuesta ────────────────┘
```

## 2. Cronograma de 120 minutos (incluye crear el proyecto)

| Tiempo | Min. | Trabajo | Comprobación |
|---|---:|---|---|
| 00–08 | 8 | Problema, flujo de datos y predicción | Reconocer dos entradas y una salida |
| 08–30 | 22 | **Crear Maven desde cero**, paquetes y archivos Java base | Proyecto abre, compila y corre `AppPruebas` |
| 30–52 | 22 | EJ01 · `esCapicua()` y `esPalindromo()` | Dos validaciones correctas |
| 52–66 | 14 | EJ02 · `esPrimo()` usando `Math.sqrt()` | Primos y compuestos |
| 66–78 | 12 | EJ03 · `puntaje()` y `nivel()` | Cuatro niveles correctos |
| 78–92 | 14 | EJ04 · Crear `index.jsp` | Formulario y nombres de campos |
| 92–112 | 20 | EJ05 · Crear `resultado.jsp`, generar WAR y abrir Tomcat | Resultado en navegador |
| 112–118 | 6 | Probar cuatro combinaciones | Tabla de comprobación |
| 118–120 | 2 | Conclusión y entrega | Evidencias |
| **TOTAL** | **120** | **Un proyecto; dos temas** | |

> **Para lograrlo en dos horas:** IntelliJ IDEA, **JDK 21**, Maven integrado y Tomcat 10.1/11 deben estar instalados y configurados **antes de la clase**. La sesión enseña a **crear el proyecto**, pero no incluye instalar programas ni descargar dependencias con una red lenta. Los estudiantes pueden pegar los bloques de referencia para centrarse en comprenderlos.

---

## 3. CREACIÓN DEL PROYECTO DESDE CERO (min 08–30)

### PASO 0 · Revisar el entorno (antes de comenzar)

1. Abre **IntelliJ IDEA** en Windows; el curso trabaja con **JDK 21**.
2. Ve a **File → Project Structure → Project** (atajo `Ctrl+Alt+Shift+S`) y comprueba que el SDK disponible sea **21**; no es necesario cambiar todavía nada.
3. En la **terminal** del sistema, `java -version` debe indicar una versión 21. Que este comando no funcione no significa necesariamente que IntelliJ no tenga configurado el JDK; comprueba también el SDK del proyecto.
4. Confirma con el docente que **Apache Tomcat 10.1 o 11** ya existe y cuál es su carpeta (`TOMCAT_HOME`) y su puerto (usualmente `8080`). **No es obligatorio IntelliJ Ultimate**: con Community puedes empaquetar un WAR y desplegarlo manualmente en Tomcat.

### PASO 1 · Crear un proyecto Maven desde IntelliJ

**Haz exactamente lo siguiente:**

1. En IntelliJ selecciona **File → New → Project**.
2. En las versiones recientes, elige **Java** como lenguaje y **Maven** como *Build system*; algunas versiones muestran directamente una categoría **Maven**. Ambas rutas son válidas.
3. Escribe **Name: `RetoSimetriaWeb`**. Escoge una carpeta local donde tengas permisos; por ejemplo `Documentos/ISIL/`.
4. Selecciona el **JDK 21** y deja Maven con distribución **Bundled** o la distribución Maven que ya tengas configurada.
5. En **Advanced Settings**, si aparecen, utiliza **GroupId: `pe.edu.isil`** y **ArtifactId: `RetoSimetriaWeb`**. Si tu asistente no muestra esos campos, los definiremos directamente en `pom.xml`.
6. Haz clic en **Create**. Espera a que se complete la importación Maven. No elijas un proyecto Gradle.

**¿Por qué Maven?** Maven establece carpetas estándar y genera el archivo `.war` que Apache Tomcat puede desplegar. Un proyecto Java sin Maven suele producir un `.jar` y no crea directamente el empaquetado web requerido.

**Comprobación visual:** en el panel Project debes tener una carpeta `RetoSimetriaWeb` y un archivo llamado `pom.xml` en su raíz. Si no ves Project, utiliza `Alt+1`.

### PASO 2 · Configurar `pom.xml` para una aplicación WEB

**Ubicación:** archivo `pom.xml`, justo en la raíz del proyecto (NO dentro de `src`). Abre el archivo, **reemplaza su contenido completo** por el siguiente y guarda con `Ctrl+S`:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>pe.edu.isil</groupId>
  <artifactId>RetoSimetriaWeb</artifactId>
  <version>1.0-SNAPSHOT</version>
  <packaging>war</packaging>
  <properties>
    <maven.compiler.release>21</maven.compiler.release>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
  </properties>
  <build>
    <finalName>RetoSimetriaWeb</finalName>
    <plugins>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-compiler-plugin</artifactId>
        <version>3.13.0</version>
      </plugin>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-war-plugin</artifactId>
        <version>3.4.0</version>
        <configuration><failOnMissingWebXml>false</failOnMissingWebXml></configuration>
      </plugin>
    </plugins>
  </build>
</project>
```

**Qué significa cada parte importante:**

| Elemento | Motivo | Consecuencia |
|---|---|---|
| `groupId` | Identificar la organización académica | Maven clasifica el proyecto bajo `pe.edu.isil` |
| `artifactId` | Nombre lógico del módulo | Se identifica como `RetoSimetriaWeb` |
| `<packaging>war</packaging>` | Crear una aplicación web Java | Se genera un `.war`, NO un `.jar` |
| `<maven.compiler.release>21` | Compilar con lenguaje/API compatibles con JDK 21 | Permite usar la sintaxis `switch` que se utiliza en la guía |
| `maven-compiler-plugin` | Configuración del compilador | Compila las clases `.java` |
| `maven-war-plugin` y `failOnMissingWebXml` | Empaquetar sin exigir `web.xml` | Coloca archivos JSP y clases en el WAR |
| `<finalName>RetoSimetriaWeb` | Fijar nombre del WAR | Salida: `target/RetoSimetriaWeb.war` |

**Importante:** si IntelliJ muestra la barra «Load Maven Changes» o el ícono de recarga Maven, pulsa **Reload All Maven Projects**. El primer uso puede necesitar descargar plugins. No escribas código Java dentro de `pom.xml`.

### PASO 3 · Crear las carpetas correctas

En el panel **Project** cambia a la vista **Project** si la agrupación oculta carpetas. Si IntelliJ creó algunas automáticamente, **no las dupliques**. Crea solamente las que falten usando **clic derecho sobre la carpeta padre → New → Directory**:

```text
RetoSimetriaWeb/
├── pom.xml                        (lo creó Maven; lo editaste en PASO 2)
└── src/
    └── main/
        ├── java/                  (código Java del servidor)
        │   └── pe/
        │       └── edu/
        │           └── isil/
        │               └── retosimetria/
        │                   ├── ValidadorReto.java
        │                   ├── AppPruebas.java
        │                   └── HtmlSeguro.java
        └── webapp/                (archivos que atiende Tomcat)
            ├── index.jsp
            ├── resultado.jsp
            └── estilos.css
```

**Pasos exactos:**

1. Sobre `src/main/java`: clic derecho → **New → Package** → escribe `pe.edu.isil.retosimetria` → Enter. IntelliJ creará la jerarquía de carpetas del paquete; **no crees una carpeta con puntos en el nombre**.
2. Si `src/main/java` no existe: crea `src/main/java` mediante **New → Directory**, después crea el paquete; si no reconoce los paquetes, clic derecho en `java` → **Mark Directory as → Sources Root**.
3. Sobre el paquete `pe.edu.isil.retosimetria`: clic derecho → **New → Java Class** → `ValidadorReto`. Repite con `AppPruebas` y `HtmlSeguro`.
4. Sobre `src/main`: clic derecho → **New → Directory** → `webapp`. Si ya existe, úsala.
5. Sobre `webapp`: clic derecho → **New → File** → crea **`index.jsp`**, **`resultado.jsp`** y **`estilos.css`**, uno por uno. **No utilices `New → Java Class` para los JSP**. Déjalos vacíos hasta EJ04/EJ05; en PASO 7 agregarás CSS.

**¿Por qué separar?** `src/main/java` contiene el algoritmo (lógica de negocio); `src/main/webapp` contiene la interfaz visible. Maven empaquetará ambas partes en la misma aplicación.

### PASO 4 · Crear `ValidadorReto.java`: atributos, constructor y métodos pendientes

**Ruta exacta:** `src/main/java/pe/edu/isil/retosimetria/ValidadorReto.java`.

Sustituye cualquier plantilla generada por IntelliJ por este código base **completo**. Debe existir antes de añadir los algoritmos; los métodos que por ahora devuelven `false`, `0` o `PENDIENTE` son **marcadores provisionales**, no la solución final.

```java
package pe.edu.isil.retosimetria;

import java.util.Locale;

public class ValidadorReto {
    private final int codigo;
    private final String frase;

    public ValidadorReto(int codigo, String frase) {
        if (codigo < 0 || codigo > 999999) {
            throw new IllegalArgumentException("El código debe estar entre 0 y 999999.");
        }
        if (frase == null || frase.isBlank() || frase.length() > 80) {
            throw new IllegalArgumentException("La frase debe contener entre 1 y 80 caracteres útiles.");
        }
        this.codigo = codigo;
        this.frase = frase;
    }

    public int getCodigo() { return codigo; }
    public String getFrase() { return frase; }

    // EJ01: recuperar validaciones conocidas
    public boolean esCapicua() { return false; }
    public boolean esPalindromo() { return false; }
    // EJ02: comprobación adicional
    public boolean esPrimo() { return false; }
    // EJ03: resultado integrado
    public int puntaje() { return 0; }
    public String nivel() { return "PENDIENTE"; }
}
```

**Explicación, antes de continuar:**

- `package ...;` indica el nombre del paquete. La primera línea debe coincidir en **las tres clases**.
- `private final int codigo` y `private final String frase` guardan los datos del reto **sin permitir modificarlos después de construir el objeto**.
- `ValidadorReto(int codigo, String frase)` es un **constructor**: se ejecuta al escribir `new ValidadorReto(...)`. Verifica que el código sea entero entre `0` y `999999` y que la frase no sea vacía y tenga como máximo 80 caracteres.
- `this.codigo = codigo` diferencia el **atributo del objeto** del **parámetro recibido**.
- `getCodigo()` y `getFrase()` permiten consultar los atributos desde la JSP sin exponerlos directamente.
- `import java.util.Locale;` será utilizado en EJ01 cuando se convierta el texto a minúsculas.
- Los métodos públicos existen como **contrato de trabajo**: los sustituirás en EJ01, EJ02 y EJ03, sin crear clases adicionales.

**Comprueba:** revisa que **no hayas dejado dos líneas `package`** ni dos clases `ValidadorReto` en el mismo archivo. Debe haber una sola clase pública con ese nombre.

### PASO 5 · Crear `AppPruebas.java`: primer botón «Run»

**Ruta exacta:** `src/main/java/pe/edu/isil/retosimetria/AppPruebas.java`. Reemplaza su contenido por:

```java
package pe.edu.isil.retosimetria;

/** Ejecución sin Tomcat: permite comprobar primero la lógica del reto. */
public class AppPruebas {
    public static void main(String[] args) {
        mostrar(1221, "Anita lava la tina"); // 2 puntos: no es primo
        mostrar(131, "somos");             // 3 puntos
        mostrar(37, "Java");               // 1 punto
        mostrar(120, "Java");              // 0 puntos
    }

    private static void mostrar(int codigo, String frase) {
        ValidadorReto reto = new ValidadorReto(codigo, frase);
        System.out.printf("%d / %s | capicúa=%s, primo=%s, palíndromo=%s | %d/3 %s%n",
                codigo, frase, reto.esCapicua(), reto.esPrimo(),
                reto.esPalindromo(), reto.puntaje(), reto.nivel());
    }
}
```

**¿Por qué crear este archivo?** Todavía NO tenemos un servidor web funcionando. `main()` permite **ejecutar y depurar la lógica en consola antes de añadir JSP**. `mostrar()` recibe entradas, crea un objeto y muestra sus métodos mediante `System.out.printf`.

**Ejecución inicial en IntelliJ:** clic en el **triángulo verde al costado de `main`** → **Run 'AppPruebas.main()'**. La salida de esta primera ejecución **aún será incorrecta a propósito**: las validaciones imprimirán `false` y el nivel `PENDIENTE`. Esto confirma que la estructura inicial **compila**, no que el ejercicio esté terminado.

**Si NO aparece el triángulo verde:** comprueba que el JDK del proyecto sea 21, que el archivo esté bajo `src/main/java` y que contenga `public static void main(String[] args)`.

### PASO 6 · Crear `HtmlSeguro.java`: utilidad para el texto de la web

**Ruta:** `src/main/java/pe/edu/isil/retosimetria/HtmlSeguro.java`. Pega el siguiente código completo; es una utilidad proporcionada para no distraernos del foco de las dos unidades.

```java
package pe.edu.isil.retosimetria;

/** Utilidad lista para usar. Evita que el texto ingresado se interprete como HTML. */
public final class HtmlSeguro {
    private HtmlSeguro() { }

    public static String escapar(String valor) {
        if (valor == null) return "";
        return valor.replace("&", "&amp;")
                    .replace("<", "&lt;")
                    .replace(">", "&gt;")
                    .replace("\"", "&quot;")
                    .replace("'", "&#39;");
    }
}
```

**¿Para qué sirve?** Si el visitante escribe caracteres como `<` o `&`, no deben interpretarse como etiquetas HTML al mostrar una frase. `escapar()` devuelve una versión segura para el texto visible. **Esta clase no decide capicúas, primos ni palíndromos.**

### PASO 7 · Crear `estilos.css` (diseño entregado; no es tema nuevo)

**Ruta:** `src/main/webapp/estilos.css`. Puedes copiar este CSS sin analizarlo línea por línea; el objetivo del curso es la lógica Java y el flujo JSP.

```css
*{box-sizing:border-box}body{margin:0;background:#f1f5fb;color:#17243b;font-family:system-ui,-apple-system,Segoe UI,Arial,sans-serif}
main{max-width:720px;margin:48px auto;padding:0 16px}.card{background:white;border-radius:18px;padding:28px;box-shadow:0 8px 34px #182d4e17}
h1{font-size:30px;margin:4px 0 8px}.lead{color:#465774;line-height:1.55;margin-bottom:24px}
label{display:block;font-weight:700;margin:18px 0 7px}input{width:100%;padding:13px 14px;border:1px solid #c0ccdb;border-radius:10px;font-size:16px}
button,.button{display:inline-block;border:0;border-radius:10px;padding:12px 20px;background:#1765c1;color:white;font-size:16px;text-decoration:none;margin-top:22px;font-weight:700;cursor:pointer}
.badge{display:inline-block;border-radius:50px;background:#dff1fe;color:#124d91;padding:7px 12px;font-weight:700}
.grid{display:grid;grid-template-columns:repeat(3,1fr);gap:10px;margin:19px 0}.item{border:1px solid #dae3f0;border-radius:12px;padding:12px;text-align:center}
.item strong{display:block;font-size:14px;margin-bottom:5px}.yes{color:#137b54}.no{color:#a03247}.score{font-size:28px;font-weight:800;color:#174c8a}
.alert{border-left:4px solid #c04958;background:#fff2f4;padding:13px;border-radius:7px}
@media(max-width:600px){.grid{grid-template-columns:1fr}h1{font-size:24px}.card{padding:20px}}
```

**Punto de control de los primeros 22 minutos:** en IntelliJ deben verse **1 `pom.xml`, 3 `.java`, 2 `.jsp` vacíos y 1 `.css`**. `AppPruebas` debe ejecutar sin errores de compilación. Los dos JSP se completarán en EJ04 y EJ05.

**Si trabajas más despacio:** el docente puede facilitar `FASE_15/Proyecto_Base_Vacio` (solo `pom.xml` de referencia) o mostrar la solución; esto no modifica el orden de trabajo de esta guía.

---

# TEMA 1 — LÓGICA JAVA (`Math`, `String` y POO)

## EJ01 · Construimos las dos validaciones conocidas (min 30–52)

### A. Problema y razón del componente

El formulario nos enviará un número y una frase, pero necesitamos una clase que pueda analizar ambos valores. `ValidadorReto` representa **una inscripción al reto**, guarda sus dos atributos y reúne las operaciones para evaluar ese objeto. La creaste en el paso 3.4; conserva su constructor y completa los métodos pendientes.

**¿Qué hace el constructor?** `new ValidadorReto(1221, "Anita lava la tina")` guarda ambos parámetros como `codigo` y `frase`. Los atributos se declaran `final` porque no vamos a modificar esos datos después de crear el objeto. El constructor que escribiste valida que el código esté entre 0 y 999999 y que la frase no sea vacía ni exceda 80 caracteres.

### B. Completar `esCapicua()`

Abre `ValidadorReto.java`. **Sustituye el método** `public boolean esCapicua() { return false; }` por este bloque completo, dentro de la misma clase:

```java
public boolean esCapicua() {
    int restante = codigo;
    int invertido = 0;
    do {
        int digito = restante % 10;
        invertido = invertido * 10 + digito;
        restante = restante / 10;
    } while (restante > 0);
    return codigo == invertido;
}
```

**Por qué y cómo funciona:** `restante` conserva las cifras pendientes; `% 10` extrae la última; `invertido * 10 + digito` construye la cifra invertida; `/ 10` elimina la cifra ya usada. `do-while` se ejecuta incluso con el número 0. **No modifica `codigo`**: modifica variables locales. `return` compara los valores al finalizar.

| Vuelta (`codigo=1221`) | `restante` antes | `digito` | `invertido` después | `restante` después |
|---:|---:|---:|---:|---:|
| 1 | 1221 | 1 | 1 | 122 |
| 2 | 122 | 2 | 12 | 12 |
| 3 | 12 | 2 | 122 | 1 |
| 4 | 1 | 1 | 1221 | 0 |

**Predice:** ¿el número `120` devolverá `true` o `false`? ¿Por qué?

### C. Completar `esPalindromo()`

En el mismo archivo sustituye el método pendiente `esPalindromo()` por:

```java
public boolean esPalindromo() {
    String limpio = frase.toLowerCase(Locale.ROOT).replace(" ", "");
    for (int i = 0; i < limpio.length() / 2; i++) {
        if (limpio.charAt(i) != limpio.charAt(limpio.length() - 1 - i)) {
            return false;
        }
    }
    return !limpio.isEmpty();
}
```

**¿Por qué?** `toLowerCase(Locale.ROOT)` permite comparar sin distinguir mayúsculas; `replace(" ", "")` retira **espacios normales**; `length()` indica el número de caracteres; `charAt(i)` y `charAt(length-1-i)` comparan ambos extremos. Si hay una diferencia, retornamos `false` antes de finalizar. Si ninguna pareja difiere, `true`. El alcance de la actividad **no elimina tildes, tabulaciones ni signos de puntuación**.

**Traza pequeña para `somos`:** `s` con `s` (iguales), `o` con `o` (iguales); el carácter central `m` no necesita compararse consigo mismo.

### D. Ejecución, error y tarea espejo

Ejecuta `AppPruebas.main()` otra vez. Como aún faltan EJ02 y EJ03, **solo** comprueba los primeros dos indicadores en pantalla, que ahora deben devolver `true` para `1221 / Anita lava la tina`.

**Error frecuente:** cambiar `restante` por `codigo` dentro del bucle altera el valor que necesitamos comparar; olvidar `restante = restante / 10` ocasionaría un bucle que no avanza.

**T01:** cambia temporalmente el caso de prueba a `120 / Anita lava la tina`. Sin ejecutar, escribe qué devolverán `esCapicua()` y `esPalindromo()`. Después comprueba. **Aceptación:** explicar en una oración la diferencia entre el número original y el invertido.

---

## EJ02 · NUEVO EJERCICIO: ¿el código es un número primo? (min 52–66)

### A. Problema

Hasta ahora solo comprobamos simetría. Vamos a añadir una característica matemática **distinta**: determinar si el código es **primo**, es decir, si es mayor que 1 y tiene exactamente dos divisores positivos: 1 y él mismo. `131` es primo; `1221` no lo es porque es divisible por 3.

### B. ¿Por qué utilizamos `Math.sqrt()`?

Para comprobar si un número tiene divisores no necesitamos revisar todos los números hasta él mismo. Si tiene un divisor no trivial, al menos uno de sus divisores es **menor o igual que su raíz cuadrada**. Por eso `Math.sqrt(codigo)` reduce las comprobaciones.

**Ejemplo:** `Math.sqrt(131) ≈ 11.45`. Solo buscaremos posibles divisores del 2 al 11. Usaremos `for` (iteración conocida) y `%` (resto de división).

### C. Código a incorporar

En `ValidadorReto.java`, sustituye **solo** el método `esPrimo()` pendiente por:

```java
public boolean esPrimo() {
    if (codigo < 2) return false;
    int limite = (int) Math.sqrt(codigo);
    for (int divisor = 2; divisor <= limite; divisor++) {
        if (codigo % divisor == 0) return false;
    }
    return true;
}
```

| Instrucción | Necesidad | Efecto |
|---|---|---|
| `if (codigo < 2) return false;` | Excluir 0 y 1, que no son primos | Termina el método inmediatamente |
| `Math.sqrt(codigo)` | Hallar el límite suficiente de búsqueda | Entrega `double`; el molde `(int)` trunca |
| `for (int divisor = 2; ...)` | Probar solo los divisores relevantes | Incrementa `divisor` de 2 hasta el límite |
| `codigo % divisor == 0` | Detectar división exacta | Si se cumple, ya sabemos que **no** es primo |
| `return true` | No se encontró divisor | Confirma que el número (≥2) es primo |

**Predice antes de ejecutar:** ¿qué devuelve para `2`, `9`, `29` y `131`? En particular, explica por qué el bucle para 2 no necesita ejecutarse.

### D. Comprobación y error controlado

Ejecuta `AppPruebas`. Espera `esPrimo() = true` para `131` y `37`, y `false` para `1221` y `120`.

**Error frecuente:** comenzar el bucle con `divisor = 1` (todos los números son divisibles por 1, por lo que todos resultarían «no primos»). **Corrección:** comenzar desde 2. Otro error: omitir el caso `codigo < 2` hace que el método considere primos a 0 y 1.

**T02:** escribe en tu cuaderno por qué `29` es primo y `30` no. Luego cambia en `AppPruebas` el número de una de las pruebas. **Aceptación:** el programa y tu razonamiento coinciden.

---

## EJ03 · NUEVO EJERCICIO: calcular un puntaje útil (min 66–78)

### A. Problema y decisión de diseño

Tres resultados `true/false` pueden ser difíciles de interpretar juntos. Necesitamos un **puntaje de 0 a 3** y un **nivel** que resuma el resultado:

| Puntaje | Nivel | Significado |
|---:|---|---|
| 0 | AÚN SIN PUNTOS | No se cumplió ningún criterio |
| 1 | INICIAL | Se cumplió uno |
| 2 | AVANZADO | Se cumplieron dos |
| 3 | EXPERTO | Se cumplieron los tres |

Crear un método `puntaje()` evita repetir las tres validaciones en cada JSP. Crear `nivel()` mantiene la regla de presentación en la clase Java.

### B. Código del puntaje

Sustituye el método pendiente `puntaje()` por:

```java
public int puntaje() {
    int puntos = 0;
    if (esCapicua()) puntos++;
    if (esPrimo()) puntos++;
    if (esPalindromo()) puntos++;
    return puntos;
}
```

`puntos` empieza en 0; cada `if` ejecuta `puntos++` solo cuando una condición se cumple; `return puntos` devuelve la suma, **sin cambiar el número ni la frase originales**.

Sustituye también el método pendiente `nivel()` por:

```java
public String nivel() {
    return switch (puntaje()) {
        case 3 -> "EXPERTO";
        case 2 -> "AVANZADO";
        case 1 -> "INICIAL";
        default -> "AÚN SIN PUNTOS";
    };
}
```

**¿Qué significa `switch (puntaje())`?** Usa el valor obtenido (0, 1, 2 o 3) para escoger un texto. La expresión `switch` con `->` está disponible en Java 21. `default` sirve para el caso 0 en esta rúbrica.

### C. Comprueba las cuatro salidas de la consola

Ejecuta `AppPruebas`: `131 / somos` debe terminar en **3/3 EXPERTO**; `1221 / Anita lava la tina`, **2/3 AVANZADO**; `37 / Java`, **1/3 INICIAL**; `120 / Java`, **0/3 AÚN SIN PUNTOS**.

**Error frecuente:** escribir `if (esPrimo)` en vez de `if (esPrimo())`: un método se ejecuta con paréntesis. Otro error: sumar dos veces el mismo criterio altera el máximo 3.

**T03:** explica cuál es el único criterio verdadero cuando la entrada es `37 / Java`. **Aceptación:** justificar el resultado 1/3 sin cambiar el código de la rúbrica.

---

# TEMA 2 — FRONTEND JSP Y PROCESAMIENTO CON TOMCAT

## EJ04 · Crear el formulario web `index.jsp` (min 78–92)

### A. ¿Por qué necesitamos un formulario?

Hasta este momento, los valores se escribían en `AppPruebas.java`. Un usuario normal no debe editar código fuente para participar. Construiremos una **vista HTML/JSP** que permita escribir número y frase en el navegador y enviarlos al servidor.

### B. Dónde escribir y qué reemplazar

Abre `src/main/webapp/index.jsp`. Como lo creaste vacío en el paso 3.7, escribe el siguiente contenido completo en ese archivo. **No escribas esta página en `ValidadorReto.java`**.

```jsp
<%@ page contentType="text/html; charset=UTF-8" pageEncoding="UTF-8" %>
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>Reto Simetría Web | Registro</title>
  <link rel="stylesheet" href="estilos.css">
</head>
<body>
  <main><section class="card">
    <span class="badge">ISIL · Repaso POO · Sesión 08</span>
    <h1>Reto Simetría Web</h1>
    <p class="lead">Ingresa un código y una frase. Java evaluará si el código
       es capicúa y primo, y si la frase es palíndroma.</p>
    <form action="resultado.jsp" method="post" accept-charset="UTF-8">
      <label for="codigo">Código numérico (0 a 999999)</label>
      <input id="codigo" name="codigo" type="number" min="0" max="999999"
             step="1" value="131" required>
      <label for="frase">Frase (máximo 80 caracteres)</label>
      <input id="frase" name="frase" type="text" maxlength="80"
             value="somos" required>
      <button type="submit">Evaluar reto</button>
    </form>
  </section></main>
</body>
</html>
```

### C. Explica el envío de los datos (la parte esencial)

| Fragmento | ¿Qué hace? | ¿Qué pasaría si cambia? |
|---|---|---|
| `<form action="resultado.jsp" ...>` | Define a qué página van los datos | Un destino mal escrito causaría una ruta inexistente |
| `method="post"` | Envía datos en el cuerpo de la solicitud | No aparecen como parámetros de la URL como en GET |
| `name="codigo"` | Identifica el valor que leerá `getParameter("codigo")` | Si no coinciden, el servidor recibe `null` |
| `name="frase"` | Identifica el texto del formulario | El servidor usa el mismo nombre exacto |
| `min`, `max`, `required` | Ayudan al usuario a ingresar datos correctos | **No reemplazan** la validación en el servidor |
| `link rel="stylesheet"` | Usa `estilos.css`, que creaste en el PASO 7 | Cambia el diseño, pero no la lógica del algoritmo |

**Predicción:** cuando hagas clic en «Evaluar reto» con 131 y «somos», ¿a qué archivo llegará la solicitud? ¿Cuáles son los nombres de sus dos parámetros?

**T04:** modifica **solo** los valores iniciales `value` del formulario: `1221` y `Anita lava la tina`. **Aceptación:** comprobar que siguen existiendo `name="codigo"` y `name="frase"`, y que el formulario sigue apuntando a `resultado.jsp`.

---

## EJ05 · Procesar la información y ver el resultado en JSP (min 92–112)

### A. Problema: ya tenemos entrada, falta respuesta

El navegador envía cadenas de texto, incluso cuando el campo visual es numérico. `resultado.jsp` debe obtener las cadenas con `request.getParameter()`, transformar `codigo` a `int`, crear un `ValidadorReto` y consultar sus cinco métodos. Si llegan datos inválidos, debemos mostrar un mensaje en lugar de un error sin explicar.

### B. Reemplaza `resultado.jsp` por la solución gradual completa

En `src/main/webapp/resultado.jsp`, escribe el siguiente código en el archivo que creaste vacío. Observa que los `import` coinciden con el paquete real `pe.edu.isil.retosimetria`. **No crees otro método de evaluación dentro del JSP**: solamente llamaremos a los que ya desarrollaste.

```jsp
<%@ page contentType="text/html; charset=UTF-8" pageEncoding="UTF-8" %>
<%@ page import="pe.edu.isil.retosimetria.ValidadorReto" %>
<%@ page import="pe.edu.isil.retosimetria.HtmlSeguro" %>
<%
    request.setCharacterEncoding("UTF-8");
    String error = null;
    ValidadorReto reto = null;
    if (!"POST".equalsIgnoreCase(request.getMethod())) {
        error = "Debes enviar el formulario.";
    } else {
        String codigoTexto = request.getParameter("codigo");
        String fraseTexto = request.getParameter("frase");
        if (codigoTexto == null || fraseTexto == null) {
            error = "Faltan campos en la solicitud.";
        } else {
            try {
                int codigo = Integer.parseInt(codigoTexto.trim());
                reto = new ValidadorReto(codigo, fraseTexto);
            } catch (NumberFormatException ex) {
                error = "El código debe ser un número entero válido.";
            } catch (IllegalArgumentException ex) {
                error = ex.getMessage();
            }
        }
    }
%>
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>Reto Simetría Web | Resultado</title>
  <link rel="stylesheet" href="estilos.css">
</head>
<body><main><section class="card">
  <span class="badge">Resultado del reto</span>
  <% if (error != null) { %>
    <h1>Revisa los datos</h1>
    <p class="alert"><%= HtmlSeguro.escapar(error) %></p>
  <% } else { %>
    <h1>Evaluación completada</h1>
    <p><strong>Código:</strong> <%= reto.getCodigo() %></p>
    <p><strong>Frase:</strong> <%= HtmlSeguro.escapar(reto.getFrase()) %></p>
    <div class="grid">
      <div class="item"><strong>Capicúa</strong><span><%= reto.esCapicua() %></span></div>
      <div class="item"><strong>Primo</strong><span><%= reto.esPrimo() %></span></div>
      <div class="item"><strong>Palíndromo</strong><span><%= reto.esPalindromo() %></span></div>
    </div>
    <p class="score">Puntaje: <%= reto.puntaje() %> / 3</p>
    <p><strong>Nivel:</strong> <%= HtmlSeguro.escapar(reto.nivel()) %></p>
  <% } %>
  <a class="button" href="index.jsp">Intentar otro reto</a>
</section></main></body>
</html>
```

### C. Qué significa cada grupo de instrucciones

| Bloque | Propósito | Qué produce |
|---|---|---|
| `<%@ page ... %>` | Configurar JSP e importar clases Java | Acceso a `ValidadorReto` y `HtmlSeguro` |
| `<% ... %>` | Ejecutar código Java en el servidor | Variables `error` y `reto` |
| `request.setCharacterEncoding("UTF-8")` | Interpretar los datos enviados en UTF-8 | Conserva correctamente las tildes |
| `request.getParameter("codigo")` | Obtener el contenido del campo con ese `name` | Primero llega como `String` |
| `Integer.parseInt(...)` | Convertir código a entero | Permite operaciones matemáticas |
| `new ValidadorReto(...)` | Crear un objeto con las entradas | Activa validaciones de constructor |
| `catch (...)` | Controlar dato inválido | Mensaje comprensible, sin fallar la página |
| `<%= reto.puntaje() %>` | Insertar en HTML el resultado calculado en Java | Muestra un número de 0 a 3 |
| `HtmlSeguro.escapar(...)` | Impedir que caracteres del usuario se interpreten como etiquetas HTML | Muestra texto de forma segura |

**Atención a la seguridad:** `HtmlSeguro.java` se entrega implementada y no debes modificarla. La usamos cuando imprimimos una frase proporcionada por el usuario; **no** escribas `<%= reto.getFrase() %>` sin escapar el texto.

### D. Compilar y desplegar (al final del bloque)

1. En IntelliJ, abre la pestaña **Maven** y ejecuta el objetivo **`package`**. Maven genera `target/RetoSimetriaWeb.war`. También puedes ejecutar `mvn package` si tienes Maven en la terminal.
2. Copia el `.war` generado a `TOMCAT_HOME/webapps/`. Si Apache Tomcat ya estaba iniciado, el despliegue automático depende de su configuración; si no aparece la aplicación, reinicia Tomcat.
3. En Windows, inicia Apache Tomcat desde su carpeta `bin` con `startup.bat` (si el servidor aún no estaba iniciado).
4. Abre el navegador en **`http://localhost:8080/RetoSimetriaWeb/index.jsp`**. El puerto 8080 es el predeterminado y podría ser otro según la instalación.
5. Ingresa `131` y `somos`. Debes obtener **Capicúa=true · Primo=true · Palíndromo=true · Puntaje=3/3 · EXPERTO**.

**Alternativa cuando Maven no está listo:** el docente puede copiar el `RetoSimetriaWeb.war` de referencia incluido en `FASE_15` y mostrar el resultado final. Esto no sustituye la construcción del proyecto por el estudiante, pero permite observar el flujo completo del formulario.

### E. Errores frecuentes que debes distinguir

- **HTTP 404:** revisa que `RetoSimetriaWeb.war` esté desplegado con ese nombre, el puerto y la ruta `index.jsp`.
- **`cannot find symbol ValidadorReto`:** revisa paquete/import, y que Maven genere las clases en `WEB-INF/classes`.
- **`null` al recibir parámetros:** revisa que `name="codigo"` y `name="frase"` coincidan exactamente con `getParameter(...)`.
- **Código no numérico:** el servidor debe mostrar «El código debe ser un número entero válido», sin una página de error.
- **Puntaje siempre 0:** revisa que realmente reemplazaste los métodos provisionales (`false`/`0`/`PENDIENTE`) de `ValidadorReto`.

**T05:** registra los resultados obtenidos en el navegador para `131 / somos`, `1221 / Anita lava la tina`, `37 / Java` y `120 / Java`. Prueba que una solicitud sin campos no provoque una excepción visible. **Aceptación:** presentar una captura del formulario y otra de uno de los resultados.

---

## 4. Comprobación final (min 112–118)

Sin modificar la solución, verifica:

| Código | Frase | Capicúa | Primo | Palíndromo | Puntaje | Nivel |
|---:|---|---|---|---|---:|---|
| 131 | somos | true | true | true | 3/3 | EXPERTO |
| 1221 | Anita lava la tina | true | false | true | 2/3 | AVANZADO |
| 37 | Java | false | true | false | 1/3 | INICIAL |
| 120 | Java | false | false | false | 0/3 | AÚN SIN PUNTOS |

**Salida rápida (responde en 6 minutos):**

1. ¿Por qué `codigo % divisor == 0` demuestra que un número no es primo cuando `divisor` está entre 2 y su raíz cuadrada?
2. ¿Para qué utilizamos `Math.sqrt(codigo)`?
3. ¿Qué diferencia existe entre `<% ... %>` y `<%= ... %>` en JSP?
4. ¿Qué nombre del formulario debe coincidir con `request.getParameter("frase")`?
5. ¿Por qué el JSP debe llamar a `reto.puntaje()` en vez de repetir las tres validaciones?

## 5. Cierre académico (min 118–120)

Completa: «Antes ingresaba los datos en la clase `AppPruebas`. Ahora los ingreso en __________; Tomcat los recibe en __________; y la clase __________ determina el resultado». Entrega el proyecto, las dos capturas y una explicación breve de `esPrimo()`.

