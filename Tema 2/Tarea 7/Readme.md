# Tarea 7
## Paso 1
Primero iniciamos la terminal y cargamos el fichero de sql para cargar als tablas
```bash
C:\Users\ese_s\Desktop\project\tarea5\tarea1>sqlite3 tarea7.db
SQLite version 3.49.1 2025-02-18 13:38:58
Enter ".help" for usage hints.
sqlite> .read base-datos-clientes1.sql
```
### Listar los coches vendidos con sus modelos y precios, junto con los nombres de los clientes que los compraron.
```sql
sqlite> SELECT c.modelo, c.precio, cl.nombre
   ...> FROM ventas v
   ...> JOIN coches c ON v.id_coche = c.id_coche
   ...> JOIN clientes cl ON v.id_cliente = cl.id_cliente;
+----------------+---------+-----------------+
|     modelo     | precio  |     nombre      |
+----------------+---------+-----------------+
| Sedán 2022     | 25000.0 | Juan Pérez      |
| Hatchback 2021 | 22000.0 | María Gómez     |
| SUV 2023       | 30000.0 | Carlos López    |
| Coupé 2022     | 28000.0 | Ana Martínez    |
| Camioneta 2023 | 32000.0 | Pedro Rodríguez |
| Compacto 2021  | 20000.0 | Laura Sánchez   |
| Híbrido 2022   | 27000.0 | Miguel González |
| Deportivo 2023 | 35000.0 | Isabel Díaz     |
| Eléctrico 2021 | 40000.0 | Elena Torres    |
| Sedán 2022     | 25000.0 | Juan Pérez      |
| Hatchback 2021 | 22000.0 | María Gómez     |
| SUV 2023       | 30000.0 | Carlos López    |
| Coupé 2022     | 28000.0 | Ana Martínez    |
| Camioneta 2023 | 32000.0 | Pedro Rodríguez |
| Compacto 2021  | 20000.0 | Laura Sánchez   |
| Híbrido 2022   | 27000.0 | Miguel González |
| Deportivo 2023 | 35000.0 | Isabel Díaz     |
| Eléctrico 2021 | 40000.0 | Elena Torres    |
+----------------+---------+-----------------+
```
### Encontrar los clientes que han comprado coches con precios superiores al promedio de todos los coches vendidos.
```sql
sqlite> SELECT DISTINCT cl.nombre
   ...> FROM ventas v
   ...> JOIN coches c ON v.id_coche = c.id_coche
   ...> JOIN clientes cl ON v.id_cliente = cl.id_cliente
   ...> WHERE c.precio > (SELECT AVG(precio) FROM coches);
+-----------------+
|     nombre      |
+-----------------+
| Carlos López    |
| Pedro Rodríguez |
| Isabel Díaz     |
| Elena Torres    |
+-----------------+
```

