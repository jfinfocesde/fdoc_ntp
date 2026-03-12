---
title: "Semana 5: Entornos, Dependencias y Ejemplos Prácticos"
description: "Gestión de entornos virtuales, dependencias con pip, manejo de Excel y chat con IA (Gemini)."
position: 5
---

# Tutoriales y Ejemplos Prácticos

En esta sección consolidamos los conocimientos sobre gestión de entornos de desarrollo y exploramos aplicaciones prácticas con bases de datos en Excel e Inteligencia Artificial.

---

## 1. Entornos Virtuales en Python

Los entornos virtuales son una herramienta esencial para gestionar las dependencias de tus proyectos. Permiten crear un espacio aislado para cada proyecto, evitando conflictos entre las librerías.

### **¿Para qué sirven?**

* **Aislamiento de dependencias:** Cada proyecto puede tener sus propias versiones de librerías.
* **Control de versiones:** Asegura la compatibilidad entre diferentes versiones de un mismo proyecto.
* **Simplificación:** Facilita la instalación y actualización de librerías específicas.

### **Creación de un entorno virtual:**

```bash
python -m venv .venv
```

### **Activación del entorno:**

```tabs
---[tab title="Windows" lang="bash"]---
.venv\Scripts\activate

---[tab title="Linux/macOS" lang="bash"]---
source .venv/bin/activate
```

### **Desactivación:**
```bash
deactivate
```

---

## 2. Gestión de Dependencias con pip

Trabajar en un entorno virtual facilita instalar, actualizar y reproducir dependencias de forma controlada.

### **Operaciones básicas**

- **Instalar un paquete**:
  ```bash
  pip install <paquete>
  ```
- **Desinstalar**:
  ```bash
  pip uninstall <paquete>
  ```
- **Ver paquetes instalados**:
  ```bash
  pip list
  # o para el formato de requisitos:
  pip freeze
  ```

### **Congelar e instalar desde `requirements.txt`**

- **Guardar dependencias del proyecto**:
  ```bash
  pip freeze > requirements.txt
  ```
- **Reproducir el entorno en otra máquina**:
  ```bash
  pip install -r requirements.txt
  ```

---

## 3. Ejemplo Práctico: Automatización de Excel

Este ejemplo muestra cómo agregar una fila a un archivo `asistencia.xlsx` usando la librería `openpyxl`.

### **Preparación**
```bash
pip install openpyxl
```

### **Código (asistencia.py)**
```python
import openpyxl

# Cargar el libro y la hoja
workbook = openpyxl.load_workbook("asistencia.xlsx")
sheet = workbook["Asistencia"]

# Insertar nueva fila al final
last_row = sheet.max_row
sheet.insert_rows(last_row + 1)

# Capturar datos
nombre = input("Ingrese su nombre: ")
fecha = input("Ingrese la fecha (AAAA-MM-DD): ")
hora = input("Ingrese la hora de entrada (HH:MM): ")

# Asignar valores
sheet.cell(row=last_row + 1, column=1).value = nombre
sheet.cell(row=last_row + 1, column=2).value = fecha
sheet.cell(row=last_row + 1, column=3).value = hora

# Guardar cambios
workbook.save("asistencia.xlsx")
```

---

## 4. Chat en Consola con Gemini AI

Crea un chat de consola utilizando la librería oficial `google-genai` y el modelo `gemini-2.5-flash`.

### **Requisitos**
```bash
pip install -q -U google-genai
```

### **Código de ejemplo**
```python
from google import genai

def generar_respuesta(prompt: str) -> str:
    if not prompt:
        return "Por favor, ingresa un tema o pregunta."
    try:
        client = genai.Client(api_key="YOUR_API_KEY")
        response = client.models.generate_content(
            model="gemini-2.5-flash", contents=prompt
        )
        return response.text
    except Exception as e:
        return f"Error: {str(e)}"

print("--- Chat con Gemini ---")
print("Escribe 'salir' para terminar.\n")

while True:
    prompt = input("Tú: ").strip()
    if prompt.lower() == 'salir':
        break
    if prompt:
        print("Generando respuesta...\n")
        respuesta = generar_respuesta(prompt)
        print(f"Gemini: {respuesta}\n")
        print("="*50 + "\n")
```

---

## Notas y Recomendaciones Finales

1. **Seguridad**: Nunca subas tus `API_KEY` a repositorios públicos (GitHub). Usa variables de entorno.
2. **Buenas Prácticas**: Siempre activa tu entorno virtual (`.venv`) antes de instalar cualquier librería.
3. **Persistencia**: Recuerda actualizar habitualmente tu archivo `requirements.txt`.

