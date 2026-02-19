---
title: "Semana 3 - Estructuras de Control y Ciclos"
description: "Domina el flujo de tu programa con condicionales y bucles en Python."
position: 3
---

Domina el arte de dirigir el flujo de ejecución de tus programas. En esta semana aprenderás a tomar decisiones lógicas y a repetir tareas de manera eficiente.

+++cards
---
columns: 2
items:
  - title: "Condicionales"
    icon: "GitBranchIcon"
    content: "Toma decisiones con if, elif, else y match."
    href: "#condicionales-toma-de-decisiones"
  - title: "Ciclos"
    icon: "RepeatIcon"
    content: "Automatiza tareas repetitivas con for y while."
    href: "#ciclos-repeticion-de-tareas"
  - title: "Control Avanzado"
    icon: "CpuIcon"
    content: "Domina break, continue y el uso de else en bucles."
    href: "#control-de-flujo-avanzado"
  - title: "Ejercicios Resueltos"
    icon: "CodeIcon"
    content: "Aprende con casos reales: Login, Carrito, y más."
    href: "#ejercicios-resueltos-casos-del-mundo-real"
---
+++

## Condicionales: Toma de Decisiones

Las estructuras condicionales permiten que tu programa "razone" y ejecute diferentes bloques de código según se cumplan o no ciertas condiciones.

### El Bloque `if-elif-else`

La estructura fundamental para la toma de decisiones.

+++mermaid
graph TD
    A[Inicio] --> B{¿Condición?}
    B -->|Verdadero| C[Ejecutar Bloque A]
    B -->|Falso| D{¿Otra Condición?}
    D -->|Verdadero| E[Ejecutar Bloque B]
    D -->|Falso| F[Ejecutar Bloque Else]
    C --> G[Fin]
    E --> G
    F --> G
+++

#### Sintaxis y Ejemplo

```python
nota = 85

if nota >= 90:
    print("Excelente: Tu nota es A")
elif nota >= 70:
    print("Aprobado: Tu nota es B")
else:
    print("Reprobado: Debes estudiar más")
```

+++admonition
---
type: warning
title: "Cuidado con la Indentación"
---
Python utiliza la indentación (sangría) para definir bloques de código. Si no indentas correctamente las líneas dentro de un `if` o `else`, obtendrás un `IndentationError`.
+++

### Match-Case (Python 3.10+)

Una alternativa elegante a múltiples `if-elif` cuando comparas una misma variable contra varios valores posibles.

```tabs
---[tab title="Python (Match)" lang="python"]---
status = 404

match status:
    case 200:
        print("Éxito: Solicitud completada")
    case 400:
        print("Error: Solicitud incorrecta")
    case 404:
        print("Error: No encontrado")
    case _:
        print("Error desconocido")

---[tab title="Equivalente If-Elif" lang="python"]---
status = 404

if status == 200:
    print("Éxito: Solicitud completada")
elif status == 400:
    print("Error: Solicitud incorrecta")
elif status == 404:
    print("Error: No encontrado")
else:
    print("Error desconocido")
```

---

## Ciclos: Repetición de Tareas

Los ciclos te permiten ejecutar un bloque de código múltiples veces, ahorrando tiempo y líneas de código.

### Comparativa: For vs While

+++comparison-table
---
headers:
  - "Característica"
  - { text: "Ciclo For", highlight: true }
  - "Ciclo While"
rows:
  - ["Uso Principal", "Iterar sobre secuencias (listas, rangos)", "Repetir mientras una condición sea verdad"]
  - ["Riesgo de Bucle Infinito", "Bajo (termina al acabar la secuencia)", "Alto (si no se actualiza la condición)"]
  - ["Conocimiento de Iteraciones", "Se sabe de antemano (o es finito)", "Puede ser indeterminado"]
---
+++

### El Ciclo `for`

Ideal para recorrer elementos de una colección o ejecutar código un número determinado de veces.

+++steps
### 1. Definir el Iterable
El ciclo necesita algo sobre lo que iterar, como una lista `[1, 2, 3]` o un rango `range(5)`.

### 2. Asignar la Variable
En cada vuelta, el valor actual se asigna a una variable temporal (ej. `for numero in numeros:`).

### 3. Ejecutar el Bloque
El código indentado se ejecuta para ese valor específico.

### 4. Repetir
El proceso se repite hasta que se agotan los elementos del iterable.
+++

#### Ejemplos Prácticos

**Recorriendo un rango y una lista:**

```python
# Rango del 0 al 4
print("--- Range ---")
for i in range(5):
    print(f"Iteración {i}")

# Recorriendo una lista de frutas
print("\n--- Lista ---")
frutas = ["Manzana", "Banano", "Cereza"]
for fruta in frutas:
    print(f"Me gusta la {fruta}")
```

**Iteración avanzada con `enumerate` y `zip`:**

```python
nombres = ["Ana", "Luis"]
edades = [25, 30]

# Zip une dos listas
for nombre, edad in zip(nombres, edades):
    print(f"{nombre} tiene {edad} años")
```

### El Ciclo `while`

Ejecuta código *mientras* una condición sea verdadera. Es poderoso pero requiere cuidado.

```python
contador = 5

while contador > 0:
    print(f"Cuenta regresiva: {contador}")
    contador -= 1  # ¡Importante! Modificar la condición
print("¡Despegue!")
```

---

## Control de Flujo Avanzado

A veces necesitas alterar el comportamiento normal de un ciclo.

### Break, Continue y Else

