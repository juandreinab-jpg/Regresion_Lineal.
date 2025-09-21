# Regresion_Lineal.
Parte 1: Definición del Problema
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

Parte 3: Interpretación y Métricas de Regresión Simple

Para esta sección, elige un caso simple de regresión (puede ser el tuyo o uno hipotético, como predecir la demanda de un producto según su precio).

1. Define claramente las variables Y y X junto con sus unidades (ej. Y: número de unidades vendidas, X: precio en dólares).
2. Supón que entrenas un modelo y obtienes una pendiente de . Escribe una interpretación clara y concisa de este coeficiente en el contexto de tu problema.
3. ¿Qué métrica de evaluación usarías (MAE, RMSE, o MAPE) y por qué es la más adecuada para tu caso?
4. Menciona un supuesto del modelo de regresión lineal que validarías (ej. linealidad, homocedasticidad) y explica cómo lo harías (usando un gráfico o una prueba

Parte 4: Regresión Múltiple y Colinealidad

Volviendo a tu caso de la Parte 1 (con múltiples variables).

1. Escribe el vector de variables X y la respuesta Y.
2. Explica cómo interpretarías el coeficiente de una de tus variables clave (incluyendo unidades y el sentido de la relación: positiva o negativa).
3. Si sospecharas que existe colinealidad entre tus variables, menciona dos acciones que podrías tomar para mitigarla.
   
Respuesta (escribe aquí):

Parte 5: Interacciones y Multicolinealidad (VIF)

1. Plantea un caso con una variable Y y entre 4 y 6 variables X. ¿Qué término de interacción entre dos variables podrías añadir al modelo y por qué crees que sería útil?
2. Si al calcular el Factor de Inflación de la Varianza (VIF) para una variable, obtienes un valor alto (ej. > 10), menciona dos acciones que podrías tomar para solucionarlo.
3. 
Respuesta (escribe aquí):

Parte 6: Variables Categóricas e Interacciones

1. Define una variable categórica para tu caso (puedes inventarla si no la tenías). Elige una de sus categorías como el nivel base o de referencia y justifica tu elección.
2. Crea una interacción entre una variable numérica y la variable categórica que definiste. Explica cómo se interpretaría el coeficiente de esta interacción.
Respuesta (escribe aquí):

Parte 7: Conceptos Clave de Clasificación

Aunque el taller se centra en regresión, estos conceptos son fundamentales en Machine Learning.

1. Explica qué es la curva ROC y para qué se utiliza en un problema de clasificación.
2. Define el concepto de accuracy (exactitud) y menciona una situación en la que podría ser una métrica engañosa.
3. Describe qué es una matriz de confusión y cómo se interpretan sus componentes (Verdaderos Positivos, Falsos Positivos, Verdaderos Negativos, Falsos Negativos).
   
Respuesta (escribe aquí):












estadística).
Respuesta (escribe aquí):
