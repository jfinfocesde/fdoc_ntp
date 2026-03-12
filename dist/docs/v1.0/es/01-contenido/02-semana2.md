---
title: "Semana 2: Bases de Python para datos"
description: "Resolución de problemas comunes y guía de uso de Python (variables, listas, diccionarios)."
position: 2
---

```video
---
src: "https://vimeo.com/1162191856?share=copy&fl=sv&fe=ci"
title: "Semana 2 - Introducción a Python"
---
```

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

## Estructuras de datos - Colecciones en Python

En Python, una colección es una estructura de datos que puede almacenar varios elementos. 

+++admonition
---
type: note
title: "Tipos de Colecciones"
---
- **Listas**: Ordenadas, modificables, permiten duplicados.
- **Tuplas**: Ordenadas, **inmutables**, permiten duplicados.
- **Conjuntos**: **No ordenados**, no indexados, **sin duplicados**.
- **Diccionarios**: Pares clave-valor, modificables (v3.7+ ordenados por inserción).
+++

### Listas

Una lista es una colección ordenada y modificable. Permite almacenar elementos de diferentes tipos.

```python
# Creación y acceso
my_list = [1, 2, 3, 'cuatro', 'cinco']
print(my_list[0])  # Salida: 1
```

+++admonition
---
type: tip
title: "Métodos Útiles"
---
Las listas tienen métodos poderosos integrados:
- `.append(x)`: Agrega al final.
- `.insert(i, x)`: Inserta en posición `i`.
- `.remove(x)`: Elimina el primer `x`.
- `.pop([i])`: Elimina y devuelve el elemento en `i` (o el último).
- `.sort()`: Ordena la lista in-situ.
+++

**Ejemplo completo de operaciones:**

```python
mylist = [1, 2, "tres", 4.5]

# Modificar
mylist[2] = 3
print(mylist) # [1, 2, 3, 4.5]

# Agregar
mylist.append(5)

# Eliminar
del mylist[0] 
```

#### Ejercicios de Listas

1. **Números Pares**: Filtrar una lista para obtener solo los pares.

```python
def numeros_pares(lista):
    return [num for num in lista if num % 2 == 0]

print(numeros_pares([1, 2, 3, 4, 5, 6])) # [2, 4, 6]
```

#### Iterando Listas

+++tabs
---[tab title="Bucle For" lang="python"]---
frutas = ["manzana", "banana", "cereza"]
for fruta in frutas:
    print(fruta)
---[tab title="Con índice (enumerate)" lang="python"]---
frutas = ["manzana", "banana", "cereza"]
for i, fruta in enumerate(frutas):
    print(f"{i}: {fruta}")
---[tab title="Range y Len" lang="python"]---
frutas = ["manzana", "banana", "cereza"]
for i in range(len(frutas)):
    print(frutas[i])
---[tab title="Comprensión de Listas" lang="python"]---
# Crear una nueva lista de una sola línea
cuadrados = [x**2 for x in range(10)]
print(cuadrados)
---
+++

### Tuplas

Colecciones ordenadas e **inmutables**. Una vez creadas, no puedes cambiar su contenido.

+++comparison-table
---
headers:
  - "Característica"
  - { text: "Lista", highlight: false }
  - { text: "Tupla", highlight: true }
rows:
  - ["Sintaxis", "[]", "()"]
  - ["Mutable", "Sí", "**No**"]
  - ["Velocidad", "Normal", "Más rápida"]
  - ["Uso", "Datos dinámicos", "Datos constantes protegidos"]
---
+++

```python
mi_tupla = (1, 2, 'tres')
# mi_tupla[0] = 5  # ¡Error! TypeError
```

+++admonition
---
type: warning
title: "Inmutabilidad"
---
Si intentas modificar una tupla (`t[0] = x`), Python lanzará un error. Si necesitas modificarla, primero debes convertirla a lista: `list(tupla)`, modificarla y volver a convertir: `tuple(lista)`.
+++

#### Iterando Tuplas

Las tuplas se iteran de forma idéntica a las listas.

```python
mi_tupla = (10, 20, 30)
for numero in mi_tupla:
    print(numero)
```

### Conjuntos

Colecciones no ordenadas y **sin elementos duplicados**. Son ideales para operaciones de conjuntos matemáticos y eliminar duplicados.

```python
# Eliminando duplicados automáticamente
numeros = [1, 2, 2, 3, 4, 4, 5]
conjunto_unicos = set(numeros)
print(conjunto_unicos) # {1, 2, 3, 4, 5}
```

+++admonition
---
type: info
title: "Operaciones de Conjuntos"
---
- **Unión (`|` o `.union()`)**: Elementos en A o B.
- **Intersección (`&` o `.intersection()`)**: Elementos en A y B.
- **Diferencia (`-` o `.difference()`)**: Elementos en A pero no en B.
+++

```python
a = {1, 2, 3}
b = {3, 4, 5}

print(a.union(b))        # {1, 2, 3, 4, 5}
print(a.intersection(b)) # {3}
```

#### Iterando Conjuntos

+++admonition
---
type: note
title: "Nota sobre el Orden"
---
Recuerda que los conjuntos **no tienen orden garantizado**. Al iterarlos, los elementos pueden aparecer en cualquier secuencia.
+++

```python
colores = {"rojo", "verde", "azul"}
for color in colores:
    print(color)
```

### Diccionarios

Almacenan datos en pares `clave: valor`. El acceso es muy rápido a través de la clave.

```python
usuario = {
    'nombre': 'Juan',
    'edad': 30,
    'rol': 'admin'
}

print(usuario['nombre']) # Juan
```

#### Iterando Diccionarios

Existen varias formas de recorrer un diccionario:

+++tabs
---[tab title="Por Claves" lang="python"]---
# Itera sobre las claves (por defecto)
for clave in usuario:
    print(clave)
# 'nombre', 'edad', 'rol'
---[tab title="Por Valores" lang="python"]---
# Itera solo sobre los valores
for valor in usuario.values():
    print(valor)
# 'Juan', 30, 'admin'
---[tab title="Por Ambos" lang="python"]---
# Itera sobre clave y valor al tiempo
for clave, valor in usuario.items():
    print(f"{clave}: {valor}")
---[tab title="Comprensión de Diccionarios" lang="python"]---
# Crear un nuevo diccionario transformando datos
cuadrados = {x: x**2 for x in range(5)}
print(cuadrados)
# {0: 0, 1: 1, 2: 4, 3: 9, 4: 16}
---
+++

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

