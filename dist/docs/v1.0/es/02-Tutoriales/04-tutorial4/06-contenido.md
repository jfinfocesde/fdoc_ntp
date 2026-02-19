---
title: "Gráficos y visualizaciones (API charts)"
position: 6
date: 2025-11-11
---

## Introducción

Streamlit incluye elementos nativos de gráficos y soporta librerías populares como Matplotlib, Altair, Vega-Lite, Plotly, Bokeh y PyDeck. Este tema muestra ejemplos mínimos para visualizar datos rápidamente durante la comprensión de un conjunto de datos.

## Instalación de dependencias

Para ejecutar los ejemplos de este tema, instala las siguientes librerías:

```bash
pip install streamlit pandas numpy matplotlib altair plotly bokeh pydeck
```

Opcionalmente, puedes crear un `requirements.txt` y usar instalación por archivo:

```text
streamlit
pandas
numpy
matplotlib
altair
plotly
bokeh
pydeck
```

```bash
pip install -r requirements.txt
```

## Datos de ejemplo

```python
import pandas as pd

df = pd.DataFrame({
    "mes": ["Ene", "Feb", "Mar", "Abr", "May"],
    "ventas": [120, 150, 90, 200, 170],
    "costos": [80, 100, 70, 110, 95],
})
```

## Gráficos nativos de Streamlit

```python
import streamlit as st

st.subheader("Gráficos nativos")
st.line_chart(df[["ventas", "costos"]])
st.area_chart(df[["ventas"]])
st.bar_chart(df[["ventas", "costos"]])

# Para scatter con datos 2D
import numpy as np
scatter_df = pd.DataFrame({
    "x": np.random.randn(200),
    "y": np.random.randn(200)
})
st.scatter_chart(scatter_df)
```

## Matplotlib

```python
import matplotlib.pyplot as plt

fig, ax = plt.subplots()
ax.plot(df["mes"], df["ventas"], marker="o")
ax.set_title("Ventas por mes")
st.pyplot(fig)
```

## Altair

```python
import altair as alt

chart = alt.Chart(df).mark_line(point=True).encode(
    x="mes",
    y="ventas"
)
st.altair_chart(chart, use_container_width=True)
```

## Vega-Lite

```python
vega_spec = {
  "data": {"values": df.to_dict(orient="records")},
  "mark": "bar",
  "encoding": {
    "x": {"field": "mes", "type": "ordinal"},
    "y": {"field": "ventas", "type": "quantitative"}
  }
}
st.vega_lite_chart(vega_spec, use_container_width=True)
```

## Plotly

```python
import plotly.express as px

fig = px.line(df, x="mes", y="ventas", title="Ventas por mes")
st.plotly_chart(fig, use_container_width=True)
```

## Bokeh

```python
from bokeh.plotting import figure

p = figure(x_range=list(df["mes"]), height=300, title="Ventas")
p.vbar(x=df["mes"], top=df["ventas"], width=0.8)
st.bokeh_chart(p, use_container_width=True)
```

## PyDeck (mapas)

```python
import pydeck as pdk
import pandas as pd

map_df = pd.DataFrame({
    "lat": [4.7110, 6.2518],
    "lon": [-74.0721, -75.5636]
})

layer = pdk.Layer(
    "ScatterplotLayer",
    map_df,
    get_position=["lon", "lat"],
    get_radius=20000,
    get_color=[255, 0, 0]
)
view_state = pdk.ViewState(latitude=5.5, longitude=-74.8, zoom=5)
st.pydeck_chart(pdk.Deck(layers=[layer], initial_view_state=view_state))
```

## GraphViz

```python
spec = """
digraph {
  A -> B
  B -> C
  A -> C
}
"""
st.graphviz_chart(spec)
```

## Cargar datos desde CSV con caché

```python
import streamlit as st
import pandas as pd

@st.cache_data
def cargar_csv(archivo):
    return pd.read_csv(archivo)

archivo = st.file_uploader("Sube un CSV", type=["csv"]) 
if archivo:
    datos = cargar_csv(archivo)
    st.bar_chart(datos.select_dtypes(include="number"))
else:
    st.info("Sube un archivo para visualizar métricas numéricas.")
```

## Consejos

- Usa `use_container_width=True` para que los gráficos se adapten al ancho disponible.
- Selecciona columnas por tipo para evitar errores (por ejemplo, mostrar solo numéricas en `st.bar_chart`).
- Mantén visualizaciones sencillas y enfocadas en comprensión: tendencias, distribuciones y comparaciones básicas.

## Referencia oficial

Consulta la documentación de elementos de gráficos:
https://docs.streamlit.io/develop/api-reference/charts