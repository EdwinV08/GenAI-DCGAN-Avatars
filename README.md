# 🧬 GenAI-DCGAN: Generador de Avatares Sintéticos

> **Estado del Proyecto:** Completado (v1.0)  
> **Tecnologías:** PyTorch, Python, Gradio, Scikit-Learn  
> **Tipo:** Deep Convolutional Generative Adversarial Network (DCGAN)

## 📋 Descripción del Proyecto
Este proyecto implementa una solución de **Inteligencia Artificial Generativa** diseñada para crear rostros humanos sintéticos desde cero. El sistema aborda problemáticas de privacidad de datos (GDPR) y propiedad intelectual, permitiendo a diseñadores y desarrolladores generar "personas que no existen" para uso en prototipos, mockups y datasets de prueba.

La solución utiliza una arquitectura **DCGAN** entrenada con el dataset LFW (Labeled Faces in the Wild), optimizada con técnicas de *Label Smoothing* para mejorar la estabilidad del entrenamiento. Incluye una interfaz web interactiva basada en **Gradio**.

---

## ⚙️ Requisitos Técnicos

Para ejecutar este proyecto, se recomienda un entorno con aceleración por GPU (CUDA), como Google Colab o una máquina local con tarjeta NVIDIA.

### Dependencias Principales
*   Python 3.8+
*   PyTorch (con soporte CUDA)
*   Torchvision
*   Gradio (Interfaz UI)
*   Scikit-Learn (Carga de datasets)
*   Matplotlib (Visualización)

---

## 🚀 Manual de Instalación

### Opción A: Ejecución en la Nube (Google Colab) - Recomendado
1. Descarga el archivo `.ipynb` de este repositorio.
2. Súbelo a [Google Colab](https://colab.research.google.com/).
3. Asegúrate de activar la GPU: Ir a `Entorno de ejecución` > `Cambiar tipo de entorno de ejecución` > Seleccionar **T4 GPU**.
4. Ejecuta las celdas secuencialmente.

### Opción B: Ejecución Local
1. Clona este repositorio:
   ```bash
   git clone https://github.com/TU_USUARIO/GenAI-DCGAN-Avatars.git
   cd GenAI-DCGAN-Avatars

1.Crea un entorno virtual (Opcional pero recomendado):
python -m venv venv
source venv/bin/activate  # En Windows: venv\Scripts\activate

2.Instala las dependencias:
pip install -r requirements.txt

📖 Guía de Usuario

Una vez iniciado el entorno, sigue estos pasos para operar el sistema:
1. Entrenamiento del Modelo

Al ejecutar el script completo, el sistema realizará automáticamente:
- Descarga y preprocesamiento del dataset LFW.
- Inicialización de los pesos de la red neuronal.
- Fase de Entrenamiento: Verás en consola el progreso de las épocas (Loss del Generador y Discriminador).
Nota: Para una demo rápida, el entrenamiento dura aprox. 10 minutos (20-30 épocas). Para alta definición, ajustar a 200+ épocas.

2. Uso de la Interfaz Gráfica (Demo)
Al finalizar el script, se desplegará una interfaz web con Gradio.
- Local: Haz clic en el enlace http://127.0.0.1:7860.
- Público (Colab): Haz clic en el enlace generado automáticamente que termina en ...gradio.live.

Controles de la Interfaz:

- Slider "Cantidad de Rostros": Elige cuántos avatares generar simultáneamente (1 a 16).
- Slider "Semilla (Seed)":
  
    Usa -1 para generar caras totalmente nuevas y aleatorias.
    Usa un número fijo (ej. 42) para reproducir exactamente el mismo rostro generado anteriormente.
  
Botón "Generar": Crea las imágenes en tiempo real.

3. Interpretación de Resultados
   
- Si los rostros se ven borrosos: Es normal en resoluciones de 64x64px con pocas épocas.
- Si el Discriminador Loss llega a 0: Reinicia el entrenamiento; ha ocurrido un colapso. (El código actual incluye mitigaciones para esto).

🧠 Arquitectura del Modelo

El núcleo del sistema consta de dos redes adversarias:
Generador (G):
- Entrada: Vector latente z ∈R100
- Capas: 4 bloques de ConvTranspose2d + BatchNorm + ReLU.
- Salida: Imagen RGB 64x64.

Discriminador (D):
- Entrada: Imagen RGB 64x64.
- Capas: 4 bloques de Conv2d + LeakyReLU + Sigmoid.
- 
Optimizaciones Aplicadas:
- Inicialización de pesos con distribución Normal (0.0, 0.02).
- Label Smoothing (Real = 0.9) para evitar gradientes saturados.
  
📄 Licencia y Ética

Este proyecto tiene fines educativos y académicos.

- Dataset: LFW (Labeled Faces in the Wild) es de dominio público para investigación.
- Uso Ético: Las imágenes generadas no corresponden a personas reales. Se prohíbe el uso de este código para generar Deepfakes malintencionados o desinformación.
Desarrollado por [Adriana Aguilar y Edwin Villa] - Ingeniería de Software & Deep Learning





   
