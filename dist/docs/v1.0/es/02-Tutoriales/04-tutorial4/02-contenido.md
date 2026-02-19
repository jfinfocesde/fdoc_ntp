---
title: "Widgets y estado"
position: 2
date: 2025-11-11
---

## Widgets esenciales

```python
import streamlit as st

st.subheader("Widgets comunes")
opcion = st.selectbox("Selecciona una opción", ["A", "B", "C"])
valor = st.slider("Valor", min_value=0, max_value=100, value=50)
boton = st.button("Procesar")

if boton:
    st.write(f"Opción: {opcion}, Valor: {valor}")
```

## Layout con columnas y pestañas

```python
col1, col2 = st.columns(2)
with col1:
    st.info("Panel izquierdo")
with col2:
    st.warning("Panel derecho")

tab1, tab2 = st.tabs(["Resultados", "Configuración"])
with tab1:
    st.write("Mostrar resultados aquí")
with tab2:
    st.write("Parámetros y opciones")
```

## Estado de la aplicación

```python
if "contador" not in st.session_state:
    st.session_state.contador = 0

if st.button("Incrementar"):
    st.session_state.contador += 1

st.write("Contador:", st.session_state.contador)
```

## Componentes principales de Streamlit

### Texto y Markdown

```python
import streamlit as st

st.title("Título de la app")
st.header("Encabezado")
st.subheader("Subencabezado")
st.markdown("Texto en **Markdown** con _estilos_.")
st.caption("Texto en tamaño pequeño para notas.")
st.divider()
```

### Datos: DataFrame, tabla y JSON

```python
import streamlit as st
import pandas as pd

df = pd.DataFrame({"A": [1, 2, 3], "B": [4, 5, 6]})
st.dataframe(df)           # Tabla interactiva
st.table(df.head())        # Tabla estática
st.json({"status": "ok", "items": len(df)})
```

### Métricas

```python
import streamlit as st

st.metric(label="Usuarios activos", value=128, delta=+5)
```

### Media (imagen, audio, video)

```python
import streamlit as st

st.image("https://placekitten.com/400/250", caption="Imagen remota")

audio_bytes = b"\x00\x00"  # ejemplo mínimo
st.audio(audio_bytes, format="audio/wav")

st.video("https://www.w3schools.com/html/mov_bbb.mp4")
```

### Código y ayuda

```python
import streamlit as st

st.code("""def sumar(a, b):\n    return a + b""", language="python")

with st.echo():
    x = 2
    y = 3
    st.write("Resultado:", x + y)

st.help(st.write)  # Mostrar ayuda de una función
```

### Descarga de archivos

```python
import streamlit as st

contenido = "Hola Streamlit".encode("utf-8")
st.download_button("Descargar saludo", contenido, file_name="saludo.txt")
```

### Enlace a páginas (multipágina)

```python
import streamlit as st

# Enlaza a otra página dentro de una app multipágina
st.page_link("app.py", label="Ir a inicio", icon="🏠")
```

Para más componentes y detalles, consulta la referencia oficial de la API:
https://docs.streamlit.io/develop/api-reference

### Formularios

```python
import streamlit as st

with st.form(key="mi_formulario"):
    nombre = st.text_input("Nombre")
    edad = st.number_input("Edad", min_value=0, max_value=120, value=25)
    enviado = st.form_submit_button("Enviar")

if enviado:
    st.success(f"Formulario recibido: {nombre}, {edad} años")
```

### Editor de datos y configuración de columnas

```python
import streamlit as st
import pandas as pd

df = pd.DataFrame({
    "Producto": ["A", "B", "C"],
    "Precio": [10, 20, 30],
    "Stock": [5, 3, 9],
})

st.data_editor(
    df,
    column_config={
        "Precio": st.column_config.NumberColumn("Precio (USD)", min_value=0, format="$%d"),
        "Stock": st.column_config.NumberColumn("Unidades", min_value=0),
    },
    num_rows="dynamic",
)
```

### HTML, LaTeX y texto preformateado

```python
import streamlit as st

st.html("<p style='color:tomato'>HTML renderizado</p>")
st.latex(r"\int_0^1 x^2 \, dx")
st.text("Texto preformateado (monoespaciado)")
st.badge("Nuevo")
```

### Enlaces y streaming de texto

```python
import streamlit as st

st.link_button("Ir a la galería", url="https://streamlit.io")

def generador():
    yield "Hola "
    yield "desde "
    yield "un stream de texto."

st.write_stream(generador())
```