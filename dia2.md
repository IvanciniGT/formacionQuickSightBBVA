
# Nuestro fichero de datos

| Nombre | Plataforma | Año | Genero | Editorial | Ventas NA | Ventas EU | Ventas JP | Ventas Otros | Ventas Global |
| ------ | ---------- | --- | ------ | --------- | --------- | --------- | --------- | ------------ | ------------- |
| Boulder Dash: Rocks! | DS | 2007 | Puzzle | 10TACLE Studios | 0 | 0.03 | 0 | 0 | 0.03 |
| Panzer Tactics | DS | 2007 | Strategy | 10TACLE Studios | 0.06 | 0 | 0 | 0 | 0.06 |
| Pirates: Legend of the Black Buccaneer | PS2 | 2006 | Adventure | 10TACLE Studios | 0.01 | 0.01 | 0 | 0 | 0.02 |
| King's Bounty: Armored Princess | PC | 2009 | Role-Playing | 1C Company | 0 | 0.01 | 0 | 0 | 0.01 |
| Men of War: Assault Squad | PC | 2011 | Strategy | 1C Company | 0.01 | 0.03 | 0 | 0.01 | 0.05 |
| Off-Road Drive | PC | 2011 | Racing | 1C Company | 0 | 0.03 | 0 | 0.01 | 0.04 |

Nombre: Nombre de un videojuego que se ha lanzado al mercado
Plataforma: Plataforma en la que se ha lanzado el videojuego . En qué consola está disponible: XBOX, PlayStation, PC, etc.
Año: Año en el que se ha lanzado el videojuego
Genero: Género del videojuego. Tipo de juego... Disparos, puzzle...
Editorial: Empresa que ha publicado el videojuego
Ventas: (están en millones de unidades)
 - NA: Ventas en Norteamérica
 - EU: Ventas en Europa
 - JP: Ventas en Japón
 - Otros: Ventas en el resto del mundo
 - Global: Ventas totales del videojuego

---

# Tipos de variables:

- NOMBRE: Cualitativa nominal <<<<< IDENTIFICADOR del videojuego
- PLATAFORMA: Cualitativa nominal
- AÑO: Cuantitativa discreta DE INTERVALO
- GENERO: Cualitativa nominal
- EDITORIAL: Cualitativa nominal
- VENTAS: Cuantitativa continua DE RAZÓN... Algo especial con esta columna? Qué es esa columna? NUMERO DE VIDEOJUEGOS VENDIDOS
    0.1 millones = 100.000 unidades  

> En general cualquier columna con el nombre "Número de..." es una FRECUENCIA!

Lo que tenemos delante es un conjunto de datos YA RESUMIDOS! Cuál sería el conjunto de datos subyacente? Cada una de las ventas

DIA X, Federico ha comprado el videojuego "Boulder Dash: Rocks!" en la plataforma DS, en Japón
DIA Y, Menchu ha comprado el videojuego "Boulder Dash: Rocks!" en la plataforma DS, en Japón


```
Nombre	                    Plataforma	Año	    Genero	    Editorial	Ventas NA	Ventas EU	Ventas JP	Ventas Otros	Ventas Global
Men of War: Assault Squad	PC	        2011	Strategy	1C Company	0,01	    0,03	    0	        0,01	        0,05

Nombre	                    Plataforma	Año	    Genero	    Editorial	Ventas  Región
Men of War: Assault Squad	PC	        2011	Strategy	1C Company	0,01	NA
Men of War: Assault Squad	PC	        2011	Strategy	1C Company	0,01	Otros
Men of War: Assault Squad	PC	        2011	Strategy	1C Company	0,03	EU
```

Interesa, cuando me enfrento a un conjunto de datos, tener un visión más amplia de lo que tengo delante. Una cosa es cómo me hayan pasado los datos... otra cosa son los datos que realmente tengo.
Hay una columna más... que no habíamos visto: REGION (Nominal)

---
A la hora de comenzar un análisis hay que ser un poco metódico. Vamos a empezar haciendo un análisis descriptivo univariable de los datos.

