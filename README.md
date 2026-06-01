# 🛒 Customer Segmentation — RFM + Clustering

Segmentación de clientes de una empresa de retail online del Reino Unido usando análisis RFM y algoritmos de clustering no supervisado, con el objetivo de diseñar estrategias de fidelización personalizadas por segmento.

---

## 📌 Contexto del negocio

Una empresa minorista online con sede en el Reino Unido, cuyos clientes incluyen tanto consumidores individuales como mayoristas internacionales, necesitaba una forma de distinguir entre sus distintos tipos de compradores para optimizar sus campañas de marketing y retención.

El problema central era la ausencia de una segmentación clara: sin ella, el presupuesto de marketing se distribuía de forma homogénea entre clientes con comportamientos y niveles de valor muy diferentes.

---

## 🎯 Objetivo

Segmentar la base de clientes a partir de sus métricas de comportamiento de compra (**RFM**) y aplicar técnicas de clustering para identificar grupos homogéneos sobre los cuales diseñar estrategias de fidelización accionables.

---

## 📊 Dataset

- **Fuente:** [UCI Machine Learning Repository — Online Retail II](https://archive.ics.uci.edu/dataset/502/online+retail+ii)
- **Período:** Diciembre 2009 – Diciembre 2011
- **Registros originales:** 1.067.371 transacciones
- **Variables:** Invoice, StockCode, Description, Quantity, InvoiceDate, Price, Customer ID, Country

---

## ⚙️ Pipeline

```
Datos crudos
    │
    ▼
Limpieza (nulos, duplicados, cancelaciones, registros administrativos)
    │
    ▼
Construcción de Matriz RFM (5.861 clientes únicos)
    │   • Recency  — días desde última compra
    │   • Frequency — facturas únicas por cliente
    │   • Monetary  — total gastado en £
    ▼
Separación de outliers (Z-score > 3)
    │
    ▼
Escalamiento (StandardScaler)
    │
    ▼
Entrenamiento y comparación de modelos
    │
    ▼
Perfilado de segmentos + estrategias de marketing
```

---

## 🤖 Modelos evaluados

| Modelo | Silhouette k=2 | Silhouette k=3 | Silhouette k=4 |
|---|:---:|:---:|:---:|
| **K-Means** | **0.6895** | 0.5405 | 0.5603 |
| Aglomerativo | — | 0.4823 | 0.4906 |
| MiniBatch K-Means | — | 0.5406 | 0.5562 |
| GMM | — | 0.2215 | 0.3217 |

> **Modelo seleccionado:** K-Means con k=4 (Silhouette: 0.5603) sobre la matriz RFM estándar. Se eligió k=4 sobre k=2 porque genera segmentos más accionables para el negocio, con perfiles diferenciados y estrategias específicas por grupo.

---

## 👥 Segmentos identificados

| Cluster | Perfil | Característica principal |
|---|---|---|
| 0 | Clientes inactivos | Alta recencia, baja frecuencia y valor |
| 1 | Clientes recientes de bajo valor | Compra reciente pero poco gasto |
| 2 | Clientes frecuentes | Alta frecuencia, valor monetario medio |
| 3 | Clientes de alto valor | Baja recencia, alta frecuencia y gasto |

---

## 🛠️ Tecnologías

![Python](https://img.shields.io/badge/Python-3.10-blue)
![Pandas](https://img.shields.io/badge/Pandas-2.x-150458?logo=pandas)
![Scikit-learn](https://img.shields.io/badge/Scikit--learn-1.x-F7931E?logo=scikit-learn)
![Seaborn](https://img.shields.io/badge/Seaborn-0.13-4C72B0)
![Google Colab](https://img.shields.io/badge/Google_Colab-notebook-F9AB00?logo=googlecolab)

- `pandas`, `numpy` — manipulación y transformación de datos
- `scikit-learn` — KMeans, AgglomerativeClustering, MiniBatchKMeans, DBSCAN, GaussianMixture, PCA, StandardScaler, GridSearchCV
- `scipy` — detección de outliers (Z-score)
- `matplotlib`, `seaborn` — visualización

---

## 🚀 Cómo correr el notebook

1. Abrir `Entrega_4.ipynb` en Google Colab
2. Ejecutar las celdas en orden — el dataset se carga automáticamente desde Google Sheets
3. No se requiere configuración adicional ni credenciales

---

## 👨‍💻 Equipo

- Miguel Alejandro Bermúdez
- Jose Ricardo Cepeda
- Santiago Giraldo