### Mostrar los modelos de coches y sus precios que no han sido vendidos aún:
```sql
sqlite> SELECT modelo, precio
   ...> FROM coches
   ...> WHERE id_coche NOT IN (SELECT id_coche FROM ventas);
+----------------+---------+
|     modelo     | precio  |
+----------------+---------+
| Pickup 2022    | 31000.0 |
| Sedán 2022     | 25000.0 |
| Hatchback 2021 | 22000.0 |
| SUV 2023       | 30000.0 |
| Coupé 2022     | 28000.0 |
| Camioneta 2023 | 32000.0 |
| Compacto 2021  | 20000.0 |
| Híbrido 2022   | 27000.0 |
| Deportivo 2023 | 35000.0 |
| Pickup 2022    | 31000.0 |
| Eléctrico 2021 | 40000.0 |
+----------------+---------+
```
### Calcular el total gastado por todos los clientes en coches:
```sql
sqlite> SELECT SUM(c.precio) AS total_gastado
   ...> FROM ventas v
   ...> JOIN coches c ON v.id_coche = c.id_coche;
+---------------+
| total_gastado |
+---------------+
| 518000.0      |
+---------------+
```
### Listar los coches vendidos junto con la fecha de venta y el nombre del cliente, ordenados por fecha de venta de forma descendente:
```sql
sqlite> SELECT c.modelo, c.precio, cl.nombre, v.fecha_venta
   ...> FROM ventas v
   ...> JOIN coches c ON v.id_coche = c.id_coche
   ...> JOIN clientes cl ON v.id_cliente = cl.id_cliente
   ...> ORDER BY v.fecha_venta DESC;
+----------------+---------+-----------------+-------------+
|     modelo     | precio  |     nombre      | fecha_venta |
+----------------+---------+-----------------+-------------+
| Eléctrico 2021 | 40000.0 | Elena Torres    | 2023-10-05  |
| Eléctrico 2021 | 40000.0 | Elena Torres    | 2023-10-05  |
| Deportivo 2023 | 35000.0 | Isabel Díaz     | 2023-08-25  |
| Deportivo 2023 | 35000.0 | Isabel Díaz     | 2023-08-25  |
| Híbrido 2022   | 27000.0 | Miguel González | 2023-07-20  |
| Híbrido 2022   | 27000.0 | Miguel González | 2023-07-20  |
| Compacto 2021  | 20000.0 | Laura Sánchez   | 2023-06-15  |
| Compacto 2021  | 20000.0 | Laura Sánchez   | 2023-06-15  |
| Camioneta 2023 | 32000.0 | Pedro Rodríguez | 2023-05-05  |
| Camioneta 2023 | 32000.0 | Pedro Rodríguez | 2023-05-05  |
| Coupé 2022     | 28000.0 | Ana Martínez    | 2023-04-10  |
| Coupé 2022     | 28000.0 | Ana Martínez    | 2023-04-10  |
| SUV 2023       | 30000.0 | Carlos López    | 2023-03-25  |
| SUV 2023       | 30000.0 | Carlos López    | 2023-03-25  |
| Hatchback 2021 | 22000.0 | María Gómez     | 2023-02-20  |
| Hatchback 2021 | 22000.0 | María Gómez     | 2023-02-20  |
| Sedán 2022     | 25000.0 | Juan Pérez      | 2023-01-15  |
| Sedán 2022     | 25000.0 | Juan Pérez      | 2023-01-15  |
+----------------+---------+-----------------+-------------+
```
### Encontrar el modelo de coche más caro.
 ```sql
 sqlite> SELECT modelo, precio
   ...> FROM coches
   ...> WHERE precio = (SELECT MAX(precio) FROM coches);
+----------------+---------+
|     modelo     | precio  |
+----------------+---------+
| Eléctrico 2021 | 40000.0 |
| Eléctrico 2021 | 40000.0 |
+----------------+---------+
```

### Mostrar los clientes que han comprado al menos un coche (un coche o más) y la cantidad de coches comprados.
```sql
 sqlite> SELECT cl.nombre, COUNT(v.id_coche) AS cantidad_compras
   ...> FROM ventas v
   ...> JOIN clientes cl ON v.id_cliente = cl.id_cliente
   ...> GROUP BY cl.nombre
   ...> ORDER BY cantidad_compras DESC;
+-----------------+------------------+
|     nombre      | cantidad_compras |
+-----------------+------------------+
| Pedro Rodríguez | 2                |
| Miguel González | 2                |
| María Gómez     | 2                |
| Laura Sánchez   | 2                |
| Juan Pérez      | 2                |
| Isabel Díaz     | 2                |
| Elena Torres    | 2                |
| Carlos López    | 2                |
| Ana Martínez    | 2                |
+-----------------+------------------+
```

### Encontrar los clientes que han comprado coches de la marca 'Toyota':
```sql
sqlite> SELECT DISTINCT cl.nombre
   ...> FROM ventas v
   ...> JOIN coches c ON v.id_coche = c.id_coche
   ...> JOIN clientes cl ON v.id_cliente = cl.id_cliente
   ...> WHERE c.marca = 'Toyota';
+------------+
|   nombre   |
+------------+
| Juan Pérez |
+------------+
```
### Calcular el promedio de edad de los clientes que han comprado coches de más de 25,000.
```sql
sqlite> SELECT AVG(cl.edad) AS promedio_edad
   ...> FROM ventas v
   ...> JOIN coches c ON v.id_coche = c.id_coche
   ...> JOIN clientes cl ON v.id_cliente = cl.id_cliente
   ...> WHERE c.precio > 25000;
+------------------+
|  promedio_edad   |
+------------------+
| 32.8333333333333 |
+------------------+
```
### Mostrar los modelos de coches y sus precios que fueron comprados por clientes mayores de 30 años.
```sql
sqlite> SELECT c.modelo, c.precio
   ...> FROM ventas v
   ...> JOIN coches c ON v.id_coche = c.id_coche
   ...> JOIN clientes cl ON v.id_cliente = cl.id_cliente
   ...> WHERE cl.edad > 30;
+----------------+---------+
|     modelo     | precio  |
+----------------+---------+
| SUV 2023       | 30000.0 |
| Camioneta 2023 | 32000.0 |
| Compacto 2021  | 20000.0 |
| Deportivo 2023 | 35000.0 |
| SUV 2023       | 30000.0 |
| Camioneta 2023 | 32000.0 |
| Compacto 2021  | 20000.0 |
| Deportivo 2023 | 35000.0 |
+----------------+---------+
```

