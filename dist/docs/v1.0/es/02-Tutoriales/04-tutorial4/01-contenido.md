---
title: "Introducción a Streamlit"
position: 1
date: 2025-11-11
---

## ¿Qué es Streamlit?

Streamlit es un framework en Python que permite construir aplicaciones web de forma rápida para análisis de datos y machine learning, sin necesidad de escribir HTML/CSS/JS.

## Instalación

```bash
pip install streamlit
```

## Tu primera app

Crea un archivo `app.py`:

```python
import streamlit as st

st.title("Hola, Streamlit")
st.write("Esta es tu primera aplicación con Streamlit.")

st.header("Interactividad básica")
nombre = st.text_input("¿Cuál es tu nombre?")
if nombre:
    st.success(f"¡Bienvenido, {nombre}!")
```

Ejecuta la app:

```bash
streamlit run app.py
```

## Conceptos clave

- Renderizado reactivo: la app se actualiza cuando cambian los inputs.
- Widgets: entrada del usuario (`text_input`, `selectbox`, `slider`, etc.).
- Layout: columnas y pestañas (`st.columns`, `st.tabs`).
- Estado: `st.session_state` para conservar variables entre interacciones.