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

## Licencia

Este proyecto está licenciado bajo la Licencia MIT. Consulta el archivo LICENSE para más detalles.

## Contacto

Para preguntas o comentarios, puedes contactar al autor en saidortigoza@gmail.com.
