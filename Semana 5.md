---
course_id: ISIL-POO-JAVA
session_id: S05
module_id: TEMA-05
course_version: 2026
source_origin: PPT
status: draft
---

# Guía del Estudiante - Sesión 05
## Conociendo JSP (Java Server Pages) + Apache Tomcat

> Curso: Programación Orientada a Objetos  
> Sesión: Tema 05  
> Modalidad sugerida: clase-laboratorio guiada  
> Sistema operativo principal del procedimiento: Windows  
> Resultado final: una aplicación web Java que solicita un nombre en `index.jsp` y responde con un saludo personalizado desde `saludo.jsp`.

---

# 1. Propósito de la sesión

En esta sesión vas a pasar de ejecutar Java como una aplicación local a comprender un flujo web básico en el que intervienen un navegador, Apache Tomcat y páginas JSP. El objetivo no es estudiar todavía una arquitectura web avanzada, sino construir un primer recorrido completo y observable: comprobar que Java está disponible, iniciar Tomcat, crear un proyecto web, construir una página de entrada, enviar un dato y mostrar una respuesta dinámica.

Trabajarás con cuatro piezas visibles: **Java/JDK**, **Apache Tomcat**, **IntelliJ IDEA** y **el navegador**. Cada una cumple una responsabilidad diferente. El JDK permite ejecutar Java; Tomcat aloja y procesa la aplicación web; IntelliJ IDEA facilita crear y editar el proyecto; el navegador realiza la solicitud y muestra el HTML resultante.

La evidencia final será concreta: al escribir un nombre en un formulario y pulsar **Saludar**, el navegador deberá mostrar un mensaje como `Hola, Ana! Bienvenido a tu primera app JSP.`. Además, deberás poder explicar qué dato viajó, qué archivo lo recibió y por qué el usuario ve HTML en lugar del código Java que se ejecuta en el servidor.

---

# 2. Resultado observable

## A. Lectura sugerida del docente

Al finalizar esta práctica no bastará con que la página "funcione". Debes poder reconstruir mentalmente el recorrido completo. Primero validarás que Java esté instalado porque Tomcat depende de una JVM disponible. Después iniciarás Tomcat y comprobarás que escucha en `http://localhost:8080`. Luego crearás una aplicación web en IntelliJ IDEA. IntelliJ se utilizará para editar y empaquetar; Apache Tomcat se ejecutará como un proceso externo de Windows. En la ruta base de esta clase no usarás el botón Run del IDE para arrancar Tomcat. Dentro del proyecto construirás `index.jsp`, que contiene el formulario de entrada, y `saludo.jsp`, que recupera el parámetro enviado y genera un saludo. Finalmente ejecutarás tres pruebas: un nombre válido, un intento de envío vacío desde el formulario y el acceso directo a `saludo.jsp` sin parámetro. Con esas pruebas podrás diferenciar qué validación ocurre en el navegador y qué validación ocurre en la propia página JSP. La meta es que puedas describir el flujo **navegador -> JSP -> Tomcat -> procesamiento Java -> HTML -> navegador** sin memorizarlo como una lista, sino relacionándolo con lo que observaste al ejecutar.

## B. Desempeños observables

Al terminar deberás poder:

1. validar si existe un JDK utilizable mediante `java -version`;
2. iniciar y detener Apache Tomcat desde Windows;
3. comprobar el estado del servidor desde `localhost:8080`;
4. crear un proyecto web Java con Maven en IntelliJ IDEA y asociarlo a Tomcat;
5. construir `index.jsp` con un formulario que envía el parámetro `nombre`;
6. construir `saludo.jsp` y recuperar el dato con `request.getParameter("nombre")`;
7. diagnosticar un error de parámetro o ruta sin cambiar de tecnología;
8. ejecutar e interpretar el flujo completo de la aplicación.

## C. Criterio de dominio

Dominas la sesión si puedes reconstruir el proyecto desde cero, justificar por qué existe cada archivo y explicar por qué `name="nombre"` en el formulario debe coincidir con `request.getParameter("nombre")` en la página de respuesta. También debes poder distinguir un problema de servidor no iniciado, un problema de ruta y un problema de parámetro.

---

# 3. Antes de iniciar

## Debe saber

- reconocer una variable `String` en Java;
- interpretar una condición `if`;
- reconocer etiquetas HTML básicas como `<html>`, `<head>`, `<body>`, `<h2>`, `<form>` e `<input>`;
- ejecutar una aplicación o comando y observar su salida.

No necesitas experiencia previa con JSP ni con configuración de Tomcat.

## Debe tener disponible

Para una práctica actual y estable se recomienda:

- **JDK 25 LTS** como JDK de trabajo;
- **Apache Tomcat 11.0.26**;
- **IntelliJ IDEA 2026.2.x**;
- navegador web moderno;
- Windows con permisos para ejecutar programas locales;
- conexión a Internet solo para descargar software si todavía no está instalado.

> Si tu institución ya fijó versiones concretas, utiliza las versiones institucionales siempre que sean compatibles con Tomcat 11.

## No se asumirá todavía

Esta sesión no requiere:

- Spring Boot;
- JSTL;
- Expression Language avanzada;
- MVC;
- base de datos;
- creación manual de servlets Java;
- despliegue en nube;
- autenticación;
- APIs REST.

---

# 4. Herramientas y recursos

## 4.1 JDK

**Qué es:** el kit de desarrollo de Java.  
**Para qué se usa aquí:** Apache Tomcat necesita una JVM compatible para iniciar y compilar las páginas JSP cuando corresponda.  
**Recomendación del curso:** conservar el JDK ya utilizado desde las primeras sesiones si es compatible. Para un equipo nuevo, esta guía toma **JDK 25 LTS** como referencia estable.  
**Validación:**

```bat
java -version
```

Tomcat 11 requiere Java 17 o posterior. No es necesario instalar un JRE separado si ya existe un JDK funcional.

## 4.2 Apache Tomcat

**Qué es:** servidor web y contenedor de servlets/JSP.  
**Para qué se usa aquí:** ejecutar la aplicación web y procesar `index.jsp` y `saludo.jsp` como servidor externo a IntelliJ IDEA.  
**Rama usada:** Tomcat 11.  
**Versión de referencia al reconstruir esta guía:** 11.0.26.  
**Sitio oficial:** `https://tomcat.apache.org/`  
**Descarga Windows:** Tomcat 11 > Binary Distributions > Core > zip.  
**Validación:** abrir `http://localhost:8080` después de iniciar el servidor.

## 4.3 IntelliJ IDEA

**Decisión de continuidad del curso:** se mantiene **IntelliJ IDEA**, porque es el IDE que se viene utilizando desde las primeras sesiones. La PPT presenta NetBeans como herramienta operativa, pero el objetivo académico real es construir y ejecutar una aplicación JSP sobre Tomcat; cambiar de IDE no modifica JSP, Tomcat, el formulario ni el flujo HTTP.

A partir de IntelliJ IDEA 2025.3 existe un único instalador del producto. Las funciones básicas Java/Kotlin son gratuitas; las funciones empresariales avanzadas, entre ellas la integración completa con servidores Jakarta EE/Tomcat, requieren que las funciones **Ultimate** estén activas.

### ¿Es obligatorio instalar un plugin?

**No para la ruta base de esta clase.** Todos los estudiantes pueden trabajar con:

```text
IntelliJ IDEA
+ Maven
+ estructura src/main/webapp
+ Apache Tomcat externo
```

En esta ruta IntelliJ se usa para crear/editar el proyecto y Maven empaqueta el WAR. Tomcat se inicia externamente y se despliega el WAR en `webapps`. Es la ruta recomendada como **base institucional**, porque no obliga a que todos los estudiantes tengan una suscripción Ultimate.

### Integración opcional si tienes funciones Ultimate activas

Si tu instalación tiene acceso a las funciones Ultimate, puedes integrar Tomcat directamente dentro del IDE. Revisa en `File > Settings > Plugins` que estén disponibles y habilitados:

