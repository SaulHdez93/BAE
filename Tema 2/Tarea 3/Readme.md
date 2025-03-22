## Paso 2 Lectura del fichero sql
```sql
sqlite3>.read empleados-dump
```
para comprobarlo usamos:
```sql
sqlite3>.table
```
## Paso 3: Realización de consultas
Realiza las siguientes consultas, y muestra el resultado obtenido:

### Funciones UPPER y LOWER

### Muestra el nombre de todos los empleados en mayúsculas
```sql
sqlite> SELECT UPPER(nombre) AS nombre_mayusculas FROM empleados;
+-------------------+
| nombre_mayusculas |
+-------------------+
| JUAN              |
| MARíA             |
| CARLOS            |
| ANA               |
| PEDRO             |
| LAURA             |
| JAVIER            |
| CARMEN            |
| MIGUEL            |
| ELENA             |
| DIEGO             |
| SOFíA             |
| ANDRéS            |
| ISABEL            |
| RAúL              |
| PATRICIA          |
| ALEJANDRO         |
| NATALIA           |
| ROBERTO           |
| BEATRIZ           |
+-------------------+
```
## Funciones Numéricas

### Calcula el valor absoluto del salario de todos los empleados
```sql
sqlite> SELECT nombre, ABS(salario) AS salario_absoluto, departamento FROM empleados;
+-----------+------------------+------------------+
|  nombre   | salario_absoluto |   departamento   |
+-----------+------------------+------------------+
| Juan      | 50000.0          | Ventas           |
| María     | 60000.0          | TI               |
| Carlos    | 55000.0          | Ventas           |
| Ana       | 48000.0          | Recursos Humanos |
| Pedro     | 70000.0          | TI               |
| Laura     | 52000.0          | Ventas           |
| Javier    | 48000.0          | Recursos Humanos |
| Carmen    | 65000.0          | TI               |
| Miguel    | 51000.0          | Ventas           |
| Elena     | 55000.0          | Recursos Humanos |
| Diego     | 72000.0          | TI               |
| Sofía     | 49000.0          | Ventas           |
| Andrés    | 60000.0          | Recursos Humanos |
| Isabel    | 53000.0          | TI               |
| Raúl      | 68000.0          | Ventas           |
| Patricia  | 47000.0          | Recursos Humanos |
| Alejandro | 71000.0          | TI               |
| Natalia   | 54000.0          | Ventas           |
| Roberto   | 49000.0          | Recursos Humanos |
| Beatriz   | 63000.0          | TI               |
+-----------+------------------+------------------+
```
## Funciones de Fecha y Hora

### Muestra la fecha actual
```sql
sqlite> SELECT DATE('now') AS fecha_actual;
+--------------+
| fecha_actual |
+--------------+
| 2025-03-17   |
+--------------+

```

### Calcula el promedio de salarios de todos los empleados
```sql
sqlite> SELECT AVG(salario) AS promedio_salarios FROM empleados;
+-------------------+
| promedio_salarios |
+-------------------+
| 57000.0           |
+-------------------+

```

### Convierte la cadena '123' a un valor entero.
```sql
sqlite> SELECT CAST('123' AS INTEGER) AS valor_entero;
+--------------+
| valor_entero |
+--------------+
| 123          |
+--------------+

```


