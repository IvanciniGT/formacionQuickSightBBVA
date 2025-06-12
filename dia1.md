
# QuickSight

Es la herramienta de BI de AWS. 

---

# BI: Business Intelligence

Buscamos aportar datos para mejorar la toma de decisiones... de negocio.
Que haya una toma de decisiones basada en datos.

Punto 1... necesitaremos analizar los datos. Lo que vamos a hacer desde el punto de vista de BI es aplicar técnicas estadísticas básicas (descriptivas... técnicas nivel instituto)

Vamos a manejar datos... y las computadoras .. y los programas que en ellas se ejecutan (salvo GLORIOSAS EXCEPCIONES) clasifican esos datos en bases a su TIPO DE DATO.
Tipos de datos:
- Integer
- Float
- String
- Date
- Boolean

Eso está guay.. desde el punto de vista de la computación. Y tiene su impacto.

Pero desde el punto de vista de BI (análisis), esa clasificación es relevante? ME LA PELA!
Y casi todos los programas de BI, me hablan de conceptos (tipos de datos) computacionales, pero no de tipos de datos desde el punto de vista del análisis. Y ESTO ES LA BASE.. Es lo primero.

Tipos de datos, desde el punto de vista estadístico?
- Cualitativos
  - Norminales
  - Ordinales
- Cuantitativos               Unidad de medida (y por ende cantidades), las operaciones matemáticas toman sentido... si no NO. Qué operaciones puedo hacer sobre los datos? 
  (- Discretos / Continuos)
  - Intervalo      SUMAS, RESTAS
    Es cuando en la escala de medición no hay un CERO ABSOLUTO.
         Temperatura en grados centígrados. El 0º es absoluto.
          - Si en Barcelona hay 20 grados
          - Madrid tiene 10 grados
         En Barcelona hay 10 grados más que en Madrid ? SI
         En Barcelona hay el doble de grados que en Madrid? NO

  - Razón          SUMAS, RESTAS, MULTIPLICACIONES, DIVISIONES
    Es cuando en la escala de medición hay un CERO ABSOLUTO, indica ausencia de la propiedad que mido.
        Eso implica que si FELIPE tiene 2 hijos y Menchu tiene 4:
        - Menchu tiene 2 hijos más que Felipe (RESTA)
        - Menchu tiene el doble de hijos que Felipe (DIVISIÓN)

CP: 19200 <- NOMINAL
NUMERO DE HIJOS QUE TIENE UNA FAMILIA: 0,1,2,3,4... hijo <- CUANTITATIVO DISCRETO RAZON


NOMINALES       Asigno un nombre a cada valor que mido. Me permite clasificar sujetos en grupos.

    Madrid
    Barcelona
    Bilbao

ORDINALES       Asigno un nombre a cada valor que mido, pero además, los valores tienen un orden.
                Me permiten: Clasificar sujetos en grupos y establecer un orden entre eso sujetos.

    Alto > Medio > Bajo

CUANTITATIVOS   Asigno un nombre a cada valor que mido, pero además, los valores tienen un orden y una distancia entre ellos.
                Me permiten: Clasificar sujetos en grupos, establecer un orden entre esos sujetos y establecer una distancia entre ellos.
                - Discretos: Valores enteros (número de hijos, número de coches, etc.)
                - Continuos: Valores con decimales (altura, peso, etc.)
    10 cm < 20 cm < 30 cm

Necesitamos claramente separar a nivel conceptual la naturaleza del dato desde el punto de vista informático (tipos de datos) y la forma en que mido el dato desde el punto de vista del análisis (tipos de datos estadísticos).

Un dato CUALITATIVO siempre por definición es un dato ORDINAL, que a su vez, siempre por definición es un dato NOMINAL. NUNCA AL REVES!
   CUALITATIVO > ORDINAL > NOMINAL

Otra cosa distinta es cómo lo guardo... y también es importante... no para el análisis... pero si para costes y rendimiento de los sistemas.

NUMERO DEL DNI! 1-8 números y una letra (A-Z)
Cómo lo guardo en una BBDD? Opciones:
- OPCIÓN 1: TEXTO (que ocupará? 9 caracteres)... pero en los HDD guardamos caracteres? o por una red transmitimos caracteres? NO! Guardamos bytes. 
  Cuánto ocupa 1 carácter en bytes? Depende el JUEGO de CARACTERES que usemos.
    - ASCII: 1 byte por carácter (pero podré representar como mucho 256 caracteres)
    - ISO 8859-1: 1 byte por carácter (pero podré representar como mucho 256 caracteres)
    - UTF-8: de 1 a 4 bytes por carácter
    - UTF-16: de 2 a 4 bytes por carácter
    - UTF-32: 4 bytes por carácter
  Esos 9 caracteres ocuparán 9 bytes en cualquier juego de caracteres con cierto sentido
