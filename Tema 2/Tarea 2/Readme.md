### Tarea 2

Crea la db `tarea2.db` y crea la tabla de propietarios:

```sh
C:\Users\ese_s\Desktop\project\tarea5\tarea1>sqlite3 tarea2.db
SQLite version 3.49.1 2025-02-18 13:38:58
Enter ".help" for usage hints.
sqlite> CREATE TABLE Propietarios (
   ...>   id INTEGER PRIMARY KEY AUTOINCREMENT,
   ...>   nombre TEXT NOT NULL,
   ...>   apellido TEXT NOT NULL,
   ...>   dni TEXT UNIQUE
   ...> );
sqlite>
sqlite> CREATE TABLE Vehiculos (
   ...>   id INTEGER PRIMARY KEY AUTOINCREMENT,
   ...>   marca TEXT NOT NULL,
   ...>   modelo TEXT NOT NULL,
   ...>   anio INTEGER NOT NULL,
   ...>   id_propietario INTEGER,
   ...>   FOREIGN KEY (id_propietario) REFERENCES Propietarios (id)
   ...> );
sqlite>
```
### Paso 2

```sql
sqlite> INSERT INTO Propietarios (nombre, apellido, dni)
   ...> VALUES ('Maria', 'Lopez', '87654321B');
sqlite> INSERT INTO Vehiculos (marca, modelo, anio, id_propietario)
   ...> VALUES ('Ford', 'Fiesta', 2019, (SELECT id FROM Propietarios WHERE dni = '87654321B'));
sqlite> INSERT INTO Propietarios (nombre, apellido, dni)
   ...> VALUES ('Carlos', 'Ruiz', '11111111C');
sqlite> INSERT INTO Vehiculos (marca, modelo, anio, id_propietario)
   ...> VALUES ('Nissan', 'Sentra', 2020, (SELECT id FROM Propietarios WHERE dni = '11111111C'));
sqlite> VALUES ('Toyota', 'Corolla', 2018, (SELECT id FROM Propietarios WHERE dni = '87654321B'));
sqlite> INSERT INTO Propietarios (nombre, apellido, dni)
   ...> VALUES('Javier', 'Leon','77777777I');
sqlite> INSERT INTO Vehiculos (marca, modelo, anio, id_propietario)
   ...> VALUES ('honda', 'CR-V', 2018, (SELECT id FROM Propietarios WHERE dni = '77777777I'));
sqlite> INSERT INTO Propietarios (nombre, apellido, dni)
   ...> VALUES('Lucia', 'Castillo','88888888J');
sqlite> INSERT INTO Vehiculos (marca, modelo, anio, id_propietario)
   ...> VALUES ('Nissan', 'Altima', 2017, (SELECT id FROM Propietarios WHERE dni = '88888888J'));
sqlite> INSERT INTO Propietarios (nombre, apellido, dni)
   ...> VALUES('Luis', 'Gonzalez','999999999K');
sqlite> INSERT INTO Vehiculos (marca, modelo, anio, id_propietario)
   ...> VALUES ('Chevrolet', 'Malibu', 2019, (SELECT id FROM Propietarios WHERE dni = '99999999K'));
sqlite> INSERT INTO Propietarios (nombre, apellido, dni)
   ...> VALUES('Marta', 'Diaz','10101010L');
sqlite> INSERT INTO Vehiculos (marca, modelo, anio, id_propietario)
   ...> VALUES ('Toyota', 'Camry', 2020, (SELECT id FROM Propietarios WHERE dni = '10101010L'));
sqlite> INSERT INTO Propietarios (nombre, apellido, dni)
   ...> VALUES('Victor', 'Vargas','11111112M');
sqlite> INSERT INTO Vehiculos (marca, modelo, anio, id_propietario)
   ...> VALUES ('Honda', 'Accord', 2018, (SELECT id FROM Propietarios WHERE dni = '11111112M'));
sqlite> INSERT INTO Propietarios (nombre, apellido, dni)
   ...> VALUES('Elena', 'Castro','12121212N');
sqlite> INSERT INTO Vehiculos (marca, modelo, anio, id_propietario)
   ...> VALUES ('Ford', 'Explorer', 2021, (SELECT id FROM Propietarios WHERE dni = '12121212N'));
sqlite> INSERT INTO Propietarios (nombre, apellido, dni)
   ...> VALUES('Roberto', 'Blanco','13131313O');
sqlite> INSERT INTO Vehiculos (marca, modelo, anio, id_propietario)
   ...> VALUES ('Nissan', 'Rogue', 2017, (SELECT id FROM Propietarios WHERE dni = '13131313O'));
sqlite> INSERT INTO Propietarios (nombre, apellido, dni)
   ...> VALUES('Natalia', 'Paredes','14141414P');
sqlite> INSERT INTO Vehiculos (marca, modelo, anio, id_propietario)
   ...> VALUES ('Volkswagen', 'Jetta', 2019, (SELECT id FROM Propietarios WHERE dni = '14141414P'));
sqlite> INSERT INTO Propietarios (nombre, apellido, dni)
   ...> VALUES('Fernando', 'Herrera','15151515Q');
sqlite> INSERT INTO Vehiculos (marca, modelo, anio, id_propietario)
   ...> VALUES ('Chevrolet', 'Equinox', 2018, (SELECT id FROM Propietarios WHERE dni = '15151515Q'));
sqlite> INSERT INTO Propietarios (nombre, apellido, dni)
   ...> VALUES('Clara', 'Soto','16161616R');
sqlite> INSERT INTO Vehiculos (marca, modelo, anio, id_propietario)
   ...> VALUES ('Toyota', 'Highlander', 2020, (SELECT id FROM Propietarios WHERE dni = '16161616R'));
sqlite> INSERT INTO Propietarios (nombre, apellido, dni)
   ...> VALUES('Sergio', 'Mendoza','17171717S');
sqlite> VALUES ('Honda', 'Odyssey', 2016, (SELECT id FROM Propietarios WHERE dni = '17171717S'))
sqlite> INSERT INTO Vehiculos (marca, modelo, anio, id_propietario)
   ...> VALUES ('Honda', 'Odyssey', 2016, (SELECT id FROM Propietarios WHERE dni = '17171717S'));
sqlite> INSERT INTO Propietarios (nombre, apellido, dni)
   ...> VALUES('Patricia', 'Navarro','18181818T');
sqlite> INSERT INTO Vehiculos (marca, modelo, anio, id_propietario)
   ...> VALUES ('Nissan', 'Murano', 2019, (SELECT id FROM Propietarios WHERE dni = '18181818T'));
```
### Paso 3

