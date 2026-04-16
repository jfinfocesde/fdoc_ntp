---
title: "Semana 11: Talleres Prácticos de Manipulación y Filtrado de Datos con Pandas"
position: 11
draft: false
---


## Taller Práctico: Diagnóstico y Limpieza de Datos con Pandas

En el mundo real, los datos nunca llegan perfectos. Vienen con errores de digitación, valores faltantes, formatos incorrectos y registros duplicados. En esta actividad, los aprendices pasarán de ser simples lectores de datos a ingenieros de calidad de datos, aprendiendo a "sanear" un DataFrame antes de cualquier análisis.

Para este taller, utilizaremos el caso de estudio **"Inventario de Hardware y Sensores IoT"**, simulando el registro desordenado de componentes en un laboratorio de desarrollo tecnológico.

---

## Fase 1: Preparación del Entorno

Si los aprendices ya tienen su entorno virtual configurado del taller anterior, pueden reutilizarlo. Si no, recuérdales los pasos:

**Paso 1:** En la terminal, crear y activar el entorno virtual:
```bash
# Windows
python -m venv venv
venv\Scripts\activate

# macOS/Linux
python -m venv venv
source venv/bin/activate
```

**Paso 2:** Crear un archivo llamado `limpieza_pandas.py` para escribir el código.

---

## Fase 2: El Dataset "Sucio" (Nuestro material de trabajo)

Copia y pega el siguiente código. Este conjunto de datos ha sido diseñado intencionalmente con los errores más comunes que se encuentran en la industria: espacios en blanco, formatos de dinero inconsistentes, fechas mezcladas y valores nulos.

```python
import pandas as pd
import numpy as np

# 1. Datos con errores intencionales
datos_desordenados = {
    'ID_Componente': ['IOT-001', 'IOT-002', 'IOT-003', 'IOT-002', 'IOT-005', 'IOT-006', np.nan, 'IOT-008', 'IOT-009', 'IOT-010'],
    ' Nombre Equipo ': ['  Raspberry Pi 5  ', 'Sensor DHT11', 'Pantalla LCD 16x2', 'Sensor DHT11', 'Microcontrolador ESP32', '  cables jumper m-m', 'Sensor de Humedad', 'RELE 5V', 'Cámara Módulo', 'Raspberry Pi 5'],
    'Categoria': ['Microordenador', 'Sensor', 'Periférico', 'Sensor', 'Microcontrolador', 'Accesorio', 'Sensor', 'Actuador', 'Periférico', 'Microordenador'],
    'Precio_COP': ['$350.000', '15.000 COP', '45,000', '15.000 COP', '$25.000', 'nan', '12000', '8.500', '65.000 COP', '$350.000'],
    'Estado_Actual': ['Activo', 'Dañado', 'Activo', 'Dañado', 'activo', 'ACTIVO', 'en revisión', 'Activo', 'Activo', 'activo'],
    'Fecha_Ingreso': ['2026/01/15', '15-02-2026', '2026-03-10', '15-02-2026', '2026/04/22', 'Hoy', '2025-11-30', '2026-01-01', '2026-02-28', '2026/01/15'],
    'Cantidad_Stock': [5, 20, 10, 20, 50, -5, np.nan, 30, 15, 5000] # Ojo a los valores imposibles (-5 y 5000)
}

df_inventario = pd.DataFrame(datos_desordenados)

print("--- 1. DATAFRAME ORIGINAL (SUCIO) ---")
print(df_inventario)
```

---

## Fase 3: Diagnóstico Inicial (Conociendo al enemigo)

Antes de limpiar, debemos saber qué está mal. Pandas nos ofrece herramientas de rayos X para evaluar la salud de nuestro DataFrame.

```python
print("\n--- 2. DIAGNÓSTICO: INFORMACIÓN GENERAL ---")
# .info() nos dice el tipo de dato de cada columna y cuántos valores NO nulos hay
df_inventario.info()

print("\n--- 3. DIAGNÓSTICO: CONTEO DE VALORES NULOS ---")
# .isna().sum() suma la cantidad de vacíos por columna
print(df_inventario.isna().sum())

print("\n--- 4. DIAGNÓSTICO: VALORES DUPLICADOS ---")
# .duplicated().sum() nos dice cuántas filas son exactamente iguales a otra
duplicados = df_inventario.duplicated().sum()
print(f"Filas duplicadas encontradas: {duplicados}")
```

