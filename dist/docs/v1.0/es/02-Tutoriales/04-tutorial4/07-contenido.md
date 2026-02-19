---
title: "Gestión de secretos (st.secrets)"
position: 7
date: 2025-11-11
---

## Por qué usar secretos

Nunca guardes credenciales sin cifrar en tu repositorio. Streamlit ofrece `st.secrets` para almacenar y acceder a secretos de forma segura, ya sea en un archivo global o por proyecto.

## Configuración local

- Archivo global (Windows): `%userprofile%/.streamlit/secrets.toml`
- Archivo por proyecto: `./.streamlit/secrets.toml`

Añade este archivo a tu `.gitignore` para evitar comprometer credenciales.

### Ejemplo de `secrets.toml`

```bash
db_username = "Jane"
db_password = "mypassword"

[my_other_secrets]
things_i_like = ["Streamlit", "Python"]
```

### Acceso a secretos en la app

```python
import streamlit as st
import os

st.write("Usuario:", st.secrets["db_username"])  # dict-like
st.write("Password:", st.secrets["db_password"])  # dict-like

# Variables de entorno (root-level)
st.write(
    "Env coincide:", os.environ.get("db_username") == st.secrets["db_username"]
)

# Secciones como atributos (TOML)
# [db_credentials]
# username = "my_username"
# password = "my_password"
# my_db.connect(**st.secrets.db_credentials)
```

## Errores comunes y soluciones

- Crear `secrets.toml` mientras el server está corriendo: reinicia el server para que tome cambios.
- `FileNotFoundError`: no existe `secrets.toml`; crea el archivo en la ruta correcta.
- `KeyError`: intentas acceder a una clave que no existe; revisa nombres.

## En despliegue (Streamlit Community Cloud)

Además del archivo local, configura tus secretos en el panel de Secrets de la nube para que estén disponibles en producción.

## Referencia oficial

Consulta la documentación de gestión de secretos:
https://docs.streamlit.io/develop/concepts/connections/secrets-management