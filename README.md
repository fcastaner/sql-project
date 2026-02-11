La base de datos utilizada en este proyecto es Shakila, una base de datos de ejemplo orientada a la gestión de un videoclub.
El esquema de la base de datos ha sido creado ejecutando el script SQL proporcionado en PostgreSQL y posteriormente visualizado mediante el diagrama generado en DBeaver.
La base de datos está compuesta por varias tablas relacionadas entre sí, organizadas principalmente en torno a películas, actores, clientes, alquileres y pagos.

Explicación de las principales tablas y relaciones
Películas
film: contiene la información principal de las películas (título, duración, idioma, precio de alquiler, clasificación, etc.).
language: indica el idioma de las películas.
film_actor: tabla que relaciona películas y actores.
film_category y category: permiten clasificar las películas por género.

Actores
actor: almacena el nombre y apellido de los actores.
Se relaciona con las películas a través de la tabla film_actor.

Clientes y alquileres
customer: información de los clientes.
rental: registra los alquileres de películas realizados por los clientes.
inventory: representa las copias de las películas disponibles en cada tienda.
Cada alquiler está asociado a una copia concreta de una película

Pagos
payment: almacena los pagos realizados por los clientes por cada alquiler.
Está relacionada con customer, rental y staff.

Tiendas y empleados
store: representa las tiendas del videoclub.
staff: empleados que trabajan en las tiendas.
address, city y country: gestionan la información de direcciones.
Las tiendas y empleados están vinculados a direcciones y localizaciones geográficas.

Conclusión del esquema
El esquema de la base de datos Shakila muestra un conjunto de relaciones entre variables de uno a muchos y muchos a muchos, lo que permitirá realizar consultas detalladas sobre películas, actores, clientes, alquileres y pagos.