1. **Jakarta EE Platform**.
2. **Jakarta EE: Application Servers**.
3. **Jakarta EE: Web/Servlets**.
4. **Tomcat and TomEE**.
5. **Jakarta EE: Server Pages (JSP)** para soporte específico de JSP; si no está instalado, búscalo en `Marketplace`, pulsa **Install** y reinicia el IDE si lo solicita.

> No se requiere instalar un plugin de terceros como condición de la clase. La integración oficial de Tomcat se utiliza solo cuando las funciones Ultimate están disponibles.

## 4.4 Maven

El proyecto será Maven porque la sesión original trabaja una Web Application con Maven y este formato es portable entre IDEs.

**No necesitas instalar Maven por separado** si vas a compilar desde la ventana Maven de IntelliJ IDEA. El IDE puede utilizar su Maven integrado. Si deseas usar la terminal con `mvn`, entonces sí debes tener Maven disponible en el sistema.

Validación opcional en terminal:

```bat
mvn -version
```

## 4.5 Navegador

Se utiliza como cliente HTTP para:

- validar `http://localhost:8080`;
- abrir `http://localhost:8080/ProyectoWebUno/`;
- enviar el formulario;
- observar el HTML dinámico resultante.

---

# 5. Preparación del entorno desde cero con IntelliJ IDEA

## 5.1 Decisión de ruta antes de comenzar

Usa este criterio:

```text
¿Tienes integración Ultimate/Jakarta EE activa?
        |
        +-- SÍ --> RUTA A: IntelliJ + Tomcat integrado
        |
        +-- NO --> RUTA B: IntelliJ + Maven + Tomcat externo
```

**La Ruta B es suficiente para completar toda la sesión.** La Ruta A es una comodidad del IDE, no un requisito conceptual.

## 5.2 Paso 1 - Descargar e instalar IntelliJ IDEA si el equipo aún no lo tiene

Si ya vienes trabajando con IntelliJ desde las sesiones anteriores, **no reinstales el IDE**. Salta al paso 2.

En un equipo nuevo:

1. Abre la página oficial: `https://www.jetbrains.com/idea/download/`.
2. Descarga **IntelliJ IDEA** para Windows. Desde 2025.3 JetBrains utiliza un producto unificado, por lo que no debes buscar un instalador separado llamado Community.
3. Ejecuta el instalador descargado.
4. Conserva la carpeta propuesta o selecciona una ruta institucional.
5. Si el instalador ofrece **Add bin folder to PATH**, puedes marcarlo; no es obligatorio para esta sesión, pero facilita abrir el IDE desde terminal.
6. Finaliza la instalación.
7. Abre IntelliJ IDEA.
8. Si aparece importación de configuración, importa tu configuración anterior solo si corresponde; en un equipo nuevo puedes iniciar con la configuración por defecto.
9. Si aparece la prueba Ultimate, puedes utilizarla. La ruta base de esta guía seguirá funcionando aunque posteriormente continúes con el conjunto gratuito de funciones.

### Evidencia de validación

Debes poder abrir IntelliJ IDEA y llegar a la pantalla de bienvenida o a un proyecto.

## 5.3 Paso 2 - Comprobar el JDK usado por el curso

En una terminal de Windows ejecuta:

```bat
java -version
```

### Si aparece una versión válida

Conserva ese JDK si es el mismo que estás usando en las sesiones anteriores y es Java 17 o superior.

### Si Java no existe en el equipo

Puedes instalar un JDK desde IntelliJ al crear el proyecto:

1. `File > New > Project`.
2. En el selector **JDK**, abre la lista.
3. Elige **Download JDK**.
4. Selecciona una distribución OpenJDK disponible y **versión 25** si quieres seguir la referencia LTS de esta guía.
5. Espera a que el IDE termine la descarga.

También puedes instalar un JDK externamente y luego seleccionar **Add JDK from Disk**.

### Validación dentro de IntelliJ

Abre:

```text
File > Project Structure > Project
```

Comprueba que **Project SDK** apunte al JDK de la clase.

## 5.4 Paso 3 - Descargar Apache Tomcat

1. Abre `https://tomcat.apache.org/`.
2. Selecciona la rama **Tomcat 11**.
3. En la sección de binarios, localiza **Core**.
4. En Windows descarga el archivo **zip**.
5. No descargues el código fuente para esta práctica.
6. Descomprime el ZIP en una ruta simple. Ejemplo:

```text
C:\Java\apache-tomcat-11.0.26
```

7. Comprueba que dentro existan carpetas como:

```text
bin
conf
lib
logs
webapps
```

No muevas archivos individuales fuera de esa estructura.

## 5.5 Paso 4 - Probar Tomcat sin depender del IDE

Esta prueba separa los problemas del servidor de los problemas del proyecto.

1. Abre la carpeta:

```text
C:\Java\apache-tomcat-11.0.26\bin
```

2. Ejecuta:

```text
startup.bat
```

3. Espera a que el proceso termine de iniciar.
4. Abre el navegador.
5. Visita:

```text
http://localhost:8080
```

6. Si aparece la página inicial de Tomcat, el servidor funciona.
7. Para detenerlo ejecuta:

```text
shutdown.bat
```

### Si la ventana se cierra demasiado rápido

Abre `cmd`, entra a `bin` y ejecuta:

```bat
catalina.bat run
```

Así podrás leer el error directamente en la terminal.

## 5.6 Paso 5 - Revisar plugins de IntelliJ

Abre:

```text
File > Settings > Plugins
```

### Caso A - Vas a usar la ruta base sin Ultimate

No necesitas instalar ningún plugin adicional. Continúa con la creación del proyecto Maven descrita en EJ04.

### Caso B - Tienes funciones Ultimate activas

1. En la pestaña **Installed**, busca `Tomcat and TomEE`.
2. Confirma que esté habilitado.
3. Busca `Jakarta EE Platform` y `Jakarta EE: Application Servers`; confirma que estén habilitados.
4. Busca `Jakarta EE: Web/Servlets`; confirma que esté habilitado.
5. Abre **Marketplace**.
6. Busca exactamente:

```text
Jakarta EE: Server Pages (JSP)
```

7. Si aparece como no instalado, pulsa **Install**.
8. Reinicia IntelliJ IDEA si el IDE lo solicita.

### Cómo saber si la integración Tomcat está disponible

Abre:

```text
File > Settings > Build, Execution, Deployment > Application Servers
```

Si puedes usar `+` y seleccionar **Tomcat Server**, la integración oficial está disponible.

## 5.7 Paso 6 - Registrar Tomcat dentro de IntelliJ (solo Ruta A / Ultimate)

1. Abre `File > Settings`.
2. Ve a `Build, Execution, Deployment > Application Servers`.
3. Pulsa `+`.
4. Selecciona **Tomcat Server**.
5. En **Tomcat Home**, selecciona la carpeta raíz de Tomcat, por ejemplo:

```text
C:\Java\apache-tomcat-11.0.26
```

6. IntelliJ detectará la versión.
7. Aplica los cambios con **Apply** y **OK**.

### Evidencia

Tomcat debe quedar listado como servidor de aplicaciones.

## 5.8 Qué NO debes instalar para esta sesión

No necesitas:

- Spring Boot;
- GlassFish;
- WildFly;
- Docker;
- XAMPP;
- servidor Node.js;
- plugin Tomcat de terceros;
- base de datos;
- JSTL adicional.

La sesión se mantiene en JSP + Apache Tomcat + Maven + navegador.

---


# EJ01 - Validar Java antes de usar Tomcat

## Qué vamos a construir / resolver

Vamos a comprobar el prerrequisito más básico: Tomcat no debe iniciarse "a ciegas". Primero verificaremos que Windows encuentra Java y que la JVM puede ejecutarse.

## Qué aprenderás aquí

- por qué `java -version` es una validación previa;
- cómo interpretar una salida válida;
- por qué **Java disponible** y **`JAVA_HOME` configurado** son comprobaciones distintas;
- cómo diferenciar un problema de JDK, variables de entorno y Tomcat.

