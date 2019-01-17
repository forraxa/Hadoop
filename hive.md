#### HIVE
Permite acceder a HDFS como si fuese una base de datos  
Lenguaje de programación HiveSql, es parecido a SQL  

Tipos de datos más habituales en HIVE  

| TYPW | DESCRIPTION | EXAMPLE |
-------|-------------|----|
| TINYINT | 8-bit signed integer | 1 |
| SMALLINT | 16-bit signed integer | 1 |
| INT | 32-bit signed integer| 1 |
| BIGINT | 64-bit signed integer | 1 |
| FLOAT | 32-bit single precision floating point number | 1.0 |
| DOUBLE | 64-bit double precision floating point number | 1.0 |
| BOOLEAN | true/false value | TRUE |
| STRING | Character string | 'a',"a" |
| TIMESTAMP | Timestamp with nanosecond precision | '2012-01-02 03:04:05.123456789' |
------------------------------

Tipos complejos  

TYPE | DESCRIPTION | EXAMPLE
-----|------|--------------
ARRAY | Colección ordenada de campos. Los campos deben ser del mismo tipo | array(1,2)
MAP | Colección no ordenada de pares clave-valor. Las claves deben ser primitivas y los valores de cualquier tipo | map('a',1,'b',2)
STRUCT | Colección de campos con nombre. Los campos pueden ser de distinto tipo | struct('a',1,1.0)

##### Comandos HIVE  

**Comandos DDL** (DATA DEFINITION LANGUAGE), nos permiten crear objetos  
  - [ ] Create table  
  - [ ] Create/Drop/Alter/Use Database  
  - [ ] Create/Drop/Truncate Table  
  - [ ] Alter Table/Partition/Column  
  - [ ] Create/Drop/Alter View  
  - [ ] Create/Drop/Alter Index  
  - [ ] Create/Drop Macro  
  ...
 
 Creación de una tabla  
 ```
 create table table_name (
  id          int,
  dtQonQuery  string,
  name        string
 )
 partitioned by (date string)
 ```
 Creacin base de datos  
 ```
 Create database db1
 ```
 
 **Comandos DML** (DATA MANIPULATION LANGUAGE)  
  - [ ] LOAD
  - [ ] INSERT
  - [ ] UPDATE
  - [ ] DELETE
  - [ ] MERGE  
  
  Cargar un fichero y asociarlo a una tabla de HIVE
  ```
  LOAD DATA LOCAL INPATH '/home/datos/Escritorio/employee.txt'
  OVERWRITE INTO TABLE employee_internal;
  ```
  Realizar un doble **INSERT**
  ```
  INSERT INTO TABLE students
    VALUES('juan fernandez',35,1.28),('pedro alvarez',32,2.32);
  ```
  
  Realizar un **DELETE**
  ```
  DELETE FROM students WHERE gpa <=1,0;
  ```
  
  Realizar un **MERGE** y **UPDATE**
  ```
  merge into customer
  using(select * from new_customer_stage) sub
  on sub.id = customer.id
  when matched then update set name = sub.name, state = sub.new_state
  when not matched then insert values (sub.id, sub.name, sub.state);
  ```
**Comandos SELECT**
```
SELECT [ALL / DISTINCT] select_expr, select_expr...
FROM table_reference
[WHERE where_condition]
[GROUP BY col_list]
[HAVING having_condition]
[CLUSTER BY col_list | [DISTRIBUTE BY col_list][SORT BY col_list]]
[LIMIT number]
;
```

**Hive** también cuenta con:    
- Mathematical Functions  
- Collection Functionss  
- Type Conversion Functions  
- Date Functions  
- Conditional Functions  
- String Functions  
- Misc Functions  

**Ejemplos básicos**  
```
SELECT * FROM employee WHERE salary>30000;

SELECT Id, Name, Dept FROM employee ORDER BY DEPT;

SELECT Dept, count(*) FROM employee GROUP BY DEPT;

SELECT c.ID, c.NAME, c.AGE, o.AMOUNT FROM CUSTOMERS c JOIN ORDERS o ON(c.ID = o.CUSTOMER_ID);

SELECT c.ID, c.NAME, o.AMOUNT, o.DATE FROM CUSTOMERS c LEFT OUTER JOIN ORDERS o ON(c.ID = o.CUSTOMER_ID);
```