CONCLUSIONES POR CONSULTA
2. Extraemos primero todos los nombres de película y con WHERE condicionamos a que el rating sea R
3. Extraemos primero todos los actores y luego usamos WHERE y BETWEEN para condicionar que el actor_id esté entre 30 y 40.
4. Usamos WHERE e IS NOT NULL para que no nos muestre las películas con idioma original vacío y AND para que añada además la condición de que el idioma de la película coincida con el idioma original. No nos da resultados porque vemos que el idioma original en la BBDD siempre viene vacío. 
5. Usamos WHERE e IS NOT NULL para que nos muestre solo películas cuya duración no esté vacía (no informada) y ORDER BY ASC para ordenar de menor a mayor duración. 
6. Usamos WHERE y LIKE '%ALLEN%' para indicar la condición de que el apellido del actor contenga ALLEN
7. Usamos COUNT(*) para calcular todas las películas y GROUP BY para agruparlas por clasificación
8. Usamos WHERE y OR para indicar la condición de que las películas sean de la clasificación PG-13 o tengan una duración mayor a 3h
9.Con la función VARIANCE encontramos la variabilidad del coste de reemplazo. Hay bastante variabilidad en el coste de reemplazo de las películas. Por tanto, no todas tienen el mismo coste de reemplazo, sino que son bastante diferentes. 
10.Con las funciones min y max podemos extraer la duración mínima y máxima del repositorio de películas. Sorprende que una película solo dure 46 min vs la más larga que dura 185.
11. Primero ordenamos los pagos del más reciente al más antiguo y luego con Offset y limit extraemos solo el antepenúltimo pago
12. Gracias a incluir 'NOT IN' podemos excluir los ratings solicitados
13. Con Group By agrupamos los resultados (promedio de duración) por clasificación. Las películas de PG-13 son las que más duran.
14. Filtramos con >180 la duración de las películas que duran más de 3h
15. Obtenemos el total de ingresos con la función SUM. El total generado por la empresa es de 67416,51€
16. Ordenamos con ORDER BY customer_id DESC el valor de customer_id de mayor a menor. Luego con LIMIT 10 le pedimos que nos devuelva solo los 10 primeros
17. Nos hemos encontrado con el problema de que tal como está escrito en el enunciado el título de la película Egg Igby no nos mostraba resultados para la query. Por ello verificamos primero el valor exacto del título en la tabla film y reejecutamos de nuevo la query pero con el título correctamente escrito. En este ejercicio hemos usado JOIN para unir tres tablas diferentes (actor, film_actor y film). De esta manera podemos extraer lo que se nos solicita. 
18. Con Select Distinct podemos ver los 1000 títulos de películas únicos (no se repiten)
19. Unimos con JOIN tres tablas diferentes (film, film_category y category) y luego usamos WHERE y AND para especificar los condicionantes y extraer así los títulos de las comedias de duración mayor a 180 minutos.
20. Usamos JOIN para extraer datos de 3 tablas diferentes (film, category y film_category). Además AVG para sacar el promedio de duración y GROUP BY para agrupar por categoría, lo cual nos obliga a usar HAVING para indicar el condicionante de que la duración promedio sea mayor a 110
21. Con AVG rental_duration podemos extraer el promedio de duración de alquiler de las películas que nos da un número con bastantes decimales (4,985) por lo que reejecutamos la query incluyendo ROUND y nos devuelve 5. Por lo que podemos concluir que son 5 el promedio de días que alquilan películas
22. Usamos ||' ' || para concatenar y añadir un espacio entre nombre y apellido. Luego le damos nombre a la columna con AS (nombre_completo)
23. Lo primero que hacemos es transformar a fecha sin hora los días de alquiler con la función DATE. Con COUNT(*) contamos todos los alquileres y damos nombre de numero_alquileres a esa nueva columna. Con GROUP BY DATE agrupamos por día de alquiler y con ORDER BY numero_alquileres DESC los ordenamos de mayor a menor, siendo el 31/07/2005 el día donde hubo más alquileres (679)
24. Extraemos primero los títulos de las películas y su duración y luego realizamos una subconsulta con SELECT para seleccionar solo aquellas de duración mayor al promedio
25. Utilizamos la función DATE_TRUNC para agrupar los alquileres por mes, ignorando el día, minuto y segundo, así nos podremos centrar en lo que nos piden que es el mes. calculamos el total de alquileres por mes con COUNT(*) y luego con GROUP BY agrupamos los resultados por mes.
26. Usamos AVG, STDDEV y VARIANCE para calcular promedio, desviación estándar y varianza del total pagado. En promedio los clientes se gastan 4,2€ cada uno. Dichos pagos se desvían +-2,36€ respecto al promedio. Calculando la varianza corroboramos la dispersión entre los importes pagados por los clientes. 
27. Primero extraemos los títulos de las películas y su precio. Luego incluimos una subconsulta después del WHERE para que calcule el precio medio y solo nos muestre las películas con un precio mayor al mismo.
28. Extraemos los actor_id y los agrupamos con GROUP BY, lo que nos obliga a usar HAVING para introducir la condición de COUNT(film_id)>40
29.Usamos LEFT JOIN para extraer todos los títulos de película, independientemente de que estén o no en el inventario y usamos GROUP BY para agrupar por título
30.Necesitamos primero contabilizar el número de películas de la tabla film_actor: COUNT(film_actor.film_id). Luego tenemos que unir dos tablas (actor, film_actor) para extraer los datos solicitados con JOIN y con GROUP BY los agrupamos por actor. 
31.Primero extraemos el título de la película y todos los actores de la tabla film, luego con LEFT JOIN vinculamos tres tablas (film, film_actor y actor), siendo la principal film de donde extraemos películas, de manera que se muestren todas aunque no tengan actores implicados.
32. Es el inverso del apartado anterior, primero extraemos todos los actores y con LEFT JOIN unimos tres tablas (actor, film_actor y film), de manera que el nombre del actor se priorice y por tanto se muestren todos los actores con independencia de que no tengan película asociada
33. Para poder encontrar todas las películas con independencia de que se hayan alquilado alguna vez o no, y los registros de alquiler (si es que lo hay), hacemos LEFT JOIN y unimos la información de tres tablas (film, inventory y rental) para extraer lo solicitado
34. Unimos la información de la tabla payment y customer con JOIN y con SUM(payment.amount) calculamos el total gastado. Luego lo ordenamos de mayor a menor con ORDER BY DESC, con GROUP BY agrupamos por cliente y con LIMIT 5 seleccionamos solo los 5 que más gastaron.
35. Extraemos de la tabla actor el nombre y apellidos de los actores y con WHERE condicionamos a que el primer nombre sea Johnny. Solo se muestran dos (Johnny Cage y Johnny Lollobrigida)
36. Con la función AS logramos modificar el nombre de las columnas first_name y last_name por Nombre y Apellido.
37. Con MIN y MAX obtenemos el actor_id más bajo (1) y el más alto (200)
38. Con COUNT(*) podemos extraer el total de actores
39. Seleccionamos primero todos los nombres y apellidos de los actores y con ORDER BY last_name ASC los ordenamos por apellido de forma ascendente. 
40. Con la función LIMIT extraemos solo las 5 primeras películas de la tabla film
41. Contamos primero cuantos nombres hay de cada con COUNT(*) first_name, luego agrupamos por nombre y luego los ordenamos por la cantidad de repeticiones. Los nombres más repetidos son Kenneth, Penélope y Julia, todos los cuales se repiten 4 veces que es lo máximo. 
42. Unimos con JOIN las tablas de rental y customer para encontrar lo solicitado
43. Usamos LEFT JOIN para unir la información de dos tablas (customer y rental) porque queremos encontrar todos los clientes, con independencia de que hayan alquilado alguna vez o no
44. Esta consulta con CROSS JOIN combina cada película con cada una de las categorías que existen. Esto no ocurre en la vida real, pues una película no pertenece a todas las categorías existentes. Por tanto esta consulta no aporta ningún valor analítico.
45. Para contar solo una vez los actores que aparecen en películas de acción y no por cada película de acción en la que aparecen usamos SELECT DISTINCT. Para extraer la información requerida necesitamos unificar con JOIN varias tablas (actor, film_actor,film, film_category y category. Por último, con WHERE incluimos el condicionante de que category sea 'Action'.
46. Usamos LEFT JOIN para unir la información de la tabla actor y film_actor, para que muestre todos los actores y con WHERE añadimos la condición de que film_actor.actor_id IS NULL para que nos devuelva solo los actores que no hayan participado en ninguna película. La consulta no da resultados, por lo que todos los actores en la BBDD tiene alguna película asociada. 
47. Unimos con JOIN las tablas actor y film_actor. Usamos COUNT(film_actor.film_id) para calcular cuántas películas ha hecho cada actor y con GROUP BY las agrupamos por actor. En esta BBDD la actriz Susan Davis es la que aparece en más películas (54)
48. Creamos la vista actor_num_peliculas con CREATE VIEW. Seleccionamos nombre y apellidos de los actores y con COUNT(film_actor.film_id) calculamos el número de películas de los mismos, para ello necesitamos usar JOIN y unir la tabla actor con film_actor. Luego con GROUP BY agrupamos resultados por nombre y apellidos. Al ir a comprobar que todo el conjunto de consultas se pudieran lanzar sin problema y dieran resultados, vemos que esta consulta justo da error porque ya encuentra la vista actor_num_peliculas. Vemos que tenemos la opción de usar la función DROP VIEW IF EXISTS para hacer que la borre si la encuentra y luego la vuelva a crear, así evitar problemas al ejecutar todo el script.  
49. Extraemos nombre y apellidos de los clientes y con COUNT(rental.rental_id) calculamos el total de alquileres. Unimos con JOIN las tablas customer y rental, con GROUP BY agrupamos por cliente y con ORDER BY DESC lo ordenamos de mayor a menor n.º de alquileres. Eleanor Hunt es la clienta con mayor n.º de alquileres (46)
50. Usamos SUM(film.length) para sumar la duración de todas las películas. Unimos las tablas film, film_category y category con JOIN y usamos la función WHERE para añadir el condicionante de que la categoría sea 'Action'
51. Con la función CREATE TEMP TABLE creamos la tabla temporal solicitada. 
52. Con la función CREATE TEMP TABLE creamos la tabla temporal solicitada. Con JOIN unificamos varias tablas (film, rental e inventory). Agrupamos con GROUP BY resultados por título e id de película, lo cual nos obliga a usar el condicionante HAVING COUNT(rental.rental_id) >= 10 para limitar los resultados a aquellos con un n.º de alquileres superior o igual a 10. 
53. Usamos la función SELECT DISTINCT para extraer las películas alquiladas (y aunque se haya alquilado la misma varias veces solo aparezca una sola vez). Con JOIN unimos la información de varias tablas (customer, rental, inventory y film). Con WHERE y AND añadimos varias condiciones: que el nombre sea Tammy, su apellido sea Sanders y rental.return_date IS NULL. Ordenamos por título de película alfabéticamente con ORDER BY ASC. Comprobamos que Lust Lock, Sleepy Japanese y Trouble date son las películas que aún no ha devuelto Tammy Sanders. 
54. Usamos la función SELECT DISTINCT para extraer los actores (y aunque dicho actor aparezca en varias películas solo aparezca una vez). Unificamos con JOIN los datos de varias tablas (actor, film_actor, film, film_category y category). Con WHERE condicionamos a que solo aparezcan las películas de categoría 'Sci-Fi' y con ORDER BY ASC ordenamos resultados por apellido del actor alfabéticamente. 
55. Esta consulta tiene varios pasos:
	1. SELECT DISTINCT para mostrar todos los actores únicos (que no se repita ninguno). 
	2. JOIN	para unir la data de varias tablas (actor, film_actor, inventory y rental)
	3. WHERE para añadir un condicionante a la consulta 
	4. Subconsulta dentro de WHERE para extraer la fecha de la primera vez que se alquiló Spartacus Cheaper con SELECT MIN 	(rental.rental_date) [primera vez que se alquila] y con WHERE film_title = 'SPARTACUS CHEAPER' para seleccionar dicha película
	5. ORDER BY para ordenar alfabéticamente los resultados por apellido del actor
Nosotros hemos querido comprobar que los resultados que nos devolvía la consulta eran correctos. Para ello ejecutamos dos consultas separadas. La primera para saber la primera vez que se alquiló Spartacus Cheaper (8/07 a las 6:43h) y la segunda para ver las fechas de alquiler que aparecen en nuestra consulta y verificar que efectivamente son posteriores a esa fecha. 
56. Primero extraemos todos los actores. Realizamos luego una subconsulta con WHERE NOT EXISTS y SELECT 1 para poder excluir a los actores que hayan actuado en al menos una película de la categoría 'Music'. Vemos que varios actores no han actuado en películas de 'Music'.
57. Usamos SELECT DISTINCT para extraer las películas únicas (no repetidas). Unificamos con JOIN la data de las tablas film, inventory y rental. Con WHERE y AND añadimos dos condicionantes: que la película ya se haya devuelto y que entre la fecha de alquiler y la de devolución hayan pasado más de 8 días (rental.return_date - rental.rental_date > INTERVAL '8 days')
58. Usamos SELECT DISTINCT para extraer las películas únicas (no repetidas). Unificamos con JOIN la data de las tablas film, film_category y category. Añadimos condicionante con WHERE para extraer solo las de la categoría 'Animation'.
59. Primero extraemos todas las películas y su duración. Luego ejecutamos una subconsulta con WHERE para encontrar solo aquellas cuya duración sea igual a la de la película Dancing Fever. Vemos que hay siete películas además de la misma con la misma duración (144 min). Usamos ORDER BY ASC para ordenar los resultados por el título de película alfabéticamente. 
60. Primero extraemos todos los clientes. Usamos JOIN para unificar varias tablas (customer, rental e inventory). Con GROUP BY agrupamos resultados por cliente, lo cual nos obliga a usar HAVING para introducir el condicionante. Usamos COUNT(DISTINCT) para que se contabilicen solo una vez las películas (por si alguna película fue alquilada más de una vez por el mismo cliente) y >=7 para indicar que sean igual o más de 7 distintas. Por último, usamos ORDER BY ASC para ordenar alfabéticamente por apellido de cliente.
61. Extraemos el nombre de todas las categorías y renombramos con AS la columna category.name como categoría para su posterior visualización. Posteriormente unificamos con JOIN las tablas category, rental, film, film_category e inventory. Con GROUP BY agrupamos por nombre de categoría.
62. Extraemos el nombre de todas las categorías y renombramos con AS la columna category.name como categoría para su posterior visualización. Posteriormente unificamos con JOIN las tablas category, film_category y film. Añadimos WHERE para incluir el condicionante de que el año de estreno sea 2006. Agrupamos con GROUP BY por nombre de categoría. 
63. Primero extraemos todos los empleados de las tiendas (hay 2 en total) y luego hacemos CROSS JOIN para obtener todas las combinaciones posibles de empleados y tiendas existentes. Esta consulta no tiene sentido porque los empleados actualmente ya trabajan cada uno en una tienda concreta y por tanto no es real que pertenezcan a más de una. 
64. Extraemos todos los clientes primero. Luego usamos COUNT para calcular el total de peliculas alquiladas. Unimos las tablas customer y rental con LEFT JOIN para mostrar todos los clientes, independientemente de que nunca hayan alquilado películas. Agrupamos por cliente con GROUP BY. 