- OPCIÓN 2: NUMERO + LETRA                                  <- 4 bytes + 1 bytes = 5 bytes
- OPCIÓN 3: Guardo solo el número.. la letra se calcula.    <- 4 bytes... eso si.. penalizamos luego CPU... para calcular la letra cuando haga falta

LA LETRA DEL DNI Es una huella (HASH) del número del DNI.

La U de UTF viene de UNICODE, que es un estándar que define un JUEGO DE CARACTERES (un conjunto de caracteres) y cómo representarlos en bytes.... contiene casi 150.000 caracteres diferentes.

                  INT_UNSIGNED    INT_SIGNED    CARACTER      OTRO JUEGO DE CARACTERES
1 byte
0000 0000            0             -128           A                a
0000 0001            1             -127           B                b
...
1111 1111          255              127


1 bytes guardo hasta 256 valores diferentes.
2 bytes guardo hasta 65.536 valores diferentes.
4 bytes guardo hasta 4.294.967.296 valores diferentes.

El hecho de declinarnos por guardar el Nº del DNI como Integer y no como String ha hecho que ocupe menos de la mitad 4/9= 44% 
Eso es relevante? CLARO QUE SI ...
Pero no solo por el coste de alcenamiento (que en si mismo ya lo justifica).
Si tengo que escribir el doble de datos en el disco.. tardaré el doble de tiempo.
Si tengo que transmitir el doble de datos por la red... tardaré el doble de tiempo.
Si tengo que comparar o buscar o subir a ram el doble de datos... tardaré el doble de tiempo.
Y eso para un campo... si tengo 20 campos así... flipas!
El cambiar la forma de almacenar un dato puede hacer que el rendimiento de mi sistema se dispare o se hunda.

---

El almacenamiento es hoy en día CARO o BARATO? LO MAS CARO CON DIFERENCIA EN UN ENTORNO DE PRODUCCIÓN.
Tenemos la sensación de que el almacenamiento hoy en día es barato...pero no es verdad.. o si.. depende de qué almacenamiento hablemos.

Si quiero un HDD para casa.. para guardar mis fotos del verano... me voy al MediaMark y compro un Wester Blue... de 3Tbs 

En una empresa necesito un disco que soporte funcionamiento 24x7... muchos días al año... 365(o 366)
Ese disco costará al menos x3 del otro... pudiendo llegar a un x20 en algunos casos.

Pero no queda ahí.
Cuántas copias hago de un dato en un entorno de producción? AL MENOS 3.
Eso implica que para tener esos 3 Tbs en la empresa, necesito 3x3tbs.. con cada disco a un x20 de los que me compré en el MediaMarkt.

Y ahora mete backups (Recuperación ante desastres)... multiplica x 3 x 2

Si empiezo a multiplicar... flipas... 1Tb x 3 x (3 x2 )... al final salen cifras astronómicas.

---


# Análisis de datos en BI

Desde el punto del análisis de datos, lo que hacemos es aplicar técnicas estadísticas descriptivas para analizar los datos y aportar información útil para la toma de decisiones.
La clave está en entender bien los datos que tengo... y su tipo de datos.

    NOMINAL          clasificar
    ORDINAL          clasificar + ordenar
    CUANTITATIVO     clasificar + ordenar + distancia

El problema es que tener datos y entender los datos no es lo mismo.
Yo puedo tener muchos datos.. pero eso no implica que los entienda.

Mi cerebro de nuevo no da... necesitamos RESUMIR LA INFORMACIÓN.

La forma más básica que nos ofrece la estadística para resumir la información es a través de tablas de frecuencias. Para montar una tabla de frecuencias que necesito? Poder clasificar los datos en grupos (clase o modalidad) y contar cuántos datos hay en cada grupo (frecuencia absoluta).

                                        (F. absoluta)  (F. relativa)  (F. ac. absoluta) (F. ac. relativa)
                                         Nº Personas    %                Fr. Acumulada   % Fr. Acumulada
    Otros                                  100         6.67                 100             6.67    
    Grado                                  800        53.33                 900            60.00
    Carrera universitaria superior         300        20.00                1200            80.00
    Master                                 200        13.33                1400            93.33
    Doctorado                              100         6.67                1500           100.00
    Total                                  1500       100%

Los valores acumulados, de nuevo, siempre puedo calcularlos, pero no siempre tienen sentido.
Solo tiene sentido si tengo los datos ordenados de alguna forma.

Cuidado, los podré tener ordenados por distintos criterios.
- Tenemos una variable ORDINAL (por ejemplo, el nivel de estudios) y la ordenamos por el nivel de estudios.
- Imaginad que tengo provincias... podría generar las frecuencias acumuladas por provincias?
  PROVINCIAS es NOMINAL... no me da ordenación intrínseca de los grupos. 
  Podría ordenarlos por otro concepto... Por ejemplo, las provincias que más volumen de negocio me generan.
  O las ordeno por frecuencia (de las que más hay)

