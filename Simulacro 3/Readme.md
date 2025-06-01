<div align="justify">
1. Mostrar las columnas de la tabla `estudiantes`.

```sql
mysql> SELECT * FROM estudiantes;
+----+-----------------+----------------+-----------+
| id | nombre          | email          | ciudad    |
+----+-----------------+----------------+-----------+
|  1 | Maria Lopez     | maria@uni.edu  | Madrid    |
|  2 | Juan Perez      | juan@uni.edu   | Barcelona |
|  3 | Lucia Fernandez | lucia@uni.edu  | Valencia  |
|  4 | Carlos Ruiz     | carlos@uni.edu | Sevilla   |
+----+-----------------+----------------+-----------+
4 rows in set (0.000 sec)
```

2. Mostrar las columnas de la tabla `cursos`.

```sql
mysql> SELECT * FROM cursos;
+----+----------------------+-------------+----------+
| id | nombre               | profesor_id | creditos |
+----+----------------------+-------------+----------+
|  1 | Algebra Lineal       |           1 |        6 |
|  2 | Programacion I       |           2 |        5 |
|  3 | Mecanica Clasica     |           3 |        6 |
|  4 | Estructuras de Datos |           2 |        5 |
|  5 | Calculo I            |           1 |        6 |
+----+----------------------+-------------+----------+
5 rows in set (0.000 sec)

```

3. Mostrar las columnas de la tabla `matriculas`.

```sql
mysql> SELECT * FROM matriculas;
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

---

## 📊 Parte 2: Consultas Avanzadas sobre Datos

4. Mostrar cada estudiante con la cantidad de cursos en los que está matriculado.

```sql
mysql> SELECT e.nombre, COUNT(m.curso_id) AS total_cursos
    -> FROM estudiantes e
    -> LEFT JOIN matriculas m ON e.id = m.estudiante_id
    -> GROUP BY e.id;
+-----------------+--------------+
| nombre          | total_cursos |
+-----------------+--------------+
| Maria Lopez     |            2 |
| Juan Perez      |            2 |
| Lucia Fernandez |            2 |
| Carlos Ruiz     |            2 |
+-----------------+--------------+
8 rows in set (0.000 sec)
```

5. Mostrar cada estudiante con el total de créditos acumulados.

```sql
mysql> SELECT e.nombre, COALESCE(SUM(c.creditos), 0) AS total_creditos
    -> FROM estudiantes e
    -> LEFT JOIN matriculas m ON e.id = m.estudiante_id
    -> LEFT JOIN cursos c ON m.curso_id = c.id
    -> GROUP BY e.id;
+-----------------+----------------+
| nombre          | total_creditos |
+-----------------+----------------+
| Maria Lopez     |             12 |
| Juan Perez      |             10 |
| Lucia Fernandez |             12 |
| Carlos Ruiz     |             10 |
+-----------------+----------------+
```

6. Mostrar cursos con la cantidad de estudiantes matriculados, ordenados de mayor a menor.

```sql
mysql> SELECT c.nombre, COUNT(m.estudiante_id) AS total_estudiantes
    -> FROM cursos c
    -> LEFT JOIN matriculas m ON c.id = m.curso_id
    -> GROUP BY c.id
    -> ORDER BY total_estudiantes DESC;
+----------------------+-------------------+
| nombre               | total_estudiantes |
+----------------------+-------------------+
| Algebra Lineal       |                 2 |
| Programacion I       |                 2 |
| Estructuras de Datos |                 2 |
| Mecanica Clasica     |                 1 |
| Calculo I            |                 1 |
+----------------------+-------------------+
```

7. Mostrar la media de créditos por curso.

```sql
mysql> SELECT avg(creditos) FROM cursos;
+---------------+
| avg(creditos) |
+---------------+
|        5.6000 |
+---------------+
1 row in set (0.000 sec)
```

8. Listar los cursos que no tienen estudiantes matriculados.

```sql
mysql> SELECT c.nombre
    -> FROM cursos c
    -> LEFT JOIN matriculas m ON c.id = m.curso_id
    -> WHERE m.id IS NULL;