NOMBRE? No le aplica mucho todo lo que hemos discutido ayer.. Es un IDENTIFICADOR.
 Técnicas más raras: NUBE DE PALABRAS: Extraer las palabras del nombre... hacer tablas de frecuencias de las palabras.
 Más adelante buscar si hay palabras que se repiten mucho en juegos con muchas ventas.

 Tabla de frecuencias aplicando el peso de ventas: Ventas por juego...> TOP 10 juegos con más ventas

(GENERO,EDITORIAL,) PLATAFORMA
  Tabla de frecuencias? Quiero entender qué plataformas hay.
   - Hago esa tabla de frecuencias sobre el conjunto de datos... el que tengo delante.
     ¿Qué título le pongo a la tabla? ¿A qué pregunta responde?                         Número de juegos disponibles por plataforma
                                                                                                         publicados
     La información de ventas está resumida en una columna (VENTAS GLOBAL).
     Distinto sería aplicar el mismo procedimiento sobre el conjunto subyacente.
   - Podría hacer esa tabla, multiplicando cada fila por el número de ventas globales (asignando un PESO a cada fila: VENTAS GLOBALES)
     ¿Qué título le pongo a la tabla? ¿A qué pregunta responde?                         Número de juegos vendidos por plataforma
  En función a nuestros intereses podríamos calcularla con datos relativos o absolutos. En un caso como éste nos interese más absolutos.
    - GRÁFICO: 
    - BARRAS
    - SECTORES
  ¿Podría calcular valores acumulados en la tabla de frecuencias?
    La variable no es ordinal.. por lo que no tiene un orden implícito... 
    Pero ... ¿podríamos ordenar los datos con algún tipo de sentido? Podríamos ordenar por la frecuencia.
    Dejo arriba las plataformas que más juegos tienen disponibles o que más juegos hayan vendido (en base a si aplico el peso o no)
    El dato acumulado me ayudaría a ver las 3 plataformas que tienen más del X% de los juegos disponibles o vendidos.

AÑO
  TABLA DE FRECUENCIAS? A pesar de ser una variable cuantitativa es discreta .. y tiene pocas categorías (<30)
    - ¿Qué título le pongo a la tabla? ¿A qué pregunta responde?                         Número de juegos publicados por año
    - Si tengo en cuenta el peso de las ventas globales:                                 Número de juegos vendidos   por año
  GRAFICO? 
  - HISTOGRAMA!!
  ESTADISTICOS: 
    - MEDIA/MEDIANA? No parece tener mucho sentido. 
    - RANGO: Mínimo-Máximo

VENTAS: VARIABLE CUANTITATIVA... con MUCHOS DATOS DIFERENTES
  TABLA DE FRECUENCIAS? Si la calculase... sería enorme.... y una tabla enorme... aporta poco.
    Podría crear intervalos
  Qué título tendría esa tabla? 
    Número de veces que un juego en una plataforma ha obtenido ventas en un intervalo = RARO!
  ESTA VARIABLE(s) SON FRECUENCIAS. No tiene sentido someterlas a este tratamiento.
  DIBUJAR UN HISTOGRAMA
  Estadísticos:
  - RANGO: Mínimo-Máximo
  - MEDIA/MEDIANA? 

---
Con este estudio, lo que conseguimos es comenzar a entender los datos.
Una vez analizadas las variables por separado... podemos empezar a juntar variables. AQUÍ ES DONDE SE PONE LA COSA DIVERTIDA!

NOMBRE, PLATAFORMA, AÑO, GENERO, EDITORIAL, VENTAS

- NOMBRE x ???? No tiene sentido... es un identificador.
- PLATAFORMA x AÑO

   Lo que me contará será qué plataformas tiene juegos nuevos en cada año.
   Si añado (VENTAS GLOBAL.. como PESO) obtendré  cuántas ventas ha tenido cada plataforma en cada año.

   Qué pasa con el tiempo/fecha y las plataformas? HAY RELACIÓN ENTRE ESTAS 2 VARIABLES? SEGURO... ENORME
   Al mercado, según pasan los años, van saliendo nuevas consolas... y otras van desapareciendo.

