Se generaron distintos gráficos para el análisis y estudio de los datos. 

---hist_medhouseval---
El histograma de los valores medios de las casas refleja asimetría cargada hacia los valores relativamente bajos (La mayor concentración se presenta entre 70,000 y 200,000 USD, el intervalo con mayor frecuencia está en 1.5-1.7). Conforme aunmenta el valor de las casas disminuye la frecuencia. Además se refleja una cola hacia los valores más altos. 
El histograma no aparenta algún tipo de distribución normal.
Se observa una acumulación importante al final del histograma (en 5.0) lo cual puede estar relacionado a que el análisis tenía una cota en 5. Es decir, todos los valores mayores a 5 fueron acumulados ahí y aparentemente representan una gran parte de los datos.

---Boxplot_medhouseval---
La mediana del boxplot se encuentra aproximadamente en 1.8. El 50% de las observaciones se encuentran entre 1.2 y 2.6. El gráfico de bigotes refleja también un cúmulo de valores atípicos fuera de los bigotes, dichos valores reflejan los datos acumulados en 5 observados en el histograma. Además de una asimetría en los bigotes (el izquierdo es más corto).


---hist_variables---
El histograma de ingreso medio refleja ingresos bajos en la mayoria de los datos, en la antigüedad de las viviendas no parece seguir algún tipo de forma normal, existe heretogeneidad. Para el número promedio de habitantes existen zonas con promedios de habitaciones extraordinariamente elevados respecto al resto, de igual manera hay datos excepcionalmente elevados en el número promedio de dormitorios. La ocupación promedio también presenta valores elevados. Para la latitud y longitud ocuparemos otro tipo de visualiazción.

---boxplot_variables---
Respecto a los diagramas de caja, se identificaron numerosos posibles valores atípicos en MedInc, AveRooms, AveBedrms, Population y AveOccup. Estas observaciones requieren una revisión posterior para determinar si representan valores legítimos o situaciones particulares del conjunto de datos.

En general, el análisis muestra que varias variables presentan distribuciones asimétricas y posibles valores extremos, características que deberán considerarse durante la preparación de los datos y la construcción de los modelos de regresión.



------------------------------------

Las variables AveRooms, AveBedrms y AveOccup presentan valores extremos muy alejados de la concentración principal. Para hacer un análisis más profundo calculamos

Variable: AveRooms
Máximo: 141.91
Límite superior: 8.47
Cantidad de posibles outliers: 466
Porcentaje: 2.26%

Variable: AveBedrms
Máximo: 34.07
Límite superior: 1.24
Cantidad de posibles outliers: 1236
Porcentaje: 5.99%

Variable: AveOccup
Máximo: 1243.33
Límite superior: 4.56
Cantidad de posibles outliers: 704
Porcentaje: 3.41%

---¿Cuál de las tres variables presenta mayor proporción de posibles valores atípicos y cuál presenta los valores extremos más alejados de su distribución principal?---

El promedio de dormitorios es el que presenta un mayor porcentaje de datos atípicos, mientras que la ocupación promedio es la que presenta mayor diferencia entre el límite superior y el máximo.

Lo cual quiere decir que pese a que tienen valores atípicos muy alejados de la media, estos representan porcentajes muy bajos respecto a la cantidad total de datos. Por lo cual, por el momento no descartaremos estos valores atípicos.

Los valores atípicos de averooms y avebedrms tienden a ser valores poco lógicos para ocupaciones de casa y habitaciones, esto puede estar relacionado a la estructura de los grupos censales, no deberían considerarse como errores.


### Investigación de valores extremos en AveRooms y AveBedrms

Al investigar las observaciones con mayores valores de `AveRooms`, encontramos que algunas presentan poblaciones considerablemente pequeñas.

Por ejemplo, las dos observaciones más extremas tienen poblaciones de 30 y 36 habitantes, respectivamente.

Al utilizar la relación entre población y ocupación promedio, estimamos que estos grupos censales tienen aproximadamente 11 y 15 hogares.

Esto sugiere que los promedios de habitaciones y dormitorios pueden verse considerablemente afectados por las características particulares de unas pocas viviendas.

Por lo tanto, los valores extremos identificados no deben considerarse automáticamente errores de captura, sino que requieren analizarse considerando la estructura de los grupos censales.


La matriz de correlaciones permitió identificar relaciones importantes entre las variables del conjunto de datos. Se observó una correlación positiva fuerte entre `MedInc` y `MedHouseVal`, lo que sugiere que las zonas con mayores ingresos medianos tienden a presentar mayores valores medianos de vivienda.

También se identificó una relación positiva entre `AveRooms` y `AveBedrms`, así como una relación negativa entre `Latitude` y `Longitude`, posiblemente asociada con la distribución geográfica de las zonas censales.

Finalmente, la correlación elevada entre `Population` y `EstimatedHouseholds` es esperable, ya que esta última variable fue construida a partir de `Population` y `AveOccup`. Por ello, se considera una variable auxiliar y no se incorporará automáticamente al modelo.


La gráfica de dispersión entre `medinc` y `medhouseval` refleja la relación positiva entre las variables, sin embargo la dispersión nos puede indicar que que `medinc` no explica toda la variabilidad del objetivo. También se aprecia acumulación en el límite superior debido a la cota en 5. Esto es importante considerarlo al interpretar los datos de los modelos de regresión.


Los diagramas de dispersión de `MedHouseVal` con `AveRooms` y `AveBedrms` presentan una concentración considerable de observaciones, formando patrones verticales que dificultan la identificación visual de una tendencia clara. Aunque estas variables presentan correlación con la variable objetivo, su relación no resulta tan evidente gráficamente como la observada con `MedInc`.


En conclusión, se utilizará principalmente (si no es que únicamente), medinc como variable explicativa para la regresión linela simple.