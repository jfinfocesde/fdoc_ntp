---
title: "Semana 13: Visualización de Datos con Streamlit"
position: 13
draft: false
---

# 📊 Visualización de Datos con Streamlit (Guía Definitiva)

Streamlit transforma la visualización de datos en una experiencia sencilla y poderosa. No solo permite mostrar gráficos, sino que los hace **interactivos** con apenas unas líneas de código.

Existen dos formas principales de trabajar con gráficos en Streamlit:
1. **Gráficos Nativos (`st.line_chart`, `st.bar_chart`, etc.)**: Ideales para visualizaciones rápidas y elegantes sin configurar casi nada.
2. **Integración con Librerías Externas (Seaborn, Plotly, Altair)**: Para cuando necesitas control total o interactividad avanzada.

---

## 1. Gráficos Nativos de Streamlit (Simples y Rápidos)

Estos gráficos son "azúcar sintáctico" sobre Altair. Son responsivos por defecto y tienen un diseño limpio.

### 📈 Gráfico de Líneas (`st.line_chart`)
Se usa principalmente para mostrar **tendencias a lo largo del tiempo**.

```python
import streamlit as st
import pandas as pd
import numpy as np

st.title("Evolución de Ventas")

# Ejemplo 1: Una sola línea (Serie temporal simple)
chart_data = pd.DataFrame(
    np.random.randn(20, 1),
    columns=['Ventas']
)
st.subheader("Tendencia Mensual")
st.line_chart(chart_data)

# Ejemplo 2: Comparativa de múltiples productos con fechas reales
st.subheader("Ventas por Semanas (Datos Reales)")
fechas = pd.date_range("20240101", periods=10, freq="W")
df_tiempo = pd.DataFrame(
    np.random.randint(100, 500, size=(10, 2)),
    index=fechas,
    columns=['Producto A', 'Producto B']
)
st.line_chart(df_tiempo)
```

### 🏔️ Gráfico de Área (`st.area_chart`)
Similar al de líneas, pero resalta el **volumen acumulado**. Es excelente para visualizar cuotas de mercado o uso de recursos.

```python
st.subheader("Uso de Servidores (GB)")
data_area = pd.DataFrame(
    np.random.rand(20, 2),
    columns=['Servidor Principal', 'Servidor Backup']
)
st.area_chart(data_area)
```

### 📊 Gráfico de Barras (`st.bar_chart`)
Ideal para **comparar categorías discretas**. Ahora soporta gráficos horizontales y apilados.

```python
st.subheader("Inventario por Categoría")
data_bar = pd.DataFrame({
    'Categoría': ['Electrónica', 'Hogar', 'Moda', 'Juguetes'],
    'Stock': [45, 32, 89, 12]
}).set_index('Categoría')

st.bar_chart(data_bar)

# Ejemplo avanzado: Barras apiladas (Stacked)
st.subheader("Ventas por Sucursal y Turno")
sucursales = pd.DataFrame({
    "Sucursal": ["Norte", "Sur", "Este", "Oeste"],
    "Mañana": [10, 20, 15, 25],
    "Tarde": [30, 15, 25, 20]
}).set_index("Sucursal")
st.bar_chart(sucursales)
```

### 🎯 Gráfico de Dispersión Nativo (`st.scatter_chart`)
Añadido recientemente, permite ver correlaciones rápidamente sin librerías externas.

```python
st.subheader("Correlación: Peso vs Altura")
df_scatter = pd.DataFrame(
    np.random.randn(50, 2),
    columns=['Peso', 'Altura']
)
st.scatter_chart(df_scatter, x='Peso', y='Altura', color='#ff4b4b')
```

### 📍 Mapas Interactivos (`st.map`)
Si tu DataFrame tiene columnas llamadas `lat` (latitud) y `lon` (longitud), Streamlit dibuja un mapa automáticamente.

```python
st.subheader("Ubicación de Tiendas")
map_data = pd.DataFrame({
    'lat': [6.2442, 4.7110, 3.4516],
    'lon': [-75.5812, -74.0721, -76.5320],
    'Nombre': ['Medellín', 'Bogotá', 'Cali']
})
st.map(map_data, size=20, color='#0044ff')
```