## Funciones de Manipulación de Cadenas
### Concatena el nombre y el departamento de cada empleado
```sql
sqlite> SELECT nombre || departamento AS nombre_departamento
   ...> FROM empleados;
+--------------------------+
|   nombre_departamento    |
+--------------------------+
| JuanVentas               |
| MaríaTI                  |
| CarlosVentas             |
| AnaRecursos Humanos      |
| PedroTI                  |
| LauraVentas              |
| JavierRecursos Humanos   |
| CarmenTI                 |
| MiguelVentas             |
| ElenaRecursos Humanos    |
| DiegoTI                  |
| SofíaVentas              |
| AndrésRecursos Humanos   |
| IsabelTI                 |
| RaúlVentas               |
| PatriciaRecursos Humanos |
| AlejandroTI              |
| NataliaVentas            |
| RobertoRecursos Humanos  |
| BeatrizTI                |
+--------------------------+
```
## Funciones de Manipulación de Cadenas (CONCAT_WS):
### Concatena el nombre y el departamento de cada empleado con un guion como separador.
En sqlite3 de forma nativa no se puede usar el comando concat_ws se sustituyo por el comando || - ||
```sql
sqlite> SELECT nombre || ' - ' || departamento AS nombre_departamento
   ...> FROM empleados;
+-----------------------------+
|     nombre_departamento     |
+-----------------------------+
| Juan - Ventas               |
| María - TI                  |
| Carlos - Ventas             |
| Ana - Recursos Humanos      |
| Pedro - TI                  |
| Laura - Ventas              |
| Javier - Recursos Humanos   |
| Carmen - TI                 |
| Miguel - Ventas             |
| Elena - Recursos Humanos    |
| Diego - TI                  |
| Sofía - Ventas              |
| Andrés - Recursos Humanos   |
| Isabel - TI                 |
| Raúl - Ventas               |
| Patricia - Recursos Humanos |
| Alejandro - TI              |
| Natalia - Ventas            |
| Roberto - Recursos Humanos  |
| Beatriz - TI                |
+-----------------------------+
```
## Funciones de Control de Flujo (CASE):
### Categoriza a los empleados según sus salarios.
```sql
sqlite> SELECT nombre,
   ...>        salario,
   ...>        CASE
   ...>            WHEN salario < 50000 THEN 'Bajo'
   ...>            WHEN salario BETWEEN 50000 AND 70000 THEN 'Medio'
   ...>            WHEN salario > 70000 THEN 'Alto'
   ...>        END AS categoria_salario
   ...> FROM empleados;
+-----------+---------+-------------------+
|  nombre   | salario | categoria_salario |
+-----------+---------+-------------------+
| Juan      | 50000.0 | Medio             |
| María     | 60000.0 | Medio             |
| Carlos    | 55000.0 | Medio             |
| Ana       | 48000.0 | Bajo              |
| Pedro     | 70000.0 | Medio             |
| Laura     | 52000.0 | Medio             |
| Javier    | 48000.0 | Bajo              |
| Carmen    | 65000.0 | Medio             |
| Miguel    | 51000.0 | Medio             |
| Elena     | 55000.0 | Medio             |
| Diego     | 72000.0 | Alto              |
| Sofía     | 49000.0 | Bajo              |
| Andrés    | 60000.0 | Medio             |
| Isabel    | 53000.0 | Medio             |
| Raúl      | 68000.0 | Medio             |
| Patricia  | 47000.0 | Bajo              |
| Alejandro | 71000.0 | Alto              |
| Natalia   | 54000.0 | Medio             |
| Roberto   | 49000.0 | Bajo              |
| Beatriz   | 63000.0 | Medio             |
+-----------+---------+-------------------+
```
## Funciones de Agregación (SUM):
### Calcula la suma total de salarios de todos los empleados.
```sql
sqlite> SELECT SUM(salario) AS suma_total_salarios
   ...> FROM empleados;
+---------------------+
| suma_total_salarios |
+---------------------+
| 1140000.0           |
+---------------------+
```
## Funciones Numéricas (ROUND):
### Redondea el salario de todos los empleados a dos decimales.
```sql
sqlite> SELECT nombre, ROUND(salario, 2) AS salario_redondeado
   ...> FROM empleados;
+-----------+--------------------+
|  nombre   | salario_redondeado |
+-----------+--------------------+
| Juan      | 50000.0            |
| María     | 60000.0            |
| Carlos    | 55000.0            |
| Ana       | 48000.0            |
| Pedro     | 70000.0            |
| Laura     | 52000.0            |
| Javier    | 48000.0            |
| Carmen    | 65000.0            |
| Miguel    | 51000.0            |
| Elena     | 55000.0            |
| Diego     | 72000.0            |
| Sofía     | 49000.0            |
| Andrés    | 60000.0            |
| Isabel    | 53000.0            |
| Raúl      | 68000.0            |
| Patricia  | 47000.0            |
| Alejandro | 71000.0            |
| Natalia   | 54000.0            |
| Roberto   | 49000.0            |
| Beatriz   | 63000.0            |
+-----------+--------------------+
```
## Funciones de Manipulación de Cadenas (LENGTH):
### Muestra la longitud de cada nombre de empleado.
```sql
sqlite> SELECT nombre, LENGTH(nombre) AS longitud_nombre
   ...> FROM empleados;
+-----------+-----------------+
|  nombre   | longitud_nombre |
+-----------+-----------------+
| Juan      | 4               |
| María     | 5               |
| Carlos    | 6               |
| Ana       | 3               |
| Pedro     | 5               |
| Laura     | 5               |
| Javier    | 6               |
| Carmen    | 6               |
| Miguel    | 6               |
| Elena     | 5               |
| Diego     | 5               |
| Sofía     | 5               |
| Andrés    | 6               |
| Isabel    | 6               |
| Raúl      | 4               |
| Patricia  | 8               |
| Alejandro | 9               |
| Natalia   | 7               |
| Roberto   | 7               |
| Beatriz   | 7               |
+-----------+-----------------+
```

