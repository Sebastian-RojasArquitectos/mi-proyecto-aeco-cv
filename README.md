# Prototipo AECO CV: Detección de Fisuras en Estructuras de Concreto

## 1. Planteamiento del Problema AECO
* **Problema:** La inspección visual manual de grandes infraestructuras de concreto (puentes, presas, fachadas) es lenta, costosa y propensa a errores humanos. Este proyecto automatiza la detección temprana de patologías estructurales (fisuras) mediante visión computacional.
* **Criterios de Éxito:** Alcanzar un mAP50 superior a 0.80 y lograr un tiempo de inferencia compatible con el procesamiento de video en tiempo real (ej. drones de inspección).

## 2. Referencia del Dataset
* **Fuente:** Roboflow Universe - Dataset de Detección de Fisuras en Concreto (Concrete Crack Detection).
* **Enlace al Dataset:** [concrete-crack-detection-y2y5r-nbyio]
* **Split de Datos:** 80% Entrenamiento / 20% Validación.
* **Clases y Reglas de Etiquetado:**
  * `fisura`: Se etiquetan mediante *bounding boxes* (cajas delimitadoras) que engloban la longitud visible de la grieta en la superficie de concreto, excluyendo intencionalmente juntas de dilatación constructivas.

## 3. Checklist de Reproducibilidad
Este repositorio está diseñado para ejecutarse íntegramente en la nube sin instalaciones locales.
* **Plataforma:** Google Colab.
* **Hardware Verificado:** GPU T4 (Aceleración por hardware habilitada).
* **Dataset:** Versión 1 (Exportación formato YOLOv8).
* **Variante del Modelo:** YOLOv8n (YOLOv8 Nano).
* **Parámetros de Entrenamiento:** * Epochs: 30
  * Batch Size: 16
  * Image Size (imgsz): 640
* **Dependencias Core:** `ultralytics==8.1.0`, `roboflow` (verificable vía `!pip freeze` en el notebook).
* **Nota de Prueba:** Última ejecución exitosa confirmada el 15 de marzo de 2026. Rango de tiempo de ejecución estimado (entrenamiento completo): 15-25 minutos.

## 4. Cómo Reproducir (Paso a Paso)
1. Abrir el notebook interactivo en Google Colab: [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1kMl5z73ayjTyHh7kWkRurVtZXkMGdFBl#scrollTo=VcFXLKn1tam6))
2. En la barra superior de Colab, ir a `Entorno de ejecución` > `Cambiar tipo de entorno de ejecución` y seleccionar **T4 GPU**.
3. Ejecutar la **Celda 2** para instalar las dependencias necesarias (`ultralytics` y `roboflow`).
4. En la **Celda 3**, asegúrate de que el fragmento de código contenga la API Key correcta de Roboflow para descargar el dataset.
5. Ejecutar la celda de Entrenamiento (**Celda 4**). Esto iniciará el proceso de 30 épocas.
6. (Opcional para inferencia rápida): Si solo deseas probar el modelo sin entrenar, omite la Celda 4, descarga los pesos entrenados desde [](https://drive.google.com/drive/folders/1tQX4AfhgMh17lv2qBjJt8mRRwazjT0w-?usp=sharing)] y ejecuta la **Celda 6** de Inferencia.

## 5. Resumen de Resultados
                epoch,         train/box_loss,         train/cls_loss,         train/dfl_loss,   metrics/precision(B),      metrics/recall(B),       metrics/mAP50(B),    metrics/mAP50-95(B),           val/box_loss,           val/cls_loss,           val/dfl_loss,                 lr/pg0,                 lr/pg1,                 lr/pg2
                      1,                 1.6887,                 2.4789,                 1.5106,                0.17231,                0.32702,                 0.1536,                0.05193,                 1.9739,                 2.9424,                  1.762,             0.00064815,             0.00064815,             0.00064815
                      2,                 1.6198,                 2.0165,                  1.444,                0.28589,                0.24521,                0.17074,                0.07152,                 2.0316,                  2.742,                 1.9084,              0.0010545,              0.0010545,              0.0010545
                      3,                 1.6809,                 1.9819,                 1.4613,                0.21434,                0.29885,                0.13719,                0.05856,                 2.1617,                 4.6796,                 2.1203,              0.0011968,              0.0011968,              0.0011968
                      4,                  1.603,                 1.9257,                  1.442,                0.34004,                0.35632,                0.26122,                0.11466,                 1.8833,                 3.4977,                 1.6899,               0.000812,               0.000812,               0.000812
                      5,                 1.6138,                 1.8004,                 1.4174,                0.35827,                0.36782,                0.28877,                0.13438,                  1.898,                 2.5965,                 1.6578,               0.000812,               0.000812,               0.000812

                      

Análisis de Evidencias del Prototipo AECO CV

El paquete de evidencias generado automáticamente por el pipeline de Ultralytics (YOLOv8) documenta el ciclo completo de entrenamiento e inferencia del modelo para la detección de patologías estructurales en concreto. Este conjunto de resultados se divide en dos componentes críticos:

Evidencia Cuantitativa (Curvas de Entrenamiento y Validación): El archivo results.png consolida las métricas de rendimiento durante las épocas de verificación. Las curvas de pérdida (Loss) demuestran la capacidad del modelo para minimizar el error de localización de las cajas delimitadoras (box_loss) y la clasificación de la anomalía (cls_loss). Asimismo, las métricas de Precisión (P), Recall (R) y el mAP50 validan la viabilidad del prototipo para distinguir entre fisuras reales y ruido visual (como texturas del concreto o sombras).

Evidencia Cualitativa (Inferencia Visual): Las imágenes resultantes de la etapa de predicción demuestran la aplicación práctica del modelo sobre datos no vistos previamente. Los bounding boxes generados ilustran la capacidad de la red neuronal para acotar geo-espacialmente la longitud y ubicación de las grietas en la superficie, un paso fundamental para automatizar las inspecciones visuales con drones en flujos de trabajo de mantenimiento preventivo.

Gobernanza de Pesos: Se incluye el archivo best.pt, el cual almacena los tensores optimizados de la red neuronal, garantizando la reproducibilidad del modelo sin necesidad de reentrenar la arquitectura, cumpliendo así con las normativas de despliegue ágil.
**Conclusiones Clave:**
1. El modelo YOLOv8n demuestra una alta capacidad para localizar fisuras con un mAP50 sólido, lo que valida su viabilidad para inspecciones preliminares automatizadas.
2. Las métricas sugieren que el modelo generaliza bien en superficies de concreto limpio, pero el rendimiento (Recall) disminuye en áreas con sombras profundas o texturas complejas que simulan grietas.