- GENERO x AÑO
   
    Para qué géneros se van publicando juegos cada año? Cuántos publicaciones de juegos en plataforma diferentes van saliendo de cada género cada año? RARO

    HABRÁ RELACIÓN? ENORME
     Los gustos de la gente cambian... las tecnologías también cambia.
     Antiguamente a la gente le gustaban más cierto tipo de juegos... y ahora otros.
     Antiguamente teníamos capacidad para hacer ciertos tipos de juegos... y ahora otros.

    Si añado (VENTAS GLOBAL.. como PESO) obtendré  cuántas ventas ha tenido cada género en cada año.

- EDITORIAL x AÑO
    Nos pasa un poco igual que con el género:
    1. Una misma editorial aparecerá repetida para cada plataforma en la que haya publicado un juego.
    2. También habrá una relación entre las editoriales y los años. 
       Hay empresas que salen al mercado... y otras van muriendo.

- PLATAFORMA x GENERO

    En todas las consolas se juega al mismo de juegos? NO
     - Capacidad tecnológica del dispositivo/plataforma
     - Forma de interactuar con el dispositivo/plataforma

    Pero aquí va a haber otra cosa? Y es jodido. VER NOTA 1
        Qué variable afectaba a las plataformas? LA FECHA/AÑO
        Que variable afectaba a los géneros? LA FECHA/AÑO
        Y debido a esto, plataforma y género van a estar relacionados... fijo! a través de la variable mediadora (FECHA/AÑO)
        La pregunta que debemos hacernos es, si descontando el efecto de la variable mediadora (FECHA/AÑO), hay relación entre plataforma y género?

    Caso en el que el paso del tiempo puede estar forzando una relación entre plataforma y género:
        Si con el paso del tiempo, tenemos capacidades tecnológicas que permiten generar simuladores de conducción mucho más realistas...
        Puede ser que según pase el tiempo, vea que hay más juegos de conducción en las plataformas que tienen más capacidad tecnológica?
        Pero por el simple hecho del paso del tiempo ya tengo más capacidad tecnológica... 
        Y por el simple hecho del paso del tiempo, van saliendo nuevas plataformas.
        Y puede pasar que haya plataformas donde vea muchos juegos de simulación de conducción... Pero no por la plataforma... 
        Sino porque esa plataforma ha salido en un momento del tiempo que la tecnología lo permite.
        Y en otras plataformas más antiguas no veo tantos juegos de simulación de conducción... porque la tecnología no lo permitía.
    Caso en el que hay una relación entre plataforma y género con independencia del paso del tiempo:
        Podría pasar que haya plataformas especializadas en distintas edades... y asociado a la edad del jugador, se tiende hacia un género u otro.
        En la consola WII, hay un mando especial... que invita más a jugar a juegos de tipo DEPORTIVOS.


- PLATAFORMA x EDITORIAL
   Relación encontraremos fijo... por estar siempre la variable TIEMPO... 
   La pregunta de nuevo será si a pesar de la variable mediadora (FECHA/AÑO), hay relación entre plataforma y editorial?
   Es decir, si hay editoriales que se han especializado en publicar juegos para ciertas plataformas... o si por el contrario, todas las editoriales publican en todas las plataformas.  

    Evidentemente hay editoriales que no publicarán en ciertas plataformas... porque esa editorial ha existido en un momento del tiempo en el que esa plataforma no existía. (YA ESTA JODIENDO LA VARIABLE MEDIADORA)

    Pero... de entre las que existían en ese momento del tiempo... ¿hay editoriales que se especializan en publicar en ciertas plataformas? ( Y ESTA ES LA RELACIÓN QUE PUEDE INTERESAR)

- GENERO x EDITORIAL
   Aquí lo mismo!


> A la hora de buscar relaciones en Business Intelligence, hay una variable que marca mucho... TODO: FECHA

Las cosas cambian con el tiempo, las tendencias cambian con el tiempo, los comportamientos cambian con el tiempo.


---

# NOTA 1

¿Hay relación entre la altura de un ser humano y sus conocimientos de matemáticas? NO

Si miro en personas de 30-40 años... posiblemente en los datos no encuentre relación entre la altura y los conocimientos de matemáticas.
Si miro en personas de 5-15 años...  posiblemente encuentre una relación GIGANTE entre la altura y los conocimientos de matemáticas.

