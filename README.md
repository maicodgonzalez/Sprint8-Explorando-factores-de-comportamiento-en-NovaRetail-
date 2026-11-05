# Sprint8-Explorando-factores-de-comportamiento-en-NovaRetail-
Este repositorio contiene el análisis durante el Sprint 8 NovaRetail+ es una plataforma de comercio electrónico en Latinoamérica con millones de usuarios. Para el cierre de este año 2024, el equipo de Crecimiento y Retención busca entender:
¿Qué factores del comportamiento del cliente están más fuertemente asociados con el ingreso anual generado?


Contenido del repositorio
Notebook principal con limpieza, distribuciones, valores atípicos y conclusiones.

🧠 Objetivo del análisis
Integrar múltiples técnicas de correlación en un solo análisis.
Identificar relaciones significativas entre variables mediante el uso de scatterplots y heatmaps.
Detectar correlaciones engañosas.
Documentar supuestos y limitaciones.
Convertir hallazgos en recomendaciones de negocio.

## 📌 Descripción del proyecto

**NovaRetail+** es una plataforma de comercio electrónico con millones de usuarios en Latinoamérica. Para el cierre de 2024, el equipo de **Crecimiento y Retención** necesita responder una pregunta clave:

> **¿Qué factores del comportamiento del cliente están más fuertemente asociados con el ingreso anual generado?**

Este proyecto construye un análisis correlacional estructurado que combina variables de comportamiento, segmentación y valor económico, **evitando interpretaciones causales incorrectas**.
<img width="340" height="280" alt="image" src="https://github.com/user-attachments/assets/ffbbaf10-3919-4639-9645-46a8d5e86d3e" />

## 🎯 Objetivos

- Integrar múltiples técnicas de correlación en un solo análisis.
- Identificar relaciones significativas mediante *scatterplots* y *heatmaps*.
- Detectar correlaciones engañosas y posibles variables de confusión.
- Documentar supuestos y limitaciones.
- Convertir hallazgos en recomendaciones de negocio.
- Redactar un reporte ejecutivo profesional.

## 🔥 Matriz de correlación

Se calculó la matriz de correlación de Pearson entre las variables numéricas continuas y se visualizó con un *heatmap* para identificar rápidamente qué variables se asocian más con `ingreso_anual`.

![Heatmap de correlaciones](images/heatmap_correlaciones.png)

### Hallazgos principales

| Variable | Correlación con `ingreso_anual` | Interpretación |
|---|---|---|
| `compras_mes` | **0.97** | Asociación muy fuerte y positiva |
| `visitas_mes` | 0.34 | Asociación moderada y positiva |
| `gasto_publicidad_dirigida` | 0.20 | Asociación débil y positiva |
| `satisfaccion` | 0.056 | Prácticamente nula |
| `edad` | 0.017 | Sin relación lineal |
| `nivel_ingreso` | 0.017 | Sin relación lineal |

**1. `compras_mes` es el principal factor asociado al ingreso anual (r = 0.97).**
Los clientes que realizan más compras al mes tienden a generar un ingreso anual considerablemente mayor. Es una relación esperable, ya que las compras alimentan directamente el ingreso, por lo que conviene verificar que no exista redundancia entre ambas variables (ver sección de limitaciones).

**2. `visitas_mes` muestra una relación moderada (r = 0.34).**
Más visitas se asocian con mayor ingreso, pero su efecto parece operar sobre todo a través de las compras (`visitas_mes` y `compras_mes` correlacionan en 0.35).

**3. `gasto_publicidad_dirigida` tiene una relación débil con el ingreso (r = 0.20) pero fuerte con las visitas (r = 0.58).**
La publicidad dirigida parece estar más ligada a la generación de tráfico que al ingreso directo. Este patrón sugiere una posible cadena: *publicidad → visitas → compras → ingreso*, que debe validarse con experimentos.

**4. `satisfaccion`, `edad` y `nivel_ingreso` no muestran relación lineal relevante con el ingreso anual** (|r| < 0.06). Esto no descarta relaciones no lineales, que se explorarán con *scatterplots*.

### ⚠️ Consideraciones

- **Correlación ≠ causalidad:** estos coeficientes describen asociaciones, no efectos causales.
- **Posible correlación engañosa:** la correlación de 0.97 entre `compras_mes` e `ingreso_anual` puede deberse a que el ingreso se calcula a partir de las compras. Más que un "driver" independiente, podría ser una relación casi mecánica.
- **Solo variables numéricas continuas:** las variables binarias (`miembro_premium`, `abandono`) y categóricas (`tipo_dispositivo`, `region`) se analizan por separado.
- **Pearson mide relaciones lineales:** se complementará con *scatterplots* para detectar patrones no lineales o valores atípicos.

🛠️ Herramientas de la lección
Jupyter Notebook
Python: pandas, numpy, seaborn, matplotlib
