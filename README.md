# Proyecto Final — IA 1
## Mantenimiento Predictivo de Maquinaria Industrial

> **Curso:** IA1 — Grupo C2 2026-1  
> **Integrantes** Juan Cardenas - Jose Erazo - Javier Patiño
> **Dataset:** AI4I 2020 Predictive Maintenance (UCI Machine Learning Repository)  
> **Problema:** Clasificación binaria — predecir fallas de maquinaria industrial antes de que ocurran



---

## Contenido del repositorio

```
├── ProyectoIA (3).ipynb 
├── ai 2020.csv   
├── dataset.ipynb  
├── proyecto_final_IA.ipynb                   
└── README.md                     
```

---

## Dataset

### ¿Qué datos se usaron?

**AI4I 2020 Predictive Maintenance Dataset**  
Simulación de sensores de una máquina industrial con 10,000 registros y 14 columnas.

| Variable | Tipo | Descripción |
|----------|------|-------------|
| `Type` | Categórica (H/L/M) | Calidad del producto: High / Low / Medium |
| `air_temp` | Numérica [K] | Temperatura del aire |
| `process_temp` | Numérica [K] | Temperatura del proceso |
| `rot_speed` | Numérica [rpm] | Velocidad de rotación |
| `torque` | Numérica [Nm] | Torque aplicado |
| `tool_wear` | Numérica [min] | Desgaste de la herramienta |
| **`machine_failure`** | **Binaria (0/1)** | **Variable objetivo: 0 = sin falla, 1 = con falla** |

### ¿Dónde están los datos?

El notebook carga los datos de **dos formas** automáticamente (con fallback):

#### Opción 1 — Descarga automática desde UCI (requiere internet)
El notebook intenta cargar el dataset desde la fuente oficial:
```
https://archive.ics.uci.edu/ml/machine-learning-databases/00601/ai4i2020.csv
```
No es necesario hacer nada, el notebook lo descarga solo al ejecutar la celda de carga.

#### Opción 2 — Archivo local (sin internet / fallback automático)
Si la URL no está disponible, el notebook carga el archivo local incluido en este repositorio:
```
ai 2020.csv
```
**Si usas Google Colab:** sube el archivo `ai 2020.csv` al entorno de Colab antes de ejecutar (panel izquierdo → ícono de carpeta → subir archivo).

#### Descarga manual del dataset
Si necesitas descargarlo manualmente:
1. Ve a: **https://archive.ics.uci.edu/dataset/601/ai4i+2020+predictive+maintenance+dataset**
2. Haz clic en **"Download"**
3. Extrae el archivo `.csv` y colócalo en la misma carpeta que el notebook con el nombre `ai 2020.csv`

---
## Estructura del Notebook

El notebook está organizado en **5 secciones** que cubren todos los criterios de la rúbrica:

### Sección 1 — Planteamiento del Problema
- Contexto: costos de mantenimiento reactivo vs predictivo
- Definición del problema de clasificación binaria
- Justificación de la métrica primaria: **Recall** (detectar todas las fallas reales es más importante que evitar falsas alarmas)

### Sección 2 — Análisis Exploratorio (EDA)
- Distribuciones de variables numéricas
- Análisis del desbalance de clases (96.6% sin falla / 3.4% con falla)
- Matriz de correlación
- Pairplot de separabilidad
- Boxplots por variable vs `machine_failure`

### Sección 3 — Aprendizaje Supervisado
Entrenamiento y comparación de **5 modelos**:

| Modelo | Datos usados | Nota clave |
|--------|-------------|------------|
| Gaussian Naive Bayes | Sin escalar | Baseline de comparación |
| SVM (RBF) | Escalados | `class_weight='balanced'` — mejor Recall |
| Decision Tree | Sin escalar | Visualización del árbol incluida |
| Random Forest | Sin escalar | Feature importance incluida |
| Red Neuronal (DNN) | Escalados | Keras Sequential, curva de aprendizaje |

- Tabla comparativa de métricas (Accuracy, Recall, Precision, F1, Specificity)
- Curvas ROC-AUC de todos los modelos
- Validación cruzada estratificada 5-Fold

### Sección 4 — Aprendizaje No Supervisado + Reducción Dimensional

**Reducción de dimensionalidad:**
- **PCA** — varianza explicada, proyección 2D, componentes principales
- **t-SNE** — perplexity=30, comparación visual con PCA

**Clustering:**
- **K-means** — Método del codo + Silhouette Score para K óptimo
- **DBSCAN** — K-distance graph para selección de `eps`, análisis de ruido/anomalías
---