---

## Fase 4: Limpieza Paso a Paso

Aquí comienza el proceso de ingeniería de datos. Cada paso transforma el DataFrame en una versión más limpia.

### 4.1 Normalización de Nombres de Columnas
Los nombres de las columnas en nuestro dataset tienen mayúsculas, espacios al principio y al final. Esto es una pesadilla para programar. Vamos a estandarizarlos.

```python
print("\n--- 5. LIMPIEZA: NOMBRES DE COLUMNAS ---")
# Usamos comprensión de listas o métodos de strings para limpiar los nombres
df_inventario.columns = df_inventario.columns.str.strip().str.lower().str.replace(' ', '_')
print("Nuevas columnas:", df_inventario.columns.tolist())
```

### 4.2 Eliminación de Duplicados Exactos
Tenemos sensores ingresados dos veces por error humano.

```python
print("\n--- 6. LIMPIEZA: ELIMINAR DUPLICADOS ---")
# drop_duplicates() elimina filas idénticas. 
# inplace=True aplica el cambio directamente al DataFrame original
df_inventario.drop_duplicates(inplace=True)
print(f"Filas después de borrar duplicados: {len(df_inventario)}")
```

### 4.3 Estandarización de Textos (Categorías)
La columna `estado_actual` tiene "Activo", "activo" y "ACTIVO". Para Pandas, son tres cosas diferentes. Debemos unificarlas.

```python
print("\n--- 7. LIMPIEZA: ESTANDARIZAR TEXTOS ---")
# Quitamos espacios extra y pasamos todo a minúsculas
df_inventario['nombre_equipo'] = df_inventario['nombre_equipo'].str.strip()
df_inventario['estado_actual'] = df_inventario['estado_actual'].str.strip().str.lower()

print(df_inventario[['nombre_equipo', 'estado_actual']])
```

### 4.4 Transformación de Tipos de Datos (El problema del Dinero)
El `precio_cop` entró como texto (`$350.000`, `15.000 COP`). No podemos hacer matemáticas con texto. Debemos quitar los símbolos y convertir a números.

```python
print("\n--- 8. LIMPIEZA: CONVERSIÓN DE MONEDA A NÚMERO ---")
# 1. Convertimos a string (por si acaso)
# 2. Reemplazamos el signo $, la palabra COP, el punto y la coma por "nada" ('')
df_inventario['precio_cop'] = df_inventario['precio_cop'].astype(str)\
    .str.replace('$', '', regex=False)\
    .str.replace(' COP', '', regex=False)\
    .str.replace('.', '', regex=False)\
    .str.replace(',', '', regex=False)

# 3. Convertimos el texto resultante a números enteros. 
# errors='coerce' fuerza a que si algo sale mal (como la palabra 'nan'), lo vuelva un nulo (NaN) real.
df_inventario['precio_cop'] = pd.to_numeric(df_inventario['precio_cop'], errors='coerce')

print(df_inventario[['nombre_equipo', 'precio_cop']])
```

### 4.5 Manejo de Valores Nulos (NaN)
¿Qué hacemos con los espacios vacíos? Tenemos dos opciones: rellenarlos (imputación) o eliminar la fila entera.

```python
print("\n--- 9. LIMPIEZA: MANEJO DE NULOS ---")
# Opción A: Rellenar nulos con un valor por defecto (ej. Cantidad de stock a 0)
df_inventario['cantidad_stock'] = df_inventario['cantidad_stock'].fillna(0)

# Opción B: Eliminar filas donde un dato CRÍTICO sea nulo (ej. Si no tiene ID, no sirve)
# subset=['id_componente'] le dice que solo busque nulos en esa columna específica
df_inventario.dropna(subset=['id_componente'], inplace=True)

print(df_inventario[['id_componente', 'cantidad_stock']])
```

### 4.6 Corrección de Fechas (Datetime)
Las fechas tienen formatos horribles (`2026/01/15`, `15-02-2026`, `Hoy`). Vamos a obligar a Pandas a estandarizarlas.

```python
print("\n--- 10. LIMPIEZA: ESTANDARIZAR FECHAS ---")
# errors='coerce' convertirá valores absurdos como 'Hoy' en NaT (Not a Time / Nulo de tiempo)
df_inventario['fecha_ingreso'] = pd.to_datetime(df_inventario['fecha_ingreso'], errors='coerce')

print(df_inventario[['nombre_equipo', 'fecha_ingreso']])
```

