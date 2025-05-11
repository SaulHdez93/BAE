<div align="justify">

# Tarea 1 de trabajo con índices

<div align="center">
<img src="../../img/indices.png"/>
</div>

Un instituto de enseñanza guarda los siguientes datos de sus alumnos:
 - número de inscripción, comienza desde 1 cada año,
 - año de inscripción,
 - nombre del alumno,
 - documento del alumno,
 - domicilio,
 - ciudad,
 - provincia,
 - clave primaria: número de inscripto y año de inscripción.

Se pide: 
- Elimine la tabla "alumno" si existe. 
   ```sql
    sqlite> DROP TABLE IF EXISTS alumno;
   ``` 
- Cree la tabla definiendo una clave primaria compuesta (año de inscripción y número de 
inscripción).
   
    ```sql
    sqlite> CREATE TABLE alumno (
(x1...>     numero_inscripcion INTEGER,
(x1...>     anio_inscripcion INTEGER,
(x1...>     nombre TEXT,
(x1...>     documento TEXT,
(x1...>     domicilio TEXT,
(x1...>     ciudad TEXT,
(x1...>     provincia TEXT,
(x1...>     PRIMARY KEY (anio_inscripcion, numero_inscripcion)
(x1...> );
    ``` 
- Define los siguientes indices:
   - Un índice único por el campo "documento" y un índice común por ciudad y provincia.
    ```sql
    sqlite> CREATE UNIQUE INDEX idx_unico_documento ON alumno(documento);
    sqlite> CREATE INDEX idx_ciudad_provincia ON alumno(ciudad, provincia);
    ```
    - Vea los índices de la tabla.
    ```sql
    sqlite> .schema alumno
    CREATE TABLE alumno (
        numero_inscripcion INTEGER,
        anio_inscripcion INTEGER,
        nombre TEXT,
        documento TEXT,
        domicilio TEXT,
        ciudad TEXT,
        provincia TEXT,
        PRIMARY KEY (anio_inscripcion, numero_inscripcion)
    );
    CREATE UNIQUE INDEX idx_unico_documento ON alumno(documento);
    CREATE INDEX idx_ciudad_provincia ON alumno(ciudad, provincia);
    ```
    Uso el .schema porque en sqlite3 no existe el show index.

- Intente ingresar un alumno con clave primaria repetida.
    
    ```sql
    sqlite> INSERT INTO alumno (
    (x1...>     numero_inscripcion,
    (x1...>     anio_inscripcion,
    (x1...>     nombre,
    (x1...>     documento,
    (x1...>     domicilio,
    (x1...>     ciudad,
    (x1...>     provincia
    (x1...> ) VALUES (
    (x1...>     1, 2025, 'Juan Pérez', '12345678', 'Calle Falsa 123', 'Rosario', 'Santa Fe'
    (x1...> );
    sqlite> INSERT INTO alumno (
    (x1...>     numero_inscripcion,
    (x1...>     anio_inscripcion,
    (x1...>     nombre,
    (x1...>     documento,
    (x1...>     domicilio,
    (x1...>     ciudad,
    (x1...>     provincia
    (x1...> ) VALUES (
    (x1...>     1, 2025, 'Ana García', '87654321', 'Av. Siempreviva 742', 'Rosario', 'Santa Fe'
    (x1...> );
    Runtime error: UNIQUE constraint failed: alumno.anio_inscripcion, alumno.numero_inscripcion (19)
    ```
- Intente ingresar un alumno con documento repetido.
  ```sql
    sqlite> INSERT INTO alumno (
    (x1...>     numero_inscripcion,
    (x1...>     anio_inscripcion,
    (x1...>     nombre,
    (x1...>     documento,
    (x1...>     domicilio,
    (x1...>     ciudad,
    (x1...>     provincia
    (x1...> ) VALUES (
    (x1...>     2, 2025, 'Laura Gómez', '12345678', 'San Martín 456', 'Córdoba', 'Córdoba'
    (x1...> );
    Runtime error: UNIQUE constraint failed: alumno.documento (19)
  ```

- Ingrese varios alumnos de la misma ciudad y provincia.
    ```sql
    sqlite> INSERT INTO alumno (
    (x1...>     numero_inscripcion,
    (x1...>     anio_inscripcion,
    (x1...>     nombre,
    (x1...>     documento,
    (x1...>     domicilio,
    (x1...>     ciudad,
    (x1...>     provincia
    (x1...> ) VALUES
    ...> (2, 2025, 'María López', '23456789', 'Belgrano 100', 'Rosario', 'Santa Fe'),
    ...> (3, 2025, 'Carlos Méndez', '34567890', 'Mitre 200', 'Rosario', 'Santa Fe'),
    ...> (4, 2025, 'Lucía Fernández', '45678901', 'Urquiza 300', 'Rosario', 'Santa Fe'),
    ...> (5, 2025, 'Pedro Suárez', '56789012', 'Sarmiento 400', 'Rosario', 'Santa Fe');
    ```

- Elimina los indices creados, y muestra que ya no se encuentran.
    ```sql
    sqlite> DROP INDEX IF EXISTS idx_unico_documento;
    sqlite> DROP INDEX IF EXISTS idx_ciudad_provincia;
    ```
Verificamos que ya no existen los indices

    ```sql
    sqlite> .schema alumno
CREATE TABLE alumno (
    numero_inscripcion INTEGER,
    anio_inscripcion INTEGER,
    nombre TEXT,
    documento TEXT,
    domicilio TEXT,
    ciudad TEXT,
    provincia TEXT,
    PRIMARY KEY (anio_inscripcion, numero_inscripcion)
);
    ```
Volmemos a usar .schema por lo que dije con anterioridad que en sqlite3 no podemos usar show index.

</div>