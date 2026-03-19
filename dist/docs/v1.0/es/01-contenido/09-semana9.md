---
title: "Semana 9: Manipulación de Datos con Pandas"
position: 9
draft: true
---

[Documentación Oficial de Pandas](https://pandas.pydata.org/docs/index.html) 

+++admonition
---
type: note
title: "El Poder de Transformar la Información"
---
¡Bienvenido a la fase más activa de la ciencia de datos! En la sesión anterior aprendiste a **observar** tus datos. Ahora entrarás en la cocina: aprenderás a **editarlos, limpiarlos y transformarlos**. 

Imagina que recibes la lista de invitados para una gran fiesta, pero algunos nombres están mal escritos, otros están repetidos y a algunos se les olvidó poner su edad. Esta etapa es vital: **Si los datos están "sucios", tus conclusiones serán falsas.**
+++

---

## 1. Filtrado Inteligente: Seleccionando lo que importa

El filtrado es como usar un buscador avanzado. Para crear reglas de búsqueda, usamos **Operadores de Comparación** y **Operadores Lógicos**.

### 1.1 Operadores de Comparación: "¿Cumple la regla?"
Estos operadores comparan dos cosas y nos dicen si es verdad (`True`) o mentira (`False`). 

**Nuestro Dataset de Práctica:**
Copia esto en tu entorno para seguir los ejemplos. Es una tabla de empleados con 15 registros.

```python
import pandas as pd
import numpy as np

# Dataset robusto para práctica
data = {
    'nombre': ['Ana García', 'Beto Pérez', 'Carla Ruiz', 'David León', 'Elena Rosa', 
               'Fabio Sol', 'Gina Paz', 'Hugo Lima', 'Iris Mar', 'Jairo Luz',
               'Katy Oro', 'Luis Mar', 'Marta Gil', 'Noé Vera', 'Olga San'],
    'edad': [25, 30, 22, 17, 28, 45, 33, 29, 41, 26, 19, 52, 24, 16, 35],
    'salario': [50000, 75000, 45000, 15000, 60000, 95000, 70000, 55000, 85000, 48000, 52000, 98000, 47000, 12000, 66000],
    'ciudad': ['Medellín', 'Bogotá', 'Medellín', 'Cali', 'Bogotá', 'Madrid', 'Medellín', 'Cali', 'Madrid', 'Bogotá', 'Cali', 'Madrid', 'Medellín', 'Bogotá', 'Cali'],
    'activo': [True, True, True, False, True, True, True, True, False, True, True, True, True, False, True]
}
df = pd.DataFrame(data)
```

| Símbolo | Qué hace | Ejemplo |
| :--- | :--- | :--- |
| `==` | Igual a | `df[df['ciudad'] == 'Madrid']` |
| `!=` | Diferente de | `df[df['ciudad'] != 'Madrid']` |
| `>` | Mayor que | `df[df['edad'] > 40]` |
| `<` | Menor que | `df[df['salario'] < 20000]` |

---

## 2. Sondeo de Datos: Entendiendo las Categorías

Antes de manipular, debemos saber qué hay en nuestras columnas.

### 2.1 Encontrar Valores Únicos
- `df['columna'].unique()`: Lista de valores sin repetir.
- `df['columna'].nunique()`: Total de categorías diferentes.

### 2.2 Contar Frecuencias (`value_counts`)
Nos dice cuántas veces aparece cada valor. Es fundamental para ver si los datos están balanceados.

```python
print(df['ciudad'].value_counts())
```

---

## 3. Mantenimiento y Orden: Pulinedo la Tabla

### 3.1 Ordenar Datos (`sort_values`)
```python
# De MAYOR a MENOR
ranking = df.sort_values(by='salario', ascending=False)
```

### 3.2 Renombrar y Eliminar Columnas
```python
# Renombrar: {viejo: nuevo}
df = df.rename(columns={'salario': 'sueldo'})

# Eliminar irrelevantes
df = df.drop(columns=['columna_inutil'], errors='ignore') 
```

---

## 4. Limpieza de Datos: El "Lavado" Profesional

La limpieza es el 80% del trabajo de un científico de datos. Aquí es donde convertimos basura en oro.

### 4.1 Manejo de nulos (NaN)
Los valores nulos (`NaN`) son como "agujeros negros" en tus datos: cualquier operación que toque un `NaN` se vuelve `NaN`.

**Estrategias de Reparación:**

```python
import pandas as pd
import numpy as np

# Dataset de prueba para Nulos
df_test = pd.DataFrame({
    'estudiante': ['Ana', 'Juan', 'Pedro', 'Marta'],
    'nota': [90, np.nan, 85, np.nan],
    'asistencia': [10, 8, np.nan, 9]
})

# 1. Rellenar con la Media (Promedio): 
# Útil si los datos son uniformes y no hay valores "locos".
df_test['nota'] = df_test['nota'].fillna(df_test['nota'].mean())

# 2. Rellenar con un valor fijo:
df_test['asistencia'] = df_test['asistencia'].fillna(0)

# 3. Borrar filas con huecos (dropna):
# how='any' (por defecto): borra si hay AL MENOS UN nulo.
# how='all': borra solo si TODA la fila es nula.
df_test = df_test.dropna(subset=['asistencia'])
```

### 4.2 Conversión de Tipos (`astype` y "Casting")
A veces Pandas lee los números como texto (por ejemplo, si vienen de un CSV mal formado). Esto se llama "Tipo Objeto" (`object`).

**¿Por qué es vital cambiar el tipo?**
1.  **Cálculos:** No puedes sumar `"10" + "20"` (daría `"1020"`, no `30`).
2.  **Memoria:** Los tipos numéricos (`float`, `int`) ocupan mucho menos espacio que el texto.

```python
# Convertir una columna de texto a número decimal
df['salario'] = df['salario'].astype(float)

# Convertir una columna a Categoría (Ahorra muchísima memoria si hay pocos valores únicos)
df['ciudad'] = df['ciudad'].astype('category')
```

---

## 5. Inteligencia de Datos: Agrupación y Fusión

Aquí es donde empezamos a responder preguntas de negocio complejas.

### 5.1 Agrupación (`groupby`): El modelo "Dividir-Aplicar-Combinar"
Cuando haces un `groupby`, Pandas sigue estos tres pasos internos:
1.  **Dividir:** Separa el DataFrame en pequeños grupos (ej. por "Ciudad").
2.  **Aplicar:** Ejecuta un cálculo en cada grupito (ej. la suma).
3.  **Combinar:** Junta los resultados en una nueva tabla resumen.

**Uso de `.agg()` para múltiples cálculos:**
No te limites a sumar. Puedes pedir muchas cosas a la vez:

```python
# Reporte Pro: Suma total, promedio y conteo de empleados por ciudad
reporte = df.groupby('ciudad')['salario'].agg(['sum', 'mean', 'count'])
print(reporte)
```

### 5.2 Uniendo Tablas (`merge`): ¿Cuál elegir?
Unir tablas es como un rompecabezas. Tienes una columna "puente" (ID) que conecta ambos mundos. Existen varios tipos de unión:

> [!TIP]
> **Analogía Visual:**
> - **LEFT Join (El más común):** Imagina que tu tabla de la izquierda es sagrada. Mantienes a todos tus empleados, y si alguno no tiene bono en la otra tabla, le pones un `NaN`. No pierdes a nadie de tu base original.
> - **INNER Join:** Solo mantiene a los que aparecen en AMBAS tablas. Si un empleado no tiene bono, desaparece del reporte. Si un bono no tiene empleado, también desaparece.

```python
# Unimos Empleados con sus Bonos
# how='left' asegura que ningún empleado sea borrado del reporte final
df_unido = pd.merge(df_empleados, df_bonos, on='nombre', how='left')

# Limpieza post-unión: Los que no tenían bono aparecen como NaN. Ponemos 0.
df_unido['bono'] = df_unido['bono'].fillna(0)
```

---

## 🚀 ¡Todo listo!
Ahora que entiendes la lógica profunda de la limpieza y la agregación, estás listo para aplicarlo en el **[Proyecto: Dashboard Aroma & Grano](04-actividad-guiada.md)**.