---

## 2. Visualización Estadística con Seaborn & Matplotlib

Cuando necesitas gráficos más técnicos (boxplots, correlaciones, etc.), usamos `st.pyplot()`.

### 🧪 Preparación de Datos Reales
Usaremos el famoso dataset `tips` (propinas) que viene con Seaborn.

```python
import seaborn as sns
import matplotlib.pyplot as plt

df_tips = sns.load_dataset("tips")

# Tip: Para que los gráficos se vean bien en Streamlit
plt.style.use('dark_background') # O 'ggplot'
```

### 📉 Scatter Plot con Línea de Regresión
Para ver no solo la relación, sino la tendencia matemática.

```python
st.subheader("Relación Cuenta vs Propina (Regresión)")
fig, ax = plt.subplots()
sns.regplot(data=df_tips, x="total_bill", y="tip", ax=ax, scatter_kws={'alpha':0.5})
st.pyplot(fig)
```

### 📦 Violin Plot (Avanzado)
Muestra la distribución completa, incluyendo la densidad de los datos.

```python
st.subheader("Distribución Detallada por Día y Género")
fig, ax = plt.subplots()
sns.violinplot(data=df_tips, x="day", y="total_bill", hue="sex", split=True, ax=ax)
st.pyplot(fig)
```

### 🌡️ Heatmap de Correlación
Perfecto para visualizar qué variables están relacionadas.

```python
st.subheader("Matriz de Correlación")
fig, ax = plt.subplots()
numeric_df = df_tips.select_dtypes(include=[np.number])
sns.heatmap(numeric_df.corr(), annot=True, cmap="mako", ax=ax)
st.pyplot(fig)
```

---

## 3. Gráficos Interactivos Pro con Plotly

Plotly permite hacer **zoom**, ver detalles al pasar el mouse y descargar el gráfico como imagen directamente desde la app.

### 🍩 Gráfico de Pastel (Donut Chart)
Ideal para mostrar porcentajes de un total.

```python
import plotly.express as px

st.subheader("Distribución de Clientes por Día")
fig_pie = px.pie(df_tips, values='total_bill', names='day', hole=0.5, 
                 title="Porcentaje de Ingresos por Día",
                 color_discrete_sequence=px.colors.sequential.RdBu)
st.plotly_chart(fig_pie, use_container_width=True)
```

### 📉 Gráfico de Burbujas (Bubble Chart)
Permite visualizar 3 o 4 dimensiones a la vez (X, Y, Tamaño y Color).

```python
st.subheader("Análisis Iris: Largo vs Ancho")
df_iris = sns.load_dataset("iris")
fig_bubble = px.scatter(df_iris, x="sepal_width", y="sepal_length", 
                        color="species", size="petal_length",
                        hover_data=['petal_width'])
st.plotly_chart(fig_bubble, use_container_width=True)
```

---

## 4. Interactividad: Filtros en Tiempo Real

Lo más potente de Streamlit es usar widgets para que el usuario controle los gráficos.

```python
st.header("🎮 Panel Interactivo Dinámico")

# Slider para filtrar por rango de cuenta
min_bill, max_bill = st.slider(
    "Selecciona el rango de la cuenta ($)",
    float(df_tips['total_bill'].min()), 
    float(df_tips['total_bill'].max()), 
    (10.0, 40.0)
)

# Filtrar DataFrame
df_filtrado = df_tips[(df_tips['total_bill'] >= min_bill) & (df_tips['total_bill'] <= max_bill)]

# Mostrar gráfico actualizado
st.write(f"Mostrando {len(df_filtrado)} registros en el rango seleccionado.")
st.bar_chart(df_filtrado.groupby('day')['tip'].sum())
```

---

## 💡 ¿Cuándo usar cada uno?