### 4.7 Tratamiento de Valores Atípicos (Outliers Lógicos)
Un stock no puede ser negativo (-5), y un error de digitación puso 5000 Raspberry Pi.

```python
print("\n--- 11. LIMPIEZA: CORREGIR OUTLIERS ---")
# Si el stock es menor a 0, lo igualamos a 0 usando .loc
df_inventario.loc[df_inventario['cantidad_stock'] < 0, 'cantidad_stock'] = 0

# Si el stock es sospechosamente alto (mayor a 1000), lo marcamos para revisión (lo volvemos nulo o lo limitamos)
# En este caso, lo limitaremos al máximo lógico del laboratorio (ej. 100)
df_inventario.loc[df_inventario['cantidad_stock'] > 1000, 'cantidad_stock'] = 100

print(df_inventario[['nombre_equipo', 'cantidad_stock']])
```

---

## Fase 5: El DataFrame Final Limpio y Exportación

Al final de nuestra tubería de procesamiento, podemos visualizar el resultado y guardarlo de forma segura para usarlo en otras aplicaciones.

```python
print("\n--- 12. DATAFRAME FINAL LIMPIO ---")
# Reiniciamos el índice para que no haya saltos numéricos tras borrar filas
df_inventario.reset_index(drop=True, inplace=True)
print(df_inventario)

# Opcional: Exportar el trabajo limpio a CSV
# df_inventario.to_csv('inventario_limpio.csv', index=False)
```

---

## Fase 6: Ejercicios Resueltos de Calidad de Datos

A continuación, se presentan las soluciones paso a paso para los requerimientos del jefe de laboratorio, aplicados al DataFrame `df_inventario`.

### Ejercicio 1: Salvando los ID Perdidos
En lugar de eliminar la fila que no tiene `id_componente`, rellenamos ese valor nulo con el texto `"ID_PENDIENTE"`.
```python
# .fillna() reemplaza los valores NaN por el valor especificado
df_inventario['id_componente'] = df_inventario['id_componente'].fillna('ID_PENDIENTE')
print("ID recuperados:")
print(df_inventario[['id_componente', 'nombre_equipo']].head(7))
```

### Ejercicio 2: Recuperando Fechas Inválidas
Reemplazamos las fechas nulas (como la que se convirtió en `NaT` por haber dicho "Hoy") por la fecha actual del sistema.
```python
from datetime import datetime

# Buscamos las fechas nulas y aplicamos la fecha actual en formato YYYY-MM-DD
fecha_actual = pd.to_datetime(datetime.now().strftime('%Y-%m-%d'))
df_inventario['fecha_ingreso'] = df_inventario['fecha_ingreso'].fillna(fecha_actual)
print("\nFechas inválidas recuperadas:")
print(df_inventario[['nombre_equipo', 'fecha_ingreso']].head(7))
```

### Ejercicio 3: Estandarización Avanzada de Texto
Después de haber pasado `estado_actual` a minúsculas, reemplazamos todas las ocurrencias de `"dañado"` por `"inactivo"`.
```python
# Ya lo habíamos pasado a minúsculas: df_inventario['estado_actual'] = df_inventario['estado_actual'].str.lower()
df_inventario['estado_actual'] = df_inventario['estado_actual'].str.replace('dañado', 'inactivo')
print("\nEstados estandarizados:")
print(df_inventario[['nombre_equipo', 'estado_actual']].head(5))
```

### Ejercicio 4: Filtrado Post-Limpieza
Generamos un nuevo DataFrame `equipos_costosos` con componentes cuyo `precio_cop` sea estrictamente mayor a 30000 COP y que estén "activos".
```python
# Filtro con doble condición usando el operador & (AND)
equipos_costosos = df_inventario[(df_inventario['precio_cop'] > 30000) & (df_inventario['estado_actual'] == 'activo')].copy()
print("\nEquipos costosos y activos:")
print(equipos_costosos[['nombre_equipo', 'precio_cop', 'estado_actual']])
```

### Ejercicio 5: Limpieza de Categorías Ocultas
Aplicamos `.str.strip()` a toda la columna `categoria` para eliminar los espacios en blanco accidentales que podrían crear redundancias (ej. `" Sensor"` vs `"Sensor"`).
```python
df_inventario['categoria'] = df_inventario['categoria'].str.strip()
print("\nCategorías limpias, frecuencia de datos:")
print(df_inventario['categoria'].value_counts())
```

























