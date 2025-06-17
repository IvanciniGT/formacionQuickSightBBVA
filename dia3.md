
# Análisis conjunto de 2 variables o más.

Esto lo más interesante.
Cualquier persona que tenga experiencia con un negocio, al poco tiempo entiende cómo son los datos (esto es lo mismo que cuando os preguntaba que peso tiene una personas de 3 años.)

Lo que tratamos es de identificar relaciones que se dan en los datos... esas relaciones son las que nos ayudan a tomar decisiones.

Lo que vamos a querer es tomar decisiones sobre el futuro basadas en datos pasados. Esto es jugar a ser adivinos. De cara a hacer una predicción puedo usar varias técnicas:
- Mirar la bola de cristal
- Mirar los posos del café / té
- Mirar datos, entenderlos y suponer (y ojo que eso es mucho decir!!!) que el mundo va a seguir funcionando más o menos igual (RIESGO GIGANTE!)

La estadística lo que me ofrece es una forma de tasar el riesgo de equivocarme (INFERENCIAL).
Lo cierto es que tiene sentido aplicarlo cuando trabajamos con muestras pequeñas.

---

Para saber cómo está el tema de los €€€ en el banco... digo... tomo a unos cuantos y les pregunto.
15 personas... y les pregunto.. Cuánto te pagan. MEDIANA = 7.304€ / mes
Esa mediana que he calculado es representativa del salario que se cobra en el banco?
- Si la muestra que he tomado tiene la misma representación que el conjunto de datos, entonces si.
- El problema es la probabilidad de que eso ocurra.

Cuantas potenciales muestras existen de 15 personas que trabajen en el banco? INFINITAS
5000 personas. Y las tomo en grupos de 15. Cuántos grupos de 15 diferentes puedo sacar de 5000?
- 5000! / (15! * (5000 - 15)!) = 1.53e+13
La probabilidad de que la muestra que he tomado la ideal (sea muy representativa) es muy baja.

Esa probabilidad aumentaría de sobremanera si tomo más datos.
Es peculiar el tema. Pero... tomando más de 200... 300 datos... la probabilidad de que la muestra sea representativa es muy alta.... con independencia del tamaño de la población.

--- 

Sin meternos en la parte de inferencial... las conclusiones de un estudio descriptivo las podremos dar por ciertas (significativas ... desde el punto de vista estadístico) si tenemos un conjunto de datos de un tamaño medio / Grande (>= 200, 300 datos vamos bien)

A veces creemos que tenemos ese volumen de datos... pero no es así.
Yo no puedo hacer una estadística de 8 datos. La significación estadística es 0 con 8 datos.

El problema es que muchas veces quedamos en eso.

Imaginad que tengo 16.000 videojuegos... y tengo 8 mil millones de ventas. SERA POR DATOS !
Plataformas: 30/40 plataformas diferentes.
Géneros: 20 géneros diferentes.

16.000/40 = 400 videojuegos por plataforma / 20 géneros = 20 videojuegos por género y plataforma.
Y el problema es que habrá plataformas y géneros mayoritarios.
Esos 20 no son constantes... Es decir, habrá combinaciones de plataformas/géneros que tendrán 300 videojuegos y otras que tendrán 1...3...8 videojuegos.

Cuando empiezo a agrupar datos, me voy a encontrar con conjuntos muy pequeños... que no me sirven para hacer una estadística significativa. En la mayor parte de los caso, podré descartar esa información... tirarla a la basura... simplemente porque lo que voy a obtener al hacer un estudio no tiene VALIDEZ estadística. NINGUNA.
---

Además de este problema... tengo otro:
Si tengo 20 géneros y 30 plataformas... en total tengo 600 combinaciones de géneros y plataformas.
Ya no me da el cerebro. Podré entender que hay una combinación... o 3 que destacan

---

Los estudios que podemos hacer:

- NOMINAL x NOMINAL
  Tabla de frecuencias a 2 columnas (contingencia) ... que podré representar gráficamente (barras agrupadas, apiladas, etc.)
  Lo que buscamos son casillas dentro de esa tabla que nos escamen(que no nos cuadren...)
- NOMINAL x ORDINAL
  Aquí puedo hacer lo mismo que con NOMINAL x NOMINAL
  Pero además puedo calcular la mediana de la variable ordinal => Estudio de comparación de medianas entre los grupos que nos da la variable nominal.
- NOMINAL x CUANTITATIVO
  Lo mismo que las anteriores... pero además puedo calcular la media => Estudio de comparación de medias entre los grupos que nos da la variable nominal.
  Si las medias / medianas son diferentes para distintos grupos... concluyo que hay relación entre las variables => Impacto a la hora de tomar decisiones. GRÁFICO: BOXPLOT MULTIPLES / pirámide poblacional, gráficos de violín.

    VENTAS
        GRUPOS: Mes (12 meses)
        Cantidad de bicicletas/gafas de sol/camisetas de tirantes/ropa de esquí vendidas
        Precio medio de hotel