Podría hacer lo mismo para la variable SALARIO QUE PAGAN EN EL BANCO? SI... pero no tendría sentido... cuanta filas iba a tener esa tabla... miles.. y si tiene miles... he resumido algo? NO... entonces pa' que!

 variable SALARIO > rango salarial (ORDINAL)

                            # de personas
    0-1000                     1000
    1001-2000                  2000
    2001-3000                  2500
    3001-4000                  4000
    Más de 4000                9000

Esas tablas ahora podría representarlas gráficamente:  BARRAS (absoluto.. relativo)/ SECTORES (relativo)

Para representar los datos de una variable, lo hacemos atendiendo a su tipo:

 - NOMINAL: BARRAS (absoluto.. relativo) / SECTORES (relativo)
 - ORDINAL: BARRAS (absoluto.. relativo) / SECTORES (relativo)
 - CUANTITATIVO: 
   - BARRAS (absoluto.. relativo) / SECTORES (relativo)??? Solo si tiene muy pocas modalidades y es discreta (enteros): Número de hijos: 0,1,2,3,4,5, 10, 25
   - HISTOGRAMA / BOXPLOT (Caja y bigote) (VIOLIN = HISTOGRAMA + BOXPLOT)

                                        (F. absoluta)  (F. relativa)  (F. ac. absoluta) (F. ac. relativa)
                                         Nº Personas    %                Fr. Acumulada   % Fr. Acumulada
    Otros                                  100         6.67                 100             6.67    
    Grado                                  800        53.33                 900            60.00
    Carrera universitaria superior         300        20.00                1200            80.00
    Master                                 200        13.33                1400            93.33
    Doctorado                              100         6.67                1500           100.00
    Total                                  1500       100%

    Frecuencia (Número de personas)
    ^
    |
    |
    |           X
    |           X
    |           X        x
    |    x      X        X        X        x
    +---------------------------------------------------------------- Nivel de estudios
        Otros  Grado  Carrera   Master  Doctorado
                universitaria superior



                            # de personas
    0-1000                     1000
    1001-2000                  4000
    2001-3000                  3000
    3001-4000                  1000
    4001-5000                     0
    5001-6000                   500

    Frecuencia (Número de personas)
    ^
    |
    |
    |
    |                  X
    |                  X          X
    |                  X          X
    |      X           X          X           X                        x  
    +----------------------------------------------------------------------> Salario
         0-1000   1001-2000   2001-3000   3001-4000   4001-5000   5001-6000

# La estadística nos da un nivel adicional de resumen de los datos.

Las tablas de frecuencias son una primera forma de resumir los datos, pero no es la única.

Pero luego puedo resumirlos aún más... aquí salen los estadísticos descriptivos univariables.

## Estadísticos de tendencia central

> BASICAMENTE NOS INFORMAN DE POR DONDE VAN LOS TIROS

- Moda          Valor que más se repite en una variable. Se entiende bien.
                Para calcularla necesito AGRUPAR LOS VALORES (lo cual implica poder clasificarlos)
                A qué tipos de datos puedo aplicarla? TODOS
- Mediana       Valor que divide en 2 partes iguales (o lo intenta) a la población. Se entiende bien.
                Para calcular la mediana necesito ORDENAR LOS VALORES
                A qué tipos de datos puedo aplicarla? ORDINALES y A CUANTITATIVOS
- Media         Es el más complejo de entender... porque no atiende a una definición humana... 
                Atiende a una fórmula matemática.
                MEDIA = SUMATORIA DE LOS VALORES / NÚMERO DE VALORES
                A qué tipos de datos puedo aplicarla? CUANTITATIVOS

RESUMEN. Si tengo un dato NOMINAL, damos la MODA.
         Si tengo un dato ORDINAL, doy la MODA y la MEDIANA.
         Si tengo un dato CUANTITATIVO, doy la MODA, la MEDIANA y la MEDIA.

### Para cuantitativos...

La moda nos da un poco igual.
Entre media y mediana cual nos interesa? Cuál es mejor? DEPENDE..
Cuál es el objetivo de estar haciendo esto? Ayudar a entender los datos.
Queremos un número que cuando alguien lo vea, le ayude a entender los datos.

La media... es muy peligrosa.. y en ocasiones mentirosa.

> Sease villarriba de arriba.

 10 vecinos... con sus coches... y esos coches contaminan... Y se ha estimado que echan:

  5 5 5 10 10 10 10 15 15 15 
    
    ^
    |                      X 
    |       X              X              X
    |       X              X              X
    |       X              X              X
    +----------------------------------------------------------------> Contaminación (grCO/dia)
         5 grCO/dia     10 grCO/dia     15 grCO/dia
                           ^
                        MEDIANA
                           ^
                         MEDIA

  MEDIA: 10 grCO/dia
  MEDIANA: 10 grCO/dia