## Funciones de Agregación (COUNT):
### Cuenta el número total de empleados en cada departamento.
```sql
sqlite> SELECT departamento, COUNT(*) AS total_empleados
   ...> FROM empleados
   ...> GROUP BY departamento;
+------------------+-----------------+
|   departamento   | total_empleados |
+------------------+-----------------+
| Recursos Humanos | 6               |
| TI               | 7               |
| Ventas           | 7               |
+------------------+-----------------+
```
## Funciones de Fecha y Hora (CURRENT_TIME):
### Muestra la hora actual.
```sql
sqlite> SELECT DATETIME('now') AS fecha_y_hora_actual;
+---------------------+
| fecha_y_hora_actual |
+---------------------+
| 2025-03-17 17:11:25 |
+---------------------+
```

## Funciones de Conversión (CAST):
### Convierte el salario a un valor de punto flotante.
```sql
sqlite> SELECT nombre, CAST(salario AS REAL) AS salario_flotante
   ...> FROM empleados;
+-----------+------------------+
|  nombre   | salario_flotante |
+-----------+------------------+
| Juan      | 50000.0          |
| María     | 60000.0          |
| Carlos    | 55000.0          |
| Ana       | 48000.0          |
| Pedro     | 70000.0          |
| Laura     | 52000.0          |
| Javier    | 48000.0          |
| Carmen    | 65000.0          |
| Miguel    | 51000.0          |
| Elena     | 55000.0          |
| Diego     | 72000.0          |
| Sofía     | 49000.0          |
| Andrés    | 60000.0          |
| Isabel    | 53000.0          |
| Raúl      | 68000.0          |
| Patricia  | 47000.0          |
| Alejandro | 71000.0          |
| Natalia   | 54000.0          |
| Roberto   | 49000.0          |
| Beatriz   | 63000.0          |
+-----------+------------------+
```

## Funciones de Manipulación de Cadenas (SUBSTR):
### Muestra los primeros tres caracteres de cada nombre de empleado.
```sql
sqlite> SELECT nombre, SUBSTR(nombre, 1, 3) AS primeros_tres_caracteres
   ...> FROM empleados;
+-----------+--------------------------+
|  nombre   | primeros_tres_caracteres |
+-----------+--------------------------+
| Juan      | Jua                      |
| María     | Mar                      |
| Carlos    | Car                      |
| Ana       | Ana                      |
| Pedro     | Ped                      |
| Laura     | Lau                      |
| Javier    | Jav                      |
| Carmen    | Car                      |
| Miguel    | Mig                      |
| Elena     | Ele                      |
| Diego     | Die                      |
| Sofía     | Sof                      |
| Andrés    | And                      |
| Isabel    | Isa                      |
| Raúl      | Raú                      |
| Patricia  | Pat                      |
| Alejandro | Ale                      |
| Natalia   | Nat                      |
| Roberto   | Rob                      |
| Beatriz   | Bea                      |
+-----------+--------------------------+ 
```

