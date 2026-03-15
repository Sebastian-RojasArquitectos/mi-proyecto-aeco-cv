# Análisis de Errores y Plan de Iteración

Basado en la inspección visual de las predicciones del conjunto de validación, se identifican los siguientes patrones de error y áreas de mejora.

## 1. Falsos Positivos (FP) - ¿Qué detectó erróneamente y por qué?
1. **Juntas de Dilatación Constructivas:** El modelo frecuentemente enmarcó las juntas de dilatación o separaciones entre paneles prefabricados como fisuras. *Por qué:* Visualmente comparten la misma característica de línea recta, oscura y estrecha que una fisura regular.
2. **Cables Oscuros Sueltos:** En algunas imágenes con instalaciones eléctricas expuestas, los cables negros sobre el concreto gris fueron detectados como fisuras largas. *Por qué:* El contraste y la geometría tubular del cable en 2D simula el patrón de alto contraste de una grieta profunda.
3. **Manchas de Humedad Lineales / Escurrimientos:** El agua al escurrir genera líneas oscuras en el concreto que el modelo confundió. *Por qué:* La diferencia de textura y color (más oscuro) engaña al detector de bordes de la red neuronal.

## 2. Falsos Negativos (FN) - ¿Qué omitió y por qué?
1. **Microfisuras Capilares:** Fisuras extremadamente finas no fueron detectadas. *Por qué:* La resolución de entrada (`imgsz=640`) hace que las características de unos pocos píxeles de grosor se pierdan tras las capas de convolución iniciales (pérdida de información espacial fina).
2. **Fisuras en Zonas de Sombra Intensa:** Las grietas ubicadas debajo de voladizos o elementos que proyectan sombra dura fueron ignoradas. *Por qué:* La falta de contraste entre la fisura oscura y la sombra circundante impide que el modelo extraiga los bordes correctamente.
3. **Fisuras en Imágenes con Desenfoque por Movimiento (Motion Blur):** *Por qué:* Los bordes de la fisura se difuminan con el fondo gris, eliminando el gradiente nítido que YOLO necesita para activar las detecciones.

## 3. Plan de Iteración: Mejoras Prioritarias de Datos
Para mitigar estos errores en la siguiente versión del modelo, se proponen tres acciones concretas en la gestión del dataset:

1. **Inclusión de Imágenes de Fondo (Background Images):** Añadir al dataset de entrenamiento un 10-15% de imágenes de concreto puro que contengan *exclusivamente* cables, juntas de dilatación y manchas de humedad, **sin ninguna anotación** (cero bounding boxes). Esto forzará al modelo a aprender estas características como "fondo" y reducirá los FP drásticamente.
2. **Aumento de la Resolución de Entrenamiento y Tiling:** Para detectar microfisuras (reducir FN), incrementar el tamaño de imagen de entrenamiento (`imgsz=1024`) o implementar técnicas de *slicing/tiling* (SAHI), dividiendo las imágenes grandes en parches más pequeños antes de la inferencia para conservar la resolución de los capilares finos.
3. **Data Augmentation Específico:** Aplicar variaciones agresivas de brillo y contraste (Brightness & Contrast augmentation) durante el preprocesamiento en Roboflow para simular las condiciones de sombra intensa, mejorando la robustez ante diferentes escenarios de iluminación.
