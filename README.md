# Proyecto de regresión lineal y clasificación a partir de un dataset de estudiantes

## Objetivo
El objetivo de este proyecto es analizar los datos de un grupo de estudiantes y, tras la limpieza y preprocesamiento de los datos, aplicar dos modelos:
- Regresión lineal: predecir la nota final.
- Clasificación: predecir si un estudiante aprueba o suspende.
El trabajo se ha realizado en Python mediante un Jupyter Notebook. El código está organizado en cuatro bloques:
1.- Análisis exploratorio del conjunto de datos
2.- Preprocesamiento de los datos
3.- Entrenamiento y validación del modelo de regresión
4.- Entrenamiento y validación del modelo de clasificación

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
