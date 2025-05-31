<div align="justify">
## 🔎 Parte 1: Consultas SQL

### A. Consultas Simples

1. Mostrar todos los cursos disponibles.

```sql
mysql> SELECT * FROm cursos;
+----+----------------------+-------------+----------+
| id | nombre               | profesor_id | creditos |
+----+----------------------+-------------+----------+
|  1 | Álgebra Lineal      |           1 |        6 |
|  2 | Programación I      |           2 |        5 |
|  3 | Mecánica Clásica   |           3 |        6 |
|  4 | Estructuras de Datos |           2 |        5 |
|  5 | Cálculo I           |           1 |        6 |
+----+----------------------+-------------+----------+
5 rows in set (0.000 sec)

```

2. Mostrar el nombre de todos los profesores.

```sql
mysql> Select nombre from profesores;
+------------------+
| nombre           |
+------------------+
| Dra. Ana Torres  |
| Dr. Luis Gómez  |
| Dra. Marta Díaz |
+------------------+
```

3. Listar todas las matrículas.

```sql
mysql> select * from matriculas;
+----+---------------+----------+------------+
| id | estudiante_id | curso_id | fecha      |
+----+---------------+----------+------------+
|  1 |             1 |        1 | 2021-09-01 |
|  2 |             2 |        2 | 2022-09-01 |
|  3 |             3 |        3 | 2023-09-02 |
|  4 |             4 |        4 | 2024-09-03 |
|  5 |             1 |        5 | 2020-09-04 |
|  6 |             2 |        4 | 2022-09-05 |
|  7 |             3 |        1 | 2023-09-06 |
|  8 |             4 |        2 | 2024-09-06 |
+----+---------------+----------+------------+
```

4. Ver los nombres y correos de los estudiantes.

```sql
mysql> Select nombre, email from estudiantes;
+-------------------+----------------+
| nombre            | email          |
+-------------------+----------------+
| María López     | maria@uni.edu  |
| Juan Pérez       | juan@uni.edu   |
| Lucía Fernández | lucia@uni.edu  |
| Carlos Ruiz       | carlos@uni.edu |
+-------------------+----------------+
```

5. Ver los cursos y su número de créditos.

```sql
mysql> select nombre, creditos from cursos;
+----------------------+----------+
| nombre               | creditos |
+----------------------+----------+
| Álgebra Lineal      |        6 |
| Programación I      |        5 |
| Mecánica Clásica   |        6 |
| Estructuras de Datos |        5 |
| Cálculo I           |        6 |
+----------------------+----------+
```
---

### B. Consultas con `WHERE`. Obligatorio utilizar **WHERE** donde se **combine dos o más tablas**

1. Obtener los cursos impartidos por profesores del departamento de Informática.

```sql
mysql> Select c.nombre, p.nombre from cursos as c, profesores as p where c.profesor_ID = p.id AND p.departamento="Informatica";
+----------------------+----------------+
| nombre               | nombre         |
+----------------------+----------------+
| Programacion I       | Dr. Luis Gomez |
| Estructuras de Datos | Dr. Luis Gomez |
+----------------------+----------------+
```

2. Obtener los estudiantes que viven en Madrid.

```sql
mysql> select nombre from estudiantes
    -> where ciudad = "Madrid";
+-------------+
| nombre      |
+-------------+
| Maria Lopez |
+-------------+
```

3. Mostrar los cursos con más de 5 créditos.

```sql
mysql> select nombre, creditos from cursos where creditos >5;
+------------------+----------+
| nombre           | creditos |
+------------------+----------+
| Algebra Lineal   |        6 |
| Mecanica Clasica |        6 |
| Calculo I        |        6 |
+------------------+----------+
```

4. Ver las matrículas realizadas después del año 2022.

```sql
mysql> SELECT c.nombre, m.fecha from cursos as c, matriculas as m
    -> Where m.curso_id = c.id AND m.fecha LIKE("2022%");
+----------------------+------------+
| nombre               | fecha      |
+----------------------+------------+
| Programacion I       | 2022-09-01 |
| Estructuras de Datos | 2022-09-05 |
+----------------------+------------+
```

5. Ver los cursos impartidos por la profesora “Dra. Ana Torres”.

```sql
mysql> Select c.nombre from cursos as c , profesores as p
    -> where c.profesor_id = p.id AND p.nombre="Dra. Ana Torres";
+----------------+
| nombre         |
+----------------+
| Algebra Lineal |
| Calculo I      |
+----------------+
```

---

### C. Consultas con `JOIN`.  Obligatorio utilizar **JOIN** donde se **combine dos o más tablas**

> (Devuelven el mismo resultado que las anteriores, pero usando combinaciones de tablas)

1. Mostrar cursos impartidos por profesores del departamento de Informática.

```sql
mysql> Select c.nombre from cursos as c
    -> JOIN profesores as p
    -> ON c.profesor_ID =p.id
    -> AND p.departamento="Informatica";
+----------------------+
| nombre               |
+----------------------+
| Programacion I       |
| Estructuras de Datos |
+----------------------+
```