## Archivos, recursos o artefactos involucrados

- Símbolo del sistema de Windows;
- comandos `java -version`, `where java` y `set JAVA_HOME`;
- ruta del JDK configurado en IntelliJ IDEA.

## Punto de partida

Tienes Windows abierto y todavía no has iniciado Tomcat.

## Paso 1 - Comprender la necesidad

### Problema actual

Todavía no sabemos si el equipo puede ejecutar Java.

### Qué necesitamos crear/modificar

No crearemos archivos. Necesitamos producir una **evidencia de entorno**.

### Por qué lo necesitamos

Tomcat se ejecuta sobre Java. Si Java no puede iniciarse, cualquier fallo posterior de Tomcat sería difícil de interpretar.

### Qué responsabilidad tendrá

El comando solo responde una pregunta: **¿Windows puede localizar y ejecutar Java?**

## Paso 2 - Ejecutar el primer microbloque

### Estado antes

No hay evidencia del JDK.

### Escribe ahora

```bat
java -version
```

### Explicación detallada

- `java` invoca el ejecutable de Java disponible en el sistema.
- `-version` pide mostrar la versión y datos del runtime.
- Si aparece una versión, el comando fue localizado.
- Si Windows indica que `java` no se reconoce, no continúes con Tomcat: primero necesitas corregir la disponibilidad del JDK.

### Elementos nuevos

`java`: ejecutable de Java.  
`-version`: opción de consulta; no ejecuta tu proyecto.

### Estado después

Ahora tienes una salida que confirma o niega la disponibilidad de Java.

## Paso 3 - Verificar que Tomcat pueda localizar el JDK

Que `java -version` funcione **no garantiza** que `startup.bat` tenga definida la variable que necesita. Comprueba:

```bat
where java
set JAVA_HOME
```

### Cómo interpretar

- `where java` indica qué ejecutable encuentra Windows.
- `set JAVA_HOME` debe mostrar una ruta al directorio raíz de un JDK.
- La ruta correcta termina en la carpeta del JDK; **no** debe terminar en `\bin` ni en `java.exe`.

Si `JAVA_HOME` no está definido, localiza el JDK en IntelliJ IDEA:

```text
File > Project Structure > Platform Settings > SDKs
```

Anota el **JDK home path** y realiza una prueba temporal en el CMD actual:

```bat
set "JAVA_HOME=C:\RUTA\REAL\DEL\JDK"
set "PATH=%JAVA_HOME%\bin;%PATH%"
"%JAVA_HOME%\bin\java.exe" -version
```

Después verifica que Tomcat ya puede leer Java:

```bat
cd /d <TOMCAT_HOME>\bin
catalina.bat version
```

### Estado después

Tienes dos evidencias diferentes:

```text
JAVA EJECUTABLE = confirmado por java -version
JAVA_HOME PARA TOMCAT = confirmado por catalina.bat version
```

### Por qué podemos avanzar

Tomcat solo debe probarse después de confirmar ambos prerrequisitos.

## Auditoría del artefacto construido

| Elemento | Qué hace | Por qué existe | Efecto |
|---|---|---|---|
| `java` | ejecuta Java | Tomcat depende de Java | inicia la JVM |
| `-version` | consulta la versión | valida el entorno | muestra evidencia |

## Antes de ejecutar o validar: predicción

1. Si Java está correctamente instalado, ¿esperas ver una versión o una página web?
2. ¿Tomcat debería estar iniciado para que `java -version` funcione?

## Ejecuta / valida

Ejecuta el comando una vez y copia la primera línea de salida en tus apuntes.

## Resultado esperado

Una salida con una versión de Java. Para la configuración recomendada, debería indicar Java 25; una versión compatible con la política institucional también puede ser válida.

## Cómo interpretarlo

La prueba confirma Java. Todavía **no confirma Tomcat**, IntelliJ IDEA ni la aplicación JSP.

## Error o caso límite controlado

### Caso A - `java` no se reconoce

El problema está antes de Tomcat: falta el JDK o Windows no encuentra `java`.

### Caso B - `java -version` funciona, pero `startup.bat` muestra:

```text
Neither the JAVA_HOME nor the JRE_HOME environment variable is defined
```

Este caso es distinto: Java puede existir, pero Tomcat iniciado desde ese CMD no conoce la carpeta del JDK.

## Por qué ocurre

IntelliJ puede tener un JDK configurado para el proyecto sin que una ventana externa de CMD tenga definida la variable `JAVA_HOME`. Además, las variables que se agregan en Windows no aparecen retroactivamente en terminales que ya estaban abiertas.

## Corrección razonada

1. Identifica el **JDK home path** en IntelliJ.
2. No uses la carpeta `bin` como valor de `JAVA_HOME`.
3. Para una prueba inmediata usa:

```bat
set "JAVA_HOME=C:\RUTA\REAL\DEL\JDK"
set "PATH=%JAVA_HOME%\bin;%PATH%"
catalina.bat version
```

4. Cuando confirme que funciona, registra `JAVA_HOME` de forma persistente en las Variables de entorno de Windows y agrega `%JAVA_HOME%\bin` a `Path`.
5. Cierra y vuelve a abrir CMD.
6. Repite `set JAVA_HOME`, `java -version` y `catalina.bat version`.

En un equipo institucional sin permisos, no modifiques variables de sistema sin autorización; utiliza variables de usuario o solicita apoyo al responsable del laboratorio.

## Qué debes poder explicar con tus palabras

Por qué validar Java reduce la cantidad de causas posibles cuando Tomcat no inicia.

## T01 - Tarea espejo

### Enunciado

Ejecuta `java -version`, registra la primera línea y decide si el equipo cumple el prerrequisito para Tomcat 11.

### Archivos/artefactos a modificar

Ninguno.

### Restricción

No inicies Tomcat hasta justificar tu decisión.

### Pista

Tomcat 11 necesita una versión moderna de Java; la guía recomendada usa JDK 25 LTS.

### Evidencia que debes mostrar

- captura o copia textual de la salida;
- una frase: `APTO` o `NO APTO`, seguida de tu justificación.

### Cómo saber si está correcta

Tu decisión debe basarse en la versión observada, no en asumir que Java "ya estaba instalado".

---

# EJ02 - Iniciar y detener Apache Tomcat manualmente

## Qué vamos a construir / resolver

Vamos a cambiar el estado del servidor de **detenido** a **activo**, comprobarlo desde el navegador y luego devolverlo a **detenido**.

## Qué aprenderás aquí

- qué hace `startup.bat`;
- qué hace `shutdown.bat`;
- por qué `localhost:8080` es una evidencia distinta de `java -version`;
- cómo leer el estado antes y después.

## Archivos, recursos o artefactos involucrados

- carpeta de Tomcat;
- subcarpeta `bin`;
- `startup.bat`;
- `shutdown.bat`;
- navegador.

## Punto de partida

EJ01 fue validado y Java funciona.

## Paso 1 - Comprender la necesidad

### Problema actual

Tenemos Java, pero todavía no existe un servidor escuchando solicitudes web para nuestra aplicación.

### Qué necesitamos crear/modificar

No crearemos código. Cambiaremos el **estado operativo de Tomcat**.

### Por qué lo necesitamos

Las páginas JSP de esta sesión deben ser atendidas por Tomcat. Abrir un archivo JSP directamente desde el explorador de archivos no reproduce el flujo de servidor.

### Qué responsabilidad tendrá

Tomcat recibirá solicitudes HTTP locales y procesará la aplicación web.

## Paso 2 - Iniciar Tomcat

### Estado antes

```text
Tomcat = DETENIDO
Navegador -> localhost:8080 = sin servicio de Tomcat
```

### Escribe / ejecuta ahora

Desde la carpeta `bin`:

```bat
startup.bat
```

### Explicación detallada

- `startup.bat` es el archivo por lotes de Windows utilizado para iniciar Tomcat.
- Debe ejecutarse desde una instalación de Tomcat válida.
- El comando inicia el proceso del servidor; no abre automáticamente tu proyecto JSP.

### Estado después