Empty set (0.001 sec)
```

9. Mostrar el nombre del profesor y cuántos cursos imparte.

```sql
mysql> SELECT p.nombre, COUNT(c.id) AS cursos_imparte
    -> FROM profesores p
    -> LEFT JOIN cursos c ON p.id = c.profesor_id
    -> GROUP BY p.id;
+-----------------+----------------+
| nombre          | cursos_imparte |
+-----------------+----------------+
| Dra. Ana Torres |              2 |
| Dr. Luis Gomez  |              2 |
| Dra. Marta Diaz |              1 |
+-----------------+----------------+
5 rows in set (0.000 sec)
```

10. Mostrar los profesores que no imparten ningún curso.

```sql
   mysql> SELECT p.nombre
    -> FROM profesores p
    -> LEFT JOIN cursos c ON p.id = c.profesor_id
    -> WHERE c.id IS NULL;
Empty set (0.000 sec)

```

11. Mostrar la ciudad con mayor número de estudiantes registrados.

```sql
mysql> SELECT ciudad, COUNT(*) AS total
    -> FROM estudiantes
    -> GROUP BY ciudad
    -> ORDER BY total DESC
    -> LIMIT 1;
+--------+-------+
| ciudad | total |
+--------+-------+
| Madrid |     1 |
+--------+-------+
```

12. Mostrar estudiantes que están matriculados en más de 1 curso.

```sql
mysql> SELECT e.nombre, COUNT(m.id) AS total_matriculas
    -> FROM estudiantes e
    -> JOIN matriculas m ON e.id = m.estudiante_id
    -> GROUP BY e.id
    -> HAVING total_matriculas > 1;
+-----------------+------------------+
| nombre          | total_matriculas |
+-----------------+------------------+
| Maria Lopez     |                2 |
| Juan Perez      |                2 |
| Lucia Fernandez |                2 |
| Carlos Ruiz     |                2 |
+-----------------+------------------+
```

13. Listar cursos junto a su clasificación según créditos:
    - 6 o más: "Alta carga"
    - Menos de 6: "Carga estándar"

```sql
mysql> SELECT nombre,
    ->   IF(creditos >= 6, 'Alta carga', 'Carga estndar') AS clasificacion
    -> FROM cursos;SELECT nombre,
+----------------------+---------------+
| nombre               | clasificacion |
+----------------------+---------------+
| Algebra Lineal       | Alta carga    |
| Programacion I       | Carga estndar |
| Mecanica Clasica     | Alta carga    |
| Estructuras de Datos | Carga estndar |
| Calculo I            | Alta carga    |
+----------------------+---------------+
```

14. Listar estudiantes y clasificar su carga académica:
    - Más de 12 créditos: "Carga Alta"
    - 6 a 12 créditos: "Carga Media"
    - Menos de 6 créditos: "Carga Baja"

```sql
SELECT e.nombre,
  SUM(c.creditos) AS total_creditos,
  IF(SUM(c.creditos) >= 12, 'Carga Alta',
     IF(SUM(c.creditos) >= 6, 'Carga Media', 'Carga Baja')) AS clasificacion
FROM estudiantes e
LEFT JOIN matriculas m ON e.id = m.estudiante_id
LEFT JOIN cursos c ON m.curso_id = c.id
GROUP BY e.id;
+-----------------+----------------+---------------+
| nombre          | total_creditos | clasificacion |
+-----------------+----------------+---------------+
| Maria Lopez     |             12 | Carga Media   |
| Juan Perez      |             10 | Carga Media   |
| Lucia Fernandez |             12 | Carga Media   |
| Carlos Ruiz     |             10 | Carga Media   |
+-----------------+----------------+---------------+
```

15. Mostrar cursos en los que se haya matriculado al menos un estudiante de Sevilla.

```sql
mysql> SELECT c.nombre FROM cursos as c
    -> JOIN matriculas as m ON m.curso_id = c.id
    -> JOIN estudiantes as e ON m.estudiante_id = e.id
    -> WHERE e.ciudad = "Sevilla";
