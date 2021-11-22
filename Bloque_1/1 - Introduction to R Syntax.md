# Introducción a la syntaxis de R
***
## Cálculos
```r
- 573 - 74 + 1
    - El resultado es "50"
- 25 * 2
    - El resultado es "50"
- 10 / 5
    - El resultado es "2"
```
Las operaciones matemáticas en R siguen el orden matemático estándar de operaciones. ¡Escribamos su primera línea de código R y calculemos algunas matemáticas básicas!
***
## Ejercicio
Calcule el resultado de esta ecuación: 25 * 4 + 9/3 en el bloque de código R de su cuaderno. Archivo RMD R-markdown. Antes de presionar Ejecutar, intente averiguar cuál sería la respuesta según el orden de las operaciones. ¡Tu respuesta debe coincidir con la salida!

## Código
```r
title: "Introduction to R Syntax"
output: html_notebook
25 * 4 + 9 / 3
```
## Comentarios
Irónicamente, lo segundo que vamos a hacer es mostrarle cómo decirle a R que ignore una parte de su programa. Prometemos que es muy útil saber cómo hacer esto. El texto escrito en un programa pero no ejecutado por la computadora se denomina comentario. R interpreta cualquier cosa después de un # como un comentario. ¿Por qué querría alguien que la computadora ignorara una parte de su archivo? ¡Varias razones! Los comentarios pueden:
- Proporcione el contexto de por qué algo está escrito como está:
    ```r
    # This code will be used to count the number of times anyone tweets the word
    persnickety
    persnickety_count <- 0
    ```
- Ayude a otras personas que lean el código a entenderlo más rápido:
    ```r
    # This code will calculate the likelihood that it will rain tomorrow
    complicated_rain_calculation_for_tomorrow()
    ```
- Ignore una línea de código y vea cómo se ejecutará un programa sin ella:
    ```r
    # useful_value <- old_sloppy_code()
    useful_value <- new_clean_code()
    ```
Anotar o documentar su código puede ayudar a otras personas a leer su programa más tarde. También podría ayudar a su yo futuro a comprender el código cuando vuelva atrás y lea un archivo antiguo tratando de recordar cómo funciona. Documentar su código ayudará a otros a reproducirlo y también lo ayudará a usted a convertirse en un mejor programador. Nota: En los cuadernos de R, también puede agregar documentación utilizando texto de rebajas fuera de los bloques de código.

## Ejercicio
***
Agregue un comentario dentro del bloque de código que explique que la línea de código dentro de notebook.Rmd está calculando el volumen en un cubo.
```r
title: "Introduction to R Syntax"
output: html_notebook
#En el siguiente codigo se realiza la multiplicacion de 3 numeros
3 * 3 * 3
```
## Tipos de datos
***
Ahora que sabe cómo calcular las matemáticas básicas y agregar comentarios que expliquen su código, profundicemos en cómo R "piensa" los diferentes tipos de datos. En R y en programación, los tipos de datos son las clasificaciones que damos a diferentes tipos de piezas de información. En esta lección, exploramos los siguientes tipos de datos R:

1. Numérico: cualquier número con o sin punto decimal: 23, 0,03 y el valor nulo numérico NA.

2. Carácter: cualquier agrupación de caracteres en su teclado (letras, números, espacios, símbolos, etc.) o texto. La mayoría de las cadenas están entre comillas simples: '...' o comillas dobles "...", aunque preferimos las comillas simples. A veces escuchará a este tipo referirse como "cadena".

3. Lógico: este tipo de datos solo tiene dos valores posibles: VERDADERO o FALSO (sin comillas). Es útil pensar en los tipos lógicos o booleanos como interruptores de encendido y apagado o como respuestas a una pregunta de "sí" o "no".

4. Vectores: una lista de datos relacionados que son todos del mismo tipo.

5. NA: este tipo de datos representa la ausencia de un valor y está representado por la palabra clave NA (sin comillas) pero tiene su propio significado en el contexto de los diferentes tipos. Es decir, hay un NA numérico, un carácter NA y un NA lógico.

Vamos a familiarizarnos con comprobar el tipo de datos de lo siguiente:
```r
class(2) # numeric class('hello') # character class('23') #character class (FALSE) #logical class(NA) #logical
```
En el ejemplo anterior, observe que la tercera línea está etiquetada como un tipo de carácter. ¿Por qué? Debido a que los caracteres 23 están entre comillas, se clasifica como un personaje.

Para imprimir un valor, debe poner el valor dentro de la siguiente sintaxis: print (). Imprime tu nombre como una cadena de caracteres. Imprime tu edad como un tipo numérico. En una nueva línea de código, escriba su edad como tipo de carácter.

