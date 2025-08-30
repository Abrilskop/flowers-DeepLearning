# Proyecto Comparativo de Modelos de Deep Learning para la Clasificación de Flores

## 1. Descripción del Proyecto

Este proyecto aborda la tarea de clasificación de imágenes multi-clase mediante el uso de técnicas de **Transfer Learning**. El objetivo es realizar un estudio comparativo riguroso del rendimiento de tres arquitecturas de Redes Neuronales Convolucionales (CNNs) preentrenadas para identificar 5 especies comunes de flores. Los modelos seleccionados para la comparación son:

1.  **MobileNetV2:** Representa las arquitecturas ligeras y eficientes, optimizadas para entornos con recursos limitados.
2.  **VGG16:** Un modelo clásico y profundo que sirve como una sólida línea base por su arquitectura secuencial y robustez.
3.  **EfficientNetB0:** Una arquitectura de vanguardia que utiliza escalado compuesto para lograr un balance superior entre precisión y eficiencia computacional.

## 2. Dataset: "Flowers Recognition"

### 2.1. Fuente y Contenido
El proyecto utiliza el dataset público "Flowers Recognition", disponible en la plataforma Kaggle.

*   **Enlace a la Fuente:** [Kaggle - Flowers Recognition Dataset](https://www.kaggle.com/datasets/alxmamaev/flowers-recognition)
*   **Autor:** Alexander Mamaev
*   **Contenido:** El dataset contiene 4242 imágenes de baja resolución (aprox. 320x240 píxeles) distribuidas en 5 clases:
    *   `daisy` (764 imágenes)
    *   `dandelion` (1052 imágenes)
    *   `rose` (784 imágenes)
    *   `sunflower` (733 imágenes)
    *   `tulip` (984 imágenes)

### 2.2. Licencia y Consideraciones Éticas
La licencia del dataset está marcada como **"Desconocida"**. Esto implica que, si bien su uso es adecuado para fines académicos y de investigación, se deben tomar precauciones para su aplicación en contextos comerciales debido a posibles restricciones de derechos de autor sobre las imágenes originales. Este proyecto reconoce dicha limitación y procede bajo un marco de uso responsable y educativo.

## 3. Metodología

El flujo de trabajo implementado en el notebook `Proyecto_Clasificacion_Flores.ipynb` sigue los siguientes pasos:

1.  **Configuración del Entorno:** Se instala la API de Kaggle y se verifica la disponibilidad de una GPU en Google Colab.
2.  **Carga de Datos:** El dataset se descarga y descomprime automáticamente desde Kaggle para garantizar la reproducibilidad.
3.  **Preprocesamiento:** Se crean generadores de datos (`ImageDataGenerator`) que realizan:
    *   **Partición de Datos:** División del conjunto en 80% para entrenamiento y 20% para validación.
    *   **Aumento de Datos (Data Augmentation):** Se aplican transformaciones aleatorias (rotación, zoom, volteo horizontal) a las imágenes de entrenamiento para mejorar la generalización del modelo.
    *   **Normalización:** Cada imagen se preprocesa con la función específica requerida por cada arquitectura preentrenada.
4.  **Entrenamiento:** Cada uno de los tres modelos se entrena en dos fases:
    *   **Transfer Learning:** Se congelan las capas convolucionales del modelo base y se entrena únicamente la cabeza de clasificación recién añadida.
    *   **Fine-Tuning:** Se descongelan las capas superiores del modelo base y se continúa el entrenamiento con una tasa de aprendizaje (learning rate) muy baja para ajustar finamente los pesos a la tarea específica.
5.  **Evaluación:** El rendimiento de cada modelo final se mide en el conjunto de validación utilizando las siguientes métricas:
    *   **Accuracy (Precisión Global)**
    *   **F1-Score (Macro)**, para evaluar el equilibrio entre precisión y exhaustividad.
    *   **Matriz de Confusión**, para un análisis visual detallado de los errores de clasificación por clase.

## 4. Cómo Replicar el Experimento

### Prerrequisitos
*   Una cuenta de Google (para Google Colab).
*   Una cuenta de Kaggle y un token de API (`kaggle.json`).

### Pasos
1.  **Clonar/Descargar el Repositorio:** Obtén el archivo `Proyecto_Clasificacion_Flores.ipynb`.
2.  **Abrir en Google Colab:** Sube y abre el notebook en tu entorno de Colab.
3.  **Activar Acelerador por GPU:** Navega a `Entorno de ejecución` > `Cambiar tipo de entorno de ejecución` y selecciona `GPU` en el menú desplegable.
4.  **Ejecutar el Notebook:** Ejecuta todas las celdas en secuencia. El script te pedirá que subas tu archivo `kaggle.json` en la Sección 2 para proceder con la descarga del dataset.

## 5. Resultados

Todos los artefactos generados (gráficos de entrenamiento, matrices de confusión y la tabla comparativa en formato `.csv`) se guardan automáticamente en una carpeta llamada `/results` dentro del entorno de Colab. Estos archivos son la base para el informe final del proyecto.
