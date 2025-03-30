# Tarea 6
## Paso 1
Primero iniciamos la terminal y cargamos el fichero de sql para cargar als tablas
```bash
C:\Users\ese_s\Desktop\project\tarea5\tarea1>sqlite3 tarea6.db
SQLite version 3.49.1 2025-02-18 13:38:58
Enter ".help" for usage hints.
sqlite> .read base-datos-clientes.sql
```
### Obtener todos los clientes.
```sql
sqlite> select * from clientes
   ...> ;
+----+-----------------+---------------------------+
| id |     nombre      |           email           |
+----+-----------------+---------------------------+
| 1  | Juan Pérez      | juan@example.com          |
| 2  | María Gómez     | maria@example.com         |
| 3  | Carlos López    | carlos@example.com        |
| 4  | Ana Rodríguez   | ana@example.com           |
| 5  | Luisa Martínez  | luisa@example.com         |
| 6  | Pedro Sánchez   | pedro@example.com         |
| 7  | Laura García    | laura@example.com         |
| 8  | Miguel Martín   | miguel@example.com        |
| 9  | Elena González  | elena@example.com         |
| 10 | David Torres    | david@example.com         |
| 11 | Sofía Ruiz      | sofia@example.com         |
| 12 | Javier López    | javier@example.com        |
| 13 | Carmen Vargas   | carmen@example.com        |
| 14 | Daniel Muñoz    | daniel@example.com        |
| 15 | Isabel Serrano  | isabel@example.com        |
| 16 | Alejandro Muñoz | alejandro@example.com     |
| 17 | Raquel Herrera  | raquel@example.com        |
| 18 | Francisco Mora  | francisco@example.com     |
| 19 | Marina Díaz     | marina@example.com        |
| 20 | Antonio Jiménez | antonio@example.com       |
| 21 | Beatriz Romero  | beatriz@example.com       |
| 22 | Carlos Gómez    | carlos.gomez@example.com  |
| 23 | Clara Sánchez   | clara.sanchez@example.com |
| 24 | Andrés Martínez | andres@example.com        |
| 25 | Lucía Díaz      | lucia@example.com         |
| 26 | Mario Serrano   | mario@example.com         |
| 27 | Eva Torres      | eva.torres@example.com    |
| 28 | Roberto Ruiz    | roberto@example.com       |
| 29 | Celia García    | celia@example.com         |
+----+-----------------+---------------------------+
```
### Obtener la cantidad total de productos en todos los pedidos
```sql
sqlite> SELECT SUM(cantidad) AS total_productos
   ...> FROM Pedidos
   ...> WHERE cantidad REGEXP '^[0-9]+$';
+-----------------+
| total_productos |
+-----------------+
| 54              |
+-----------------+
```

