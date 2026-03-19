---
title: "Semana 8: Análisis Exploratorio de Datos (EDA)"
position: 8
---

[Documentación Oficial de Pandas](https://pandas.pydata.org/docs/index.html) 

+++admonition
---
type: note
title: "¡Bienvenido al mundo del Análisis de Datos!"
---
En esta sesión, profundizaremos en el **Análisis Exploratorio de Datos (EDA)**. El EDA no se trata de cambiar los datos, sino de **entenderlos profundamente**. Aprenderás a inspeccionar la estructura, los tipos de información y las estadísticas clave para descubrir qué historias esconden tus tablas sin modificar ni una sola fila.
+++

Pandas es nuestra herramienta principal para este trabajo. Es una **biblioteca** de Python diseñada para manipular y analizar datos de forma rápida y sencilla.

---

## ¿Qué es el EDA?

El **Análisis Exploratorio de Datos (EDA)** es la fase de **descubrimiento**. Es el proceso de analizar conjuntos de datos para resumir sus características principales. Imagina que eres un investigador que acaba de encontrar un manuscrito antiguo:
1. No empiezas a corregir el texto ni a borrar palabras (eso es limpieza).
2. Primero observas cuántas páginas tiene (estructura).
3. Miras en qué idioma está escrito (tipos de datos).
4. Cuentas cuántas veces aparecen ciertos nombres (frecuencias).
5. Buscas si hay dibujos relacionados con el texto (relaciones).

**Eso es el EDA:** una observación pura y detallada para entender la naturaleza de la información antes de tomar cualquier decisión.

---

## Inspección Estructural: "Conociendo el Terreno"

Antes de analizar los números, debemos entender cómo está construida nuestra tabla.

### 1. Vistazo Rápido
- `df.head(n)`: Muestra las primeras `n` filas. Es vital para ver si los datos cargaron como esperábamos.
- `df.tail(n)`: Muestra las últimas `n` filas (útil para detectar si el archivo se cortó al final).
- `df.sample(n)`: Muestra una muestra aleatoria. A veces los datos están ordenados y el principio no representa la realidad; `sample` nos da una visión más imparcial.

### 2. Metadatos y Memoria
- `df.info()`: El resumen definitivo. Muestra el número de filas, columnas, nombres y si hay valores faltantes.
- `df.dtypes`: Lista específicamente qué tipo de dato hay en cada columna (números, texto, fechas).
- `df.shape`: Nos da las dimensiones exactas (Filas, Columnas).

---

## Sondeo de Categorías y Frecuencias

Para las columnas que no son números (como nombres de ciudades o categorías), usamos estas herramientas:

- `df['Columna'].unique()`: Lista todos los valores diferentes que existen en esa columna sin repetirlos.
- `df['Columna'].nunique()`: Nos da el **número total** de valores únicos.
- `df['Columna'].value_counts()`: Cuenta cuántas veces aparece cada valor. Es fundamental para saber qué categorías son las más dominantes.

---

## Análisis Estadístico y Relaciones

Aquí es donde los números empiezan a hablar por sí solos.

### 1. Estadísticas Descriptivas
El comando `df.describe()` nos entrega el perfil numérico de la tabla:
- **Media y Mediana:** Para entender el centro de los datos.
- **Desviación Estándar:** Para saber qué tan variados son los valores.
- **Mínimo y Máximo:** Para detectar los límites (y posibles valores extremadamente raros).

### 2. Relaciones entre Variables
- `df.corr()`: Calcula la **correlación**. Nos dice si dos columnas numéricas se mueven juntas. Por ejemplo, si al aumentar el "Precio" también suelen aumentar las "Ventas", o si no tienen ninguna relación entre sí.

---

## Ejemplo Práctico: Observación Pura de una Tienda

En este ejercicio no filtraremos ni cambiaremos nada. Simplemente observaremos la tabla para extraer conclusiones.

```python
import pandas as pd

# Datos de ventas simulados (Observación pura)
datos = {
    "Producto": ["Laptop", "Mouse", "Monitor", "Laptop", "Teclado", "Monitor", "Mouse"],
    "Categoria": ["Electronica", "Accesorios", "Electronica", "Electronica", "Accesorios", "Electronica", "Accesorios"],
    "Precio": [1200, 25, 300, 1200, 45, 300, 25],
    "Unidades_Vendidas": [5, 50, 12, 4, 35, 15, 60]
}
df = pd.DataFrame(datos)

# --- INICIAMOS EL ANÁLISIS OBSERVACIONAL ---

# A. ¿Cuál es la estructura de mi inventario?
print("Tipos de datos detectados:")
print(df.dtypes)

# B. ¿Qué categorías tenemos y qué tanto se repiten?
print("\nDistribución por categoría:")
print(df["Categoria"].value_counts())

# C. Resumen estadístico de precios y ventas
print("\nPerfil estadístico del negocio:")
print(df.describe())

# D. Agrupación descriptiva (Sin filtrar)
# ¿Cómo se comportan los ingresos promedio por categoría?
df['Ingreso_Estimado'] = df['Precio'] * df['Unidades_Vendidas']
print("\nIngreso promedio por categoría:")
print(df.groupby('Categoria')['Ingreso_Estimado'].mean())

# E. Relación entre precio y unidades vendidas
# ¿Los productos más caros se venden menos?
print("\nCorrelación Precio vs Unidades:")
print(df[['Precio', 'Unidades_Vendidas']].corr())
```

---

## Conclusión

El EDA es el arte de la **contemplación analítica**. Un buen científico de datos pasa la mayor parte de su tiempo inspeccionando dtypes, revisando informes de `describe()` y entendiendo las frecuencias de `value_counts()`. Antes de intentar manipular los datos, asegúrate de haberlos escuchado con atención.



## 🚀 Actividad Práctica: Tu primer EDA Real

Para cerrar esta sesión, es momento de que pongas en práctica tu curiosidad sobre un conjunto de datos del mundo real. 

#### **Instrucciones:**

1.  **Selecciona una fuente:** Visita uno de estos portales de datos abiertos de Medellín:
    - [Medata](https://medata.gov.co/)
    - [Datos Abiertos Colombia](https://www.datos.gov.co/)
2.  **Descarga un Dataset:** Busca un tema que te interese (movilidad, salud, medio ambiente) y descarga el archivo en formato **CSV**.
3.  **Carga y Observa:** Usa Jupyter o Google Colab para cargar el archivo y aplica las herramientas de esta sesión:
    - Usa `info()` y `dtypes` para ver la estructura.
    - Analiza una columna categórica con `value_counts()`.
    - Obtén el resumen estadístico con `describe()`.
    - Busca relaciones interesantes con `corr()`.

#### **Tu reto:**
Escribe **3 hallazgos** que te hayan sorprendido al observar los datos. Recuerda: **no limpies ni Filtres todavía**, solo observa lo que los datos tienen para decirte.