### Encontrar los coches vendidos en el año 2022 junto con la cantidad total de ventas en ese año.
 ```sql
 sqlite> SELECT c.modelo, COUNT(v.id_venta) AS total_ventas_2022
   ...> FROM ventas v
   ...> JOIN coches c ON v.id_coche = c.id_coche
   ...> WHERE strftime('%Y', v.fecha_venta) = '2022'
   ...> GROUP BY c.modelo;
```
No sale resultado porque no se ha realizado ninguna venta en 2022 ta y como observamos en la tabla de ventas:
```sql
sqlite> select * from ventas
   ...> ;
+----------+------------+----------+-------------+
| id_venta | id_cliente | id_coche | fecha_venta |
+----------+------------+----------+-------------+
| 1        | 1          | 1        | 2023-01-15  |
| 2        | 2          | 2        | 2023-02-20  |
| 3        | 3          | 3        | 2023-03-25  |
| 4        | 4          | 4        | 2023-04-10  |
| 5        | 5          | 5        | 2023-05-05  |
| 6        | 6          | 6        | 2023-06-15  |
| 7        | 7          | 7        | 2023-07-20  |
| 8        | 8          | 8        | 2023-08-25  |
| 9        | 10         | 10       | 2023-10-05  |
| 10       | 1          | 1        | 2023-01-15  |
| 11       | 2          | 2        | 2023-02-20  |
| 12       | 3          | 3        | 2023-03-25  |
| 13       | 4          | 4        | 2023-04-10  |
| 14       | 5          | 5        | 2023-05-05  |
| 15       | 6          | 6        | 2023-06-15  |
| 16       | 7          | 7        | 2023-07-20  |
| 17       | 8          | 8        | 2023-08-25  |
| 18       | 10         | 10       | 2023-10-05  |
+----------+------------+----------+-------------+
```
### Listar los coches cuyos precios son mayores que el precio promedio de coches vendidos a clientes menores de 30 años.
```sql
sqlite> SELECT c.modelo, c.precio
   ...> FROM coches c
   ...> WHERE c.precio > (
(x1...>     SELECT AVG(c2.precio)
(x1...>     FROM ventas v
(x1...>     JOIN coches c2 ON v.id_coche = c2.id_coche
(x1...>     JOIN clientes cl ON v.id_cliente = cl.id_cliente
(x1...>     WHERE cl.edad < 30
(x1...> );
+----------------+---------+
|     modelo     | precio  |
+----------------+---------+
| SUV 2023       | 30000.0 |
| Camioneta 2023 | 32000.0 |
| Deportivo 2023 | 35000.0 |
| Pickup 2022    | 31000.0 |
| Eléctrico 2021 | 40000.0 |
| SUV 2023       | 30000.0 |
| Camioneta 2023 | 32000.0 |
| Deportivo 2023 | 35000.0 |
| Pickup 2022    | 31000.0 |
| Eléctrico 2021 | 40000.0 |
+----------------+---------+
```
### Calcular el total de ventas por marca de coche, ordenado de forma descendente por el total de ventas:
```sql
sqlite> SELECT c.marca, COUNT(v.id_venta) AS total_ventas
   ...> FROM ventas v
   ...> JOIN coches c ON v.id_coche = c.id_coche
   ...> GROUP BY c.marca
   ...> ORDER BY total_ventas DESC;
+------------+--------------+
|   marca    | total_ventas |
+------------+--------------+
| Volkswagen | 2            |
| Toyota     | 2            |
| Tesla      | 2            |
| Nissan     | 2            |
| Mazda      | 2            |
| Hyundai    | 2            |
| Honda      | 2            |
| Ford       | 2            |
| Chevrolet  | 2            |
+------------+--------------+
```