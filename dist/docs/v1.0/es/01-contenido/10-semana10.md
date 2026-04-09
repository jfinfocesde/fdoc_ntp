---
title: "Semana 10: Localización de Datos con loc e iloc"
position: 10
draft: false
---

[Documentación Oficial de Pandas](https://pandas.pydata.org/docs/index.html) 

+++admonition
---
type: note
title: "Localizando Datos: El GPS de Pandas"
---
¡Bienvenido a la sesión sobre selección precisa! En la sesión anterior aprendiste a filtrar y limpiar datos. Ahora aprenderás a usar el "GPS" de Pandas: `loc` e `iloc`. Estas herramientas te permiten encontrar exactamente la fila y columna que necesitas, ya sea por su **nombre** o por su **posición numérica**.

Imagina que tu tabla de datos es un archivador gigante. `loc` es como buscar una carpeta por la **etiqueta** escrita en ella, mientras que `iloc` es como decir "tráeme la **tercera** carpeta del **segundo** cajón".
+++

---

##  Filtros `.loc` y `.iloc`


## Version Google Colab

Este tutorial se puede ejecutar en Google Colab. Para abrir el notebook en Colab, haz clic en el siguiente enlace:

[Abrir en Colab](https://colab.research.google.com/drive/17cFE9yLHrShL5w42Yt335ZDeQkf7AVFs?usp=sharing){target = "_blank"}


Pandas es una biblioteca de Python ampliamente utilizada para el análisis de datos. Los métodos **`.loc`** y **`.iloc`** permiten acceder a filas y columnas de un **DataFrame** de manera precisa. La principal diferencia entre ellos radica en cómo seleccionan los datos:

- **`.loc`**: Selecciona datos utilizando **etiquetas** (nombres de filas o columnas).
- **`.iloc`**: Selecciona datos utilizando **índices numéricos** (posiciones enteras).

Ambos métodos son muy flexibles y admiten selecciones de filas, columnas o subconjuntos de datos, ya sea individuales, rangos o listas específicas.

---


## **1. Preparación del entorno**

Antes de comenzar, asegúrate de tener instalada la biblioteca **Pandas**. Si no la tienes, instálala con:

```bash
pip install pandas
```

Carguemos un **DataFrame** de ejemplo para trabajar con él:

```python
import pandas as pd

# Crear un DataFrame de ejemplo
data = {
    'Nombre': ['Ana', 'Bob', 'Clara', 'David', 'Emma'],
    'Edad': [25, 30, 22, 35, 28],
    'Ciudad': ['Madrid', 'Barcelona', 'Sevilla', 'Valencia', 'Bilbao'],
    'Puntuación': [85, 90, 88, 92, 87]
}

df = pd.DataFrame(data, index=['a', 'b', 'c', 'd', 'e'])
print(df)
```

**Salida:**

```
   Nombre  Edad     Ciudad  Puntuación
a    Ana    25    Madrid          85
b    Bob    30 Barcelona          90
c  Clara    22   Sevilla          88
d  David    35  Valencia          92
e   Emma    28    Bilbao          87
```

Este **DataFrame** tiene:
- **Índices** de filas: `'a', 'b', 'c', 'd', 'e'`.
- **Columnas**: `'Nombre', 'Edad', 'Ciudad', 'Puntuación'`.

Ahora, usaremos este **DataFrame** para explorar **`.loc`** y **`.iloc`**.

---

## **2. Uso de `.loc`**

El método **`.loc`** se basa en **etiquetas** (nombres de filas y columnas). Su sintaxis general es:

```python
df.loc[filas, columnas]
```

Donde:
- `filas`: Puede ser una etiqueta de índice, una lista de etiquetas, un rango de etiquetas (usando `:`) o una condición booleana.
- `columnas`: Puede ser una etiqueta de columna, una lista de etiquetas o un rango de etiquetas.

### **2.1. Seleccionar una sola fila por etiqueta**

```python
# Seleccionar la fila con índice 'b'
print(df.loc['b'])
```

**Salida:**

```
Nombre            Bob
Edad               30
Ciudad      Barcelona
Puntuación         90
Name: b, dtype: object
```

Esto devuelve una **Serie** con los valores de la fila `'b'`.

### **2.2. Seleccionar una celda específica**

Puedes especificar tanto la fila como la columna:

```python
# Seleccionar la edad de la fila 'c'
print(df.loc['c', 'Edad'])
```

**Salida:**

```
22
```

### **2.3. Seleccionar múltiples filas**

Puedes pasar una lista de etiquetas o un rango:

```python
# Seleccionar las filas 'a' y 'c'
print(df.loc[['a', 'c']])
```

**Salida:**

```
   Nombre  Edad   Ciudad  Puntuación
a    Ana    25  Madrid          85
c  Clara    22 Sevilla          88
```

Usando un rango:

```python
# Seleccionar filas desde 'a' hasta 'c' (inclusive)
print(df.loc['a':'c'])
```

**Salida:**

```
   Nombre  Edad     Ciudad  Puntuación
a    Ana    25    Madrid          85
b    Bob    30 Barcelona          90
c  Clara    22   Sevilla          88
```

**Nota**: En **`.loc`**, los rangos incluyen el valor final (a diferencia de los índices numéricos en Python).

### **2.4. Seleccionar columnas específicas**

Puedes seleccionar columnas específicas para una o más filas:

```python
# Seleccionar 'Nombre' y 'Edad' de la fila 'b'
print(df.loc['b', ['Nombre', 'Edad']])
```

**Salida:**

```
Nombre    Bob
Edad       30
Name: b, dtype: object
```

### **2.5. Seleccionar con condiciones booleanas**

**`.loc`** es muy poderoso para filtrar filas basadas en condiciones:

```python
# Seleccionar filas donde la edad sea mayor a 25
print(df.loc[df['Edad'] > 25])
```

**Salida:**

```
   Nombre  Edad     Ciudad  Puntuación
b    Bob    30 Barcelona          90
d  David    35  Valencia          92
e   Emma    28    Bilbao          87
```

Puedes combinar condiciones:

```python
# Seleccionar filas donde Edad > 25 y Puntuación >= 90
print(df.loc[(df['Edad'] > 25) & (df['Puntuación'] >= 90)])
```

**Salida:**

```
   Nombre  Edad     Ciudad  Puntuación
b    Bob    30 Barcelona          90
d  David    35  Valencia          92
```

### **2.6. Modificar datos con `.loc`**

**`.loc`** también permite modificar valores en el **DataFrame**:

```python
# Cambiar la puntuación de la fila 'a'
df.loc['a', 'Puntuación'] = 95
print(df.loc['a'])
```

**Salida:**

```
Nombre          Ana
Edad             25
Ciudad       Madrid
Puntuación       95
Name: a, dtype: object
```

---

## **3. Uso de `.iloc`**

El método **`.iloc`** se basa en **índices numéricos** (posiciones enteras). Su sintaxis es similar:

```python
df.iloc[filas, columnas]
```

Donde:
- `filas`: Posiciones de las filas (0, 1, 2, ...).
- `columnas`: Posiciones de las columnas (0, 1, 2, ...).

### **3.1. Seleccionar una sola fila por posición**

```python
# Seleccionar la fila en la posición 1 (segunda fila)
print(df.iloc[1])
```

**Salida:**

```
Nombre            Bob
Edad               30
Ciudad      Barcelona
Puntuación         90
Name: b, dtype: object
```

### **3.2. Seleccionar una celda específica**

```python
# Seleccionar la celda en la fila 2, columna 1 (Edad de Clara)
print(df.iloc[2, 1])
```

**Salida:**

```
22
```

### **3.3. Seleccionar múltiples filas**

Puedes usar listas o rangos de posiciones:

```python
# Seleccionar las filas en las posiciones 0 y 2
print(df.iloc[[0, 2]])
```

**Salida:**

```
   Nombre  Edad   Ciudad  Puntuación
a    Ana    25  Madrid          95
c  Clara    22 Sevilla          88
```

Usando un rango:

```python
# Seleccionar filas desde la posición 0 hasta la 2 (excluye la 2)
print(df.iloc[0:2])
```

**Salida:**

```
  Nombre  Edad     Ciudad  Puntuación
a   Ana    25    Madrid          95
b   Bob    30 Barcelona          90
```

**Nota**: A diferencia de **`.loc`**, los rangos en **`.iloc`** excluyen el valor final, como es habitual en Python.

### **3.4. Seleccionar columnas específicas**

```python
# Seleccionar las columnas en las posiciones 0 y 2 para la fila 1
print(df.iloc[1, [0, 2]])
```

**Salida:**

```
Nombre          Bob
Ciudad    Barcelona
Name: b, dtype: object
```

### **3.5. Seleccionar un subconjunto de filas y columnas**

```python
# Seleccionar las primeras 3 filas y las primeras 2 columnas
print(df.iloc[0:3, 0:2])
```

**Salida:**

```
   Nombre  Edad
a    Ana    25
b    Bob    30
c  Clara    22
```

### **3.6. Modificar datos con `.iloc`**

Al igual que **`.loc`**, puedes modificar valores:

```python
# Cambiar la edad en la fila 0
df.iloc[0, 1] = 26
print(df.iloc[0])
```

**Salida:**

```
Nombre          Ana
Edad             26
Ciudad       Madrid
Puntuación       95
Name: a, dtype: object
```

---

## **4. Diferencias clave entre `.loc` y `.iloc`**

| Característica             | `.loc`                              | `.iloc`                             |
|----------------------------|-------------------------------------|-------------------------------------|
| **Selección basada en**    | Etiquetas (nombres)                | Índices numéricos (posiciones)      |
| **Rangos**                | Incluye el valor final             | Excluye el valor final             |
| **Uso típico**             | Cuando conoces los nombres de filas/columnas | Cuando trabajas con posiciones      |
| **Condiciones booleanas**  | Compatible                        | No compatible                      |

---

## **5. Errores comunes y cómo evitarlos**

1. **Error de índice en `.loc`**:
   - Si usas una etiqueta que no existe, obtendrás un **KeyError**:
     ```python
     df.loc['z']  # Error: 'z' no es un índice
     ```
   - **Solución**: Verifica las etiquetas con `df.index` o `df.columns`.

2. **Error de índice en `.iloc`**:
   - Si usas un índice fuera de rango, obtendrás un **IndexError**:
     ```python
     df.iloc[10]  # Error: índice 10 no existe
     ```
   - **Solución**: Usa `df.shape` para conocer las dimensiones del **DataFrame**.

3. **Confundir `.loc` con `.iloc`**:
   - Usar etiquetas con **`.iloc`** o índices numéricos con **`.loc`** causará errores:
     ```python
     df.loc[0]    # Error si el índice no es 0
     df.iloc['a'] # Error: iloc no acepta etiquetas
     ```
   - **Solución**: Recuerda que **`.loc`** usa etiquetas y **`.iloc`** usa posiciones.

4. **Modificar vistas en lugar de copias**:
   - Al usar **`.loc`** o **`.iloc`** para seleccionar un subconjunto y modificarlo, puedes encontrarte con un **SettingWithCopyWarning** si no tienes cuidado:
     ```python
     subset = df.loc[df['Edad'] > 25]
     subset['Edad'] = 0  # Puede causar advertencia
     ```
   - **Solución**: Usa `.copy()` para crear una copia explícita:
     ```python
     subset = df.loc[df['Edad'] > 25].copy()
     subset['Edad'] = 0
     ```

---