> Sease villarriba de abajo.

 10 vecinos... con sus coches... y esos coches contaminan... 
 Pero los vecinos de abajo están más concienciados con el medio ambiente y se han puesto de acuerdo para comprar coches eléctricos que contaminan menos.

  5 5 5 5 5 5 5 5 5 1000

                                     ^
                                     |       x
                                     |       X
                                     |       X
                                     |       X
  x                                  |       X                                            x
<------------------------------------+-----------------------^----------------------------->  (grCO/dia)
  -955                                     5 grCO/dia          104,5                      1000 grCO/dia
                                             ^
   Gertru                                 MEDIANA                                        MANOLO
                                             ^
                                           MEDIA 

 SUMA: 1045 grCO/dia
 MEDIA: 1045/10 = 104,5 grCO/dia
 MEDIANA: 5 grCO/dia

Pregunta.. qué dato es más representativo del colectivo? Claramente la MEDIANA.
Si pusiéramos la MEDIA en un informe.. que pensaría quien lea el informe? ESTARÍA ENGAÑANDO (con o sin intención) a quien lo lee.

En estadística decimos que la MEDIA es un indicador SUFICIENTE, porque tiene en cuenta todos los datos al calcularla... y eso está guay... El problema es que la media es lo que llamamos un indicador NO ROBUSTO, porque se ve muy afectada por los valores extremos (outliers, como Manolo).

La MEDIANA por su parte no es un indicador SUFICIENTE, porque no tiene en cuenta todos los datos al calcularla (solo los que están en el medio), pero es un indicador ROBUSTO, porque no se ve afectada por los valores extremos (outliers).

Hay que decidir... Y usamos mucho el OJO DE BUEN CUBERO!
Si media y mediana son razonablemente parecidas, usamos la MEDIA.
Si son muy diferentes, usamos la MEDIANA.
Qué significa razonablemente parecidas? Pues lo que yo considere en mi negocio!

RESUMEN: USAREMOS MEDIA CUANDO TENGAMOS UNA DISTRIBUCION ASIMETRICA, la mediana será más representativa del colectivo, mientras que la media será igual de representativa que la mediana en una distribución simétrica... y en ese caso preferimos la media porque es un indicador suficiente.

En nuestro ejemplo lo que querríamos medir es el nivel de conciencia medioambiental de los vecinos, llego a ese dato mediante una medida INDIRECTA: la contaminación generada por sus coches.

Pensando yo que hay relación entre la conciencia medioambiental de los vecinos y la contaminación que generan sus coches.

Hay muchos datos que no podemos medir directamente... es más... hay muchos datos que ni siquiera somos capaces de definir... como para medirlos.

Por ejemplo: NIVEL DE SATISFACCIÓN DE MIS CLIENTES.
- Encuesta telefónica: Esta usted contento? TIENE RUIDO A KILOS !!!!
- Número de productos que tienen contratados
- Numero de incidencias que han abierto en el último año


MEDIA SALARIOS:      5.500€ (tenemos manolos.. los directivos...los consejeros...)
MEDIANA DE SALARIOS: 4.700€

Los estadísticos de tendencia central son unos... pero no los únicos.. es más NUNCA JAMAS EN LA VIDA BAJO PENA CAPITAL puedo dar un estadístico de tendencia central sin su estadístico de dispersión asociado.

> Ejemplos de alturas de portales

 PORTAL  NUMERO 0 ( 4 vecinos)
     165cm 165cm 185cm 185cm
  
     *MEDIA: 175cm
     MEDIANA: 175cm

     -10cm -10cm  10cm  10cm    MEDIA: 0
                                MEDIA ABS: 10 cm 
                                MEDIA CUADRADOS: 100 cm^2
                                RAIZ DE ESO: 10 cm >: DESVIACIÓN TÍPICA 

 PORTAL NUMERO 1 ( 4 vecinos)
     160cm 170cm 180cm 190cm
  
     *MEDIA: 175cm
     MEDIANA: 175cm

     -15cm -5cm  5cm  15cm    MEDIA: 0
                              MEDIA ABS: 10 cm >: DESVIACIÓN MEDIA ... ya no la usamos.
                              MEDIA CUADRADOS: 125 cm^2 VARIANZA (y tiene un problema... la ud. de medida... que no la entendemos)
                              RAIZ DE ESO: 11,18 cm >: DESVIACIÓN TÍPICA

 PORTAL NUMERO 2 ( 4 vecinos)
     160cm 160cm 190cm 190cm

     *MEDIA: 175cm
     MEDIANA: 175cm

     -15cm -15cm  15cm  15cm  MEDIA: 0
                              MEDIA ABS: 15 cm 
                              MEDIA CUADRADOS: 225 cm^2
                                RAIZ DE ESO: 15 cm >: DESVIACIÓN TÍPICA

 PORTAL NUMERO 3 ( 4 vecinos)
     175cm 175cm 175cm 175cm

    *MEDIA: 175cm
    MEDIANA: 175cm

        0cm 0cm 0cm 0cm        MEDIA: 0
                               MEDIA ABS: 0 cm
                               MEDIA CUADRADOS: 0 cm^2
                                 RAIZ DE ESO: 0 cm >: DESVIACIÓN TÍPICA

