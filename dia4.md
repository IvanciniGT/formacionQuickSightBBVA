---
Filtros / Parámetros
Publicar un análisis -> Paneles
Seguridad (Proteger datos)
 - En principio, los conjuntos de datos, análisis y paneles que vamos definiendo en QuickSight son de uso privado. PARA MI! Lo que podemos hacer es compartirlos con otros usuarios:
    - Podemos compartir un conjunto de datos:
      - Lo puedo compartir para su edición        (EDITAR)     - Propietario
      - Lo puedo compartir para su visualización  (VISUALIZAR) - Espectador
        En este caso, lo que posibilita es que el usuario pueda crear sus propios análisis a partir de ese conjunto de datos, o que puedan usar los datos de ese conjunto de datos para enriquecer los datos de otros conjuntos de datos que estén creando otros usuarios.
    - Podemos compartir un análisis               (VISUALIZAR o EDITAR)
    - Podemos compartir un panel                  (VISUALIZAR)
    El problema de eso es que o comparto todo o no comparto nada.
    En muchas ocasiones lo que va a pasar es que quiero compartir.. pero solo parte de los datos.
    Lo primero que necesito siempre es compartir conjunto de datos / análisis / panel.
    Pero luego ... puedo refinar la compartición:
     -  Compartir solo ciertas columnas de datos                    <<<<< MUY FACIL
     -  Compartir solo ciertas filas de los conjuntos de datos.     <<<<< MAS COMPLEJO
    Cualquiera de esos 2 aplica en cascada:
    - Si he compartido de un conjunto de datos solo ciertas columnas de datos... cuando esté en un análisis/panel, donde se use ese conjunto de datos solo podrá ver las columnas que haya compartido a ESE usuario.
      Los elementos visuales (tablas, gráficos, etc..) que usaran información de esas otras columnas que no se han compartido, aparecerá vacías.
    La compartición de filas se puede hacer de 2 formas:
       - Mediante ficheros de datos donde explicitemos qué filas son accesibles por cada usuario / grupo.
             ^^ MAS SIMPLE                                      Esto es menos mantenible en el tiempo
                                                                Implica más trabajo cuando hay cambios 
       - Mediante etiquetas en una BBDD externa de usuarios.
             ^^ MUCHO MAS COMPLEJO                              Esto es más mantenible en el tiempo
Importar datos de otras fuentes
---

# Restringir columnas

En nuestro caso, tenemos 5 columnas:
- Ventas Global
- Ventas EU
- Ventas NA
- Ventas JP
- Ventas Otros

Puedo decidir a qué usuarios / grupos les permito el acceso a cada columna.

# Restringir filas

1. Opción 1: Introduciendo una tabla (mediante BBDD... fichero EXCEL) con los usuarios/grupos y a que VALORES CONCRETOS de COLUMNAS CONCRETAS PUEDEN ACCEDER <- RULES DATASET

2. Opción 2: Mediante etiquetas en una BBDD externa de usuarios.


Las empresas suelen tener una herramienta para registrar a todos los usuarios de la empresa... con su contraseña y otros metadatos (email, teléfono... y MÁS!)

Puedo pedirle a QuickSight que cuando un usuario quiera acceder a un panel, y necesite autenticarle, que esa operación la delegue a esa herramienta de la empresa (MS Active Directory, Directorio LDAP, Keycloak, Oracle Identity, etc..)


---

# SEGURIDAD

- Identificar           Decir quien soy
- Autenticar            Asegurarme que eres quien dices ser (ESTA ES LA OPERACIÓN QUE QUICK SIGHT PUEDE DELEGAR EN OTRA HERRAMIENTA)
- Autorizar             Sabiendo que eres quien dices ser, ver si puedes hacer algo.
                        Esta parte la gestiona QuickSight.
                        Hay herramientas que esta parte también la delegan a esas otras herramientas de la empresa. No es el caso de QuickSight.

    Autorización:
    - ROLE del usuario: Autor, Administrador
    - Compartición (Si un usuario puede acceder a un conjunto de datos, análisis o panel) o no
    - Restricciones a nivel de fila / columna
      - En el caso de filas, lo que hace QuickSight es aplicar reglas de seguridad a nivel de fila (RLS) para determinar si un usuario puede acceder a una fila concreta del conjunto de datos o no.
      - El tema es que hay 2 formas de suministrar a QS esas reglas:
        - Mediante el fichero / Tabla de datos con UserName (+ GroupName) + Valores concretos de columnas concretasa los que puede acceder.
        - Mediante etiquetas que le son suministradas por la herramienta de autenticación de la empresa (AD, LDAP, etc..)


Cuando a QuickSight quiere acceder un usuario, si tengo habilitado la autenticación delegada, QuickSight le pide a la herramienta de autenticación de la empresa que le autentique al usuario.
En ese proceso de autenticación, la herramienta de autenticación le devuelve a QuickSight el nombre del usuario, su email, y el resto de metadatos que tenga configurado ese usuario en la herramienta de autenticación.

Igual que un usuario puede tener:
- Telefono
- Email
- Región
- Plataformas que administra=PLAT1;PLAT2 (MENCHU)
- Plataformas que administra=PLAT4       (FEDERICO)

Esos metadatos son entregados por la herramienta de autenticación a QuickSight.

Basándose en esos metadatos, QuickSight puede aplicar las reglas de seguridad a nivel de fila (RLS) para determinar si un usuario puede acceder a una fila concreta del conjunto de datos o no.
- En este caso, las reglas (YO, que soy quien defino quién tiene acceso a mis datos) de quién puede acceder a qué filas, las defino en base a esas etiquetas (los metadatos) que entrega la herramienta de autenticación de la empresa a QuickSight.

---

# Parámetros

Son constantes que podemos definir con un valor, y que una vez definidas podemos usar en nuestras fórmulas, filtros...
La idea es definir un dato una sola vez, y poderlo re-usar en diferentes partes del análisis.
Y si el día de mañana queremos cambiar el valor, lo haremos en un solo sitio y se actualizará en todas partes.

> Podríamos haber sacado un informe de ventas de juegos del último año o de los últimos 3 meses.

FILTRO: Toma la fecha actual y réstale 3 meses.
                                       ^

> Queremos identificar en una tabla los juegos que con respecto al año anterior han tenido un aumento del número de ventas superior al 25%

> Aplicado a un conjunto de datos. Quiero traerme datos de una BBDD... y lo hago con una query SQL:
```sql
SELECT * FROM ventas WHERE ...  AND campo > 7

```

Ese 7 lo podemos definir como un parámetro, y luego usarlo en la query:
```sql
SELECT * FROM ventas WHERE ...  AND campo > {{ parametro }}
```

---


    <iframe
        width="960"
        height="720"
        src="https://us-east-1.quicksight.aws.amazon.com/sn/embed/share/accounts/820634527231/dashboards/fb3fa240-f22f-49c8-aac8-e197fb15d415?directory_alias=Formacion">
    </iframe>

---

La peor (en términos de rendimiento) operación CON DIFERENCIA que puedo pedir a una BBDD es ORDER BY.

Qué tal se le da a un ordenador ORDENAR datos? FATAL! 
Es lo peor.

Una operación que exige previamente hacer un ORDER BY es el JOIN (hay distintas estrategias que usan las bases de datos para resolver el JOIN: NestedLoop)

Hay muchas operaciones en BBDD que implicitamente realizan un ORDER BY:
- GROUP BY
- DISTINCT <- ORDER BY por todos los campos de la query
- UNION <- DISTINCT