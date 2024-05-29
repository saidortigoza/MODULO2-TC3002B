# Clasificador de Desechos 🗑️

## Descripción del Proyecto

Este proyecto desarrolla un clasificador de desechos utilizando técnicas de aprendizaje supervisado. El objetivo es crear un sistema que pueda identificar y clasificar diferentes tipos de residuos (vidrio, cartón, orgánicos, textiles, plástico, etc.) a partir de de imágenes. Esto puede resultar útil para mejorar la gestión de residuos y promover prácticas de reciclaje eficientes.

## Descripción del Dataset

El dataset RealWaste proviene del repositorio de aprendizaje automático de la Universidad de California, Irvine (UCI) y se utiliza para el desarrollo de sistemas de clasificación de desechos. El dataset se emplea para entrenar y evaluar modelos de aprendizaje supervisado con el objetivo de clasificar diferentes tipos de residuos.

El dataset contiene 4752 imágenes de residuos etiquetados en las siguientes categorías:

- Cartón: 461 imágenes

- Orgánicos: 411 imágenes.

- Vidrio: 420 imágenes.

- Metal: 790 imágenes.

- Basura Miscelánea: 495 imágenes.

- Papel: 500 imágenes.

- Plástico: 921 imágenes.

- Basura Textil: 318 imágenes.

- Vegetación: 436 imágenes.

Cada categoría tiene su propia carpeta, y cada carpeta contiene imágenes en formato .jpg.