PORTAL NUMERO 4 ( 4 vecinos)
     165cm 175cm 175cm 185cm

     *MEDIA: 175cm
     MEDIANA: 175cm

       -10cm 0cm 0cm 10cm     MEDIA: 0
                              MEDIA ABS: 5 cm
                              MEDIA CUADRADOS: 25 cm^2
                                RAIZ DE ESO: 5 cm >: DESVIACIÓN TÍPICA

Como se interpreta esa desv. típica:
- Si tengo un salario medio de 2500€ con una desviación típica de 500€.
  ~~2000-3000 la gente gana entre eso ~~

La interpretación de la desv. típica nos la dió Chebyshev: REGLA DE CHEBYSHEV
Si abrimos un rango de una desv. típica alrededor de la media, siempre, con independencia del tipo de distribución, al menos el 50% de los datos estarán dentro de ese rango.... el 50% de los datos más centrados... la mayor parte de la población más representativa.

El 50%(al menos) de los datos más representativos estarán entre 2000€ y 3000€. Habrá gente de más de 3000€ y gente de menos de 2000€, pero la mayoría de la gente estará entre esos valores.

CUIDADO... la desv. típica se basa en la media... y si la media no es representativa del colectivo, la desv. típica tampoco lo será. Y NO LA CALCULO.

## Estadísticos de dispersión

> BASICAMENTE NOS INFORMAN DE CUANTO CAMBIAN LAS COSAS CON RESPECTO AL POR DONDE VAN LOS TIROS

Si uso la media como indicador de por donde van los tiros, usaré la desviación típica como indicador de cuánto cambian las cosas con respecto a ese por donde van los tiros.

Si uso la mediana como indicador de por donde van los tiros, usaré el rango semi-intercuartílico como indicador de cuánto cambian las cosas con respecto a ese por donde van los tiros.

---

### Medidas de posición

- Percentiles     Dividen la población en 100 partes iguales. El percentil 50 es la mediana.
- Cuartiles       Dividen la población en 4 partes iguales. El cuartil 2 es la mediana.
- Deciles         Dividen la población en 10 partes iguales. El decil 5 es la mediana.
Los valores que dejan por debajo a un determinado porcentaje de la población.

   1 2 4 4 6 6 6 7 9 10
     
     El 2 sería el percentil 20, decil 2
     El 9 sería el percentil 90, decil 9
     El 6 sería el percentil 70, cuartil 7

Los percentiles dividen la población en 100 partes iguales
Los deciles en 10 partes iguales
Los cuartiles en 4 partes iguales

Hay una medida de posición adicional que ya os había presentado... aunque no la habíamos llamado así.
LA MEDIANA: Valor que deja por debajo al 50% de la población.

MEDIANA = Q2 = D5 = P50

Cuántos cuartiles hay?  3 partes... dividen en 4 al colectivo.

    |----|----|----|----|
         Q1  Q2   Q3
            MEDIANA

Rango intercuartílico: Q3 - Q1. En ese rango el 50% de los datos más representativos del colectivo.
Rango semi-intercuartílico: (Q3 - Q1) / 2.
Conceptualmente, si abrimos un rango semi-intercuartílico alrededor de la mediana, tendremos entorno al 50% de los datos más representativos del colectivo dentro de ese rango. Es una interpretación similar a la que hacíamos con la desviación típica.

          BOXPLOT

    -----------------------------------------------------------------------------> Valor de la variable

                           
  <-----1.5RIC--------><----RIC-------><-----1.5RIC--------><-----1.5RIC-------->

          |            +---------+----+                    |
          +------------+      o  |    +--------------------+    ···                  o o
          |            +---------+----+                    |
                                                                 Valores atípicos
          ^            ^         ^    ^                    ^                          Valores atípicos extremos
         MIN           Q1       Q2    Q3                  MAX
     "razonable"              MEDIANA                  "razonable"


    o = MEDIA

Esa es la formula que habitualmente usamos para identificar valores atípicos (outliers) y extremos (extreme outliers).
- MEDIANA: Valores inferiores al Q1-1.5RI
           Valores superiores al Q3+1.5RI
- MEDIA:   2*DESVIACIÓN TÍPICA (3SIGMA ... valores atípicos extremos)
           Valores inferiores a MEDIA - 2*DESVIACIÓN TÍPICA
           Valores superiores a MEDIA + 2*DESVIACIÓN TÍPICA

# Una vez hecho un análisis de una variable, empezamos a juntar variables...

Y empezamos juntando 2 a 2 las variables.
Buscamos relaciones entre variable. CORRELACIONES.

## NOMINAL x NOMINAL