```text
Tomcat = INICIANDO / ACTIVO
```

### Por qué avanzamos

Ahora podemos probar si el servidor realmente responde.

## Paso 3 - Validar con el navegador

### Escribe / abre ahora

```text
http://localhost:8080
```

### Explicación detallada

- `localhost` representa el mismo equipo.
- `8080` es el puerto utilizado por la configuración estándar de Tomcat en esta práctica.
- Ver la página inicial de Tomcat demuestra que el servidor está atendiendo solicitudes en ese puerto.

### Estado después

```text
Navegador -> Tomcat = RESPUESTA VISIBLE
```

## Paso 4 - Detener Tomcat

Ejecuta:

```bat
shutdown.bat
```

Después intenta actualizar `http://localhost:8080`.

## Estado antes y después

```text
ANTES: Tomcat detenido
   v startup.bat
DESPUÉS: Tomcat activo
   v localhost:8080
EVIDENCIA: página de Tomcat
   v shutdown.bat
FINAL: Tomcat detenido
```

## Auditoría del artefacto construido

| Elemento | Qué hace | Por qué existe | Efecto |
|---|---|---|---|
| `bin` | contiene scripts operativos | centraliza comandos de Tomcat | permite iniciar/detener |
| `startup.bat` | inicia Tomcat | activa servidor | abre puerto de servicio |
| `localhost:8080` | solicita al servidor local | valida desde cliente | muestra respuesta |
| `shutdown.bat` | detiene Tomcat | cierra el servicio manual | deja de responder |

## Antes de ejecutar o validar: predicción

1. ¿Qué debe ocurrir en el navegador antes de `startup.bat`?
2. ¿Qué debe cambiar después de iniciar Tomcat?
3. ¿Qué esperas después de `shutdown.bat`?

## Resultado esperado

Con Tomcat activo, la página inicial debe ser accesible en `localhost:8080`.

## Error o caso límite controlado

`localhost:8080` no responde aunque Java funciona.

## Por qué ocurre

La validación de Java no inicia Tomcat. El servidor puede estar detenido o haber fallado al iniciar.

## Corrección razonada

No repitas `startup.bat` a ciegas. Desde `bin`, ejecuta primero:

```bat
catalina.bat version
```

Si allí aparece un problema de `JAVA_HOME`, corrígelo antes de continuar. Si la versión se muestra correctamente, ejecuta:

```bat
catalina.bat run
```

Esta modalidad mantiene el servidor y los mensajes en la misma terminal. Interpreta el primer error visible antes de modificar código JSP.

### Si el puerto 8080 está ocupado

Comprueba:

```bat
netstat -ano | findstr :8080
```

Si aparece un proceso escuchando en ese puerto, identifica la causa antes de cambiar `server.xml`. En un laboratorio institucional, no finalices procesos ajenos sin autorización.

## Qué debes poder explicar con tus palabras

La diferencia entre validar el JDK y validar el servidor.

## T02 - Tarea espejo

### Enunciado

Realiza un ciclo completo `iniciar -> validar -> detener -> volver a validar` y registra qué cambia en cada etapa.

### Archivos/artefactos a modificar

Ninguno.

### Restricción

No uses IntelliJ IDEA para iniciar Tomcat en esta tarea; el objetivo es comprobar el modo manual.

### Pista

Usa `startup.bat`, navegador y `shutdown.bat` en ese orden.

### Evidencia que debes mostrar

Una tabla de cuatro filas: estado inicial, después de iniciar, respuesta del navegador y estado después de detener.

### Cómo saber si está correcta

La tabla debe distinguir claramente el estado del proceso y la evidencia observable en el navegador.

---

# EJ03 - Instalar Tomcat como servicio de Windows

## Qué vamos a construir / resolver

Vamos a registrar Tomcat como un servicio de Windows para poder administrarlo desde la consola de servicios del sistema.

## Qué aprenderás aquí

- diferencia entre iniciar Tomcat con un script y registrarlo como servicio;
- función de `service.bat install`;
- por qué el nombre del servicio debe ser identificable;
- qué permisos pueden ser necesarios.

## Archivos, recursos o artefactos involucrados

- Símbolo del sistema;
- carpeta `bin` de Tomcat;
- `service.bat`;
- consola **Servicios** de Windows.

## Punto de partida

Tomcat ya funciona en modo manual.

## Paso 1 - Comprender la necesidad

### Problema actual

Cada inicio manual depende de ejecutar `startup.bat`.

### Qué necesitamos crear/modificar

Registrar una entrada de servicio en Windows.

### Por qué lo necesitamos

El material de la sesión muestra una segunda forma de operación: administrar Tomcat desde Servicios de Windows.

### Qué responsabilidad tendrá

El servicio permitirá iniciar, detener, pausar o configurar el inicio desde la herramienta de servicios.

## Paso 2 - Abrir una terminal con permisos apropiados

La instalación de un servicio suele requerir permisos administrativos. Si el equipo institucional no te permite elevar permisos, **no fuerces la configuración**; realiza EJ02 y deja EJ03 como demostración del docente.

## Paso 3 - Entrar a `bin`

Ejemplo:

```bat
cd C:\Java\apache-tomcat-11.0.26\bin
```

La ruta debe adaptarse a tu instalación real.

## Paso 4 - Registrar el servicio

### Escribe ahora

```bat
service.bat install Tomcat11
```

### Explicación detallada

- `service.bat` administra el registro de Tomcat como servicio en Windows.
- `install` indica que queremos crear el servicio.
- `Tomcat11` es el nombre utilizado para identificarlo.

### Estado antes

```text
Windows Services: no existe el servicio Tomcat11
```

### Estado después

```text
Windows Services: aparece Tomcat11
```

## Paso 5 - Validar en Servicios de Windows

1. Abre la herramienta **Servicios**.
2. Busca el servicio registrado.
3. Comprueba que puedes identificar su estado.
4. Si tu entorno lo permite, inicia y detén el servicio desde esa consola.

## Auditoría del artefacto construido

| Fragmento | Qué hace | Por qué existe | Efecto |
|---|---|---|---|
| `service.bat` | administra servicio Tomcat | integra con Windows | permite registrar |
| `install` | crea el registro | define operación | servicio disponible |
| `Tomcat11` | nombre del servicio | permite identificarlo | aparece en Servicios |

## Antes de ejecutar o validar: predicción

1. ¿Qué diferencia habrá entre `startup.bat` y un servicio registrado?
2. ¿Dónde esperas ver `Tomcat11` después de la instalación?

## Error o caso límite controlado

El comando devuelve error de permisos.

## Por qué ocurre

Crear servicios modifica configuración del sistema y puede requerir privilegios administrativos.

## Corrección razonada

En un equipo personal autorizado, abre la terminal con permisos apropiados. En laboratorio institucional, solicita apoyo al docente o usa el modo manual de EJ02.

## Qué debes poder explicar con tus palabras

Por qué instalar como servicio no cambia el código JSP, sino la forma de operar el servidor.

## T03 - Tarea espejo

### Enunciado

Si tu equipo permite instalar servicios, registra Tomcat con el nombre indicado por el docente y demuestra que aparece en Servicios. Si no tienes permisos, documenta exactamente el punto donde el sistema lo impide.

### Archivos/artefactos a modificar

Configuración de servicio de Windows, solo cuando esté autorizado.

### Restricción

No desactives controles de seguridad ni uses credenciales ajenas.

### Pista

La evidencia principal no es el navegador; es la entrada visible en Servicios de Windows.

### Evidencia que debes mostrar

Nombre del servicio y estado observado, o evidencia del bloqueo de permisos.

### Cómo saber si está correcta

La evidencia debe demostrar que comprendes la diferencia entre operación manual y servicio.

---

# EJ04 - Crear `ProyectoWebUno` en IntelliJ IDEA

## Qué vamos a construir / resolver

Crearemos el proyecto Maven que contendrá `index.jsp` y `saludo.jsp`. La meta es obtener una estructura portable que funcione tanto con la integración Ultimate de Tomcat como con el despliegue manual sobre un Tomcat externo.

