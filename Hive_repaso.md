
1 - Tipos de datos  
2 - create, drop database  
3 - create, alter, drop table (interna, externa)  
4 - Partitions and buckets  
5 - Index and Views  
6 - Queries: Order y, Group By, Distribute By, Cluster By  
7 - Join and Subqueries  
8 - Operadores (Relacional, aritmético, lógico, complejo...)  
9 - Funciones incorparadas y definidas por el usuario (UDF)  
10 - ETL desde Json y XML  

## Tipos de datos

- Numeric Types  
- String Types  
- Date/Time Types  
- Complex Types  

Numeric Types:

Type | Memory allocation
-|-
TINY INT |	Its 1-byte signed integer (-128 to 127)
SMALL INT	| 2-byte signed integer (-32768 to 32767)
INT	| 4 –byte signed integer ( -2,147,484,648 to 2,147,484,647)
BIG INT	| 8 byte signed integer
FLOAT	| 4 – byte single precision floating point number
DOUBLE	| 8- byte double precision floating point number
DECIMAL	| We can define precision and scale in this Type

String Types:  

Type |	Length
-|-
CHAR	| 255
VARCHAR	| 1 to 65355
STRING	| We can define length here(No Limit)

Date/Time Types:

Type	| Usage
-|-
Timestamp |	Supports traditional Unix timestamp with optional nanosecond precision
Date	| It's in YYYY-MM-DD format.
  | The range of values supported for the Date type is be 0000-01-01 to 9999-12-31, dependent onsupport by the primitive Java Date type

Complex Types:

Type	| Usage
-|-
Arrays	| ARRAY<data_type> Negative values and non-constant expressions not allowed
Maps	| MAP<primitive_type, data_type> Negative values and non-constant expressions not allowed
Structs	| STRUCT<col_name :datat_type, ….. >
Union	| UNIONTYPE<data_type, datat_type, ……>


### Joins (join, left outer join, right outer join, full outer join)
Unión de dos o más tablas  

**JOIN**:  
Muestra las filas que coincidan en ambas tablas.  
```
SELECT c.Id, c.Name, c.Age, o.Amount FROM sample_joins c JOIN sample_joins1 o ON(c.Id=o.Id);
```
**LEFT OUTER JOIN**:  
Muestra todas las filas de la tabla izquierda y las que coincidan en de la tabla izquierda.  
```
SELECT c.Id, c.Name, o.Amount FROM sample_joins c LEFT OUTER JOIN sample_joins1 o ON(c.Id=o.Id)
```
**RIGHT OUTER JOIN**:  
Muestra todas las filas de la tabla izquierda y las que coincidan en de la tabla izquierda.  
```
  SELECT c.Id, c.Name, o.Amount FROM sample_joins c RIGHT OUTER JOIN sample_joins1 o ON(c.Id=o.Id)
```
**FULL OUTER JOIN**:  
Muestra todas las filas de ambas tablas.  
```
SELECT c.Id, c.Name, o.Amount FROM sample_joins c FULL OUTER JOIN sample_joins1 o ON(c.Id=o.Id)
```