1. Tabla de contingencia

Más o menos lo mismo que una tabla de frecuencias... pero con 2 variables... que las repartimos entre filas y columnas.

                       50%      50%
                SEXO: Hombre / Mujer
            BUS        25        25
            TREN      105        95
            TIENDA     45        55
            MEDICO     30        70

Esa es nuestra tabla de contingencia.
La puedo representar gráficamente? BARRAS APILADAS / BARRAS AGRUPADAS

Nuestro objetivo es identificar si hay relaciones entre las variables.
ESO QUE SIGNIFICA? Si hay relación entre ubicación y sexo.
Lo que buscamos son valores que descuadren... que no nos encajen con lo que esperamos (a priori).. que me escamen!


                VALORES ESPERADOS (a priori)          VALORES REALES (observados)

                       50%      50% 
                SEXO: Hombre / Mujer   Total         Hombre / Mujer
            BUS         25      25       50            19      31   ENCAJA...
            TREN       100     100      200           110      90   ENCAJA...
            TIENDA      15      15       30            17      13   ENCAJA...
            MEDICO      30      30       60             1      29   NO ENCAJA... EIN!!!!! QUA PASAO!!!!
            (ginecólogo)

            Eso es lo que identifica la estadística... casos que no encajan con lo que esperamos.
            Qué significa aquello? NPI... la estadística no nos dice nada de eso.
            Eso lo analizaré a posteriori.
            Lo que pasa.. es que encaja porque HAY UNA RELACIÓN entre ESTAR EN EL GINECÓLOGO y EL SEXO < EXPLICACIÓN!
            El problema es como estandarizar esto! Donde pongo el corte entre lo que me encaja y lo que no me encaja.
            Sobre todo para que si somos muchos, todos los hagamos igual.   NO QUIERO UN CRITERIO SUBJETIVO.

    Chi-cuadrado es un estadístico que vale entre 0.. e infinito. que me "cuantifica" la relación entre dos variables cualitativas (nominales y ordinales). Tiene un problema chi-cuadrado... como no hay valor superior límite.. no se cómo interpretarlo.

    Lo que tenemos luego en estadística son otros estadísticos que se calculan desde el chi-cuadrado y que tienen un valor entre 0 y 1, que me indican la fuerza de la relación entre las variables cualitativas.

      - V de Cramer: Entre 0 y 1. Cuanto más cerca de 1, más fuerte es la relación entre las variables cualitativas.
      - Phi: Entre 0 y 1. Cuanto más cerca de 1, más fuerte es la relación entre las variables cualitativas.
      - Coeficiente de contingencia: Entre 0 y 1. Cuanto más cerca de 1, más fuerte es la relación entre las variables cualitativas.

      Dan valores muy similares.


## NOMINAL x ORDINAL

De entrada puedo hacer lo mismo de arriba (NOMINAL x NOMINAL).
Lo que pasa es que ahora tengo una variable además que tiene un orden.... y entonces puedo hacer algo adicional.

A una variable ORDINAL que le puedo calcular? La mediana.
Y podría clasificar los sujetos en base a la variable nominal y para cada subgrupo calcular la mediana de la variable ordinal.
HACER UN ESTUDIO DE COMPARACIÓN DE MEDIANAS.

    Provincia   |  Mediana nivel de estudios
    Madrid      |  Grado
    Cuenca      |  Master

Hay relación entre la provincia y el nivel de estudios? Parece que la gente de Cuenca tiene un nivel de estudios más alto que la gente de Madrid.

## NOMINAL x CUANTITATIVO

De entrada puedo hacer lo mismo que en las anteriores:
- NOMINAL x NOMINAL (tabla de contingencia + estadísticos de asociación chi-cuadrado, V de Cramer, Phi, Coeficiente de contingencia)
- Estudio de comparación de medianas.
- Estudio de comparación de medias (siempre y cuando la media sea representativa del colectivo).

    Provincia   |  Media salario
    Madrid      |  2.500€
    Cuenca      |  3.000€

Podría pintar un gráfico para visualizar esto?
Podría hacer un histograma o un boxplot por cada grupo de la variable nominal.
- Pirámide poblacional (si la variable es dicotómica: NOMINAL con 2 modalidades)
- Boxplot múltiple

## ORDINAL x ORDINAL

Va a ser el mismo caso que NOMINAL x ORDINAL.... pero decidiendo cuál quiero tratar como nominal y cuál ordinal.
- NOMINAL x NOMINAL
- ESTUDIO DE COMPARACIÓN DE MEDIANAS (de una variable en base a los grupos de la otra o al revés)

## ORDINAL x CUANTITATIVO

Igual que si es NOMINAL x CUANTITATIVO... 
Adicionalmente podríamos calcular un coef. de correlación de Spearman.

## CUANTITATIVO x CUANTITATIVO

Gráfico? Diagrama de dispersión / nube de puntos