## Taller Práctico: Extracción y Filtrado de Datos con Pandas

En esta actividad, aprenderemos cómo extraer exactamente la información que necesitamos de un conjunto de datos. Imagina que Pandas es un colador muy avanzado; hoy aprenderemos a configurar los agujeros de ese colador utilizando el caso de estudio **"EcoGestión PYME"**, enfocado en la gestión ambiental del sector textil en el Valle de Aburrá.

## Fase 1: Preparación del Entorno (VS Code)

Antes de programar, debemos preparar nuestro espacio de trabajo de forma profesional aislando nuestras dependencias.

**Paso 1:** Abre la terminal integrada en VS Code (puedes usar `Ctrl + \`` o `Cmd + \``) y crea una carpeta para el proyecto:
```bash
mkdir analisis_ambiental_textil
cd analisis_ambiental_textil
```

**Paso 2:** Crea el entorno virtual. Esto crea una "burbuja" donde instalaremos Pandas sin afectar el resto de tu computadora.
```bash
python -m venv venv
```

**Paso 3:** Activa el entorno virtual.
* En **Windows**: `venv\Scripts\activate`
* En **macOS/Linux**: `source venv/bin/activate`

**Paso 4:** Instala la librería Pandas y selecciona el intérprete en VS Code.
```bash
pip install pandas
```
*(En VS Code, presiona `Ctrl + Shift + P`, escribe "Python: Select Interpreter" y elige la ruta que termina en "venv").* **Paso 5:** Crea un archivo llamado `filtros_pandas.py` para escribir tu código.

---

## Fase 2: Creación de nuestro Dataset de Estudio

Copia y pega el siguiente código en tu archivo `filtros_pandas.py`. Esta será nuestra base de datos central, simulando métricas ambientales de diferentes empresas.

```python
import pandas as pd
import numpy as np

# 1. Creamos un diccionario con nuestros datos
datos_completos = {
    'id_empresa': [101, 102, 103, 104, 105, 106, 107, 108, 109, 110],
    'nombre': ['Textiles El Valle', 'Hilanderías Aburrá', 'Confecciones La 70', 'Tintorería ColorEco', 
               'Tejidos de la Montaña', 'Cortes San Javier', 'Hilos y Agujas', 'Moda Circular S.A.',
               'Estampados Bello', 'Tintes Itagüí'],
    'municipio': ['Medellín', 'Bello', 'Medellín', 'Itagüí', 'Envigado', 'Medellín', 'Bello', 'Envigado', 'Bello', 'Itagüí'],
    'subsector': ['Confección', 'Hilandería', 'Confección', 'Tintorería', 'Confección', 'Corte', 'Hilandería', 'Confección', 'Estampado', 'Tintorería'],
    'empleados': [45, 120, 15, 85, 200, 10, 55, 30, 40, 110],
    'consumo_agua_m3': [150.5, 400.0, 50.2, 1200.8, 300.0, 20.5, 350.0, 80.0, 190.0, 950.5],
    'emisiones_co2_ton': [12.5, 45.0, 5.0, 80.0, 35.5, 2.0, 40.0, 8.0, 18.5, 75.0],
    'certificacion_iso14001': [False, True, False, True, True, False, False, True, False, False],
    'riesgo_ambiental': ['Medio', 'Bajo', 'Bajo', 'Alto', 'Medio', 'Bajo', 'Medio', 'Bajo', 'Medio', 'Alto'],
    'presupuesto_ambiental_cop': [5000000, 15000000, 1200000, 25000000, 18000000, 800000, 4500000, 9000000, 3000000, 500000],
    'fecha_auditoria': ['2025-01-15', '2025-02-20', '2026-03-10', '2025-11-05', '2026-01-22', '2026-02-18', '2025-08-30', '2026-04-01', '2026-05-15', '2025-12-10'],
    'comentarios_inspector': ['Falta control de residuos', np.nan, 'Excelente manejo', 'Planta de tratamiento en mejora', np.nan, 'Operación pequeña', 'Fuga en tubería principal', 'Procesos óptimos', 'Requiere revisión de químicos', 'ALERTA: Vertimientos no autorizados']
}

# 2. Convertimos el diccionario en un DataFrame
df = pd.DataFrame(datos_completos)

# 3. Formateamos la columna de fechas
df['fecha_auditoria'] = pd.to_datetime(df['fecha_auditoria'])

print("--- DATAFRAME ORIGINAL ---")
print(df.head()) # Muestra las primeras 5 filas
```

