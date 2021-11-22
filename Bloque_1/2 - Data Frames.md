# Introducción a los Dataframes en R
***
Un dataframe es un objeto R que almacena datos tabulares en una estructura de tabla formada por filas y columnas. Puede pensar en un dataframe como una hoja de cálculo o como una tabla SQL. Si bien los dataframe se pueden crear en R, generalmente se importan con datos de un CSV, una hoja de cálculo de Excel o una consulta SQL.

Algunas de las librerias principales para la manipulacion de dataframe son readr y dplyr.
```r
# load libraries
library(readr)
library(dplyr)
```
El contenido los datos se guardan en una variable como se muestra a continuacion.
```r
# load data frame
artists <- read_csv('artists.csv')
```

## CSVs
***
Cuando trabaje con marcos de datos, la mayoría de las veces cargará datos de un conjunto de datos existente. Uno de los formatos más comunes para grandes conjuntos de datos es el CSV.

La primera fila de un CSV contiene encabezados de columna. Todas las filas posteriores contienen valores. Cada encabezado de columna y cada variable están separados por una coma:
```r
name,cake_flavor,frosting_flavor,topping
Red Velvet Cake,chocolate,cream cheese,strawberries
Birthday Cake,vanilla,vanilla,rainbow sprinkles
Carrot Cake,carrot,cream cheese,almonds
```

## Cargar y guardar archivos CSV
Cuando tienes datos en un CSV, puedes cargarlos en un dataframe en R usando la función read_csv () de readr:
```r
df <- read_csv('my_csv_file.csv')
```
También puede guardar datos de un dataframe en un CSV usando la función write_csv () de readr:
```r
write_csv(df,'new_csv_file.csv')
```

## Ejercicio
***
```r
# load libraries
library(readr)
library(dplyr)

# load data frame
artists <- read_csv('artists.csv')
artists
```

## Inspección de dataframes
***
Si el marco de datos es pequeño, puedes mostrarlo escribiendo su nombre df. Si el marco de datos es más grande, puede ser útil inspeccionar unas pocas filas del marco de datos sin tener que mirar el resto.

La función head () devuelve las primeras 6 filas de un dataframe. Si desea ver más filas, puede pasar un argumento adicional n a head (). Por ejemplo, head (df, 8) mostrará las primeras 8 filas.
```r
# inspect data frame
artists
head(artists)
summary(artists)
```

## Piping
***
El operador de piping, o %>%, ayuda a aumentar la legibilidad del código del marco de datos canalizando el valor a su izquierda en el primer argumento de la función que le sigue. Por ejemplo:
```r
df %>%
  head()
```
Canaliza el dataframe df al primer argumento de head (), convirtiéndose en:
```r
head(df)
```

## Seleccionar columnas
***
Puede seleccionar las columnas adecuadas para su análisis utilizando la función select () de dplyr:
```r
select(customers,age,gender)
```
Puede simplificar la legibilidad de su código utilizando la pipe:
```r
customers %>%
  select(age,gender)
```

## Ejercicio
***
- Seleccione la columna de grupo de artistas usando select () y guarde el resultado en artist_groups.
- Seleccione el grupo, spotify_monthly_listeners y las columnas year_founded de artistas usando select () y guarde el resultado en group_info.
```r
# select multiple columns

artist_groups <- select(artists, group)
artist_groups 

group_info <- select(artists, group,spotify_monthly_listeners,year_founded)
group_info
```

## Exclusión de columnas
***
A veces, en lugar de especificar qué columnas desea seleccionar de un marco de datos, es más fácil indicar qué columnas no desea seleccionar. La función select () de dplyr también le permite hacer precisamente eso.

Las columnas a eliminar son seleccionadas con un -, se dan como argumentos.
```r
customers %>%
  select(-name,-phone)
```

## Ejercicio
***
Selecciona todas las columnas de artistas excepto los álbumes usando select() y guarda el resultado en no_albums.
```r
# select all columns except one
 
no_albums <- select(artists,-albums)
no_albums
```
Seleccione todas las columnas de artistas excepto genre, spotify_monthly_listeners y year_founded usando select () y guarde el resultado en df_cols_removed.
```r
# select all columns except a set

df_cols_removed <- select(artists,-genre,-spotify_monthly_listeners,-year_founded)
df_cols_removed
```

## Filtrar filas con Logic I
***
Además de subdividir un marco de datos por columnas, también puede dividir un marco de datos en filas utilizando la función filter () de dplyr y los operadores de comparación.

Supongamos que desea buscar todos los pedidos realizados por clientes con el nombre "Joyce".
```r
orders %>%
  filter(first_name == 'Joyce')
```
Tambien es posible filtrar con multiples condiciones.
```r
orders %>%
  filter(shoe_material == 'faux-leather',price > 25)
```

## Ejercicio
***
Filtra las filas de artistas donde el género es 'Rock' y guarda el resultado en rock_groups. Ver rock_groups.
```r
# filter rows one condition 
rock_groups <- filter(artists,genre == 'Rock')
rock_groups
```
Filtra las filas de artistas donde el género es 'Rock' y spotify_monthly_listeners es mayor que 20000000. Guarda el resultado en popular_rock_groups y visualízalo.
```r
# filter rows multiple conditions
popular_rock_groups <- filter(artists,genre == 'Rock',spotify_monthly_listeners > 20000000 )
popular_rock_groups
```

## Filtrar filas con Logic II
***
La función filter () también permite un filtrado más complejo con la ayuda de operadores lógicos.

Está interesado en ver todos los pedidos de 'obstrucciones' O que cuestan menos de 20. Con el operador o  " | ":
```r
orders %>%
  filter(shoe_type == 'clogs' | price < 20)
```
¿Qué sucede si desea encontrar todos los pedidos en los que se compraron zapatos en cualquier color excepto el rojo? Usando el operador not o bang (!):
```r
orders %>%
  filter(!(shoe_color == red))
```

## Organizar filas
***
Para ordenar a los clientes en orden ascendente por nombre:
```r
customers %>%
  arrange(name)
```
arrange() también puede ordenar filas por orden descendente! Para ordenar los clientes en orden descendente por edad:
```r
customers %>%
  arrange(desc(age))
```

## Ejercicio
***
Organice las filas de artistas en orden ascendente por grupo. Guarde el resultado en group_asc y véalo.
```r
# arrange rows in ascending order
group_asc <- arrange(artists,group)
group_asc
```
Organiza las filas de artistas en orden descendente por youtube_subscribers. Guarde el resultado en youtube_desc y véalo.
```r
# arrange rows in descending order
youtube_desc <- arrange(artists,desc(youtube_subscribers))
youtube_desc
```