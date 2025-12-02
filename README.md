# 🧬 GenAI-DCGAN: Generador de Avatares Sintéticos

<!-- Badge de Colab para acceso rápido -->
[![Python](https://img.shields.io/badge/Python-3.8%2B-blue)](https://www.python.org/)
[![PyTorch](https://img.shields.io/badge/PyTorch-2.0%2B-ee4c2c)](https://pytorch.org/)
[![Gradio](https://img.shields.io/badge/Gradio-UI-orange)](https://gradio.app/)

> **Proyecto de Ingeniería de Software / Deep Learning**  
> Desarrollo de una Red Generativa Adversaria (DCGAN) capaz de sintetizar rostros humanos originales a partir de ruido gaussiano, enfocado en privacidad de datos y diseño UX.

---

## 📋 Descripción del Proyecto

En el contexto actual de la protección de datos (GDPR/CCPA) y los derechos de imagen, el uso de fotografías reales para prototipado de software, campañas de marketing o entrenamiento de IAs plantea riesgos legales y éticos significativos.

Este proyecto implementa una solución de **Inteligencia Artificial Generativa** que crea "personas que no existen". Utilizando una arquitectura DCGAN entrenada sobre el dataset LFW (Labeled Faces in the Wild), el sistema aprende la distribución latente de los rasgos faciales humanos para generar nuevas muestras on-demand.

### ✨ Características Principales
*   **Generación en Tiempo Real:** Inferencia rápida en CPU/GPU tras el entrenamiento.
*   **Interfaz Interactiva:** Dashboard web basado en Gradio para controlar la generación.
*   **Privacidad por Diseño:** Los avatares generados son sintéticos y libres de derechos.
*   **Entrenamiento Estable:** Implementación de técnicas como *Label Smoothing* para mitigar el colapso del modo.

---

## 🛠️ Stack Tecnológico

*   **Lenguaje:** Python 3.10+
*   **Motor de IA:** PyTorch & Torchvision
*   **Interfaz:** Gradio 3.x
*   **Procesamiento de Datos:** NumPy, Scikit-Learn
*   **Visualización:** Matplotlib

---

## 🧠 Arquitectura del Modelo (Deep Learning)

El sistema se basa en un juego de suma cero entre dos redes neuronales profundas (DCGAN):

| Componente | Estructura Técnica | Función |
| :--- | :--- | :--- |
| **Generador (G)** | `Input Z(100)` $\to$ `ConvTranspose2d` $\to$ `BatchNorm` $\to$ `ReLU` $\to$ `Output(64x64)` | Toma un vector de ruido y "sueña" una imagen. |
| **Discriminador (D)** | `Input(64x64)` $\to$ `Conv2d` $\to$ `LeakyReLU(0.2)` $\to$ `Sigmoid` | Actúa como crítico, clasificando si la imagen es real o falsa. |

### Optimizaciones Implementadas
1.  **Label Smoothing:** Se ajustaron las etiquetas reales a `0.9` en lugar de `1.0`. Esto introduce incertidumbre en el Discriminador, evitando que se vuelva demasiado "confiado" y permitiendo que el Generador aprenda durante más tiempo.
2.  **Pesos Iniciales:** Inicialización personalizada con distribución normal (`mean=0.0`, `std=0.02`) según el paper de Radford et al.
3.  **Optimizador:** Adam (`lr=0.0002`, `beta1=0.5`).

---

## 🚀 Guía de Instalación y Ejecución

Existen dos formas de ejecutar este proyecto:

### Opción A: Google Colab (Recomendada)
Para probar el sistema sin instalaciones locales y usando GPUs gratuitas:
1.  Haz clic en el botón **"Open in Colab"** al inicio de este documento.
2.  En Colab, ve a `Entorno de ejecución` > `Cambiar tipo de entorno` > **T4 GPU**.
3.  Ejecuta todas las celdas (Menú `Entorno de ejecución` > `Ejecutar todas`).
4.  Al finalizar, busca el enlace público generado al final (ej: `https://xxxx.gradio.live`).

### Opción B: Ejecución Local
1.  **Clonar repositorio:**
    ```bash
    git clone https://github.com/TU_USUARIO/NOMBRE_DEL_REPO.git
    cd NOMBRE_DEL_REPO
    ```
2.  **Instalar dependencias:**
    ```bash
    pip install -r requirements.txt
    ```
3.  **Ejecutar Jupyter Notebook:**
    ```bash
    jupyter notebook
    ```
    Y abre el archivo `.ipynb`.

---

## 📖 Manual de Usuario

Una vez desplegada la interfaz de Gradio, encontrarás los siguientes controles:

1.  **Slider "Cantidad de Avatares":**
    *   Define cuántas imágenes generar en lote (1 a 16).
    *   *Tip:* Generar más imágenes consume más RAM, pero permite ver más variedad.
2.  **Slider "Semilla (Seed)":**
    *   Valor `-1`: Generación totalmente aleatoria.
    *   Valor `> 0` (ej. 42): Generación determinista. Útil si encuentras un rostro que te gusta y quieres volver a generarlo idéntico.
3.  **Botón "Generar":**
    *   Dispara el proceso de inferencia. La primera vez puede tardar unos segundos mientras el modelo calienta.

---

## ⚖️ Análisis Ético y Limitaciones

Como parte del desarrollo responsable de IA, se declaran los siguientes aspectos:

*   **Sesgos del Dataset:** El modelo fue entrenado con LFW, un dataset académico histórico que presenta un desbalance significativo hacia sujetos caucásicos, adultos y masculinos. Por ende, las generaciones del modelo reflejarán estos sesgos demográficos.
    *   *Mitigación propuesta:* Para versiones futuras, se recomienda curar el dataset o utilizar alternativas más inclusivas como *FairFace*.
*   **Resolución:** La arquitectura actual genera imágenes de **64x64 pixeles**. Son útiles como íconos o avatares pequeños, pero no aptas para impresión de gran formato. Se requeriría escalar a *StyleGAN* o implementar *Super-Resolución* para HD.
*   **Uso Malicioso:** Aunque las imágenes son sintéticas, el proyecto está diseñado estrictamente para fines de diseño y desarrollo. No se autoriza su uso para creación de perfiles falsos destinados a la desinformación (astroturfing).

---

> ⚠️ **Nota de Rendimiento:** Se incluye un notebook optimizado para **Kaggle** (`KAguilar_Adriana_Villa_Edwin_EA3_GenerativeAI_NB_k`). Se recomienda utilizar esta versión para entrenar el modelo, ya que aprovecha las **GPUs T4 x2** y permite una ejecución estable de 300+ épocas para obtener resultados de alta definición. Se uso como comparativo en temas de optimización de recursos de google colab vs Kaggle.

## 📄 Licencia

Este proyecto es de código abierto bajo la Licencia MIT. Eres libre de usarlo, modificarlo y distribuirlo, citando la autoría original.

**Desarrollado por Adriana Aguilar y Edwin Villa**  
*Ingeniería de Software y Datos*