2. Obtener estudiantes que viven en Madrid.

```sql
mysql> select nombre from estudiantes
    -> where ciudad = "Madrid";
+-------------+
| nombre      |
+-------------+
| Maria Lopez |
+-------------+
```

3. Mostrar cursos con más de 5 créditos.

```sql
mysql> select nombre, creditos from cursos where creditos >5;
+------------------+----------+
| nombre           | creditos |
+------------------+----------+
| Algebra Lineal   |        6 |
| Mecanica Clasica |        6 |
| Calculo I        |        6 |
+------------------+----------+
```

4. Listar matrículas realizadas después del año 2022.

```sql
mysql> SELECT c.nombre, m.fecha from cursos as c
    -> JOIN matriculas as m
    -> ON m.curso_id =c.id
    -> AND m.fecha LIKE("2022%");
+----------------------+------------+
| nombre               | fecha      |
+----------------------+------------+
| Programacion I       | 2022-09-01 |
| Estructuras de Datos | 2022-09-05 |
+----------------------+------------+
```

5. Mostrar los cursos impartidos por la profesora “Dra. Ana Torres”.

```sql
mysql> Select c.nombre from cursos as c
    -> JOIN profesores as p
    -> ON c.profesor_ID = p.id
    -> AND p.nombre="Dra. Ana Torres";
+----------------+
| nombre         |
+----------------+
| Algebra Lineal |
| Calculo I      |
+----------------+
```
---

### D. Consultas con Subconsultas

> (Devuelven el mismo resultado que las anteriores, pero usando subconsultas)

1. Cursos impartidos por profesores del departamento de Informática.

```sql
mysql> select nombre from(
    -> Select c.nombre from cursos as c
    -> JOIN profesores as p
    -> ON c.profesor_id = p.id
    -> AND p.departamento="Informatica")
    -> as cursos_filtrados;
+----------------------+
| nombre               |
+----------------------+
| Programacion I       |
| Estructuras de Datos |
+----------------------+
```

2. Estudiantes que viven en Madrid.

```sql
mysql> select nombre from
    -> ( select nombre from estudiantes
    -> where ciudad = "Madrid") as cuidad_filtrada;
+-------------+
| nombre      |
+-------------+
| Maria Lopez |
+-------------+
```

3. Cursos con más de 5 créditos.

```sql
mysql> SELECT nombre, creditos
    -> FROM (
    ->     SELECT * FROM cursos WHERE creditos > 5
    -> ) AS cursos_filtrados;
+------------------+----------+
| nombre           | creditos |
+------------------+----------+
| Algebra Lineal   |        6 |
| Mecanica Clasica |        6 |
| Calculo I        |        6 |
+------------------+----------+
```

4. Matrículas realizadas después del año 2022.

```sql
mysql> select nombre, fecha
    -> from(
    -> Select c.nombre, m.fecha from cursos as c
    -> JOIN matriculas as m
    -> ON m.curso_id = c.id
    -> AND m.fecha LIKE("2022%")
    -> ) as matriculas_filtradas;
+----------------------+------------+
| nombre               | fecha      |
+----------------------+------------+
| Programacion I       | 2022-09-01 |
| Estructuras de Datos | 2022-09-05 |
+----------------------+------------+
```

5. Cursos impartidos por la profesora “Dra. Ana Torres”.

```sql
mysql> select nombre from
( select c.nombre from cursos as c 
JOIN profesores as p 
ON c.profesor_id = p.id 
AND p.nombre="Dra. Ana Torres") 
as Ana_filtro;
+----------------+
| nombre         |
+----------------+
| Algebra Lineal |
| Calculo I      |
+----------------+
```

---

## 📂 Parte 2: Índices

1. Crear un índice en la columna `ciudad` de la tabla `estudiantes`.

```sql
mysql> create index cuidades ON estudiantes(ciudad);
Query OK, 0 rows affected (0.021 sec)
Records: 0  Duplicates: 0  Warnings: 0
```

2. Crear un índice en la columna `departamento` de la tabla `profesores`.

```sql
mysql> create index departamentos ON profesores(departamento);
Query OK, 0 rows affected (0.018 sec)
Records: 0  Duplicates: 0  Warnings: 0
```

3. Consultar los índices creados.