---

## Fase 3: Laboratorio de Filtros (Paso a Paso)

Añade los siguientes bloques de código a tu archivo y ejecútalos uno por uno. Lee los comentarios `#` para entender la lógica de cada extracción.

### 3.1 Selección Básica y Localización (`.iloc` y `.loc`)
Antes de establecer condiciones, recordemos cómo ubicar coordenadas exactas.

```python
# Ver múltiples columnas específicas (nota los dobles corchetes)
datos_basicos = df[['nombre', 'municipio', 'riesgo_ambiental']]

# .iloc: Traer las primeras 3 filas por su posición numérica
primeras_tres = df.iloc[0:3]

# .loc: Traer todas las filas (:), pero solo columnas específicas por su nombre
datos_agua_co2 = df.loc[:, ['nombre', 'consumo_agua_m3', 'emisiones_co2_ton']]
```

### 3.2 Máscaras Booleanas (Condicionales Simples)
Creamos una condición que devuelve `True` o `False`. Pandas solo nos mostrará las filas que sean `True`.

```python
print("\n--- 1. EMPRESAS GRANDES (MÁS DE 50 EMPLEADOS) ---")
filtro_empleados = df[df['empleados'] > 50]
print(filtro_empleados[['nombre', 'empleados']])

print("\n--- 2. EMPRESAS DEL SECTOR TINTORERÍA ---")
# Condición de igualdad (usamos doble igual ==)
filtro_tintoreria = df[df['subsector'] == 'Tintorería']
print(filtro_tintoreria[['nombre', 'consumo_agua_m3']])
```

### 3.3 Múltiples Condiciones (`&`, `|`, `~`)
**Reglas de sintaxis en Pandas:**
* "Y" (AND) es `&`
* "O" (OR) es `|`
* "NO" (NOT) es `~`
* ¡Obligatorio encerrar cada condición en paréntesis `()`!

```python
print("\n--- 3. CONDICIÓN AND (&) ---")
# Riesgo alto Y ubicadas en Itagüí
filtro_and = df[(df['riesgo_ambiental'] == 'Alto') & (df['municipio'] == 'Itagüí')]
print(filtro_and[['nombre', 'municipio', 'riesgo_ambiental']])

print("\n--- 4. CONDICIÓN OR (|) ---")
# Presupuesto mayor a 10 millones O certificación ISO activa
filtro_or = df[(df['presupuesto_ambiental_cop'] > 10000000) | (df['certificacion_iso14001'] == True)]
print(filtro_or[['nombre', 'presupuesto_ambiental_cop', 'certificacion_iso14001']])

print("\n--- 5. NEGACIÓN (NOT ~) ---")
# Todas las empresas que NO son de Medellín
filtro_not = df[~(df['municipio'] == 'Medellín')]
print(filtro_not[['nombre', 'municipio']])
```

### 3.4 Filtros de Texto y Listas (`.str` e `.isin()`)
Herramientas vitales para trabajar con categorías y cadenas de caracteres.

```python
print("\n--- 6. FILTRO DE LISTAS (ISIN) ---")
# Buscar múltiples sectores sin usar muchos operadores OR
sectores = ['Hilandería', 'Estampado']
filtro_isin = df[df['subsector'].isin(sectores)]
print(filtro_isin[['nombre', 'subsector']])

print("\n--- 7. FILTROS DE TEXTO (CONTAINS) ---")
# Nombres que contienen "Textil" o "Tejido". 
# case=False ignora mayúsculas/minúsculas. na=False evita errores con nulos.
filtro_texto = df[df['nombre'].str.contains('Textil|Tejido', case=False, na=False)]
print(filtro_texto[['nombre']])
```

### 3.5 Valores Nulos, Rangos y Fechas
En la vida real, los datos vienen incompletos o necesitamos buscar dentro de ventanas de tiempo específicas.

