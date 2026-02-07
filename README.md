# 🚗 Clasificación de Vueltas de Fórmula 1 mediante Algoritmos de Clustering

Este proyecto implementa un **modelo de Inteligencia Artificial basado en aprendizaje no supervisado** para agrupar vueltas de pilotos de Fórmula 1 durante el GP de España 2025.  

El enfoque se centra en aplicar técnicas de **clustering** sobre un **dataset de vueltas de F1**, optimizando la capacidad del modelo para encontrar patrones en los datos y clasificar automáticamente las vueltas en grupos con características similares.

---

## 🧠 1. Objetivo del proyecto

Desarrollar un sistema capaz de:

- Procesar información de vueltas de carrera.  
- Identificar patrones de rendimiento de los pilotos y coches.  
- Clasificar automáticamente cada vuelta en clústers según sus características, como:  
  - **Vueltas rápidas estables**  
  - **Vueltas lentas estables**  
  - **Vueltas rápidas con variabilidad**  
  - **Vueltas lentas con errores leves**  

---

## 🗂 2. Dataset

El dataset, obtenido de **Kaggle**, contiene variables relacionadas con cada vuelta, incluyendo:

- Tiempo total de cada vuelta de cada piloto.  
- Tiempo por sectores de la pista.  
- Posición del piloto en cada vuelta.  
- Variables numéricas adicionales relevantes.  

No existe una **etiqueta de salida**, ya que el problema se aborda como **clustering**. Los datos se utilizan para descubrir grupos de vueltas con comportamientos similares.

---

## 🔧 3. Preprocesamiento de datos

Para garantizar que los datos fueran aptos para los algoritmos de clustering, se aplicó el siguiente pipeline:

- **Limpieza de datos:** eliminación de registros incompletos o inconsistentes.  
- **Normalización de variables numéricas** para que las diferencias en segundos o posiciones no sesgaran los algoritmos.  
- **Ingeniería de características:** selección de variables más relevantes y creación de métricas derivadas de sectores o velocidad media.  
- **Tratamiento de escala:** estandarización para asegurar que todos los atributos contribuyan de forma equilibrada al clustering.  

Este proceso asegura que los algoritmos identifiquen patrones reales y consistentes entre las vueltas.

---

## 🏗 4. Algoritmos implementados

Se aplicaron y compararon distintos algoritmos de **clustering**:

- **K-Means**  
- **DBSCAN**  
- **Clustering Jerárquico**  
- **Gaussian Mixture Model (GMM)**  

### 🧪 Análisis de modelos

- **K-Means:** identificó 2 clústers óptimos según inercia, separando vueltas rápidas y lentas, pero no captura subvariaciones ni el ruido.  
- **Clustering Jerárquico:** útil para interpretar relaciones jerárquicas, rendimiento similar a K-Means, pero menos flexible para densidades variadas.  
- **GMM:** menor capacidad de agrupamiento, con métricas inferiores en Silhouette Score y Davies-Bouldin Index.  
- **DBSCAN:** mejor desempeño, identifica 4 clústers distintos (sin contar ruido), considerando densidad de puntos en lugar de número fijo de clústers.  

**Conclusión:** DBSCAN es el algoritmo más confiable y estable para este dataset, capturando tanto el número de clústers como su densidad y separando correctamente vueltas atípicas.

---

## ⚙️ 5. Entrenamiento del modelo DBSCAN

Parámetros y técnicas clave:

- **Radio de vecindad (eps):** optimizado mediante análisis de curvas k-distancias.  
- **Número mínimo de puntos (min_samples):** 5  
- **Métricas de evaluación:** Silhouette Score, Davies-Bouldin Index, número de clústers y distribución de vueltas.  

DBSCAN permite identificar automáticamente el número de clústers y clasificar el ruido sin necesidad de predefinir el número de grupos.

---

## 📊 6. Resultados finales

- **DBSCAN seleccionado como modelo final**  
- **Silhouette Score:** 0.89 (clústers bien definidos y separados)  
- **Davies-Bouldin Index:** bajo (clusters compactos y separados)  
- **Número de clústers encontrados:** 4 (sin contar ruido)  

### 🔍 Interpretación de los clústers

- **Clúster 0:** Vueltas rápidas “estables” (1072 vueltas, grupo más grande)  
- **Clúster 1:** Vueltas lentas “estables”  
- **Clúster 2:** Vueltas rápidas con cierta variabilidad (por ejemplo, Safety Car o cambios de pista)  
- **Clúster 3:** Vueltas lentas con errores leves de conducción  

> Nota: El ruido identifica vueltas atípicas que no encajan en los patrones definidos.

---

## 🚀 7. Conclusiones y mejoras futuras

El proyecto demuestra que los **algoritmos de clustering, especialmente DBSCAN, pueden capturar patrones relevantes** en vueltas de F1, permitiendo analizar el rendimiento de pilotos y coches de forma automática.  

### 🔧 Posibles mejoras

- **Ampliar y enriquecer el dataset**: incluir velocidad media, tipo de neumático, número de correcciones de volante y otros factores.  
- **Validación en distintos escenarios:** evaluar el modelo con datos de otras sesiones o circuitos para mejorar la generalización.  
- **Comparación con métodos híbridos o ensembles:** combinar DBSCAN con otras técnicas para captar patrones más complejos.

---

## 📦 8. Dependencias

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
from sklearn.preprocessing import StandardScaler
from sklearn.cluster import KMeans, DBSCAN, AgglomerativeClustering
from sklearn.mixture import GaussianMixture
from sklearn.metrics import silhouette_score, davies_bouldin_score
```

---

## ▶️ 9. Cómo ejecutar el proyecto

1. Clonar el repositorio:

```bash
git clone https://github.com/criscantero15/clustering-f1.git
```

2. Instalar dependencias:

```bash
pip install -r requirements.txt
```

3. Abrir el proyecto en VSCode y ejecutar el notebook

Una vez instalado todo, abre el proyecto en VSCode, accede al archivo modelo.ipynb y simplemente pulsa el botón ▶ (Run/Play) de cada celda (o de ejecutar todo). VSCode detectará automáticamente los kernels disponibles en tu sistema (por ejemplo, el que tengas configurado en tu entorno virtual), y podrás seleccionar el que desees usar en la esquina superior derecha del notebook.

Normalmente, si tienes un entorno virtual creado para ese proyecto, VSCode te sugerirá usar el kernel correspondiente al venv. Si no, podrás elegir otro kernel Python instalado en tu sistema.

---

## 📝 10. Autor

Proyecto desarrollado por Cristian Cantero López como parte del Máster en Inteligencia Artificial y Big Data en la asignatura de Sistemas de Aprendizaje Automático.

---

¡Gracias por visitar este proyecto! Si quieres contribuir o proponer mejoras, no dudes en abrir un issue o un pull request.