## Order By and Like.
## Empleados en el departamento de 'Ventas' con salarios superiores a 52000.
```sql
sqlite> SELECT nombre, salario, departamento
   ...> FROM empleados
   ...> WHERE departamento = 'Ventas' AND salario > 52000;
+---------+---------+--------------+
| nombre  | salario | departamento |
+---------+---------+--------------+
| Carlos  | 55000.0 | Ventas       |
| Raúl    | 68000.0 | Ventas       |
| Natalia | 54000.0 | Ventas       |
+---------+---------+--------------+
```


## Empleados cuyos nombres contienen la letra 'a' y tienen salarios ordenados de manera ascendente.
```sql
sqlite> SELECT nombre, salario, departamento
   ...> FROM empleados
   ...> WHERE nombre LIKE '%a%'
   ...> ORDER BY salario ASC;
+-----------+---------+------------------+
|  nombre   | salario |   departamento   |
+-----------+---------+------------------+
| Patricia  | 47000.0 | Recursos Humanos |
| Ana       | 48000.0 | Recursos Humanos |
| Javier    | 48000.0 | Recursos Humanos |
| Sofía     | 49000.0 | Ventas           |
| Juan      | 50000.0 | Ventas           |
| Laura     | 52000.0 | Ventas           |
| Isabel    | 53000.0 | TI               |
| Natalia   | 54000.0 | Ventas           |
| Carlos    | 55000.0 | Ventas           |
| Elena     | 55000.0 | Recursos Humanos |
| María     | 60000.0 | TI               |
| Andrés    | 60000.0 | Recursos Humanos |
| Beatriz   | 63000.0 | TI               |
| Carmen    | 65000.0 | TI               |
| Raúl      | 68000.0 | Ventas           |
| Alejandro | 71000.0 | TI               |
+-----------+---------+------------------+
```

## Empleados en el departamento 'Recursos Humanos' con salarios entre 45000 y 55000.
```sql
sqlite> SELECT nombre, salario, departamento
   ...> FROM empleados
   ...> WHERE departamento = 'Recursos Humanos' AND salario BETWEEN 45000 AND 55000;
+----------+---------+------------------+
|  nombre  | salario |   departamento   |
+----------+---------+------------------+
| Ana      | 48000.0 | Recursos Humanos |
| Javier   | 48000.0 | Recursos Humanos |
| Elena    | 55000.0 | Recursos Humanos |
| Patricia | 47000.0 | Recursos Humanos |
| Roberto  | 49000.0 | Recursos Humanos |
+----------+---------+------------------+
```

## Empleados con salarios en orden descendente, limitando a los primeros 5 resultados.
```sql
sqlite> SELECT nombre, salario, departamento
   ...> FROM empleados
   ...> ORDER BY salario DESC
   ...> LIMIT 5;
+-----------+---------+--------------+
|  nombre   | salario | departamento |
+-----------+---------+--------------+
| Diego     | 72000.0 | TI           |
| Alejandro | 71000.0 | TI           |
| Pedro     | 70000.0 | TI           |
| Raúl      | 68000.0 | Ventas       |
| Carmen    | 65000.0 | TI           |
+-----------+---------+--------------+
```

