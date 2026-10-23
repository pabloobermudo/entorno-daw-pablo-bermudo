# Documentación de mi entorno de desarrollo · Práctica 2

**Nombre y apellidos:**
**URL de mi repositorio:**

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
| ¿Libre o propietario?                   |                             |            |
| Licencia / empresa o comunidad          |                             |            |
| ¿Tiene coste? ¿Con qué límites?         |                             |            |
| ¿Se puede usar fuera de GitHub?         |                             |            |
| Lo que más me ha gustado                |                             |            |
| Lo que menos me ha gustado              |                             |            |
| ¿Para qué tipo de trabajo lo elegiría?  |                             |            |

---

## 2. Módulos y extensiones (CE 2.b)

| Extensión | ¿Para qué sirve? | ¿Qué cambió al instalarla? | ¿La mantengo? ¿Por qué? |
|-----------|------------------|----------------------------|-------------------------|
| Extension Pack for Java |   |   |   |
| Code Spell Checker      |   |   |   |

¿Qué diferencia hay entre instalar una extensión **solo desde el panel** y añadirla **también a `devcontainer.json`**?

> 

---

## 3. Personalización y automatización (CE 2.c)

- **Tema visual elegido** (paso 10) y por qué:
- **Ajuste del proyecto** (paso 10). ¿Qué archivo se ha creado y qué contiene?

```
pega aquí el contenido de .vscode/settings.json
```

- **Atajo de teclado** (paso 11). ¿Qué acción, qué combinación y para qué te sirve?
- **Snippet** (paso 12). ¿Qué escribes y qué aparece?
- **Automatización al crear el entorno** (paso 14). ¿Qué hace `postCreateCommand` y qué archivos/carpetas han aparecido después de reconstruir?
- **Tareas** (paso 13). ¿Cuántas tareas hay en `tasks.json` y qué hace cada una?

¿Qué parte de toda esta configuración es **personal** (solo para ti) y qué parte es **del proyecto** (la recibe cualquiera que abra el repositorio)?

> 

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
| Java       | `src/java/Factura.java` |   |   |   |
| TypeScript | `src/ts/factura.ts`     |   |   |   |

**Opcional:** ¿has podido ejecutar los mismos archivos desde JupyterLab (paso 19)? ¿Por qué funciona en los dos IDE sin instalar nada más?

> 

---

## 5. Sistema de actualizaciones (CE 2.d)

| Elemento | ¿Quién lo actualiza? | Modo (automático / manual / ninguno) | Qué he configurado yo |
|----------|----------------------|--------------------------------------|-----------------------|
| El editor de Codespaces |   |   |   |
| Las extensiones         |   |   |   |
| Java                    |   |   |   |
| Node.js                 |   |   |   |
| Dependencias npm (lodash, typescript…) |   |   |   |

Versión de Java **antes** (paso 5) y **después** (paso 18):

```
pega aquí
```

Resultado de `npm outdated` (paso 17):

```
pega aquí
```

Resultado de `npm audit` **antes** de actualizar lodash (solo el resumen final):

```
pega aquí
```

Resultado de `npm audit` **después**:

```
pega aquí
```

**Mi política de actualizaciones**: si este entorno lo usara un equipo de 5 personas durante todo el curso, ¿qué dejarías en automático y qué fijarías a mano? Justifícalo.

> 

---

## 6. Incidencias

Anota cualquier problema que hayas tenido y cómo lo resolviste (también si usaste un fragmento completo).

> 

## 7. Reflexión final

¿Qué ventaja tiene describir el entorno «como código» frente a instalar cada programa a mano en tu ordenador? Piensa en un equipo con Mac y Windows.

> 