Seleccionar todos los propietarios:

```sql
sqlite> select * from Propietarios;
```
| id |  nombre  | apellido  |    dni     |
|----|----------|-----------|------------|
| 1  | Juan     | Perez     | 12345678A  |
| 2  | Maria    | Lopez     | 87654321B  |
| 3  | Carlos   | Ruiz      | 11111111C  |
| 4  | Laura    | Gomes     | 22222222D  |
| 5  | Pedro    | Martinez  | 33333333E  |
| 6  | Ana      | Fernandez | 44444444F  |
| 7  | Diego    | Sanchez   | 55555555G  |
| 8  | Diego    | Sanchez   | 66666666H  |
| 9  | Javier   | Leon      | 77777777I  |
| 10 | Lucia    | Castillo  | 88888888J  |
| 11 | Luis     | Gonzalez  | 999999999K |
| 12 | Marta    | Diaz      | 10101010L  |
| 13 | Victor   | Vargas    | 11111112M  |
| 14 | Elena    | Castro    | 12121212N  |
| 15 | Roberto  | Blanco    | 13131313O  |
| 16 | Natalia  | Paredes   | 14141414P  |
| 17 | Fernando | Herrera   | 15151515Q  |
| 18 | Clara    | Soto      | 16161616R  |
| 19 | Sergio   | Mendoza   | 17171717S  |
| 20 | Patricia | Navarro   | 18181818T  |

### Listar todos los vehículos

