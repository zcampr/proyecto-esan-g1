# Rotación temprana en operarios de almacén

**Proyecto ESAN · People Analytics**

Caso de negocio sobre la rotación temprana de operarios de almacén en una empresa industrial (anonimizada). Analizamos cuándo y por qué se van los trabajadores, construimos un modelo predictivo para identificar los factores asociados a la salida y propusimos acciones de selección y acompañamiento para el primer mes.

## Contenido del repositorio

| Archivo | Qué es |
|---|---|
| `presentacion_rotacion_temprana.html` | Presentación del caso (13 diapositivas). Descárgala y ábrela en el navegador, o publícala con GitHub Pages. |
| `preprocessing_data_ESAN.ipynb` | Limpieza de las bases de ingresos y ceses e ingeniería de variables para el modelo. |

## El problema

- La rotación mensual promedio subió **3 puntos porcentuales**: de 12 % en 2024 a 15 % entre enero y octubre de 2025.
- El **54 % de los ceses ocurre en el primer mes** de vínculo laboral.
- Los meses con más rotación tienden a tener más gasto en horas extras (correlación r ≈ 0.94 en 18 meses). Es una asociación, no una prueba de causa.

## Qué hicimos

1. **Limpieza de datos** (notebook):
   - Se quitaron los campos que identifican a las personas (nombre, código, correo y dirección). El DNI se usó solo como clave para unir las tablas y luego se eliminó.
   - Se eliminaron los registros duplicados por reingreso, conservando el último ingreso de cada persona.
   - Se unieron las bases de ingresos y ceses en una sola tabla (505 trabajadores).
   - Al calcular la antigüedad se trataron los registros con fecha de ingreso posterior a la fecha de cese.
2. **Ingeniería de variables** (notebook): edad, antigüedad en meses, nivel de rol agrupado a partir del cargo y variables indicadoras de división, estado civil, grado educativo y provincia.
3. **Análisis exploratorio:** rotación por mes y por tiempo de vínculo.
4. **Modelo predictivo:** comparamos tres algoritmos.

| Modelo | AUC-ROC | AUC-PR |
|---|---|---|
| **Regresión logística** (elegido) | ~0.71 | ~0.50 |
| Random Forest | ~0.66 | ~0.49 |
| Gradient Boosting | ~0.69 | ~0.45 |

Elegimos la regresión logística porque tuvo el mejor desempeño y es la más fácil de interpretar. Un AUC-ROC de 0.71 indica una capacidad predictiva moderada: el modelo sirve para identificar factores asociados a la salida, no para decidir sobre una persona en particular.

## Hallazgos y propuesta

- **Factores asociados a mayor permanencia.** Los relacionados con el puesto son el nivel educativo y la experiencia en zonas logísticas o industriales. Las variables personales (edad, estado civil y lugar de residencia) no se usan como criterio de selección, en línea con la Ley 26772, y sirven para diseñar acciones de inducción, transporte y acompañamiento.
- **Rediseño de la selección:** entrevista estructurada por competencias, assessment conductual y preview realista del puesto.
- **Mentor con experiencia** durante el primer mes.
- **Valor esperado:** si la rotación mensual baja de 15 % a 10 %, se estima una eficiencia de aproximadamente **S/ 32 mil al año**, por ahorro en costos de reclutamiento y equipos de protección personal, y en horas extras. Es una estimación bajo premisas, no un ahorro logrado.
- **Siguiente paso propuesto:** validar la propuesta con un piloto con grupo control. El piloto no se ejecutó.

## Datos y confidencialidad

Los datos son reales y pertenecen a la empresa, por eso **no se incluyen en este repositorio**.

## Herramientas

Python (pandas, NumPy) en Google Colab.

## Equipo

Equipo de ESAN, Grupo 1.