| Tipo de Gráfico | Función | Cuándo usarlo |
| :--- | :--- | :--- |
| **Líneas** | Tendencia | Datos temporales (años, meses, días). |
| **Barras** | Comparación | Comparar valores entre grupos (Países, Categorías). |
| **Área** | Acumulación | Ver cómo cambia el total y sus partes. |
| **Scatter** | Relación | Ver si una variable afecta a otra. |
| **Boxplot** | Estadística | Identificar "outliers" (valores extraños) y rangos. |
| **Violín** | Densidad | Ver dónde se concentran más los datos. |
| **Pie/Donut** | Composición | Ver partes de un todo (porcentajes). |

---

## 🚀 Proyecto Final: Dashboard de Negocios Completo

Copia este código en un archivo `app_ventas.py` para ver un ejemplo de nivel profesional.

```python
import streamlit as st
import pandas as pd
import numpy as np
import plotly.express as px
import seaborn as sns

# Configuración
st.set_page_config(page_title="Ventas Globales 2024", layout="wide", page_icon="💰")

# Generar datos falsos pero realistas
@st.cache_data
def load_business_data():
    np.random.seed(42)
    paises = ['Colombia', 'México', 'Argentina', 'España', 'Chile']
    categorias = ['Software', 'Hardware', 'Consultoría', 'Soporte']
    data = []
    for _ in range(500):
        data.append({
            'Fecha': pd.to_datetime('2024-01-01') + pd.to_timedelta(np.random.randint(0, 180), unit='D'),
            'País': np.random.choice(paises),
            'Categoría': np.random.choice(categorias),
            'Venta': np.random.uniform(500, 5000),
            'Satisfacción': np.random.randint(1, 6)
        })
    return pd.DataFrame(data)

df_ventas = load_business_data()

# SIDEBAR
st.sidebar.image("https://cdn-icons-png.flaticon.com/512/1055/1055644.png", width=100)
st.sidebar.header("Filtros de Análisis")
pais_sel = st.sidebar.multiselect("Seleccionar Países", options=df_ventas['País'].unique(), default=df_ventas['País'].unique())
cat_sel = st.sidebar.selectbox("Categoría Principal", options=['Todas'] + list(df_ventas['Categoría'].unique()))

# Filtrado lógico
df_view = df_ventas[df_ventas['País'].isin(pais_sel)]
if cat_sel != 'Todas':
    df_view = df_view[df_view['Categoría'] == cat_sel]

# UI PRINCIPAL
st.title("💹 Dashboard Corporativo: Ventas 2024")
st.markdown("---")

# Métricas
m1, m2, m3, m4 = st.columns(4)
m1.metric("Ventas Totales", f"${df_view['Venta'].sum():,.0f}", "+12%")
m2.metric("Ticket Promedio", f"${df_view['Venta'].mean():,.2f}")
m3.metric("Satisfacción Prom.", f"{df_view['Satisfacción'].mean():.1f} ⭐")
m4.metric("Países Activos", len(pais_sel))

# Gráficos
col_izq, col_der = st.columns(2)

with col_izq:
    st.subheader("📈 Ventas Acumuladas en el Tiempo")
    df_time = df_view.groupby('Fecha')['Venta'].sum().reset_index()
    fig_time = px.line(df_time, x='Fecha', y='Venta', template="plotly_dark")
    st.plotly_chart(fig_time, use_container_width=True)

with col_der:
    st.subheader("📊 Ventas por Categoría y País")
    fig_bar = px.bar(df_view, x='País', y='Venta', color='Categoría', barmode='group')
    st.plotly_chart(fig_bar, use_container_width=True)

# Sección inferior
st.subheader("🔍 Detalle de Transacciones")
st.dataframe(df_view.sort_values(by='Fecha', ascending=False), use_container_width=True)
```

### 🎯 Retos para practicar:
1. **Colores**: Intenta cambiar la paleta de colores de los gráficos de Seaborn usando `sns.set_palette("husl")`.
2. **Columnas**: Usa `st.columns` para poner tres gráficos pequeños en una sola fila.
3. **Mapas**: Busca un dataset con coordenadas de tu ciudad y represéntalo con `st.map`.