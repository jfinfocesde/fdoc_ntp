---
title: "Semana 5 - GitHub: Colaboración en la Nube"
description: "Lleva tu código a la nube y aprende a trabajar en equipo con GitHub."
position: 5
---

Bienvenido a la red social de los programadores. Si Git es tu cámara, **GitHub es tu Instagram**.

En esta guía aprenderás cómo subir tu código a internet, trabajar con compañeros y contribuir al mundo del Open Source de manera sencilla.

+++cards
---
columns: 2
items:
  - title: "¿Qué es GitHub?"
    icon: "GlobeIcon"
    content: "La nube donde vive tu código."
    href: "#que-es-github-y-para-que-sirve"
  - title: "Primeros Pasos"
    icon: "RepoIcon"
    content: "Crea tu primer repositorio remoto."
    href: "#tu-primer-repositorio-en-la-nube"
  - title: "Sincronización"
    icon: "SyncIcon"
    content: "Push, Pull y Clone: Comandos esenciales."
    href: "#sincronizando-tierra-vs-nube"
  - title: "Flujo de Trabajo"
    icon: "PeopleIcon"
    content: "Domina el arte de los Pull Requests."
    href: "#el-flujo-de-trabajo-profesional-github-flow"
---
+++

## ¿Qué es GitHub y para qué sirve?

Git (la herramienta) vive en tu computadora. GitHub (la plataforma) vive en internet.

GitHub es un servicio que aloja tus repositorios de Git en la nube.
- **Respaldo**: Si tiras café sobre tu laptop, tu código sigue a salvo en GitHub.
- **Portafolio**: Es tu hoja de vida técnica. Las empresas miran tu perfil para ver qué sabes hacer.
- **Colaboración**: Permite que múltiples personas trabajen en el mismo código sin pisarse la manguera.

---

## Tu Primer Repositorio en la Nube

Para subir tu código, primero necesitas un lugar vacío en la nube donde ponerlo.