Al menos es lo que la estadística me va a decir. Y es cierto... lo que pasa es que no pedo usar esa información para sacar conclusiones de causalidad. 
NO PUEDO DECIR QUE POR EL HECHO DE SER MÁS ALTO VOY A SABER MÁS MATEMÁTICAS. No es cierto! Pero estadísticamente si voy a ver una relación entre las variables... Y CON ESTO HAY QUE TENER MUCHO CUIDADO... para no caer en malas interpretaciones de los datos.
ESTO ES LO QUE EN ESTADISTICA LLAMAMOS UNA CORRELACIÓN ESPURIA. Y salen muchas.

En este caso, lo que tenemos es una variable mediadora... que nos está jodiendo.. la edad.

Y ES LA EDAD la que influye en la altura.
Y ES LA EDAD la que influye en los conocimientos de matemáticas.

Y eso provoca que al mirar los datos encuentre una relación entre la altura y los conocimientos de matemáticas... pero que no es causal.

Estas cosas NECESITAMOS IDENTIFICARLAS.

---

QUICKSIGHT es una herramienta de BI.
Le tienen que llegar los datos de la mejor forma posible para poder hacer un análisis.
Eso nos pasa con cualquier herramienta de este tipo.

Una cosa es cómo tenemos los datos en un entorno de PRODUCCION, otra como los llevamos al Datalake.
Y otra diferente es cómo los necesito en un DATAWAREHOUSE para hacer un análisis de BI.

Quicksight no es una herramienta que nos vaya a permitir hacer un tratamiento fuerte de los datos.
Su objetivo es el análisis.
En la mayor parte de los casos, en BI nos interesa tener los datos organizados en un modelo en estrella o copo de nieve (=snowflake). El snowflake es la generalización del modelo en estrella.

            dimension1
                 ^
    dim2    <  HECHOS  > dim 3

Si hiciéramos algo como esto en nuestros datos:

               
                        plataforma
                            ^
      genero  <  ventas_juego_plataforma  > editorial
                            v
                           año

Básicamente es lo que tenemos... la tabla de ventas la tenemos agrupada.
En nuestro excel, la información de plataforma, género, editorial son campos de tipo TEXTO (STRING)..
Nos gusta eso? Ni de coña!
- Ocupan mucho
- Y van a hacer que todo vaya más lento

En general NUNCA queremos tener ese tipos de campos (dimensiones) ligadas mediante textos... y los textos repitiéndose una y otra vez.

Luego habría otros temas... que en nuestro caso no aplican mucho.
Si tuvieramos una fecha (lo que tenemos es un año)... esa fecha la meteríamos:
- en la tabla de dimensiones?  AQUI.
- o en un campo en la tabla de hechos?

Y qué campos tendría esa tabla:
- AÑO
- MES
- DIA
- TRIMESTRE
- CUATRIMESTRE
- SI CAE EN FESTIVO
- SI CAE EN FIN DE SEMANA
- El DIA DE LA SEMANA (Lunes o si es jueves)

Vinculamos la tabla de dimensiones a la tabla de hechos mediante un ID NUMERICOS !

En nuestro caso no tenemos esa casuística... tenemos un AÑO que ya es numérico! no tiene sentido sacarlo a una tabla de dimensiones.
El resto de datos si los vamos a sacar a varias tablas de dimensiones. Aunque nuestras tablas no tendrán más información.

Lo tenemos en un EXCEL. 
Qué tal son los EXCEL para BI?
CSV MEJOR, JSON, XML, YAML

TODOS ESOS Tienen el mismo problema que el EXCEL (xlsx)... es un XML

Todos estos ficheros tienen el mismo problema: Son ficheros de texto plano. Lo que se guarda en esos ficheros son caracteres... codificados como bytes... pero caracteres.

AÑO: 1990 <- Lo que guardo son 4 caracteres
XBOX: "XBOX" <- Lo que guardo son 4 caracteres
"20th Century Fox Video Games" <- Lo que guardo son 27 caracteres = 27 bytes -> (como mucho si hay caracteres raros: 30-32)
Si lo codifico como número entero, lo que guardo son 4 bytes.

No es solo el hecho de la codificación... es que como se guarda como texto, ocupa más espacio.
Fecha: 2023-10-01 <- 10 caracteres 
                  <- 4 bytes si la guardo como fecha