### Obtener el precio promedio de los productos:
### Obtener los clientes que tienen un email válido (contiene '@'):
```sql
sqlite> SELECT * FROM Clientes
   ...> WHERE email REGEXP '.+@.+';
+----+-----------------+---------------------------+
| id |     nombre      |           email           |
+----+-----------------+---------------------------+
| 1  | Juan Pérez      | juan@example.com          |
| 2  | María Gómez     | maria@example.com         |
| 3  | Carlos López    | carlos@example.com        |
| 4  | Ana Rodríguez   | ana@example.com           |
| 5  | Luisa Martínez  | luisa@example.com         |
| 6  | Pedro Sánchez   | pedro@example.com         |
| 7  | Laura García    | laura@example.com         |
| 8  | Miguel Martín   | miguel@example.com        |
| 9  | Elena González  | elena@example.com         |
| 10 | David Torres    | david@example.com         |
| 11 | Sofía Ruiz      | sofia@example.com         |
| 12 | Javier López    | javier@example.com        |
| 13 | Carmen Vargas   | carmen@example.com        |
| 14 | Daniel Muñoz    | daniel@example.com        |
| 15 | Isabel Serrano  | isabel@example.com        |
| 16 | Alejandro Muñoz | alejandro@example.com     |
| 17 | Raquel Herrera  | raquel@example.com        |
| 18 | Francisco Mora  | francisco@example.com     |
| 19 | Marina Díaz     | marina@example.com        |
| 20 | Antonio Jiménez | antonio@example.com       |
| 21 | Beatriz Romero  | beatriz@example.com       |
| 22 | Carlos Gómez    | carlos.gomez@example.com  |
| 23 | Clara Sánchez   | clara.sanchez@example.com |
| 24 | Andrés Martínez | andres@example.com        |
| 25 | Lucía Díaz      | lucia@example.com         |
| 26 | Mario Serrano   | mario@example.com         |
| 27 | Eva Torres      | eva.torres@example.com    |
| 28 | Roberto Ruiz    | roberto@example.com       |
| 29 | Celia García    | celia@example.com         |
+----+-----------------+---------------------------+
```
### Obtener el producto más caro.
```sql
sqlite> SELECT * FROM Productos
   ...> WHERE precio REGEXP '^[0-9]+(\.[0-9]+)?$'
   ...> AND precio = (SELECT MAX(precio) FROM Productos WHERE precio REGEXP '^[0-9]+(\.[0-9]+)?$');
+----+--------+--------+
| id | nombre | precio |
+----+--------+--------+
| 1  | Laptop | 1200.0 |
+----+--------+--------+
```
### Obtener los pedidos realizados en febrero de 2024.
```sql
sqlite> SELECT * FROM Pedidos
   ...> WHERE fecha_pedido REGEXP '^2024-02';
+-----------+------------+-------------+----------+--------------+
| id_pedido | id_cliente | id_producto | cantidad | fecha_pedido |
+-----------+------------+-------------+----------+--------------+
| 1         | 1          | 1           | 2        | 2024-02-01   |
| 2         | 2          | 2           | 1        | 2024-02-02   |
| 3         | 3          | 3           | 3        | 2024-02-03   |
| 4         | 4          | 4           | 1        | 2024-02-04   |
| 5         | 5          | 5           | 2        | 2024-02-05   |
| 6         | 6          | 6           | 1        | 2024-02-06   |
| 7         | 7          | 7           | 3        | 2024-02-07   |
| 8         | 8          | 8           | 2        | 2024-02-08   |
| 9         | 9          | 9           | 1        | 2024-02-09   |
| 10        | 10         | 10          | 2        | 2024-02-10   |
| 11        | 11         | 11          | 1        | 2024-02-11   |
| 12        | 12         | 12          | 3        | 2024-02-12   |
| 13        | 13         | 13          | 1        | 2024-02-13   |
| 14        | 14         | 14          | 2        | 2024-02-14   |
| 15        | 15         | 15          | 1        | 2024-02-15   |
| 16        | 16         | 16          | 3        | 2024-02-16   |
| 17        | 17         | 17          | 2        | 2024-02-17   |
| 18        | 18         | 18          | 1        | 2024-02-18   |
| 19        | 19         | 19          | 2        | 2024-02-19   |
| 20        | 20         | 20          | 1        | 2024-02-20   |
| 21        | 21         | 21          | 3        | 2024-02-21   |
| 22        | 22         | 22          | 1        | 2024-02-22   |
| 23        | 23         | 23          | 2        | 2024-02-23   |
| 24        | 24         | 24          | 1        | 2024-02-24   |
| 25        | 25         | 25          | 3        | 2024-02-25   |
| 26        | 26         | 26          | 2        | 2024-02-26   |
| 27        | 27         | 27          | 1        | 2024-02-27   |
| 28        | 28         | 28          | 2        | 2024-02-28   |
| 29        | 29         | 29          | 1        | 2024-02-29   |
+-----------+------------+-------------+----------+--------------+
```
### Obtener la cantidad total de productos en todos los pedidos por producto.
```sql
sqlite> SELECT id_producto, SUM(cantidad) AS total_cantidad
   ...> FROM Pedidos
   ...> WHERE cantidad REGEXP '^[0-9]+$'
   ...> GROUP BY id_producto;
+-------------+----------------+
| id_producto | total_cantidad |
+-------------+----------------+
| 1           | 2              |
| 2           | 1              |
| 3           | 3              |
| 4           | 1              |
| 5           | 2              |
| 6           | 1              |
| 7           | 3              |
| 8           | 2              |
| 9           | 1              |
| 10          | 2              |
| 11          | 1              |
| 12          | 3              |
| 13          | 1              |
| 14          | 2              |
| 15          | 1              |
| 16          | 3              |
| 17          | 2              |
| 18          | 1              |
| 19          | 2              |
| 20          | 1              |
| 21          | 3              |
| 22          | 1              |
| 23          | 2              |
| 24          | 1              |
| 25          | 3              |
| 26          | 2              |
| 27          | 1              |
| 28          | 2              |
| 29          | 1              |
| 30          | 3              |
+-------------+----------------+
```
### Obtener los clientes que han realizado más de un pedido.

