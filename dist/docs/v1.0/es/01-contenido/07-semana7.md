---
title: "Semana 7: Carga de Datos en Pandas"
position: 7
---

[Documentación Oficial de Pandas](https://pandas.pydata.org/docs/index.html) 

+++admonition
---
type: note
title: "¡Bienvenido al mundo de la Ciencia de Datos!"
---
En esta sesión, daremos nuestros primeros pasos con una de las herramientas más importantes y utilizadas en Python para el análisis de datos: **Pandas**. No te preocupes si nunca antes has analizado datos, aquí lo explicaremos paso a paso, con un lenguaje muy claro y lleno de ejemplos prácticos.
+++

Pandas es una **biblioteca** (un conjunto de herramientas ya programadas) de software libre, creada específicamente para el análisis de datos y la manipulación de estructuras de información en Python. Es muy popular entre científicos de datos, analistas y cualquier persona que necesite trabajar con grandes cantidades de información (como archivos de Excel gigantes, bases de datos, etc.).

Piensa en Pandas como un "Excel supervitaminado", donde en lugar de hacer clics con el ratón, utilizas código Python para ordenar, filtrar, analizar y transformar tus datos a una velocidad increíble.

## ¿Qué nos ofrece Pandas?

- **Estructuras de datos potentes:** Pandas nos da dos "contenedores" principales para guardar nuestra información: las **Series** (que son como una sola columna de datos) y los **DataFrames** (que son como una tabla completa con filas y columnas).
- **Una enorme caja de herramientas:** Podrás limpiar datos desordenados, calcular promedios, buscar tendencias, o conectar tus datos con herramientas de visualización (para hacer gráficos).
- **Facilidad de uso:** Aunque al principio usar código parece difícil, Pandas tiene instrucciones muy lógicas y parecidas a cómo hablamos, lo que lo hace ideal para principiantes.

## Instalación de Pandas

Antes de poder usar Pandas en nuestro código Python, necesitamos instalarlo en nuestra computadora. 

+++steps
### Paso 1: Abrir la terminal
Abre tu consola de comandos (Command Prompt en Windows, Terminal en macOS o Linux).

### Paso 2: Ejecutar el comando de instalación
Escribe el comando de instalación de Python y presiona Enter.

### Paso 3: Esperar la descarga
Verás una barra de progreso. Una vez que termine, Pandas estará listo para usarse.
+++

Aquí tienes el código exacto que debes escribir en tu terminal:

```bash
pip install pandas
```

+++admonition
---
type: tip
title: "¿Problemas con la instalación?"
---
Si te aparece un error diciendo que "pip no se reconoce", asegúrate de haber marcado la opción "Add Python to PATH" cuando instalaste Python en tu computadora.
+++

---

## Estructuras de Datos Principales

Para trabajar con Pandas, debemos entender sus dos piezas fundamentales. Imagina que vas a construir un edificio de legos; primero necesitas conocer las piezas individuales antes de armar una casa completa.

### 1. Las Series en Pandas

Una **Serie** es una estructura de datos unidimensional. En español sencillo: es como una lista sencilla o **una sola columna** de datos en un Excel.

**Características principales de una Serie:**
- **Almacenan cualquier dato:** Pueden guardar números, nombres (texto), fechas, o respuestas lógicas (Verdadero/Falso).
- **Tienen un Índice:** Es decir, cada dato tiene una "etiqueta" o "dirección". Por defecto son números (0, 1, 2, 3...), así puedes pedirle a Pandas "dame el dato número 2".
- **Son ordenables y operables:** Puedes ordenarlas de mayor a menor y puedes sumarles valores matemáticos a toda la lista de un solo golpe.

**Ejemplo de una Serie:**

Imagina que queremos guardar las temperaturas de una ciudad durante la semana.

```python  
# Siempre debemos importar la biblioteca antes de usarla.
# Se usa 'pd' como un apodo corto por convención mundial.
import pandas as pd

# Creamos una Serie pasando una lista de números de Python
temperaturas = pd.Series([20, 25, 30, 22, 28])

# Mostrar toda la serie
print("Temperaturas de la semana:")
print(temperaturas)

# Mostrar solo la temperatura que está en el índice 2 (recuerda que se cuenta desde 0)
print("\nLa temperatura en el índice 2 es:", temperaturas[2])

# Pandas puede hacer matemáticas por nosotros muy rápido
print("\nLa temperatura promedio fue:", temperaturas.mean())

# Podemos ordenar los valores de menor a mayor
print("\nTemperaturas ordenadas de menor a mayor:")
print(temperaturas.sort_values())
```

### 2. Los DataFrames en Pandas

![Visualización de un DataFrame](https://pandas.pydata.org/docs/_images/01_table_dataframe.svg)

Un **DataFrame** es una estructura de datos bidimensional. En palabras sencillas: **es una tabla completa**, exactamente igual a una hoja de cálculo, con sus columnas y sus filas.

**Características de un DataFrame:**
- **Variedad de columnas:** Una columna puede tener nombres (texto) y la de al lado edades (números enteros), y otra precios (números con decimales).
- **Tienen índices para filas (dirección vertical):** Cada fila tiene un número o nombre para identificar ese registro.
- **Tienen nombres en las columnas (dirección horizontal):** Como "Nombre", "Edad", "Ciudad", para saber qué dato estamos viendo.

**Ejemplo de un DataFrame:**

Vamos a crear una pequeña libreta de contactos.

```python  
import pandas as pd

# Primero creamos un "diccionario" en Python con la información
datos = {
    "Nombre": ["Pedro", "María", "Juan", "Laura"],
    "Edad": [20, 25, 30, 22],
    "Ciudad": ["Medellín", "Bogotá", "Cali", "Barranquilla"]
}

# Convertimos ese diccionario en un DataFrame mágico de Pandas
df = pd.DataFrame(datos)

# Veamos cómo se ve nuestra tabla
print("Nuestra tabla de contactos:")
print(df)
```


### Relación entre Series y DataFrames

- Si tomas **un DataFrame (una tabla)** y le arrancas una sola columna, lo que te queda en la mano es una **Serie**.
- Si tomas varias **Series** y las pegas una al lado de la otra, construyes un **DataFrame**.

+++admonition
---
type: info
title: "Resumen Visual"
---
Puedes pensar en una Serie como un simple tren de un solo vagón con asientos numerados. Un DataFrame sería todo un estacionamiento de trenes, ordenados uno al lado del otro, formando una cuadrícula gigante.
+++

### Comparativa: Series vs DataFrames

| Característica | Series (Serie) | DataFrame (Tabla) |
|--------------|----------------|-------------------|
| **Dimensión** | Una dimensión (como una sola columna) | Dos dimensiones (como una hoja de finanzas) |
| **Índice** | Un solo índice (vertical que etiqueta elementos) | Índices de filas (vertical) y columnas (horizontal) |
| **Tipos de datos** | Solo un tipo de dato (o todos números, o todo texto) | Diferentes tipos (columna 1 texto, columna 2 números) |
| **Analogía** | Una lista del mercado | Una hoja completa de cálculo |

---

## ¿Cómo crear un DataFrame desde cero?

Uno de los superpoderes de Pandas es que puede construir "hojas de cálculo" (DataFrames) a partir de casi cualquier parte. Puede leer desde variables de Python, hasta bases de datos complejas en internet.

A continuación, daremos múltiples ejemplos muy detallados para principiantes.

### Método 1: Juntando varias Series

Podemos fabricar y luego unir distintas columnas para construir la tabla final.

```python
import pandas as pd

# 1. Creamos nuestras columnas separadas (Series)
nombres = pd.Series(['Alicia', 'Bob', 'Carlos'])
edades = pd.Series([25, 30, 28])
ciudades = pd.Series(['Nueva York', 'Londres', 'París'])

# 2. Las juntamos todas dándole un nombre a cada columna
mi_dataframe = pd.DataFrame({
    'Nombre del Cliente': nombres, 
    'Años': edades, 
    'Lugar de Residencia': ciudades
})

# 3. Imprimimos el resultado
print(mi_dataframe)
```


### Método 2: Desde una Lista de Listas

También podemos verlo como una cuadrícula donde cada pequeña lista representa una fila de nuestra tabla final.

```python
import pandas as pd

# Cada paréntesis cuadrado interno es una fila de datos
datos_en_filas = [
    ["Ana", 25, "Madrid"],       # Fila 1
    ["Juan", 30, "Barcelona"],   # Fila 2
    ["Pedro", 35, "Sevilla"]     # Fila 3
]

# Al crearlo, le decimos específicamente cómo queremos que se llamen las columnas
df = pd.DataFrame(datos_en_filas, columns=["Nombre", "Edad", "Ciudad"])

print(df)
```

---

## Cargando archivos reales a Pandas

En la vida real, los científicos de datos casi nunca escriben los datos a mano. En lugar de eso, abren archivos gigantes que vienen de empresas, sensores o páginas web.

### 1. Desde un archivo CSV y URL

Los archivos `.csv` (Valores Separados por Comas) son el estándar mundial para compartir tablas de datos. Abrir un CSV en Pandas toma apenas una línea de código.

```tabs
---[tab title="Desde archivo local" lang="python"]---
import pandas as pd

# Leemos un archivo que esté en nuestra computadora
try:
    df_local = pd.read_csv("mi_archivo_data.csv")
    print(df_local.head()) # .head() muestra solo las primeras 5 líneas
except FileNotFoundError:
    print("Por favor asegúrate de que el archivo exista en la misma carpeta.")

---[tab title="Desde internet (URL)" lang="python"]---
import pandas as pd

# Podemos pasarle directamente un enlace de internet a Pandas
url = "https://raw.githubusercontent.com/datasets/data/master/people.csv"
df_internet = pd.read_csv(url)

# Le pedimos que nos enseñe cómo quedó
print(df_internet.head())
```

+++admonition
---
type: warning
title: "Nota sobre la lectura desde URL"
---
Para leer un CSV de internet usando una URL con `pd.read_csv`, tu computadora necesita estar conectada a internet y el enlace debe apuntar hacia el archivo en formato "texto crudo" (Raw).
+++

### 2. Desde un archivo de Excel

Muchos datos empresariales están en archivos Excel (`.xlsx`). Pandas también puede leerlos mágicamente.

```python
import pandas as pd

# Nota: Para leer Excel es posible que necesites instalar una librería extra:
# pip install openpyxl

# Cargamos nuestro excel
df_excel = pd.read_excel("reporte_ventas.xlsx")

print("Datos extraídos de Excel:")
print(df_excel)
```

### 3. Desde un archivo JSON

JSON es un formato muy usado por programadores web para enviar información. Parece un diccionario de Python.

**Imagina que tienes este archivo llamado `empleados.json`:**
```json
[
  { "Nombre": "Ana", "Edad": 25, "Ciudad": "Madrid" },
  { "Nombre": "Juan", "Edad": 30, "Ciudad": "Barcelona" }
]
```

**Para cargarlo en Pandas:**

```python
import pandas as pd

# Leer el formato JSON es igual de simple
df_json = pd.read_json("empleados.json")

print("\nNuestra tabla desde un JSON:")
print(df_json)
```

---

## Conexiones Avanzadas: Bases de Datos y APIs

Cuando empieces a trabajar en proyectos corporativos, te encontrarás con que la información vive en "Bases de Datos" o servidores web. ¡Pandas también puede hablar con ellos!

### Conectando a una API REST

Una API es una forma en la cual las computadoras se mandan mensajes por internet. Podemos preguntarle a una API por datos (como el clima, usuarios, precios de acciones) y convertir esa respuesta en una tabla.

```python
import pandas as pd
import requests # Ayuda a hablar con servidores en internet

# 1. Le pedimos datos a una página web de prueba (Mockoon)
url_api = 'https://playground.mockoon.com/users'
respuesta = requests.get(url_api)

# 2. Verificamos si el servidor contestó bien (código 200 significa "Todo en orden")
if respuesta.status_code == 200:
    # 3. Extraemos el mensaje (datos)
    datos_crudos = respuesta.json()
    
    # 4. Construimos nuestro DataFrame de Pandas!
    df_usuarios = pd.DataFrame(datos_crudos)
    
    print("Exclusiva: Tenemos los datos de los usuarios!")
    print(df_usuarios.head(3)) # Mostramos solo los primeros tres
else:
    print(f"Uy! Hubo un error, el servidor contestó: {respuesta.status_code}") 
```

### Bases de Datos en la Nube: MongoDB y Firebase

Si los datos están protegidos en colecciones en la nube, debes usar las llaves de seguridad de la base de datos y primero extraer los datos en Python en forma de lista, y finalmente, entregarle esa lista a Pandas.

```tabs
---[tab title="Ejemplo con MongoDB" lang="python"]---
# Requiere instalación previa: pip install pymongo pandas
import pandas as pd
from pymongo import MongoClient

# 1. Te conectas con tu usuario y contraseña
cliente = MongoClient('mongodb+srv://tu_usuario:tu_clave@cluster.mongodb.net') 

# 2. Eliges qué cajón revisar
base_datos = cliente["dbTest"]
coleccion = base_datos["user"]

# 3. Pandas convierte los documentos a Tabla automáticamente
df_mongo = pd.DataFrame(list(coleccion.find()))
print(df_mongo)

---[tab title="Ejemplo con Firebase" lang="python"]---
# Requiere instalación previa: pip install firebase-admin pandas
import pandas as pd
import firebase_admin
from firebase_admin import credentials, firestore

# 1. Usas tu archivo secreto de seguridad ('key.json')
credenciales = credentials.Certificate('key.json')
firebase_admin.initialize_app(credenciales)
bd_firestore = firestore.client()

# 2. Traes todos los datos que hay en 'users'
usuarios_documentos = bd_firestore.collection('user').stream()

# 3. Agrupas los datos en una lista usando un bucle corto (List Comprehension)
datos_lista = [documento.to_dict() for documento in usuarios_documentos]

# 4. Magia de Pandas
df_firebase = pd.DataFrame(datos_lista)
print(df_firebase)
```

+++admonition
---
type: success
title: "¡Gran progreso!"
---
Has aprendido qué es Pandas, cuáles son sus piezas principales (Series y DataFrames) y todas las formas imaginables de crear tus tablas de datos, desde escribirlas a mano hasta bajarlas de la nube. Estás completamente preparado para empezar a limpiar y analizar datos en el mundo real.
+++
