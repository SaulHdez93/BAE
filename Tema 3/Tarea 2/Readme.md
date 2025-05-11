<div align="justify">

# Tarea 2 de trabajo con índices

<div align="center">
<img src="../../img/indices.png"/>
</div>

Una empresa guarda los siguientes datos de sus clientes, con los siguientes campos:
- documento char (8) not null,
- nombre varchar(30) not null,
- domicilio varchar(30),
- ciudad varchar(20),
- provincia varchar (20),
- telefono varchar(11)

Se pide:

- Elimine la tabla "cliente" si existe. 
  ```sql
    sqlite> DROP TABLE IF EXISTS cliente;
  ```

- Cree la tabla sin clave primaria y incluye a posteriori esta.
```sql
    sqlite> CREATE TABLE cliente (
(x1...>     documento CHAR(8) NOT NULL,
(x1...>     nombre VARCHAR(30) NOT NULL,
(x1...>     domicilio VARCHAR(30),
(x1...>     ciudad VARCHAR(20),
(x1...>     provincia VARCHAR(20),
(x1...>     telefono VARCHAR(11)
(x1...> );
```
Segudno comando añadiendo la clave primaria

```sql
  ALTER TABLE cliente
ADD PRIMARY KEY (documento);  
```
Pero en sqlite3 esa opción no funciona por lo cual voy a borrar la tabla de neuov y a añadirlo en la propia tabla cuando se crea

```sql
    sqlite> DROP TABLE IF EXISTS cliente;
sqlite>
sqlite> CREATE TABLE cliente (
(x1...>     documento CHAR(8) NOT NULL PRIMARY KEY,
(x1...>     nombre VARCHAR(30) NOT NULL,
(x1...>     domicilio VARCHAR(30),
(x1...>     ciudad VARCHAR(20),
(x1...>     provincia VARCHAR(20),
(x1...>     telefono VARCHAR(11)
(x1...> );

```


- Define los siguientes indices:
  - Un índice único por el campo "documento" y un índice común por ciudad y provincia.

   ```sql
    sqlite> CREATE UNIQUE INDEX idx_unico_documento ON cliente(documento);
    sqlite> CREATE INDEX idx_ciudad_provincia ON cliente(ciudad, provincia);
   ```     

    - Vea los índices de la tabla.
```sql
    sqlite> .schema cliente
CREATE TABLE cliente (
    documento CHAR(8) NOT NULL PRIMARY KEY,
    nombre VARCHAR(30) NOT NULL,
    domicilio VARCHAR(30),
    ciudad VARCHAR(20),
    provincia VARCHAR(20),
    telefono VARCHAR(11)
);
CREATE UNIQUE INDEX idx_unico_documento ON cliente(documento);
CREATE INDEX idx_ciudad_provincia ON cliente(ciudad, provincia);
sqlite>
```

- Agregue un índice único por el campo "telefono".

```sql
sqlite> CREATE UNIQUE INDEX idx_unico_telefono ON cliente(telefono);
sqlite> .schema cliente
CREATE TABLE cliente (
    documento CHAR(8) NOT NULL PRIMARY KEY,
    nombre VARCHAR(30) NOT NULL,
    domicilio VARCHAR(30),
    ciudad VARCHAR(20),
    provincia VARCHAR(20),
    telefono VARCHAR(11)
);
CREATE UNIQUE INDEX idx_unico_documento ON cliente(documento);
CREATE INDEX idx_ciudad_provincia ON cliente(ciudad, provincia);
CREATE UNIQUE INDEX idx_unico_telefono ON cliente(telefono);
```
Ademas de crear el indice único de telefono poenmos ademas un .schema cliente apra poder ver la estrucxtura completa en sqlite3

- Elimina los índices.

 ```sql
sqlite> DROP INDEX IF EXISTS idx_unico_documento;
sqlite> DROP INDEX IF EXISTS idx_ciudad_provincia;
sqlite> DROP INDEX IF EXISTS idx_unico_telefono;
 ```   
 Para verificar que se han eliminado los indices hacemos un .schema cliente 

 ```sql
 sqlite> .schema cliente
CREATE TABLE cliente (
    documento CHAR(8) NOT NULL PRIMARY KEY,
    nombre VARCHAR(30) NOT NULL,
    domicilio VARCHAR(30),
    ciudad VARCHAR(20),
    provincia VARCHAR(20),
    telefono VARCHAR(11)
);  
 ```  
</div>