| Palabra Clave | Función |
|---------------|---------|
| **break** | Rompe el ciclo inmediatamente y sale de él. |
| **continue** | Salta el resto del código actual y pasa a la siguiente iteración. |
| **else** | Se ejecuta al finalizar el ciclo *si y solo si* no se usó `break`. |

#### Ejemplo Visual de Break/Continue

+++mermaid
graph LR
    A[Inicio Ciclo] --> B{Condición}
    B -->|True| C{¿Es caso especial?}
    C -->|Break| F[Salir del Ciclo]
    C -->|Continue| A
    C -->|Normal| D[Ejecutar Código]
    D --> A
    B -->|False| E[Bloque Else]
    E --> F
+++

#### Ejemplo de Código

```python
for numero in range(10):
    if numero == 5:
        print("Rompiendo el ciclo en 5")
        break  # Sale completamente
    if numero % 2 == 0:
        continue  # Salta los pares (no imprime)
    print(f"Número impar procesado: {numero}")
```

---

## Mejores Prácticas

+++admonition
---
type: tip
title: "Consejos de Experto"
---
1. **Evita bucles infinitos**: Asegúrate siempre de que tu `while` tenga una condición que eventualmente sea falsa.
2. **Prefiere `for` sobre `while`**: Si sabes cuántas veces vas a iterar, `for` es más seguro y legible.
3. **Nombres descriptivos**: Usa `for estudiante in estudiantes` en lugar de `for x in y` para mejorar la legibilidad.
+++

---

## Ejercicios Resueltos: Casos del Mundo Real

Aprende analizando cómo se aplican las estructuras de control en situaciones de la vida real.

### Caso 1: Sistema de Autenticación (Login)

**Conceptos**: `while`, `input`, `if-else`, `break`, contadores.

Simulamos un sistema de inicio de sesión que permite un máximo de 3 intentos antes de bloquear al usuario.

```python
intentos_maximos = 3
intentos = 0
contrasena_correcta = "python123"

print("--- Sistema de Login ---")

while intentos < intentos_maximos:
    contrasena = input("Ingrese su contraseña: ")
    
    if contrasena == contrasena_correcta:
        print("¡Acceso concedido! Bienvenido al sistema.")
        break  # Importante: Salir del ciclo si la contraseña es correcta
    else:
        intentos += 1
        restantes = intentos_maximos - intentos
        print(f"Contraseña incorrecta. Te quedan {restantes} intentos.")

if intentos == intentos_maximos:
    print("¡Cuenta bloqueada por seguridad!")
```

### Caso 2: Carrito de Compras Inteligente

**Conceptos**: `for`, diccionarios, acumuladores, lógica aritmética.

Calcula el total de una compra, aplicando un descuento del 10% si el subtotal supera los $100.

```python
carrito = [
    {"producto": "Camisa", "precio": 25.00},
    {"producto": "Pantalón", "precio": 45.50},
    {"producto": "Zapatos", "precio": 60.00}
]

subtotal = 0

print(f"{'Producto':<15} | {'Precio':>8}")
print("-" * 26)

for item in carrito:
    print(f"{item['producto']:<15} | ${item['precio']:>8.2f}")
    subtotal += item['precio']

print("-" * 26)
print(f"Subtotal:       ${subtotal:>8.2f}")

# Aplicar descuento si corresponde
if subtotal > 100:
    descuento = subtotal * 0.10
    total = subtotal - descuento
    print(f"Descuento (10%): -${descuento:>8.2f}")
else:
    total = subtotal
    print("Descuento:      $    0.00")

print("=" * 26)
print(f"Total a Pagar:  ${total:>8.2f}")
```

### Caso 3: Analizador de Calificaciones

**Conceptos**: Iteración de listas, filtrado con `if`, `f-strings`.

Dada una lista de estudiantes y sus notas, queremos saber quiénes aprobaron (nota >= 3.0) y quiénes no.

```python
estudiantes = {
    "Ana": 4.5,
    "Carlos": 2.8,
    "Beatriz": 3.9,
    "David": 1.5
}

aprobados = []
reprobados = []

for nombre, nota in estudiantes.items():
    if nota >= 3.0:
        aprobados.append(nombre)
    else:
        reprobados.append(nombre)

print(f"Estudiantes que aprobaron ({len(aprobados)}): {', '.join(aprobados)}")
print(f"Estudiantes que reprobaron ({len(reprobados)}): {', '.join(reprobados)}")
```

### Caso 4: Menú Interactivo (Cajero Automático)

**Conceptos**: `while True`, `match-case` (o `if-elif`), interacción continua.

Un menú que no termina hasta que el usuario elige "Salir".

```python
saldo = 1000

while True:
    print("\n--- CAJERO AUTOMÁTICO ---")
    print("1. Consultar Saldo")
    print("2. Retirar Dinero")
    print("3. Salir")
    
    opcion = input("Seleccione una opción: ")
    
    match opcion:
        case "1":
            print(f"Su saldo actual es: ${saldo}")
        case "2":
            retiro = float(input("¿Cuánto desea retirar? "))
            if retiro > saldo:
                print("Fondos insuficientes.")
            elif retiro <= 0:
                print("Cantidad no válida.")
            else:
                saldo -= retiro
                print(f"Retiro exitoso. Nuevo saldo: ${saldo}")
        case "3":
            print("Gracias por usar nuestro servicio. ¡Adiós!")
            break  # Rompe el while True
        case _:
            print("Opción no válida. Intente de nuevo.")
```

---
# Semana 4 - Estructuras de Datos y Funciones

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
