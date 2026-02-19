---
title: "Servir archivos estáticos"
position: 8
date: 2025-11-11
---

## ¿Para qué sirve?

Permite alojar y servir archivos estáticos pequeños (imágenes, fuentes, PDFs, JSON) para enriquecer tu app en casos donde los elementos estándar no cubren ciertas necesidades.

## Activar el servicio de estáticos

Crea `./.streamlit/config.toml` y habilita la opción:

```bash
[server]
enableStaticServing = true
```

## Estructura y URL

- Coloca archivos en la carpeta `./static/` relativa al archivo principal (`app.py`).
- Se sirven en la ruta `app/static/<filename>`, por ejemplo: `http://localhost:8501/app/static/cat.png`.

## Extensiones soportadas

- Imágenes: `.jpg`, `.jpeg`, `.png`, `.gif`
- Fuentes: `.otf`, `.ttf`, `.woff`, `.woff2`
- Otros: `.pdf`, `.xml`, `.json`

Otros tipos se entregan como `text/plain` por seguridad.

## Ejemplo de uso

```python
import streamlit as st

st.title("Ejemplo estáticos")
st.markdown("[![Click](app/static/cat.png)](https://streamlit.io)")
```

## Consideraciones en la nube

- En Community Cloud, los archivos del repositorio se sirven; los generados en tiempo de ejecución no se garantizan entre sesiones.
- Muchas o grandes cantidades de archivos pueden superar límites de recursos y detener la app.

## Referencias y configuración

Más detalles en:
https://docs.streamlit.io/develop/concepts/configuration/serving-static-files

Configuración general:
https://docs.streamlit.io/develop/concepts/configuration