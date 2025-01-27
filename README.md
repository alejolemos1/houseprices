# House prices analysis project
## Objetivos principales
La idea principal de este proyecto es analizar las distintas variables del dataset "House prices" que muestra el precio de venta de distintas casas en la ciudad de Ames, Iowa. El mismo contiene +80 variables con cada ejemplo de casa, esto nos servirá para entender **cuáles son los factores que más afectan al precio de las casas en Ames**.

## Proyecto
Lo primero a realizar fue una exploración y limpieza de los datos. Nos encontramos demasiados valores nulos dentro de las distintas columnas. Para resolver esto se han agrupado las columnas numéricas, por un lado, y las categóricas, por otro, luego se han rellenado los valores numéricos con la media de la columna y para los valores categóricos simplemente los he rellenado con 'Missing Value', para no tener problemas a la hora de analizar. Esto puede verse en [notebook.ipynb](notebooks/notebook.ipynb) (ordenes de ejecución 38, 39 y 40)

Lo primero que quise observar fue la distribución de los precios de las casas.
Vemos que entre 100.000 y 200.000 aproximadamente es el precio de la mayoría de las casas.
![Distribución del precio de las casas en Ames](/images/price_dist.png "Distribución del precio de las casas en Ames")

Luego, mediante un gráfico de "mapa de calor", he ordenado las distintas variables numéricas en función de su correlación lineal con el precio.
![Mapa de calor](/images/numeric_vars_heatmap.png "Correlación lineal de las variables numéricas con el precio")

### Resultado del mapa de calor
El anterior mapa de calor nos muestra cuáles son las variables numéricas que tienen mayor correlación lineal con el precio de las casas, es decir, que a mayor de esta variable, mayor es el precio de la casa. La variable más correlacionada es la calidad de los materiales y el acabado final, con uno o.79 de correlación, es decir, que por cada 0.79% que cambie esta variable, hacia arriba o hacia abajo, el precio aumentaría o disminuiría en un 1%. Con base en esto decidimos las columnas numéricas a analizar (de las cuales ya observamos su correlación con el precio, es decir, cuánto influyen estas en el mismo) y algunas categóricas que creemos pueden influir en el precio.

### Columnas a analizar:
* Numéricas:
    * OverallQual: Califica el material general y el acabado de la casa
    * GrLivArea: Superficie habitable sobre el nivel del suelo (pies cuadrados)
    * GarageCars: Tamaño del garaje medido en cantidad de autos
    * TotalBsmtSF: Total de pies cuadrados del área del sótano
    * 1stFlrSF: Pies cuadrados del primer piso
    * FullBath: Cantidad de baños por encima del nivel del suelo (no sótano)
    * TotRmsAbvGrd: Total de habitaciones sobre el nivel del suelo (no incluye baños)
    * YearBuilt: Fecha de construcción original
* Categóricas
    * MSZoning: Clasificación general de zonificación de la venta (comercial, casas flotantes y residencial de baja, media y alta densidad poblacional)
    * LotConfig: Configuración del lote (Lote interior, Callejón sin salida, Esquina, Frente en 2 lados de la propiedad y Frente en 3 lados de la propiedad)
    * Neighborhood: Ubicación física dentro de los límites de la ciudad de Ames. (Vecindario)
    * HouseStyle: Estilo de vivienda (1, 2, 1.5, 2.5 pisos, finalizados y no finalizados, vestíbulo en)

## Análisis de las columnas categóricas seleccionadas
### Neighborhood
![Precio medio por vecindario](/images/price_by_nhood.png "Precio medio por vecindario")<br>
En este gráfico vemos el precio medio por vecindario, puede ser un gran dato de partida para analizar otras variables según el precio que se esté dispuesto a pagar.

### MSZoning
![boxplot precio de las casas según su tipo de zona](/images/price_by_zoning_boxplot.png "Precio en diagrama de cajas según el tipo de zona")<br>
En este gráfico se observan 5 categorías de la zona: Residencial de baja, media y alta densidad, zonas comerciales y pueblos flotantes. Como se puede ver, en las zonas de residencias con baja densidad (RL), los precios elevados atípicos respecto de la mediana son demasiados, esto puede deberse al estilo de casa (HouseStyle) variable analizada abajo.

### HouseStyle
![boxplot precio de las casas según su estilo](/images/price_by_style_boxplot.png "Precio en diagrama de cajas según el estilo de las casas")<br>
Este es el comportamiento del precio según el estilo de casa. Como vemos, hay ciertos estilos que tienen demasiados valores atipicos respecto de la mediana.

![Estilo de casa por tipo de zona](/images/style_by_zoning_barplot.png "Estilo de casa según el tipo de zona")<br>
En este gráfico hemos agrupado las casas por su tipo de zona, comercial, residencial baja densidad, etc. pero también lo hemos hecho por el *porcentaje* que ocupa cada estilo de casa dentro de cada tipo de zona, que van desde simples con uno o dos pisos hasta con pisos y medio y casas con pisos divididos. Lo que podemos observar en el gráfico es la razón de por qué las casas en zonas **residenciales** de **baja** y **media** densidad tienen tantos precios atípicos muy altos en relación a la mediana, lo que ocurre es que estas zonas están mayormente compuestas por casas de 1, 2 y 1.5 pisos (ese 0.5 piso puede ser un ático o espacio reducido), estilos de casa que tienden a un mayor precio (como se observa en el gráfico anterior a este).

### LotConfig
![Precio medio de las configuraciones de lote segun la zona](/images/price_by_lotconfig_by_zoning_barplot.png "Precio medio de las configuraciones de lote segun la zona")<br>
Aquí podemos ver como varían los precios de las distintas configuraciones del lote según la zona, por ejemplo si se estuviera considerando comprar un lote esquina, y lo único relevante fuera el precio, la mejor opción es una zona residencial de alta densidad, unque es válido analizar otras variables para confirmar que es la mejor opción.
<br><br>

Consulta el codigo completo en [notebook.ipynb](./notebooks/notebook.ipynb)

Requerimientos para poder ejecutar el codigo:
* python 3.8 o superior
* librerias:
    pandas: Para manejar y procesar el dataset.
    numpy: Para cálculos matemáticos y funciones auxiliares.
    matplotlib: Para la creación de gráficos.
    seaborn: Para visualización avanzada y gráficos de correlación.
* jupyter notebook

## Proximos pasos
Este proyecto se encuentra en una versión preliminar. Actualmente, incluye análisis exploratorio de datos y visualizaciones básicas que ayudan a comprender las variables principales que influyen en los precios de las casas en el dataset de Housing Prices. A continuacion se enumeran algunos de los proximos pasos para seguir desarrollando el proyecto.

1. Modelado de Datos: Implementar modelos de aprendizaje supervisado, como regresión lineal, para predecir los precios de las viviendas.
2. Optimización: Evaluar la importancia de las características mediante técnicas de selección de variables.
3. Documentación: Completar y pulir la documentación del proyecto, explicando detalladamente las decisiones tomadas en cada paso.
4. Mejorar Visualizaciones: Refinar los gráficos para que sean más claros y atractivos.
5. Pruebas: Implementar tests para asegurar la reproducibilidad del análisis.

