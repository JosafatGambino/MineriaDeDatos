# Aggregates en R
***
En esta lección, aprenderá acerca de los aggregates en R usando dplyr. Una estadística aggregate es una forma de crear un solo número que describe un grupo de números. Las estadísticas aggregate comunes incluyen media, mediana y desviación estándar.
## Cálculo de estadísticas de columna
***
En este ejercicio, aprenderá a combinar todos los valores de una columna para un solo cálculo. Esto se puede hacer con la ayuda de la función dplyr summary(), que devuelve un nuevo marco de datos que contiene el cálculo deseado.

Algunos ejemplos de este tipo de cálculo incluyen:

- Los customers del dataframe contienen los nombres y edades de todos sus clientes. Quieres encontrar la edad media:
```r
customers %>%
  select(age)
# c(23, 25, 31, 35, 35, 46, 62)
customers %>%
  summarize(median_age = median(age))
# 35
```

- Los shipments del dataframe contienen información sobre la dirección de todos los envíos que envió el año pasado. Quiere saber a cuántos estados diferentes ha enviado.
```r
shipments %>%
  select(states)
# c('CA', 'CA', 'CA', 'CA', 'NY', 'NY', 'NJ', 'NJ', 'NJ', 'NJ', 'NJ', 'NJ', 'NJ')
shipments %>%
  summarize(n_distinct_states = n_distinct(states))
# 3
```

- El inventory del dataframe contiene una lista de tipos de camisetas que fabrica su empresa. Quieres conocer la desviación estándar de los precios de tu inventario.
```r
inventory %>%
  select(price)
# c(31, 23, 30, 27, 30, 22, 27, 22, 39, 27, 36)    
inventory %>% 
  summarize(sd_price = sd(price))
# 5.465595
```
## Ejercicio
***
- ShoeFly.com tiene un nuevo lote de pedidos almacenados en el dataframe orders. Inspeccione las primeras 10 filas si el dataframe usa head().
```r
# load order data
orders <- read_csv("orders.csv")

# inspect orders here:
head(orders,10)
```
- Nuestro departamento de finanzas quiere saber el precio del par de zapatos más caro comprado. Guarde su respuesta en la variable most_expensive.
```r
# define most_expensive here:
most_expensive <- orders %>%
  summarize(max_price = max(price, na.rm = TRUE))
most_expensive
```
- Nuestro departamento de moda quiere saber cuántos colores diferentes de zapatos estamos vendiendo. Guarde su respuesta en la variable num_colors.
```r
# define num_colors here:
num_colors <- orders %>% 
  summarize(n_distinct_shoe_color = n_distinct(shoe_color))
num_colors
```

## Cálculo de funciones agregadas I
***
En el ejercicio anterior, nuestro departamento de finanzas quería saber cuál era el zapato más caro que vendimos. Ahora, quieren saber el precio del zapato más caro para cada tipo de zapato (es decir, el precio de la bota más cara, el precio de la bailarina más cara, etc.). Guarde su respuesta en la variable pricey_shoes y visualícela.
```r
# define pricey_shoes here:
pricey_shoes <- orders %>%
  group_by(shoe_type) %>%
  summarize(max_price = max(price, na.rm = TRUE))
pricey_shoes
```
El equipo de inventario desea saber cuántos de cada tipo de zapato se han vendido para poder pronosticar el inventario para el futuro. Guarde su respuesta en la variable shoes_sold y visualícela.
```r
# define shoes_sold here:
shoes_sold <- orders %>%
  group_by(shoe_type) %>%
  summarize(count = n())
shoes_sold
```
## Cálculo de funciones agregadas II
***
Encuentre el número total de zapatos de cada combinación de shoe_type / shoe_color comprados usando group_by, resume () yn (). Guarde su resultado en la variable shoe_counts y visualícelo.
```r
# define shoe_counts here:

shoe_counts<- orders %>%
  group_by(shoe_type, shoe_color) %>%
  summarize(count = n())

shoe_counts
```
Encuentre el precio medio de cada combinación de shoe_type / shoe_material comprada usando group_by, resume () y mean (). Guarde su resultado en la variable shoe_prices y visualícelo.
```r
# define shoe_prices here:
shoe_prices<- orders %>%
  group_by(shoe_type,shoe_material) %>%
  summarize(mean_price = mean(price, na.rm = TRUE))

shoe_prices
```

## Combinar agrupación con filter
***
Agrupe los pedidos por shoe_type y filtre para incluir solo los pedidos con un shoe_type que se haya pedido más de 16 veces. Guarde el resultado en most_pop_orders y véalo. Puede incluir cualquiera de las funciones de resumen como parte de un argumento para filter(), ¡incluido n ()!
```r
# define most_pop_orders here:

most_pop_orders<- orders %>%
  group_by(shoe_type) %>%
  filter(n() > 16)
```
## Combinando agrupación con Mutate
***
Agrupe los pedidos por shoe_type y cree una nueva columna denominada diff_from_shoe_type_mean que almacene la diferencia de precio entre el precio de un pedido y el precio medio de los pedidos con el mismo shoe_type. Guarde el resultado en diff_from_mean y véalo.

¡No olvide incluir na.rm = TRUE como argumento en la función de resumen que llame!
```r
# define diff_from_mean here:
diff_from_mean <- orders %>%
  group_by(shoe_type) %>%
  mutate(diff_from_shoe_type_mean = price - mean(price, na.rm = TRUE))
diff_from_mean
```

## Review
***
Encuentre el precio promedio de un pedido en el dataframe de pedidos usando resume() y la función de resumen mean(). Guarde el marco de datos resultante en una variable denominada precio_promedio y visualícelo.
```r
# define average_price here:
average_price <- orders %>% 
  summarize(mean_price = mean(price, na.rm = TRUE))
average_price
```
Use una declaración group_by para calcular cuántas visitas provienen de cada una de las diferentes fuentes. Guarde su respuesta en la variable click_source y visualícela.
```r
# define click_source here:
click_source <- page_visits %>%
  group_by(utm_source) %>%
  summarize(count = n())
click_source
```
Nuestro departamento de marketing cree que el tráfico a nuestro sitio ha ido cambiando durante los últimos meses. Utilice group_by para calcular el número de visitas a nuestro sitio desde cada utm_source para cada mes. Guarde su respuesta en la variable click_source_by_month y visualícela.
```r
# define click_source_by_month here:
click_source_by_month <- page_visits %>%
  group_by(utm_source,month) %>%
  summarize(count = n())
click_source_by_month
```