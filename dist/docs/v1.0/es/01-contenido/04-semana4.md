---
title: "Semana 4 - Git: Control de Versiones"
description: "Aprende a viajar en el tiempo con tu código. La guía definitiva de Git para principiantes."
position: 4
---

```video
---
src: "https://vimeo.com/1166221102?share=copy&fl=sv&fe=ci"
title: "Git"
---
```

Bienvenido al superpoder más importante de todo programador: **El Control del Tiempo**.

En esta guía aprenderás **Git** desde cero. No hablaremos de GitHub todavía (eso es la nube), aquí nos centraremos en **Git**, la herramienta que vive en tu computadora y que te salvará la vida mil veces.

+++cards
---
columns: 2
items:
  - title: "¿Qué es Git?"
    icon: "GitBranchIcon"
    content: "Entiende la máquina del tiempo."
    href: "#que-es-git-y-por-que-usarlo"
  - title: "Tu Identidad"
    icon: "UserIcon"
    content: "Configura quién eres para la historia."
    href: "#configuracion-inicial-tu-identidad"
  - title: "El Flujo de Trabajo"
    icon: "RefreshIcon"
    content: "Init, Add, Commit: El ciclo de la vida."
    href: "#el-ciclo-de-vida-tus-primeros-comandos"
  - title: "Ramas (Multiverso)"
    icon: "RepoForkedIcon"
    content: "Crea universos paralelos para experimentar."
    href: "#ramas-el-multiverso-del-codigo"
---
+++

## ¿Qué es Git y Por Qué Usarlo?

Imagina que estás escribiendo un documento muy importante. Seguramente has hecho esto:

- `tesis_final.docx`
- `tesis_final_v2.docx`
- `tesis_final_corregida.docx`
- `tesis_final_ESTA_SI_ES.docx`

Esto es un caos. **Git soluciona esto.**

Git es un **Sistema de Control de Versiones Distribuido**. Piensa en él como una **cámara fotográfica mágica** para tu código.
Cada vez que terminas una tarea importante, tomas una "foto" (llamada **Commit**) de cómo se ven todos tus archivos en ese momento.

### ¿Por qué lo necesitas?

1.  **Puntos de Guardado**: Puedes volver a cualquier punto del pasado. ¿Borraste algo por error y guardaste? Con Git, puedes "viajar en el tiempo" y recuperarlo.
2.  **Experimentación sin Miedo**: Puedes crear una "copia paralela" (rama) de tu proyecto, romper todo lo que quieras probando una idea loca, y si no funciona, simplemente borras esa línea temporal y vuelves a la original intacta.
3.  **Historia**: Sabes exactamente **quién** hizo qué cambio, **cuándo** y **por qué**.

---

## Conceptos Clave (Antes de los Comandos)

Para entender Git, debes visualizar tres áreas donde vive tu código:

1.  **Directorio de Trabajo (Working Directory)**: Es tu carpeta actual, donde estás escribiendo código y guardando archivos. Es el "Presente".
2.  **Área de Preparación (Staging Area)**: Es una zona intermedia. Aquí colocas los archivos que *quieres* incluir en tu próxima foto. Es como "preparar a los modelos" antes de la foto.
3.  **El Repositorio (.git)**: Es el álbum de fotos. Aquí se guardan permanentemente los cambios confirmados (Commits).

+++mermaid
graph LR
    A[Directorio de Trabajo] -- git add --> B[Staging Area]
    B -- git commit --> C[Repositorio .git]
    C -- git checkout --> A
+++

---

## Configuración Inicial: Tu Identidad

Antes de empezar, Git necesita saber quién eres. Esto es vital porque cada "foto" (commit) llevará tu firma.

Abre tu terminal (Git Bash, PowerShell o Terminal) y ejecuta **una sola vez**:

```bash
# Configura tu nombre (aparecerá en el historial)
git config --global user.name "Tu Nombre Completo"

# Configura tu correo (el mismo que usarás luego en GitHub)
git config --global user.email "tu_email@ejemplo.com"
```