### Paso 1: Crear el Repo en GitHub
1.  Ve a [github.com](https://github.com) e inicia sesión.
2.  Haz clic en el botón **+** (arriba a la derecha) y selecciona **"New repository"**.
3.  Ponle un nombre (ej. `mi-web-increible`).
4.  Déjalo en **Public**.
5.  **No** marques "Add a README file" todavía.
6.  Dale a **"Create repository"**.

### Paso 2: Conectar tu PC con GitHub

GitHub te mostrará unos comandos. Si ya tienes un proyecto en tu PC, usa la opción que dice **"…or push an existing repository from the command line"**.

```bash
# Conecta tu carpeta local con la dirección web del repo
git remote add origin https://github.com/TU_USUARIO/mi-web-increible.git

# Renombra tu rama principal a 'main' (el estándar moderno)
git branch -M main

# Sube tus cambios a la nube por primera vez (-u conecta tu rama local con la nube)
git push -u origin main
```

¡Listo! Si recargas la página de GitHub, verás tus archivos ahí.

---

## Sincronizando: Tierra vs Nube

Ahora tienes dos copias de tu proyecto: **Local** (tu PC) y **Remota** (GitHub).

+++mermaid
graph LR
    A["Tu PC (Local)"] -- "git push" --> B("GitHub Nube")
    B -- "git pull" --> A
    C["Otro PC"] -- "git clone" --> A
+++

### Los Comandos Esenciales

1.  **`git push` (Subir)**: Envía tus nuevos commits a la nube.
    *   *Analogía*: "Publicar post".
2.  **`git pull` (Bajar)**: Trae los cambios que otros subieron y actualiza tu carpeta.
    *   *Analogía*: "Refrescar feed".
3.  **`git clone` (Copiar)**: Descarga un repo completo por primera vez.
    *   *Analogía*: "Descargar álbum".

---

## El Flujo de Trabajo Profesional (GitHub Flow)

Aquí es donde muchos principiantes se pierden. ¿Cómo trabajan 5 personas sin borrar el trabajo del otro?

### La Regla de Oro: Nunca trabajes en `main`

La rama `main` es sagrada. Siempre debe tener código que funcione perfecto. Para hacer cambios, crea una **Rama (Feature Branch)**.

### Paso a Paso Graficado

1.  **Crear Rama**: Creas un universo paralelo para tu tarea.
2.  **Commit & Push**: Guardas cambios en TU rama y la subes a la nube.
3.  **Pull Request**: Pides permiso para unir tu rama a `main`.
4.  **Merge**: Si te aprueban, se fusiona.

+++mermaid
sequenceDiagram
    participant Yo as Mi PC
    participant GH as GitHub (Nube)
    participant Reviewer as Jefe/Compañero

    Note over Yo, GH: 1. Crear Rama y Trabajar
    Yo->>Yo: git switch -c nueva-funcion
    Yo->>Yo: git commit -m "Terminé"
    
    Note over Yo, GH: 2. Subir Rama
    Yo->>GH: git push origin nueva-funcion
    
    Note over GH, Reviewer: 3. Pull Request (PR)
    GH->>Reviewer: Notificación: "Nuevo PR abierto"
    Reviewer->>GH: Revisa el Código
    Reviewer-->>GH: Aprueba cambios
    
    Note over GH: 4. Merge (Fusión)
    GH->>GH: Fusionar 'nueva-funcion' en 'main'
    
    Note over Yo, GH: 5. Actualizar Local
    Yo->>GH: git pull origin main
+++

### Detalle de los Pasos

#### 1. Crear tu Rama
```bash
git switch -c boton-login
```

#### 2. Hacer Cambios y Subir tu Rama
```bash
git add .
git commit -m "Crear botón de login azul"
git push -u origin boton-login
```
*(No subas a main, sube a `origin boton-login`)*

#### 3. Abrir el Pull Request (PR)
Ve a tu repositorio en GitHub. Verás un botón amarillo que dice **"Compare & pull request"**.
-   Escribe un título: "Agrega botón de login".
-   Escribe una descripción: "Hice el botón azul porque combina con el logo".
-   Dale a **Create Pull Request**.

#### 4. Revisión y Aprobación
Ahora tu código está en una "sala de espera". Tus compañeros pueden verlo, dejar comentarios línea por línea y pedir cambios.
Si todo está bien, alguien le dará al botón verde **Merge pull request**.

#### 5. Actualizar tu PC
Ahora `main` en la nube tiene tu código nuevo, ¡pero tu `main` en el PC no!

```bash
git switch main
git pull origin main
```

---

## Trabajando con Forks (Código Ajeno)

Si quieres aportar a un proyecto donde **no tienes permiso** (como React o el proyecto de código abierto de otra empresa), el flujo cambia un poco.

+++mermaid
graph TD
    A["Repo Original (Upstream)"] -- "1. Fork" --> B["Tu Copia en GitHub (Origin)"]
    B -- "2. Clone" --> C["Tu PC (Local)"]
    C -- "3. Push" --> B
    B -- "4. Pull Request" --> A
+++

1.  **Fork**: Haces clic en el botón "Fork" en GitHub. Esto crea una copia exacta en **TU** cuenta.
2.  **Clone**: Clonas **TU** copia a tu PC.
3.  **Trabaja**: Haces cambios en una rama y subes a **TU** copia (`push`).
4.  **Pull Request**: Desde GitHub, pides enviar tus cambios desde **TU** copia hacia el **Repo Original**.

---

## Resumen de Comandos de Nube

| Comando | Acción | Cuándo usarlo |
| :--- | :--- | :--- |
| `git clone <url>` | Clonar | Cuando no tienes el proyecto en tu PC. |
| `git remote -v` | Verificar | Para ver a dónde estás conectado. |
| `git push origin <rama>` | Subir | Para enviar tus commits a la nube. |
| `git pull origin <rama>` | Actualizar | Para bajar lo nuevo de la nube. |
| `git fetch` | Consultar | Para ver si hay cambios nuevos sin bajarlos aún. |

---

## Consejos de Oro

1.  **Baja cambios antes de empezar**: Siempre corre `git pull origin main` antes de crear una nueva rama. Así empiezas desde la versión más nueva.
2.  **Ramas con nombres claros**: `feature/login`, `fix/header-roto`, `docs/readme`.
3.  **No subas secretos**: Jamás subas contraseñas o archivos `.env`.

¡Ahora estás listo para trabajar en cualquier equipo de desarrollo del mundo! 🚀