- ORDINAL x ORDINAL
- ORDINAL x CUANTITATIVO
- CUANTITATIVO x CUANTITATIVO
  Grafos de dispersión (nube de puntos) 
   Son gráficos muy potentes.. pero tienen un problema. Hay veces que tengo muchos puntos uno encima de otro... y en el gráfico eso no lo veo.

        Variable A
        ^
        |   X                            X
        |                     X                       O
        |                          O
        |        O             X           X
        | O                        X                     X
        +----------------------------------------------------------> Variable B
    
    Por eso a veces echamos mano de indicadores estadísticos que nos ayudan a ver la relación entre las variables: Coeficiente de correlación de Pearson (r) 

---

En el mundo BI hay una variable que marca demasiado: TIEMPO.

Una variable FECHA es de tipo cuantitativo.
La variable AÑO (extraído de una fecha) es una variable cuantitativa.
La variable MES (extraído de una fecha) es una variable NOMINAL. Ni siquiera es ordinal.
   ABRIL < MAYO < JUNIO < JULIO < AGOSTO < SEPTIEMBRE < OCTUBRE < NOVIEMBRE < DICIEMBRE < ENERO < FEBRERO < MARZO                                                                          2023     2024

AÑO / MES  también es cuantitativa

---

Hemos visto que a lo largo del tiempo, hay géneros que lo han petado más que otros.
También vemos que a lo largo del tiempo van saliendo nuevas consolas que van reemplazando a las anteriores.

Las 2 tienen relación ocn el tiempo.

Si queremos hacer un análisis de géneros x plataforma, deberíamos tener en cuenta que:
- Hay géneros que es ciertos momentos estaban de moda.. y por ende, para las plataformas que salieron en un momento del tiempo, es previsible que hubiera más ventas de esos géneros.
- ** Las plataformas que salieron en un momento del tiempo pudieron introducir mejoras tecnológicas que hicieron que ciertos géneros se vendieran más en esas plataformas que en otras. **

---

Canales de venta:                            Tipo de producto comprado

- Teléfono                                  Tipo de Producto A
- Web                                       Tipo de producto B
- Tienda física                             Tipo de producto C
- App          

---

Precio <- Fecha, Género, Plataforma

Ventas?? -> Precio NO PUEDE SER

Si acaso las ventas vienen influidas por el precio... pero no al revés.. por una simple cuestión de temporalidad

Además de fecha, género y plataforma(consola), que otra cosa puede influir en el precio?
- Región. (DESCARTADO)
- Editorial... Que haya editoriales más caras que otras (FAMA)
- Edad... pero tenemos ese dato? NO... DESCARTADO
- Calidad del producto
Tenemos una forma de medir la calidad del producto? Si tenemos un buen juego o no. Mola o no mi juego?
  Esto que estamos midiendo ... es algo SUBJETIVO!
  Qué significa que el juego mola? ESTO YA NOS CUESTA DEFINIRLO!
    0    No mola nada
    10   Que a todo el mundo le mola
  Cómo definiríais el nivel de ANSIEDAD de una persona? Cómo mido esto?
   ¿Qué escala uso para medirlo? 0-100
    0 -> No hay ansiedad
    100 -> Ansiedad máxima
  Tiene que ver con si es aditivo. Valoraciones de jugadores

  Muchas de estas variables, que tienen que ver con calidad... satisfacción... son variables que no sabemos casi ni definir... ni determinar con precisión una escala de medición.
  Desde luego no tengo ni siquiera instrumentos para medirlo directamente.

Nivel de empoderamiento de una persona! y cómo lo mido?
0
100


Muchas de estas variables, las medimos de forma indirecta.
No sabemos muchas veces ni definirlas.. pero si sabemos cosas con las que tienen que ver.

Si el juego mola o no mola... medirlo es complejo. Puedo hacer una encuesta de satisfacción... el problema es que para distintas personas, el concepto de molar es distinto.

Quizás en parte tiene que ver con las unidades vendidas de ese juego.

Depende solo de si el juego mola o no mola que se venda o no se venda? Seguro que no.
Pero.. de alguna forma veo que puede haber una relación... entre molar y vender más o menos el juego.

Podría generar un indicador de si el juego "mola" en base a ciertas medidas:
- Ventas
- Valoraciones de jugadores
- Valoraciones de críticos
- ...

Y quizás puedo calcular ese INDICE / INDICADOR sobre los juegos que ya tengo en la base de datos.
Y cruzarlo con el precio.
Y aplicarlo luego a mi juego nuevo.

