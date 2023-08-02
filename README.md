# Examen_Big_Data_Analisis_Clustering_Tweets
Trabajo_grupal_Kendry_Caravajal_y_Ana_Ortega
<div style="background-color: #f2f2f2; padding: 20px; position: relative;">
    <h2 style="margin-bottom: 10px;">Exámen final de Big Data: Análisis de Clustering en Tweets</h2>
    <img src="impelia_logo-cabecera_-02.png" alt="Logo Impelia" style="width: 100px; position: absolute; top: 10px; right: 10px;">
    <p style="position: absolute; bottom: -11px; right: 5px; font-style: italic; font-size: 12px;">by Kendry Caravajal y Ana Ortega</p>
</div>


### INFORME

**1) Se han utilizado las siguientes librerias:**

**Análisis y manipulación de datos tabulares**
- pandas
- numpy

**Visualización** 
- matplotlib.pyplot 
- seaborn 
- plotly
- wordcloud

**Tratamiento de caractes especiales**
- regex (re)

**Análisis de Lenguaje Natural**
- nltk
- stopwords
- WordNetLemmatizer
- SnowballStemmer
- WordNetLemmatizer
- Spacy

**Clustering**
- K-Means
- Agglomerative
- HdpModel
- NMF
- LatentDirichletAllocation
- LsiModel

**Evaluación de modelos (métricas)**
- silhouette_score
- homogeneity_score
- completeness_score
- f1_score
- homogeneity_completeness_v_measure

**2) Limpieza y preprocesado de los datos**

- Se ha trabajado con tweets de 5 países diferentes.
- El dataset corresponde a un conjunto aleatorio de datos
- Los registros que contiene cada dataset son: 
     - Costa Rica: 777, 
     - España: 1126, 
     - Perú: 966, 
     - México: 990, 
     - Uruguay: 943.
- Se ha utilizado la librería **Regex** para el tratado de caracteres especiales
- (@,# y url) han sido eliminados para este estudio.
- Los caracteres especiales como signos de puntuación y acentos han sido descartados.
- Los tweets han sido convertidos a minúsculas.

Es decir, se han conservado solo las palabras, excluyendo todo lo anteriormente nombrado y los números.
 
**Aporte**: Aunque se ha realizado un analisis exhaustivo para eliminar aquellos caracteres que entorpecía dicho análisis, se necesita más tiempo para realizar una limpieza profunda y así eliminar el ruido de manera efectiva.

Luego se ha realizado la tokenización.

El resultados de la eliminación de **Stopswords** no fue el esperado, debido al ruido anteriormente comentado.

La librería utilizada, no tuvo el desempeño esperado ya que ruido en los textos es de gran magnitud.

Se ha realizado **Lematización y Stemización**, debido a las características de los datos, a los objetivos y a los resultados obtenidos se ha optado por utilizar lematización, ya que la lematización es un proceso más avanzado que busca reducir las palabras a su lema o forma base, que es el término canónico o diccionario de una palabra.

- Además para probar librerías novedosas se ha utilizado Spacy que es una poderosa librería de procesamiento de lenguaje natural  que proporciona herramientas y funciones para realizar tareas de procesamiento de texto, como tokenización, lematización, etiquetado gramatical, reconocimiento de entidades, análisis de dependencias y extracción de frases clave. SpaCy se destaca por su rapidez y precisión. También se integra fácilmente con otras bibliotecas populares de Python, lo que lo hace versátil en aplicaciones de análisis de datos y aprendizaje automático. 


**3) Clustering**
**Kmeans:** 
- Gracias a los resultados obtenidos con el Elbow method, el número de clusters óptimo es entre 4 y 6.

- En la gráfica se puede observar que en los clusters no se delimita bien su agrupación, por lo que concluimos que su interpretación se dificulta.

**Agglomerative:**
- Una diferencia notoria entre ambos modelos es que en agglomerative se observa una superposición muy marcada en los clusters.

**HDP, NMF, LDA, LSI:**
- A pesar de que hay diferencias notorias en cada uno de los modelos (detalladas más abajo), los resultados obtenidos no permiten sacar conclusiones fácilmente interpretables.
- Hay modelos que son muy generales o sea, han entregado, por ejemplo, 5 tópicos a partir del tratado de toda la base de datos y con la implementación de otros modelos se han obtenido resultados muy específicos ya que han entregado tantos tópicos como tweets, por lo que hacer una interpretación de los resultados es muy dificultoso. 
- Se cree que la dificultad para realizar un correcta interpretación se debe al ruido en los datos, la falta de información acerca de los datos y/o la elección incorrecta de los modelos.