## Código
```r
title: "Introduction to R Syntax"
output: html_notebook

print("Kevin Josafat Hernández Gambino")
print(23)
print("23")
```
## Variables
***
Ahora que sabe cómo R clasifica algunos de los tipos de información básica, descubramos cómo almacenarlos. En programación, las variables nos permiten almacenar información y asociar esa información con un nombre. En R, asignamos variables usando el operador de asignación, un signo de flecha (<-) hecho con un quilate y un guión.
```r
full_name <-"Juan Perez López"
```
En el ejemplo anterior, almacenamos el valor de cadena “Natalia Rodríguez Nuñez” en una variable llamada full_name. Las variables no pueden tener espacios o símbolos en sus nombres que no sean un guión bajo (_). No pueden comenzar con números, pero pueden tener números después de la primera letra (por ejemplo, cool_variable_5 está bien).

No es una coincidencia que llamemos a estas criaturas "variables". Si necesitamos actualizar una variable pero realizar el mismo proceso lógico en ella, ¡podemos cambiar su valor! Por ejemplo, tome la variable message_string:
```r
# Greeting
message_string <- "Hello there"
print(message_string)

# Farewell
message_string <- "Hasta la vista"
print(message_string)
```
Arriba, creamos la variable message_string, asignamos un mensaje de bienvenida e imprimimos el saludo. Después de saludar al usuario, queremos despedirnos de él. Luego actualizamos message_string a un mensaje de salida y lo imprimimos.

- Nota: También puede usar = en lugar de <- para asignar un valor, pero los R-tists (programadores de R) prefieren hacerlo con una flecha.

## Ejercicio
***
Cree un nombre de variable con su nombre como una cadena. Cree una edad variable con su edad como un número
```r
title: "Introduction to R Syntax"
output: html_notebook

name <- "Kevin Josafat Hernández Gambino"
age <- 23
```
## Vectores
***
Mencionamos Vectores cuando presentamos los tipos de datos anteriormente. En R, los vectores son una estructura similar a una lista que contiene elementos del mismo tipo de datos.

Eche un vistazo aquí:
```r
spring_months <- c("March", "April","May","June")
```
En el ejemplo anterior, creamos una nueva variable con el valor de un nuevo vector. Creamos este vector separando cuatro cadenas de caracteres con una coma y envolviéndolas dentro de c ().

Algunas cosas que debe saber hacer con los vectores:

- Puede verificar el tipo de elementos en un vector usando typeof (vector_name)
- Puede verificar la longitud de un vector usando length (vector_name)
- Puede acceder a elementos individuales en el vector usando [] y colocando la posición del elemento dentro de los corchetes. Por ejemplo, si quisiéramos acceder al segundo elemento escribiríamos: vector_name [2]. Nota: En R, comienza a contar elementos en la posición uno, no en cero.

## Ejercicio
***
```r
title: "Introduction to R Syntax"
output: html_notebook

phone <- c(664,219,7770)
```
    
## Condicionales
***
En R, a menudo realizaremos una tarea basada en una condición. Por ejemplo, si estamos analizando datos para el verano, solo querremos ver los datos que caen en junio, julio y septiembre.

Podemos realizar una tarea basada en una condición usando una declaración if:
```R
if (TRUE) {
  print('This message will print!')
} 
```
    
Observe que en el ejemplo anterior tenemos una declaración if. La sentencia if se compone de:
- La palabra clave if seguida de un conjunto de paréntesis () seguida de un bloque de código, o declaración de bloque, indicado por un conjunto de llaves {}.
- Dentro de los paréntesis (), se proporciona una condición que se evalúa como VERDADERO o FALSO.
- Si la condición se evalúa como verdadera, el código dentro de las llaves {} se ejecuta o se ejecuta.
- Si la condición se evalúa como falsa, el código dentro del bloque no se ejecutará.

Saber cómo usar las declaraciones if le ayudará a introducir la lógica en su análisis de datos. También hay una forma de agregar una instrucción else. Una instrucción else debe combinar con una instrucción if, y juntas se denominan instrucción if ... else.
```r
if (TRUE) {
   print("Go to sleep!")
} else {
   print("Wake up!")
}
```
En el ejemplo anterior, la declaración else:
- Utiliza la palabra clave else que sigue al bloque de código de una instrucción if.
- Tiene un bloque de código que está envuelto por un conjunto de llaves {}.
- El código dentro del bloque de código de la instrucción else se ejecutará cuando la condición de la instrucción if se evalúe como falsa. Estas declaraciones if ... else nos permiten automatizar soluciones a preguntas de sí o no, también conocidas como decisiones binarias.

## Ejercicio
***