EXAMEN DE MATES: El grado de aprovechamiento de las clases de mates / con el nivel que ha ido adquiriendo sobre los conceptos manejados durante las clases.
P1 = 3+4        SABER SUMAR
P2 = 5+6        SABER SUMAR
P3 = 7x8        SABER LAS TABLAS
P4 = 9x3        SABER LAS TABLAS
P5 = 7x12       SABER LAS TABLAS y SUMAR

De alguna forma yo creo que el saber hacer esas operaciones guarda relación con el aprovechamiento de las clases de mates o con los conceptos aprendidos en las clases de mates.

Un dato, mide una cosa.. siempre. En nuestro caso, la pregunta P5 mide si el alumno saber hacer la operación 7x12.
Lo que pasa es que ese dato incluye INFORMACIÓN de otros conceptos... que puedo aprovechar (extraer)... destilar, para medir otras cosas

Igual pasa con la variable ventas de videojuegos... parte de la información que contiene tiene que ver con si el juego mola! Además contendrá información de si se ha hecho una buena campaña de marketing, si el juego es de una saga famosa, si es tipo de juego está de moda moda, si es para una consola con mucho tirón...

Pocas veces quiero trabajar con los datos en bruto... En general eso no da buen resultado. Las cosas son mucho más complejas de lo que parecen.

---

- IMAGINAD UNA COMPAÑIA DE SEGUROS DE COCHES.

Para darle precio a un cliente / o para decidir si aceptan al cliente o no, tienen en cuenta un montón de variables:

- MODELO DE COCHE?
- CASADO?
- TIENE HIJOS?
- EDAD?
- LA CANTIDAD DE KMS QUE HACE AL AÑO?
- SI HA TENIDO OSTIAS ANTES?
- AÑOS DE CARNET

Esas cosas tiene relación directa con el hecho de si la persona va a tener un accidente o no el próximo año.

Que tiene relación directa con la probabilidad de tener un accidente de coche?
  - EXPERIENCIA DE CONDUCCIÓN                   EDAD(a más edad, más experiencia) AÑOS DE CARNET
  - NIVEL DE EXPOSICIÓN AL PELIGRO              HIJOS 
  - AGRESIVIDAD EN LA CONDUCCIÓN                EDAD(a más edad, menos agresividad)
  - CAPACIDAD DE REACCIÓN DEL CONDUCTOR         EDAD(a más edad, menos capacidad de reacción)
  - NIVEL DEL RESPONSABILIDAD AL VOLANTE        CASADA/HIJOS


Sabéis quien hace ese trabajo de maravilla?
 Las redes neuronales (IA) (MACHINE LEARNING)
 - Un modelo de IA de hoy en día... GPT-4... tienen en torno a decenas de millardos de parámetros
   10.000.000.000 parámetros

Eso, con 1 millón de datos... un ser humano.. no se empapa de nada!
Una computadora, lo hace de de forma extraordinaria.

Este es un siguiente nivel en nuestros estudios.    
Esa queda fuera de nuestro alcance! Hay muchos comportamientos/relaciones que no son lineales(directos).


Medir el nivel de satisfacción de un cliente no es llamarle por teléfono y hacerle una pregunta.
Pero es que es má gordo.. es que me vale mierda el nivel de satisfacción de un cliente... como empresa.

Lo que pasa es que creo que hay una relación entre ese concepto "satisfacción" y el hecho de que un cliente vuelva a comprarme o no.... o hable mal de mi o bien... o vaya a abandonar mi marca o no.

Y a su vez, el concepto satisfacción tiene que ver con un montón de cosas:
- Encuesta (Una llamada por teléfono) (que tendrá una cantidad de ruido de narices)
- Número de reclamaciones que ha hecho
- El tiempo que lleve con nosotros
- Número de productos que tiene con nosotros

--- 
1. Cargamos en nuevo fichero
2. Generamos un conjunto de datos nuevo, con NOMBRE, PLATAFORMA, PRECIO : Precio videojuegos
3. Enriquecemos el conjunto de datos que ya tenemos (PRECIOS VENTAS Videojuegos) con el nuevo conjunto de datos (PRECIO)
4. Hacemos un análisis y vemos si hay relación entre precio y:
 - Ventas
 - Año
 - Género
 - Plataforma
 - Editorial
Y a ver qué sale. <... CONCLUSION

---

Hay una variable que no ha sido adecuada... en el trabajo:
PLATAFORMA... Porque las plataformas guardan una relación directa con el tiempo enorme...
Y nacen y mueren.

Posiblemente una variable más interesante habría sido TIPO DE PLATAFORMA:
- Portátil
- En casa con la tele
Otra variable interesante: RANGOS DE AÑOS / Generación consola

 PS5 - XBOX SERIES X     Juntando consolas que llevan la misma tecnología
 PS4 - XBOX ONE
 PS3 - XBOX 360
 PS2 - XBOX