---
title: "Semana 4 - Estructuras de Datos y Funciones"
description: "Domina las colecciones de datos (Listas, Tuplas, Conjuntos, Diccionarios) y la modularización con Funciones en Python."
position: 4
---

En esta semana profundizaremos en cómo organizar y manipular datos eficientemente en Python, y cómo estructurar tu código mediante funciones reutilizables.

+++cards
---
columns: 2
items:
  - title: "Listas"
    icon: "ListIcon"
    content: "Colecciones ordenadas y modificables."
    href: "#listas"
  - title: "Tuplas"
    icon: "LockIcon"
    content: "Colecciones ordenadas e inmutables."
    href: "#tuplas"
  - title: "Conjuntos"
    icon: "ArchiveIcon"
    content: "Colecciones sin orden y sin duplicados."
    href: "#conjuntos"
  - title: "Diccionarios"
    icon: "KeyIcon"
    content: "Estructuras clave-valor para acceso rápido."
    href: "#diccionarios"
  - title: "Funciones"
    icon: "CodeIcon"
    content: "Bloques de código reutilizables."
    href: "#funciones"
---
+++

```video
---
src: "https://vimeo.com/1164222787?share=copy&fl=sv&fe=ci"
title: "Estructuras de Datos y Funciones"
---
```

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

## Funciones

Las funciones permiten modularizar el código, haciéndolo más legible, reutilizable y fácil de mantener.

```python
def saludar(nombre, saludo="Hola"):
    """
    Imprime un saludo personalizado.
    Args:
        nombre (str): Nombre de la persona.
        saludo (str): Saludo opcional.
    """
    return f"{saludo}, {nombre}!"

print(saludar("Ana"))            # Hola, Ana!
print(saludar("Carlos", "Buen día")) # Buen día, Carlos!
```

### Variables Globales vs Locales

+++admonition
---
type: danger
title: "Uso de 'global'"
---
Las variables definidas dentro de una función son **locales**. Para modificar una variable global dentro de una función, debes declararla con `global`. Sin embargo, **evita usar variables globales** siempre que sea posible, ya que dificultan la depuración.
+++

```python
contador = 0

def incrementar():
    global contador
    contador += 1

incrementar()
print(contador) # 1
```

### Ejercicio con Funciones

Calculadora de precio total con lista de diccionarios:

```python
productos = [
    {'nombre': 'Laptop', 'precio': 1000, 'cantidad': 1},
    {'nombre': 'Mouse', 'precio': 20, 'cantidad': 2}
]

def calcular_total(lista_productos):
    total = 0
    for p in lista_productos:
        total += p['precio'] * p['cantidad']
    return total

print(f"Total a pagar: ${calcular_total(productos)}") # 1040
```


## Retos de Programación: Estructuras de Datos y Funciones

Pon a prueba tus conocimientos con estos 5 ejercicios diseñados para combinar colecciones y funciones.

### 1. Gestor de Inventario
**Objetivo**: Usar diccionarios y funciones.
Crea un programa que gestione el stock de una tienda. Usa un diccionario donde la clave es el nombre del producto y el valor es la cantidad.
Debes crear funciones para:
- agregar_producto(nombre, cantidad): Si existe, suma la cantidad; si no, lo crea.
- mostrar_inventario(): Imprime todos los productos y cantidades.

**Pista**: Usa .get() o verifica con in.

### 2. Análisis de Texto Único
**Objetivo**: Usar conjuntos y métodos de cadenas.
Escribe una función palabras_unicas(texto) que reciba un texto largo, lo convierta a minúsculas, elimine los signos de puntuación básicos y devuelva un conjunto con las palabras únicas presentes.

**Ejemplo**:
_Hola mundo, hola Python_ -> {'hola', 'mundo', 'python'}

### 3. Procesador de Notas
**Objetivo**: Listas de diccionarios y cálculos.
Tienes una lista de estudiantes con sus respectivas notas.
`python
estudiantes = [
    {'nombre': 'Ana', 'notas': [4.5, 3.8, 4.2]},
    {'nombre': 'Luis', 'notas': [2.5, 3.0, 2.8]}
]
`
Crea una función que recorra la lista y devuelva un nuevo diccionario donde la clave es el nombre del estudiante y el valor es el promedio de sus notas.

### 4. Filtro de Contactos
**Objetivo**: Tuplas y listas.
Dada una lista de tuplas (Nombre, Teléfono), crea una función filtrar_por_prefijo(lista, prefijo) que devuelva una nueva lista con los contactos cuyo teléfono empiece por ese prefijo.

`python
contactos = [('Pedro', '300-123'), ('Ana', '310-456'), ('Juan', '300-789')]
# filtrar_por_prefijo(contactos, '300') -> [('Pedro', '300-123'), ('Juan', '300-789')]
`

### 5. Recomendador de Películas
**Objetivo**: Operaciones de conjuntos.
Dos amigos tienen conjuntos de sus películas favoritas.
`python
amigo1 = {'Matrix', 'Avengers', 'Titanic'}
amigo2 = {'Avengers', 'Avatar', 'Titanic'}
`
Crea funciones para encontrar:
- **Coincidencias**: Películas que les gustan a ambos (Intersección).
- **Novedades para amigo1**: Películas que le gustan al amigo 2 pero que el amigo 1 no ha visto (Diferencia).

