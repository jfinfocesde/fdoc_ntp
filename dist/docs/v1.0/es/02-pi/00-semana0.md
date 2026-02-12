---
title: "Proyecto Integrador"
description: ""
position: 0
---

### ENUNCIADO DEL PROYECTO INTEGRADOR  
- **Programa:** Técnico en Desarrollo de Software – CESDE  
- **Nombre del proyecto:** Plataforma Interactiva de Análisis y Visualización de Datos Empresariales (PIA-VDE)  
- **Modalidad:** Proyecto Integrador grupal.
- **Fecha de entrega final:** Semana 17



+++gallery
---
columns: 3
items:
  - src: "https://iili.io/q9liDut.png"
    alt: "Pueblo en un lago" 
---
+++


### 1. Descripción general del proyecto
El grupo desarrollará una **solución integral moderna** compuesta por tres frentes tecnológicos que se comunican entre sí mediante una **API REST centralizada**. El objetivo es crear una plataforma que permita a una empresa mediana (ejemplo: comercio minorista, servicios o manufactura ligera) cargar, gestionar y analizar sus datos de ventas/operaciones de forma interactiva, combinando:

- Un **backend robusto y escalable** (API REST)
- Un **frontend moderno y responsive** para usuarios administrativos y gerenciales
- Un **dashboard analítico interactivo** enfocado en exploración y visualización de datos

La solución debe demostrar integración efectiva entre las tres tecnologías aprendidas en los submódulos correspondientes.

### 2. Submódulos y tecnologías obligatorias

| Submódulo                          | Tecnología principal                  | Responsabilidad principal del submódulo                                                                 | Rol en la integración                                                                 |
|------------------------------------|----------------------------------------|----------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------|
| **Backend 2**                      | Spring Boot (Java) + API RESTful      | Crear una **API REST completa**, segura y documentada (con Swagger/OpenAPI)                              | Núcleo central – provee todos los datos y lógica de negocio a los otros dos frentes   |
| **Nueva Tecnologías de Programación** | Python + Streamlit + Pandas + (Plotly / Matplotlib / Seaborn) | Desarrollar una **aplicación web analítica interactiva** de exploración y visualización de datos       | Consume la API para obtener datos limpios y mostrar dashboards dinámicos              |
| **Programación para la Web 2**     | React (Vite recomendado) + Tailwind CSS + (Axios o TanStack Query) | Construir una **interfaz de usuario moderna**, responsive y con buena experiencia de usuario (UX)     | Consume la API para realizar CRUD y mostrar vistas operativas / gerenciales           |

### 3. Dominio y funcionalidades mínimas obligatorias (MVP)

**Tema sugerido (puede ajustarse):** Gestión y análisis de ventas de una cadena de tiendas de ropa / minimercado / repuestos automotrices / servicios técnicos (elegir uno concreto).

Funcionalidades transversales mínimas que deben estar presentes en **al menos dos** de los frentes (idealmente en los tres):

1. Autenticación básica (login / registro) → JWT recomendado en backend
2. Gestión de productos/artículos (CRUD)
3. Registro y consulta de ventas/transacciones (CRUD)
4. Gestión básica de clientes o proveedores (CRUD mínimo)
5. Visualización de reportes / métricas clave:
   - Ventas por período (día, semana, mes)
   - Producto más vendido / menos vendido
   - Ventas por categoría / sucursal (si aplica)
   - Tendencias mensuales / comparativos año anterior
   - Gráficos interactivos (barras, líneas, pastel, heatmaps, etc.)

### 4. Arquitectura general de la solución

```txt
                  +---------------------+  
                  |  Frontend React     |  
                  |  + Tailwind CSS     |  
                  +----------▲----------+  
                             │   (consume API)
                             ▼
+-------------------------------------------+     +-------------------------------+
|               API REST Spring Boot        |◄────┤  Dashboard Streamlit (Python) |
|  - JPA / Hibernate                        |     |  - Pandas                     |
|  - Spring Security + JWT                  |     |  - Plotly / Altair            |
|  - MySQL / PostgreSQL / H2                |     +-------------------------------+
|  - Documentación Swagger                  |
+-------------------------------------------+
                Base de datos
```

### 5. Entregables mínimos obligatorios (por submódulo y generales)

- Repositorio Git organizado (frontend, backend, streamlit en carpetas separadas o repositorios separados con README que explique integración)
- Documentación técnica básica:
  - Diagrama de arquitectura (C4, diagrama de componentes o similar)
  - Endpoints de la API documentados (Swagger + tabla resumen)
  - Instrucciones claras de instalación y ejecución de cada módulo
- Video corto (3-7 min) mostrando la integración completa funcionando
- Presentación final (10-15 diapositivas) explicando: problema, solución, tecnologías, retos superados y lecciones aprendidas

### 6. Criterios de evaluación principales (sugeridos)

- Integración efectiva entre los tres módulos (la API es consumida correctamente por React y por Streamlit)
- Calidad y limpieza del código (convenciones, comentarios útiles, estructura)
- Buenas prácticas en cada tecnología (componentes reutilizables en React, endpoints REST bien diseñados, buen uso de Pandas/Streamlit)
- Experiencia de usuario (UI/UX) en frontend y en dashboard analítico
- Manejo de errores y validaciones
- Seguridad básica implementada (autenticación, protección de rutas)
- Documentación clara y profesional

