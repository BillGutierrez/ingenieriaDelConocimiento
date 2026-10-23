# Ingeniería del Conocimiento

Repositorio académico de la asignatura **Ingeniería del Conocimiento (ISO56B)** de la Facultad de Ingeniería de Sistemas de la Universidad Nacional del Centro del Perú. Reúne notebooks, datasets y actividades prácticas desarrolladas durante el curso para explorar el ciclo de vida de proyectos de machine learning, modelos de clasificación y redes neuronales convolucionales.

## Contenido

| Semana / actividad | Contenido |
| --- | --- |
| [`semana3/`](./semana3/) | Ciclo de vida de un proyecto de machine learning: preparación de datos, entrenamiento, evaluación, serialización, búsqueda de hiperparámetros y registro de experimentos con MLflow. Incluye ejercicios con datos de enfermedades cardíacas y Bank Marketing. |
| [`semana4/`](./semana4/) | Material de apoyo: guía paso a paso en PDF. |
| [`semana5/`](./semana5/) | Modelos de clasificación: regresión logística, árboles, SVM y KNN; evaluación, validación cruzada, ajuste de hiperparámetros y manejo del desbalance. Incluye ejercicios con Bank Marketing y Student Dropout and Academic Success. |
| [`semana8-parcial/actividad1-clasificar/`](./semana8-parcial/actividad1-clasificar/) | Clasificación del nivel de daño en edificios afectados por el terremoto de Nepal de 2015. Consulta su [README](./semana8-parcial/actividad1-clasificar/README.md) para los datos y la ejecución. |
| [`semana8-parcial/actividad2-imagenes/`](./semana8-parcial/actividad2-imagenes/) | Clasificación de imágenes de minerales con redes neuronales convolucionales. Consulta su [README](./semana8-parcial/actividad2-imagenes/README.md) para los datos, el entorno y la ejecución. |

## Empezar

Clona el repositorio y abre el notebook de la semana o actividad que quieras revisar:

```bash
git clone <URL_DEL_REPOSITORIO>
cd <CARPETA_DEL_REPOSITORIO>
```

Los notebooks se pueden abrir con **Jupyter Notebook**, **JupyterLab** o **Visual Studio Code** con soporte para Jupyter. Cada ejercicio puede tener dependencias, rutas de datos y pasos de configuración propios; sigue el README de la carpeta correspondiente cuando exista. Ejecuta las celdas en orden y comprueba que el directorio de trabajo sea el esperado por el notebook.

No existe un único entorno de Python que garantice la ejecución de todos los notebooks: los proyectos usan bibliotecas y conjuntos de datos distintos. En particular, la actividad de CNN requiere preparar el dataset de imágenes según las instrucciones de su README.

## Datos

Algunos datasets tabulares están incluidos junto a los ejercicios que los utilizan. La carpeta de la actividad de terremotos contiene `train_merged.csv`, que su notebook carga directamente. La actividad de clasificación de minerales requiere descargar por separado el dataset **Mineral Photos** desde Kaggle; las imágenes no están incluidas en el repositorio.

Antes de redistribuir cualquier dataset, revisa sus condiciones de uso y licencia. Para detalles sobre fuentes, estructura, instalación y rutas, consulta la documentación específica de cada actividad.

## Estructura

```text
.
├── semana3/
│   └── notebooks sobre ciclo de vida de machine learning
├── semana4/
│   └── guía de apoyo en PDF
├── semana5/
│   ├── notebooks sobre modelos de clasificación
│   └── datasets de ejercicios
└── semana8-parcial/
    ├── actividad1-clasificar/
    │   ├── README.md
    │   ├── terremoto_completado.ipynb
    │   └── train_merged.csv
    └── actividad2-imagenes/
        ├── README.md
        ├── actividad2_cnn.ipynb
        ├── pyproject.toml
        └── src/
```

## Alcance

Este repositorio es material educativo y experimental. Los modelos y resultados de los notebooks no deben interpretarse como sistemas listos para uso productivo ni como sustitutos de evaluación profesional.
