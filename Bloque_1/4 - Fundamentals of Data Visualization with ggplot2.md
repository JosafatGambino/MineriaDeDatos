# Fundamentos de la visualización de datos con ggplot2
***
El paquete ggplot2 es parte de tidyverse, por lo que viene equipado con otras herramientas de procesamiento y limpieza de datos. El paquete está diseñado teniendo en cuenta la gramática de los gráficos. Esta gramática de gráficos describe un patrón general a seguir al crear una visualización. De hecho, de ahí viene el "gg" en ggplot: gramática de gráficos. ggplot2 ha fomentado una gran comunidad de programación, por lo que descubrirá que, a medida que se esfuerza por crear su propia trama fuera de la plataforma Codecademy, habrá muchos recursos y ejemplos para darle la bienvenida.

Esta lección le enseñará la gramática básica necesaria para crear una trama. Después de aprender la estructura subyacente o la "filosofía" de ggplot2, puede ampliar la lógica para crear muchos tipos de gráficos. Una vez que obtenga la estructura básica, nuestras próximas lecciones explorarán cómo personalizar su gráfico y calcular estadísticas en su visualización.

## Capas y Geoms
***
Las unidades básicas de la "gramática de los gráficos" consisten en:

- Los datos o la información real que desea visualizar.
- Las geometrías, abreviadas como "geoms", describen las formas que representan nuestros datos. Ya sean puntos en un diagrama de dispersión, gráficos de barras en el gráfico o una línea para trazar los datos. La lista continua. Las geoms son las formas que "mapean" nuestros datos.
- La aesthetics o los atributos visuales de la trama, incluidas las escalas de los ejes, el color, el relleno y otros atributos relacionados con la apariencia.

Ejemplo de grafico:
```r
# load libraries and data
library(readr)
library(dplyr)
library(ggplot2)
movies <- read_csv("imdb.csv")
```

```r
# Observe layers being added with the + sign
viz <- ggplot(data=movies, aes(x=imdbRating, y=nrOfWins)) +
       geom_point(aes(color=nrOfGenre), alpha=0.5) + 
       labs(title="Movie Ratings Vs Award Wins", subtitle="From IMDB dataset", y="Number of Award Wins", x="Move Rating", color = "Number of Genre")


# Prints the plot
viz
```

## La función ggplot()
***
Lo primero que debe hacer para crear un objeto ggplot es invocar la función ggplot (). Conceptualice este paso como inicializar el "lienzo" de la visualización. En este paso, también es estándar asociar el dataframe que el resto de la visualización usará con el lienzo.

Aquí invocamos ggplot () para crear un objeto ggplot y asignar el dataframe df, guardándolo dentro de una variable llamada viz:
```r
viz <- ggplot(data=df)
 
viz
```

## Asociación de los datos
***
- Los datos están vinculados a una visualización ggplot2 pasando un dataframe como primer argumento en la llamada a la función ggplot(). Puede incluir el argumento nombrado como ggplot(data = df_variable) o simplemente pasar el dataframe como ggplot (dataframe).

- Debido a que los datos están vinculados en este paso, esto significa que el resto de nuestras capas, que son llamadas a funciones que agregamos con un signo +, todas tienen acceso al marco de datos y pueden usar los nombres de las columnas como variables.

```r
viz <- ggplot(data=sales) + 
       geom_point(aes(x=cost, y=profit))
viz # renders plot
```

## Ejercicio
***
Cree una nueva variable llamada viz y asígnele el valor de un nuevo objeto ggplot que cree invocando la llamada ggplot() y asignándole las películas del dataframe como argumento de datos.
```r
#Define variable and print it
viz <- ggplot(data=movies)
  viz
```

## ¿Qué son los aesthetics?
***
En la visualización que crearemos, queremos trazar las calificaciones de la película (imdbRating) en el eje xy el número de premios (nrOfWins) en el eje y para ver si existe una correlación entre la calificación de una película y la cantidad de premios. gana. Usaremos esta escala en las capas posteriores, así que cree las asignaciones estéticas a nivel del lienzo.
```r
#Create aesthetic mappings at the canvas level
viz <- ggplot(data=movies, aes(x=imdbRating, y=nrOfWins))
viz
```

## Añadiendo Geoms
***
Agregue un diagrama de dispersión de los datos al objeto viz ggplot usando la capa geom_point ().
```r
# Add a geom point layer
viz <- ggplot(data=movies, aes(x=imdbRating, y=nrOfWins)) +
geom_point()

# Prints the plot
viz
```

## Geom Aesthetics
***
Dentro de nuestro conjunto de datos de películas, tenemos una columna llamada nrOfGenre que describe el número de géneros que se asigna a una película. Agregue un mapeo estético a la capa geom_point() que coordina el color de los datos según nrO Genre.
```r
# Add color aesthetic mapping
viz <- ggplot(data=movies, aes(x=imdbRating, y=nrOfWins)) +
       geom_point(aes(color=nrOfGenre)) 


# Prints the plot
viz
```

## Manual Aesthetics
***
Parece haber algo de aglomeración en el diagrama de dispersión de nuestra película. Cambiemos la opacidad de nuestros puntos haciéndolos .5 translúcidos. Podemos lograrlo asignando manualmente el valor alfa de la capa geom_point().
```r
# Add manual alpha aesthetic mapping
viz <- ggplot(data=movies, aes(x=imdbRating, y=nrOfWins)) +
       geom_point(aes(color=nrOfGenre),alpha=0.5) 


# Prints the plot
viz
```

## Etiquetas
***
Agregue una llamada a la función labs () y cambie los siguientes argumentos:
- Cambia el título a "Movie Ratings Vs Award Wins" para contextualizar el objetivo del plot.
- Contextualice los detalles sobre el origen de los datos dentro del subtitle agregando "From IMDB dataset"
- Cambie la etiqueta x a "Movie Rating" y la etiqueta y a "Number of Award Wins".
- Cambie la etiqueta de la leyenda proporcionando un argumento de color con el valor de cadena de "Number of Genreo"
```r
# Add labels as specified
viz <- ggplot(data=movies, aes(x=imdbRating, y=nrOfWins)) +
       geom_point(aes(color=nrOfGenre), alpha=0.5) + 
       labs(title="Movie Ratings Vs Award Wins", subtitle="From IMDB dataset", x="Movie Rating", y="Number of Award Wins", color = "Number of Genre")

# Prints the plot
viz
```

## Extendiendo la gramática
***
- Inspeccione el mpg del conjunto de datos incorporado imprimiendo su head(). Tome nota especial de la columna de clase que describe la clase de vehículo para los automóviles con un total de 7 tipos (compact, SUV, minivan etc.)
- Cree una variable var que sea igual a un objeto ggplot() con el conjunto de datos incorporado mpg asociado como su argumento de datos.
```r
# Inspect the mpg builtin dataset
head(mpg)
```

```r
#Create a bar chart
bar<- ggplot(data=mpg,  aes(x=class)) + geom_bar(aes(fill=class))+labs(title="Types of Vehicles", subtitle="From fuel economy data for popular car models (1999-2008)")

bar
```