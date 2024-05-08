# Aircraft-Accidents-Project
#Accidentes aéreos y víctimas mortales desde 1908 a 2023

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

#Exploración inicial de los datos
#tipos de datos
#Nulos (comprobar, no trabajar con ellos todavía)
#columnas

![Captura de pantalla 2024-05-08 142604](https://github.com/19972024/Aircraft-Accidents-Project/assets/156945446/fd68c3e7-cf62-4ed9-a92d-56013a0eb6f8)



#Luego empezamos a analizar los distintos campos categóricos. 

#Definir tratamientos a realizar:
#Corrección de categorías: value_counts? gráficas?
#Hay algún campo que se pueda utilizar para feature extraction?
#Hay algún campo que deba eliminarse por cantidad de nulos? Se podría hacer algo para evitarlo?
#Hay algún campo que deba eliminarse ya que no aporta información?
#Una vez corregidas las categorías -> chequear test chi-cuadrado para eliminar variables relacionadas

A traves de una funcion realizamos un value counts a todas nuestras variables categoricas:

![Captura de pantalla 2024-05-08 142750](https://github.com/19972024/Aircraft-Accidents-Project/assets/156945446/b19703ec-543b-4fc6-b58d-ee466ae70f32)

# Realizamos un value_counts de todas las columans que aparecen como categoricas para dar una primera mirada.

# Separaremos la columna date en año, mes, dia para buscar patrones, eliminaremos la columna time por su gran cantidad de nulos, ya que no encontre una manera correcta de poder rellenar esos datos.

# En la columna location, buscaremos eliminar espacios y signos si los hay a traves de algun metodo regex o lambda, luego analizaremos agruparlos por ciudades y paises. (Ver que hacemos con esos 4 nulos)

# En la columna Operador, buscaremos eliminar espacios y signos a traves de algun metodo regex o lambda. (Ver que hacemos con esos 10 nulos).

# La columna flight la eliminaremos por su gran cantidad de nulos.

# La columna route nos puede aportar algun tipo de informacion podemos elegir algunas categorias y agruparlas depende de que cantidad de informacion nos aporte sino la eliminaremos.

# La columna ac_type nos ayudara a comprender ciertos aspectos de nuestro df ya que aqui tenemos los modelos de aviones involucrados en estos accidentes, hay que solo analizar que hacer con los 70 nulos que tenemos

# De las columnas registration y cn_ln que eliminaremos seguramente por ser poco relevantes para nuestro analisis.

# Por ultimo la columna summary seguramente sera eliminada ya que para el modelo que luego tenemos que hacer no nos servira, si ayudara al principio a limpiar nuestro df ya que tiene una gran cantidad de informacion que puede ayudar y/o rellenar las demas columnas del df, ademas de arrojar gran informacion para entender patrones o buscar curiosidades de los diferentes accidentes.