Cree una declaración condicional en notebook.Rmd de modo que cambie el valor del mensaje de la variable a '¡Ejecuto esto cuando sea cierto!' cuando la condición es VERDADERA, y el valor del mensaje es '¡Ejecuto esto cuando es falso!' cuando es FALSO.
```r
title: "Introduction to R Syntax"
output: html_notebook

message <- "I change based on a condition."
if(TRUE){
 message <- "I execute this when true!"
}else{
  message <- "I execute this when false!"
}

print(message)
```

## Operadores de comparación
***
Al escribir declaraciones condicionales, a veces necesitamos usar diferentes tipos de operadores para comparar valores. Estos operadores se denominan operadores de comparación.

Aquí hay una lista de algunos operadores de comparación útiles y su sintaxis:
- Menor que: <
- Mayor que:>
- Menor o igual que: <=
- Mayor o igual que:> =
- Es igual a: ==
- NO es igual a: !=

Los operadores de comparación comparan el valor de la izquierda con el valor de la derecha. Por ejemplo:
```r
10 < 12 # Evaluates to TRUE
```
Puede resultar útil pensar en las declaraciones de comparación como preguntas. Cuando la respuesta es "sí", la declaración se evalúa como verdadera, y cuando la respuesta es "no", la declaración se evalúa como falsa. El código anterior estaría preguntando: ¿es 10 menos que 12? ¡Si! Entonces 10 <12 se evalúa como verdadero.
## Ejercicio
***
Utilice un operador de comparación para verificar si 56 es mayor o igual que 129. ¿A qué se debe evaluar esta expresión? ¡Compruébalo ejecutando tu código!

En una nueva línea, use el operador de comparación correcto para verificar si 56 NO es igual a 129. ¿A qué se debe evaluar esta expresión? ¡Compruébalo ejecutando tu código!
```r
title: "Introduction to R Syntax"
output: html_notebook

56 >= 129
56 != 129
```

## Operadores lógicos
***
Trabajar con condicionales significa que usaremos valores lógicos, verdaderos o falsos. En R, hay operadores que trabajan con valores lógicos conocidos como operadores lógicos. Podemos usar operadores lógicos para agregar una lógica más sofisticada a nuestros condicionales. Hay tres operadores lógicos:

- El operador AND (&)
- El operador OR (|)
- El operador NOT, también conocido como operador bang (!)

Cuando usamos el operador &, estamos comprobando que dos cosas son ciertas:
```r
if (stopLight == 'green' & pedestrians == 0) {
  print('Go!');
} else {
  print('Stop');
}
```
Cuando se usa el operador &, ambas condiciones deben evaluarse como verdaderas para que toda la condición se evalúe como verdadera y se ejecute. De lo contrario, si alguna de las condiciones es falsa, la condición & se evaluará como falsa y se ejecutará el bloque else.

Si solo nos importa que una de las dos condiciones sea verdadera, podemos usar el | operador:
```r
if (day == 'Saturday' | day == 'Sunday') {
  print('Enjoy the weekend!')
} else {
  print('Do some work.')
}
```
Al utilizar el | operador, solo una de las condiciones debe evaluarse como verdadera para que la declaración general se evalúe como verdadera. En el ejemplo del código anterior, si el día == 'sábado' o el día == 'domingo' se evalúa como verdadero, la condición de if se evaluará como verdadera y su bloque de código se ejecutará. Si la primera condición en un | declaración se evalúa como verdadera, la segunda condición ni siquiera se comprobará.

Los ! El operador NOT invierte o niega el valor de un valor VERDADERO:
```r
excited <- TRUE
print(!excited) # Prints FALSE
```
Esencialmente, el! El operador tomará un valor verdadero y devolverá falso, o tomará un valor falso y devolverá verdadero.

Los operadores lógicos se usan a menudo en declaraciones condicionales para agregar otra capa de lógica a nuestro código.
## Ejercicio
***
Hay dos variables en su código, el clima y high_chance_of_rain. Escribe una declaración condicional que:
- Comprueba si el clima es igual de nublado y si hay una alta probabilidad de lluvia.
- Si es ambos, el bloque de código debe asignar el valor del mensaje variable como "¡Paquete paraguas!"
- De lo contrario, el bloque de código debería asignar el valor del mensaje variable a "¡No se necesita paraguas!"
- Imprime la variable de mensaje después de la declaración condicional. Según la condición, ¿cuál debería ser su valor?

## Código
```r
title: "Introduction to R Syntax"
output: html_notebook

message <- 'Should I pack an umbrella?'
weather <- 'cloudy'
high_chance_of_rain <- TRUE

if( weather == "cloudy" & high_chance_of_rain ){
message <- "Pack umbrella!"
}else{
  message <- "No need for umbrella!"
}

print(message)
```

## Llamar a una función
***
Las funciones son acciones que podemos realizar. R proporciona una serie de funciones y, de hecho, ha estado utilizando algunas de ellas aunque tal vez no se haya dado cuenta.