Si trabajo con pocos datos... un Excel... cualquiera de esas variantes me sirve.
Si trabajo con muchos datos ... todo eso NO ME VALE.

Necesitamos formatos BINARIOS. Esos formatos me permiten asignar a cada dato un TIPO DE DATO... y que se guarden en consecuencia.
Los formatos binarios son:
- Parquet
- Avro

Esos formatos, tanto PARQUET como AVRO son formatos binarios.. que hacen que el almacenamiento de los datos sea más eficiente.
- No es solo que ahorre en almacenamiento
- Por ser más pequeños los datos se leen más rápido.
- Los podré escribir más rápido
- Los mandaré por red más rápido

Entre ellos también hay diferencia... y tienen casos de uso muy diferentes.
- PARQUET Es un formato orientado a columnas    < BI
- AVRO Es un formato orientado a filas          < ETL


Imaginad este conjunto de datos:

```csv
NOMBRE, APELLIDOS, EDAD
Federico, Fernández, 30
Menchu, García, 28
Fernando, Gómez, 35
```

Esos datos, dentro de un archivo parquet se guardarían:
```
NOMBRE(STRING), APELLIDOS(STRING), EDAD(INTEGER)
INDICE :
NOMBRE-> byte 50
APELLIDOS-> byte 101
EDAD-> byte 100
Datos:
NOMBRES: ["Federico", "Menchu", "Fernando"]
APELLIDOS: ["Fernández", "García", "Gómez"]
EDADES: [30, 28, 35]
```

En AVRO se guardarían de forma diferente:
```
NOMBRE(STRING), APELLIDOS(STRING), EDAD(INTEGER)
INDICE : 
0 ->  byte 50
1 -> byte 101
2 -> byte 100
Datos:
Federico, Fernández, 30
Menchu, García, 28
Fernando, Gómez, 35
```

Tanto en Datalakes como en datawarehouse manejamos mucho ese tipo de ficheros.

---

QUICKSIGHT, para acceder a nuestros datos nos ofrece 2 opciones:
- Conectarse a un origen externo (Una BBDD...) y cada vez que necesite acceso a los datos, se conectará a ese origen externo.
- Importar los datos a su propio almacenamiento interno (SPICE) y trabajar con ellos desde allí.

Si opto por usar SPICE, todo va a ir muy rápido... está muy optimizado.
Además hay un tema... y es que SPICE lo iremos actualizando a intervalos de tiempo.
Y mientras no se haya actualizado, sabemos (QUICKSIGHT sabe) que los datos no han cambiado.
Por ende, puede generar un sistema de CACHE muy eficiente. 
Cualquier cálculo que haya que hacer sobre los datos, se puede almacenar en ese sistema de CACHE y no volver a calcularlo a no ser que los datos cambien.

TENGO QUE PAGARLO!

La otra opción es conectar el QS a mi BBDD... pero claro.. cada vez que haya que hacer un cálculo, va a tener que ir a la BBDD, hacer la consulta y traer el resultado. Y además, no se puede asegurar que los datos no hayan cambiado... por lo que no es posible disponer de un sistema de cache! Si 10 personas hacen en un minuto un informe... una query a la BBDD... la query se ejecuta 10 veces (ahí luego entran las optimizaciones de las BBDD.. y sus caches)

Esto va MUCHO MAS LENTO!
El tema es que si trabajo con SPICE no estoy accediendo a datos en tiempo real... lo cual en el mundo de BI no suele ser un problema.
Normalmente los estudios de BI se hacen sobre datos históricos... y no sobre datos en tiempo real.
Me puedo permitir perfectamente el trabajar con datos actualizados a AYER.

OJO... hay casos donde no puedo... entonces mejor me iría cambiar totalmente de enfoque y dejar de usar QUICKSIGHT.
Hay otras herramientas para datos en tiempo real: ELASTICSEARCH -> KIBANA

---

En nuestro caso, por ahora, vamos a cargar el excel.. y lo llevaremos a SPICE... no hay opción!
Ojo... tanto desde ficheros, como desde BBDD ... etc...  me puedo traer datos a SPICE.


-----
0.9999999999999..... = 1