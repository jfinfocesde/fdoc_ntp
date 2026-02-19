---
title: "Cargar CSV y análisis básico"
position: 3
date: 2025-11-11
---

## Cargar archivos CSV

```python
import streamlit as st
import pandas as pd

st.title("Cargar y explorar CSV")

archivo = st.file_uploader("Selecciona un archivo CSV", type=["csv"])
if archivo is not None:
    df = pd.read_csv(archivo)
    st.write("Vista inicial", df.head())
    
    st.subheader("Tipos de datos")
    st.write(df.dtypes)

    st.subheader("Resumen numérico")
    st.write(df.describe())

    st.subheader("Distribución categórica")
    cols_cat = df.select_dtypes(include=["object", "category"]).columns
    for col in cols_cat:
        st.write(f"Distribución de {col}")
        st.write(df[col].value_counts())

    st.subheader("Transformaciones permitidas")
    # Convertir posibles columnas a category
    for col in cols_cat:
        df[col] = df[col].astype("category")
    
    # Parseo de fechas si hay columnas con 'fecha' en el nombre
    for col in df.columns:
        if "fecha" in col.lower():
            df[col] = pd.to_datetime(df[col], errors="coerce")
    
    st.success("Transformaciones aplicadas según contenidos básicos")
```

Nota: Este análisis se basa en los conceptos del documento de tipos de variables (numéricas, categóricas, fechas, texto, booleanas).