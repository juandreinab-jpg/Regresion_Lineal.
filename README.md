Regresion_Lineal.ipynb

Miembros:

Maria elena quimbayo patiño 100816

Diana carolina quiroga

Juan david reina bogota 90230

**Parte 1: Definición del Problema**
Piensa en tu experiencia académica o laboral en un área de operaciones y elige un problema relacionado con inventarios, calidad, mantenimiento o productividad.

1. Indica cuál es tu variable dependiente Y (aquello que quieres predecir o clasificar).
2. Lista entre 3 y 5 variables independientes X que medirías para predecir Y.
3. Especifica si tu problema es de regresión (predecir un valor numérico) o de clasificación.
Respuesta (escribe aquí):

Respuesta 1: 
Variable dependiente (Y): Nivel de productividad diaria de la planta (unidades producidas por día).

Respuesta 2:
Variables independientes (X):

A. Horas de operación de la maquinaria.

B. Cantidad de materia prima disponible al inicio de la jornada.

C. Número de trabajadores asignados a la línea de producción.

D. Tiempo promedio de inactividad por fallas o mantenimiento.

E. Nivel de calidad del insumo (índice de defectos en materia prima).

Respuesta 3:
Es un problema de regresión, ya que se busca predecir un valor numérico (unidades producidas).


**Parte 2: Preprocesamiento de Datos y *Leakage***
Basado en el caso que definiste en la Parte 1:

1. Lista entre 3 y 5 transformaciones que aplicarías a tus datos (ej. imputación de valores faltantes, codificación de variables categóricas, escalado, creación de lags, etc.) y justifica por qué cada una es necesaria.

RTA/ Respuesta 1 (Transformaciones):

Imputación de valores faltantes: si hay días sin registro de horas de operación o personal, se aplicará imputación (media o mediana) para no perder datos importantes.

Escalado de variables numéricas: variables como horas de operación o cantidad de materia prima tienen escalas diferentes; normalizarlas permitirá que el modelo no dé más peso a las de mayor rango.

Codificación de variables categóricas: si existiera información categórica como "turno de trabajo" (mañana, tarde, noche), se codificaría en variables dummy para que el modelo pueda interpretarlas.

Creación de lags (rezagos): generar variables que reflejen productividad del día anterior o fallas previas de maquinaria, porque la productividad actual puede depender de tendencias recientes.

Justificación: cada transformación asegura calidad de datos, comparabilidad entre variables y captura de relaciones temporales relevantes para la predicción.
  
2. Señala un posible riesgo de data leakage (fuga de datos) en tu plan y explica cómo lo evitarías usando un pipeline de preprocesamiento.
   
RTA/ Respuesta 2 (Riesgo de data leakage):
Un posible riesgo de data leakage sería usar información del futuro, por ejemplo: incluir la productividad total de la semana para predecir un solo día. Esto daría ventaja artificial al modelo porque estaría “espiando” datos que en la vida real no tendría disponibles.

Cómo evitarlo con un pipeline:

Definir claramente las variables solo con información disponible hasta el momento de la predicción.

Aplicar imputación, escalado y creación de lags dentro del pipeline, asegurando que estas transformaciones se calculen únicamente sobre los datos de entrenamiento y luego se apliquen al test, evitando filtrar datos futuros.

**Parte 3: Interpretación y Métricas de Regresión Simple**

Para esta sección, elige un caso simple de regresión (puede ser el tuyo o uno hipotético, como predecir la demanda de un producto según su precio).

1. Define claramente las variables Y y X junto con sus unidades (ej. Y: número de unidades vendidas, X: precio en dólares).
   RTA/Respuesta 1:
Y (variable dependiente): Nivel de productividad diaria (unidades producidas por día).
X (variable independiente): Horas de operación de la maquinaria (horas/día).
   
2. Supón que entrenas un modelo y obtienes una pendiente de . Escribe una interpretación clara y concisa de este coeficiente en el contexto de tu problema.
   RTA/ Respuesta 2:
Si el modelo arroja una pendiente de 𝛽^1=−0.6, significa que:

Por cada hora adicional de operación de la maquinaria, la productividad disminuye en promedio 0.6 unidades.
Esto podría interpretarse como un efecto de fatiga o desgaste en los procesos, donde más horas no necesariamente implican mayor producción, sino pérdidas por ineficiencia o errores.
   