**4) Métricas**
El **índice de silueta (silhouette_score)** es una medida que evalúa la calidad de la agrupación o clustering de tus datos. Proporciona una medida de cuán bien están separados los datos dentro de un clúster en comparación con otros clústeres. El valor del índice de silueta oscila entre -1 y 1, donde:

1. Un valor cercano a 1 indica que las muestras están bien agrupadas y están separadas de otros clústeres.
2. Un valor cercano a 0 indica que las muestras están cerca del límite de decisión entre dos clústeres.
3. Un valor cercano a -1 indica que las muestras están mal asignadas a los clústeres y que podrían estar mejor en un clúster diferente.
 - Con K-Means se obtuvo un silhouette_score de 0,036 y con Agglomerative -0.18. Se puede observar que ambos modelos arrojan resultados que muestran que las muestras están mal asignadas. Entre ambos modelos, el de K-Means tiene un valor más cercano a 0 (cero), por lo que se podría decir que tuvo mejor desempeño. 
 
**Coherence** 
La coherencia es una medida que se utiliza para evaluar la calidad de los modelos de temas generados por algoritmos de modelado de temas, tiene como objetivo cuantificar la interpretabilidad y consistencia de los temas generados.
Un valor de coherencia más alto indica que los temas son más interpretables y coherentes.
Se utiliza para comparar diferentes modelos de temas generados con diferentes configuraciones o parámetros, y para seleccionar el modelo que produce los temas más coherentes. También se puede utilizar para ajustar los parámetros del modelo y mejorar la calidad de los temas generados.

- Los resultados de **coherence** obtenidos por cada modelo fueron: 
1. HDP = 0.74
2. NMF = inf
3. LDA = 0.25
4. LSI = 0.28
Podemos observar que el modelo HDP es que el mejor desempeño tiene. 


**5) Clasificación de sentimientos**

- Debido a que en el dataset original ha sido proporcionada una columna con las etiquetas (negativo, positivo, neutro) de los sentimientos de los tweets, se ha realizado una nueva clasificación utilizando la técnica Naive Bayes, para contrastar los resultados, y confirmar si las etiquetas concidían. 
- Se ha observado que las diferencias entre las etiquetas dadas y las obtenidas no variaron lo suficiente como para considerarlo significativo. 

**6) Determinación del sentimiento mayoritario**
A partir del análisis realizado a los tweets, se ha observado que la etiqueta que mayor porcentaje tiene es la negativa. 
Los porcentajes obtenidos fueron: 
1. Negativos: 43%
2. Positivos: 29%
3. Neutros: 27%

 - Además se ha realizado un análisis de sentimientos de los tweets segregados por países, en el cual se ha observado que el país que tenía mayor cantidad de tweets etiquetados negativamente fue México y el que menos tenía fue Perú. 
 - Los 5 países tienen tweets clasificados positivamente en porcentaje similiar, y aquellos que tienen tweets con etiqueta neutra el único que sobresale es Perú. 
 - Un detalle observado es que las bases de datos de cada país tienen diferentes dimensiones lo que influye en el análisis y los resultados. 

Porcentaje de etiquetas por país
<img src="newplot (7).png"
alt="Markdown Monster icon"
style="float: left; margin-right: 10px;" />

**7) La descripción de cada modelo está desarrollado en el punto 8.** 
- Luego de haber realizado clustering con K-means se obtuvieron como resultado 4 clusters (número elegido a partir del elbow method), convinándolos con el análisis de sentimientos se ha podido llegar a la conclusión de que la polaridad influyente en los clusters es: 
1. cluster 0: negativo
2. cluster 1: neutro
3. cluster 2: negativo
4. cluster 3: positivo

-Luego de haber realizado un análisis de la frecuencia de las palabras, se pudo observar que dentro de los clusters hay términos que tienen mayor frecuencia que otros, o sea que son mayormente utilizados, algunos ejemplos pueden ser: verbos y conectores mal escritos que no fueron detectados. 

**8) Conclusiones:** 
- Debido a que los registros son un conjunto aleatorio de datos y que el objetivo no fue pautado previamente, es muy dificultoso interpretar los resultados obtenidos.
- Se requiere de mayor tiempo para hacer limpieza y tratamiento de los datos, correctamente. 
- Para que el rendimiento de algunos modelos elegidos sea el adecuado, se requieren grandes cantidades de datos, por lo tanto los resultados obtenidos se vieron influenciados por la escasez de los mismos. 
- Se ha observado que hay modelos no supervisados que entregan la cantidad de tópicos que creen optimos sin pasarle previamente un número determinado, haciéndolos muy específicos y otros que necesitan que se estipule previamente el número de temas, haciéndolos muy generales, lo que dificulta la interpretración los resultados, ya que algunos son muy generalistas y otros muy específicos.
