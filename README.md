# Curso de herramientas de Análisis de Datos
# Alerta Temprana de Reprobación Estudiantil
## Descripción del Proyecto
Este repositorio contiene un proyecto de análisis de datos y modelado predictivo orientado a la identificación proactiva de estudiantes en riesgo de fracaso escolar, permitiendo a las instituciones educativas diseñar e implementar estrategias preventivas de apoyo escolar.
Las instituciones educativas enfrentan el desafío de identificar a los estudiantes en riesgo de fracaso escolar antes de las evaluaciones finales para poder intervenir a tiempo. Con una tasa general de aprobación estimada del 77,4% dentro de una muestra representativa de 100.000 registros, este proyecto
analiza patrones de comportamiento y características clave que definen al segmento de alumnos con riesgo de reprobación.

### Pregunta de Investigación
**¿Se puede predecir con precisión si un alumno va a reprobar un examen
basándose en su asistencia a clases y su rendimiento académico histórico?**

### Objetivos Generales
1. Desarrollar un modelo predictivo de clasificación que permita identificar tempranamente a los estudiantes con alto riesgo de reprobación para el diseño de estrategias preventivas de apoyo escolar.
2. Analizar los distintos factores y variables (conocimientos previos, hábitos, entorno y bienestar) que influyen en el estado de aprobación final de los estudiantes.

## Dataset utilizado
* **Fuente de los datos:** Kaggle Datasets
* **Nombre del dataset:** `student_exam_performance.csv `
* **Tamaño del dataset:** 100000 registros.
* **Información contenida:** El conjunto de datos recopila variables socioeducativas y académicas, tales como:
  * Porcentaje de asistencia a clases (`Percentage attendance`).
  * Promedio de calificaciones previo y puntaje de examen anterior (`Exam
score`).
  * Nivel de educación de los estudiantes (`Education level`).
  * Estado final de aprobación (`Pass` / `Fail`).

 ## Tecnologías Utilizadas
* **Lenguaje:** Python 3
* **Entorno:** Google Colab / Jupyter Notebooks
* **Librerías principales:**
  * `pandas` (Carga, manipulación, limpieza e imputación de datos)
  * `matplotlib` & `seaborn` (Visualización de datos y análisis exploratorio)

## Proceso de Limpieza e Imputación
1. **Duplicados:** Se verificó la inexistencia de registros duplicados en el dataset.
2. **Tratamiento de Nulos:** Se identificó que las variables clave presentaban menos del 10% de valores faltantes. Se optó por una estrategia de **imputación por la mediana** para las variables numéricas de interés:
   * `time_management_score`
   * `attendance_percentage`
   * `previous_gpa`

## Modelo de Alerta Temprana (Regla Lógica)
Se definió un criterio de alerta temprano basado en el historial académico y de asistencia del estudiante.

### Resultados del Modelo:
* **Total de alumnos reales reprobados (`Fail`):** 22,611
* **Alumnos en riesgo que efectivamente reprobaron:** 20,341
* **Porcentaje de coincidencia (Sensibilidad / Recall):** **89.96%**

*Este resultado demuestra que mediante estas tres métricas simples e históricas, es posible capturar de forma temprana a casi el 90% de los estudiantes que terminarán reprobando el curso.*

## Visualizaciones e Interpretación
Para validar si estas variables seleccionadas responden adecuadamente a nuestra pregunta de análisis, se desarrollaron tres gráficos con `seaborn`:

### 1. Distribución de Asistencia según el Estado de Aprobación (Boxplot)
* **Interpretación:** Este gráfico compara la asistencia de alumnos aprobados frente a reprobados. Se observa claramente que el grupo de alumnos que reprueba muestra una dispersión de asistencia más baja en comparación con los aprobados, teniendo su mediana notablemente desplazada hacia abajo.
* **Respuesta a la pregunta:** Confirma que la asistencia es un factor fuertemente asociado con el éxito del estudiante, validando su uso como una regla de corte dentro de nuestra alerta temprana.

### 2. GPA Previo vs. Calificación en Examen Previo (Scatterplot)
* **Interpretación:** Al cruzar el promedio histórico (GPA) con el examen previo en una muestra de 1,000 estudiantes, se evidencia una fuerte correlación lineal positiva. Los puntos rojos (estudiantes que finalmente reprobaron) se concentran casi en su totalidad en el extremo inferior izquierdo del gráfico (bajo GPA previo y baja nota en examen anterior).
* **Respuesta a la pregunta:** Demuestra visualmente que el rendimiento histórico es un predictor potente del resultado final. Un bajo desempeño previo anticipa de manera casi inequívoca una alta probabilidad de reprobación.

### 3. Relación entre la Alerta de Riesgo y la Aprobación Real (Countplot)
* **Interpretación:** Este gráfico de barras clasifica a los estudiantes según si el modelo activó o no la bandera de riesgo. En la barra de alumnos sin riesgo ('No'), el porcentaje de desaprobados reales es ínfimo. En cambio, en la barra de alumnos bajo alerta ('Sí'), se contiene a casi la totalidad de los estudiantes reprobados del conjunto de datos.
* **Respuesta a la pregunta:** Es una prueba para nuestra hipótesis. Muestra que la regla de clasificación basada en asistencia y notas previas no solo es simple, sino sumamente certera, capturando al 89.96% de los estudiantes en riesgo real antes de que realicen la evaluación final.

## Exportación
El dataset limpio, procesado y enriquecido con la variable lógica `alumnos_en_riesgo` fue exportado bajo el nombre de `student_exam_performance_limpio.csv` para su posterior consumo y visualización interactiva en herramientas de Business Intelligence como **Power BI**.

## Análisis del Tablero de Power BI: Predicción del Rendimiento Estudiantil
​El presente reporte visualiza los resultados del modelo predictivo y el análisis de los factores que influyen en el rendimiento académico de un total de 100.000 estudiantes, incorporando un segmento interactivo por Nivel de educación (High School y Undergraduate).
​### 1. Tarjetas de Métricas Principales 
​Total de Estudiantes: 100 mil registros analizados en el dataset.
​Porcentaje de Asistencia a Clases: Promedio general del 76%.
​Filtros Dinámicos: Segmentador por nivel de educación para alternar y comparar el comportamiento entre los distintos grupos.
​### 2. Relación entre Asistencia y Calificaciones (Gráfico de Dispersión)
​Descripción: Visualiza la correlación entre el porcentaje de asistencia a clases (eje horizontal) y la calificación porcentual de exámenes anteriores (eje vertical).
​Interpretación: Permite observar claramente cómo los estudiantes con menor porcentaje de asistencia se agrupan en las zonas de menores calificaciones, confirmando el impacto directo de la presencialidad en el éxito académico.
​### 3. Validación del Modelo de "Estudiantes en Riesgo" (Gráfico de Barras)
​Descripción: Compara la clasificación predictiva del modelo (Estudiantes en riesgo: True / False) frente al resultado real de los alumnos (Pass Status: Pass / Fail).
​Interpretación: Facilita la evaluación de la efectividad del modelo de alerta temprana, permitiendo verificar qué proporción de los alumnos catalogados en riesgo efectivamente reprobaron y cuáles lograron aprobar.
​### 4. 🍰 Distribución General del Estado de Aprobación (Gráfico de Torta)
​Descripción: Representa la proporción total del rendimiento académico final de la cohorte analizada.
​Métricas clave:
​Aprobados (Pass): 77.39% (o 77.19% según segmentación global)
​Reprobados (Fail): 22.61%