3. ¿Qué métrica de evaluación usarías (MAE, RMSE, o MAPE) y por qué es la más adecuada para tu caso?
   RTA/ Respuesta 3:
Usaría la métrica RMSE (Root Mean Squared Error) porque penaliza más los errores grandes, lo cual es importante en este caso: un error significativo en la predicción de unidades producidas podría afectar seriamente la planeación de inventarios y entregas.
   
4. Menciona un supuesto del modelo de regresión lineal que validarías (ej. linealidad, homocedasticidad) y explica cómo lo harías (usando un gráfico o una prueba
   RTA/Respuesta 4:
Un supuesto que validaría es la linealidad entre horas de operación (X) y productividad (Y).

Para comprobarlo, graficaría un diagrama de dispersión de productividad vs. horas de operación, con la recta de regresión superpuesta.

Si se observa una tendencia curva o no lineal, sabría que la relación no es estrictamente lineal y el modelo simple no sería adecuado.

**Parte 4: Regresión Múltiple y Colinealidad**

Volviendo a tu caso de la Parte 1 (con múltiples variables).

1. Escribe el vector de variables X y la respuesta Y.
   RTA/Respuesta 1:

Vector de variables 𝑋⃗:

A. Horas de operación de la maquinaria (horas/día).
B. Cantidad de materia prima disponible (kg/día).
C. Número de trabajadores en la línea de producción (personas).
D. Tiempo promedio de inactividad por fallas (minutos/día).
E. Nivel de calidad de la materia prima (índice de defectos).

Respuesta Y: Nivel de productividad diaria (unidades producidas/día).

2. Explica cómo interpretarías el coeficiente de una de tus variables clave (incluyendo unidades y el sentido de la relación: positiva o negativa).
   RTA/Respuesta 2:
Si, por ejemplo, el coeficiente de la variable cantidad de materia prima disponible (kg/día) es 𝛽=2.5:

Significa que, manteniendo las demás variables constantes, por cada kilogramo adicional de materia prima, la planta produce en promedio 2.5 unidades más por día.
La relación es positiva, lo cual tiene sentido ya que más insumo disponible facilita mayor producción.

3. Si sospecharas que existe colinealidad entre tus variables, menciona dos acciones que podrías tomar para mitigarla.
   RTA/   Respuesta 3:
Si sospechara colinealidad entre variables (ejemplo: horas de operación y tiempo de inactividad), tomaría estas acciones:

A. Eliminar o combinar variables altamente correlacionadas (ej. en lugar de ambas, usar solo “tiempo efectivo de operación”).

B. Aplicar técnicas de regularización como Ridge o Lasso Regression, que reducen el impacto de la multicolinealidad al penalizar coeficientes excesivamente grandes.


**Parte 5: Interacciones y Multicolinealidad (VIF)**

1. Plantea un caso con una variable Y y entre 4 y 6 variables X. ¿Qué término de interacción entre dos variables podrías añadir al modelo y por qué crees que sería útil?
   RTA/ Respuesta 1 (Interacción útil):
Propongo añadir el término de interacción
(Numero de trabajadores)×(Horas de operacion)
Por qué sería útil:

Captura el efecto conjunto: por ejemplo, más horas de operación sólo aumentan producción si hay suficiente personal; con pocas personas, aumentar horas puede llevar a fatiga y menor rendimiento.
Permite que el modelo represente que el impacto de las horas depende del tamaño del equipo (y viceversa), es decir, no asume que ambos efectos son puramente aditivos.
(Alternativa útil: interacción entre Nivel de calidad de la materia prima × Tiempo de inactividad — porque mala calidad puede aumentar la sensibilidad del proceso a las paradas.)
   
2. Si al calcular el Factor de Inflación de la Varianza (VIF) para una variable, obtienes un valor alto (ej. > 10), menciona dos acciones que podrías tomar para solucionarlo.
   RTA/ Respuesta 2 (Si VIF > 10 — dos acciones para solucionarlo):

Eliminar o combinar variables correlacionadas / crear variables compuestas

A. Si dos variables miden casi lo mismo (ej. Horas de operación y Tiempo efectivo de operación), elimina una o crea una variable compuesta (tiempo efectivo = horas totales - inactividad) para reducir redundancia.

B. Ventaja: simple, interpretable y reduce la multicolinealidad directamente.

Usar regularización o reducción de dimensionalidad

A. Ridge Regression (penalización L2) o Lasso (L1) para estabilizar los coeficientes en presencia de colinealidad.

B. O aplicar PCA sobre el subgrupo de variables correlacionadas y usar los componentes principales en el modelo.

C. Ventaja: mantiene la información predictiva mientras reduce la varianza de los coeficientes.

**Parte 6: Variables Categóricas e Interacciones**

1. Define una variable categórica para tu caso (puedes inventarla si no la tenías). Elige una de sus categorías como el nivel base o de referencia y justifica tu elección.
   RTA/ Respuesta 1 (Variable categórica):
Defino la variable categórica Turno de trabajo, con tres categorías:

Mañana
Tarde
Noche

Elijo como nivel base o de referencia el Turno de mañana, ya que suele ser el más estable en términos de productividad (menos fatiga acumulada y mejor disponibilidad de personal). Esto permite comparar el efecto de los turnos tarde y noche respecto a la mañana.
   
2. Crea una interacción entre una variable numérica y la variable categórica que definiste. Explica cómo se interpretaría el coeficiente de esta interacción.
Respuesta (escribe aquí):
   RTA/ Respuesta 2 (Interacción):
Creo la interacción entre la variable numérica Horas de operación y la variable categórica Turno de trabajo.

Interpretación del coeficiente:

Si el coeficiente de la interacción (Horas de operacion×Turno noche) es negativo, significa que las horas adicionales de operación durante el turno de noche tienen un impacto menor (o incluso negativo) en la productividad, comparado con el turno de la mañana.

En cambio, si fuera positivo en el turno tarde, interpretaría que aumentar horas en ese turno tiene un efecto adicional positivo en la producción respecto al turno de mañana.

**Parte 7: Conceptos Clave de Clasificación**

Aunque el taller se centra en regresión, estos conceptos son fundamentales en Machine Learning.

1. Explica qué es la curva ROC y para qué se utiliza en un problema de clasificación.
   RTA/Respuesta 1 (Curva ROC):
La curva ROC (Receiver Operating Characteristic) es una gráfica que muestra la capacidad de un modelo de clasificación para distinguir entre clases. Se construye con la tasa de verdaderos positivos (TPR) frente a la tasa de falsos positivos (FPR) para diferentes umbrales de decisión.
Se utiliza para evaluar el desempeño de un modelo más allá de un único punto de corte y comparar modelos mediante el AUC (Área Bajo la Curva): cuanto más cerca de 1 esté el AUC, mejor es el modelo.
   
2. Define el concepto de accuracy (exactitud) y menciona una situación en la que podría ser una métrica engañosa.
   RTA/El accuracy (exactitud) es la proporción de predicciones correctas (positivas y negativas) sobre el total de casos.

Accuracy=TP+TN+FP+FN/TP+TN

 ​
Puede ser una métrica engañosa en problemas con clases desbalanceadas. Por ejemplo: si en un hospital solo el 1% de pacientes tiene una enfermedad, un modelo que siempre predice “no enfermo” tendrá 99% de accuracy, pero no sirve para identificar a los enfermos.
   
3. Describe qué es una matriz de confusión y cómo se interpretan sus componentes (Verdaderos Positivos, Falsos Positivos, Verdaderos Negativos, Falsos Negativos).
   RTA/ Una matriz de confusión es una tabla que resume el desempeño de un modelo de clasificación comparando las predicciones con los valores reales.

A. Verdaderos Positivos (TP): Casos positivos que el modelo clasificó correctamente como positivos.

B. Falsos Positivos (FP): Casos negativos que el modelo clasificó incorrectamente como positivos (error tipo I).

C. Verdaderos Negativos (TN): Casos negativos que el modelo clasificó correctamente como negativos.

D. Falsos Negativos (FN): Casos positivos que el modelo clasificó incorrectamente como negativos (error tipo II).

La interpretación depende del contexto: por ejemplo, en detección de fallas en maquinaria, un FN sería crítico porque significa no detectar una falla real.
   













Respuesta (escribe aquí):