+----------------------+
| nombre               |
+----------------------+
| Estructuras de Datos |
| Programacion I       |
+----------------------+
2 rows in set (0.001 sec)
```

16. Listar los cursos impartidos por profesores del departamento de Matemáticas.

```sql
mysql> SELECT c.nombre FROM cursos as c
    -> JOIN profesores as p
    -> ON c.profesor_id = p.id
    -> WHERE p.departamento = "Matematicas";
+----------------+
| nombre         |
+----------------+
| Algebra Lineal |
| Calculo I      |
+----------------+
2 rows in set (0.000 sec)
```

17. Mostrar los cursos en los que se haya inscrito algún estudiante antes del año 2022.

```sql
mysql> SELECT DISTINCT c.nombre
    -> FROM cursos c
    -> JOIN matriculas m ON c.id = m.curso_id
    -> WHERE YEAR(m.fecha) < 2022;
+----------------+
| nombre         |
+----------------+
| Algebra Lineal |
| Calculo I      |
+----------------+
```

18. Mostrar estudiantes que han cursado materias impartidas por el profesor “Dr. Luis Gómez”.

```sql
mysql> SELECT DISTINCT e.nombre from estudiantes as e 
JOIN matriculas as m ON m.estudiante_id = e.id 
JOIN cursos as c ON m.curso_id = c.id 
JOIN profesores as p ON c.profesor_id = p.id
 WHERE p.nombre = "Dr. Luis Gomez";
+-------------+
| nombre      |
+-------------+
| Juan Perez  |
| Carlos Ruiz |
+-------------+
2 rows in set (0.003 sec)

```

19. Mostrar los cursos más recientes (última matrícula por curso).

```sql
mysql> SELECT c.nombre, MAX(m.fecha) AS ultima_matricula
    -> FROM cursos c
    -> JOIN matriculas m ON c.id = m.curso_id
    -> GROUP BY c.id;
+----------------------+------------------+
| nombre               | ultima_matricula |
+----------------------+------------------+
| Algebra Lineal       | 2023-09-06       |
| Programacion I       | 2024-09-06       |
| Mecanica Clasica     | 2023-09-02       |
| Estructuras de Datos | 2024-09-03       |
| Calculo I            | 2020-09-04       |
+----------------------+------------------+
```

20. Mostrar el número total de estudiantes por departamento del profesor que imparte el curso.

```sql
mysql> SELECT p.departamento, COUNT(DISTINCT m.estudiante_id) AS total_estudiantes
    -> FROM profesores p
    -> JOIN cursos c ON p.id = c.profesor_id
    -> JOIN matriculas m ON c.id = m.curso_id
    -> GROUP BY p.departamento;
+--------------+-------------------+
| departamento | total_estudiantes |
+--------------+-------------------+
| Fisica       |                 1 |
| Informatica  |                 2 |
| Matematicas  |                 2 |
+--------------+-------------------+
```

---

## ⚙ Parte 3: Procedimiento Almacenado

1. Crear un procedimiento llamado `inscribir_estudiante` que reciba:
   - ID del estudiante
   - ID del curso
   - Fecha de inscripción  
   El procedimiento debe:
   - Verificar que el estudiante no esté ya matriculado en ese curso.
   - Si no lo está, insertarlo en `matriculas`; si ya lo está, lanzar un error.

```sql

```

> El **ERROR es opcional, dado que esta parte no la hemos trabajado pero el if si**.

2. Ejecutar el procedimiento para inscribir al estudiante con ID 1 en el curso con ID 2.

```sql