```sql
sqlite> select * from Vehiculos;
```
| id |   marca    |   modelo   | anio | id_propietario |
|----|------------|------------|------|----------------|
| 1  | Ford       | Fiesta     | 2019 | 1              |
| 2  | Ford       | Fiesta     | 2019 | 2              |
| 3  | Nissan     | Sentra     | 2020 | 3              |
| 4  | Chevrolet  | Spark      | 2017 | 4              |
| 5  | Honda      | Civic      | 2016 | 5              |
| 6  | Ford       | Mustang    | 2021 | 6              |
| 7  | Toyota     | RAV4       | 2019 | 7              |
| 8  | honda      | CR-V       | 2018 | 9              |
| 9  | Nissan     | Altima     | 2017 | 10             |
| 10 | Chevrolet  | Malibu     | 2019 |                |
| 11 | Toyota     | Camry      | 2020 | 12             |
| 12 | Honda      | Accord     | 2018 | 13             |
| 13 | Ford       | Explorer   | 2021 | 14             |
| 14 | Nissan     | Rogue      | 2017 | 15             |
| 15 | Volkswagen | Jetta      | 2019 | 16             |
| 16 | Chevrolet  | Equinox    | 2018 | 17             |
| 17 | Toyota     | Highlander | 2020 | 18             |
| 18 | Honda      | Odyssey    | 2016 | 19             |
| 19 | Nissan     | Murano     | 2019 | 20             |

### Seleccionar solo los nombres y apellidos de los propietarios

```sql
sqlite> SELECT nombre, apellido FROM Propietarios;
```
|  nombre  | apellido  |
|----------|-----------|
| Juan     | Perez     |
| Maria    | Lopez     |
| Carlos   | Ruiz      |
| Laura    | Gomes     |
| Pedro    | Martinez  |
| Ana      | Fernandez |
| Diego    | Sanchez   |
| Diego    | Sanchez   |
| Javier   | Leon      |
| Lucia    | Castillo  |
| Luis     | Gonzalez  |
| Marta    | Diaz      |
| Victor   | Vargas    |
| Elena    | Castro    |
| Roberto  | Blanco    |
| Natalia  | Paredes   |
| Fernando | Herrera   |
| Clara    | Soto      |
| Sergio   | Mendoza   |
| Patricia | Navarro   |

### Listar todas las marcas y modelos de los vehículos

```sql
sqlite> SELECT marca, modelo FROM Vehiculos;
```
|   marca    |   modelo   |
|------------|------------|
| Ford       | Fiesta     |
| Ford       | Fiesta     |
| Nissan     | Sentra     |
| Chevrolet  | Spark      |
| Honda      | Civic      |
| Ford       | Mustang    |
| Toyota     | RAV4       |
| honda      | CR-V       |
| Nissan     | Altima     |
| Chevrolet  | Malibu     |
| Toyota     | Camry      |
| Honda      | Accord     |
| Ford       | Explorer   |
| Nissan     | Rogue      |
| Volkswagen | Jetta      |
| Chevrolet  | Equinox    |
| Toyota     | Highlander |
| Honda      | Odyssey    |
| Nissan     | Murano     |

### Seleccionar solo los propietarios con apellido "Perez"

```sql
sqlite> SELECT * FROM Propietarios WHERE apellido = 'Perez';
```
| id | nombre | apellido |    dni    |
|----|--------|----------|-----------|
| 1  | Juan   | Perez    | 12345678A |

### Listar todos los vehículos con año 2019

```sql
sqlite> SELECT * FROM Vehiculos WHERE anio = 2019;
| id |   marca    | modelo | anio | id_propietario |
|----|------------|--------|------|----------------|
| 1  | Ford       | Fiesta | 2019 | 1              |
| 2  | Ford       | Fiesta | 2019 | 2              |
| 7  | Toyota     | RAV4   | 2019 | 7              |
| 10 | Chevrolet  | Malibu | 2019 |                |
| 15 | Volkswagen | Jetta  | 2019 | 16             |
| 19 | Nissan     | Murano | 2019 | 20             |
```
### Seleccionar propietarios que tienen vehículos de la marca "Toyota"

```sql
sqlite> SELECT Propietarios.*
   ...> FROM Propietarios
   ...> JOIN Vehiculos ON Propietarios.id = Vehiculos.id_propietario
   ...> WHERE Vehiculos.marca = 'Toyota';
```
| id | nombre | apellido |    dni    |
|----|--------|----------|-----------|
| 7  | Diego  | Sanchez  | 55555555G |
| 12 | Marta  | Diaz     | 10101010L |
| 18 | Clara  | Soto     | 16161616R |

### Listar vehículos con marca "Ford" y modelo "Fiesta"

