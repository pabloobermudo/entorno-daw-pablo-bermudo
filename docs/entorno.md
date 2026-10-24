# Documentación de mi entorno de desarrollo · Práctica 2

**Nombre y apellidos:** Pablo Bermudo Jiménez
**URL de mi repositorio:** https://github.com/pabloobermudo/entorno-daw-pablo-bermudo

> Rellena cada apartado a medida que avanzas. Donde pone «pega aquí», copia el texto
> de la terminal (no hace falta captura). Escribe con tus palabras: no se valora la longitud,
> sino que se note que entiendes lo que has hecho.

---

## 1. Instalación de entornos (CE 2.a)

### 1.1. Entorno vacío (paso 3)

Resultado de `java -version` y `node -v` **antes** de instalar nada:

```
$ java -version
bash: java: command not found
$ node -v
bash: node: command not found
```

¿Por qué crees que aparece ese mensaje? (relaciónalo con la diapositiva «Problemas habituales del entorno»)

> El entorno está vacío: en devcontainer.json solo hay una imagen base (un Ubuntu mínimo, base:jammy) y no se ha añadido ninguna feature, así que Java y Node.js no están instalados. Cuando escribo java o node, la terminal busca ese programa en las carpetas del PATH y, como no lo encuentra, responde «command not found». Es el síntoma «Comando no encontrado» de la diapositiva de problemas habituales del entorno, pero aquí no es un fallo: simplemente todavía no hemos instalado los lenguajes. Se solucionará al añadir sus features a la receta y reconstruir el entorno.

### 1.2. Después de la 1.ª reconstrucción (paso 5)

Resultado de `java -version`, `node -v` y `jupyter lab --version` **después**:

```
$ java -version
openjdk version "27" 2026-09-15
OpenJDK Runtime Environment Temurin-27+35 (build 27+35)
OpenJDK 64-Bit Server VM Temurin-27+35 (build 27+35, mixed mode, sharing)
$ node -v
v24.22.1
$ jupyter lab --version
4.6.4
```

¿Qué líneas nuevas han aparecido en `devcontainer.json`? Explica con tus palabras qué hace cada una:

> Ha aparecido el bloque "features", que es la lista de módulos que se instalan en el contenedor al reconstruirlo. Dentro hay tres líneas: "java:1" instala Java (el JDK, con el compilador javac); "node:1" instala Node.js con npm; y "python:1" instala Python, y con la opción "installJupyterlab": true también el IDE JupyterLab. Las llaves vacías {} significan que se usan las opciones por defecto, es decir, la versión que trae cada feature. Además, la línea "image" ahora lleva una coma al final porque ya no es el último elemento del JSON.

### 1.3. Comparativa de los dos IDE (paso 6)

|                                         | Editor de GitHub Codespaces | JupyterLab |
|-----------------------------------------|-----------------------------|------------|
| ¿Libre o propietario?                   | Propietario | Libre (código abierto) |
| Licencia / empresa o comunidad          | Servicio comercial de GitHub (empresa de Microsoft). El editor está basado en VS Code | Licencia BSD 3-Clause. Lo mantiene la comunidad Project Jupyter |
| ¿Tiene coste? ¿Con qué límites?         | Gratis con límite: la cuenta Free incluye 120 horas de núcleo al mes (unas 60 h reales con la máquina de 2 núcleos) y 15 GB de almacenamiento. Si se gastan, hay que pagar o esperar al mes siguiente | Gratuito y sin límites de uso; solo pagas el ordenador o servidor donde lo ejecutes |
| ¿Se puede usar fuera de GitHub?         | No, el servicio Codespaces va unido a GitHub (aunque VS Code sí se puede instalar aparte en el ordenador) | Sí, se instala en cualquier ordenador o servidor con Python |
| Lo que más me ha gustado                | Que el entorno se crea solo a partir de la receta y es igual para todos, con terminal, extensiones y Git integrados | Que funciona en el navegador y permite mezclar código, texto y resultados en notebooks |
| Lo que menos me ha gustado              | Depende de internet y de las horas gratuitas, cada reconstrucción tarda varios minutos y se detiene solo si lo dejas sin usar un rato | No he podido probarlo en clase porque se quitó el paso 6; para proyectos Java es menos completo que el editor de Codespaces |
| ¿Para qué tipo de trabajo lo elegiría?  | Proyectos en equipo (web, Java, TypeScript) donde todos necesitan el mismo entorno | Python, análisis de datos y ejercicios en los que quiero ir viendo los resultados paso a paso |

---