Llamamos, o usamos, estas funciones indicando el nombre de la función y siguiéndola con un paréntesis de apertura y cierre: es decir. nombre de la función(). Además, entre paréntesis, generalmente pasamos un argumento o un valor que la función usa para realizar una acción, es decir, functionName (valor).

¿Esa sintaxis parece un poco familiar? Cuando hemos usado print () llamamos a la función de impresión. Cuando creamos un vector, ¡usamos la función combinar c ()! ¡Veamos print () y algunas funciones reales en acción!
```r
sort(c(2,4,10,5,1)); # Outputs c(1,2,4,5,10)
length(c(2,4,10,5,1)); # Outputs 5
sum(5,15,10) #Outputs 30
```
Veamos cada una de las líneas anteriores:
- En la primera línea, se llama a la función sort () con un parámetro del vector c (2,4,10,5,1). El resultado es un vector ordenado c (1, 2, 4, 5, 10) con los valores en orden ascendente.
- En la segunda línea, llamamos a una función que habíamos visto antes: length () y devolvió el valor 5 porque había cinco elementos en el vector.
- En la tercera línea, llamamos a una función sum () que suma todos los argumentos que le pasamos.
Comprender cómo llamar a una función y qué argumentos necesita es una parte fundamental del aprovechamiento de R como herramienta para realizar análisis. ¡Practiquemos llamar a algunas funciones útiles!

## Ejercicio
***
La función unique () toma un argumento de vector y devuelve un vector con solo los elementos únicos en ese vector (eliminando todos los duplicados).

- Llame a esta función y pase los datos del argumento.
- Guarde ese resultado dentro de una variable llamada unique_vals
- Imprima la variable unique_vals para que pueda ver lo que hay dentro del vector con sólo valores únicos.
Obtén la raíz cuadrada sqrt () del número 49 llamando a la función con el argumento especificado. Guarde el resultado dentro de una variable llamada solución.

Imprima la variable de solución para que pueda ver que confirm sqrt () calculó la raíz cuadrada correctamente.

La función floor () redondea un decimal hacia abajo al siguiente número entero, y la función techo () redondea hacia arriba al siguiente número entero. Llame a ambas funciones en el número 3.14 y guarde cada resultado dentro de dos nuevas variables que cree: round_down y round_up respectivamente.

Imprima ambas variables para que pueda ver su contenido.

## Código
***
```r
title: "Introduction to R Syntax"
output: html_notebook

data <- c(120,22,22,31,15,120)

unique_vals = unique(data)
print(unique_vals)

solution <- sqrt(49)
print(solution)

round_down <- floor(3.14)
round_up <- ceiling(3.14)

print(round_down)
print(round_up)
```

## Importación de paquetes
***
La popularidad de R también se debe en gran parte a los fantásticos paquetes disponibles en el idioma. Un paquete es un conjunto de código que facilita la codificación de determinadas tareas. Hay todo tipo de paquetes para todo tipo de propósitos, que van desde visualizar y limpiar datos hasta pedir pizza o publicar un tweet. De hecho, la mayoría de los programadores R (programadores R) usan paquetes cuando codifican. Es por eso que es posible que los escuche diferenciar los paquetes de "Base R". Base R se refiere al lenguaje R por sí mismo y todo lo que puede hacer sin importar ningún paquete.

Base R es muy potente, pero la mayoría de las veces, querrá importar un paquete para hacer su vida más fácil. Solo necesita ejecutar este comando la primera vez que instala un paquete, después de eso no es necesario ejecutarlo:
```r
install.packages('package-name')
```
Para importar un paquete, simplemente:
```r
library(package-name)
```
Puede buscar documentación para los diferentes paquetes disponibles en R en CRAN (Red de archivo integral de R).

En esta lección, codificamos en Base R, pero practiquemos la importación de uno de los paquetes R más populares: dplyr. Dplyr es un paquete que se utiliza para limpiar, procesar y organizar datos que utilizará a medida que aprenda sobre R.
## Ejercicio
***
Actualmente, el código dentro de notebook.Rmd arroja un error porque usa los paquetes dplyr y readr sin importarlos. Importe los paquetes dplyr y readr usando la función library () y luego presione ejecutar para que pueda observar que los paquetes hacen su magia.
```r
title: "Introduction to R Syntax"
output: html_notebook

# load libraries
#install.packages('dplyr')
#install.packages('readr')

library(dplyr)
library(readr)

# load data frame
artists <- read_csv('artists.csv')

# inspect data frame
artists
head(artists)
summary(artists)

artists %>%
  select(-country,-year_founded,-albums) %>%
  filter(spotify_monthly_listeners > 20000000, genre != 'Hip Hop') %>%
  arrange(desc(youtube_subscribers))
```