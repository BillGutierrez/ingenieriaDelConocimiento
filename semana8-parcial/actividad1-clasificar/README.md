# Predicción de daños en edificios por terremoto

Proyecto de clasificación desarrollado en [`terremoto_completado.ipynb`](./terremoto_completado.ipynb). Usa datos de edificios afectados por el terremoto de Gorkha, Nepal, en 2015, para entrenar y comparar modelos que predicen el nivel de daño estructural.

> **En pocas palabras:** a partir de características del edificio y de su ubicación, el notebook predice `damage_grade` (nivel de daño 1, 2 o 3). Es un ejercicio de análisis y modelado con datos históricos; no es una herramienta de evaluación estructural ni debe usarse para tomar decisiones de seguridad.

## Objetivo

La variable que se busca predecir es `damage_grade`:

| Clase | Interpretación |
| --- | --- |
| 1 | Daño bajo |
| 2 | Daño medio |
| 3 | Daño casi total |

El conjunto contiene **260.601 edificios**, **38 variables predictoras** y la etiqueta objetivo. Las clases están desbalanceadas, así que el proyecto compara los modelos con más de una métrica y presta especial atención a **F1 macro**, que da el mismo peso a cada clase.

## Datos y fuentes

El notebook lee el archivo [`train_merged.csv`](./train_merged.csv) desde su directorio de trabajo. Este CSV debe estar disponible para ejecutar el proyecto; sin él, la celda de carga no encontrará los datos.

El dataset se conoce como **Richter's Predictor: Modeling Earthquake Damage**. Sus registros provienen de edificios encuestados después del terremoto de Nepal de 2015.

- [Dataset en Kaggle](https://www.kaggle.com/datasets/mullerismail/richters-predictor-modeling-earthquake-damage)
- [Competencia original en DrivenData](https://www.drivendata.org/competitions/57/nepal-earthquake/)
- [Portal de datos abiertos del terremoto de Nepal](http://eq2015.klldev.org)

El archivo local es una tabla combinada de características y etiquetas. `building_id` identifica cada edificio, pero se excluye de las variables usadas para entrenar.

## Qué hace el notebook

El flujo está organizado en las siguientes etapas:

1. **Exploración:** revisa dimensiones, tipos de datos, valores faltantes o repetidos, distribuciones y relaciones entre las características y el nivel de daño.
2. **Preprocesamiento:** trata `age = 995` como un valor desconocido, añade un indicador y deja que la imputación use la mediana aprendida en entrenamiento. Codifica variables categóricas y estandariza las numéricas.
3. **División de los datos:** separa entrenamiento y prueba en proporción 80/20, con estratificación para conservar la distribución de las clases.
4. **Comparación de modelos:** entrena regresión logística, árbol de decisión, Random Forest, HistGradientBoosting y K vecinos más cercanos (KNN).
5. **Selección y ajuste:** selecciona el modelo inicial con mayor F1 macro y explora sus hiperparámetros con `RandomizedSearchCV`.
6. **Evaluación final:** mide el modelo ajustado en el conjunto de prueba y calcula importancia por permutación.
7. **Serialización:** guarda el modelo entrenado en `modelo_terremoto.joblib`.

### Decisiones de preprocesamiento

- Se conserva `age = 0`; el valor especial `995` se interpreta como desconocido, se marca y se imputa.
- Las variables categóricas de baja cardinalidad se codifican con One-Hot Encoding.
- Las variables geográficas de alta cardinalidad (`geo_level_2_id` y `geo_level_3_id`) usan target encoding; `geo_level_1_id` usa One-Hot Encoding.
- Las variables numéricas se estandarizan con `StandardScaler`.
- Las transformaciones que aprenden estadísticas se ajustan con entrenamiento, no con prueba. El target encoding de entrenamiento utiliza validación cruzada interna para reducir la fuga de información.

## Métricas

El notebook compara **accuracy**, **F1 macro** y **AUC**, y también presenta matrices de confusión y métricas por clase. La curva ROC se centra en distinguir la clase 3 frente a las clases 1 y 2. Dado el desbalance de clases, accuracy por sí sola puede ocultar un rendimiento pobre en las clases menos frecuentes.

Las conclusiones del cuaderno tienen campos que deben completarse después de ejecutarlo. No se informa aquí un modelo ganador ni valores de rendimiento porque dependen de los resultados obtenidos al ejecutar las celdas.

## Requisitos y ejecución

Se requiere Python 3 y Jupyter Notebook. Desde la raíz del repositorio, instala las bibliotecas utilizadas:

```bash
python -m pip install "scikit-learn>=1.3" pandas numpy matplotlib seaborn scipy joblib notebook
```

Luego cambia al directorio de este proyecto y abre el notebook:

```bash
cd semana8-parcial/actividad1-clasificar
jupyter notebook terremoto_completado.ipynb
```

También puedes abrir el archivo `.ipynb` con VS Code. En ambos casos, asegúrate de que el directorio de trabajo sea `actividad1-clasificar`, ya que la carga de datos usa la ruta relativa `train_merged.csv`. Ejecuta las celdas en orden, desde el principio.

## Archivos

| Archivo | Descripción |
| --- | --- |
| [`terremoto_completado.ipynb`](./terremoto_completado.ipynb) | Análisis, preprocesamiento, entrenamiento, evaluación y conclusiones. |
| [`train_merged.csv`](./train_merged.csv) | Datos de entrada requeridos para ejecutar el notebook. |
| `modelo_terremoto.joblib` | Modelo final serializado; se crea al ejecutar la sección de guardado. |

## ¿Debo subir el CSV a GitHub?

**Sí, si quieres que otras personas puedan ejecutar el notebook al clonar el repositorio**, incluye `train_merged.csv` en esta misma carpeta. El notebook lo necesita y no descarga los datos automáticamente. El archivo local mide aproximadamente **23,1 MB**, por debajo del límite de 100 MB por archivo de GitHub, así que no requiere Git LFS por tamaño.

Antes de publicarlo, verifica que la licencia y las condiciones de la fuente permitan redistribuir el CSV. Si no puedes subir los datos, deja el enlace a la fuente y añade instrucciones para que cada persona los descargue y prepare con el nombre y formato esperados por el notebook.