```python
print("\n--- 8. VALORES NULOS (ISNA) ---")
# Empresas sin comentarios del inspector (NaN)
filtro_nulos = df[df['comentarios_inspector'].isna()]
print(filtro_nulos[['nombre', 'comentarios_inspector']])

print("\n--- 9. FILTRO DE RANGOS (BETWEEN) ---")
# Consumo de agua entre 100 y 500 m3
filtro_rango = df[df['consumo_agua_m3'].between(100, 500)]
print(filtro_rango[['nombre', 'consumo_agua_m3']])

print("\n--- 10. FILTRO DE FECHAS ---")
# Auditorías realizadas durante el año 2026 usando el atributo .dt
filtro_año = df[df['fecha_auditoria'].dt.year == 2026]
print(filtro_año[['nombre', 'fecha_auditoria']])
```

### 3.6 Filtros Dinámicos y Avanzados
A veces el filtro depende de los mismos datos (como promedios) o requiere el uso de lenguaje similar a SQL.

```python
print("\n--- 11. FILTRO CONTRA PROMEDIOS ---")
# Consumo de agua MAYOR al promedio general
promedio_agua = df['consumo_agua_m3'].mean()
filtro_dinamico = df[df['consumo_agua_m3'] > promedio_agua]
print(filtro_dinamico[['nombre', 'consumo_agua_m3']])

print("\n--- 12. FILTRO ELEGANTE (.QUERY) ---")
# Permite escribir las condiciones como una sola cadena de texto
filtro_query = df.query("riesgo_ambiental == 'Medio' and empleados < 50")
print(filtro_query[['nombre', 'riesgo_ambiental', 'empleados']])

print("\n--- 13. FILTRAR BASADO EN GRUPOS (GROUPBY.FILTER) ---")
# Conservar solo empresas de municipios donde la suma de emisiones CO2 supera las 50 toneladas
filtro_grupos = df.groupby('municipio').filter(lambda x: x['emisiones_co2_ton'].sum() > 50)
print(filtro_grupos[['nombre', 'municipio', 'emisiones_co2_ton']])
```

---

## Fase 4: Buenas Prácticas y Prevención de Errores

**🚨 Concepto Crítico: El `SettingWithCopyWarning`**
Cuando filtras un DataFrame para crear uno nuevo y planeas modificar ese nuevo DataFrame después, Pandas puede lanzar una alerta de seguridad. Para evitarlo, **siempre** utiliza el método `.copy()` al guardar tu filtro final.

```python
# MALA PRÁCTICA (Puede causar errores si luego modificas df_limpio)
df_limpio = df[df['empleados'] > 20]

# BUENA PRÁCTICA (Crea un objeto totalmente independiente en memoria)
df_limpio = df[df['empleados'] > 20].copy()
```

---

## Fase 5: Ejercicios Resueltos "EcoGestión"

A continuación, se presenta la solución detallada y explicada a cada requerimiento gerencial utilizando las lógicas de extracción de Pandas.

### Ejercicio 1: Las "Peligrosas"
Necesitamos empresas con rango de `riesgo_ambiental` 'Alto' **Y** que **NO** tengan certificación ISO 14001.
```python
# Usamos el operador & para AND, y ~ para la negación en la columna booleana.
empresas_peligrosas = df[(df['riesgo_ambiental'] == 'Alto') & (~df['certificacion_iso14001'])]
print("Empresas de alto riesgo sin ISO 14001:")
print(empresas_peligrosas[['nombre', 'municipio']])
```

### Ejercicio 2: Inconsistencias Financieras
Buscamos empresas con subsector 'Tintorería' **o** 'Estampado' cuyo `presupuesto_ambiental_cop` sea menor a 5.000.000.
```python
# Usamos .isin() para la opción múltiple del subsector, junto con el operador &
inconsistencias = df[(df['subsector'].isin(['Tintorería', 'Estampado'])) & (df['presupuesto_ambiental_cop'] < 5000000)]
print("\nInconsistencias Financieras detectadas:")
print(inconsistencias)
```

### Ejercicio 3: Análisis por Municipio usando Query
Buscamos empresas de **Medellín** o **Bello** con emisiones de CO2 mayores a 10 toneladas, utilizando el poderoso método `.query()`.
```python
# .query() permite escribir la condición como si fuera texto de SQL o Python simple.
analisis_municipal = df.query("municipio in ['Medellín', 'Bello'] and emisiones_co2_ton > 10")
print("\nEmisiones altas en Medellín y Bello:")
print(analisis_municipal[['nombre', 'municipio', 'emisiones_co2_ton']])
```

