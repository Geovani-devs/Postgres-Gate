# Agravity ProDev Training Center  
## Gate de Certificación - Base de datos  
**[www.agravity.dev](https://www.agravity.dev)**

El **Gate de Certificación** constituye un punto de validación técnica diseñado para evaluar la capacidad del participante para analizar problemas, investigar soluciones y resolver desafíos técnicos en contextos similares a los que se presentan en el mundo profesional.

Durante el desarrollo del Gate, el participante podrá encontrarse con escenarios, herramientas, consultas o situaciones que no necesariamente fueron explicadas de forma directa durante el entrenamiento. Esto es intencional. En la industria tecnológica es común enfrentarse a problemas nuevos que requieren investigación, análisis, documentación y capacidad de adaptación.

Por esta razón, el Gate de Certificación busca medir no únicamente la repetición de contenidos vistos durante el módulo, sino la capacidad real de enfrentar problemas técnicos, investigar soluciones y aplicar criterio profesional para resolverlos.

La aprobación del Gate de Certificación es un requisito indispensable para obtener la **Certificación de Bases de Datos**. Este Gate debe completarse y aprobarse obligatoriamente; en caso contrario, el participante no podrá recibir la certificación del módulo, independientemente de su asistencia o participación durante el proceso de entrenamiento.

Una vez finalizado el Gate de Certificación, el participante deberá enviar su entrega para revisión al correo **ev@agravity.dev**.

El Gate será evaluado mediante un proceso de revisión técnica similar al utilizado en entornos profesionales de desarrollo tecnológico. Como resultado de esta revisión, el trabajo podrá recibir uno de los siguientes estados:

- **Aprobado:** el trabajo cumple con los criterios técnicos establecidos y se considera validado.
- **Rechazado:** el trabajo no cumple con los criterios mínimos requeridos y deberá realizarse nuevamente.
- **Con solicitud de cambios:** el trabajo presenta observaciones técnicas que deben ser corregidas antes de poder ser aprobado.

**Advertencia:** Si en la revisión se detecta que **más del 20%** de las soluciones presentan errores o no son válidas, el documento será **devuelto** y se solicitará al participante que **vuelva a analizar todo** el Gate antes de una nueva entrega. Se recomienda verificar cada consulta contra la base de datos y revisar la coherencia de las respuestas antes de enviar.

En este proceso no se utilizan calificaciones numéricas ni sistemas de puntos. El objetivo es replicar una dinámica similar a la que ocurre en entornos profesionales, donde el trabajo se valida cuando cumple con los estándares requeridos o se devuelve para corrección.

Este enfoque busca fomentar en los participantes una cultura de investigación, pensamiento crítico, autonomía técnica y mejora continua, habilidades esenciales para desenvolverse en el sector tecnológico.

**Formato de entrega:** debes devolver el mismo archivo **Cate_de_certificación_soluciones.md** (agregandole la palabra de ultimo _soluciones.md) con tus consultas y soluciones **incrustadas** en la sección **Solución** de cada problema. Envía ese archivo al correo **ev@agravity.dev**. En el documento de problemas con soluciones encontrarás un ejemplo de cómo debe quedar cada respuesta.

---

## Requisitos: base de datos con Docker

Para realizar los ejercicios, **la base de datos debe levantarse con Docker**. Debes usar la misma imagen con la que se han probado los ejercicios, así el esquema y los datos coinciden.

### Imagen Docker (origen oficial)

| Dato | Valor |
|------|--------|
| **Imagen** | `mujz/pagila` |
| **Origen** | [Docker Hub — mujz/pagila](https://hub.docker.com/r/mujz/pagila) |

### Levantar la base de datos

**Crear y arrancar el contenedor:**

```bash
docker run -d \
  --name nivel1-pagila-postgresql \
  -p 5432:5432 \
  -e POSTGRES_PASSWORD=postgres \
  mujz/pagila
```

---

# 147 Problemas SQL — Pagila (PostgreSQL)

Cada ítem es una solicitud real de desarrollo. Responde con la consulta o el objeto SQL adecuado (SELECT, INSERT, UPDATE, DELETE, vista, trigger, vista materializada, etc.).  
---

## Problema 0 — Ejemplo de cómo responder (no se evalúa)

**Enunciado:** En la pantalla de detalle de película se debe mostrar también la categoría. Se requiere la consulta que devuelva título de película y nombre de categoría usando las tablas `film`, `film_category` y `category`.

**Indicación:** Tablas `film`, `film_category` y `category`. Une film con film_category por `film_id`, y film_category con category por `category_id`. Devuelve el título de la película y el nombre de la categoría.

**Cómo debes responder en el archivo de entrega:** En **problemas_pagila_con_soluciones.md**, en la sección **Solución** de cada problema, escribe tu consulta SQL dentro de un bloque de código. El código debe estar **debidamente indentado**: en consultas con varias líneas (JOINs, WHERE, ORDER BY, etc.) usa sangrías para alinear cláusulas y columnas. Ejemplo:

```sql
SELECT f.title,
       c.name AS categoria
FROM film f
JOIN film_category fc ON f.film_id = fc.film_id
JOIN category c ON fc.category_id = c.category_id
ORDER BY f.title;
```

El Problema 0 está resuelto arriba como referencia (consulta con JOINs e indentación). Los problemas 1 a 147 debes resolverlos tú, incrustar cada respuesta en la sección **Solución** del documento con soluciones, con código correctamente indentado, antes de enviar.

---

## NIVEL BÁSICO (1–17)

1. El desarrollador backend solicita una consulta que devuelva el nombre y apellido de todos los actores para alimentar el listado del panel de administración.  
   **Indicación:** Tabla `actor`. Las columnas que necesitas son `first_name` y `last_name`; no hace falta filtrar, solo seleccionar.

2. En el catálogo web se debe mostrar solo las películas con duración mayor a 120 minutos. Se requiere la consulta que devuelva los títulos.  
   **Indicación:** Tabla `film`. Filtra por la columna `length` (> 120) y devuelve `title`.

3. Marketing necesita localizar a los clientes con apellido exactamente "Williams" para hacer una campaña especial. Proporciona la consulta que devuelva nombre y apellido.  
   **Indicación:** Tabla `customer`. Usa WHERE con `last_name = 'Williams'` y selecciona `first_name` y `last_name`.

4. Para el dropdown list de categorías en el front se necesita un listado de todos los nombres de categoría ordenados alfabéticamente.  
   **Indicación:** Tabla `category`. Selecciona la columna `name` y ordena con ORDER BY name.

5. Se está desarrollando la ficha de películas y se requiere mostrar título, año de estreno y duración solo para las películas del año 2006.  
   **Indicación:** Tabla `film`. Columnas: `title`, `release_year`, `length`. Filtra por `release_year = 2006`.

6. Inventario solicita el siguiente dato: conocer el número total de películas en catálogo. Proporciona la consulta que devuelva ese conteo.  
   **Indicación:** Tabla `film`. Usa la función de agregación COUNT(*) para obtener el total de filas.

7. Para el dropdown list de países en el formulario de direcciones se necesita la lista de nombres de países ordenados alfabéticamente.  
   **Indicación:** Tabla `country`. La columna del nombre del país es `country`; ordénala alfabéticamente.

8. Comercial solicita un listado de películas con tarifa de alquiler mayor o igual a 4.99, mostrando título y tarifa, para revisar precios.  
   **Indicación:** Tabla `film`. Filtra con `rental_rate >= 4.99` y devuelve `title` y `rental_rate`.

9. El desarrollador backend necesita el nombre y apellido de los actores cuyo nombre comienza por 'A' para una funcionalidad de búsqueda por inicial.  
   **Indicación:** Tabla `actor`. Usa WHERE con un patrón tipo `first_name LIKE 'A%'` y selecciona first_name y last_name.

10. Se requiere una búsqueda por palabra clave: mostrar los títulos de películas cuya descripción contenga la palabra "shark".  
    **Indicación:** Tabla `film`. La descripción está en `description`; usa ILIKE (o LIKE) con '%shark%' para buscar sin importar mayúsculas y devuelve `title`.

11. Para el formulario de alta de películas se necesita el listado de idiomas disponibles en el sistema, ordenado por nombre.  
    **Indicación:** Tabla `language`. Selecciona la columna `name` y ordénala; es una tabla pequeña de referencia.

12. se solicita el reporte de tiendas: debe incluir el número total de clientes por tienda. Proporciona la consulta que devuelva store_id y total de clientes.  
    **Indicación:** Tabla `customer`. Agrupa por `store_id` y usa COUNT(*) para el total de clientes por grupo.

13. Ventas solicita un listado de películas con coste de reemplazo entre 15 y 25 (incluidos), mostrando título y coste de reemplazo.  
    **Indicación:** Tabla `film`. Filtra `replacement_cost` con BETWEEN 15 AND 25 y devuelve `title` y `replacement_cost`.

14. Se va a dar de alta un nuevo actor desde el panel: nombre "Juan", apellido "Pérez". Se requiere el INSERT en la tabla `actor` (incluir `last_update` con la fecha actual).  
    **Indicación:** Tabla `actor`. INSERT con first_name, last_name y last_update (usa NOW() para la fecha). actor_id es SERIAL, se genera solo.

15. El alta del actor "Juan Pérez" fue errónea y se debe revertir. Se solicita el DELETE que elimine ese actor de la tabla `actor`.  
    **Indicación:** Tabla `actor`. DELETE WHERE first_name = 'Juan' AND last_name = 'Pérez' para eliminar solo esa fila.

16. Un cliente reportó que su apellido está mal; se debe corregir el apellido del cliente con `customer_id = 1` a "García". Proporciona el UPDATE en `customer`.  
    **Indicación:** Tabla `customer`. UPDATE SET last_name = 'García' (y last_update = NOW() si existe) WHERE customer_id = 1.

17. En la pantalla de detalle de película se debe mostrar también la categoría. Se requiere la consulta que devuelva título de película y nombre de categoría (usar `film`, `film_category` y `category`).  
    **Indicación:** Tablas `film`, `film_category`, `category`. film se relaciona con category a través de film_category (film_id y category_id). Haz JOIN entre las tres y devuelve title y name de categoría.

---

## NIVEL MEDIO (18–34)

18. El módulo de facturación necesita el listado de clientes que han realizado al menos un pago (nombre y apellido, sin repetidos) para enviar comunicaciones.  
    **Indicación:** Tablas `customer` y `payment`. Relación por customer_id. Usa JOIN y DISTINCT en first_name y last_name para no repetir clientes.

19. Para el catálogo se debe mostrar en cada película cuántos actores tiene. Se solicita la consulta que devuelva título de película y número de actores (solo películas con al menos un actor).  
    **Indicación:** Tablas `film` y `film_actor`. JOIN por film_id, agrupa por película (film_id, title) y usa COUNT(actor_id). Ordena por cantidad descendente si conviene.

20. Se va a exponer en una API un subconjunto de películas de alto valor. Se requiere crear una vista `v_peliculas_caras` con film_id, title, rental_rate y replacement_cost para películas con replacement_cost mayor a 25.  
    **Indicación:** Tabla `film`. CREATE VIEW v_peliculas_caras AS SELECT film_id, title, rental_rate, replacement_cost FROM film WHERE replacement_cost > 25.

21. En la ficha de la película "ACADEMY DINOSAUR" se deben listar los actores que participan. Proporciona la consulta que devuelva nombre y apellido de dichos actores.  
    **Indicación:** Tablas `actor`, `film_actor`, `film`. Une actor con film vía film_actor; filtra por film.title = 'ACADEMY DINOSAUR' y devuelve first_name y last_name del actor.

22. El dashboard de clientes debe mostrar el total gastado por cada cliente. Se solicita la consulta que devuelva customer_id, nombre, apellido y total de ingresos (suma de amount en payment).  
    **Indicación:** Tablas `customer` y `payment`. JOIN por customer_id, agrupa por cliente y usa SUM(p.amount). Ordena por total descendente.

23. Durante la revisión del catálogo se detectó que algunas películas podrían no tener categoría asignada. Se requiere la consulta que liste las películas sin ningún registro en `film_category` (LEFT JOIN y condición NULL).  
    **Indicación:** Tablas `film` y `film_category`. Haz LEFT JOIN film con film_category por film_id; WHERE film_category.film_id IS NULL devuelve las películas sin categoría.

24. Se va a incorporar la categoría "Documental" al catálogo. Se solicita el INSERT en la tabla `category` (incluir `last_update`).  
    **Indicación:** Tabla `category`. Columnas: name, last_update (NOW()). category_id es SERIAL.

25. La categoría "Documental" ya no se usará. Se solicita el DELETE que la elimine de la tabla `category` por nombre.  
    **Indicación:** Tabla `category`. DELETE WHERE name = 'Documental'. Revisa si hay film_category que la referencie; si hay restricción, habría que borrar antes esas filas.

26. Para un reporte offline se necesita una tabla `peliculas_por_idioma` con el nombre del idioma y la cantidad de películas. Crear la tabla a partir de una consulta sobre `film` y `language`.  
    **Indicación:** Tablas `language` y `film`. LEFT JOIN language con film por language_id, agrupa por idioma (name), COUNT(film_id). CREATE TABLE peliculas_por_idioma AS con esa consulta.

27. En la ficha de película se debe mostrar el idioma. Se requiere la consulta que devuelva título de película y nombre del idioma (film y language).  
    **Indicación:** Tablas `film` y `language`. JOIN por language_id; devuelve film.title y language.name.

28. Compras solicita las 10 películas con mayor coste de reemplazo (título y replacement_cost, ordenado de mayor a menor) para priorizar seguros.  
    **Indicación:** Tabla `film`. SELECT title, replacement_cost ORDER BY replacement_cost DESC LIMIT 10.

29. El módulo de fidelización debe mostrar cuántos alquileres ha realizado cada cliente. Se solicita la consulta con customer_id, nombre, apellido y cantidad de alquileres (solo clientes con al menos uno).  
    **Indicación:** Tablas `customer` y `rental`. JOIN por customer_id, agrupa por cliente, COUNT(rental_id). Ordena por cantidad descendente.

30. En el informe de sedes se deben listar las ciudades con su país. Proporciona la consulta que una `city` y `country` y devuelva ciudad y país.  
    **Indicación:** Tablas `city` y `country`. city tiene country_id; JOIN y devuelve city.city y country.country. Ordena por país y ciudad.

31. Para el programa de clientes premium se necesita una vista `v_top_clientes` con los clientes que han gastado más de 150 en pagos: customer_id, nombre, apellido y total gastado.  
    **Indicación:** Tablas `customer` y `payment`. JOIN, GROUP BY cliente, SUM(amount), y en la vista filtra con HAVING SUM(amount) > 150.

32. Se ha decidido bajar el precio de alquiler de "ACADEMY DINOSAUR" a 2.99. Se solicita el UPDATE en la tabla `film` para ese título.  
    **Indicación:** Tabla `film`. UPDATE SET rental_rate = 2.99, last_update = NOW() WHERE title = 'ACADEMY DINOSAUR'.

33. RR. HH. necesita el listado de empleados con su dirección completa (calle, distrito, ciudad). Proporciona la consulta que una staff, address y city.  
    **Indicación:** Tablas `staff`, `address`, `city`. staff tiene address_id; address tiene city_id. Dos JOINs y devuelve first_name, last_name, address, district, city.

34. El reporte de categorías debe mostrar cuántas películas tiene cada categoría (nombre de categoría y cantidad), ordenado por cantidad descendente.  
    **Indicación:** Tablas `category` y `film_category`. LEFT JOIN para incluir categorías sin películas; agrupa por categoría y COUNT(film_id). Ordena por cantidad DESC.

---

## NIVEL AVANZADO (35–50)

35. Operaciones solicita una tabla de resumen `resumen_inventario` con store_id, nombre de tienda y total de copias en inventario, para cruzar con proveedores. Crear la tabla a partir de `inventory` y `store`.  
    **Indicación:** Tablas `store` e `inventory`. LEFT JOIN store con inventory por store_id, agrupa por tienda, COUNT(inventory_id). CREATE TABLE resumen_inventario AS con esa consulta.

36. El area de contabilidad quiere un reporte de los clientes que nunca han realizado un pago (para campaña de activación). Se requiere la consulta usando `customer` y `payment` (LEFT JOIN y WHERE payment_id IS NULL).  
    **Indicación:** Tablas `customer` y `payment`. LEFT JOIN customer con payment por customer_id; WHERE payment.payment_id IS NULL devuelve clientes sin ningún pago.

37. Para el exportador de catálogo se necesita por cada película: título, idioma y categoría (una fila por combinación si tiene varias categorías). Usar film, language, film_category y category.  
    **Indicación:** Tablas `film`, `language`, `film_category`, `category`. JOIN film con language, con film_category y con category; cada película puede salir varias veces si tiene varias categorías.

38. Se va a destacar en la web a los actores más prolíficos. Se solicita crear la vista `v_actores_populares` con actores que han participado en más de 15 películas (actor_id, nombre, apellido, cantidad de películas).  
    **Indicación:** Tablas `actor` y `film_actor`. JOIN, GROUP BY actor, COUNT(film_id), y en la vista usa HAVING COUNT(film_id) > 15.

39. Solicitan un reporte de las películas cuya duración supera la duración media del catálogo (mostrar título y length).  
    **Indicación:** Tabla `film`. Usa una subconsulta en el WHERE: length > (SELECT AVG(length) FROM film). Devuelve title y length.

40. Se está cargando una película de prueba desde el panel: título "Mi Película Test", language_id 1, rental_duration 3, rental_rate 2.99, replacement_cost 19.99. El resto de columnas obligatorias con valores coherentes (description, release_year, length, rating según corresponda; last_update NOW(); fulltext con to_tsvector del título).  
    **Indicación:** Tabla `film`. INSERT indicando todas las columnas obligatorias: description NULL, release_year NULL, length NULL, rating NULL, last_update NOW(), fulltext to_tsvector('english', 'Mi Película Test'). Revisa si hay más NOT NULL en el esquema.

41. La película de prueba "Mi Película Test" debe eliminarse. Considerar claves foráneas (film_actor, film_category, inventory); proporcionar los DELETE necesarios y luego el DELETE de la película.  
    **Indicación:** Primero DELETE en `film_actor` y `film_category` WHERE film_id = (SELECT film_id FROM film WHERE title = 'Mi Película Test'). Si hay filas en inventory/rental, tratarlas según las reglas del negocio. Luego DELETE FROM film WHERE title = 'Mi Película Test'.

42. El informe de perfil de cliente debe mostrar nombre completo, dirección (calle y ciudad) y total gastado. Solo clientes con al menos un pago. Usar customer, address, city y payment.  
    **Indicación:** Tablas `customer`, `address`, `city`, `payment`. customer → address → city; customer → payment. JOIN las cuatro, agrupa por cliente y dirección, SUM(amount).

43. Para un análisis de contenido largo se necesita una tabla `peliculas_largas` con las películas de duración mayor a 150 minutos (film_id, title, length, rental_rate). Crear la tabla a partir de una consulta.  
    **Indicación:** Tabla `film`. CREATE TABLE peliculas_largas AS SELECT film_id, title, length, rental_rate FROM film WHERE length > 150.

44. Atención al cliente solicita un reporte de los alquileres aún no devueltos (return_date NULL). Se solicita la consulta que devuelva rental_id, rental_date, customer_id e inventory_id.  
    **Indicación:** Tabla `rental`. WHERE return_date IS NULL y devuelve rental_id, rental_date, customer_id, inventory_id. Ordena por rental_date DESC.

45. se necesita que el dashboard que se tiene dentro del sistema de tiendas, por cada tienda debe mostrar, el número de pagos y el importe total. Usar store, staff y payment, agrupando por tienda.  
    **Indicación:** Tablas `store`, `staff`, `payment`. store → staff (store_id); staff → payment (staff_id). LEFT JOIN para incluir tiendas sin pagos, agrupa por store, COUNT y SUM(amount).

46. Para la sección "Películas por actor" se requiere una vista `v_peliculas_por_actor` con nombre y apellido del actor, título de la película y nombre de la categoría (actor, film_actor, film, film_category, category).  
    **Indicación:** actor → film_actor → film → film_category → category. JOIN las cinco tablas; la categoría puede ser LEFT JOIN si una película no tiene categoría. Devuelve first_name, last_name, title, category name.

47. El equipo de reporteria necesita detectar películas con exactamente 2 categorías asignadas. Se solicita la consulta que devuelva título y número de categorías.  
    **Indicación:** Tablas `film` y `film_category`. JOIN, GROUP BY film (film_id, title), COUNT(category_id), y filtra con HAVING COUNT(...) = 2.

48. Se ha definido un coste de reemplazo estándar de 20.99 para la categoría "Horror". Se solicita el UPDATE en `film` para todas las películas de esa categoría (subconsulta o JOIN).  
    **Indicación:** Tablas `film`, `film_category`, `category`. Identifica los film_id cuya category_id corresponde a 'Horror' (SELECT de category WHERE name = 'Horror'). UPDATE film SET replacement_cost = 20.99 WHERE film_id IN (subconsulta) o con UPDATE FROM.

49. El informe de rendimiento por categoría debe mostrar el top 5 de categorías por ingresos totales (suma de payment.amount), relacionando payment → rental → inventory → film → film_category → category. Mostrar nombre de categoría y total.  
    **Indicación:** Cadena: category → film_category → film → inventory → rental → payment. JOIN todas, agrupa por categoría, SUM(amount), ORDER BY total DESC LIMIT 5.

50. Para el CRM se necesita una tabla `estadisticas_cliente` con customer_id, nombre completo, total de alquileres, total pagado y fecha del último pago. Crear la tabla a partir de customer, rental y payment.  
    **Indicación:** Tabla base `customer`. Puedes usar subconsultas para total alquileres (COUNT en rental), total pagado (SUM en payment) y MAX(payment_date), o JOINs con GROUP BY. Nombre completo: first_name || ' ' || last_name. CREATE TABLE estadisticas_cliente AS.

---

## TRIGGERS (51–60)

51. Se exige que en toda modificación de un actor quede actualizada la columna `last_update`. Se solicita implementar un trigger BEFORE UPDATE en `actor` que asigne NEW.last_update = NOW().  
    **Indicación:** Tabla `actor`. Crea una función que retorne TRIGGER y en el cuerpo haga NEW.last_update := NOW(); RETURN NEW;. Luego CREATE TRIGGER BEFORE UPDATE ON actor FOR EACH ROW EXECUTE PROCEDURE nombre_funcion();

52. Auditoría requiere registrar cada nuevo pago. Se debe crear la tabla `auditoria_payment` (id SERIAL, payment_id, accion varchar, monto, fecha_auditoria) y un trigger AFTER INSERT en `payment` que inserte una fila con los datos del pago insertado.  
    **Indicación:** Nueva tabla `auditoria_payment`; tabla disparadora `payment`. En la función del trigger (AFTER INSERT) haz INSERT INTO auditoria_payment (payment_id, accion, monto) VALUES (NEW.payment_id, 'INSERT', NEW.amount); RETURN NEW;

53. La columna `fulltext` de `film` debe mantenerse sincronizada cuando cambien título o descripción. Se solicita un trigger BEFORE UPDATE en `film` que asigne NEW.fulltext = to_tsvector('english', COALESCE(NEW.title,'') || ' ' || COALESCE(NEW.description,'')).  
    **Indicación:** Tabla `film`. Trigger BEFORE UPDATE; si cambió title o description, asigna NEW.fulltext con to_tsvector. Compara OLD.title/description con NEW para no sobrescribir sin necesidad.

54. El director del establecimiento solicita que la tarifa de alquiler de una película sea siempre mayor que 0. Se requiere un trigger BEFORE INSERT (y UPDATE) en `film` que valide rental_rate > 0 y lance excepción si no se cumple.  
    **Indicación:** Tabla `film`. Trigger BEFORE INSERT OR UPDATE. En la función: IF NEW.rental_rate IS NOT NULL AND NEW.rental_rate <= 0 THEN RAISE EXCEPTION '...'; END IF; RETURN NEW;

55. No se debe permitir borrar un cliente que tenga pagos asociados. Se solicita un trigger BEFORE DELETE en `customer` que impida el borrado si existe al menos un registro en `payment` (lanzar excepción en ese caso).  
    **Indicación:** Tablas `customer` (disparadora) y `payment`. En la función BEFORE DELETE: IF EXISTS (SELECT 1 FROM payment WHERE customer_id = OLD.customer_id) THEN RAISE EXCEPTION; END IF; RETURN OLD;

56. Se necesita un resumen en tiempo cuasi real del total cobrado: tabla `resumen_total_pagos` (total_pagos, ultima_actualizacion), inicializada con el SUM(amount) actual, y un trigger que tras INSERT o DELETE en `payment` actualice esa tabla.  
    **Indicación:** Tabla `payment` (disparadora) y tabla `resumen_total_pagos` (una fila). Inicializa con INSERT ... SELECT SUM(amount) FROM payment. Trigger AFTER INSERT OR DELETE: en INSERT suma NEW.amount al total; en DELETE resta OLD.amount; actualiza ultima_actualizacion = NOW().

57. En todo nuevo actor se debe registrar la fecha de última actualización. Se solicita un trigger BEFORE INSERT en `actor` que asigne last_update = NOW().  
    **Indicación:** Tabla `actor`. Función BEFORE INSERT: NEW.last_update := NOW(); RETURN NEW;. CREATE TRIGGER en INSERT.

58. Auditoría amplía el requisito: además de insertar en `auditoria_payment` al crear un pago, se debe registrar también cada UPDATE en `payment` (accion 'UPDATE', payment_id y monto nuevo).  
    **Indicación:** Misma tabla `auditoria_payment` del problema 52; disparador en `payment`. Crea un trigger AFTER UPDATE que haga INSERT INTO auditoria_payment (payment_id, accion, monto) VALUES (NEW.payment_id, 'UPDATE', NEW.amount); RETURN NEW;

59. Se considera crítico que no se modifiquen las claves film_id ni actor_id en `film_actor`. Se solicita un trigger BEFORE UPDATE que impida ese cambio y lance excepción si se intenta.  
    **Indicación:** Tabla `film_actor`. En BEFORE UPDATE compara NEW.film_id con OLD.film_id y NEW.actor_id con OLD.actor_id; si alguno cambió, RAISE EXCEPTION. Opcionalmente actualiza last_update.

60. Se mantiene un contador de alquileres en la tabla `contador_rentals` (una fila, columna total). Inicializar con el COUNT(*) actual de rental y crear un trigger AFTER INSERT en `rental` que incremente total en 1.  
    **Indicación:** Tabla `rental` (disparadora) y tabla `contador_rentals` (total integer). INSERT INTO contador_rentals SELECT COUNT(*) FROM rental; luego trigger AFTER INSERT que haga UPDATE contador_rentals SET total = total + 1; RETURN NEW;

---

## VISTAS MATERIALIZADAS (61–70)

PostgreSQL permite `CREATE MATERIALIZED VIEW`; se actualizan con `REFRESH MATERIALIZED VIEW nombre`.

61. Para una API de catálogo cacheada se necesita una vista materializada `mv_peliculas_con_categoria` con film_id, title y nombre de la categoría (film, film_category, category).  
    **Indicación:** Tablas `film`, `film_category`, `category`. CREATE MATERIALIZED VIEW mv_peliculas_con_categoria AS SELECT f.film_id, f.title, c.name FROM film f JOIN film_category fc ... JOIN category c ...

62. El dashboard de ingresos por cliente se alimentará de una vista materializada `mv_ingresos_por_cliente` con customer_id, first_name, last_name y total_gastado (SUM(amount) por cliente).  
    **Indicación:** Tablas `customer` y `payment`. LEFT JOIN para incluir clientes sin pagos, GROUP BY customer, SUM(amount) AS total_gastado.

63. Para el listado de actores con número de películas se solicita la vista materializada `mv_actores_con_conteo` (actor_id, first_name, last_name, cantidad_peliculas). Solo actores con al menos una película.  
    **Indicación:** Tablas `actor` y `film_actor`. JOIN, GROUP BY actor, COUNT(film_id) AS cantidad_peliculas. Ordena por cantidad DESC.

64. Operaciones solicita una vista materializada `mv_inventario_por_tienda` con store_id, nombre de tienda y total de copias en inventario (COUNT por tienda).  
    **Indicación:** Tablas `store` e `inventory`. LEFT JOIN, agrupa por store_id y name, COUNT(inventory_id).

65. Compras trabajará con un snapshot de las 100 películas de mayor coste de reemplazo. Se requiere la vista materializada `mv_top_100_peliculas_caras` (film_id, title, replacement_cost).  
    **Indicación:** Tabla `film`. SELECT film_id, title, replacement_cost ORDER BY replacement_cost DESC LIMIT 100 dentro del CREATE MATERIALIZED VIEW.

66. El informe mensual de pagos se basará en una vista materializada `mv_pagos_por_mes` con año, mes, total de pagos (COUNT) y monto total (SUM(amount)), agrupado por año y mes.  
    **Indicación:** Tabla `payment`. Usa EXTRACT(YEAR FROM payment_date) y EXTRACT(MONTH FROM payment_date), agrupa por ambos y haz COUNT(*) y SUM(amount).

67. El reporte de ingresos por categoría se alimentará de una vista materializada `mv_ingresos_por_categoria` (category_id, nombre_categoria, total_ingresos) usando la cadena payment → rental → inventory → film → film_category → category.  
    **Indicación:** Une category → film_category → inventory → rental → payment (o desde payment hacia atrás). Agrupa por categoría y SUM(payment.amount). LEFT JOIN para categorías sin ingresos.

68. Para envíos se necesita un snapshot de direcciones de clientes: vista materializada `mv_direcciones_clientes` con customer_id, first_name, last_name, address, district, city, country (customer, address, city, country).  
    **Indicación:** customer → address → city → country. JOIN en cadena y selecciona las columnas indicadas. Ordena por customer_id.

69. El exportador de catálogo requiere una vista materializada `mv_peliculas_idioma_categoria` con film_id, title, idioma y categoría (una fila por combinación película–categoría).  
    **Indicación:** film → language (por language_id); film → film_category → category. JOIN y devuelve film_id, title, language.name, category.name. Una película puede repetirse por cada categoría.

70. E El dashboard de ventas por tienda se alimentará de la vista materializada \mv_ventas_por_tienda`, que debe incluir `store_id`, `nombre_tienda`, `num_pagos` e `ingreso_total`. La información debe obtenerse por tienda a partir de la relación entre `store`, `staff` y `payment`.`
    **Indicación:** store → staff → payment. LEFT JOIN para tiendas sin ventas; agrupa por store, COUNT(payment_id) y SUM(amount).

---

## CINCO TABLAS NUEVAS, RELACIONES E INSERTS (71–80)

71. Se va a extender el modelo con promociones, preferencias de cliente, metas por tienda, valoraciones de películas e historial de cambios de precio. Se solicita crear las 5 tablas con PK y FK hacia Pagila: (1) **promocion** (sin FK), (2) **cliente_preferencia** FK customer y category, (3) **meta_tienda** FK store, (4) **valoracion_pelicula** FK customer y film, (5) **log_cambios_precio** FK film.  
    **Indicación:** Crea cada tabla con CREATE TABLE, SERIAL para PK, REFERENCES para las FK indicadas. Usa UNIQUE(store_id, anio, mes) en meta_tienda y UNIQUE(customer_id, category_id) en cliente_preferencia; CHECK para puntuacion 1–5 y mes 1–12 si aplica.

72. Marketing ha definido tres promociones: "Verano 2025" 10% (01/06/2025–31/08/2025), "Nuevos Clientes" 15% (01/01/2025–31/12/2025), "Fin de Año" 20% (15/12/2025–31/12/2025). Se solicita el INSERT en `promocion` para las tres.  
    **Indicación:** Tabla `promocion`. INSERT con tres filas: nombre, descuento_pct (10, 15, 20), fecha_inicio y fecha_fin en formato DATE.

73. Se van a cargar preferencias de categoría para 5 clientes (customer_id 1 a 5), asignando a cada uno una o dos category_id. Proporciona los INSERT en `cliente_preferencia`.  
    **Indicación:** Tabla `cliente_preferencia` (customer_id, category_id). Usa category_id existentes (p. ej. 1 Action, 2 Animation). Inserta varias filas respetando UNIQUE(customer_id, category_id).

74. Se definen metas de ventas para 2025: las dos tiendas (store_id 1 y 2), los 12 meses, con meta_ventas 8000 cada uno. Se solicita el INSERT en `meta_tienda`.  
    **Indicación:** Tabla `meta_tienda`. Puedes usar CROSS JOIN entre (SELECT 1 UNION SELECT 2) de tiendas y generate_series(1,12) para mes, o 24 INSERTs. store_id, anio 2025, mes 1..12, meta_ventas 8000.

75. Para probar el módulo de valoraciones se deben insertar al menos 10 valoraciones en `valoracion_pelicula` (distintos clientes y películas, puntuación 1–5, usando customer_id y film_id existentes).  
    **Indicación:** Tabla `valoracion_pelicula`. INSERT con (customer_id, film_id, puntuacion); usa IDs que existan en customer y film. fecha puede ser DEFAULT.

76. Se simulan 3 cambios de precio en películas (film_id 1, 2, 3) para probar el historial. Se solicita el INSERT en `log_cambios_precio` con rental_rate_anterior y rental_rate_nuevo que definas.  
    **Indicación:** Tabla `log_cambios_precio`. Inserta tres filas con film_id 1, 2, 3 y valores numéricos para rental_rate_anterior y rental_rate_nuevo (p. ej. 2.99 → 3.99).

77. En la web se deben mostrar solo las promociones vigentes (fecha actual entre fecha_inicio y fecha_fin). Proporciona la consulta usando CURRENT_DATE.  
    **Indicación:** Tabla `promocion`. SELECT ... WHERE CURRENT_DATE BETWEEN fecha_inicio AND fecha_fin. Devuelve las columnas que necesite el front.

78. El perfil de cliente debe mostrar nombre, apellido, categoría preferida y fecha de registro de la preferencia. Se solicita la consulta que una cliente_preferencia, customer y category.  
    **Indicación:** Tablas `cliente_preferencia`, `customer`, `category`. JOIN por customer_id y category_id; devuelve first_name, last_name, category.name, fecha_registro.

79. Para el informe de cumplimiento de metas se necesita, para tienda 1, año 2025 y mes 5: meta_ventas, total real de pagos (SUM(amount) donde el staff es de esa tienda y payment_date en mayo 2025), y si se superó o no la meta. Proporciona la consulta.  
    **Indicación:** Tablas `meta_tienda`, `staff`, `payment`. JOIN meta_tienda con staff por store_id; staff con payment por staff_id. Filtra store_id=1, anio=2025, mes=5 y EXTRACT año/mes de payment_date. Agrupa y compara SUM(amount) con meta_ventas; usa CASE para "Sí"/"No".

80. El listado de valoraciones en el panel debe mostrar cliente (nombre y apellido), película (título) y puntuación. Se solicita crear la vista `v_valoraciones_detalle` que una valoracion_pelicula con film y customer (columnas: customer_id, first_name, last_name, film_id, title, puntuacion, fecha).  
    **Indicación:** Tablas `valoracion_pelicula`, `customer`, `film`. JOIN valoracion_pelicula con customer y con film; SELECT las columnas indicadas. Ordena por fecha o puntuación si conviene.

---

## MÓDULO EXTRA — JSONB (81–90)

En Pagila no hay tablas con JSONB; se crearán dos tablas que usan este tipo para almacenar y consultar datos semiestructurados.

81. Se requiere almacenar metadatos extensibles por película y un log de eventos. Crear: (1) Tabla **metadatos_pelicula**: `film_id` (SMALLINT, FK a film, PK), `metadatos` (JSONB). (2) Tabla **eventos_auditoria**: `id` (SERIAL PK), `entidad` (VARCHAR 50), `evento` (VARCHAR 50), `datos` (JSONB), `fecha` (TIMESTAMP DEFAULT NOW()).
82. Cargar en `metadatos_pelicula` tres filas para film_id 1, 2 y 3. El JSONB debe incluir al menos: `pais_rodaje` (texto), `tags` (array de textos, p. ej. ["drama","acción"]) y `premios` (array opcional). Usa sintaxis JSONB (ej. `'{"pais_rodaje":"USA","tags":["drama"]}'::jsonb` o `jsonb_build_object`).
83. El backend debe mostrar por cada película el país de rodaje extraído del JSONB. Consulta que devuelva `film_id`, título de la película (desde `film`) y el valor de la clave `pais_rodaje` del campo `metadatos` (operador ->>).
84. Se necesita listar las películas cuyo metadato `pais_rodaje` sea exactamente "USA". Proporciona la consulta que una `metadatos_pelicula` con `film` y filtre por el contenido JSONB.
85. Para un reporte de etiquetas se debe “expandir” el array `tags` del JSONB: cada etiqueta en una fila. Usar `jsonb_array_elements_text(metadatos->'tags')` (o equivalente) y mostrar film_id, título y cada tag en una fila.
86. Actualizar el documento JSONB de la película con film_id = 1: añadir o reemplazar la clave `premios` con el array `["Oscar", "Globo de Oro"]`. Usar `jsonb_set` o el operador || de concatenación de JSONB.
87. Obtener por cada film_id (de `metadatos_pelicula`) la lista de todas las claves de primer nivel del objeto `metadatos`, en una sola fila por película (p. ej. con `jsonb_object_keys` en una subconsulta o con `string_agg` de las keys). Alternativa: listar film_id y un array agregado de los tags de esa película usando `jsonb_agg`.
88. Listar las filas de `metadatos_pelicula` donde el JSONB contenga la clave `premios` (operador `?`). Mostrar film_id y metadatos (o metadatos->>'pais_rodaje').
89. Insertar en `eventos_auditoria` dos registros: (entidad 'film', evento 'actualizacion_metadatos', datos con JSONB como `{"film_id": 1, "usuario": "admin", "cambios": ["premios"]}`) y otro similar. Luego consultar los eventos mostrando id, entidad, evento, datos->>'film_id', datos->'cambios', fecha.
90. Crear una vista `v_peliculas_con_metadatos` que una `film` con `metadatos_pelicula` y muestre: film_id, title, metadatos->>'pais_rodaje' AS pais_rodaje, metadatos->'tags' AS tags_json (o el array como texto). Solo películas que tengan fila en metadatos_pelicula.
---

## RANKING Y CTEs (91–100)

91. Usando una CTE `total_cliente` que calcule el SUM(amount) por customer_id en `payment`, lista los clientes cuyo total gastado sea mayor a 200. Muestra customer_id y total.
92. Ranking de clientes por tienda: para cada store_id, asigna un rango (RANK o ROW_NUMBER) según el total gastado por el cliente en esa tienda. Usa payment, customer (tiene store_id) y agrupa por store_id y customer_id. Muestra store_id, customer_id, total, rango.
93. Clientes que gastan más que el promedio de todos los clientes. CTE con el promedio (AVG del total por cliente) y luego SELECT los clientes cuyo total > ese promedio.
94. Top 1 cliente por tienda (el que más ha gastado en cada tienda). Usa ROW_NUMBER() o DISTINCT ON (store_id) ordenando por total descendente.
95. Comparar totales entre años: obtén el SUM(amount) por año (EXTRACT(YEAR FROM payment_date)) y muestra año y total. Opcional: comparar con LAG(total) para ver diferencia respecto al año anterior.
96. Usando CTE, lista las películas cuyo número de actores (COUNT en film_actor) sea mayor que el promedio de actores por película.
97. Ranking de categorías por ingresos: RANK() sobre la suma de amount por categoría (payment → rental → inventory → film → film_category → category). Muestra categoría, total, rango.
98. Clientes con más alquileres que la mediana de alquileres por cliente. Usa una CTE con COUNT(rental_id) por cliente y otra con PERCENTILE_CONT(0.5) para la mediana.
99. Top 5 películas por recaudación (SUM(amount) vía payment → rental → inventory → film). Usa CTE o subconsulta y LIMIT 5.
100. Por cada actor, calcular el total de películas en que participa y el rango (RANK) dentro de su categoría favorita (asumir categoría del primer film_category de sus películas, o simplificar: ranking global de actores por cantidad de películas).
---

## CONSULTAS RECURSIVAS (101–110)

101. Generar la serie de números del 1 al 10 usando WITH RECURSIVE (cte base: SELECT 1 AS n; recursivo: SELECT n+1 FROM cte WHERE n < 10).
102. Con RECURSIVE, listar la “jerarquía” store → staff (solo un nivel): cada tienda con su manager_staff_id y el nombre del staff. Usa store y staff; la parte recursiva puede quedar trivial si solo hay un nivel, o simular dos niveles uniendo store con staff.
103. Números de Fibonacci hasta el valor 100: WITH RECURSIVE con dos columnas (n, fib) donde fib = anterior + actual.
104. Recursivo sobre categorías: si tuvieras una tabla category con parent_id (en Pagila no existe), simularías árbol. En su lugar, usa RECURSIVE para generar 1..16 (cantidad de categorías) y hacer JOIN con category para listar categorías “por nivel” (nivel = número generado).
105. Listar todos los customer_id desde 1 hasta el máximo existente en customer, usando RECURSIVE (útil para encontrar huecos). Base: SELECT MIN(customer_id) AS id FROM customer. Recursivo: SELECT id+1 FROM cte JOIN customer c ON c.customer_id = cte.id+1 o hasta MAX(customer_id).
106. Suma acumulada por año: para cada año en payment, la suma total de ese año más la de años anteriores. Usa RECURSIVE o window function SUM() OVER (ORDER BY año). Preferir window: SUM(amount) OVER (ORDER BY EXTRACT(YEAR FROM payment_date)).
107. Con RECURSIVE, expandir los “niveles” de un inventario: por cada inventory_id, nivel 1; si quisieras “niveles” ficticios, generar niveles 1 a 5 y cruzar con inventory limitado (ej. primeros 20 ítems). Alternativa: RECURSIVE que repita cada film_id tantas veces como copias en inventory (film → inventory, contar copias por film).
108. Path de categorías: usando RECURSIVE y la tabla film_category, para una película dada (film_id=1) listar todas las category_id asociadas en una sola fila (array_agg en la parte final del RECURSIVE) o como filas. Si no hay jerarquía, usar RECURSIVE para “recorrer” las categorías de esa película (una fila por categoría).
109. RECURSIVE para “días del mes”: generar las fechas de un mes (ej. febrero 2006) con RECURSIVE. Base: SELECT '2006-02-01'::date AS d. Recursivo: SELECT d+1 FROM cte WHERE d < '2006-02-28'.
110. Factorial con RECURSIVE: calcular n! para n=5. Base: SELECT 1 AS n, 1 AS fact. Recursivo: SELECT n+1, fact*(n+1) FROM cte WHERE n < 5.
---

## PERFORMANCE Y OPTIMIZACIÓN (111–120)

En cada problema se da una consulta que puede ser costosa o mal escrita. Se pide: (1) ejecutar EXPLAIN (ANALYZE) de la consulta dada y anotar el plan; (2) proponer una versión mejorada (índices, reescritura); (3) indicar si conviene algún índice y de qué tipo (B-tree, GIN, etc.).

111. Consulta dada: SELECT * FROM film WHERE title LIKE '%ACADEMY%'; (búsqueda con comodín al inicio). Explicar por qué es costosa. Mejorar con índice o con búsqueda full-text (fulltext @@ to_tsquery). ¿Qué índice conviene para búsqueda por título con LIKE 'patrón%'?
112. Consulta dada: SELECT c.*, (SELECT SUM(amount) FROM payment p WHERE p.customer_id = c.customer_id) AS total FROM customer c; (subconsulta correlacionada para 599 clientes). Reescribir con JOIN y GROUP BY. Valorar índice en payment(customer_id).
113. Consulta que filtra por EXTRACT(YEAR FROM payment_date) = 2007. Explicar por qué no usa bien un índice en payment_date. Reescribir con rango: payment_date >= '2007-01-01' AND payment_date < '2008-01-01'. ¿Índice recomendado?
114. SELECT * FROM film WHERE description ILIKE '%dinosaur%'; Sin índice en description. Proponer uso de fulltext (columna fulltext) o índice GIN para búsqueda. Reescribir la consulta.
115. Consulta con múltiples JOINs (film, film_actor, actor, film_category, category) sin filtro hasta el final. Proponer reordenar o filtrar antes (con subconsulta o CTE que reduzca filas). Analizar orden de JOINs en el plan.
116. Tabla `metadatos_pelicula`: consultas por metadatos->>'pais_rodaje'. ¿Conviene índice B-tree sobre (metadatos->>'pais_rodaje') o GIN sobre (metadatos)? Crear el índice que consideres adecuado y ejecutar EXPLAIN ANALYZE antes y después.
117. COUNT(*) sobre rental sin WHERE. ¿Secuencia o índice? En PostgreSQL COUNT(*) puede usar índice solo en ciertos casos. Comentar y proponer alternativa si se necesita contar con filtro (ej. por customer_id) e índice.
118. Ordenación ORDER BY last_name, first_name en customer sin índice. Crear índice compuesto (last_name, first_name) y comparar plan antes/después con EXPLAIN ANALYZE.
119. Consulta que usa DISTINCT sobre muchas columnas de un JOIN grande. Proponer usar EXISTS o agrupar en subconsulta para reducir filas antes del JOIN. Redactar versión mejorada.
120. En una tabla creada por ti (ej. eventos_auditoria o valoracion_pelicula), decidir qué columnas deberían tener índice según las consultas típicas (por entidad, por fecha, por customer_id). Escribir los CREATE INDEX necesarios y justificar tipo (B-tree, BRIN para fechas, etc.).
---

## TRANSACCIONES Y CONCURRENCIA (121–125)

121. Simular una transferencia entre dos “cuentas”: usar una tabla de prueba (crear `cuenta_prueba` con id, balance NUMERIC). INSERT dos filas (id 1 y 2, balance 1000 cada una). Luego en una transacción: BEGIN; UPDATE cuenta_prueba SET balance = balance - 100 WHERE id = 1; UPDATE cuenta_prueba SET balance = balance + 100 WHERE id = 2; COMMIT; Verificar balances finales.
122. Misma tabla cuenta_prueba. Ejecutar BEGIN; UPDATE ... SET balance = balance - 100 WHERE id = 1; y luego ROLLBACK; sin hacer COMMIT. Comprobar que el balance no cambió. Redactar el script completo (BEGIN, UPDATE, ROLLBACK).
123. Explicar en un comentario qué es un deadlock y cómo evitarlo (orden consistente de bloqueo, tiempo corto de transacción). Opcional: intentar provocar un deadlock en dos sesiones con cuenta_prueba (sesión 1: UPDATE id=1; sesión 2: UPDATE id=2; sesión 1: UPDATE id=2; sesión 2: UPDATE id=1;) y observar el error.
124. Leer la documentación de niveles de aislamiento (READ COMMITTED, REPEATABLE READ, SERIALIZABLE). Escribir una transacción que use SET TRANSACTION ISOLATION LEVEL REPEATABLE READ; y dentro hacer dos SELECT del mismo balance de cuenta_prueba sin COMMIT entre medias; explicar qué esperarías si otra sesión modificara la fila.
125. Transacción que inserte en eventos_auditoria y en metadatos_pelicula; si falla la segunda inserción (por restricción), debe hacerse ROLLBACK de todo. Redactar BEGIN; INSERT ...; INSERT ...; COMMIT; y una variante con excepción donde se use ROLLBACK.
---

## LOCKS Y CONCURRENCIA (126–128)

126. Explicar para qué sirve SELECT ... FOR UPDATE. Escribir una consulta que seleccione una fila de inventory por inventory_id con FOR UPDATE (ej. para “reservar” esa copia antes de insertar un rental).
127. Evitar doble alquiler: proponer el flujo (en pseudocódigo o SQL) para que dos sesiones no puedan alquilar el mismo inventory_id a la vez. Incluir BEGIN, SELECT inventory ... FOR UPDATE, INSERT INTO rental, COMMIT.
128. Consulta que liste las películas (film) con FOR UPDATE (ej. para actualizar precios en lote). Comentar el riesgo de bloquear muchas filas y alternativas (LOCK solo las filas a actualizar, o usar batch pequeño).
---

## PARTITIONING (129–131)

129. Crear una tabla particionada `payment_por_anio` (como payment) particionada por RANGE en el año de payment_date. Crear particiones para 2006 y 2007 (FOR VALUES FROM ... TO ...). Inserción: copiar filas de payment donde EXTRACT(YEAR FROM payment_date) = 2007 a la partición correspondiente (o crear tabla vacía solo como ejercicio de DDL).
130. Consulta que filtre por payment_date en un rango que caiga en una sola partición de payment_por_anio. Ejecutar EXPLAIN y comprobar que se usa “partition pruning” (solo se escanea una partición).
131. Mantenimiento: escribir el DDL para añadir una nueva partición a payment_por_anio para el año 2008. Escribir un comentario sobre cómo hacer DROP de una partición antigua (ej. para archivar).
---

## FULL TEXT SEARCH AVANZADO (132–134)

132. Búsqueda full-text en film: listar títulos donde fulltext coincida con la consulta 'action & hero' usando to_tsquery('english', 'action & hero') y el operador @@.
133. Búsqueda por frase: usar phraseto_tsquery o to_tsquery con frase entre comillas para buscar “scientist” cerca de “dinosaur” en la descripción/fulltext. Mostrar título y fragmento (usar ts_headline si está disponible).
134. Ordenar resultados por relevancia: usar ts_rank(fulltext, to_tsquery('english', 'dragon')) y ORDER BY ts_rank DESC. Listar título y el valor de ts_rank.
---

## JSONB AVANZADO (135–137)

135. Buscar películas cuyo array `tags` dentro de metadatos contenga el valor 'drama'. Usar el operador @> (contains): metadatos @> '{"tags": ["drama"]}' o comprobar con jsonb_array_elements y WHERE elem = '"drama"'.
136. Crear un índice GIN sobre la columna metadatos de metadatos_pelicula: CREATE INDEX idx_metadatos_gin ON metadatos_pelicula USING GIN (metadatos); Ejecutar una consulta que use metadatos ? 'premios' o metadatos @> '{"pais_rodaje":"USA"}' y comprobar con EXPLAIN que se usa el índice.
137. Consulta que use jsonb_path_query o extraiga el primer elemento del array tags (metadatos->'tags'->0) para las filas que tengan al menos un tag. Mostrar film_id, primer_tag.
---

## FUNCIONES DEFINIDAS POR EL USUARIO (138–140)

138. Crear una función total_cliente(p_customer_id INT) que devuelva el SUM(amount) de payment para ese customer_id. RETURNS NUMERIC. Llamarla con SELECT total_cliente(1);
139. Función que reciba film_id y devuelva el número de actores de esa película (COUNT de film_actor). RETURNS INT.
140. Función que reciba store_id y devuelva el nombre de la tienda (name de store). RETURNS VARCHAR. Si no existe, devolver NULL o lanzar excepción.
---

## SEGURIDAD EN BASE DE DATOS (141–143)

141. Crear un rol usuario_api con LOGIN (o sin LOGIN para uso en GRANT). Conceder SELECT sobre la tabla film: GRANT SELECT ON film TO usuario_api; Verificar con \dp film en psql.
142. Revocar permisos: REVOKE INSERT ON category FROM usuario_api; (asumiendo que se le había dado). Conceder solo SELECT sobre customer y payment a usuario_api.
143. Crear un rol solo_lectura que tenga SELECT sobre todas las tablas del schema public (usar GRANT SELECT ON ALL TABLES IN SCHEMA public TO solo_lectura). Comentar en la solución el uso de DEFAULT PRIVILEGES para tablas futuras.
---

## ROW LEVEL SECURITY (144–145)

144. Habilitar RLS en la tabla customer: ALTER TABLE customer ENABLE ROW LEVEL SECURITY; Crear una policy que permita SELECT solo cuando current_setting('app.user_id', true)::INT coincida con customer_id (policy FOR SELECT USING (customer_id = current_setting('app.user_id', true)::INT)).
145. Policy adicional para INSERT: solo permitir si app.user_id está definido (o una condición que prefieras). Comentar cómo probar con SET app.user_id = '1' antes de SELECT.
---

## AUDITORÍA REAL (146–147)

146. Crear tabla audit_log con columnas: table_name TEXT, operation TEXT (INSERT/UPDATE/DELETE), old_data JSONB, new_data JSONB, changed_at TIMESTAMP DEFAULT NOW(), user_name TEXT. Sin triggers aún.
147. Crear un trigger en la tabla film que después de INSERT o UPDATE o DELETE inserte en audit_log una fila con el nombre de la tabla, la operación, old_data = row_to_json(OLD)::jsonb (NULL si INSERT), new_data = row_to_json(NEW)::jsonb (NULL si DELETE). Usar una función que reciba TG_OP, OLD, NEW y haga el INSERT en audit_log.
---

## Advertencia — Uso exclusivo del material

La restricción de uso de este material **no obedece al contenido en sí**, sino al hecho de que la **estructura progresiva** (orden, secuencia y metodología de los ejercicios) es **propiedad del centro de entrenamiento tecnológico Agravity ProDev Training Center**. Dicha estructura forma parte del modelo formativo del programa.

Este documento es **exclusivamente** para las personas aspirantes al **programa de entrenamiento de Arquitecto de Software (stack MEAN)** de Agravity ProDev Training Center. La academia cuenta con los **especialistas adecuados** para el diseño, seguimiento y evaluación del programa.

**No está permitido** compartir este material —total o parcial— con otras instituciones, programas, personas ajenas al programa o canales públicos (sitios web, redes, repositorios, etc.).

Si se detecta que el documento ha sido compartido fuera del ámbito del programa, se dará **seguimiento** al hecho. Los **especialistas en ciberseguridad** del centro podrán intervenir para conocer la **trazabilidad del archivo** y determinar **cómo llegó a compartirse** (origen, canales, destinatarios). Dicho seguimiento puede implicar:

- **Destitución** (descalificación) de la persona dentro del programa, o  
- **Otra penalización** determinada según las políticas del programa.

El objetivo de esta medida es preservar la integridad del proceso de certificación y el uso adecuado del material formativo. Se solicita a los participantes hacer uso responsable y confidencial del mismo.