+++admonition
---
type: tip
title: "Verifica tu configuración"
---
Puedes ver si guardaste bien tus datos escribiendo: `git config --list`
+++

---

## El Ciclo de Vida: Tus Primeros Comandos

Vamos a simular que empiezas un proyecto nuevo. Sigue estos pasos.

### 1. `git init` - El Big Bang

Este comando crea un nuevo universo (repositorio) en tu carpeta actual.

```bash
# Navega a tu carpeta de proyecto
cd mi-proyecto-web

# Inicializa Git
git init
```

*Resultado*: Se crea una carpeta oculta `.git`. Ahora Git está vigilando esta carpeta.

### 2. `git status` - El Radar

Este es el comando que usarás **todo el tiempo**. Te dice en qué estado están tus archivos.

```bash
git status
```

Git te dirá algo como "Untracked files" (archivos que no está vigilando) o "Changes not staged for commit" (archivos modificados pero no preparados).

### 3. `git add` - Preparar la Foto

Acabas de crear un archivo `index.html`. Git lo ve, pero no lo ha incluido en el "paquete" para la foto. Debes subirlo al **Staging Area**.

```bash
# Agregar un archivo específico
git add index.html

# Agregar TODOS los archivos modificados o nuevos (El más usado)
git add .
```

Ahora si haces `git status`, verás los archivos en verde. Están listos para la foto.

### 4. `git commit` - Tomar la Foto

Ahora que el escenario está listo en el Staging Area, tomamos la foto definitiva y la guardamos en el álbum.

```bash
git commit -m "Crear estructura inicial del proyecto"
```

**La regla de oro del mensaje (`-m`)**:
El mensaje debe ser claro y descriptivo.
- ❌ "arreglos"
- ❌ "listo"
- ✅ "Agregar barra de navegación y corregir colores del footer"

### 5. `git log` - El Libro de Historia

¿Quieres ver todos los "puntos de guardado" que has hecho?

```bash
git log
```

Te mostrará una lista con:
- El código único del commit (Hash).
- El autor.
- La fecha.
- El mensaje que escribiste.

---

## Ramas: El Multiverso del Código

Las **Ramas (Branches)** son la característica más poderosa de Git.

Imagina que tienes tu juego (código) funcionando perfecto en la "Línea Temporal Principal" (usualmente llamada `main` o `master`).
Quieres intentar agregar un "Jefe Final" (una nueva función compleja), pero te da miedo romper el juego que ya funciona.

**Solución:** Creas una rama llamada `jefe-final`. Es una copia exacta de tu realidad.
Puedes hacer lo que quieras en esa rama. Si el juego se rompe, la rama `main` sigue intacta. Si funciona perfecto, puedes "fusionar" (Merge) la rama `jefe-final` con la `main`.

### Comandos de Ramas

#### Crear y ver ramas

```bash
# Listar todas las ramas (la que tiene * es la actual)
git branch

# Crear una nueva rama
git branch nueva-funcionalidad
```

#### Viajar entre ramas (`switch` o `checkout`)

Para "moverte" a esa otra línea temporal:

```bash
# La forma moderna (Git 2.23+)
git switch nueva-funcionalidad

# La forma clásica
git checkout nueva-funcionalidad
```

#### Fusionar ramas (`merge`)

Supongamos que terminaste tu trabajo en `nueva-funcionalidad` y todo salió bien. Quieres traer esos cambios a `main`.

1.  Primero, vuelve a la rama principal: `git switch main`
2.  Luego, fusiona la otra rama hacia aquí:

```bash
git merge nueva-funcionalidad
```

¡Listo! Ahora `main` tiene todo lo nuevo.

---

## Viajando en el Tiempo: Deshacer Errores (Guía Completa)

Una de las preguntas más comunes es: *"¡Ayuda! Rompí todo, ¿cómo vuelvo atrás?"*. Aquí tienes los hechizos para cada situación.

