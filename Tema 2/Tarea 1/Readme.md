Este es un repositorio creado para realizar las práctias y ejercicios de Base de Datos 
## Creación de Tabla  
```sql
sqlite> create table ejemplo( id integer, texto text, entero integer, decimal real, fecha date, booleano boolean);
```

### Inserción de Datos  
```sql
sqlite> insert into ejemplo(id, texto, entero, decimal, fecha, booleano) values('30', 'ejemplo30', '74', '85.3', '2024-10-05', '1');
sqlite> insert into ejemplo(id, texto, entero, decimal, fecha, booleano) values('31', 'ejemplo31', '18', '11.8', '2024-11-12', '0');
sqlite> insert into ejemplo(id, texto, entero, decimal, fecha, booleano) values('32', 'ejemplo32', '83', '47.6', '2024-12-28', '1');
sqlite> insert into ejemplo(id, texto, entero, decimal, fecha, booleano) values('33', 'ejemplo33', '38', '32.7', '2024-01-15', '0');
sqlite> insert into ejemplo(id, texto, entero, decimal, fecha, booleano) values('34', 'ejemplo34', '101', '70.2', '2025-02-01', '1');
sqlite> insert into ejemplo(id, texto, entero, decimal, fecha, booleano) values('35', 'ejemplo35', '52', '18.4', '2025-03-20', '0');
sqlite> insert into ejemplo(id, texto, entero, decimal, fecha, booleano) values('36', 'ejemplo36', '67', '83.9', '2025-04-06', '1');
sqlite> insert into ejemplo(id, texto, entero, decimal, fecha, booleano) values('37', 'ejemplo37', '43', '28.3', '2025-05-13', '0');
sqlite> insert into ejemplo(id, texto, entero, decimal, fecha, booleano) values('38', 'ejemplo38', '58', '50.6', '2025-06-30', '1');
sqlite> insert into ejemplo(id, texto, entero, decimal, fecha, booleano) values('39', 'ejemplo39', '9', '8.7', '2025-07-17', '0');
sqlite> insert into ejemplo(id, texto, entero, decimal, fecha, booleano) values('40', 'ejemplo40', '82', '65.1', '2025-08-23', '1');
```

### Paso 3.1 - Selección de Datos  
```sql
sqlite> select * from ejemplo;
```

| id | texto      | entero | decimal | fecha      | booleano |
|----|-----------|--------|---------|------------|----------|
| 30 | ejemplo30 | 74     | 85.3    | 2024-10-05 | 1        |
| 31 | ejemplo31 | 18     | 11.8    | 2024-11-12 | 0        |
| 32 | ejemplo32 | 83     | 47.6    | 2024-12-28 | 1        |
| 33 | ejemplo33 | 38     | 32.7    | 2024-01-15 | 0        |
| 34 | ejemplo34 | 101    | 70.2    | 2025-02-01 | 1        |
| 35 | ejemplo35 | 52     | 18.4    | 2025-03-20 | 0        |
| 36 | ejemplo36 | 67     | 83.9    | 2025-04-06 | 1        |
| 37 | ejemplo37 | 43     | 28.3    | 2025-05-13 | 0        |
| 38 | ejemplo38 | 58     | 50.6    | 2025-06-30 | 1        |
| 39 | ejemplo39 | 9      | 8.7     | 2025-07-17 | 0        |
| 40 | ejemplo40 | 82     | 65.1    | 2025-08-23 | 1        |

### Paso 3.2 - Selección de Datos con Condición  
```sql
sqlite> SELECT * FROM ejemplo WHERE entero > 50;
```

| id | texto      | entero | decimal | fecha      | booleano |
|----|-----------|--------|---------|------------|----------|
| 30 | ejemplo30 | 74     | 85.3    | 2024-10-05 | 1        |
| 32 | ejemplo32 | 83     | 47.6    | 2024-12-28 | 1        |
| 34 | ejemplo34 | 101    | 70.2    | 2025-02-01 | 1        |
| 35 | ejemplo35 | 52     | 18.4    | 2025-03-20 | 0        |
| 36 | ejemplo36 | 67     | 83.9    | 2025-04-06 | 1        |
| 38 | ejemplo38 | 58     | 50.6    | 2025-06-30 | 1        |
| 40 | ejemplo40 | 82     | 65.1    | 2025-08-23 | 1        |

### Paso 4.1 - Selección de Datos con Condición  
```sql
sqlite> DELETE FROM ejemplo WHERE booleano = 1;
sqlite> select*from ejemplo;
```

| id | texto      | entero | decimal | fecha      | booleano |
|----|-----------|--------|---------|------------|----------|
| 31 | ejemplo31 | 18    | 85.3    | 2024-10-05 | 1        |
| 32 | ejemplo32 | 83     | 47.6    | 2024-12-28 | 1        |
| 34 | ejemplo34 | 101    | 70.2    | 2025-02-01 | 1        |
| 35 | ejemplo35 | 52     | 18.4    | 2025-03-20 | 0        |
| 36 | ejemplo36 | 67     | 83.9    | 2025-04-06 | 1        |
| 38 | ejemplo38 | 58     | 50.6    | 2025-06-30 | 1        |
| 40 | ejemplo40 | 82     | 65.1    | 2025-08-23 | 1        |
| id |   texto   | entero | decimal |   fecha    | booleano |
|----|-----------|--------|---------|------------|----------|
| 31 | ejemplo31 | 18     | 11.8    | 2024-11-12 | 0        |
| 33 | ejemplo33 | 38     | 32.7    | 2024-01-15 | 0        |
| 35 | ejemplo35 | 52     | 18.4    | 2025-03-20 | 0        |
| 37 | ejemplo37 | 43     | 28.3    | 2025-05-13 | 0        |
| 39 | ejemplo39 | 9      | 8.7     | 2025-07-17 | 0        |
### Paso 4.2
```sql
sqlite> UPDATE ejemplo
   ...> SET texto = 'Modificado'
   ...> WHERE entero < 30;
sqlite>
sqlite> select*from ejemplo;
```
| id |   texto    | entero | decimal |   fecha    | booleano |
|----|------------|--------|---------|------------|----------|
| 31 | Modificado | 18     | 11.8    | 2024-11-12 | 0        |
| 33 | ejemplo33  | 38     | 32.7    | 2024-01-15 | 0        |
| 35 | ejemplo35  | 52     | 18.4    | 2025-03-20 | 0        |
| 37 | ejemplo37  | 43     | 28.3    | 2025-05-13 | 0        |
| 39 | Modificado | 9      | 8.7     | 2025-07-17 | 0        |

### Paso 4.4

```sql
sqlite> DELETE FROM ejemplo WHERE entero < 50;
sqlite> select*from ejemplo;
```
| id |   texto   | entero | decimal |   fecha    | booleano |
|----|-----------|--------|---------|------------|----------|
| 35 | ejemplo35 | 52     | 18.4    | 2025-03-20 | 0        |
### Paso 4.3

Hice primero el paso 4.4 por eso solo se incrementará una fila.

```sql
sqlite> UPDATE ejemplo
   ...> SET entero = entero + 10
   ...> WHERE booleano = 0;
sqlite> select*from ejemplo;
```
| id |   texto   | entero | decimal |   fecha    | booleano |
|----|-----------|--------|---------|------------|----------|
| 35 | ejemplo35 | 62     | 18.4    | 2025-03-20 | 0        |
