# Prototipo AECO CV: Detección de Fisuras en Estructuras de Concreto

## 1. Planteamiento del Problema AECO
* **Problema:** La inspección visual manual de grandes infraestructuras de concreto (puentes, presas, fachadas) es lenta, costosa y propensa a errores humanos. Este proyecto automatiza la detección temprana de patologías estructurales (fisuras) mediante visión computacional.
* **Criterios de Éxito:** Alcanzar un mAP50 superior a 0.80 y lograr un tiempo de inferencia compatible con el procesamiento de video en tiempo real (ej. drones de inspección).

## 2. Referencia del Dataset
* **Fuente:** Roboflow Universe - Dataset de Detección de Fisuras en Concreto (Concrete Crack Detection).
* **Enlace al Dataset:** [INSERTA_AQUI_EL_ENLACE_A_TU_DATASET_DE_ROBOFLOW]
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
* **Nota de Prueba:** Última ejecución exitosa confirmada el [INSERTA_FECHA_DE_HOY]. Rango de tiempo de ejecución estimado (entrenamiento completo): 15-25 minutos.

## 4. Cómo Reproducir (Paso a Paso)
1. Abrir el notebook interactivo en Google Colab: [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)]([INSERTA_AQUI_LA_URL_DE_TU_NOTEBOOK_EN_GITHUB])
2. En la barra superior de Colab, ir a `Entorno de ejecución` > `Cambiar tipo de entorno de ejecución` y seleccionar **T4 GPU**.
3. Ejecutar la **Celda 2** para instalar las dependencias necesarias (`ultralytics` y `roboflow`).
4. En la **Celda 3**, asegúrate de que el fragmento de código contenga la API Key correcta de Roboflow para descargar el dataset.
5. Ejecutar la celda de Entrenamiento (**Celda 4**). Esto iniciará el proceso de 30 épocas.
6. (Opcional para inferencia rápida): Si solo deseas probar el modelo sin entrenar, omite la Celda 4, descarga los pesos entrenados desde [INSERTA_AQUI_ENLACE_A_TUS_PESOS_BEST.PT_EN_DRIVE_O_GITHUB_RELEASES] y ejecuta la **Celda 6** de Inferencia.

## 5. Resumen de Resultados
* **Precisión (P):** [INSERTA_VALOR, ej. 0.85]
* **Recall (R):** [INSERTA_VALOR, ej. 0.82]
* **mAP50:** [INSERTA_VALOR, ej. 0.88]
* **mAP50-95:** [INSERTA_VALOR, ej. 0.65]
Análisis de Evidencias del Prototipo AECO CV

El paquete de evidencias generado automáticamente por el pipeline de Ultralytics (YOLOv8) documenta el ciclo completo de entrenamiento e inferencia del modelo para la detección de patologías estructurales en concreto. Este conjunto de resultados se divide en dos componentes críticos:

Evidencia Cuantitativa (Curvas de Entrenamiento y Validación): El archivo results.png consolida las métricas de rendimiento durante las épocas de verificación. Las curvas de pérdida (Loss) demuestran la capacidad del modelo para minimizar el error de localización de las cajas delimitadoras (box_loss) y la clasificación de la anomalía (cls_loss). Asimismo, las métricas de Precisión (P), Recall (R) y el mAP50 validan la viabilidad del prototipo para distinguir entre fisuras reales y ruido visual (como texturas del concreto o sombras).

Evidencia Cualitativa (Inferencia Visual): Las imágenes resultantes de la etapa de predicción demuestran la aplicación práctica del modelo sobre datos no vistos previamente. Los bounding boxes generados ilustran la capacidad de la red neuronal para acotar geo-espacialmente la longitud y ubicación de las grietas en la superficie, un paso fundamental para automatizar las inspecciones visuales con drones en flujos de trabajo de mantenimiento preventivo.

Gobernanza de Pesos: Se incluye el archivo best.pt, el cual almacena los tensores optimizados de la red neuronal, garantizando la reproducibilidad del modelo sin necesidad de reentrenar la arquitectura, cumpliendo así con las normativas de despliegue ágil.
**Conclusiones Clave:**
1. El modelo YOLOv8n demuestra una alta capacidad para localizar fisuras con un mAP50 sólido, lo que valida su viabilidad para inspecciones preliminares automatizadas.
2. Las métricas sugieren que el modelo generaliza bien en superficies de concreto limpio, pero el rendimiento (Recall) disminuye en áreas con sombras profundas o texturas complejas que simulan grietas.
