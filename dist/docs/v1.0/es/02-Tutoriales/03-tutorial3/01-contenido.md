---
title: "Cargar Archivos CSV en Panda"
position: 1
date: 2025-10-28
---

## **Tutorial: Cargar Archivos CSV en Pandas**

Pandas es una biblioteca de Python ampliamente utilizada para el análisis de datos. Una de sus funciones más comunes es cargar archivos CSV (Comma-Separated Values) en un DataFrame. A continuación, se explican todas las formas de cargar archivos CSV, los problemas comunes que pueden surgir y cómo resolverlos.

---

### **1. Forma Básica de Cargar un Archivo CSV**

La función `pandas.read_csv()` es la herramienta principal para cargar archivos CSV en Pandas.

```python
import pandas as pd

# Cargar un archivo CSV básico
df = pd.read_csv("archivo.csv")
```

- **Descripción**: Lee el archivo CSV y lo convierte en un DataFrame de Pandas.
- **Nota**: El archivo debe estar en el mismo directorio que el script o notebook.

---

### **2. Especificar la Ruta del Archivo**

Si el archivo no está en el mismo directorio, debes proporcionar la ruta completa o relativa.

```python
# Ruta absoluta
df = pd.read_csv("/ruta/completa/al/archivo.csv")

# Ruta relativa
df = pd.read_csv("../datos/archivo.csv")
```

---

### **3. Cambiar el Delimitador con `sep`**

Por defecto, Pandas asume que el delimitador es una coma (`,`). Sin embargo, algunos archivos CSV usan otros delimitadores, como punto y coma (`;`), tabulación (`\t`) u otros caracteres.

#### **Ejemplo con Punto y Coma**
```python
df = pd.read_csv("archivo.csv", sep=";")
```

#### **Ejemplo con Tabulación**
```python
df = pd.read_csv("archivo.tsv", sep="\t")  # También puedes usar delimiter="\t"
```

#### **Ejemplo con Pipe (`|`)**
```python
df = pd.read_csv("archivo.csv", sep="|")
```

---

### **4. Manejo de Codificaciones**

Algunos archivos CSV no están codificados en UTF-8, lo que puede causar errores al leerlos.

#### **Problema Común**
```bash
UnicodeDecodeError: 'utf-8' codec can't decode byte...
```

#### **Solución**
Especifica la codificación correcta usando el parámetro `encoding`.

```python
# Usando codificación ISO-8859-1 (común en archivos de Windows)
df = pd.read_csv("archivo.csv", encoding="ISO-8859-1")

# Usando codificación UTF-8
df = pd.read_csv("archivo.csv", encoding="utf-8")
```

---

### **5. Saltar Filas Innecesarias**

Si el archivo tiene filas innecesarias al inicio o si las columnas no tienen nombres claros, puedes ajustar esto.

#### **Saltar Filas**
```python
# Saltar las primeras 2 filas
df = pd.read_csv("archivo.csv", skiprows=2)
```

#### **Usar una Fila Específica como Cabecera**
```python
# Usar la fila 3 como cabecera (índice 2)
df = pd.read_csv("archivo.csv", header=2)
```

---

### **6. Manejo de Valores Faltantes**

Pandas reemplaza automáticamente valores faltantes por `NaN`. Si el archivo usa otro valor para representar datos faltantes, puedes especificarlo.

```python
# Reemplazar "NA" y "?" con NaN
df = pd.read_csv("archivo.csv", na_values=["NA", "?"])
```

---

### **7. Leer Sólo Ciertas Columnas**

Si solo necesitas ciertas columnas, puedes especificarlas para ahorrar memoria.

```python
# Leer solo las columnas "nombre" y "edad"
df = pd.read_csv("archivo.csv", usecols=["nombre", "edad"])
```

---

### **8. Leer Sólo Cierto Número de Filas**

Para archivos grandes, puedes limitar el número de filas a leer.

```python
# Leer las primeras 100 filas
df = pd.read_csv("archivo.csv", nrows=100)
```

---

### **9. Parsear Fechas**

Si tu archivo contiene columnas con fechas, puedes parsearlas automáticamente.

```python
# Parsear la columna "fecha" como fecha
df = pd.read_csv("archivo.csv", parse_dates=["fecha"])
```

---

### **10. Leer Archivos Grandes en Fragmentos (Chunks)**

Para archivos muy grandes que no caben en memoria, puedes leerlos en fragmentos (chunks).

```python
# Leer el archivo en chunks de 1000 filas
chunk_size = 1000
chunks = []

for chunk in pd.read_csv("archivo_grande.csv", chunksize=chunk_size):
    chunks.append(chunk)

# Concatenar todos los chunks en un solo DataFrame
df = pd.concat(chunks)
```

---

### **11. Problemas Comunes y Soluciones**

#### **1. Error de Delimitador Incorrecto**
**Problema**: Los datos aparecen mal estructurados porque el delimitador no coincide.

**Solución**: Usa el parámetro `sep`.

```python
# Cambiar el delimitador
df = pd.read_csv("archivo.csv", sep=";")
```

#### **2. Error de Codificación**
**Problema**: El archivo no está codificado en UTF-8.

**Solución**: Usa el parámetro `encoding`.

```python
# Cambiar la codificación
df = pd.read_csv("archivo.csv", encoding="ISO-8859-1")
```

#### **3. Filas Innecesarias al Inicio**
**Problema**: Las primeras filas contienen metadatos o comentarios.

**Solución**: Usa el parámetro `skiprows`.

```python
# Saltar las primeras 3 filas
df = pd.read_csv("archivo.csv", skiprows=3)
```

#### **4. Datos Faltantes Representados por Otros Valores**
**Problema**: Los valores faltantes están representados por "NA", "-", etc.

**Solución**: Usa el parámetro `na_values`.

```python
# Reemplazar "NA" y "-" con NaN
df = pd.read_csv("archivo.csv", na_values=["NA", "-"])
```

#### **5. Archivo Muy Grande**
**Problema**: El archivo es demasiado grande para cargarlo completamente en memoria.

**Solución**: Usa el parámetro `chunksize`.

```python
# Leer en chunks
for chunk in pd.read_csv("archivo_grande.csv", chunksize=1000):
    print(chunk.head())
```

---

### **12. Ejemplo Completo**

Aquí tienes un ejemplo que combina varias opciones:

```python
import pandas as pd

# Cargar un archivo CSV con:
# - Delimitador personalizado
# - Codificación específica
# - Saltar filas innecesarias
# - Leer solo ciertas columnas
# - Parsear fechas
df = pd.read_csv(
    "archivo.csv",
    sep=";",
    encoding="ISO-8859-1",
    skiprows=2,
    usecols=["nombre", "edad", "fecha"],
    parse_dates=["fecha"]
)

print(df.head())
```


