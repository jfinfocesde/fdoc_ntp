---
title: "Semana 2 - Introducción a Python"
description: "Introducción a Python"
position: 2
---

Python es un lenguaje de programación de alto nivel, interpretado y de propósito general, creado por Guido van Rossum en 1989. Es conocido por su filosofía de diseño que enfatiza la legibilidad del código, utilizando una sintaxis limpia y expresiva.

+++admonition
---
type: note
title: "El Zen de Python"
---
Python se rige por principios como "Bello es mejor que feo", "Explícito es mejor que implícito" y "Simple es mejor que complejo". Puedes ver estos principios ejecutando `import this` en tu intérprete de Python.
+++

## Python: Interpretado vs Compilado

Python es un lenguaje interpretado, lo que significa que el código se ejecuta línea por línea a través de un intérprete, en lugar de ser compilado a código máquina de antemano.

+++comparison-table
---
headers:
  - "Característica"
  - { text: "Lenguajes Compilados", highlight: false }
  - { text: "Lenguajes Interpretados (Python)", highlight: true }
rows:
  - ["Ejemplos", "C, C++, Rust, Go", "Python, JavaScript, Ruby, PHP"]
  - ["Ejecución", "Traducido antes de ejecutar", "Traducido línea por línea durante ejecución"]
  - ["Velocidad", "Generalmente más rápidos", "Generalmente más lentos (aunque optimizables)"]
  - ["Portabilidad", "Dependiente de la plataforma", "Independiente (corre donde esté el intérprete)"]
  - ["Depuración", "Ciclo edición-compilación-error", "Feedback inmediato de errores"]
  - ["Tipado", "Usualmente estático", "Usualmente dinámico"]
---
+++

## Instalación de Python

A continuación te detallamos cómo preparar tu entorno de desarrollo.

+++steps
### Windows
1.  Descarga el instalador desde [python.org](https://www.python.org/downloads/).
2.  Ejecuta el instalador. **¡IMPORTANTE!** Marca la casilla "Add Python to PATH" antes de dar clic en "Install Now".
3.  Verifica la instalación abriendo PowerShell y ejecutando: `python --version`.

### macOS
1.  Descarga el instalador "macOS 64-bit universal2 installer" desde [python.org](https://www.python.org/downloads/).
2.  Sigue el asistente de instalación estándar de macOS.
3.  Verifica abriendo la Terminal y ejecutando: `python3 --version`.

### Linux (Ubuntu/Debian)
1.  La mayoría viene con Python preinstalado. Verifica con `python3 --version`.
2.  Si no está, actualiza tus repositorios: `sudo apt update`.
3.  Instala Python: `sudo apt install python3`.
+++

### Video Guía
<br>

+++video
---
src: "https://www.youtube.com/watch?v=m5i-Pq-z9w8"
title: "Guía de Instalación de Python"
---
+++

## Herramientas de Desarrollo Recomendadas

Para programar en Python eficientemente, es crucial elegir un buen entorno de desarrollo. Aquí están las opciones más populares:

+++cards
---
columns: 2
items:
  - title: "Visual Studio Code"
    icon: "TerminalIcon"
    href: "https://code.visualstudio.com/"
    content: "El editor más popular. Ligero, extensible y con excelente soporte para Python mediante extensiones."
  - title: "Google Colab"
    icon: "CloudIcon"
    href: "https://colab.research.google.com/"
    content: "Ideal para ciencia de datos y aprendizaje. Ejecuta Python en la nube gratis, sin instalación."
  - title: "PyCharm"
    icon: "CodeIcon"
    href: "https://www.jetbrains.com/pycharm/"
    content: "IDE profesional completo de JetBrains. Potente para proyectos grandes, aunque más pesado."
  - title: "Jupyter Notebooks"
    icon: "BookOpenIcon"
    href: "https://jupyter.org/"
    content: "Estándar para análisis de datos, permite mezclar código, texto y visualizaciones en un solo documento."
---
+++

### Enfoque en: Google Colab

Google Colab es una herramienta fascinante de Google Research que permite escribir y ejecutar código Python en tu navegador.

+++feature-list
---
items:
  - title: "Cero Configuración"
    icon: "SettingsIcon"
    content: |
      Empieza a programar inmediatamente sin instalar nada en tu computadora.
  - title: "Acceso a GPU Gratuito"
    icon: "ZapIcon"
    content: |
      Potencia tus cálculos de ciencia de datos o aprendizaje automático con hardware de Google.
  - title: "Fácil de Compartir"
    icon: "ShareIcon"
    content: |
      Comparte tus notebooks (cuadernos) tan fácilmente como un documento de Google Docs.
---
+++



## Sintaxis y Estructura

### Indentación (Sangrado)

A diferencia de otros lenguajes que usan llaves `{}` para definir bloques de código, Python utiliza la **indentación**.

+++admonition
---
type: warning
title: "Regla de Oro"
---
La indentación es **obligatoria** y parte de la sintaxis. Un indentado incorrecto generará un `IndentationError`. Se recomienda usar **4 espacios** por nivel de indentación.
+++

```python
if True:
    print("Este código está indentado")
    if True:
        print("Este código tiene doble indentación")
print("Este código está fuera de los bloques if")
```

### Variables y Constantes

En Python, las variables se crean cuando les asignas un valor. No necesitas declarar el tipo explícitamente (tipado dinámico).

+++admonition
---
type: info
title: "Reglas de Nombramiento (Snake Case)"
---
*   Usa minúsculas para variables y funciones: `mi_variable`.
*   Separa palabras con guiones bajos `_`.
*   No empieces con números.
*   **Constantes**: Por convención, usa MAYÚSCULAS: `PI = 3.1416`, `MAX_USERS = 100`.
+++

```python
# Variables válidas
nombre_usuario = "Juan"
edad = 25
altura = 1.75

# Constantes (convención)
DIAS_SEMANA = 7
```

## Tipos de Datos Principales

Python ofrece varios tipos de datos nativos potentes:

1.  **Numéricos**:
    *   `int`: Enteros (ej. `10`, `-5`)
    *   `float`: Decimales (ej. `3.14`, `2.5`)
    *   `complex`: Números complejos (ej. `1 + 2j`)

2.  **Texto**:
    *   `str`: Cadenas de caracteres. Pueden usar comillas simples `' '` o dobles `" "`.

3.  **Booleanos**:
    *   `bool`: Representan verdad o falsedad (`True`, `False`).

4.  **Colecciones**:
    *   `list`: Ordenada y mutable. `['a', 'b', 1]`
    *   `tuple`: Ordenada e inmutable. `('a', 'b', 1)`
    *   `dict`: Pares clave-valor. `{'nombre': 'Ana', 'edad': 30}`
    *   `set`: Colección desordenada de elementos únicos. `{1, 2, 3}`

## Entrada y Salida

### Función `print()`

Muestra información en la consola. Desde Python 3.6, las **f-strings** son la forma preferida de formatear texto.

```python
nombre = "Carlos"
edad = 28
# Uso de f-string para interpolación
print(f"Hola, soy {nombre} y tengo {edad} años.")
```

### Función `input()`

Recibe datos del usuario. **Nota**: Siempre devuelve un `str` (texto).

```python
edad_str = input("Ingresa tu edad: ")
# Convertir a entero para operaciones matemáticas
edad_num = int(edad_str)
print(f"El próximo año tendrás {edad_num + 1} años.")
```