Cada O es un sujeto que analizamos.
Qué buscamos observar? TENDENCIAS DE EVOLUCIÓN CONJUNTA entre las dos variables.

Hay relación entre edad y altura? DEPENDE... del colectivo de estudio. 

                        PERSONAS ENTRE 0 y 15 años

 Variable 1. ALTURA
   ^
   |
   |                         OO OO   O
   |                      O  O
   |                  O    O O
   |               O     O
   |         O    O
   |    O O
   |
   +-------------------------------------------------------------------------> Variable 2 EDAD
        A más edad, más altura.
        A menos edad, menos altura.
        A menos altura, menos edad.
        A más altura, más edad.
        Y además de forma lineal... tienden a una linea recta

                        PERSONAS ENTRE 30 y 50 años

 Variable 1. ALTURA
   ^
200|                                O                               O
   | O
   |        O
   |        O           O                       O               O
   |
   |               O                        O               O
   |    
   |            O               O                   O
   | O              O                   O                       O
150|
   +-------------------------------------------------------------------------> Variable 2 EDAD
 No voy a ver ninguna tendencia clara entre las dos variables.

                        PERSONAS ENTRE 65 y 80 años

 Variable 1. ALTURA
   ^
200|    O   O     O
   |      O   O   O     O     O
150|     O   O   O     O     O    O
   |                                            O     O   O
   |                   o                                O    O
   |
   |
   |
   +-------------------------------------------------------------------------> Variable 2 EDAD
 
 Hay cierta tendencia... a que a más edad, menos altura. No una tendencia muy marcada, pero sí cierta tendencia.

 Las tendencias son tendencias.. y se cuantifican.

 Si esta año está de moda llevar el color rojo en la ropa, eso significa que todo el mundo vista de rojo todos los días? NO
 Solo significa que veo más rojo del esperaría encontrar... Me escama! Me llama la atención.

 Si el año que viene se pone de moda llevar el color verde en la ropa, eso significa que todo el mundo vista de verde todos los días? NO
 Encontraré el mismo % de gente vistiendo de verde que este año vistiendo de rojo? NO TIENE POR QUE

 Quizás este año, ha pegado el color rojo... pero la gente no se ha vuelto loca tampoco.
 Pero a lo mejor el año que viene nos volvemos locos y nos convertimos todos en lechuga! HA PEGADO MUCHO!

 Hay un coeficiente en estadística que nos mide la fuerza de la relación entre dos variables cuantitativas.
 Coeficiente de correlación de Pearson: -1 y 1.
   El signo significa la dirección de la relación:
      Si es positivo, a más de una, más de la otra.
      Si es negativo, a más de una, menos de la otra.
   El valor absoluto significa la fuerza de la relación:
    Si tiende a 1, la relación es muy fuerte.
    Si tiende a 0, la relación es muy débil.
    Si es 1 = RUINA! Es que es la misma variable... que a lo mejor la estoy midiendo de 2 formas:
        Peso kgs... peso en gramos-> Correlación 1... pero es que es la misma variable.

Soy un banco... y apruebo o no hipotecas... Me importa equivocarme? ALGO ME IMPORTA.. pero poco!
Aquí estamos tomando decisiones en base a estadísticas.
LO REALMENTE IMPORTANTE ES QUE SEA CAPAZ DE TASAR EL % DE ERRORES QUE VOY A TENER.
Si sé que me voy a equivocar en 3 de cada 50 personas... el gasto que me ocasionan esas 3 personas lo reparto entre las 47 personas que no me han ocasionado gasto.(le subo el precio) y sigo ganando!

Más de esto es complicado para un humano.

# Podemos en algunos casos juntar 2 cuantitativas x 1 nominal.

Lo podemos ver en un gráfico:
 Nube de puntos con colores


Imaginad 3 variables nominales.
Qué es lo que hace una variable nominal? AGRUPAR / GRUPOS

Tengo 3.
Provincias, Sexo, Color de pelo.
47           2      6 (rubio, pelirrojo, castaño, moreno, canoso, calvo)
47x2x6 = 564 grupos.
Voy a ser capaz de entre 564 grupos que vea en un gráfico saber cual es el que me escama? el que no encaja? Ni de coña.

En estos casos... lo único que podemos hacer es estudios por separado de 2 variables, filtrando previamente por la tercera variable.

Nos saldrán muchos filtros.

---

Hay una variable CUANTITATIVA que en la mayor parte (95%) de los estudios BI nos va a salir... y que manda! TIEMPO/FECHA

La fecha es una variable cuantitativa? SI.... de INTERVALO... no hay 0 absoluto.
PUEDO RESTAR FECHAS -> días!
Puedo decir que una fecha es el doble que la otra? NO

Las cosas cambian con el tiempo.. de eso va todo esto!

---
Adicionalmente en BI usamos mucho el concepto de KPI (Key Performance Indicator) o Indicador Clave de Rendimiento.
Que no es sino un estadístico + un objetivo.
---