## Qué aprenderás aquí

- por qué mantenemos Maven al cambiar de IDE;
- por qué las páginas JSP irán en `src/main/webapp`;
- qué significa `packaging` igual a `war`;
- cómo crear el proyecto sin depender de un asistente específico de NetBeans;
- cómo preparar una ejecución equivalente en IntelliJ IDEA.

## Archivos, recursos o artefactos involucrados

- IntelliJ IDEA;
- Maven;
- `pom.xml`;
- carpeta `src/main/webapp`;
- Apache Tomcat.

## Punto de partida

JDK validado, Tomcat descargado y probado, IntelliJ IDEA abierto.

## Paso 1 - Comprender la necesidad

### Problema actual

El servidor ya existe, pero todavía no tenemos una aplicación que pueda empaquetarse y desplegarse.

### Qué necesitamos crear

Un proyecto Maven con empaquetado WAR y recursos web dentro de `src/main/webapp`.

### Por qué lo necesitamos

Tomcat despliega aplicaciones web. Maven nos permite producir un archivo `.war` independiente del IDE.

## Paso 2 - Crear el proyecto base en IntelliJ

### Ruta B - Base institucional, funciona sin Ultimate

1. En IntelliJ selecciona **File > New > Project**.
2. Selecciona **Maven** como sistema de construcción. Si la pantalla muestra primero Java, selecciona Maven como **Build system**.
3. En **Name**, escribe:

```text
ProyectoWebUno
```

4. Selecciona el JDK del curso.
5. Elige una carpeta de trabajo.
6. Crea el proyecto.
7. Espera a que IntelliJ termine la sincronización Maven.

### Estado después

Debes tener al menos:

```text
ProyectoWebUno/
|-- pom.xml
\-- src/
```

## Paso 3 - Convertirlo en aplicación web Maven

Abre `pom.xml` y asegúrate de que el proyecto contenga estas decisiones:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.lideratecacademy</groupId>
    <artifactId>ProyectoWebUno</artifactId>
    <version>1.0-SNAPSHOT</version>
    <packaging>war</packaging>

    <properties>
        <maven.compiler.release>21</maven.compiler.release>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    </properties>

    <dependencies>
        <dependency>
            <groupId>jakarta.servlet</groupId>
            <artifactId>jakarta.servlet-api</artifactId>
            <version>6.1.0</version>
            <scope>provided</scope>
        </dependency>
    </dependencies>

    <build>
        <finalName>ProyectoWebUno</finalName>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-war-plugin</artifactId>
                <version>3.4.0</version>
                <configuration>
                    <failOnMissingWebXml>false</failOnMissingWebXml>
                </configuration>
            </plugin>
        </plugins>
    </build>
</project>
```

### Explicación detallada

- `artifactId` identifica el proyecto Maven.
- `packaging>war</packaging>` indica que el producto es una aplicación web desplegable.
- `jakarta.servlet-api` aporta las APIs de Servlet compatibles con Tomcat 11; `provided` significa que Tomcat las proporciona al ejecutar.
- `finalName` hace que Maven produzca `ProyectoWebUno.war`, por lo que el contexto esperado será `/ProyectoWebUno`.
- `maven-war-plugin` empaqueta `src/main/webapp` dentro del WAR.

> Si el curso ya fijó otro JDK compatible, ajusta `maven.compiler.release` a esa versión. No cambies JDK solo por copiar este bloque.

## Paso 4 - Crear la carpeta web

En la ventana **Project**:

1. Expande `src/main`.
2. Si no existe `webapp`, haz clic derecho sobre `main`.
3. Selecciona **New > Directory**.
4. Escribe:

```text
webapp
```

La ruta final debe ser:

```text
src/main/webapp
```

Aquí estarán `index.jsp` y `saludo.jsp`.

## Paso 5 - Sincronizar Maven

Después de editar `pom.xml`:

1. IntelliJ puede mostrar un aviso para cargar los cambios Maven. Pulsa **Load Maven Changes** si aparece.
2. Si no aparece, abre la ventana Maven y pulsa **Reload All Maven Projects**.
3. Espera a que las dependencias se resuelvan.

### Error controlado

Si `jakarta.servlet-api` aparece en rojo, primero confirma conexión a Internet y vuelve a recargar Maven. No cambies la dependencia por una API `javax.servlet` antigua, porque Tomcat 11 trabaja con el espacio de nombres Jakarta.

## Paso 6 - Ruta A opcional: crear el proyecto directamente con Jakarta EE

Si tienes funciones Ultimate activas, también puedes usar:

```text
File > New > Project > Jakarta EE
```

Configura:

```text
Name: ProyectoWebUno
Template: Web application
Build tool: Maven
JDK: JDK del curso
Jakarta EE: 11
Dependency: Servlet
```

Después registra Tomcat en `Application Servers` y continúa con el mismo `src/main/webapp`.

La ruta base y la ruta Ultimate deben terminar con el mismo concepto: **un proyecto Maven empaquetable como WAR**.

## Paso 7 - Configurar ejecución con Tomcat integrado (solo Ultimate)

1. Ve a **Run > Edit Configurations**.
2. Pulsa `+`.
3. Selecciona **Tomcat Server > Local**.
4. En **Application server**, selecciona el Tomcat registrado.
5. Abre la pestaña **Deployment**.
6. Pulsa `+ > Artifact`.
7. Selecciona el artefacto WAR exploded del proyecto.
8. Define el contexto:

```text
/ProyectoWebUno
```

9. En **Server**, usa como URL:

```text
http://localhost:8080/ProyectoWebUno/
```

10. Guarda con **OK**.

## Paso 8 - Preparar ejecución sin Ultimate

No necesitas crear una configuración Tomcat en el IDE.

Cuando llegue el momento de ejecutar:

1. Abre la ventana **Maven**.
2. Expande `Lifecycle`.
3. Ejecuta `clean`.
4. Ejecuta `package`.
5. Debe aparecer:

```text
target/ProyectoWebUno.war
```

6. Copia ese WAR a:

```text
<TOMCAT_HOME>\webapps\
```

7. Inicia Tomcat con `startup.bat`.
8. Tomcat desplegará la aplicación automáticamente.
9. Abre:

```text
http://localhost:8080/ProyectoWebUno/
```

## Estado antes y después

```text
ANTES: IDE + JDK + Tomcat, pero sin aplicación
   v
CREAR proyecto Maven
   v
packaging = war
   v
src/main/webapp
   v