### Ejercicio 4: Búsqueda Ciega (Expresiones Regulares Simples)
Buscamos empresas cuyo comentario contenga variantes de "alerta" o "químicos", omitiendo si están en mayúsculas o minúsculas.
```python
# .str.contains() junto con el operador lógico OR (|) en formato texto, case=False lo hace insensible a mayúsculas
busqueda_ciega = df[df['comentarios_inspector'].str.contains('alerta|químic', case=False, na=False)]
print("\nInspectores levantaron alertas o advertencias químicas en:")
print(busqueda_ciega[['nombre', 'comentarios_inspector']])
```

### Ejercicio 5: Preparación de Datos Limpios
Creamos un nuevo DataFrame `df_oficial` excluyendo empresas con menos de 20 empleados (es decir, seleccionando las de >= 20), usando `.copy()` para aislar la variable en la memoria.
```python
# .copy() previene el SettingWithCopyWarning de Pandas.
df_oficial = df[df['empleados'] >= 20].copy()
print(f"\nDataFrame Oficial consolidado con {len(df_oficial)} empresas.")
```

---

## Taller Práctico 3: Creación y Análisis Exploratorio de Datos (EDA) (Refuerzo Semanas 7 y 8)

Para consolidar el aprendizaje de la manipulación de arreglos y la lectura analítica (EDA), vamos a crear un conjunto de datos desde cero sobre "Incidencias de red" y a explorar sus valores sin modificar una sola fila.

### Fase 1: Creación del DataFrame de Análisis

Para comenzar, construiremos un log de incidencias uniendo diccionarios de Python y listas. Esto emula la construcción de un archivo procesado listo para inspeccionar.

```python
import pandas as pd

# Creación de datos usando un diccionario con Listas de Python
datos_red = {
    'Fecha': ['2026-03-01', '2026-03-01', '2026-03-02', '2026-03-02', '2026-03-03'],
    'Sistema': ['Router_Core', 'Switch_Piso1', 'Firewall_Main', 'Router_Core', 'Switch_Piso2'],
    'Severidad': ['Alta', 'Baja', 'Critica', 'Media', 'Baja'],
    'Duracion_Mins': [45, 10, 120, 20, 15],
    'Tecnico': ['Carlos', 'Ana', 'Carlos', 'Luis', 'Ana']
}

# Transformación de los datos a DataFrame
df_incidencias = pd.DataFrame(datos_red)
print("--- DATAFRAME DE INCIDENCIAS CREADO ---")
print(df_incidencias)
```

### Fase 2: Inspección Estructural (Semanas 7 y 8)
Usaremos las herramientas integradas para conocer el tamaño y distribución de tipos de datos. Estas observaciones puras nos servirán de guía antes de modelar bases de datos.

```python
print("\n1. Información Estructural (df.info()):")
df_incidencias.info()

print("\n2. Observación de Muestra Aleatoria (df.sample(2)):")
# .sample(n) escoge 'n' filas al azar, ideal para no solo ver lo del inicio/final.
print(df_incidencias.sample(2))
```

### Fase 3: Sondeo de Categorías y Generación de Frecuencias
A veces necesitamos saber **cuántas incidencias** hay por nivel de severidad. Las herramientas de estadística nos ayudan a ver esto.

```python
print("\n3. Distribución de Niveles de Severidad (value_counts):")
# value_counts() suma cuántas ocurrencias hay de cada categoría única en la columna.
print(df_incidencias['Severidad'].value_counts())

print("\n4. Listado Único de Sistemas Involucrados (unique):")
print(df_incidencias['Sistema'].unique())
```

### Fase 4: Estadísticas Descriptivas (Semana 8)
Analizamos la duración (una columna de números), calculando la media, mínimo y el sumatorio agrupado por técnicos para saber quién trabajó más tiempo atendiendo los eventos.

```python
print("\n5. Perfil Numérico (describe) de Duración de Incidencias:")
# Genera métricas clave solo de las columnas numéricas.
print(df_incidencias.describe())

print("\n6. Relación Agrupada: Tiempo total de resolución por Técnico (groupby):")
# En el modo EDA, queremos sumar el tiempo que tardó cada elemento.
tiempo_tecnicos = df_incidencias.groupby('Tecnico')['Duracion_Mins'].sum()
print(tiempo_tecnicos)
```

Con la finalización de estos talleres solucionados, tienes en conocimiento completo del flujo del análisis que comprende desde la creación/lectura, al saneamiento, los filtrados lógicos y finalmente el Análisis Exploratorio de Datos (EDA).

---
