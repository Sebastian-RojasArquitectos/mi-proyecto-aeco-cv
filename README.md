# [Nombre de tu Proyecto AECO - ej. Detección de Fisuras en Concreto con YOLOv8]

## 1. Problema AECO y Criterios de Éxito
* **Problema:** [Describe en 2 líneas qué problema de Arquitectura, Ingeniería o Construcción estás resolviendo. Ej: Inspección visual automatizada de fachadas para identificar grietas].
* **Criterios de Éxito:** Alcanzar un mAP50 superior a [ej. 0.75] y lograr inferencia en tiempo real para viabilizar su uso en drones de inspección.

## 2. Dataset y Clases
* **Enlace al Dataset:** https://www.youtube.com/watch?v=IF9CoBWPnyQ
* **Split de Datos:** 80% Entrenamiento / 20% Validación (y Test).
* **Clases y Reglas de Etiquetado:**
  * `clase_1`: [Ej. 'fisura_severa'] - [Breve regla, ej: "Etiquetar solo grietas mayores a 2mm de grosor visible"].
  * `clase_2`: [Ej. 'fisura_leve'] - [Breve regla].

## 3. Checklist de Reproducibilidad
Para garantizar que este proyecto se puede replicar sin instalaciones locales, se ha utilizado Google Colab.
* **Versión del Dataset:** [Ej. v1]
* **Variante del Modelo:** YOLOv8[n/s] (Ultralytics)
* **Hiperparámetros:** Epochs: [ej. 30] | Batch Size: [ej. 16] | Img Size: [ej. 640]
* **Versión de Ultralytics:** `ultralytics==8.Y.Z` (Verificar con `!pip show ultralytics`)

## 4. Cómo Reproducir (Paso a Paso)
1. Abrir el notebook en Google Colab haciendo clic aquí: [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](ENLACE_A_TU_NOTEBOOK_EN_GITHUB)
2. En Colab, ir a `Entorno de ejecución` > `Cambiar tipo de entorno de ejecución` y seleccionar **T4 GPU**.
3. Ejecutar la primera celda para instalar las dependencias (`!pip install ultralytics roboflow`).
4. (Opcional) Si deseas re-entrenar, ejecuta la sección "Entrenamiento". Tomará aproximadamente [X] minutos.
5. Para inferencia directa, salta a la sección "Inferencia" donde se descargarán los pesos pre-entrenados desde [GitHub Releases / Drive / URL directa] y se ejecutarán sobre imágenes de prueba.
* **Nota de Ejecución:** Última prueba exitosa el [Fecha] usando GPU T4.

## 5. Resumen de Resultados
* **Precisión (P):** [0.XX]
* **Recall (R):** [0.XX]
* **mAP50:** [0.XX]
* **mAP50-95:** [0.XX]
* **Conclusiones clave:**
 1. El modelo es altamente capaz de detectar [Clase 1], pero confunde [Clase 2] con fondo.
 2. [Conclusión 2].