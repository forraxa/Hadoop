
1 - Tipos de datos  
2 - create, drop database  
3 - create, alter, drop table (interna, externa)  
4 - Partitions and buckets  
5 - Indexes and Views  
6 - Queries: Order y, Group By, Distribute By, Cluster By  
7 - Join and Subqueries  
8 - Operadores (Relacional, aritmético, lógico, complejo...)  
9 - Funciones incorparadas y definidas por el usuario (UDF)  
10 - ETL desde Json y XML  

## 1 - Tipos de datos

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
Date	| It's in YYYY-MM-DD format. The range of values supported for the Date type is be 0000-01-01 to 9999-12-31, dependent onsupport by the primitive Java Date type

Complex Types:

Type	| Usage
-|-
Arrays	| ARRAY<data_type> Negative values and non-constant expressions not allowed
Maps	| MAP<primitive_type, data_type> Negative values and non-constant expressions not allowed
Structs	| STRUCT<col_name :datat_type, ….. >
Union	| UNIONTYPE<data_type, datat_type, ……>


## 2 - create, drop database 

Create database <DatabaseName>
```
Create database drivers
```

Drop database <DatabaseName>
```
Drop database drivers
```

## 3 - create, alter, drop table (interna, externa)  
Las tablas externas no eliminan el fichero origen de datos cuando se elimina la tabla.

```
CREATE EXTERNAL TABLE timesheet (driverId INT, week INT, hours_logged INT , miles_logged INT)
row format delimited 
fields terminated by ',' 
lines terminated by '\n' 
STORED AS TEXTFILE
tblproperties ("skip.header.line.count"="1");  #eliminar la cabecera 
```
LOAD DATA INPATH => HDFS, LOAD DATA LOCAL INPATH => sistema de archivos local.  
```
LOAD DATA INPATH '/tmp/data/drivers.csv' OVERWRITE INTO TABLE timesheet
```
```
ALTER TABLE timesheet RENAME TO drivers;
DROP TABLE drivers;
```

## 4 - Partitions and buckets  
**Partitions**  
Dividir la tabla para obtener una mejora del rendimiento.
```
CREATE TABLE state_part(District string,Enrolments string) PARTITIONED BY(state string);

#para particionar se ha de registrar la propiedad
set hive.exec.dynamic.partition.mode=nonstrict
```

```
INSERT OVERWRITE TABLE state_part PARTITION(state)
SELECT district,enrolments,state FROM  allstates;
```
**Buckets**  
Otra manera de dividir los datos, nº de archivos = nº de buckets o clusters.

```
CREATE TABLE state_part(District string,Enrolments string, state string) 
CLUSTERED BY(state) INTO 4 BUCKETS;
```
```
FROM data
INSERT OVERWRITE TABLE state_part
SELECT District, Enrolments, state;
```


## 5 - Indexes and Views 
**index**  
Los índices permiten acelerar las consultas.  

```
Create INDEX sample_Index ON TABLE drivers(driverID)
```

**Views**  
Es una tabla para simplificar el contenido de otra tabla.  ejm. Pasar de 100 columnas a 5.  
- No se actualizan automaticamente.  
- Si la tabla cae la vista también caerá.  
- No produce una mejora de rendimiento con respecto a la tabla original.  
- Usadas como tablas transitorias o de preparación.  

```
Create VIEW Sample_View AS SELECT * FROM employees WHERE salary>25000
```

## 6 - Queries: Order y, Group By, Distribute By, Cluster By  
- Order by query  
- Group by query  
- Sort by  
- Cluster By  
- Distribute By  

**Order By**  
```
SELECT * FROM drivers ORDER BY [ASC | DESC] time;
```
**Group By**  
```
SELECT Department, count(*) FROM employees GROUP BY Department;
```
**Sort By**  
```
SELECT * FROM drivers SORT BY [ASC | DESC] time;
```
**Cluster By**  
```
SELECT  Id, Name from employees CLUSTER BY Id;
```

**Distribute By**  
```
SELECT  Id, Name from employees_guru DISTRIBUTE BY Id;
```

## 7 - Join and Subqueries 

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