```sql
mysql> show index from profesores;
+------------+------------+---------------+--------------+--------------+-----------+-------------+----------+--------+------+------------+---------+---------------+---------+------------+
| Table      | Non_unique | Key_name      | Seq_in_index | Column_name  | Collation | Cardinality | Sub_part | Packed | Null | Index_type | Comment | Index_comment | Visible | Expression |
+------------+------------+---------------+--------------+--------------+-----------+-------------+----------+--------+------+------------+---------+---------------+---------+------------+
| profesores |          0 | PRIMARY       |            1 | id           | A         |           3 |     NULL |   NULL |      | BTREE      |         |               | YES     | NULL       |
| profesores |          1 | departamentos |            1 | departamento | A         |           3 |     NULL |   NULL | YES  | BTREE      |         |               | YES     | NULL       |
+------------+------------+---------------+--------------+--------------+-----------+-------------+----------+--------+------+------------+---------+---------------+---------+------------+

mysql> show index from estudiantes;
+-------------+------------+----------+--------------+-------------+-----------+-------------+----------+--------+------+------------+---------+---------------+---------+------------+
| Table       | Non_unique | Key_name | Seq_in_index | Column_name | Collation | Cardinality | Sub_part | Packed | Null | Index_type | Comment | Index_comment | Visible | Expression |
+-------------+------------+----------+--------------+-------------+-----------+-------------+----------+--------+------+------------+---------+---------------+---------+------------+
| estudiantes |          0 | PRIMARY  |            1 | id          | A         |           4 |     NULL |   NULL |      | BTREE      |         |               | YES     | NULL       |
| estudiantes |          1 | cuidades |            1 | ciudad      | A         |           4 |     NULL |   NULL | YES  | BTREE      |         |               | YES     | NULL       |
+-------------+------------+----------+--------------+-------------+-----------+-------------+----------+--------+------+------------+---------+---------------+---------+------------+
```

4. Eliminar ambos índices.

```sql
mysql> drop index cuidades on estudiantes;
Query OK, 0 rows affected (0.016 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> drop index departamentos on profesores;
Query OK, 0 rows affected (0.008 sec)
Records: 0  Duplicates: 0  Warnings: 0

```
---

## 🪞 Parte 3: Vistas

1. Crear una vista llamada `vista_matriculas_completas` que muestre:
   - nombre del estudiante,
   - nombre del curso,
   - fecha de la matrícula.

```sql
mysql> CREATE VIEW vista_matriculas_completas AS
    -> SELECT e.nombre as nombre_estudiante, c.nombre as nombre_curso, m.fecha FROM estudiantes as e, cursos as c, matriculas as m
    -> WHERE m.estudiante_id = e.id AND m.curso_id = c.id;
Query OK, 0 rows affected (0.017 sec)
```

2. Consultar datos desde la vista, mostrando el nombre del estudiante y la fecha de matrícula.

```sql
mysql> Select nombre_estudiante, fecha from vista_matriculas_completas;
+-------------------+------------+
| nombre_estudiante | fecha      |
+-------------------+------------+
| Maria Lopez       | 2021-09-01 |
| Juan Perez        | 2022-09-01 |
| Lucia Fernandez   | 2023-09-02 |
| Carlos Ruiz       | 2024-09-03 |
| Maria Lopez       | 2020-09-04 |
| Juan Perez        | 2022-09-05 |
| Lucia Fernandez   | 2023-09-06 |
| Carlos Ruiz       | 2024-09-06 |
+-------------------+------------+
8 rows in set (0.002 sec)

```

3. Eliminar la vista.

```sql
mysql> DROP view vista_matriculas_completas;
Query OK, 0 rows affected (0.008 sec)
```

---

## ⚙ Parte 4: Procedimiento Almacenado

1. Crear un procedimiento llamado `cursos_por_profesor` que reciba el nombre del profesor como parámetro y devuelva los cursos que imparte y su número de créditos.

```sql
mysql> CREATE PROCEDURE cursos_por_profesor(
    -> IN nombre_profesor VARCHAR(50))
    -> BEGIN
    -> SELECT c.nombre, c.creditos FROM cursos as c, profesores as p
    -> WHERE c.profesor_id = p.id
    -> AND p.nombre = nombre_profesor;
    -> END $$
```

2. Ejecutar el procedimiento con el nombre “Dr. Luis Gómez”.

```sql
mysql> CALL cursos_por_profesor("Dr. Luis Gomez");
+----------------------+----------+
| nombre               | creditos |
+----------------------+----------+
| Programacion I       |        5 |
| Estructuras de Datos |        5 |
+----------------------+----------+
2 rows in set (0.005 sec)
```

3. Eliminar el procedimiento.

```sql
mysql> DROP PROCEDURE IF EXISTS cursos_por_profesor;
Query OK, 0 rows affected (0.011 sec)
```

---

## 🔢 Parte 5: Función Definida por el Usuario

1. Crear una función llamada `total_creditos_estudiante` que reciba el ID de un estudiante y devuelva el total de créditos que ha matriculado.

```sql
mysql> CREATE FUNCTION total_creditos_estudiantes (id INT)
    -> RETURNS INT
    -> DETERMINISTIC
    -> BEGIN
    -> DECLARE total INT;
    -> SELECT SUM(c.creditos)
    -> INTO total
    -> FROM cursos as c, matriculas as m
    -> WHERE m.estudiante_id = id
    -> AND m.curso_id = c.id;
    -> RETURN total;
    -> END $$
```

2. Ejecutar la función para un estudiante específico.

```sql
mysql> SELECT total_creditos_estudiantes(2);
+-------------------------------+
| total_creditos_estudiantes(2) |
+-------------------------------+
|                            10 |
+-------------------------------+
```

3. Eliminar la función.

```sql
mysql> DROP FUNCTION IF EXISTS total_creditos_estudiantes;
Query OK, 0 rows affected (0.006 sec)
```

</div>