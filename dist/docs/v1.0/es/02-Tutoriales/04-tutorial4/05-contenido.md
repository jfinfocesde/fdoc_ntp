---
title: "Aplicación multipágina con Streamlit"
position: 5
date: 2025-11-11
---

## ¿Qué es una app multipágina?

Permite organizar tu aplicación en varias páginas independientes (Exploración, Limpieza, Visualizaciones, etc.) usando la carpeta `pages/`. Streamlit detecta automáticamente los archivos dentro de `pages/` y muestra un selector de páginas sin que tengas que implementar rutas manuales.

## Estructura mínima

```bash
streamlit-app/
├── app.py               # Página principal (Home)
├── pages/               # Páginas adicionales
│   ├── 01_Exploracion.py
│   └── 02_Analisis.py
└── data/
    └── ejemplo.csv
```

Nota: El prefijo numérico (`01_`, `02_`) ordena las páginas en el menú.

## Página principal (`app.py`)

```python
import streamlit as st

st.set_page_config(page_title="Demo multipágina", layout="wide")

st.title("Home: Demo multipágina")
st.write("Usa el menú de páginas para navegar entre secciones.")

st.sidebar.success("Selecciona una página arriba para continuar.")
```

## Página de exploración (`pages/01_Exploracion.py`)

```python
import streamlit as st
import pandas as pd

st.title("Exploración de datos")

archivo = st.file_uploader("Sube un CSV", type=["csv"]) 
if archivo is not None:
    df = pd.read_csv(archivo)
    st.subheader("Vista inicial")
    st.dataframe(df.head())

    st.subheader("Tipos de datos")
    st.write(df.dtypes)

    st.subheader("Resumen numérico")
    st.write(df.describe(include="number"))

    st.subheader("Distribuciones categóricas")
    cat_cols = [c for c in df.columns if df[c].dtype == 'object']
    for c in cat_cols[:5]:
        st.write(f"Columna: {c}")
        st.write(df[c].value_counts().head(10))
else:
    st.info("Sube un archivo CSV para comenzar la exploración.")
```

## Página de análisis básico (`pages/02_Analisis.py`)

```python
import streamlit as st
import pandas as pd

st.title("Análisis básico")

archivo = st.file_uploader("Sube el mismo CSV de Exploración", type=["csv"]) 
if archivo is not None:
    df = pd.read_csv(archivo)

    st.subheader("Transformaciones permitidas")
    st.write("""
    - Manejo de faltantes: `dropna`, `fillna`
    - Conversión de tipos: `astype`
    - Filtrado por condiciones simples
    - Selección de columnas por tipo (numéricas o categóricas)
    """)

    # Ejemplo: convertir columnas numéricas a float
    num_cols = df.select_dtypes(include="number").columns
    df[num_cols] = df[num_cols].astype(float)

    st.subheader("Resumen por columna")
    resumen = {
        c: {
            "tipo": str(df[c].dtype),
            "nulos": int(df[c].isna().sum()),
            "unicos": int(df[c].nunique())
        }
        for c in df.columns
    }
    st.json(resumen)
else:
    st.info("Sube un archivo CSV para realizar análisis básico.")
```

## Ejecución

```bash
streamlit run app.py
```

## Buenas prácticas

- Usa `st.cache_data` para cachear lecturas de archivos y acelerar la experiencia.
- Reutiliza funciones de carga y validación entre páginas (por ejemplo, en un módulo `utils.py`).
- Mantén las transformaciones dentro del alcance de comprensión (limpieza ligera, tipos, faltantes) si tu objetivo es reporte de entendimiento.

## Referencia

Fuente: "Create a multipage app" — Documentación oficial de Streamlit
https://docs.streamlit.io/get-started/tutorials/create-a-multipage-app