```sql
sqlite> SELECT * FROM Vehiculos
   ...> WHERE marca = 'Ford' AND modelo = 'Fiesta';
```
| id | marca | modelo | año | id_propietario |
|----|-------|--------|-----|----------------|
| 1  | Ford  | Fiesta | 2019| 1              |
| 2  | Ford  | Fiesta | 2019| 2              |

### Seleccionar propietarios con DNI "12345678A".

```sql
SELECT * FROM Propietarios WHERE dni = '12345678A';
```

id | nombre | apellido |    dni    |
|----|--------|----------|-----------|
| 1  | Juan   | Perez    | 12345678A |


### Listar vehículos que pertenecen al propietario con ID 5.
```sql
SELECT * FROM Vehiculos WHERE id_propietario = 5;
**Paso 4:**
**Actualizar el nombre de un propietario con DNI "12345678A".**
```

```sql
UPDATE Propietarios
SET nombre = 'Pepe'
WHERE dni = '12345678A';
**Modificar el año de un vehículo con ID 3 a 2022:**
```

```sql
UPDATE Vehiculos
SET anio = 2022
```sql
WHERE id = 3;
UPDATE Vehiculos
SET modelo = 'Micra'
WHERE marca = 'Nissan';
```

```sql

UPDATE Propietarios
SET apellido = 'Gomez'
WHERE id = 7;
```

```sql

UPDATE Vehiculos
SET marca = 'Renault'
WHERE modelo = 'Fiesta';
```
Así quedarían las tablas resultantes
## Propietarios  
```sql
sqlite> SELECT * FROM Propietarios;
```

| id | nombre   | apellido  | dni        |
|----|---------|-----------|------------|
| 1  | Pepe    | Perez     | 12345678A  |
| 2  | Maria   | Lopez     | 87654321B  |
| 3  | Carlos  | Ruiz      | 11111111C  |
| 4  | Laura   | Gomes     | 22222222D  |
| 5  | Pedro   | Martinez  | 33333333E  |
| 6  | Ana     | Fernandez | 44444444F  |
| 7  | Diego   | Gomez     | 55555555G  |
| 8  | Diego   | Sanchez   | 66666666H  |
| 9  | Javier  | Leon      | 77777777I  |
| 10 | Lucia   | Castillo  | 88888888J  |
| 11 | Luis    | Gonzalez  | 999999999K |
| 12 | Marta   | Diaz      | 10101010L  |
| 13 | Victor  | Vargas    | 11111112M  |
| 14 | Elena   | Castro    | 12121212N  |
| 15 | Roberto | Blanco    | 13131313O  |
| 16 | Natalia | Paredes   | 14141414P  |
| 17 | Fernando| Herrera   | 15151515Q  |
| 18 | Clara   | Soto      | 16161616R  |
| 19 | Sergio  | Mendoza   | 17171717S  |
| 20 | Patricia| Navarro   | 18181818T  |

## Vehículos  
```sql
sqlite> SELECT * FROM Vehiculos;
```

| id | marca      | modelo      | año  | id_propietario |
|----|-----------|------------|------|---------------|
| 1  | Renault   | Fiesta     | 2019 | 1             |
| 2  | Renault   | Fiesta     | 2019 | 2             |
| 3  | Nissan    | Micra      | 2022 | 3             |
| 4  | Chevrolet | Spark      | 2017 | 4             |
| 5  | Honda     | Civic      | 2016 | 5             |
| 6  | Ford      | Mustang    | 2021 | 6             |
| 7  | Toyota    | RAV4       | 2019 | 7             |
| 8  | Honda     | CR-V       | 2018 | 9             |
| 9  | Nissan    | Micra      | 2017 | 10            |
| 10 | Chevrolet | Malibu     | 2019 |               |
| 11 | Toyota    | Camry      | 2020 | 12            |
| 12 | Honda     | Accord     | 2018 | 13            |
| 13 | Ford      | Explorer   | 2021 | 14            |
| 14 | Nissan    | Micra      | 2017 | 15            |
| 15 | VW        | Jetta      | 2019 | 16            |
| 16 | Chevrolet | Equinox    | 2018 | 17            |
| 17 | Toyota    | Highlander | 2020 | 18            |
| 18 | Honda     | Odyssey    | 2016 | 19            |
| 19 | Nissan    | Micra      | 2019 | 20            |
