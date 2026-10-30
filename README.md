# Proyecto de regresión lineal y clasificación a partir de un dataset de estudiantes

## Objetivo
El objetivo de este proyecto es analizar los datos de un grupo de estudiantes y, tras la limpieza y preprocesamiento de los datos, aplicar dos modelos:
- Regresión lineal: predecir la nota final.
- Clasificación: predecir si un estudiante aprueba o suspende.
El trabajo se ha realizado en Python mediante un Jupyter Notebook. El código está organizado en cuatro bloques:
- Análisis exploratorio del conjunto de datos
- Preprocesamiento de los datos
- Entrenamiento y validación del modelo de regresión
- Entrenamiento y validación del modelo de clasificación

## Archivos necesarios
- Proyecto_Regre_Clas_Alinares.ipynb: notebook con el código, las explicaciones y los resultados.
- dataset_estudiantes.csv: conjunto de datos utilizado.
- README.md: descripción del proyecto y conclusiones.

## Requisitos para la ejecución del proyecto
- Python
- Jupyter Notebook
- Librerías: pandas, matplotlib, scikit-learn

## Descripción de los datos
El dataset contiene registros correspondientes a 1.000 estudiantes y tiene 11 columnas.
Nueve columnas se utilizan como datos de entrada: horas de estudio semanal, nota anterior, tasa de asistencia, horas de sueño, edad, nivel de dificultad, tutor, horario de estudio y estilo de aprendizaje.
Las otras dos columnas son las variables objetivo:
- nota_final: nota entre 0 y 100
- aprobado: valor binario, 1 si la nota final es igual o superior a 60 y 0 si es inferior a este valor

## Análisis exploratorio del conjunto de datos
Se revisan el tamaño del dataset, los tipos de datos, los valores nulos, los duplicados y las estadísticas básicas. También se utilizan gráficos y comparaciones entre grupos para conocer las relaciones entre las variables.
Los principales resultados son:
- No se encuentran filas duplicadas.
- Hay 150 valores nulos en horas de sueño, 100 en horario de estudio y 50 en estilo de aprendizaje.
- La nota final media es de 71,44 puntos.
- Hay 898 aprobados y 102 suspensos, por lo que ambos grupos tienen tamaños muy diferentes.
- Las horas de estudio, la nota anterior y la asistencia presentan relaciones positivas con la nota final. Sus correlaciones de Pearson son aproximadamente 0,514, 0,470 y 0,317.
- Los estudiantes con tutor tienen una nota media mayor. Las diferencias entre horarios y estilos de aprendizaje son pequeñas.
- Los valores atípicos observados se mantienen porque son valores posibles.

## Preprocesamiento de los datos
Se reservan 800 estudiantes para entrenamiento y 200 para prueba, manteniendo aproximadamente la proporción de aprobados y suspensos. Se mantiene el orden original de los datos en la divisón.
La preparación de los datos incluye:
- Convertir la variable tiene tutor a valores 0 y 1.
- Convertir los niveles de dificultad a valores 0, 1 y 2.
- Sustituir los nulos de horas de sueño por la mediana de de los datos de entrenamiento (7.03 horas). Se utiliza este mismo valor para rellenar los valores nulos de los datos de prueba.
- Completar en las variables horarios de estudio preferidos y estilos de aprendizaje, los campos sin información con la categoría "Desconocido".
- Crear manualmente columnas de 0 y 1 para cada horario y estilo de aprendizaje.
- Comprobar los tipos de datos, los valores nulos y los nombres de columnas duplicados.
- Escalar las variables numéricas utilizando el mínimo y el máximo de entrenamiento, utilizando los límites de los datos de entrenamiento también para los de prueba.
Finalmente, queda un dataframe con 16 columnas de entrada.

## Entrenamiento y validación del modelo de regresión
Se utiliza LinearRegression para predecir la nota final. Las predicciones se comparan con las notas reales de los 200 estudiantes de prueba.
Las métricas utilizadas y sus resultados son las siguientes:
- MAE (Mean Absolute Error): diferencia media en valor absoluto entre la nota real y la predicción. El resultado es de 6,12 puntos de diferencia.
- R2: porcentaje de notas que es capaz de explicar el modelo. El resultado es de 0.3949, por lo que el modelo es capaz de explicar el 39,49% de las notas.
- RMSE (Root Mean Squared Error): media de errores que comete el modelo comparado con el resultado real. El resultado de este error medio es de 7.45.

Como conclusión, los resultados del modelo:
- Tienen gran proximidad a los reales en los valores centrales.
- En notas bajas, el modelo tiende a sobreestimar la nota prevista.
- En notas altas, el modelo tiende a subestimar la nota prevista.

## Entrenamiento y validación del modelo de clasificación
Se utiliza un modelo de regresión logística (LogisticRegression) para predecir aprobado (1) o suspenso (0).
Comparando en los datos de prueba el resultado del modelo y el valor real se obtiene la siguiente conclusión (matriz de confusión):
- Suspensos reales: 20 -> suspensos modelo: 2
- Aprobados reales: 180 -> aprobados modelo: 179
Ante la desviación detectada sobre los suspensos, se utilizan dos métricas para analizar los registros correspondientes a alumnos suspensos:
- Precision_score: porcentaje de suspensos identificados por el modelo sobre los suspensos reales. El resultado es del 66,67%.
- Recall_score: porcentaje de suspensos reales que el modelo ha sido capaz de detectar. El resultado es del 10%.

El modelo predice tres suspensos y acierta en dos de ellos. Sin embargo, solo detecta 2 de los 20 suspensos reales y deja 18 sin detectar. Aunque el porcentaje de aciertos es elevado (90%), el modelo tiene muchas dificultades para detectar los alumnos que suspenden siendo una deficiencia importante.

## Conclusiones
Se han completado los cuatro bloques del proyecto utilizando modelos básicos y una preparación de datos explicada paso a paso.
La regresión permite aproximar las notas finales, aunque mantiene un error considerable y no reproduce toda su variación. La clasificación consigue un porcentaje alto de aciertos, pero detecta pocos suspensos. Esto muestra por qué es necesario revisar varias métricas y no quedarse solo con el porcentaje de aciertos.
Los resultados corresponden a una única división de entrenamiento y prueba. No se ha realizado validación cruzada ni comparación de distintas configuraciones de los modelos. Además, solo hay 20 suspensos en prueba: detectar uno más o uno menos cambia el recall en cinco puntos porcentuales.
Al conservar todas las columnas de horario y estilo, existe información redundante. No se han interpretado los coeficientes de la regresión lineal como efectos individuales de cada categoría.
Como posible mejora futura, se podría estudiar cómo detectar más suspensos teniendo en cuenta el desequilibrio entre los dos grupos, utilizando los datos de entrenamiento para elegir los cambios y reservando los de prueba para la evaluación final.