```

> Debe de salir el **ERROR** y en caso de no tener el error no hacer **nada**.

3. Eliminar el procedimiento.


```sql

```

---

## 🪞 Parte 4: Vistas

1. Crear una vista llamada `resumen_matriculas` que muestre:
   - Nombre del estudiante
   - Nombre del curso
   - Nombre del profesor
   - Fecha de matrícula

```sql
mysql> CREATE view resumen_matriculas AS
    -> SELECT e.nombre as nombre, c.nombre as curso, p.nombre as profesor, m.fecha as fecha
    -> FROM estudiantes as e
    -> JOIN matriculas as m ON m.estudiante_id = e.id
    -> JOIN cursos as c ON m.curso_id = c.id
    -> JOIN profesores as p ON c.profesor_id = p.id;
Query OK, 0 rows affected (0.017 sec)
```

2. Consultar los datos desde la vista, mostrando nombre del estudiante y curso.

```sql

mysql> SELECT nombre, curso from resumen_matriculas;
+-----------------+----------------------+
| nombre          | curso                |
+-----------------+----------------------+
| Maria Lopez     | Algebra Lineal       |
| Juan Perez      | Programacion I       |
| Lucia Fernandez | Mecanica Clasica     |
| Carlos Ruiz     | Estructuras de Datos |
| Maria Lopez     | Calculo I            |
| Juan Perez      | Estructuras de Datos |
| Lucia Fernandez | Algebra Lineal       |
| Carlos Ruiz     | Programacion I       |
+-----------------+----------------------+
8 rows in set (0.001 sec)
```

3. Eliminar la vista.

```sql
mysql> drop view resumen_matriculas;
Query OK, 0 rows affected (0.006 sec)

```

---

## 🧮 Parte 5: Función Definida por el Usuario

1. Crear una función llamada `promedio_creditos_por_anio` que reciba un año como parámetro y devuelva el promedio de créditos matriculados por estudiante ese año.

```sql
mysql> DELIMITER //
mysql> CREATE FUNCTION promedio_creditos_por_anio(anio INT)
    -> RETURNS DECIMAL(5,2)
    -> DETERMINISTIC
    -> BEGIN
    ->   DECLARE promedio DECIMAL(5,2);
    ->   SELECT AVG(c.creditos) INTO promedio
    ->   FROM matriculas m
    ->   JOIN cursos c ON m.curso_id = c.id
    ->   WHERE YEAR(m.fecha) = anio;
    ->   RETURN promedio;
    -> END;
    -> //
Query OK, 0 rows affected (0.043 sec)
```

2. Ejecutar la función para el año 2023.

```sql
mysql> SELECT promedio_creditos_por_anio(2023);
+----------------------------------+
| promedio_creditos_por_anio(2023) |
+----------------------------------+
|                             6.00 |
+----------------------------------+
```

3. Eliminar la función.

```sql
mysql> DROP FUNCTION IF EXISTS promedio_creditos_por_anio;
Query OK, 0 rows affected (0.014 sec)
```

---

## 📂 Parte 6: Índices

1. Crear un índice en la columna `fecha` de la tabla `matriculas`.

```sql

mysql> CREATE index idx_fecha ON matriculas(fecha);
Query OK, 0 rows affected (0.047 sec)
Records: 0  Duplicates: 0  Warnings: 0