### Nivel 1: "Aún no he guardado nada"
Escenario: Modificaste `style.css` y quedó horrible. No has hecho `git add` ni `git commit`. Quieres que el archivo vuelva a como estaba.

```bash
# Comando moderno (Git 2.23+)
git restore style.css

# Comando clásico
git checkout -- style.css
```

### Nivel 2: "Ya hice git add"
Escenario: Hiciste `git add .` pero te diste cuenta de que subiste un archivo que no debías. Quieres sacarlo del "Staging Area" pero no borrar tus cambios.

```bash
# Sacar del escenario (Unstage)
git restore --staged style.css
```

### Nivel 3: "El último commit quedó mal"
Escenario: Hiciste commit pero olvidaste un archivo, o escribiste mal el mensaje "arreglar bug" y querías poner "Arreglar bug de login".

```bash
# 1. Agrega los cambios olvidados (si los hay)
git add archivo_olvidado.js

# 2. Reescribe el último commit
git commit --amend -m "Nuevo mensaje corregido"
```
*Esto no crea un nuevo commit, sino que edita el anterior.*

### Nivel 4: "Quiero volver al pasado" (Reset)
Escenario: Los últimos 2 commits son un desastre total. Quieres borrar esa línea de tiempo y volver a como estaba todo hace 2 días.

⚠️ **CUIDADO**: `git reset` es poderoso.

**Opción A: Reset Suave (Soft)**
Vuelve al pasado, pero **mantiene tus cambios** en tu carpeta para que los arregles.
```bash
# Retroceder 1 commit pero mantener cambios
git reset --soft HEAD~1
```

**Opción B: Reset Fuerte (Hard)**
Vuelve al pasado y **destruye** todo lo que hiciste después. Es como si nunca hubiera pasado.
```bash
# Retroceder 1 commit y borrar todo
git reset --hard HEAD~1
```

### Nivel 5: "Quiero deshacer algo público" (Revert)
Escenario: Ya subiste el código a la nube (GitHub). Si haces `reset`, romperás el código de tus compañeros.
**Solución**: Crear un *nuevo* commit que haga exactamente lo contrario al commit malo.

```bash
# Crea un antídoto para el último commit
git revert HEAD
```

---

## Resumen de Comandos (Tu "Cheat Sheet")

Guarda esta tabla cerca, la usarás mucho.

| Comando | Descripción | Analogía |
| :--- | :--- | :--- |
| `git init` | Crea un repositorio en la carpeta actual. | Fundar una nueva ciudad. |
| `git clone [url]` | Copia un repositorio de la nube a tu PC. | Descargar el universo. |
| `git status` | Muestra qué archivos han cambiado. | El radar del estado actual. |
| `git add [archivo]` | Mueve cambios al Staging Area. | Subir los actores al escenario. |
| `git add .` | Mueve TODOS los cambios al Staging Area. | Subir a todo el elenco. |
| `git commit -m "msg"` | Guarda los cambios staged en el historial. | **Tomar la foto.** |
| `git log` | Muestra el historial de commits. | Leer el diario de bitácora. |
| `git branch` | Lista o crea ramas. | Ver los universos paralelos. |
| `git switch [rama]` | Cambia a otra rama. | Viajar a otro universo. |
| `git merge [rama]` | Fusiona una rama en la actual. | Unir dos universos. |
| `git restore [archivo]` | Deshace cambios locales. | Ctrl+Z recargado. |

---

## Consejos Finales para Principiantes

1.  **Haz commits pequeños y frecuentes**: No esperes a terminar todo el proyecto para hacer un commit. Haz commit cada vez que termines una pequeña tarea lógica (ej. "Terminar header", "Agregar botón", "Corregir estilo").
2.  **No entres en pánico**: Si te equivocas, casi todo en Git es reversible.
3.  **Lee los mensajes de error**: Git suele decirte exactamente qué hacer para solucionar el problema en el propio mensaje de error.

¡Felicidades! Ahora tienes el control del tiempo en tus manos. 🚀
