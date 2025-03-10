Este proyecto tiene el objetivo de predecir cuando un persona es un buen match para una determinada beca.

La idea general es crear un modelo de recomendacion utilizando regresion logistica donde se combinen informacion tanto de la beca como de la persona que quiere aplicar a esa beca, esto nos da la posibilidad de predecir que nuevas becas matchean con las personas que ya tengamos en nuestro sistema, como nuevas personas que quieren hacer determinada beca de nuestro sistema.
Como sabemos este tipo de clasificacion nos da un probabilidad, esta sera utilizada para descartar, previo control de un humano, aquellos pares beca-persona que no sean compatibles.

Como baseline se crearon 3 modelos distintos:
1. Logistic Regresion.
2. Xgboost.
3. Modelo realizado con Keras.


Dando como resultad que el mejor modelo baseline fue Xgboost. En base a esto se procedio a tunnear hiperparametros.
Despues de una ronda de tunning con RandomizedSearchCV y cross-validation, se decidio aplicar PCA a nuestros datos. Se busco el numero de componentes que expliquen el 95% de la varianza 
Se volvio a entrenar el modelo post aplicacion de PCA a nuestros datos. 

Las metricas utilizadas para evaluar el modelo fueron:
1. Accuracy
2. Recall y Precision
3. ROC curve y AUC
4. Matriz de confusion


Si bien el accuracy de nuestro modelo baseline es de un 75%, esta sesgado por la cantidad de true-positives.
Despues de aplicar PCA y tunear los hiperparametros el mejor accuracy obtenido es 73%.

Si bien tenemos un recall de 0.51. Entendemos que para este problema es mejor tener, en terminos de matriz de confusion, False-Positives que False-negatives. Debido a que los primeros seran revisados y descartados, mientras que los segundos no seran tenidos en cuenta por el revisor.



Modulos utilizados en este proyecto:

Para manejo y curacion:
- Pandas
- SqlAlchemy
- Plotly Express
- Missingno

Para analsis estadistico
- Scipy
- Statsmodels

Creacion y tuning del modelo:
- Sklearn
- Xgboost


Dificultades enfrentadas y como se resolvieron:
Problema:
1. La principal dificultad encontrada fue que nuestro dataset era uno desbalanceado, el 30% tenia la clase 0 y un 70% la clase 1.
2. La poca cantidad de datos utilizables, un total de 1261 filas.
3. Pocas filas contenian una correlacion aceptable con nuestro target.

Soluciones: 
1. Uno de los metodos utilizados para palear esta dificultad a la hora de entrenar el modelo, fue la utilizacion de los parametros "scale_pos_weight" y "max_delta_step" lo que nos ayuda a equilibrar la diferencia entre clases.
2. Se penso en atacar este problema desde el oversampling o undersampling.
3. Se utilizaron tecnicas de feature engineering, como escalado, PCA y columnas sinteticas.
