## Introducción

El procesar datos que fueron capturados en un campo abierto definitivamente no es tarea fácil. La cantidad de formas distintas en que nos podemos referir a una misma cosa multiplicada por todos los errores ortográficos posibles al escribir dichas variantes resulta en un conjunto de datos abrumadoramente heterogéneo.

En la tarea de analizar datos de la ciudad de Mérida caí en la cuenta de que **las palabras de origen maya pueden llegar a ser bastante complicadas de escribir de forma "correcta"** (o más bien en la forma que fue consensuada al fusionarlas con el español) como lo son Chicxulub, Xcanatún, Dzitya y Sodzil, por mencionar algunas. Esto incluso para los que ya llevamos un rato viviendo en Yucatán. 

Llevando gran parte de las colonias de Mérida y Kanansín nombres de origen maya, procuré documentar mi experiencia e iniciar un diccionario que pueda ser de ayuda especialmente para datos de dichas colonias en una aproximación (muy) intuitiva y naïve del procesamiento de lenguaje natural.

Dicho diccionario puede ser descargado aquí o en la carpeta diccionarios.

En este apartado me di la tarea de redactar algunas reflexiones sobre delimitar zonas geográficas dentro de una ciudad.

## Objetivo :triangular_flag_on_post:

Proporcionar un diccionario que facilite el procesamiento de datos que involucren colonias en los municipios de Mérida y Kanasín, especialmente para palabras de origen maya.
:round_pushpin: Yucatán, México.

## Ejemplo 

El script se realizó en R, procesando datos del Directorio Nacional Estadístico de Unidades Económicas correspondientes al año 2010. Se tomó una fracción de las unidades económicas con clasificación "comercio al por menor" del SIAN 2018.
### Algoritmo

Básicamente lo que hace el algoritmo es lo siguiente:

1. Transforma todo a minúsculas.
1. Elimina acentos.
1. Elimina todo carácter no alfanumérico.
1. Busca si alguna de las palabras se encuentra en la columna *input* del diccionario. De encontrar alguna, sustituye la palabra por su correspondiente de la columna *output*.
1. Comprueba si la colonia corresponde a alguna de las listadas por Correos de México.

Se describe con mayor detalle en el script.

## Sobre el dilema de hacer delimitaciones dentro de una ciudad

Si nos interesa conocer lo que está pasando dentro de un país entonces probablemente analizaremos por estado (o por provincia si es Canadá). Si lo que nos interesa es un estado en particular, entonces analizaremos por municipio. Sin embargo, ¿qué zona geográfica utilizamos cuando nuestro objetivo es una ciudad en particular?

Parte **fundamental** del análisis es decidir como delimitaremos dentro de una ciudad. Probablemente lo primero que se nos vendrá a la mente es utilizar **colonias** o **códigos postales**. Otras opciones pueden ser las **áreas geoestadísticas básicas** (AGEPS) del INEGI e incluso considerar una **delimitación propia** que consista en dividir la ciudad en cuatro o seis zonas utilizando calles principales, por ejemplo.

Independientemente de que delimitación utilicemos, esta probablemente vendrá tanto con **ventajas**:heavy_check_mark: como **desventajas**:bangbang:. La elección dependerá de los datos que queremos analizar y de nuestros criterio.

### Código postal
###### Ventajas :heavy_check_mark:
- Único e identificable: es bastante preciso hablar de c. p. ya que son cinco dígitos numéricos, de los cuales dos son fijos para la ciudad pues todos inician con 97.
- Zonas más homogéneas en tamaño dentro de la periferia de Mérida.
- Catálogo de opciones más reducido por analizar (146 c. p. según Correos de México).
- Límites definidos.
- Ya hay dos shapefile de los limites.

###### Desventajas :bangbang:
- Tamaño considerablemente grande en zonas de la periferia (propuesta de solución aquí).
- Las personas no siempre tienen certeza del código postal, mucho menos del de los lugares que frecuenta y por ende no es fácil de comunicar.
- Quienes no conocen su código postal dan como respuesta 97000 lo que levanta una falsa alarma del centro.

### Colonias
###### Ventajas :heavy_check_mark:
- La gente conoce las colonias donde vive, trabaja y frecuenta (aunque con distintos nombres) lo que las hace un medio sencillo de comunicar para el público en general.

###### Desventajas :bangbang:
- Hay distintos *niveles* de colonias, es decir, se puede llegar a ser más o menos específico. Más específico si se da como referencia una privadas o menos específico si hablamos del nombre por el cuál se conoce un conjunto de colonias. Por ejemplo, a veces se da como respuesta Chuburná cuando en realidad la colonia Chuburná como tal no existe si no que es una *zona conformada por muchas colonias distintas*, gran parte de ellas llevando la palabra Chuburna como en su nombre (Chuburná Inn, Boulevares de Chuburná, Chuburná de Hidalgo) y otras no (La Noria, Bugambilias). Una cuestión interesante de las colonias que no llevan como parte de su nombre la zona en la que están es dicho nombre suele agregarse comos una especie de apellido, es decir, se dice Bugambulias de Chuburná o Torres de Caucel.
- El registro es menos preciso ya que no solo puede conocerse con distintos nombres si no que dichos nombres al ser alfanuméricos se pueden escribir de distintas formas (Ejemplo: Sodzil, Zodzil, Dzodzil).
- No son homogéneas en tamaño, especialmente si no tomamos en cuenta los distintos *niveles*.
- Catálogo de opciones más extenso por analizar (728 según Correos de México)
- Limites relativos y en constante cambio.
- ¿Hay shapefiles de esto?

### AGEPS
###### Ventajas :heavy_check_mark:
- Traen consigo un conjunto de características descriptivas de la población que habita ahí.
- Límites definidos
- Hay shapefile único.

###### Desventajas :bangbang:
- Cambian con cada censo para proteger la privacidad.
- No son faciles de comunicar.

### Contacto
Puedes mandarme un correo a veronicamtz0512@gmail.com :hatching_chick:
