# Aircraft-Accidents-Project
# Accidentes aéreos y víctimas mortales desde 1908 a 2023

https://github.com/19972024/Aircraft-Accidents-Project/assets/156945446/f67a6da3-3384-481c-b049-2406f43d0da2

Requisitos:

#Para el tercer proyecto, debe elegir entre estas dos opciones:

#Recopilar datos a través de APIs o Web Scrapping
#Descargar datos de una fuente conocida (Kaggle, fuentes de datos abiertas, etc) y realizar un Análisis de Series Temporales utilizando prophet.

#Para ambas opciones, debes llevar a cabo:
#Un análisis exploratorio de datos
#Ingeniería de características (transformación, selección, generación)
#Preprocesamiento para la regresión lineal (incluyendo elección de características objetivo, análisis de multicolinealidad, codificación, escalado...)
#Modelización de la regresión lineal y análisis de resultados
#(!) Recuerde incluir detalles sobre las elecciones y modificaciones realizadas en el proceso.


#Acerca del conjunto de datos

![download (1)](https://github.com/19972024/Aircraft-Accidents-Project/assets/156945446/8ce4e0e1-42ad-41ce-a7a0-cd40d2deee94)


#Descripción:

#Explore un completo conjunto de datos que detalla la historia de los accidentes y muertes de aviones y helicopteros en todo el mundo desde 1908 hasta 2023. Este conjunto de datos contiene información muy valiosa para investigadores, entusiastas de la aviación y expertos en seguridad interesados en comprender la dinámica, las tendencias y los patrones de los incidentes de aviación a lo largo de más de un siglo.

#Contenido:

#Fecha y hora del incidente
#Ubicación (país, ciudad )
#Aerolínea y número de vuelo
#Tipo de aeronave y matrícula
#Resumen del incidente
#Número de pasajeros y tripulación a bordo
#Víctimas mortales entre pasajeros, tripulación y personal de tierra
#Causa(s) probable(s) del accidente


Primera Fase:

Empezamos nuestro trabajo realizando las siguientes tareas:

# Exploración inicial de los datos

#tipos de datos

#Nulos (comprobar, no trabajar con ellos todavía)

#columnas

![Captura de pantalla 2024-05-08 142604](https://github.com/19972024/Aircraft-Accidents-Project/assets/156945446/fd68c3e7-cf62-4ed9-a92d-56013a0eb6f8)



# Analisis de los distintos campos categóricos. 

#Definir tratamientos a realizar:

#Corrección de categorías: value_counts? gráficas?

#Hay algún campo que se pueda utilizar para feature extraction?

#Hay algún campo que deba eliminarse por cantidad de nulos? Se podría hacer algo para evitarlo?

#Hay algún campo que deba eliminarse ya que no aporta información?

#Una vez corregidas las categorías -> chequear test chi-cuadrado para eliminar variables relacionadas

A traves de una funcion realizamos un value counts a todas nuestras variables categoricas:

![Captura de pantalla 2024-05-08 142750](https://github.com/19972024/Aircraft-Accidents-Project/assets/156945446/b19703ec-543b-4fc6-b58d-ee466ae70f32)

#Realizamos un value_counts de todas las columans que aparecen como categoricas para dar una primera mirada.

#Separaremos la columna date en año, mes, dia para buscar patrones, eliminaremos la columna time por su gran cantidad de nulos, ya que no encontre una manera correcta de poder rellenar esos datos.

#En la columna location, buscaremos eliminar espacios y signos si los hay a traves de algun metodo regex o lambda, luego analizaremos agruparlos por ciudades y paises. (Ver que hacemos con esos 4 nulos)

#En la columna Operador, buscaremos eliminar espacios y signos a traves de algun metodo regex o lambda. (Ver que hacemos con esos 10 nulos).
      
#La columna flight la eliminaremos por su gran cantidad de nulos.

#La columna route nos puede aportar algun tipo de informacion podemos elegir algunas categorias y agruparlas depende de que cantidad de informacion nos aporte sino la eliminaremos.

#La columna ac_type nos ayudara a comprender ciertos aspectos de nuestro df ya que aqui tenemos los modelos de aviones involucrados en estos accidentes, hay que solo analizar que hacer con los 70 nulos que tenemos

#De las columnas registration y cn_ln que eliminaremos seguramente por ser poco relevantes para nuestro analisis.

#Por ultimo la columna summary seguramente sera eliminada ya que para el modelo que luego tenemos que hacer no nos servira, si ayudara al principio a limpiar nuestro df ya que tiene una gran cantidad de informacion que puede ayudar y/o rellenar las demas columnas del df, ademas de arrojar gran informacion para entender patrones o buscar curiosidades de los diferentes accidentes.

![Captura de pantalla 2024-05-08 143210](https://github.com/19972024/Aircraft-Accidents-Project/assets/156945446/8cd09e78-2158-46ee-809a-9fb45ccd6316)

En mientras ya habiamos eliminado algunas columnas y rellenados los 4 valores nulos de la columna location con el valor unknown

![Captura de pantalla 2024-05-08 143327](https://github.com/19972024/Aircraft-Accidents-Project/assets/156945446/520a3494-ff7d-4ade-ba6f-bc53e1f894ee)

Luego empezamos a trabajar con la columna location para poder dividirla en dos nuevas columnas city y country para esto aplicamos diferentes metodos como los de a continuacion:

![1](https://github.com/19972024/Aircraft-Accidents-Project/assets/156945446/10893779-16e2-4cfc-810c-d207ed15350e)


![2](https://github.com/19972024/Aircraft-Accidents-Project/assets/156945446/535b0dc6-5419-489e-92ef-5b71264edd11)

Eliminamos tambien diferentes columnas y rellenamos los valores nulos de la columna operator, ac_type y summary con valores unknown.


Para finalizar con las variables categoricas realizamos varias pruebas chi cuadrado, llegando a la conlucion de que al tener todas un valor menor de 0.05 osea nn p-value de 0.0 en un análisis estadístico generalmente indica que la probabilidad de observar los datos (o datos más extremos) bajo la hipótesis nula es extremadamente baja, prácticamente nula. Esto suele interpretarse como evidencia significativa en contra de la hipótesis nula, lo que sugiere que hay una asociación significativa entre las variables en estudio.

Sin embargo, es importante tener en cuenta que un p-value de 0.0 no significa necesariamente que el resultado sea perfecto o que no haya errores en el análisis. A veces, un p-value muy bajo puede ser el resultado de una gran cantidad de datos o de otros factores que afectan la precisión del cálculo.

![3](https://github.com/19972024/Aircraft-Accidents-Project/assets/156945446/b30cdfc2-d9f9-4c98-9283-5681765d53e1)

Una vez finalizado esto comenzamos con analizar nuestras variables numericas:

# Numerical Data - Exploration

#Para las distintas variables numéricas

#Explorar nulls

#Explorar outliers

#Hay alguna variable a la que haya que aplicarle transformaciones (log, raiz cuadrada)?

#Explorar correlaciones entre variables numéricas

A traves de una funcion realizamos un value counts a todas nuestras variables numericas:

![4](https://github.com/19972024/Aircraft-Accidents-Project/assets/156945446/f0d8adb9-d734-47e7-abca-9f0dc831c5a7)

#Empezamos eliminando la columna ground y summary.
#Luego creamos una nueva columna llamada fatality ratio para calcular el porcentaje de muertes de los diferentes accidentes y asi poder estudiar una nueva variable.

![5](https://github.com/19972024/Aircraft-Accidents-Project/assets/156945446/c964373f-7a65-4c83-b647-53dbc76a4e24)

Hacemos una mirada general:



https://github.com/19972024/Aircraft-Accidents-Project/assets/156945446/ccc925f8-e08e-4b3c-88ad-7b7098cf60d8

![7](https://github.com/19972024/Aircraft-Accidents-Project/assets/156945446/8a3b85c8-5211-4a9c-8757-84300506e5dd)

![8](https://github.com/19972024/Aircraft-Accidents-Project/assets/156945446/a4c271ab-168f-4cb5-9b30-289a706c264f)

![9](https://github.com/19972024/Aircraft-Accidents-Project/assets/156945446/ab009cbf-74c1-4076-bfb8-44ca3630db71

#Luego de una mirada general podemos decir que las columnas year, month y day quedaron bastante bien, con ellas desarollaremos diferentes cuestiones y en cuanto a las columnas que abarcan aboard y fatalities casi todas son una l, estaria bien aplicar una logaritimica?

#En la columna aboard tenemos pocos nulos que podemos rellenar con algun metodo

#En la columna aboard_passangers nos pasa algo muy parecido a la columna aboard.

#En la columna aboard_crew lo mismo de arriba
 
#Con respecto a estas columnas mas de lo mismo ver como podemos tratar esos nulos y outliers ya que toda informacion es importante, podria ser una buena idea realizar una matriz de correlacion para ver como ya puede a ver algun tipo de conexion entre estas variables?

#"fatalities_passangers", "fatalities", "fatalities_crew".

#Con este .corr podemos ver una primera imagen de como estan nuestras variables numericas podemos observar una alta correlacion entre las columnas fatalities y fatalities passengers asique eliminaremos una, y tambien altas correlaciones entre aboard crew y passengers y fatalities crew y passengers, aqui tambien seguramente eliminemos columnas.


