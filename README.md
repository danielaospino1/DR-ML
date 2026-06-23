# DR-ML

Repositorio de código fuente para el desarrollo, entrenamiento y evaluación de modelos de *machine learning* aplicados a la predicción de retinopatía diabética a partir de datos clínicos y tabulares no imagenológicos.

Este repositorio contiene un notebook de trabajo en Python que implementa un pipeline completo de preprocesamiento, selección de variables, entrenamiento de modelos, evaluación de desempeño e interpretabilidad para apoyar el análisis de riesgo de retinopatía diabética.

## Contenido del repositorio

```text
DR-ML/
│
├── Entrenamiento de modelos V1.ipynb
├── raw data (1).xlsx
└── README.md
```

## Descripción general

El notebook `Entrenamiento de modelos V1.ipynb` desarrolla un flujo de trabajo para la construcción de modelos predictivos orientados a la detección o clasificación de retinopatía diabética usando variables clínicas, bioquímicas y tabulares.

El pipeline implementado incluye:

1. Carga y exploración inicial del dataset.
2. Limpieza inicial de variables con alto porcentaje de valores faltantes.
3. División estratificada del dataset en entrenamiento y prueba.
4. Imputación de valores faltantes mediante `KNNImputer`.
5. Escalado de variables continuas mediante `RobustScaler`.
6. Tratamiento de colinealidad mediante análisis VIF.
7. Análisis estadístico bivariado para variables continuas y binarias.
8. Selección de variables usando criterios estadísticos, clínicos y de importancia.
9. Creación de variables de interacción clínica.
10. Entrenamiento y comparación de modelos predictivos.
11. Evaluación del desempeño con métricas orientadas a tamizaje.
12. Interpretabilidad mediante SHAP y análisis de coeficientes.

## Pipeline general

El flujo general de trabajo puede resumirse de la siguiente manera:

```text
Carga del dataset
        ↓
Limpieza inicial
        ↓
División 80/20 estratificada
        ↓
KNN Imputer aplicado sobre train
        ↓
RobustScaler aplicado solo a variables continuas
        ↓
Reducción de colinealidad mediante VIF
        ↓
Feature engineering
        ↓
Selección de variables
        ↓
Entrenamiento con RandomizedSearchCV
        ↓
Evaluación en test
```

## Modelos implementados

El notebook compara tres enfoques de clasificación supervisada:

* Regresión Logística.
* Random Forest.
* XGBoost.

La optimización de hiperparámetros se realiza mediante `RandomizedSearchCV` y validación cruzada estratificada. La métrica principal de optimización es el **F2-score**, dado que en un contexto de tamizaje clínico se prioriza la sensibilidad o *recall* para reducir falsos negativos.

## Métricas de evaluación

Los modelos son evaluados mediante diferentes métricas de clasificación binaria, entre ellas:

* Accuracy.
* Precision.
* Recall / Sensitivity.
* Specificity.
* F1-score.
* F2-score.
* AUC-ROC.
* Matriz de confusión.
* Curvas ROC.
* Análisis de umbral precisión-recall.

El notebook evalúa los modelos con un umbral estándar de clasificación y con un umbral ajustado orientado a tamizaje.

## Interpretabilidad

Para facilitar la comprensión de los modelos, el notebook incluye análisis de interpretabilidad mediante:

* SHAP para modelos basados en árboles.
* Importancia de variables.
* Odds Ratios para la Regresión Logística.
* Visualización de coeficientes asociados al riesgo de retinopatía diabética.

## Principales librerías utilizadas

El proyecto utiliza las siguientes librerías de Python:

```bash
numpy
pandas
matplotlib
seaborn
scipy
scikit-learn
statsmodels
xgboost
shap
joblib
openpyxl
jupyter
```

## Instalación del entorno

Para ejecutar el notebook en un entorno local, se recomienda crear un entorno virtual:

```bash
python -m venv venv
```

Activar el entorno:

En Windows:

```bash
venv\Scripts\activate
```

En macOS/Linux:

```bash
source venv/bin/activate
```

Instalar las dependencias principales:

```bash
pip install numpy pandas matplotlib seaborn scipy scikit-learn statsmodels xgboost shap joblib openpyxl jupyter
```

Luego abrir Jupyter Notebook:

```bash
jupyter notebook
```

Y ejecutar el archivo:

```text
Entrenamiento de modelos V1.ipynb
```

## Ejecución en Google Colab

El notebook también puede ejecutarse en Google Colab. En ese caso, se debe cargar manualmente el archivo de datos `raw data (1).xlsx` al entorno de Colab antes de ejecutar las celdas.

En el notebook, la ruta de carga del archivo puede ajustarse según el entorno de ejecución. Por ejemplo:

```python
df = pd.read_excel("/content/raw data (1).xlsx")
```

Si se ejecuta localmente desde la carpeta raíz del repositorio, puede usarse:

```python
df = pd.read_excel("raw data (1).xlsx")
```

## Consideraciones metodológicas

El pipeline fue diseñado para reducir riesgos de *data leakage*. Por esta razón, la división entrenamiento/prueba se realiza antes de los procesos de imputación, escalado y selección de variables.

Además, el preprocesamiento incluye correcciones metodológicas específicas:

* Conservación de la variable BMI por su relevancia clínica.
* Exclusión de variables binarias del escalado.
* Re-binarización de variables binarias después de la imputación.
* Aplicación de pruebas estadísticas para variables continuas y binarias.
* Generación de variables de interacción clínica.
* Optimización orientada al F2-score para priorizar sensibilidad en un contexto de tamizaje.

## Advertencia sobre los datos

El archivo `raw data (1).xlsx` contiene los datos utilizados para el entrenamiento y evaluación de los modelos. Antes de publicar o compartir este repositorio de forma pública, se recomienda verificar que el dataset no contenga información sensible, identificable o protegida de pacientes.

Si el dataset contiene información clínica individual, se recomienda anonimizarlo o excluirlo del repositorio público.

## Objetivo del repositorio

Este repositorio tiene como objetivo facilitar la reproducibilidad del análisis desarrollado en el notebook, permitiendo revisar el flujo de procesamiento de datos, entrenamiento de modelos, comparación de desempeño e interpretación de resultados en el contexto de predicción de retinopatía diabética mediante técnicas de *machine learning*.

## Estado del proyecto

Versión inicial del notebook de entrenamiento y evaluación de modelos.

## Autoría

Repositorio desarrollado como apoyo al análisis de modelos de *machine learning* para retinopatía diabética.

## Licencia

Licencia pendiente de definir.
