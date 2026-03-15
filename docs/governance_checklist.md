# Checklist de Gobernanza, Licencias y Limitaciones

## 1. Privacidad y Consentimiento
* [X] **Evaluación de PII (Información Personal Identificable):** El dataset utilizado consiste exclusivamente en fotografías de superficies inanimadas (concreto, muros, estructuras). No contiene rostros humanos, placas de vehículos ni elementos que comprometan la privacidad de individuos o trabajadores. No se requiere anonimización adicional.

## 2. Minimización de Datos
* [X] **Relevancia y Alcance:** Las imágenes recopiladas se limitan a acercamientos técnicos de las estructuras evaluadas. No se han almacenado ni procesado metadatos de geolocalización (GPS) o información temporal (EXIF) que pudiera identificar instalaciones críticas o estratégicas sin la debida autorización.

## 3. Declaración de Limitaciones (Cuándo NO usar el modelo)
* Este prototipo es una herramienta de asistencia visual y **NUNCA debe sustituir la evaluación técnica, el criterio o el dictamen de un ingeniero estructural certificado.**
* El modelo no es funcional ni confiable en condiciones de iluminación nula o extremadamente baja (ej. inspecciones nocturnas sin iluminación artificial adecuada).
* Ha sido entrenado específicamente para concreto; su uso en asfalto, madera, mampostería de ladrillo o superficies metálicas producirá resultados impredecibles y no válidos.

## 4. Nota de Riesgos: Falsos Positivos vs. Falsos Negativos
* **Riesgo Crítico: Falsos Negativos (FN).** El mayor riesgo operacional recae en que el modelo omita una fisura real severa (FN). Esto podría derivar en una falta de mantenimiento preventivo y, en casos extremos, fallos estructurales no atendidos.
* **Impacto Secundario: Falsos Positivos (FP).** Detectar erróneamente una mancha, un cable o una junta como fisura (FP) genera "ruido" en el reporte. Aunque esto aumenta el tiempo de revisión manual redundante por parte del inspector, no representa un riesgo directo para la integridad estructural.

## 5. Licencia y Derechos de Datos
* **Licencia del Código:** El código fuente y los notebooks de este repositorio se distribuyen bajo licencia **MIT**.
* **Derechos del Dataset:** El dataset utilizado pertenece a sus respectivos autores en Roboflow Universe y se utiliza bajo los términos de uso público de la plataforma con fines estrictamente académicos y de investigación.