### Obtener los productos que tienen un precio registrado.
```sql
sqlite> SELECT * FROM Productos
   ...> WHERE precio REGEXP '^[0-9]+$' OR precio REGEXP '^[0-9]+\\.[0-9]+$';
```
### Obtener la fecha del primer pedido realizado: 
```sql
sqlite> SELECT fecha_pedido
   ...> FROM Pedidos
   ...> WHERE fecha_pedido REGEXP '^[0-9]{4}-[0-9]{2}-[0-9]{2}$'
   ...> ORDER BY fecha_pedido ASC
   ...> LIMIT 1;
+--------------+
| fecha_pedido |
+--------------+
| 2024-02-01   |
+--------------+
```
### Obtener los productos cuyos nombres comienzan con 'A' o 'B':
```sql
sqlite> SELECT * FROM Productos
   ...> WHERE nombre REGEXP '^[AB]';
+----+------------------------+--------+
| id |         nombre         | precio |
+----+------------------------+--------+
| 5  | Auriculares Bluetooth  | 79.99  |
| 9  | Altavoces Inalámbricos | 129.99 |
| 18 | Batería Externa        | 19.99  |
| 28 | Adaptador HDMI         | 12.99  |
+----+------------------------+--------+
```
### Obtener la cantidad total de productos en todos los pedidos por cliente ordenado por cliente.
```sql
sqlite> SELECT id_cliente, SUM(cantidad) AS total_cantidad
   ...> FROM Pedidos
   ...> WHERE cantidad REGEXP '^[0-9]+$'
   ...> GROUP BY id_cliente
   ...> ORDER BY id_cliente;
+------------+----------------+
| id_cliente | total_cantidad |
+------------+----------------+
| 1          | 2              |
| 2          | 1              |
| 3          | 3              |
| 4          | 1              |
| 5          | 2              |
| 6          | 1              |
| 7          | 3              |
| 8          | 2              |
| 9          | 1              |
| 10         | 2              |
| 11         | 1              |
| 12         | 3              |
| 13         | 1              |
| 14         | 2              |
| 15         | 1              |
| 16         | 3              |
| 17         | 2              |
| 18         | 1              |
| 19         | 2              |
| 20         | 1              |
| 21         | 3              |
| 22         | 1              |
| 23         | 2              |
| 24         | 1              |
| 25         | 3              |
| 26         | 2              |
| 27         | 1              |
| 28         | 2              |
| 29         | 1              |
| 30         | 3              |
+------------+----------------+
```
### Obtener los clientes que han realizado más de un pedido en febrero de 2024.
```sql
sqlite> SELECT id_cliente, COUNT(*) AS total_pedidos
   ...> FROM Pedidos
   ...> WHERE fecha_pedido REGEXP '^2024-02-[0-9]{2}$'
   ...> GROUP BY id_cliente
   ...> HAVING COUNT(*) > 1;
```
### Obtener los productos con precio entre 100 y 500.
```sql
sqlite> select * from Productos
   ...> Where precio regexp '^[1-4][0-9]{2,2}(\.[0-9]{1,2})?$' ;
+----+------------------------+--------+
| id |         nombre         | precio |
+----+------------------------+--------+
| 4  | Tablet                 | 299.99 |
| 6  | Impresora              | 199.99 |
| 7  | Cámara Digital         | 499.99 |
| 8  | Reproductor de Audio   | 149.99 |
| 9  | Altavoces Inalámbricos | 129.99 |
| 10 | Reloj Inteligente      | 249.99 |
| 13 | Monitor LED            | 349.99 |
+----+------------------------+--------+
```
### Obtener la cantidad total de productos en todos los pedidos por cliente ordenado por cantidad descendente.
```sql
sqlite> SELECT id_cliente, SUM(cantidad) AS total_cantidad
   ...> FROM Pedidos
   ...> WHERE cantidad REGEXP '^[0-9]+$'
   ...> GROUP BY id_cliente
   ...> ORDER BY total_cantidad DESC;
+------------+----------------+
| id_cliente | total_cantidad |
+------------+----------------+
| 30         | 3              |
| 25         | 3              |
| 21         | 3              |
| 16         | 3              |
| 12         | 3              |
| 7          | 3              |
| 3          | 3              |
| 28         | 2              |
| 26         | 2              |
| 23         | 2              |
| 19         | 2              |
| 17         | 2              |
| 14         | 2              |
| 10         | 2              |
| 8          | 2              |
| 5          | 2              |
| 1          | 2              |
| 29         | 1              |
| 27         | 1              |
| 24         | 1              |
| 22         | 1              |
| 20         | 1              |
| 18         | 1              |
| 15         | 1              |
| 13         | 1              |
| 11         | 1              |
| 9          | 1              |
| 6          | 1              |
| 4          | 1              |
| 2          | 1              |
+------------+----------------+
```
### Obtener los clientes que tienen una 'a' en cualquier posición de su nombre.
```sql
sqlite> SELECT * FROM Clientes
   ...> WHERE nombre REGEXP 'a';
+----+-----------------+---------------------------+
| id |     nombre      |           email           |
+----+-----------------+---------------------------+
| 1  | Juan Pérez      | juan@example.com          |
| 2  | María Gómez     | maria@example.com         |
| 3  | Carlos López    | carlos@example.com        |
| 4  | Ana Rodríguez   | ana@example.com           |
| 5  | Luisa Martínez  | luisa@example.com         |
| 7  | Laura García    | laura@example.com         |
| 8  | Miguel Martín   | miguel@example.com        |
| 9  | Elena González  | elena@example.com         |
| 10 | David Torres    | david@example.com         |
| 11 | Sofía Ruiz      | sofia@example.com         |
| 12 | Javier López    | javier@example.com        |
| 13 | Carmen Vargas   | carmen@example.com        |
| 14 | Daniel Muñoz    | daniel@example.com        |
| 15 | Isabel Serrano  | isabel@example.com        |
| 16 | Alejandro Muñoz | alejandro@example.com     |
| 17 | Raquel Herrera  | raquel@example.com        |
| 18 | Francisco Mora  | francisco@example.com     |
| 19 | Marina Díaz     | marina@example.com        |
| 21 | Beatriz Romero  | beatriz@example.com       |
| 22 | Carlos Gómez    | carlos.gomez@example.com  |
| 23 | Clara Sánchez   | clara.sanchez@example.com |
| 24 | Andrés Martínez | andres@example.com        |
| 25 | Lucía Díaz      | lucia@example.com         |
| 26 | Mario Serrano   | mario@example.com         |
| 27 | Eva Torres      | eva.torres@example.com    |
| 29 | Celia García    | celia@example.com         |
+----+-----------------+---------------------------+
```
### Obtener el precio máximo de los productos.
```sql
sqlite> SELECT * FROM Productos
   ...> WHERE precio REGEXP '^[0-9]+(\.[0-9]+)?$'
   ...> AND precio = (SELECT MAX(precio) FROM Productos WHERE precio REGEXP '^[0-9]+(\.[0-9]+)?$');
+----+--------+--------+
| id | nombre | precio |
+----+--------+--------+
| 1  | Laptop | 1200.0 |
+----+--------+--------+
```
### Obtener los pedidos realizados por el cliente con ID 1 en febrero de 2024.
```sql
sqlite> SELECT * FROM Pedidos
   ...> WHERE id_cliente = 1
   ...> AND fecha_pedido REGEXP '^2024-02-[0-9]{2}$';  -- Verifica que la fecha esté en febrero de 2024
+-----------+------------+-------------+----------+--------------+
| id_pedido | id_cliente | id_producto | cantidad | fecha_pedido |
+-----------+------------+-------------+----------+--------------+
| 1         | 1          | 1           | 2        | 2024-02-01   |
+-----------+------------+-------------+----------+--------------+
```
### Obtener la cantidad total de productos en todos los pedidos por producto ordenado por total de productos descendente.
```sql
sqlite> SELECT p.id, p.nombre, SUM(pd.cantidad) AS total_productos
   ...> FROM Productos p
   ...> JOIN Pedidos pd ON p.id = pd.id_producto
   ...> WHERE pd.cantidad REGEXP '^[0-9]+$'  
   ...> GROUP BY p.id, p.nombre
   ...> ORDER BY total_productos DESC;
+----+-----------------------------------+-----------------+
| id |              nombre               | total_productos |
+----+-----------------------------------+-----------------+
| 3  | TV LED                            | 3               |
| 7  | Cámara Digital                    | 3               |
| 12 | Ratón Óptico                      | 3               |
| 16 | Router Wi-Fi                      | 3               |
| 21 | Cargador Inalámbrico              | 3               |
| 25 | Hub USB                           | 3               |
| 1  | Laptop                            | 2               |
| 5  | Auriculares Bluetooth             | 2               |
| 8  | Reproductor de Audio              | 2               |
| 10 | Reloj Inteligente                 | 2               |
| 14 | Mochila para Portátil             | 2               |
| 17 | Lámpara LED                       | 2               |
| 19 | Estuche para Auriculares          | 2               |
| 23 | Funda para Tablet                 | 2               |
| 26 | Webcam HD                         | 2               |
| 28 | Adaptador HDMI                    | 2               |
| 2  | Smartphone                        | 1               |
| 4  | Tablet                            | 1               |
| 6  | Impresora                         | 1               |
| 9  | Altavoces Inalámbricos            | 1               |
| 11 | Teclado Inalámbrico               | 1               |
| 13 | Monitor LED                       | 1               |
| 15 | Disco Duro Externo                | 1               |
| 18 | Batería Externa                   | 1               |
| 20 | Tarjeta de Memoria                | 1               |
| 22 | Kit de Limpieza para Computadoras | 1               |
| 24 | Soporte para Teléfono             | 1               |
| 27 | Funda para Laptop                 | 1               |
+----+-----------------------------------+-----------------+
```
### Obtener los productos que no tienen un precio registrado.
sqlite> SELECT * FROM Productos
   ...> WHERE precio REGEXP '^[^0-9]*$';  
