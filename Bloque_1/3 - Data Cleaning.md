# Limpieza de datos en R
***
Repasaremos las técnicas que los científicos utilizan para lograr estos objetivos observando algunos conjuntos de datos "sucios" y tratando de llevarlos a un estado bueno y limpio. A lo largo del camino usaremos los poderosos paquetes de orden dplyr y tidyr para conseguir que nuestros datos estén limpísimos.

El primer paso para diagnosticar si un conjunto de datos está ordenado o no es utilizar las funciones de base R y dplyr para explorar y sondear el conjunto de datos.

Han visto la mayoría de las funciones que usamos a menudo para diagnosticar un conjunto de datos para su limpieza. Algunas de las más útiles son:

- head() - muestra las primeras 6 filas de la tabla
- summary() - muestra las estadísticas resumidas de la tabla
- colnames() - muestra los nombres de las columnas de la tabla

## Ejercicio
***
Tenemos dos dataframes, tienda de comestibles_1 y tienda de comestibles_2. Comienza viendo el head() de ambos comestibles_1 y comestibles_2.
- Explora los marcos de datos usando las otras funciones listadas.
- ¿Qué dataframe está "limpio", ordenado y listo para el análisis? Cree una variable llamada marco_de_datos_limpios y asígnele el valor 1 si el marco de datos "comestibles_1" es limpio y ordenado o 2 si el marco de datos "comestibles_2" es limpio y ordenado.

```r
# inspect data frames
head(grocery_1)
head(grocery_2)
summary(grocery_1)
summary(grocery_2)
print(colnames(grocery_1))
print(colnames(grocery_2))
```

```r
# clean data frame
clean_data_frame <- 2
```

## Lidiar con múltiples archivos
### Ejercicio
***
Tienes 10 archivos diferentes que contienen 100 estudiantes cada uno. Estos archivos siguen la estructura de nombres:

- exams_0.csv
- exams_1.csv
- … up to exams_9.csv
Vas a leer cada archivo en un dataframe individual y luego combinarás todas las entradas en un dataframe.

Primero, crea una variable llamada student_files y ponla igual al list.files() de todos los archivos CSV que queremos importar.
```r
# list files
student_files <- list.files(pattern = "exams_.*csv")
```
Lee cada archivo en student_files en un dataframe usando lapply() y guarda el resultado en df_list.
```r
# read files
df_list <- lapply(student_files,read_csv)
```
Concatenar todos los marcos de datos en df_list en un dataframe llamado estudiantes.
```r
# concatenate data frames
students <- bind_rows(df_list)
```
Inspeccione a los estudiantes. Guarda el número de filas de los estudiantes en nrow_students. ¿Los has tomado todos?
```r
# number of rows in students
nrow_students <- nrow(students)
```

## Cambiar la forma de sus datos
***
El dataframe de los estudiantes del ejercicio anterior se ha cargado en el cuaderno por usted. Guarde los nombres de las columnas en original_col_names e imprímalo.
```r
# original column names
original_col_names <- colnames(students)
print(original_col_names)
```
Utilice gather para crear una nueva tabla (todavía llamada estudiantes) que sigue esta estructura. Luego vea el head() de los estudiantes.
```r
# gather columns
students <- students %>%
  gather('fractions','probability',key='exam', value='score')
head(students)
```
Guarde los nombres de las columnas del marco de datos de los estudiantes actualizado en collect_col_names e imprímalo.
```r
# updated column names
gathered_col_names <- colnames(students)
print(gathered_col_names)
```
Encuentre el recuento de cada valor único en la columna del examen. Guarde el resultado en exam_counts y vea exam_counts.
```r
# unique value counts of exam
exam_counts <- students %>%
  count(exam)
exam_counts
```

## Tratar con duplicados
***
El dataframe de los students tiene una identificación de columna que no es única ni necesaria para nuestro análisis. Elimine la columna de identificación del dataframe y guarde el resultado para los students. Ver el head() de los students.
```r
# drop id column
students <- students %>%
  select(-id)
head(students)
```
Parece que en el proceso de recopilación de datos, algunas filas pueden haberse registrado dos veces. Utilice la función duplicates() en el dataframe de los estudiantes para crear un objeto vectorial llamado duplicados.
```r
# find and count duplicated rows
duplicates <- students %>%
  duplicated() %>%
  table()
duplicates
```
Actualice el valor de los estudiantes para que sea el dataframe de los students con solo filas únicas / distintas.
```r
# remove duplicated rows
students <- students %>%
  distinct()
```
Use la función duplicated() nuevamente para crear un objeto llamado updated_duplicates después de eliminar los duplicados. Canalice el resultad o a table() para ver si quedan duplicados y vea updated_duplicates. ¿Quedan VERDADEROS?
```r
# find and count duplicated rows in updated data frame
updated_duplicates <- students %>%
  duplicated() %>%
  table()
updated_duplicates
```

## División por índice
***
Imprima las columnas del marco de datos de los students.
```r
# print columns of students
print(colnames(students))
```
Vea el head() de los students para ver qué tipo de datos contiene gender_age.
```r
# view head of students
head(students)
```
Separemos los datos de género en una nueva columna llamada género. Guarde el resultado para los students y vea el head().
```r
# add gender and age columns
students <- students %>%
  mutate(gender = str_sub(gender_age,1,1),
         age = str_sub(gender_age,2))
head(students)
```
Ahora, separe los datos de edad en una nueva columna llamada edad. Guarde el marco de datos actualizado para los students y vea el head().
```r
# drop gender_age column
students <- students %>%
  select(-gender_age)
head(students)
```

## Dividiendo por caracteres
***
Ver el head() de los estudiantes. Observe que los nombres de los estudiantes se almacenan en una columna llamada full_name.
```r
# view the head of students
head(students)
```
Separe la columna full_name en dos columnas nuevas, first_name y last_name, dividiendo el carácter "".

Proporcionar como argumento adicional a la función separate() extra = 'merge'. Esto asegurará que los segundos nombres o apellidos de dos palabras terminen todos en la columna de last_name.
```r
# separate the full_name column
students <- students %>%
  separate(full_name,c('first_name','last_name'),' ', extra ='merge')

head(students)
```

## Mirando los tipos de datos
***
Inspeccionemos los tipos de datos en la tabla de alumnos. Imprime la estructura de los estudiantes.
```r
# print structure of students
str(students)
```
Si quisiéramos hacer un diagrama de dispersión de la edad frente al puntaje promedio del examen, ¿podríamos hacerlo con este tipo de datos? Pegue el siguiente código en el último bloque de código para intentar imprimir la media de la columna de puntuación de los estudiantes.
```r
# mean of age column
students %>% 
  summarise(mean_score = mean(score))
```

## Análisis de cadenas
***
En el último ejercicio vimos que es difícil encontrar la media de la columna de puntuación cuando los datos se almacenan como caracteres y no como números. Vea el head() de los students para ver los valores en la columna de puntuación.
```r
# view head of students
head(students)
```
Elimine el símbolo '%' de la columna de puntuación y guarde el marco de datos resultante para los students. Ver students.
```r
# remove % from score column
students <- students %>%
  mutate(score=gsub('\\%','',score))
head(students)
```
Convierta la columna de puntuación a un tipo numérico utilizando la función as.numeric(). Guarde este nuevo marco de datos para los estudiantes y véalo.
```r
# change score column to numeric
students <- students %>%
  mutate(score=as.numeric(score))
head(students)
```