DESPUÉS: ProyectoWebUno listo para recibir JSP
```

## Auditoría del artefacto construido

| Elemento | Qué hace | Por qué existe | Evidencia |
|---|---|---|---|
| `pom.xml` | define el proyecto Maven | hace portable el build | Maven lo reconoce |
| `packaging=war` | produce aplicación web | Tomcat despliega WAR | aparece `target/*.war` |
| `src/main/webapp` | contiene recursos web | raíz web estándar Maven | allí crearás JSP |
| `finalName` | fija nombre del WAR | mantiene `/ProyectoWebUno` | WAR con nombre estable |
| Tomcat | ejecuta JSP | servidor de la sesión | responde en 8080 |

## Antes de ejecutar o validar: predicción

1. ¿Crear el proyecto basta para obtener ya el saludo dinámico?
2. ¿Qué archivo tendremos que crear primero dentro de `src/main/webapp`?
3. Si el WAR se llama `ProyectoWebUno.war`, ¿qué contexto esperas en la URL?

## Error o caso límite controlado

### Caso 1 - No aparece `Tomcat Server` en Run Configurations

**Causa probable:** estás usando el conjunto gratuito de funciones o el plugin oficial está deshabilitado.

**Corrección:** utiliza la Ruta B con Maven + despliegue externo. No es un bloqueo para la clase.

### Caso 2 - No aparece `Jakarta EE` al crear proyecto

**Causa probable:** las funciones Ultimate no están activas.

**Corrección:** crea un proyecto Maven normal y configura `pom.xml` como se explicó.

## Qué debes poder explicar con tus palabras

Por qué el IDE es una herramienta de trabajo, mientras que Maven define el empaquetado y Tomcat ejecuta la aplicación.

## T04 - Tarea espejo

### Enunciado

Crea `ProyectoWebUno` en IntelliJ IDEA, configura el empaquetado WAR, crea `src/main/webapp` y demuestra cuál de las dos rutas de ejecución utilizarás: Tomcat integrado o Tomcat externo.

### Archivos/artefactos a modificar

- `pom.xml`;
- `src/main/webapp`.

### Restricción

Todavía no crees `saludo.jsp`.

### Pista

La tarea está completa cuando Maven reconoce el proyecto y puedes identificar dónde estarán las páginas JSP.

### Evidencia que debes mostrar

- árbol del proyecto;
- `pom.xml`;
- ruta `src/main/webapp`;
- evidencia de Tomcat registrado en IntelliJ **o** explicación de despliegue externo.

### Cómo saber si está correcta

El proyecto debe poder empaquetarse como WAR y conservar el contexto `ProyectoWebUno`.

---


# EJ05 - Construir `index.jsp`: formulario de entrada

## Qué vamos a construir / resolver

Construiremos la página que solicita un nombre y lo envía a otra página JSP.

## Qué aprenderás aquí

- cómo crear un archivo JSP;
- función de `action`, `method`, `name` y `required`;
- por qué el nombre del parámetro debe ser estable desde el formulario.

## Archivos, recursos o artefactos involucrados

- `index.jsp` dentro de `src/main/webapp`.

## Punto de partida

`ProyectoWebUno` existe, Maven lo reconoce y ya definiste cómo se desplegará en Tomcat (ruta base externa o integración Ultimate).

## Paso 1 - Crear el archivo JSP

### Antes de construir

Todavía no existe una página de entrada para la aplicación.

### ¿Por qué necesitamos este paso?

Necesitamos un recurso que el navegador pueda mostrar y desde el cual el usuario envíe su nombre.

### Crea ahora

1. Clic secundario sobre el proyecto.
2. **New**.
3. **JSP**.
4. En **File Name**, escribe `index`.
5. Finaliza.

El resultado debe ser `index.jsp` dentro de las páginas web del proyecto.

## Paso 2 - Construir la estructura HTML

### Escribe ahora

```html
<!DOCTYPE html>
<html>
<head>
    <title>Identificación</title>
</head>
<body>
</body>
</html>
```

### Explicación detallada

- `<!DOCTYPE html>` declara el documento HTML.
- `<html>` contiene el documento.
- `<head>` agrupa metadatos visibles para el navegador.
- `<title>` define el título de la pestaña.
- `<body>` contendrá el formulario visible.

### Estado después

Existe una página válida pero todavía no recibe datos.

## Paso 3 - Agregar la instrucción visible

Dentro de `<body>` escribe:

```html
<h2>Digita tu nombre:</h2>
```

`<h2>` presenta la instrucción al usuario.

## Paso 4 - Abrir el formulario

Escribe:

```html
<form action="saludo.jsp" method="get">
</form>
```

### Explicación detallada

- `<form>` agrupa datos que serán enviados.
- `action="saludo.jsp"` define el recurso que recibirá la solicitud.
- `method="get"` envía los datos como parámetros de la solicitud GET.

### Estado antes y después

```text
ANTES: página sin flujo de envío
ACCIÓN: crear form + action + method
DESPUÉS: página sabe a qué recurso enviar y con qué método
```

## Paso 5 - Crear el campo `nombre`

Dentro del formulario escribe:

```html
<input type="text" name="nombre" required>
```

### Explicación detallada

- `type="text"` crea un campo de texto.
- `name="nombre"` define la clave con la que viajará el dato.
- `required` solicita al navegador impedir el envío cuando el campo está vacío.

El atributo más importante para conectar con `saludo.jsp` será `name="nombre"`.

## Paso 6 - Crear el botón

Agrega:

```html
<input type="submit" value="Saludar">
```

- `type="submit"` envía el formulario.
- `value="Saludar"` es el texto del botón.

## Traza manual

Si el usuario escribe `Ana`:

```text
Campo visible: Ana
name del campo: nombre
method: GET
action: saludo.jsp

Solicitud conceptual:
saludo.jsp?nombre=Ana
```

## Auditoría del artefacto construido

| Elemento | Qué hace | Por qué existe | Efecto |
|---|---|---|---|
| `action` | define destino | conecta páginas | solicitud a `saludo.jsp` |
| `method="get"` | define método | transporta parámetro | dato en solicitud GET |
| `name="nombre"` | nombra dato | permite recuperarlo | clave `nombre` |
| `required` | valida en navegador | evita envío vacío desde formulario | bloqueo previo |
| `submit` | dispara envío | inicia solicitud | navegador navega al destino |

## Archivo completo al terminar este ejemplo

```jsp
<!DOCTYPE html>
<html>
<head>
    <title>Identificación</title>
</head>
<body>
    <h2>Digita tu nombre:</h2>
    <form action="saludo.jsp" method="get">
        <input type="text" name="nombre" required>
        <input type="submit" value="Saludar">
    </form>
</body>
</html>
```

## Antes de ejecutar o validar: predicción

1. Si escribes `Ana`, ¿qué clave viajará con ese valor?
2. ¿Qué archivo recibirá el formulario?
3. ¿Qué ocurrirá si intentas enviar el campo vacío desde esta página?

## Resultado esperado

`index.jsp` muestra el texto, un campo y el botón **Saludar**.

## Error o caso límite controlado

Cambiar `action="saludo.jsp"` por un archivo inexistente.

## Por qué ocurre

El formulario intentaría navegar a un recurso que no existe.

## Corrección razonada

Restaurar exactamente `action="saludo.jsp"` antes de continuar.

## Qué debes poder explicar con tus palabras

Por qué `name` no es solo un texto decorativo del campo.

## T05 - Tarea espejo

### Enunciado

Antes de crear `saludo.jsp`, utiliza el código de `index.jsp` para predecir cómo viajará el nombre `Lucía` en la solicitud GET y explica qué función cumple `required`.

### Archivos/artefactos a modificar

`index.jsp` solo si necesitas corregirlo.

### Restricción

No cambies `method="get"` ni `name="nombre"`.

### Pista

Identifica destino, método, clave y valor.

### Evidencia que debes mostrar

Una línea conceptual como:

```text
saludo.jsp?nombre=Lucía
```

y una explicación de una frase sobre `required`.

### Cómo saber si está correcta

La clave debe coincidir exactamente con el atributo `name` del input.

---

# EJ06 - Construir `saludo.jsp` y realizar el primer despliegue externo

## Qué vamos a construir / resolver

Crearemos la página que recibe el parámetro `nombre`, valida si existe y genera un saludo personalizado. Después realizaremos el **primer despliegue real en Apache Tomcat externo**.

> En esta ruta IntelliJ IDEA **no ejecuta Tomcat**. IntelliJ sirve para editar el proyecto y ejecutar Maven. El servidor se inicia desde Windows con `catalina.bat run` o `startup.bat`.

## Qué aprenderás aquí

- cómo recuperar un parámetro de la solicitud;
- por qué puede ser `null` o quedar vacío;
- cómo se usa el valor dentro del HTML generado;
- cómo empaquetar el proyecto como WAR;
- cómo desplegar el WAR en Tomcat externo;
- cómo validar la aplicación desde el navegador.

## Archivos, recursos o artefactos involucrados

- `saludo.jsp`;
- `pom.xml`;
- `target/ProyectoWebUno.war`;
- `<TOMCAT_HOME>\webapps\`.

## Punto de partida

`index.jsp` ya envía un parámetro llamado `nombre` a `saludo.jsp`.

## Paso 1 - Crear `saludo.jsp`

Dentro de `src/main/webapp`, crea `saludo.jsp`.

## Paso 2 - Construir la estructura HTML

```html
<!DOCTYPE html>
<html>
<head>
    <title>Bienvenida</title>
</head>
<body>
</body>
</html>
```

Todavía es una página estática.

## Paso 3 - Recuperar el parámetro

```jsp
<%
    String nombre = request.getParameter("nombre");
%>
```

- `<% ... %>` delimita un bloque Java ejecutado por Tomcat/JSP.
- `request.getParameter("nombre")` busca la clave `nombre` enviada por el formulario.
- Debe coincidir con `name="nombre"` de `index.jsp`.

## Paso 4 - Proteger el caso sin valor

```jsp
<%
    String nombre = request.getParameter("nombre");
    if (nombre == null || nombre.trim().equals("")) {
        nombre = "invitado";
    }
%>
```

Primero se comprueba `null`; gracias al cortocircuito de `||`, `trim()` no se invoca sobre una referencia nula.

## Paso 5 - Mostrar el resultado

```jsp
<h2>Hola, <%= nombre %>! Bienvenido a tu primera app JSP.</h2>
<a href="index.jsp">Volver</a>
```

## Archivo completo al terminar este ejemplo

```jsp
<!DOCTYPE html>
<html>
<head>
    <title>Bienvenida</title>
</head>
<body>
<%
    String nombre = request.getParameter("nombre");
    if (nombre == null || nombre.trim().equals("")) {
        nombre = "invitado";
    }
%>
    <h2>Hola, <%= nombre %>! Bienvenido a tu primera app JSP.</h2>
    <a href="index.jsp">Volver</a>
</body>
</html>
```

## Paso 6 - Guardar antes de desplegar

Guarda `index.jsp`, `saludo.jsp` y `pom.xml`.

**No pulses Run en IntelliJ esperando que Tomcat aparezca.** En la ruta base el servidor no está integrado al IDE.

## Paso 7 - Empaquetar desde IntelliJ con Maven

### Opción A - Ventana Maven

1. Abre **Maven**.
2. Expande `Lifecycle`.
3. Ejecuta `clean`.
4. Ejecuta `package`.

### Opción B - Terminal, si `mvn` está disponible

```bat
mvn clean package
```

Debe generarse:

```text
ProyectoWebUno\target\ProyectoWebUno.war
```

Si el WAR no existe, no continúes con Tomcat.

## Paso 8 - Desplegar en Tomcat externo

Si Tomcat está activo, deténlo. Si se inició con `catalina.bat run`, usa `Ctrl+C`. Si está en segundo plano:

```bat
cd /d <TOMCAT_HOME>\bin
shutdown.bat
```

Elimina **solo** la versión anterior de este laboratorio si existe:

```text
<TOMCAT_HOME>\webapps\ProyectoWebUno.war
<TOMCAT_HOME>\webapps\ProyectoWebUno\
```

Copia el WAR nuevo a:

```text
<TOMCAT_HOME>\webapps\ProyectoWebUno.war
```

## Paso 9 - Iniciar Tomcat externamente

```bat
cd /d <TOMCAT_HOME>\bin
catalina.bat run
```

Mantén esa consola abierta.

## Paso 10 - Ejecutar desde el navegador

La aplicación **se ejecuta en Tomcat**, no en IntelliJ.

Abre:

```text
http://localhost:8080/ProyectoWebUno/
```

Escribe `Ana` y pulsa **Saludar**.

Resultado esperado:

```text
Hola, Ana! Bienvenido a tu primera app JSP.
```

Prueba también:

```text
http://localhost:8080/ProyectoWebUno/saludo.jsp
```

Sin parámetro debe aparecer `invitado`.

## Traza manual

```text
IntelliJ edita JSP
      ↓
Maven genera WAR
      ↓
WAR se copia a Tomcat/webapps
      ↓
Tomcat externo despliega y procesa JSP
      ↓
Navegador recibe HTML
```

## T06 - Tarea espejo

Cambia el respaldo de `"invitado"` a `"estudiante"`. Para observar el cambio debes repetir:

```text
MODIFICAR EN INTELLIJ
→ MAVEN CLEAN/PACKAGE
→ DETENER TOMCAT
→ REEMPLAZAR WAR/DESPLIEGUE
→ CATALINA.BAT RUN
→ NAVEGADOR
```

Después restaura `"invitado"` y realiza un último redespliegue para dejar la solución canónica.

### Evidencia

- WAR generado;
- URL probada;
- resultado temporal con `estudiante`;
- resultado final restaurado con `invitado`.

---

# EJ07 - Diagnosticar parámetro y ruta con Tomcat externo

## Qué vamos a construir / resolver

Provocaremos dos errores controlados. Como Tomcat **no está integrado en IntelliJ**, cada cambio que queramos observar debe pasar por un nuevo empaquetado y un nuevo despliegue.

## Regla de ejecución de este ejemplo

Cuando la guía diga **probar** o **ejecutar**, significa:

```text
1. guardar en IntelliJ
2. Maven clean/package
3. detener Tomcat externo
4. retirar ProyectoWebUno.war y webapps\ProyectoWebUno anteriores
5. copiar el WAR nuevo a webapps
6. iniciar catalina.bat run
7. abrir la URL en el navegador
```

No significa pulsar Run en IntelliJ.

## Caso 1 - Parámetro desincronizado

Estado correcto:

```text
index.jsp: name="nombre"
saludo.jsp: request.getParameter("nombre")
```

Cambia temporalmente en `index.jsp`:

```html
<input type="text" name="nombreUsuario" required>
```

Mantén:

```jsp
request.getParameter("nombre")
```

### Predicción

```text
Solicitud: nombreUsuario=Ana
saludo.jsp busca: nombre
getParameter("nombre") -> null
fallback -> invitado
```

### Reempaquetar y redesplegar

```bat
mvn clean package
```

Luego detén Tomcat, reemplaza el WAR anterior, inicia `catalina.bat run` y abre:

```text
http://localhost:8080/ProyectoWebUno/
```

Escribe `Ana` y pulsa **Saludar**.

### Resultado esperado

Debe aparecer `invitado`, porque la clave enviada no coincide con la buscada.

### Corregir

Restaura:

```html
<input type="text" name="nombre" required>
```

Repite **package + deploy + navegador**. Debe volver a aparecer `Hola, Ana!...`.

## Caso 2 - Ruta JSP incorrecta (T07)

Cambia temporalmente:

```html
<form action="saludos.jsp" method="get">
```

No crees `saludos.jsp`.

Predice el síntoma y repite el ciclo de despliegue externo.

### Resultado esperado

El servidor debe indicar que el recurso solicitado no existe.

Diferencia:

- parámetro incorrecto: `saludo.jsp` existe y se procesa, pero la clave no coincide;
- ruta incorrecta: el recurso solicitado no existe.

### Corrección

Restaura:

```html
<form action="saludo.jsp" method="get">
```

Empaqueta y despliega nuevamente para dejar el proyecto correcto.

## Qué debes poder explicar

1. IntelliJ edita el proyecto; no ejecuta Tomcat en esta ruta.
2. Maven construye el WAR.
3. Tomcat ejecuta la aplicación desplegada.
4. Un cambio en fuente no cambia automáticamente el WAR ya desplegado.

---

# EJ08 - Integrar y ejecutar la aplicación completa

## Qué vamos a construir / resolver

Integraremos el proyecto completo y validaremos el recorrido real desde el navegador hasta el HTML generado.

## Qué aprenderás aquí

- por qué se elimina `index.html` en el flujo de la sesión;
- cómo empaquetar el proyecto desde IntelliJ IDEA y ejecutarlo en Tomcat externo;
- cómo acceder por URL;
- cómo interpretar tres casos de prueba;
- cómo relacionar JSP, Tomcat y HTML dinámico.

## Archivos, recursos o artefactos involucrados

- `index.jsp`;
- `saludo.jsp`;
- proyecto `ProyectoWebUno`;
- Apache Tomcat;
- navegador.

## Punto de partida

Los dos archivos JSP están completos y corregidos.

## Paso 1 - Revisar la carpeta web

Antes de ejecutar, confirma que existen:

```text
src/main/webapp/
|-- index.jsp
\-- saludo.jsp
```

Si el proyecto conserva un `index.html` generado por la plantilla, elimínalo según la secuencia de la sesión para que `index.jsp` sea la entrada esperada.

## Paso 2 - Asegurar que Tomcat está disponible

Si tienes integración Ultimate, ejecuta la configuración Tomcat Local. Si utilizas la ruta base, empaqueta el WAR con Maven, cópialo a `webapps` e inicia Tomcat externamente.

## Paso 3 - Ejecutar el proyecto

Ejecuta `ProyectoWebUno` mediante la ruta elegida: configuración Tomcat Local (Ultimate) o despliegue de `target/ProyectoWebUno.war` en `<TOMCAT_HOME>\webapps` (ruta base).

La ruta esperada de la práctica es:

```text
http://localhost:8080/ProyectoWebUno
```

La URL objetivo de esta guía es `http://localhost:8080/ProyectoWebUno/`. Con `finalName=ProyectoWebUno`, tanto el despliegue manual como el integrado pueden mantener ese contexto.

## Paso 4 - Caso de prueba A: nombre válido

Entrada:

```text
Ana
```

Predicción:

```text
index.jsp envía nombre=Ana
saludo.jsp recupera Ana
if = false
salida = Hola, Ana! ...
```

Resultado esperado:

```text
Hola, Ana! Bienvenido a tu primera app JSP.
```

## Paso 5 - Caso de prueba B: intento vacío desde `index.jsp`

Deja el campo vacío y pulsa **Saludar**.

Predicción:

El navegador debe impedir el envío porque el campo tiene `required`.

Interpretación:

Este control ocurre antes de llegar a `saludo.jsp` cuando el formulario se usa normalmente.

## Paso 6 - Caso de prueba C: acceso directo a `saludo.jsp`

Abre directamente una ruta equivalente a:

```text
http://localhost:8080/ProyectoWebUno/saludo.jsp
```

Predicción:

No llega el parámetro `nombre`; el código usa `invitado`.

Resultado esperado:

```text
Hola, invitado! Bienvenido a tu primera app JSP.
```

## Paso 7 - Interpretar el flujo completo

```text
1. Navegador solicita index.jsp
2. Tomcat atiende la aplicación
3. Usuario escribe nombre
4. Formulario GET solicita saludo.jsp?nombre=Ana
5. saludo.jsp recupera el parámetro
6. Java decide qué valor usar
7. JSP genera HTML dinámico
8. Tomcat envía la respuesta
9. Navegador muestra el HTML
```

## Qué ve el usuario y qué no ve

El usuario ve el resultado HTML. La lógica Java que recupera y valida `nombre` se ejecuta en el servidor.

## Auditoría final

| Hito | Evidencia |
|---|---|
| Java disponible | `java -version` |
| Tomcat activo | `localhost:8080` |
| Proyecto web creado | árbol Maven en IntelliJ IDEA |
| Entrada construida | `index.jsp` |
| Respuesta construida | `saludo.jsp` |
| Parámetro conectado | `name="nombre"` <-> `getParameter("nombre")` |
| Caso válido | saludo con nombre |
| Caso sin parámetro | saludo a invitado |

## Archivo `index.jsp` final

```jsp
<!DOCTYPE html>
<html>
<head>
    <title>Identificación</title>
</head>
<body>
    <h2>Digita tu nombre:</h2>
    <form action="saludo.jsp" method="get">
        <input type="text" name="nombre" required>
        <input type="submit" value="Saludar">
    </form>
</body>
</html>
```

## Archivo `saludo.jsp` final

```jsp
<!DOCTYPE html>
<html>
<head>
    <title>Bienvenida</title>
</head>
<body>
<%
    String nombre = request.getParameter("nombre");
    if (nombre == null || nombre.trim().equals("")) {
        nombre = "invitado";
    }
%>
    <h2>Hola, <%= nombre %>! Bienvenido a tu primera app JSP.</h2>
    <a href="index.jsp">Volver</a>
</body>
</html>
```

## Antes de ejecutar o validar: predicción

Completa una tabla con los tres casos antes de ejecutarlos.

| Caso | Entrada | Predicción |
|---|---|---|
| A | `Ana` | |
| B | campo vacío desde formulario | |
| C | acceso directo a `saludo.jsp` | |

## Error o caso límite controlado

Si `localhost:8080` funciona pero `/ProyectoWebUno` no, el problema ya no está en el JDK básico ni necesariamente en Tomcat: revisa si el WAR fue desplegado, el contexto `/ProyectoWebUno`, y el estado de Tomcat. Si usas Ultimate, revisa también la configuración Deployment.

## Qué debes poder explicar con tus palabras

Explica la frase: **"Tomcat procesa JSP y el navegador recibe HTML dinámico"** usando los archivos y pruebas que acabas de ejecutar.

## T08 - Tarea espejo

### Enunciado

Ejecuta los tres casos de prueba A/B/C y construye una traza de 6 a 9 pasos del caso A desde el clic en **Saludar** hasta que aparece el saludo.

### Archivos/artefactos a modificar

Ninguno en la solución final.

### Restricción

La traza debe usar los nombres reales `index.jsp`, `saludo.jsp`, `nombre` y Apache Tomcat.

### Pista

Separa claramente solicitud, procesamiento y respuesta.

### Evidencia que debes mostrar

- resultados de A/B/C;
- traza del caso A;
- una frase que indique qué parte se ejecuta en servidor.

### Cómo saber si está correcta

La traza debe explicar el flujo sin introducir tecnologías no utilizadas en la sesión.

---

# 6. Cierre de sesión

En esta práctica construiste un recorrido web Java completo desde el entorno hasta el resultado visible. Primero comprobaste que Java estuviera disponible; después activaste Apache Tomcat y verificaste que respondiera en `localhost:8080`. Luego creaste `ProyectoWebUno` como aplicación web Maven en IntelliJ IDEA, empaquetable como WAR, y separaste dos responsabilidades: `index.jsp` solicita el dato y `saludo.jsp` lo procesa para generar una respuesta. La clave técnica de la conexión fue mantener sincronizado `name="nombre"` con `request.getParameter("nombre")`.

También comprobaste que no todos los errores significan lo mismo. Un Tomcat detenido produce un problema de servidor; una ruta `saludos.jsp` inexistente produce un problema de recurso; una clave de parámetro distinta puede provocar que `saludo.jsp` reciba `null` y active el valor `invitado`. Esta diferenciación es más importante que memorizar pasos, porque te permite diagnosticar el sistema por capas.

Repasa especialmente el flujo **navegador -> Tomcat -> JSP -> HTML dinámico -> navegador** y la diferencia entre la validación `required` del formulario y la validación Java dentro de `saludo.jsp`.

Para reforzar la sesión puedes continuar con los recursos de Lideratec Academy:  
Blog: https://lideratecacademy.com/blog/  
YouTube: https://www.youtube.com/@LideratecAcademy

Si deseas validar tu resultado o trabajar desde una versión ya materializada, puedes utilizar el laboratorio completo de FASE 15 como recurso opcional posterior.


# Recursos oficiales para esta configuración

- IntelliJ IDEA - instalación: `https://www.jetbrains.com/help/idea/installation-guide.html`
- IntelliJ IDEA - primera aplicación Jakarta EE: `https://www.jetbrains.com/help/idea/creating-and-running-your-first-jakarta-ee-application.html`
- IntelliJ IDEA - servidores de aplicaciones: `https://www.jetbrains.com/help/idea/application-servers-support.html`
- IntelliJ IDEA - configuración Tomcat: `https://www.jetbrains.com/help/idea/run-debug-configuration-tomcat-server.html`
- IntelliJ IDEA - plugins: `https://www.jetbrains.com/help/idea/managing-plugins.html`
- Apache Tomcat 11: `https://tomcat.apache.org/download-11`

> Las pantallas pueden variar ligeramente entre actualizaciones del IDE. Conserva las decisiones técnicas: Maven + WAR + `src/main/webapp` + Tomcat 11 + JSP.

---