### Obtener la fecha del último pedido realizado.
```sql
sqlite> SELECT MAX(fecha_pedido) AS ultima_fecha
   ...> FROM Pedidos
   ...> WHERE fecha_pedido REGEXP '^\d{4}-\d{2}-\d{2}$';  -- Verifica que la fecha esté en formato YYYY-MM-DD
+--------------+
| ultima_fecha |
+--------------+
| 2024-03-01   |
+--------------+
```
### Obtener los clientes cuyo nombre tiene al menos 5 caracteres.
```sql
sqlite> SELECT * FROM Clientes
   ...> WHERE nombre REGEXP '^.{5,}$';
+----+-----------------+---------------------------+
| id |     nombre      |           email           |
+----+-----------------+---------------------------+
| 1  | Juan Pérez      | juan@example.com          |
| 2  | María Gómez     | maria@example.com         |
| 3  | Carlos López    | carlos@example.com        |
| 4  | Ana Rodríguez   | ana@example.com           |
| 5  | Luisa Martínez  | luisa@example.com         |
| 6  | Pedro Sánchez   | pedro@example.com         |
| 7  | Laura García    | laura@example.com         |
| 8  | Miguel Martín   | miguel@example.com        |
| 9  | Elena González  | elena@example.com         |
| 10 | David Torres    | david@example.com         |
| 11 | Sofía Ruiz      | sofia@example.com         |
| 12 | Javier López    | javier@example.com        |
| 13 | Carmen Vargas   | carmen@example.com        |
| 14 | Daniel Muñoz    | daniel@example.com        |
| 15 | Isabel Serrano  | isabel@example.com        |
| 16 | Alejandro Muñoz | alejandro@example.com     |
| 17 | Raquel Herrera  | raquel@example.com        |
| 18 | Francisco Mora  | francisco@example.com     |
| 19 | Marina Díaz     | marina@example.com        |
| 20 | Antonio Jiménez | antonio@example.com       |
| 21 | Beatriz Romero  | beatriz@example.com       |
| 22 | Carlos Gómez    | carlos.gomez@example.com  |
| 23 | Clara Sánchez   | clara.sanchez@example.com |
| 24 | Andrés Martínez | andres@example.com        |
| 25 | Lucía Díaz      | lucia@example.com         |
| 26 | Mario Serrano   | mario@example.com         |
| 27 | Eva Torres      | eva.torres@example.com    |
| 28 | Roberto Ruiz    | roberto@example.com       |
| 29 | Celia García    | celia@example.com         |
+----+-----------------+---------------------------+
```
### Obtener los productos que tienen la letra 'o' en cualquier posición del nombre.
```sql
sqlite> SELECT * FROM Productos
   ...> WHERE nombre REGEXP 'o';
+----+-----------------------------------+--------+
| id |              nombre               | precio |
+----+-----------------------------------+--------+
| 1  | Laptop                            | 1200.0 |
| 2  | Smartphone                        | 699.99 |
| 5  | Auriculares Bluetooth             | 79.99  |
| 6  | Impresora                         | 199.99 |
| 8  | Reproductor de Audio              | 149.99 |
| 9  | Altavoces Inalámbricos            | 129.99 |
| 10 | Reloj Inteligente                 | 249.99 |
| 11 | Teclado Inalámbrico               | 59.99  |
| 12 | Ratón Óptico                      | 29.99  |
| 13 | Monitor LED                       | 349.99 |
| 14 | Mochila para Portátil             | 49.99  |
| 15 | Disco Duro Externo                | 89.99  |
| 16 | Router Wi-Fi                      | 69.99  |
| 20 | Tarjeta de Memoria                | 24.99  |
| 21 | Cargador Inalámbrico              | 34.99  |
| 22 | Kit de Limpieza para Computadoras | 9.99   |
| 24 | Soporte para Teléfono             | 14.99  |
| 27 | Funda para Laptop                 | 29.99  |
| 28 | Adaptador HDMI                    | 12.99  |
+----+-----------------------------------+--------+
```
### Obtener la cantidad total de productos en todos los pedidos por cliente ordenado por cliente.
```sql
sqlite> SELECT c.id, c.nombre, SUM(p.cantidad) AS total_productos
   ...> FROM Clientes c
   ...> JOIN Pedidos p ON c.id = p.id_cliente
   ...> WHERE p.cantidad REGEXP '^[0-9]+$' 
   ...> GROUP BY c.id, c.nombre
   ...> ORDER BY c.nombre;  
+----+-----------------+-----------------+
| id |     nombre      | total_productos |
+----+-----------------+-----------------+
| 16 | Alejandro Muñoz | 3               |
| 4  | Ana Rodríguez   | 1               |
| 24 | Andrés Martínez | 1               |
| 20 | Antonio Jiménez | 1               |
| 21 | Beatriz Romero  | 3               |
| 22 | Carlos Gómez    | 1               |
| 3  | Carlos López    | 3               |
| 13 | Carmen Vargas   | 1               |
| 29 | Celia García    | 1               |
| 23 | Clara Sánchez   | 2               |
| 14 | Daniel Muñoz    | 2               |
| 10 | David Torres    | 2               |
| 9  | Elena González  | 1               |
| 27 | Eva Torres      | 1               |
| 18 | Francisco Mora  | 1               |
| 15 | Isabel Serrano  | 1               |
| 12 | Javier López    | 3               |
| 1  | Juan Pérez      | 2               |
| 7  | Laura García    | 3               |
| 25 | Lucía Díaz      | 3               |
| 5  | Luisa Martínez  | 2               |
| 19 | Marina Díaz     | 2               |
| 26 | Mario Serrano   | 2               |
| 2  | María Gómez     | 1               |
| 8  | Miguel Martín   | 2               |
| 6  | Pedro Sánchez   | 1               |
| 17 | Raquel Herrera  | 2               |
| 28 | Roberto Ruiz    | 2               |
| 11 | Sofía Ruiz      | 1               |
+----+-----------------+-----------------+
```
### Obtener los clientes cuyos nombres no contienen la letra 'i':
```sql
sqlite> SELECT * FROM Clientes
   ...> WHERE nombre REGEXP '^[^i]*$';
+----+-----------------+---------------------------+
| id |     nombre      |           email           |
+----+-----------------+---------------------------+
| 1  | Juan Pérez      | juan@example.com          |
| 2  | María Gómez     | maria@example.com         |
| 3  | Carlos López    | carlos@example.com        |
| 4  | Ana Rodríguez   | ana@example.com           |
| 6  | Pedro Sánchez   | pedro@example.com         |
| 7  | Laura García    | laura@example.com         |
| 9  | Elena González  | elena@example.com         |
| 13 | Carmen Vargas   | carmen@example.com        |
| 15 | Isabel Serrano  | isabel@example.com        |
| 16 | Alejandro Muñoz | alejandro@example.com     |
| 17 | Raquel Herrera  | raquel@example.com        |
| 22 | Carlos Gómez    | carlos.gomez@example.com  |
| 23 | Clara Sánchez   | clara.sanchez@example.com |
| 24 | Andrés Martínez | andres@example.com        |
| 25 | Lucía Díaz      | lucia@example.com         |
| 27 | Eva Torres      | eva.torres@example.com    |
+----+-----------------+---------------------------+
```
### Obtener los pedidos realizados por el cliente con ID 2 en febrero de 2024.
```sql
sqlite> SELECT * FROM Pedidos
   ...> WHERE id_cliente = 2
   ...> AND fecha_pedido REGEXP '^2024-02-';
+-----------+------------+-------------+----------+--------------+
| id_pedido | id_cliente | id_producto | cantidad | fecha_pedido |
+-----------+------------+-------------+----------+--------------+
| 2         | 2          | 2           | 1        | 2024-02-02   |
+-----------+------------+-------------+----------+--------------+
```
### Obtener el precio mínimo de los productos.
```sql
sqlite> SELECT MIN(precio) AS precio_minimo
   ...> FROM Productos
   ...> WHERE precio REGEXP '^[0-9]+(\.[0-9]+)?$';
+---------------+
| precio_minimo |
+---------------+
| 9.99          |
+---------------+
```
### Obtener los clientes que han realizado al menos un pedido en febrero de 2024.
```sql
sqlite> SELECT DISTINCT c.id, c.nombre
   ...> FROM Clientes c
   ...> JOIN Pedidos p ON c.id = p.id_cliente
   ...> WHERE p.fecha_pedido REGEXP '^2024-02-';
+----+-----------------+
| id |     nombre      |
+----+-----------------+
| 1  | Juan Pérez      |
| 2  | María Gómez     |
| 3  | Carlos López    |
| 4  | Ana Rodríguez   |
| 5  | Luisa Martínez  |
| 6  | Pedro Sánchez   |
| 7  | Laura García    |
| 8  | Miguel Martín   |
| 9  | Elena González  |
| 10 | David Torres    |
| 11 | Sofía Ruiz      |
| 12 | Javier López    |
| 13 | Carmen Vargas   |
| 14 | Daniel Muñoz    |
| 15 | Isabel Serrano  |
| 16 | Alejandro Muñoz |
| 17 | Raquel Herrera  |
| 18 | Francisco Mora  |
| 19 | Marina Díaz     |
| 20 | Antonio Jiménez |
| 21 | Beatriz Romero  |
| 22 | Carlos Gómez    |
| 23 | Clara Sánchez   |
| 24 | Andrés Martínez |
| 25 | Lucía Díaz      |
| 26 | Mario Serrano   |
| 27 | Eva Torres      |
| 28 | Roberto Ruiz    |
| 29 | Celia García    |
+----+-----------------+
```
### Obtener la fecha del último pedido realizado por el cliente con ID 3.
```sql
sqlite> SELECT fecha_pedido
   ...> FROM Pedidos
   ...> WHERE id_cliente = 3
   ...> AND fecha_pedido REGEXP '^[0-9]{4}-[0-9]{2}-[0-9]{2}$'
   ...> ORDER BY fecha_pedido DESC
   ...> LIMIT 1;
+--------------+
| fecha_pedido |
+--------------+
| 2024-02-03   |
+--------------+
```
### Obtener los productos que tienen una 'a' al final del nombre.
```sql
sqlite> SELECT *
   ...> FROM Productos
   ...> WHERE nombre REGEXP 'a$';
+----+--------------------+--------+
| id |       nombre       | precio |
+----+--------------------+--------+
| 6  | Impresora          | 199.99 |
| 18 | Batería Externa    | 19.99  |
| 20 | Tarjeta de Memoria | 24.99  |
+----+--------------------+--------+
```
### Obtener los clientes cuyos nombres tienen al menos 4 vocales (mayúsculas|minúsculas).
```sql
sqlite> SELECT *
   ...> FROM Clientes
   ...> WHERE nombre REGEXP '[aeiouAEIOU].*[aeiouAEIOU].*[aeiouAEIOU].*[aeiouAEIOU]';
+----+-----------------+------------------------+
| id |     nombre      |         email          |
+----+-----------------+------------------------+
| 4  | Ana Rodríguez   | ana@example.com        |
| 5  | Luisa Martínez  | luisa@example.com      |
| 7  | Laura García    | laura@example.com      |
| 8  | Miguel Martín   | miguel@example.com     |
| 9  | Elena González  | elena@example.com      |
| 10 | David Torres    | david@example.com      |
| 11 | Sofía Ruiz      | sofia@example.com      |
| 12 | Javier López    | javier@example.com     |
| 13 | Carmen Vargas   | carmen@example.com     |
| 14 | Daniel Muñoz    | daniel@example.com     |
| 15 | Isabel Serrano  | isabel@example.com     |
| 16 | Alejandro Muñoz | alejandro@example.com  |
| 17 | Raquel Herrera  | raquel@example.com     |
| 18 | Francisco Mora  | francisco@example.com  |
| 19 | Marina Díaz     | marina@example.com     |
| 20 | Antonio Jiménez | antonio@example.com    |
| 21 | Beatriz Romero  | beatriz@example.com    |
| 26 | Mario Serrano   | mario@example.com      |
| 27 | Eva Torres      | eva.torres@example.com |
| 28 | Roberto Ruiz    | roberto@example.com    |
| 29 | Celia García    | celia@example.com      |
+----+-----------------+------------------------+
```
### Obtener los productos cuyo precio tenga al menos 4 números sin contrar los decimales.
```sql
sqlite> SELECT *
   ...> FROM Productos
   ...> WHERE precio REGEXP '^[0-9]{4,}(\.[0-9]+)?$';
+----+--------+--------+
| id | nombre | precio |
+----+--------+--------+
| 1  | Laptop | 1200.0 |
+----+--------+--------+
```
### Obtener los clientes cuyos nombres tienen al menos una 'a' seguida de una 'e'.
```sql
sqlite> SELECT *
   ...> FROM Clientes
   ...> WHERE nombre REGEXP 'a.e';
+----+----------------+--------------------+
| id |     nombre     |       email        |
+----+----------------+--------------------+
| 15 | Isabel Serrano | isabel@example.com |
+----+----------------+--------------------+
```
### Obtener los productos cuyos nombres terminan con una consonante.
```sql
sqlite> SELECT *
   ...> FROM Productos
   ...> WHERE nombre REGEXP '[^aeiouAEIOU]$';
+----+-----------------------------------+--------+
| id |              nombre               | precio |
+----+-----------------------------------+--------+
| 1  | Laptop                            | 1200.0 |
| 3  | TV LED                            | 799.5  |
| 4  | Tablet                            | 299.99 |
| 5  | Auriculares Bluetooth             | 79.99  |
| 7  | Cámara Digital                    | 499.99 |
| 9  | Altavoces Inalámbricos            | 129.99 |
| 13 | Monitor LED                       | 349.99 |
| 14 | Mochila para Portátil             | 49.99  |
| 17 | Lámpara LED                       | 39.99  |
| 19 | Estuche para Auriculares          | 14.99  |
| 22 | Kit de Limpieza para Computadoras | 9.99   |
| 23 | Funda para Tablet                 | 19.99  |
| 25 | Hub USB                           | 29.99  |
| 26 | Webcam HD                         | 59.99  |
| 27 | Funda para Laptop                 | 29.99  |
+----+-----------------------------------+--------+
```
### Obtener los productos cuyos nombres empiezan con una vocal.
```sql
sqlite> SELECT *
   ...> FROM Productos
   ...> WHERE nombre REGEXP '^[aeiouAEIOU]';
+----+--------------------------+--------+
| id |          nombre          | precio |
+----+--------------------------+--------+
| 5  | Auriculares Bluetooth    | 79.99  |
| 6  | Impresora                | 199.99 |
| 9  | Altavoces Inalámbricos   | 129.99 |
| 19 | Estuche para Auriculares | 14.99  |
| 28 | Adaptador HDMI           | 12.99  |
+----+--------------------------+--------+
```