## 2. Módulos y extensiones (CE 2.b)

| Extensión | ¿Para qué sirve? | ¿Qué cambió al instalarla? | ¿La mantengo? ¿Por qué? |
|-----------|------------------|----------------------------|-------------------------|
| Extension Pack for Java | Paquete de 6 extensiones para programar en Java: autocompletado, errores, depuración, ejecución y proyectos Maven/Gradle | Se instalaron también Debugger for Java, Language Support (Red Hat), Maven, Gradle, etc. Apareció «Java: Ready» en la barra de estado y pude ejecutar Factura.java con Run | Sí, porque el proyecto está en Java y la necesita todo el equipo; por eso está en la receta |
| Code Spell Checker      | Corrector ortográfico para el código y los comentarios | Subrayó como error muchas palabras correctas en español (imponible, conceptos, compilarlo…) y aparecieron más de 130 avisos en el panel Problemas | No: su diccionario está en inglés y en un equipo de habla hispana molesta más que ayuda. La desinstalé y la quité de la receta |

¿Qué diferencia hay entre instalar una extensión **solo desde el panel** y añadirla **también a `devcontainer.json`**?

> Si la instalo solo desde el panel, la extensión está únicamente en mi codespace: si reconstruyo el entorno o otra persona abre el repositorio, no la tendrá. Si la añado a devcontainer.json (en customizations > vscode > extensions), forma parte de la receta y se instala automáticamente en cada reconstrucción y en el entorno de cualquiera que abra el repositorio. Lo comprobé en la 2.ª reconstrucción: Extension Pack for Java apareció instalada sin hacer nada y Code Spell Checker ya no estaba (pasé de 15 a 14 extensiones instaladas). En el historial del repositorio se ve el commit «Parte 2: extensiones añadidas» con las dos, antes de eliminar el corrector.

---

## 3. Personalización y automatización (CE 2.c)

- **Tema visual elegido** (paso 10) y por qué: Dark Modern, porque el fondo oscuro cansa menos la vista.
- **Ajuste del proyecto** (paso 10). ¿Qué archivo se ha creado y qué contiene? Se ha creado .vscode/settings.json, que guarda en el repositorio el ajuste «formatear al guardar», así que se aplica a cualquiera que abra el proyecto.

```
{
    "editor.formatOnSave": true
}
```

- **Atajo de teclado** (paso 11). ¿Qué acción, qué combinación y para qué te sirve? He asignado Ctrl + Option + R (⌃⌥R en Mac) al comando «Codespaces: Rebuild Container». Me sirve para reconstruir el entorno directamente, sin abrir la paleta de comandos; lo usé en la 2.ª reconstrucción.
- **Snippet** (paso 12). ¿Qué escribes y qué aparece? Escribo «cabecera» en un archivo Java o TypeScript, elijo la sugerencia «Cabecera DAW», pulso Intro y aparece un comentario de cabecera con el nombre del archivo, mi nombre, la fecha de hoy y el módulo.
- **Automatización al crear el entorno** (paso 14). ¿Qué hace `postCreateCommand` y qué archivos/carpetas han aparecido después de reconstruir? Ejecuta npm install automáticamente al crear el contenedor, para que nadie tenga que acordarse de instalar las dependencias. Después de reconstruir aparecieron la carpeta node_modules/ (con lodash y typescript) y el archivo package-lock.json, que fija las versiones exactas para todo el equipo.
- **Tareas** (paso 13). ¿Cuántas tareas hay en `tasks.json` y qué hace cada una? Hay 3 tareas: «Java: compilar, empaquetar y ejecutar» (javac compila Factura.java, jar lo empaqueta en factura.jar y java -jar lo ejecuta); «TypeScript: compilar y ejecutar» (npm run build llama a tsc, que traduce factura.ts a JavaScript, y npm start lo ejecuta con Node.js); y «Build completo (Java + TypeScript)», que lanza las dos en secuencia y es la tarea de compilación por defecto (Cmd + Shift + B).

¿Qué parte de toda esta configuración es **personal** (solo para ti) y qué parte es **del proyecto** (la recibe cualquiera que abra el repositorio)?

> Es personal (solo para mí, se guarda en mi cuenta y no en el repositorio) el tema visual, el atajo de teclado (en Métodos abreviados aparece con origen «Usuario») y el ajuste de actualización de extensiones, que se configura en la pestaña Usuario. Es del proyecto (se guarda en el repositorio, en .vscode/ y .devcontainer/, y lo recibe cualquiera que lo abra) el ajuste de formatear al guardar (que hice en la pestaña Área de trabajo), el snippet, las tareas de compilación, las extensiones de la receta y el postCreateCommand.

