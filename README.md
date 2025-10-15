# GAN

**GAN básica para MNIST (generación de dígitos)**

<br>

**Objetivo**

Desarrollar una Red Generativa Adversaria (GAN), específicamente para la tarea de generación de imágenes de 28x28 píxeles a partir de ruido, mediante la interacción competitiva entre un Generador y un Discriminad

<br>
<br>

**Metodologuía**

1.- Imports, carga MNIST y escalado

Este bloque prepara los datos de MNIST para entrenar un GAN. Se importan librerías de TensorFlow y NumPy, y se fijan semillas para reproducibilidad.

Se carga solo el conjunto de entrenamiento. Las imágenes se normalizan a [-1, 1] y se les agrega una dimensión de canal (28,28,1).

Se definen parámetros clave: tamaño de lote, buffer de shuffle, dimensión del vector latente y número de épocas.

Se crea un tf.data.Dataset con los datos, mezclado y agrupado en lotes listos para entrenamiento

<br><br>

**2.- Definir Generador y Discriminador**

Se construyen los modelos Generador y Discriminador de un GAN para MNIST. El Generador recibe un vector latente y lo transforma en una imagen 28x28x1. Incluye Dense, Reshape, BatchNormalization, LeakyReLU y Conv2DTranspose. La salida usa tanh para valores en [-1,1].

El Discriminador toma imágenes 28x28x1 y las clasifica como reales o falsas. Incluye Conv2D, LeakyReLU, Dropout, Flatten y Dense con sigmoid. Se compila con Adam y binary cross-entropy, dejando ambos modelos listos para entrenamiento.

<br>
<br>

**3.- Bucle de entrenamiento adversarial**
Se configura la GAN combinada, congelando el Discriminador al entrenar el Generador.

Se crea un modelo que toma un vector latente y devuelve la predicción del Discriminador sobre imágenes generadas.

Se compila con Adam y binary cross-entropy.

Se define una función para generar y mostrar imágenes de prueba a partir de ruido.

Durante cada época se entrena primero el Discriminador con imágenes reales y falsas.

Luego se entrena el Generador usando etiquetas “reales” y el Discriminador congelado.

Se registra la pérdida de ambos modelos y se muestran imágenes generadas cada 2 épocas.

Finalmente, se imprime el tiempo total de entrenamiento y se confirma que la GAN está lista.

<br>
<br>

**Resultados**

Si se usa D_loss, a partir de los valores 0.55 y 0.59 el modelo ya tiene dificultades para diferencias reales de falsas, Si se observa G_loss, en los valores 1.05 y 1.15, refleja que el generador mejora y engaña mejor al discriminador, los modelos aprenden de forma competitiva a partir de la época 5 a 7, donde se esperaría los mejores resultados.