```

2. Crear un índice compuesto en la tabla `matriculas` sobre `estudiante_id` y `curso_id`.

```sql
mysql> CREATE index idx_ids ON matriculas(estudiante_id, curso_id);
Query OK, 0 rows affected (0.021 sec)
Records: 0  Duplicates: 0  Warnings: 0
```

3. Consultar los índices de la tabla `matriculas`.

```sql
mysql> SHOW index from matriculas;
+------------+------------+-----------+--------------+---------------+-----------+-------------+----------+--------+------+------------+---------+---------------+---------+------------+
| Table      | Non_unique | Key_name  | Seq_in_index | Column_name   | Collation | Cardinality | Sub_part | Packed | Null | Index_type | Comment | Index_comment | Visible | Expression |
+------------+------------+-----------+--------------+---------------+-----------+-------------+----------+--------+------+------------+---------+---------------+---------+------------+
| matriculas |          0 | PRIMARY   |            1 | id            | A         |           0 |     NULL |   NULL |      | BTREE      |         |               | YES     | NULL       |
| matriculas |          1 | curso_id  |            1 | curso_id      | A         |           0 |     NULL |   NULL | YES  | BTREE      |         |               | YES     | NULL       |
| matriculas |          1 | idx_fecha |            1 | fecha         | A         |           0 |     NULL |   NULL | YES  | BTREE      |         |               | YES     | NULL       |
| matriculas |          1 | idx_ids   |            1 | estudiante_id | A         |           0 |     NULL |   NULL | YES  | BTREE      |         |               | YES     | NULL       |
| matriculas |          1 | idx_ids   |            2 | curso_id      | A         |           0 |     NULL |   NULL | YES  | BTREE      |         |               | YES     | NULL       |
+------------+------------+-----------+--------------+---------------+-----------+-------------+----------+--------+------+------------+---------+---------------+---------+------------+
```

4. Eliminar ambos índices.

```sql
drop index 
```

---

## 🕵️ Parte 7: Trigger de Auditoría

1. Crear una tabla llamada `auditoria_matriculas` que registre:
   - Tipo de operación (INSERT)
   - ID del estudiante
   - ID del curso
   - Fecha y hora de la operación
   - Usuario que realizó la acción

```sql
CREATE TABLE auditoria_matriculas (
  operacion VARCHAR(10),
  estudiante_id INT,
  curso_id INT,
  fecha_hora DATETIME,
  usuario VARCHAR(100)
);
```

2. Crear un trigger `AFTER INSERT` sobre `matriculas` que inserte un registro en `auditoria_matriculas` al realizar una matrícula.

```sql
mysql> DELIMITER //
mysql> CREATE TRIGGER after_insert_matricula
    -> AFTER INSERT ON matriculas
    -> FOR EACH ROW
    -> BEGIN
    ->   INSERT INTO auditoria_matriculas(operacion, estudiante_id, curso_id, fecha_hora, usuario)
    ->   VALUES ('INSERT', NEW.estudiante_id, NEW.curso_id, NOW(), CURRENT_USER());
    -> END;
    -> //
 mysql> DELIMITER ;   
Query OK, 0 rows affected (0.009 sec)
```

3. Consultar los registros de la auditoría.

```sql
mysql> SELECT * FROM auditoria_matriculas;
Empty set (0.002 sec)
```

4. Eliminar el trigger y la tabla de auditoría.

```sql
mysql> DROP TRIGGER IF EXISTS after_insert_matricula;
Query OK, 0 rows affected (0.009 sec)

mysql> DROP TABLE IF EXISTS auditoria_matriculas;
Query OK, 0 rows affected (0.012 sec)

```

## Notas

> Siempre se utiliza:
>  - **CREATE ..**.
>  - **DROP ..**.
>  - **FUNCIONES/TRIGGERS/PROCEDIMIENTOS** utilizan **sentencias SQL**.

## Referencias

- [Procedimientos en MySql](https://github.com/jpexposito/code-learn/blob/main/primero/bae/unidad-7/PROCEDIMIENTOS.md).
- [Funciones en MySql](https://github.com/jpexposito/code-learn/blob/main/primero/bae/unidad-7/FUNCIONES.md).
- [Vistas en MySql](https://github.com/jpexposito/code-learn/blob/main/primero/bae/unidad-6/Vistas.md).
- [Triggers en MySql](https://github.com/jpexposito/code-learn/blob/main/primero/bae/unidad-7/TRIGERS.md).

</div>