---

## 4. Ejecutables de diferentes lenguajes en el mismo entorno (CE 2.e)

Salida completa de la tarea **Build completo** (paso 15):

```
 *  Ejecutando tarea: mkdir -p build/java && javac -d build/java src/java/Factura.java && jar --create --file build/factura.jar --main-class Factura -C build/java . && java -jar build/factura.jar

=== FACTURA generada con Java 27 ===
Dominio web anual              12.00 EUR
Alojamiento web                59.90 EUR
Logotipo corporativo          150.00 EUR
-----------------------------------------
Base imponible                221.90 EUR
IVA (21 %)                     46.60 EUR
TOTAL                         268.50 EUR

 *  Ejecutando tarea: npm run build && npm start

> plantilla-entorno-daw@1.0.0 build
> tsc

> plantilla-entorno-daw@1.0.0 start
> node dist/factura.js

=== FACTURA generada con Node.js v24.22.1 ===
Dominio web anual              12.00 EUR
Alojamiento web                59.90 EUR
Logotipo corporativo          150.00 EUR
-----------------------------------------
Base imponible                221.90 EUR
IVA (21 %)                     46.60 EUR
TOTAL                         268.50 EUR
```

| Lenguaje | Archivo fuente | Herramienta que lo traduce | Archivo generado | Cómo se ejecuta |
|----------|----------------|----------------------------|------------------|-----------------|
| Java       | `src/java/Factura.java` | `javac` (compila a bytecode .class) y `jar` (lo empaqueta) | `build/factura.jar` | `java -jar build/factura.jar` |
| TypeScript | `src/ts/factura.ts`     | `tsc`, el compilador de TypeScript (con `npm run build`) | `dist/factura.js` | `node dist/factura.js` (con `npm start`) |

**Opcional:** ¿has podido ejecutar los mismos archivos desde JupyterLab (paso 19)? ¿Por qué funciona en los dos IDE sin instalar nada más?

> No lo he ejecutado desde JupyterLab porque el profesor quitó el paso 6, pero funcionaría sin instalar nada más: JupyterLab y el editor de Codespaces son dos IDE distintos conectados al mismo contenedor, así que ven los mismos archivos (build/factura.jar y dist/factura.js) y los mismos programas instalados por la receta (Java y Node.js). Todo esto es el proceso de build del tema: resolver dependencias (npm install), compilar (javac, tsc) y empaquetar (jar). Las carpetas build/ y dist/ salen en gris y no se suben al repositorio porque están en .gitignore: cualquiera puede volver a generarlas.

---

## 5. Sistema de actualizaciones (CE 2.d)

| Elemento | ¿Quién lo actualiza? | Modo (automático / manual / ninguno) | Qué he configurado yo |
|----------|----------------------|--------------------------------------|-----------------------|
| El editor de Codespaces | GitHub | Automático | Nada, no se puede elegir |
| Las extensiones         | Yo, desde los ajustes de usuario | Manual (auto-actualización desactivada) | Extensions: Auto Update = off, para que no cambien solas en semana de exámenes |
| Java                    | Yo, en la receta | Ninguno: versión fija | "version": "21" (LTS) en la feature de Java; antes instalaba la última (27) |
| Node.js                 | La feature, dentro de las LTS | Automático (solo versiones LTS estables) | Lo dejo con {}: instala la LTS más reciente |
| Dependencias npm (lodash, typescript…) | Yo, en package.json y package-lock.json | Manual | Revisé con npm outdated y npm audit y actualicé lodash de 4.17.20 a 4.18.1 |

Versión de Java **antes** (paso 5) y **después** (paso 18):

```
ANTES (paso 5):
$ java -version
openjdk version "27" 2026-09-15
OpenJDK Runtime Environment Temurin-27+35 (build 27+35)
OpenJDK 64-Bit Server VM Temurin-27+35 (build 27+35, mixed mode, sharing)

DESPUÉS (paso 18):
$ java -version
openjdk version "21" 2023-09-19 LTS
OpenJDK Runtime Environment Microsoft-8425986 (build 21+35-LTS)
OpenJDK 64-Bit Server VM Microsoft-8425986 (build 21+35-LTS, mixed mode, sharing)
```

Resultado de `npm outdated` (paso 17):