### Subquery
Una consulta dentro de otra consulta.  
La consulta principal dependerá de los valores devueltos por las subconsultas.  

- Subconsultas con FROM  
- Subconsultas con WHERE  

```
SELECT col1 FROM (SELECT a+b AS col1 FROM t1) t2
```

## 8 - Operadores (Relacional, aritmético, lógico, complejo...)  
- Relational Operators  
- Arithmetic Operators  
- Logical Operators  
- Operators on Complex types  
- Complex type Constructors  

**Relational Operators**  

Built-in Operator	| Description	| Operand
-|-|-
X = Y	| TRUE if expression X is equivalent to expression Y Otherwise FALSE. | It takes all primitive types
X != Y	| TRUE if expression X is not equivalent to expression Y Otherwise FALSE. | It takes all primitive types
X < Y	| TRUE if expression X is less than expression Y Otherwise FALSE. | It takes all primitive types
X <= Y	| TRUE if expression X is less than or equal to expression Y Otherwise FALSE. | It takes all primitive types
X>Y	| TRUE if expression X is greater than expression Y Otherwise FALSE. | It takes all primitive types
X>= Y	| TRUE if expression X is greater than or equal to expression Y Otherwise FALSE. | It takes all primitive types
X IS NULL	| TRUE if expression X evaluates to NULL otherwise FALSE.	| It takes all types
X IS NOT NULL	| FALSE If expression X evaluates to NULL otherwise TRUE. | It takes all types
X LIKE Y	| TRUE If string pattern X matches to Y otherwise FALSE. | Takes only Strings
X RLIKE Y	| NULL if X or Y is NULL, TRUE if any substring of X matches the Java regular expression Y, otherwise FALSE. | Takes only Strings
X REGEXP Y	| Same as RLIKE.	| Takes only Strings

**Arithmetic Operators**  

Built-in Operator |	Description	| Operand
-|-|-
X + Y	| It will return the output of adding X and Y value.	| It takes all number types
X - Y	| It will return the output of subtracting Y from X value.	| It takes all number types
X * Y	| It will return the output of multiplying X and Y values.	| It takes all number types
X / Y	| It will return the output of dividing Y from X.	| It takes all number types
X % Y	| It will return the remainder resulting from dividing X by Y.	| It takes all number types
X & Y	| It will return the output of bitwise AND of X and Y.	| It takes all number types
X | Y	| It will return the output of bitwise OR of X and Y.	| It takes all number types
X ^ Y	| It will return the output of bitwise XOR of X and Y.	| It takes all number types
~X	| It will return the output of bitwise NOT of X.	| It takes all number types

**Logical Operators**  
Operators |	Description	| Operands
-|-|-
X AND Y	| TRUE if both X and Y are TRUE, otherwise FALSE.	| Boolean types only
X && Y	| Same as X AND Y but here we using && symbol	| Boolean types only
X OR Y	| TRUE if either X or Y or both are TRUE, otherwise FALSE.	| Boolean types only
X || Y	| Same as X OR Y but here we using || symbol	| Boolean types only
NOT X	| TRUE if X is FALSE, otherwise FALSE.	| Boolean types only
!X	| Same as NOT X but here we using! symbol	| Boolean types only


**Operators on Complex**

Operators	| Operands	| Description
-|-|-
A[n]	| A is an Array and n is an integer type	| It will return nth element in the array A. The first element has index of 0
M[key]	| M is a Map<K, V> and key has type K	| It will return the values belongs to the key in the map

**Complex type Constructors**  
Operators	| Operands	| Description
-|-|-
array	| (val1, val2, ...)	| It will create an array with the given elements as mentioned like val1, val2
Create_ union	| (tag, val1, val2, ...)	| It will create a union type with the values that is being mentioned to by the tag parameter
map	| (key1, value1, key2, value2, ...)	| It will create a map with the given key/value pairs mentioned in operands
Named_struct	| (name1, val1, name2, val2, ...)	| It will create a Struct with the given field names and values mentioned in operands
STRUCT	| (val1, val2, val3, ...)	| Creates a Struct with the given field values. Struct field names will be col1, col2, .