# Almacenes de datos

BBDD                        Es donde tenemos los datos que se van cocinando en la empresa.
                            Suelen contener información VIVA.
  vvv
  ETL                       Programa (script) de extracción, transformación y carga de datos.
                            - Online Transaction Processing (OLTP)
                            - Offline (Modo batch)
                            Variantes:
                            - ETL
                            - ELT
                            - TELT
                            - ETLT
                            - ... 
  vvv                          
Datalake                    Recopilar información en crudo... Sin procesar. Tal y como está en origen
  vvv
  ETL
  VVV
Datawarehouse               Repositorio de información, donde la información ya ha sido procesada para un uso
                            concreto (BI, minería de datos, etc.)
                            En el mundo de BI, estos repositorios suelen tener una forma muy concreta de crearse. Modelos en estrella (o snowflake)... basados en tablas de hechos y dimensiones.
   VVV
Business Intelligence       Aplicar técnicas de estadística descriptiva (inferencial) para analizar los datos
                            y aportar información útil para la toma de decisiones:
                            - Generar tablas de frecuencias (y pintarlas)
                            - Generar estadísticas descriptivos univariables (media, mediana, moda, desviación típica, etc.)
                            - Juntar variables (análisis de correlaciones). Generar algunas tablas.. pintarlas, generar estadísticas para más de 1 variable.
                            - BI... llega hasta un análisis juntando no más de 2/3 variables.
                            - No por limitaciones de BI... por limitaciones de nuestro cerebro humano.
   VVV
Data Mining                 Buscar relaciones más complejas entre datos (relaciones no evidentes)
                            Aquí juntamos muchas variables... y le dejamos a la computadora que encuentre relaciones.
   vvvv 
Machine Learning            Lo que hacemos es pedir a la computadora (nosotros de nuevo somos demasiado
                            cortitos para hacer esto con nuestros medios): 
                            - Predecir
                            - Clasificar
                            - Agrupar
                            (- Generar)
    >>  Deep Learning       Redes neuronales multicapa.


BigData                     Simplemente es cuando tenemos que trabajar con:
                            - Un volumen de datos tan grande
                            - Datos tan complejos
                            - Datos que se van generando tan rápido
                            que las formas tradicionales de lidiar con ellos ya no me sirven.

                            Trabajar?
                            - Almacenar o no!
                            - Analizar datos o no!
                            - Transmitir datos o no!
    
                            El enfoque bigdata implica trabajar con una GRANJA de computadoras de mierda (commodity hardware) y los pongo a trabajar como si fueran una sola máquina.
                            Lo primero que necesito es una especie de SO que me permita trabajar con todas esas máquinas como si fueran una sola. Repartir la carga de trabajo entre todas las CPUs de la granja (igual que un SO reparte la carga de trabajo entre las CPUs de una única máquina). HAcer uso de la RAM de todas las máquinas como si fuera una sola RAM. Hacer uso del disco de todas las máquinas como si fuera un único disco.
                            - HADOOP <- Es el equivalente a un SO para una granja Bigdata.

    CLASH ROYALE 2v2
     En un segundo, una persona puede hacer 2 movimientos en el juego.
     Y las otras 3 personas se deben enterar.
     Eso implica que de alguna forma, se han generado 6 mensajes/segundo que se transmiten a los contrincantes.
     Pero somos 4 jugando -> 24 mensajes/segundo.
     En un momento puede haber 50.000 partidas en marcha.
     24 * 50.000 = 1.200.000 mensajes/segundo.  NO HAY MÁQUINA QUE LO MANEJE.
     - Quiero almacenar esos datos? no
     - Los quiero analizar? no
     - Los quiero transmitir? sí                ESTA ES LA NECESIDAD


* Las formas tradicionales de lidiar con ellos ya no me sirven:
No es que haya una linea que digamos a partir de aquí es BigData.

- Tengo un USB (pincho) de 16Gbs... nuevito, recién sacado de la caja.
  Quiero guardar un archivo que tengo de 5Gbs... puedo? DEPENDE del sistema de archivos (FORMATO) que tenga el USB. Si tengo FAT16/32 no.. el tamaño máximo de archivo es 4Gbs.
  No pasa nada... hay otros formatos: NTFS, exFAT, zfs, etc. Pero incluso esos tienen un límite.
  Qué pasa cuando quiero guardar u archivo de 3Pbs... qué sistema de archivos uso?
- Quiero hacer la lista de la compra: PRODUCTO x CANTIDAD
      - 100 productos - EXCEL
      - 100.000 productos - EXCEL (se hace kkita) -> MYSQL
      - 10.000.000 productos - MYSQL (se hace kkita) -> MS SQL SERVER
      - 1.000.000.000 productos - MS SQL SERVER (se hace kkita) -> ORACLE
      - Y si tengo más???? qué hago ahora... 