```
Package        Current   Wanted    Latest  Location                   Depended by
@types/lodash  4.14.202  4.14.202  4.17.27 node_modules/@types/lodash entorno-daw-pablo-bermudo
@types/node    20.11.30  20.11.30  26.6.5  node_modules/@types/node   entorno-daw-pablo-bermudo
lodash         4.17.20   4.17.20   4.18.1  node_modules/lodash        entorno-daw-pablo-bermudo
typescript     5.4.5     5.4.5     7.0.2   node_modules/typescript    entorno-daw-pablo-bermudo
```

> Current y Wanted coinciden porque en package.json las versiones están fijadas exactas (sin ^), así que npm no instala ninguna más nueva por su cuenta; Latest es la última publicada.

Resultado de `npm audit` **antes** de actualizar lodash (solo el resumen final):

```
lodash  <=4.17.23
Severity: high
fix available via `npm audit fix --force`
Will install lodash@4.18.1, which is outside the stated dependency range
node_modules/lodash

1 high severity vulnerability
```

Resultado de `npm audit` **después**:

```
$ npm install
changed 1 package, and audited 6 packages in 826ms
found 0 vulnerabilities

$ npm audit
found 0 vulnerabilities
```

**Mi política de actualizaciones**: si este entorno lo usara un equipo de 5 personas durante todo el curso, ¿qué dejarías en automático y qué fijarías a mano? Justifícalo.

> Dejaría en automático solo lo que no puedo controlar o no suele romper nada: el editor de Codespaces (lo actualiza GitHub) y Node.js dentro de las versiones LTS, que son estables. Fijaría a mano todo lo que puede romper la compilación: la versión de Java (21, que es LTS) en la receta, para que las 5 personas compilen con la misma versión y no cambie sin avisar en una reconstrucción (sin fijarla, me instaló Java 27); las dependencias con versiones exactas en package.json y el package-lock.json, para que todos instalen lo mismo; y las extensiones en modo manual. Cada cierto tiempo, y nunca en semana de exámenes o de entregas, revisaría con npm outdated y npm audit, actualizaría lo necesario (sobre todo si hay vulnerabilidades, como pasó con lodash), comprobaría con Cmd + Shift + B que todo sigue compilando (después de fijar Java 21 la factura sigue dando 268.50 EUR) y lo subiría al repositorio para que el resto lo reciba al reconstruir.

---

## 6. Incidencias

Anota cualquier problema que hayas tenido y cómo lo resolviste (también si usaste un fragmento completo).

> - El profesor indicó en clase que no se hacía el paso 6 (abrir el proyecto en JupyterLab), por eso no hay captura 1-jupyterlab.png.
> - En el paso 4, al buscar features, marqué sin querer la casilla de «seleccionar todo» (1453 seleccionadas). Cancelé con Esc y volví a elegir solo Java y Node.js.
> - El asistente del paso 4 añadió "node:2" en lugar de "node:1". Lo cambié a mano a "node:1" para que coincidiera con los fragmentos de la plantilla.
> - En el paso 7 no aparecía «Run | Debug» porque la extensión de Java estaba en «Lightweight Mode». Esperé a que pasara a «Java: Ready» y ejecuté con el botón ▷. Esa ejecución usó el Java 25 que trae la propia extensión; la tarea de compilación del paso 15 ya usó el Java 27 del entorno.
> - Al crear Prueba.java, la extensión de Java escribió sola una plantilla de clase; la borré para probar el snippet y después eliminé el archivo.
> - El codespace se detuvo solo por inactividad mientras no lo usaba. Lo reinicié con «Restart codespace» y no se perdió nada.
> - La captura 4 la subí por error a docs/ y la moví a docs/capturas/. En mi versión la opción de Extensions: Auto Update se llama «off».
> - No he usado ningún fragmento completo de devcontainer.json; todos los cambios los hice a mano o con el asistente.

## 7. Reflexión final

¿Qué ventaja tiene describir el entorno «como código» frente a instalar cada programa a mano en tu ordenador? Piensa en un equipo con Mac y Windows.

> Al describir el entorno como código (devcontainer.json y la carpeta .vscode/), cualquier persona, tenga Mac, Windows o Linux, obtiene exactamente el mismo entorno en unos minutos solo con abrir el repositorio, sin instalar nada en su ordenador. Así se evita el «en mi equipo funciona» por tener versiones distintas de Java o Node.js, problemas de PATH o diferencias entre sistemas operativos. Además, la configuración queda guardada en Git: se ve qué se cambió y cuándo, se puede volver atrás si algo falla, y una persona nueva se incorpora al equipo en minutos en lugar de pasar días instalando programas. El inconveniente es que dependes de internet y de las horas gratuitas de Codespaces.