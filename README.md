# Week14_14
## Integrantes:
DIEGO ALEJANDRO RUIZ ALFONSO - diegoaruiz@ucundinamarca.edu.co PEDRO PASCUAL MURCIA VARGAS - ppmurcia@ucundinamarca.edu.co JHON EDUARD TINJACA CRUZ - jetinjaca@ucundinamarca.edu.co JULIAN DAVID SILVA GUZMAN - jdsilva@ucundinamarca.edu.co

# Proyecto GANs: Generación de Imágenes (MNIST & Fashion MNIST)

Este proyecto implementa y compara arquitecturas de Redes Neuronales Generativas Adversarias (GAN) para la creación de imágenes sintéticas.

## Contenido
1. **Modelos implementados**:
   - **GAN MLP**: Modelo base utilizando capas densas.
   - **DCGAN Estándar**: Uso de capas convolucionales inversas (Conv2DTranspose).
   - **DCGAN Mejorada**: Arquitectura optimizada con mayor número de filtros y BatchNormalization.

2. **Datasets**:
   - **MNIST**: Dígitos escritos a mano.
   - **Fashion MNIST**: Prendas de vestir y calzado.

3. **Resultados**:
   - Se logró un entrenamiento estable de 5,000 épocas para el dataset MNIST.
   - Se incluyeron mecanismos de seguridad (try-except) para evitar errores de memoria o reinicio de runtime.

## Cómo ejecutar
1. Ejecutar las celdas de configuración e importación.
2. Definir las arquitecturas de Generador y Discriminador.
3. Entrenar los modelos utilizando la función modular `train_model`.
4. Visualizar resultados con `plot_images`.

## Archivos Generados
- Resultado.png`: Muestra de la DCGAN mejorada.
- Resultado_final.png`: Resultados tras 5000 épocas de entrenamiento.

## General del Código

El flujo de trabajo de este notebook se divide en cuatro etapas principales:

1.  **Preprocesamiento de Datos**:
    *   Carga de los datasets **MNIST** (dígitos) y **Fashion MNIST** (ropa).
    *   Normalización de píxeles al rango `[-1, 1]` para optimizar el uso de la función de activación `tanh`.
    *   Redimensionamiento de las imágenes a `(28, 28, 1)` para compatibilidad con capas convolucionales.

2.  **Definición de Arquitecturas**:
    *   **Generador (DCGAN)**: Utiliza `Conv2DTranspose` para proyectar ruido aleatorio (espacio latente) hacia una imagen completa, aplicando `BatchNormalization` para estabilidad.
    *   **Discriminador (DCGAN)**: Un clasificador convolucional con `LeakyReLU` y `Dropout` que aprende a distinguir entre imágenes reales y generadas.

3.  **Configuración del Modelo Adversario (GAN)**:
    *   Se encadena el Generador con el Discriminador.
    *   Al entrenar la GAN completa, se congela el Discriminador (`trainable = False`) para que solo los pesos del Generador se actualicen, aprendiendo a "engañar" al juez.

4.  **Ciclo de Entrenamiento y Visualización**:
    *   **Modularidad**: Uso de la función `train_model` para ejecutar el entrenamiento por lotes (batches).
    *   **Evaluación**: Generación de gráficas de pérdida para monitorear el equilibrio de Nash y uso de `plot_images` para visualizar el progreso visual del modelo tras miles de épocas.
  
## En la ejecución del código, podemos evidenciar varios puntos clave sobre el comportamiento de tus redes neuronales:

**Convergencia y Estabilidad**: En las gráficas de pérdida, se observa que tras las primeras épocas de inestabilidad, las curvas de pérdida del Generador y el Discriminador entran en una etapa de oscilación controlada. Esto es evidencia del Equilibrio de Nash, donde ambos modelos compiten sin que uno anule por completo al otro.
**Aprendizaje desde el Ruido**: Al comparar las imágenes 'Sin entrenar' (que son estática pura) con los resultados a las 2000 y 5000 épocas, se evidencia que el Generador ha aprendido a mapear vectores aleatorios a estructuras espaciales con significado (dígitos y ropa).
**Superioridad de DCGAN sobre MLP**: El código ejecutado demuestra que las capas convolucionales (Conv2DTranspose) mantienen la jerarquía espacial de la imagen, produciendo bordes más nítidos y formas menos borrosas que la versión basada únicamente en capas densas.
**Capacidad de Generalización**: Al aplicar la misma arquitectura a Fashion MNIST, el código evidencia que la lógica de las DCGAN es versátil y puede adaptarse a diferentes distribuciones de datos (de números a prendas de vestir) ajustando simplemente el flujo de entrada.


  ## Cómo Ejecutar en Colab

### Opción 1: Cargar desde GitHub
1. Abre [Google Colab](https://colab.research.google.com/)
2. Selecciona **"Archivo"** → **"Abrir cuaderno"** → **"GitHub"**
3. Pega la URL del repositorio que contiene este notebook

### Opción 2: Cargar manualmente
1. Descarga el archivo `Week14_14_GANs.ipynb` de esta carpeta
2. Abre [Google Colab](https://colab.research.google.com/)
3. Selecciona **"Archivo"** → **"Subir cuaderno"**
4. Elige el archivo descargado

### Requisitos
- NumPy
- Matplotlib
- TensorFlow
- Keras

   