## Empleados cuyos nombres comienzan con 'M' o 'N' y tienen salarios superiores a 50000.
```sql
sqlite> SELECT nombre, salario, departamento
   ...> FROM empleados
   ...> WHERE (nombre LIKE 'M%' OR nombre LIKE 'N%') AND salario > 50000;
+---------+---------+--------------+
| nombre  | salario | departamento |
+---------+---------+--------------+
| María   | 60000.0 | TI           |
| Miguel  | 51000.0 | Ventas       |
| Natalia | 54000.0 | Ventas       |
+---------+---------+--------------+
```
## Empleados en el departamento 'TI' o 'Ventas' ordenados alfabéticamente por nombre.
```sql
sqlite> SELECT nombre, salario, departamento
   ...> FROM empleados
   ...> WHERE departamento IN ('TI', 'Ventas')
   ...> ORDER BY nombre ASC;
+-----------+---------+--------------+
|  nombre   | salario | departamento |
+-----------+---------+--------------+
| Alejandro | 71000.0 | TI           |
| Beatriz   | 63000.0 | TI           |
| Carlos    | 55000.0 | Ventas       |
| Carmen    | 65000.0 | TI           |
| Diego     | 72000.0 | TI           |
| Isabel    | 53000.0 | TI           |
| Juan      | 50000.0 | Ventas       |
| Laura     | 52000.0 | Ventas       |
| María     | 60000.0 | TI           |
| Miguel    | 51000.0 | Ventas       |
| Natalia   | 54000.0 | Ventas       |
| Pedro     | 70000.0 | TI           |
| Raúl      | 68000.0 | Ventas       |
| Sofía     | 49000.0 | Ventas       |
+-----------+---------+--------------+
```
## Empleados con salarios únicos (eliminando duplicados) en orden ascendente.
```sql
sqlite> SELECT DISTINCT salario
   ...> FROM empleados
   ...> ORDER BY salario ASC;
+---------+
| salario |
+---------+
| 47000.0 |
| 48000.0 |
| 49000.0 |
| 50000.0 |
| 51000.0 |
| 52000.0 |
| 53000.0 |
| 54000.0 |
| 55000.0 |
| 60000.0 |
| 63000.0 |
| 65000.0 |
| 68000.0 |
| 70000.0 |
| 71000.0 |
| 72000.0 |
+---------+
```
## Empleados cuyos nombres terminan con 'o' o 'a' y están en el departamento 'Ventas'. 
```sql
sqlite> SELECT nombre, salario, departamento
   ...> FROM empleados
   ...> WHERE (nombre LIKE '%o' OR nombre LIKE '%a') AND departamento = 'Ventas';
+---------+---------+--------------+
| nombre  | salario | departamento |
+---------+---------+--------------+
| Laura   | 52000.0 | Ventas       |
| Sofía   | 49000.0 | Ventas       |
| Natalia | 54000.0 | Ventas       |
+---------+---------+--------------+
```

## Empleados con salarios fuera del rango de 55000 a 70000, ordenados por departamento.
```sql
sqlite> SELECT nombre, salario, departamento
   ...> FROM empleados
   ...> WHERE salario NOT BETWEEN 55000 AND 70000
   ...> ORDER BY departamento;
+-----------+---------+------------------+
|  nombre   | salario |   departamento   |
+-----------+---------+------------------+
| Ana       | 48000.0 | Recursos Humanos |
| Javier    | 48000.0 | Recursos Humanos |
| Patricia  | 47000.0 | Recursos Humanos |
| Roberto   | 49000.0 | Recursos Humanos |
| Diego     | 72000.0 | TI               |
| Isabel    | 53000.0 | TI               |
| Alejandro | 71000.0 | TI               |
| Juan      | 50000.0 | Ventas           |
| Laura     | 52000.0 | Ventas           |
| Miguel    | 51000.0 | Ventas           |
| Sofía     | 49000.0 | Ventas           |
| Natalia   | 54000.0 | Ventas           |
+-----------+---------+------------------+
```

## Empleados en el departamento 'Recursos Humanos' con nombres que no contienen la letra 'e'.
```sql
sqlite> SELECT nombre, salario, departamento
   ...> FROM empleados
   ...> WHERE departamento = 'Recursos Humanos' AND nombre NOT LIKE '%e%';
+----------+---------+------------------+
|  nombre  | salario |   departamento   |
+----------+---------+------------------+
| Ana      | 48000.0 | Recursos Humanos |
| Andrés   | 60000.0 | Recursos Humanos |
| Patricia | 47000.0 | Recursos Humanos |
+----------+---------+------------------+
```