El dataset RealWaste se puede acceder y descargar desde el siguiente enlace: [RealWaste Dataset](https://archive.ics.uci.edu/dataset/908/realwaste).

## Actividades

- **Obtener, generar o aumentar un set de datos.**

El dataset utilizado para este proyecto, RealWaste, fue obtenido del [UCI Machine Learning Repository](https://archive.ics.uci.edu/dataset/908/realwaste). Contiene imágenes clasificadas en diversas categorías de desechos. Estas imágenes se utilizarán para desarrollar un modelo de clasificación.

Previo a realizar la separación, el dataset inicial fue modificado, quedando de la siguiente manera, únicamente 5 clases:

- Cardboard: 461 imágenes.

- Food Organics: 411 imágenes.

- Glass: 420 imágenes.

- Metal: 474 imágenes.

- Plastic: 489 imágenes.

- **Hacer la separación de los sets de prueba y entrenamiento.**

Inicialmente, el dataset no estaba dividido en sets de train y test. Por lo que se realizó una división del dataset inicial para dichos conjuntos, siendo dividido de la siguiente manera:

- Entrenamiento: 80%.

- Prueba: 10%.

- Validación: 10%.

Dado que el dataset inicial cuenta con 4752 imágenes, a las que se aplicarán técnicas de escalamiento, utilizaremos el 70% de los datos para entrenar al modelo y poder realizar las técnicas de clasificación de desechos, de manera que los parámetros del modelo sean ajustados y optimizados usando estos ejemplos, una vez que sea entrenado, utilizaremos un 10% para validar qué tan bien clasifica nuestro modelo, una vez que nuestro modelo tenga un buen rendimiento, utilizaremos el 20% restante para probarlo.

El enlace para acceder a los directorios divididos es el siguiente: [Dataset](https://drive.google.com/drive/folders/15qHsKJlguvv3mBKYhYBcgTRdKG2kicfi?usp=sharing).

- **Aplicar las técnicas de escalamiento.**

Las técnicas de escalamiento aplicadas fueron las siguientes:

**rescale = 1/255:** Normaliza los valores de los píxeles de las imágenes dividiéndolos por 255. Esto escala los valores de los píxeles para que estén en el rango [0, 1]. Asegura que los valores de los píxeles estén en una escala adecuada para el procesamiento por el modelo.

**rotation_range = 40:** Aplica una rotación aleatoria a las imágenes dentro del rango especificado en grados. Introduce variabilidad en las imágenes.

**width_shift_range = 0.1:** Realiza un desplazamiento horizontal aleatorio a las imágenes dentro del rango especificado. En este caso utilizamos 0.1 para que los desechos no salgan demasiado de la imagen.

**height_shift_range = 0.1:** Realiza un desplazamiento vertical aleatorio a las imágenes dentro del rango especificado. En este caso utilizamos 0.1 para que los desechos no salgan demasiado de la imagen.

**zoom_range = 0.05:** Aplica un zoom aleatorio a las imágenes dentro del rango especificado. Estamos utilizando 0.05 para crear imágenes variadas que no modifiquen demasiado la imagen original.

**horizontal_flip = True:** Voltea horizontalmente aleatoriamente las imágenes. Agrega variabilidad al conjunto de datos al reflejar las imágenes horizontalmente.

**fill_mode='reflect':** Especifica cómo rellenar los píxeles que pueden quedar vacíos después de aplicar transformaciones. Estamos utilizando reflect para rellenar con valores reflejados los píxeles que quedan vacíos para mantener la integridad visual de las imágenes.

Este set de datos se utiliza para generar imágenes significativas para el modelo. Se probó a utilizar diferentes desplazamientos horizontales y verticales, zoom y fill mode, por ejemplo, *nearest*, sin embargo, los valores actuales fueron seleccionados porque no distorsionan demasiado las imágenes, siendo generadas imágenes de mejor calidad.

- **Hacer el preprocesado pertinente de los datos.**

En este caso, el escalado (normalización de los valores de los pixeles) de los datos se realizó como parte del preprocesamiento para los conjuntos de entrenamiento y validación.

- **Seleccionar un modelo respaldado por un paper del estado del arte.**

Se realizó la implementación de una Red Neuronal Convolucional (CNN), inspirada en la investigación presentada en el artículo "Deep Convolutional Neural Network with TensorFlow and Keras to Classify Skin Cancer Images". Esta elección se fundamenta en la robustez y eficacia demostrada por el modelo propuesto, que utiliza técnicas avanzadas de aprendizaje profundo para la clasificación precisa de imágenes de cáncer de piel.

Una CNN es un tipo de red neuronal artificial diseñada específicamente para el procesamiento de imágenes. Se compone de múltiples capas, incluyendo capas de convolución, activación y pooling. La capa de convolución resulta fundamental para la CNN, ya que aplica filtros a la imagen de entrada para detectar características como bordes, formas y texturas, siendo específicamente útil para el contexto de este proyecto. La capa de pooling reduce la dimensionalidad de las características extraídas, lo que ayuda a mejorar la eficiencia computacional y a evitar el sobreajuste.

La adaptación de esta arquitectura en el proyecto fue una pieza clave en el inicio del desarrollo, sin embargo, no se utiliza en el modelo final el modelo propuesto por el paper debido a que la CNN del paper era demasiado compleja, siendo este punto justificado debido a que se trata de un modelo de clasificación de cáncer de piel. Pero para el caso de clasificación de residuos, resultó demasiado contraproducente, consumía demasiados recursos (epochs de alrededor de 10 minutos cada uno), y después de experimentar con 5 epochs, el modelo únicamente logró un accuracy no mayor al 20%.

Se realizaron diversos ajustes, entre ellos, se experimentó con ajustes en el modelo que crearon demasiado overfitting, debido a que la accuracy del conjunto train que se obtuvo fue alta, pero la accuracy del conjunto de validación no se aceraba para nada, siendo algunos casos, por ejemplo, un 75% de accuracy, y un 30% de val_accuracy.

Adicionalmente, para efectos prácticos se modificó el dataset, reduciendo las clases de 9 a solamente 5 (Cardboard & Paper, Food Organics, Glass, Metal y Plastic).

El modelo final consta de varias capas que se organizan secuencialmente utilizando la clase Sequential de Keras. A continuación se detalla cada capa y su función:

**Capa de Convolución (Conv2D):** Realiza la convolución de los filtros sobre la imagen de entrada para extraer características como bordes, texturas y patrones visuales.

Filtrado: 16 filtros.
Tamaño del kernel: 3x3.
Función de activación: ReLU.
Tamaño de entrada: (150, 150, 3). El tamaño establecido previamente cuando se cargaron los conjuntos.

**Capa de pooling (MaxPooling2D):** Reduce la dimensionalidad de las características extraídas por la capa de convolución, conservando las características más relevantes.

Tamaño de la ventana de pooling: 2x2.

**Segunda Capa de Convolución (Conv2D):** Similar a la primera capa, pero con 32 filtros en lugar de 16.

**MaxPooling (MaxPooling2D):** Se utiliza otra capa de pooling de 2x2 para capturar características más complejas y abstractas de la imagen.

**Capa de Aplanado (Flatten):** Convierte las características 2D obtenidas de las capas convolucionales y de pooling en un vector unidimensional, que se utilizará como entrada para las capas completamente conectadas.

**Capas Densas (Dense):** Realizan la clasificación final basada en las características extraídas por las capas convolucionales y de pooling.

Dos capas densas con 32 y 5 neuronas respectivamente.
Función de activación ReLU en la primera capa densa y función de activación Softmax en la última capa densa para la clasificación multiclase.

**Capa de Normalización por Lotes (BatchNormalization):** Normaliza las activaciones de la capa anterior, lo que ayuda a acelerar el entrenamiento y mejorar la estabilidad del modelo.

El modelo se compila utilizando el optimizador Adam, que adapta la tasa de aprendizaje de forma adaptativa. La función de pérdida se establece como categorical_crossentropy, adecuada para problemas de clasificación multiclase, en este caso 5. La métrica de evaluación se establece en precisión (accuracy) para monitorear el rendimiento del modelo durante el entrenamiento.

- **Implementar el modelo usando un framework seleccionado.**

Para implementar el modelo, se seleccionó el framework TensorFlow de Google, una de las bibliotecas más populares y utilizadas para el desarrollo de modelos de aprendizaje automático y redes neuronales, lo que facilita el desarrollo del modelo de clasificación.

- **Seleccionar métricas adecuadas respaldadas por un paper del estado del arte.**

De acuerdo con los artículos consultados, las métricas para evaluar el rendimiento del modelo incluyen:

**Precisión (accuracy):** Mide la proporción de predicciones correctas sobre el total de predicciones. Fundamental para problemas de clasificación.

**Pérdida (loss):** La función de pérdida utilizada es categorical_crossentropy, que es adecuada para problemas de clasificación multiclase.

- **Reportar resultados obtenidos e interpretarlos.**

Después de entrenar el modelo con 10 epochs, los resultados obtenidos se evaluaron en términos de precisión y pérdida en los conjuntos de entrenamiento y validación. Además, se incluye una matriz de confusión.

![](https://github.com/saidortigoza/MODULO2-TC3002B/blob/main/img/accuray_loss_graphs.png)

La precisión de train muestra una tendencia alcista, llegando a más del 70%. La precisión de validation también mejora inicialmente y muestra una tendencia alcista, alcanzando un valor máximo de casi 70%, pero luego muestra cierta variabilidad con una ligera disminución al final.

La pérdida de train disminuye de manera constante a lo largo de las épocas, lo cual es una señal de que el modelo está aprendiendo. La pérdida de validation inicialmente disminuye, pero luego muestra cierta variabilidad, con picos en varias epochs antes de volver a disminuir hacia el final.

No parece haber indicios de overfitting severo, ya que las curvas de pérdida de entrenamiento y validación no se están separando drásticamente, y ambas muestran tendencia al alza. Sin embargo, la variabilidad en la precisión y pérdida de validation sugiere que el modelo podría beneficiarse de ajustes.

Según el comportamiento del modelo, no parece haber underfitting. La precisión de ambos conjuntos es razonablemente alta.

Sin embargo, las curvas no son perfectamente paralelas y muestran mucha variabilidad en el conjunto de validation, lo que sugiere mejoras. Por lo que el modelo muestra un ligero overfitting.

Adicionalmente, como parte de la evaluación se incluye una matriz de confusión. Incluir una matriz de confusión como parte de la evaluación es fundamental porque ofrece una visión detallada del rendimiento del modelo en cada clase individual.

![](https://github.com/saidortigoza/MODULO2-TC3002B/blob/main/img/confusion_matrix.png)

Las etiquetas corresponden a lo siguiente:
0: Cardboard & Paper
1: Food Organics
2: Glass
3: Metal
4: Plastic

Los valores de la diagonal corresponden con los valores estimados de forma correcta por el modelo, podemos observar que la mayoría de las clases tienen predicciones aceptables, con exepción de la clase plastic, la cual tiene muchísimas predicciones como si fuera cardboard & paper. Esto sugiere que el dataset también puede mejorar, existen entre las imágenes revistas, envases de cartón, hojas blancas, que el modelo confundió con plástico blanco, como por ejemplo, frascos de pastillas o tapas.

![](https://github.com/saidortigoza/MODULO2-TC3002B/blob/main/img/predictions.png)

## Referencias

- UCI Machine Learning Repository. (2023). Uci.edu. https://archive.ics.uci.edu/dataset/908/realwaste

- Lee, H., Lee, N., & Lee, S. (2022). A Method of Deep Learning Model Optimization for Image Classification on Edge Device. Sensors, 22(19), 7344. https://doi.org/10.3390/s22197344

- Nasir, Israa & Al-Talib, Ghaidaa. (2023). Waste Classification Using Artificial Intelligence Techniques:Literature Review. Technium: Romanian Journal of Applied Sciences and Technology. 5. 49-59. 10.47577/technium.v5i.8345.

- Houssam Benbrahim, Hanaâ Hachimi, & Amine, A. (2020). Deep Convolutional Neural Network with TensorFlow and Keras to Classify Skin Cancer Images. Scalable Computing. Practice and Experience, 21(3), 379–390. https://doi.org/10.12694/scpe.v21i3.1725

## Licencia

Este proyecto está licenciado bajo la Licencia MIT. Consulta el archivo LICENSE para más detalles.

## Contacto

Para preguntas o comentarios, puedes contactar al autor en saidortigoza@gmail.com.
