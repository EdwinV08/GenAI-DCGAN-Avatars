# 🧬 Generación de Avatares Sintéticos con DCGAN

![Estado](https://img.shields.io/badge/Estado-Completado-green) ![Tech](https://img.shields.io/badge/Tech-PyTorch%20%7C%20Gradio-firebrick) ![Entorno](https://img.shields.io/badge/Entorno-Kaggle%20%2F%20Colab-blue)

## 📖 Introducción General

Este proyecto implementa una **Red Generativa Adversaria Convolucional Profunda (DCGAN)** diseñada para resolver problemáticas de privacidad de datos y derechos de autor en la industria del desarrollo de software y el marketing.

El sistema genera rostros humanos **sintéticos** (personas que no existen) a partir de ruido aleatorio. Esto permite a las empresas poblar bases de datos de prueba o crear maquetas de diseño sin infringir normativas como la **GDPR (Reglamento General de Protección de Datos)**, ya que no se utilizan fotografías de personas reales para el producto final.

## 📂 Estructura del Proyecto

El repositorio está organizado siguiendo el flujo de trabajo estándar de *Machine Learning Ops* (MLOps), dividido en notebook de ejecución y documentación:

```text
DCGAN-Synthetic-Faces/
├── 📄 README.md                 # Documentación general.
├── 📄 requirements.txt          # Dependencias y librerías necesarias. 
├── 📁 notebooks/
│   ├── 📓 Aguilar_Adriana_Villa_Edwin_EA3_GenerativeAI_NB_k.ipynb         # Versión OPTIMIZADA (GPUs T4x2, 300 épocas).
│   └── 📓 Aguilar_Adriana_Villa_Edwin_EA3_GenerativeAI_Notebook.ipynb     # Versión estándar para pruebas rápidas y temas academicos
├── 📁 results/                  # Evidencia generada
│   ├── 📊 comparativa_loss.png  # Gráfica de estabilidad de los experimentos.
│   └── 🖼️ evolution_sample.png  # Comparativa: Rostros borrosos vs Nítidos.
└── 📁 src_modules/              # (Lógica contenida en los notebooks)
    ├── A_Data_Pipeline.py       # Descarga y normalización (LFW Dataset).
    ├── B_Architecture.py        # Clases PyTorch: Generator() y Discriminator().
    ├── C_Experimentation.py     # Motor de pruebas de hiperparámetros.
    └── D_Interface_Gradio.py    # Backend de la Web App (UI).


**Capacidades del Sistema:**
*   ✅ Generación de imágenes RGB de 64x64px.
*   ✅ Entrenamiento estable optimizado mediante *Label Smoothing*.
*   ✅ Interfaz Web interactiva para la generación bajo demanda y auditoría técnica.

---

## ⚙️ Requisitos e Instalación

El proyecto está autocontenido en Notebooks de Python y diseñado para ejecutarse en la nube (Kaggle/Colab). Las dependencias principales se instalan automáticamente al inicio del script:

*   **PyTorch & Torchvision:** Núcleo de Deep Learning.
*   **Gradio:** Para el despliegue de la interfaz de usuario.
*   **Scikit-learn:** Para la descarga controlada del dataset LFW.
*   **Matplotlib:** Para la visualización de pérdidas y resultados en tiempo real.

---

## 🛠️ Configuración y Entornos

Se proporcionan dos versiones del notebook. Seleccione la adecuada según sus necesidades de rendimiento:

### 🏆 Opción A: Versión Kaggle (Recomendada - Alta Calidad)
**Archivo:** `DCGAN_Kaggle_Optimized.ipynb`

Esta versión aprovecha las **GPUs T4 x2** de Kaggle para realizar un entrenamiento profundo de **300 épocas**, logrando la mayor nitidez visual.

> **⚠️ GUÍA DE EJECUCIÓN OBLIGATORIA EN KAGGLE:**
> Para evitar errores de conexión o rendimiento, ajuste el panel derecho ("Session Options"):
> 1.  **Accelerator:** Seleccione `GPU T4 x2` (o P100).
> 2.  **Internet:** Cambie a `Internet On`. (Requerido para bajar librerías y dataset).
>     * *Nota: Si la opción está bloqueada, Kaggle requiere verificar su cuenta con un número celular.*
> 3.  **Persistencia:** Opcional. Cambie a "Files only" si desea descargar el modelo `.pth` resultante.

### Opción B: Versión Colab (Estándar)
**Archivo:** `DCGAN_Colab_Standard.ipynb`
Versión ideal para pruebas rápidas o integración con Google Drive.
*   Configuración: Vaya a *Entorno de ejecución > Cambiar tipo de entorno > Acelerador de hardware: GPU T4*.

---

## 🚀 Guía de Uso

1.  **Carga del Notebook:** Abra el archivo `.ipynb` correspondiente en la plataforma seleccionada.
2.  **Ejecución Secuencial:** Ejecute todas las celdas en orden. El sistema realizará:
    *   Descarga y normalización del dataset (corrige el bug de tensores negros).
    *   Entrenamiento del modelo final.
    *   Lanzamiento del servidor web.
3.  **Acceso a la Demo:** Al finalizar, el notebook lanzará un servidor de Gradio y proporcionará un **Enlace Público** (ej. `https://xxxx.gradio.live`).
    *   Cree, copie el enlace y ábralo en una nueva pestaña.
    *   *Nota: No detenga la ejecución de la celda mientras usa la interfaz.*

---

## 🧪 Experimentación Técnica

Durante el desarrollo, se validaron tres hipótesis mediante experimentación automatizada para asegurar la estabilidad del modelo:

| Experimento | Estrategia | Resultado | Conclusión |
| :--- | :--- | :--- | :--- |
| **Exp 1** | **Label Smoothing (Targets = 0.9)** | ✅ **Estable** | **Seleccionado.** Mantuvo el equilibrio de Nash evitando que el discriminador saturara el gradiente. |
| **Exp 2** | Tasas Diferenciales ($LR_G > LR_D$) | ❌ Inestable | Generó una pérdida inicial excesiva (>3.0) y artefactos visuales de alta frecuencia. |
| **Exp 3** | Vector Latente Aumentado ($Z=128$) | ⚠️ Volátil | Mostró inestabilidad y caída drástica de la función de pérdida hacia el final. |

---

## 💼 Aplicación Práctica

La interfaz incluida resuelve tres casos de uso empresariales:

1.  **DevSecOps:** Provisión de avatares sintéticos para bases de datos de QA (Quality Assurance), eliminando riesgos legales.
2.  **Diseño UX/UI:** Creación de *Buyer Personas* visuales para prototipado rápido de aplicaciones.
3.  **Entretenimiento:** Generación procedural de texturas faciales para NPCs en videojuegos.

Nota sobre Métricas de Evaluación:
"Debido a la naturaleza de demostración interactiva en tiempo real del proyecto, se seleccionó la Evaluación Cualitativa (Visual Inspection) y el monitoreo de Estabilidad de Nash (Generator/Discriminator Loss) como métricas principales. Se desestimó el uso de FID (Fréchet Inception Distance) para priorizar el tiempo de cómputo en la maximización de épocas de entrenamiento (300 épocas), dado que el FID requiere inferencia masiva sobre una red InceptionV3 externa, lo cual excedía la latencia objetivo de la demostración."

---

## 📄 Licencia y Datos

*   **Dataset Base:** [Labeled Faces in the Wild (LFW)](http://vis-www.cs.umass.edu/lfw/). Utilizado bajo licencia académica/investigativa.
*   **Licencia del Código:** Este proyecto se distribuye bajo licencia **MIT** para fines educativos.
*   **Autoría:** Desarrollado como Proyecto Final de Ingeniería de Software y datos (Deep Learning avanzado).
*   Autores: Adriana Aguilar y Edwin Villa.

---
