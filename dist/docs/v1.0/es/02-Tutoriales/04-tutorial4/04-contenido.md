---
title: "Estructura y despliegue"
position: 4
date: 2025-11-11
---

## Estructura recomendada

```bash
streamlit-app/
├── app.py
├── pages/
│   ├── 01_Exploracion.py
│   └── 02_Resumenes.py
├── data/
│   └── ejemplo.csv
└── requirements.txt
```

## Ejecutar en local

```bash
pip install -r requirements.txt
streamlit run app.py
```

## Buenas prácticas

- Usar `st.cache_data` para cachear lecturas de archivos grandes.
- Separar páginas en la carpeta `pages/` para modularidad.
- Mantener transformaciones dentro del alcance de contenidos básicos cuando el objetivo sea comprensión de datos.

## Despliegue rápido

- **Streamlit Community Cloud**: subir el repo y seleccionar `app.py` como entrypoint.
- **Render** o **Railway**: usar un `requirements.txt` y un comando de start `streamlit run app.py --server.port $PORT --server.address 0.0.0.0`.