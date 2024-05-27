# Clasificador de Desechos 🗑️

## Descripción del Proyecto

Este proyecto desarrolla un clasificador de desechos utilizando técnicas de aprendizaje supervisado. El objetivo es crear un sistema que pueda identificar y clasificar diferentes tipos de residuos (vidrio, cartón, orgánicos, textiles, plástico, etc.) a partir de de imágenes. Esto puede resultar útil para mejorar la gestión de residuos y promover prácticas de reciclaje eficientes.

## Descripción del Dataset

El dataset RealWaste proviene del repositorio de aprendizaje automático de la Universidad de California, Irvine (UCI) y se utiliza para el desarrollo de sistemas de clasificación de desechos. El dataset se emplea para entrenar y evaluar modelos de aprendizaje supervisado con el objetivo de clasificar diferentes tipos de residuos.

El dataset contiene 4752 imágenes de residuos etiquetados en varias categorías:

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

- **Hacer la separación de los sets de prueba y entrenamiento.**

Inicialmente, el dataset no estaba dividido en sets de train y test. Por lo que se realizó una división del dataset inicial para dichos conjuntos, siendo dividido de la siguiente manera:

- Entrenamiento: 70%.

- Prueba: 20%.

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

El modelo final desarrollado se explica a continuación:

- **Implementar el modelo usando un framework seleccionado.**

Para implementar el modelo, se seleccionó el framework TensorFlow de Google, una de las bibliotecas más populares y utilizadas para el desarrollo de modelos de aprendizaje automático y redes neuronales, lo que facilita el desarrollo del modelo de clasificación.

- **Seleccionar métricas adecuadas respaldadas por un paper del estado del arte.**

- **Reportar resultados obtenidos e interpretarlos.**

## Referencias

- UCI Machine Learning Repository. (2023). Uci.edu. https://archive.ics.uci.edu/dataset/908/realwaste

- Lee, H., Lee, N., & Lee, S. (2022). A Method of Deep Learning Model Optimization for Image Classification on Edge Device. Sensors, 22(19), 7344. https://doi.org/10.3390/s22197344

- Nasir, Israa & Al-Talib, Ghaidaa. (2023). Waste Classification Using Artificial Intelligence Techniques:Literature Review. Technium: Romanian Journal of Applied Sciences and Technology. 5. 49-59. 10.47577/technium.v5i.8345.

- Houssam Benbrahim, Hanaâ Hachimi, & Amine, A. (2020). Deep Convolutional Neural Network with TensorFlow and Keras to Classify Skin Cancer Images. Scalable Computing. Practice and Experience, 21(3), 379–390. https://doi.org/10.12694/scpe.v21i3.1725

## Licencia

Este proyecto está licenciado bajo la Licencia MIT. Consulta el archivo LICENSE para más detalles.

## Contacto

Para preguntas o comentarios, puedes contactar al autor en saidortigoza@gmail.com.
