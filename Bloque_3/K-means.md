# Implementacion de K-means en R.
***
K-means es un método que tiene como objetivo generar una partición de un conjunto de n observaciones en k grupos. Cada grupo está representado por el promedio de los puntos que lo componen. El representante de cada grupo se denomina centroide. La cantidad de grupos a descubrir, k, es un parámetro que se debe fijar a priori. El método de clustering comienza con k centroides ubicados de forma aleatoria, y asigna cada observación al centroide más cercano. Después de asignarlos, los centroides se mueven a la ubicación promedio de todos los datos asignados a él, y se vuelven a reasignar los puntos de acuerdo a las nuevas posiciones de los centroides.

## A continuacion se presentara la implementacion de dicho metodo en el lenguaje R con el dataframe Iris.
***
La funcion ipak no pertenece necesariamente a la implementacion de k-means, sin embargo es una herramienta de suma importancia, la cual nos brinda la capacidad de cargar mas de un paquete al mismo tiempo.
```r
ipak <- function(pkg){
  new.pkg <- pkg[!(pkg %in% installed.packages()[, "Package"])]
  if (length(new.pkg)) 
    install.packages(new.pkg, dependencies = TRUE)
  sapply(pkg, require, character.only = TRUE)
}
```
En las siguientes lineas de codigo declaramos una variable packages la cual tendra asignado un vector con el nombre de los paquetes que utilizaremos, despues mandamos a llamar la funcion ipak y le sobrecargamos la variable declarada anteriormente. Una vez ejecutadas estas lineas de codigo ya estara listo nuestro enterno de trabajo para comenzar con la implementacion.
```r
packages <- c("stats","dplyr", "ggplot2","ggfortify","tidyr","tidyverse","cluster","factoextra","NbClust","tidyr")
ipak(packages)
```
R nos brinda una infinidad de bases de datos que nos sirven para comenzar a interactuar con el lenguaje. En este caso especifico utilizaremos el dataframe Iris para realizar la implementacion. A continuacion mostramos el dataframe con la palabra reservada view. El dataframe cuenta con una columna con datos que no son numericos por lo que con la palabra reservada select solo tomamos las columnas que son de nuestro interes.
```r
view(iris)

df = select(iris,c(1,2,3,4))
df
```
La funcion que se muestra a continuacion se utiliza para determinar la cantidad de clusters adeucados para nuestros datos. El analisis se hace en base a una serie de metodos ya implementados; entre ellos podemos encontrar los siguientes: wss, silhouette, gap_stat, trcovw, dindex, etc.
```r
resnumclust<-NbClust(df, distance = "euclidean", min.nc=2, max.nc=10, method = "kmeans", index = "alllong")
fviz_nbclust(resnumclust)
```
El resultado se mostrara en la consola de R y por medio de una grafica.
**En la siguiente imagen se muestra el resultado del metodo "resnumclus" en donde en base a su analisis nos recomienda utilizar los datos con solo 2 clusters**
![](Images/1.PNG)
**El metodo "resnumclus" tambien nos arroja la siguiente grafica de barras, en donde la barra con mayor valor es la que nos indica el numero de clusters recomendados.**
![](Images/2.PNG)
Una vez que sabemos que lo mas optimo es implementar dos cluster procedemos a calcularlos con las siguientes lineas de codigo.
```r
k2 <- kmeans(df, centers = 2, nstart = 25)
k2
str(k2)
```
Ahora que ya calculamos los clusters vamos a mostrarlos por medio de graficas. En nuestro caso decidimos mostrarlo por medio de 3 graficas diferentes las cuales se presentaran a continuacion.

### Código:
```r
#plotear los cluster
fviz_cluster(k2, data = df)
```
### Gráfica
![](Images/3.PNG)
### Código
```r
fviz_cluster(k2, data = df, ellipse.type = "euclid",repel = TRUE,star.plot = TRUE) #ellipse.type= "t", "norm", "euclid"
```
### Gráfica
![](Images/4.PNG)
### Código
```r
fviz_cluster(k2, data = df, ellipse.type = "norm")
```
### Gráfica
![](Images/5.PNG)