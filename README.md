# BIY7121-ev1



# 🚢 Proyecto DataTrans: Análisis Exploratorio Climático (CRISP-DM) 🌦️

> **Minería de Datos - Evaluación 1** > **Docente:** Jazna Meza Hidalgo | **Versión:** 1.0 (Marzo 2026)

Bienvenido al repositorio oficial del proyecto de análisis de datos climáticos para la naviera **DataTrans**. Este proyecto aplica las fases iniciales de la metodología estándar de la industria **CRISP-DM** (Comprensión del Negocio y Comprensión de los Datos) para evaluar y mitigar los riesgos operativos causados por fenómenos meteorológicos en los puertos del sur de Chile.

---

## 📑 Índice

1. [Contexto y Problema de Negocio](#1-contexto-y-problema-de-negocio)
2. [Indicadores Clave de Rendimiento (KPIs)](#2-indicadores-clave-de-rendimiento-kpis)
3. [Descripción del Dataset](#3-descripción-del-dataset)
4. [Insights Clave (EDA)](#4-insights-clave-eda)
5. [Auditoría y Calidad de Datos](#5-auditoría-y-calidad-de-datos)
6. [Pipeline de Preprocesamiento Propuesto](#6-pipeline-de-preprocesamiento-propuesto)
7. [Próximos Pasos (Fases Posteriores)](#7-próximos-pasos-fases-posteriores)
8. [Stack Tecnológico](#8-stack-tecnológico)
9. [Autores](#9-autores)

---

## 1. Contexto y Problema de Negocio 🌊

La empresa naviera **DataTrans** opera en los exigentes canales del sur de Chile. La continuidad operativa de su flota se ve constantemente amenazada por la geografía y el clima extremo de la región:
* **Vientos fuertes:** Impiden las maniobras seguras de atraque de las embarcaciones.
* **Alta nubosidad y neblina:** Reducen drásticamente la visibilidad.
* **Consecuencia:** Cierres de puertos ordenados por la Armada de Chile, lo que genera cuellos de botella logísticos y pérdidas económicas.

Este proyecto busca transformar datos meteorológicos históricos en inteligencia de negocios para optimizar la planificación logística y anticipar ventanas climáticas seguras.

---

## 2. Indicadores Clave de Rendimiento (KPIs) 🎯

Para medir el impacto del clima en la operación, se han definido dos KPIs estratégicos:

* 📉 **KPI 1: Porcentaje de barcos con Retraso por Ventana Climática (TRVC)**
  * *Métrica:* Mide la proporción de naves que, al llegar a su ventana de atraque (simulada a las 08:00 AM), encuentran el puerto cerrado.
  * *Condición de cierre:* Viento > 30 km/h o Lluvia intensa > 1 mm/h.
* ⚓ **KPI 2: Capacidad Efectiva de Puerto (CEP)**
  * *Métrica:* Mide la disponibilidad real de operación para maniobras de carga/descarga.
  * *Factores limitantes:* Viento, precipitación y neblina (Humedad relativa > 95%).

---

## 3. Descripción del Dataset 📊

Los datos corresponden a observaciones meteorológicas horarias de 2025 extraídas vía API, abarcando un total de **33.024 registros** perfectamente balanceados entre 4 localidades estratégicas:

* 📍 **Localidades:** Concepción, Temuco, Valdivia, Punta Arenas (8.256 registros c/u).
* 🌡️ **Variables principales:** Temperatura, Velocidad del viento (`wind_speed_10m`), Precipitación, Humedad relativa y Cobertura nubosa.

---

## 4. Insights Clave (EDA) 💡

El Análisis Exploratorio de Datos reveló patrones críticos para la toma de decisiones logísticas:

1. **El punto de inflexión del viento:** El análisis temporal demuestra que las mañanas (antes de las 11:00 AM) son estadísticamente más seguras para el atraque. Pasado el mediodía, las ráfagas de viento aumentan considerablemente, elevando el riesgo operativo.
2. **El desafío de la visibilidad en el Sur:** Al filtrar las horas con cobertura nubosa crítica (>80%), se evidenció que los puertos de **Punta Arenas** y **Valdivia** sufren las peores condiciones de visibilidad. La logística en estas latitudes exige protocolos distintos a los de Concepción.

---

## 5. Auditoría y Calidad de Datos 🛠️

Se realizó un riguroso escrutinio del dataset para garantizar su confiabilidad:
* ✅ **Valores Nulos:** 0 datos faltantes. Continuidad temporal garantizada.
* ✅ **Duplicados:** 0 filas totalmente duplicadas.
* ⚠️ **Valores Atípicos (Outliers):** Se detectaron extremos climatológicos, particularmente en la velocidad del viento (ráfagas sobre 60 km/h) y temperatura. Estos no son errores, sino los eventos climáticos críticos que el modelo debe aprender a predecir.

---

## 6. Pipeline de Preprocesamiento Propuesto ⚙️

Para evitar sesgos y preparar los datos para Machine Learning, se estructuró la siguiente rutina de limpieza:

1. **Transformación Temporal:** Conversión a formato `datetime` explícito y extracción de mes/hora.
2. **Eliminación de Duplicados Espacio-temporales:** Para evitar sobreajuste (overfitting).
3. **Imputación Continua:** Uso de interpolación lineal respetando la serie de tiempo para futuras ingestas de datos nulos.
4. **Capping de Atípicos:** Aplicación de recorte vía Rango Intercuartílico (IQR) para limitar valores físicamente imposibles, reteniendo los temporales extremos reales.
5. **One-Hot Encoding:** Para variables cualitativas (`Localidad`), evitando sesgos de jerarquía espacial.

---

## 7. Próximos Pasos (Fases Posteriores) 🚀

En base a los resultados obtenidos, el roadmap del proyecto avanza hacia la predicción automatizada:

* **Fase 3 (Ingeniería de Características):** Creación de *lag features* (rezagos de 3, 6 y 12 hrs) para capturar la inercia del clima.
* **Fase 4 (Modelado Predictivo):** Separación temporal de datos (evitando data leakage) y entrenamiento de algoritmos basados en árboles (Random Forest / XGBoost) o redes recurrentes (LSTM) para clasificar alertas.
* **Fase 5 (Despliegue):** Integración de los modelos predictivos en un **Dashboard Interactivo** (Streamlit/Power BI) para la monitorización de alertas tempranas en tiempo real.

---

## 8. Stack Tecnológico 💻

* **Lenguaje:** Python 3.x
* **Análisis y Manipulación:** Pandas, NumPy, SciPy
* **Visualización:** Matplotlib, Seaborn
* **Entorno:** Jupyter Notebook / Deepnote

---

## 9. Autores 👥

Equipo de Ingeniería y Minería de Datos:

* **Javier Cerna** ([ja.cernac@duocuc.cl](mailto:ja.cernac@duocuc.cl))
* **Joaquin Cabrera** ([joac.cabrerac@duocuc.cl](mailto:joac.cabrerac@duocuc.cl))
* **Israel Delpino** ([is.delpino@duocuc.cl](mailto:is.delpino@duocuc.cl))