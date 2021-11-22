# Uniendo tablas en R
***
## Introducción
En esta lección, aprenderemos los comandos dplyr que nos ayudan a trabajar con datos almacenados en varias tablas.

### Ejercicio

- Empiece por inspeccionar los orders usando head(). ¿Qué columnas hay en el dataframe?
- Ahora inspeccione los products usando head (). ¿Hay columnas en común con los orders?
- Finalmente, inspeccione a los clients usando head(). ¿Hay columnas en común con orders o products?

```r
# inspect orders, customers and products here:
head(orders)
head(customers)
head(products)
```

## Joining
***
### Ejercicio
Examine las tablas de pedidos y productos. ¿Cuál es la descripción del producto que se pidió en el pedido 3? Dé su respuesta como una cadena asignada a la variable order_3_description.

Examine las tablas de pedidos y clientes. ¿Cuál es el número de teléfono del cliente en el pedido 5? Dé su respuesta como una cadena asignada a la variable order_5_phone_number.
```r
# inspect orders, customers and products
head(orders)
head(customers)
head(products)
```

```r
# define order_3_description here:
order_3_description <- "thing-a-ma-jig" 

# define order_5_phone_number here:
order_5_phone_number<- "112-358-1321"
```
## Inner Join I
***
El método inner_join () busca columnas que sean comunes entre dos marcos de datos y luego busca filas donde los valores de esas columnas sean iguales. Luego combina las filas coincidentes en una sola fila en una nueva tabla.

Podemos llamar al método inner_join () con dos marcos de datos como este:
```r
joined_df <- orders %>%
  inner_join(customers)
```
### Ejercicio
```r
# inspect orders, customers and products
head(sales)
head(targets)
```
```r
# define sales_vs_targets here:
sales_vs_targets <- sales %>%
  inner_join(targets)
```
```r
# define crushing_it here:
crushing_it <- sales_vs_targets %>%
  filter(revenue > target)
crushing_it
```
## Inner Join II
***
Además de usar inner_join() para unir dos dataframe, podemos usar la pipe %>% para unir múltiples marcos de datos a la vez. El siguiente comando uniría los orders con los customers y luego uniría el dataframe resultante con los productos:
```r
big_df <- orders %>%
  inner_join(customers) %>%
  inner_join(products)
```
### Ejercicio
```r
# load men_women data here:
men_women <- read_csv("men_women_sales.csv")

# inspect men_women here:
head(men_women)
```
```r
# define all_data here:
all_data <- sales %>%
  inner_join(targets) %>%
  inner_join(men_women)
all_data
```
```r
# define results here:
results <- all_data %>%
  filter(revenue > target, women > men)
results
```

## Join on Specific Columns I
***
En el ejemplo anterior, la función inner_join () "sabía" cómo combinar tablas basándose en las columnas que eran iguales entre dos tablas. Por ejemplo, tanto los pedidos como los clientes tenían una columna llamada customer_id. Esto no siempre será cierto cuando queremos realizar una unión.

Debido a que las columnas id significarían algo diferente en cada tabla, nuestras combinaciones predeterminadas serían incorrectas.

Una forma en que podríamos abordar este problema es usar la función dplyr rename() para cambiar el nombre de las columnas para nuestras combinaciones.
```r
customers <- customers %>%
  rename(customer_id = id)
inner_join(orders, customers)
```

### Ejercicio
```r
# inspect orders and products
head(orders)
head(products)
```
```r
# rename the id column of products here:
products <- products %>%
  rename(product_id = id)
products
```
```r
# define orders_products here:
orders_products <- orders %>%
  inner_join(products)
orders_products
```

## Join on Specific Columns II
***
En el ejercicio anterior, aprendimos cómo usar rename () para unir dos marcos de datos cuyas columnas no coinciden. Sin embargo, existe una mejor opción. Podemos agregar el argumento by al llamar a inner_join() para especificar en qué columnas queremos unirnos.
```r
orders %>% 
  inner_join(customers,
             by = c('customer_id' = 'id'))
```
Nota: Si usamos esta sintaxis, terminaremos con dos columnas llamadas id, una de la primera tabla y otra de la segunda. R no le permitirá tener dos columnas con el mismo nombre, por lo que las cambiará a id_x e id_y
### Ejercicio
```r
# define orders_products here:
orders_products <- orders %>%
  inner_join(products,
            by = c('product_id' = 'id'))
orders_products
```
```r
# define products_orders here:
products_orders <- products %>%
  inner_join(orders,
            by = c('id' = 'product_id'),
            suffix = c('_product','_order'))
products_orders
```

## Mismatched Joins
***
En nuestros ejemplos anteriores, siempre había valores coincidentes cuando estábamos realizando nuestras uniones. ¿Qué pasa cuando eso no es cierto? Imaginemos que nuestra tabla de productos está desactualizada y le falta el producto más nuevo: Producto 5. ¿Qué sucede cuando alguien lo pide?
```r
# define orders_products here:
orders_products <- orders %>%
  inner_join(products)
orders_products
```
## Full Join
***
Si quisiéramos combinar los datos de ambas empresas sin perder a los clientes que faltan en una de las tablas, podríamos usar Full Join. Una unión completa incluiría todas las filas de ambas tablas, incluso si no coinciden. Los valores faltantes se rellenan con NA.
```r
full_joined_dfs <- company_a %>%
  full_join(company_b)
```
### Ejercicio
```r
# inspect store_a and store_b
head(store_a)
head(store_b)
```
```r
# define store_a_b_full here:
store_a_b_full <- store_a %>%
  full_join(store_b)
store_a_b_full
```
## Left and Right Joins
***
### Left Join
Una combinación izquierda incluye todas las filas de la primera tabla (izquierda), pero solo las filas de la segunda tabla (derecha) que coinciden con la primera tabla.
```r
left_joined_df <- company_a %>%
  left_join(company_b)
```
### Right Join
Una combinación derecha es exactamente lo contrario de una combinación izquierda. Aquí, la tabla unida incluirá todas las filas de la segunda tabla (derecha), pero solo las filas de la primera tabla (izquierda) que coincidan con la segunda tabla.
```r
right_joined_df <- company_a %>%
  right_join(company_b)
```
### Ejercicio
```r
# inspect store_a and store_b
head(store_a)
head(store_b)
```
```r
# define left_a_b here:
left_a_b <- store_a %>%
  left_join(store_b)
left_a_b

```
```r
# define left_b_a here:
left_b_a <- store_b %>%
  left_join(store_a)
left_b_a
```
## Concatenate Data Frames
***
A veces, un conjunto de datos se divide en varias tablas. Por ejemplo, los datos a menudo se dividen en varios archivos CSV para que cada descarga sea más pequeña.

Cuando necesitamos reconstruir un solo dataframe a partir de varios dataframe más pequeños, podemos usar el método dplyr bind_rows(). Este método solo funciona si todas las columnas son iguales en todos los dataframe.
```r
concatenated_dfs <- df1 %>%
  bind_rows(df_2)
```
### Ejercicio
```r
# inspect bakery and ice_cream
head(bakery)
head(ice_cream)
```
```r
# define menu here:
menu <- bakery %>%
  bind_rows(ice_cream)
```
## Review
***
```r
# define v_to_c here:
v_to_c <- visits %>%
 inner_join(checkouts)
v_to_c

v_to_c <- v_to_c %>% 
  mutate(time = checkout_time - visit_time)
v_to_c
```
```r
# define avg_time_to_check here:
avg_time_to_check <- v_to_c %>% 
  summarize(mean_time = mean(time))
avg_time_to_check
```