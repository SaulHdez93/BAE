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
```

| nombre_mayusculas |
|-------------------|
| JUAN              |
| MARÍA             |
| CARLOS            |
| ANA               |
| PEDRO             |
| LAURA             |
| JAVIER            |
| CARMEN            |
| MIGUEL            |
| ELENA             |
| DIEGO             |
| SOFÍA             |
| ANDRÉS            |
| ISABEL            |
| RAÚL              |
| PATRICIA          |
| ALEJANDRO         |
| NATALIA           |
| ROBERTO           |
| BEATRIZ           |

## Funciones Numéricas

### Calcula el valor absoluto del salario de todos los empleados
```sql
sqlite> SELECT nombre, ABS(salario) AS salario_absoluto, departamento FROM empleados;
```

| nombre   | salario_absoluto | departamento        |
|----------|------------------|----------------------|
| Juan     | 50000.0          | Ventas              |
| María   | 60000.0          | TI                  |
| Carlos   | 55000.0          | Ventas              |
| Ana      | 48000.0          | Recursos Humanos    |
| Pedro    | 70000.0          | TI                  |
| Laura    | 52000.0          | Ventas              |
| Javier   | 48000.0          | Recursos Humanos    |
| Carmen   | 65000.0          | TI                  |
| Miguel   | 51000.0          | Ventas              |
| Elena    | 55000.0          | Recursos Humanos    |
| Diego    | 72000.0          | TI                  |
| Sofía   | 49000.0          | Ventas              |
| Andrés   | 60000.0          | Recursos Humanos    |
| Isabel   | 53000.0          | TI                  |
| Raúl     | 68000.0          | Ventas              |
| Patricia | 47000.0          | Recursos Humanos    |
| Alejandro| 71000.0          | TI                  |
| Natalia  | 54000.0          | Ventas              |
| Roberto  | 49000.0          | Recursos Humanos    |
| Beatriz  | 63000.0          | TI                  |
## Funciones de Fecha y Hora

### Muestra la fecha actual
```sql
sqlite> SELECT DATE('now') AS fecha_actual;
```

| fecha_actual |
|--------------|
| 2025-03-17   |

### Calcula el promedio de salarios de todos los empleados
```sql
sqlite> SELECT AVG(salario) AS promedio_salarios FROM empleados;
```

| promedio_salarios |
|-------------------|
| 57000.0          |

### Convierte la cadena '123' a un valor entero.
```sql
sqlite> SELECT CAST('123' AS INTEGER) AS valor_entero;
```

| valor_entero |
|--------------|
| 123          |


## Funciones de Manipulación de Cadenas
### Concatena el nombre y el departamento de cada empleado
```sql
sqlite> SELECT nombre || departamento AS nombre_departamento
   ...> FROM empleados;

```

| nombre_departamento |
|---------------------|
| JuanVentas              |
| MaríaTI             |
| CarlosVentas           |
| AnaRecursosHumanos               |
| PedroTI             |
| LauraVentas             |
| JavierrecursosHumanos            |
| CarmenTI            |
| MiguelVentas            |
| ElenaRecursosHumanos             |
| DiegoTI             |
| SofiaVentas             |
| AndrésRecursosHumanos            |
| IsabelTI            |
| RaúlVentas          |
| PatriciaRecursosHumanos          |
| ALEJANDRO         |
| NATALIA           |
| ROBERTO           |
| BEATRIZ           |