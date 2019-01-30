## Ejemplo de carga y tratamiento de datos desde Hive

Descarga de dataset desde terminal local
```
wget https://raw.githubusercontent.com/hortonworks/data-tutorials/master/tutorials/hdp/how-to-process-data-with-apache-hive/assets/driver_data.zip
unzip driver_data.zip
```
driver_data.zip: 

drivers.csv 

driverID | name | ssn | location | certified | wage-plan 
-|-|-|-|-|-
10 | George Vetticaden | 621011971 | 244-4532 Nulla Rd. | N | miles



timesheet.csv  

driverID | week | hours-logged | miles-logged
-|-|-|-
10 | 1 | 70 | 3300  

truck_event_text_partition.csv  

driverID | truckID | eventTime | eventType | longitude | latitude | eventKey | correlationID | driverName | routeID | routeName | eventDate
-|-|-|-|-|-|-|-|-|-|-|-
14 | 25 | 59:21.4 | Normal | -94.58 | 37.03 | 14 | 25 | 9223370572464814373 | 3.66E+18 | Adis Cesir | 160405074 | Joplin to Kansas City Route 2 | 2016-05-27-22


#### carga de ficheros .csv locales a el directorio /tmp/data en nuestro HDFS
```
scp -P 2222 <local_directory_file> root@sandbox-hdp.hortonworks.com:<sandbox_directory_file>  
scp -P 2222 ./*.csv root@sandbox-hdp.hortonworks.com:/tmp/data/
```

#### conexión con maquina sandbox y subir archivos a HDFS 
```
ssh root@localhost -p 2222
hdfs dfs -put *.csv /tmp/data/
```

#### crear la tabla temp_drivers  

Lo más práctico sería declarar la tabla con las variables que contendrá y rellenarla con "LOAD DATA INPATH..." pero para este caso práctico se declarará con una sóla variable de tipo STRING para posteriormente poder ver la selección de texto utilizando patrones mediante **regexp_extract**  
```
CREATE TABLE temp_drivers (col_value STRING) STORED AS TEXTFILE
```
#### poblar la tabla temp_drivers
```
LOAD DATA INPATH '/tmp/data/drivers.csv' OVERWRITE INTO TABLE temp_drivers
```

#### se crea una nueva tabla tipando los datos driverId, name, ssn, location, certified and the wage-plan

```
CREATE TABLE drivers (driverId INT, name STRING, ssn BIGINT, 
                      location STRING, certified STRING, wageplan STRING)
```

#### cargar los datos de temp_driver sobre driver utilizando un patron regexp

```
insert overwrite table drivers
SELECT
  regexp_extract(col_value, '^(?:([^,]*),?){1}', 1) driverId,
  regexp_extract(col_value, '^(?:([^,]*),?){2}', 1) name,
  regexp_extract(col_value, '^(?:([^,]*),?){3}', 1) ssn,
  regexp_extract(col_value, '^(?:([^,]*),?){4}', 1) location,
  regexp_extract(col_value, '^(?:([^,]*),?){5}', 1) certified,
  regexp_extract(col_value, '^(?:([^,]*),?){6}', 1) wageplan

from temp_drivers
```

#### Ahora se crea la tabla **externa** timesheet declarando las variables
Las tablas externas no eliminan el fichero origen de datos cuando se eliminan.
```
CREATE EXTERNAL TABLE timesheet (driverId INT, week INT, hours_logged INT , miles_logged INT)
row format delimited 
fields terminated by ',' 
lines terminated by '\n' 
STORED AS TEXTFILE
tblproperties ("skip.header.line.count"="1");  #eliminar la cabecera 
```

#### Cargar datos en timesheet desde documento en HDFS, LOAD DATA LOCAL INPATH... para ficheros en local.
```
LOAD DATA INPATH '/tmp/data/timesheet.csv' OVERWRITE INTO TABLE timesheet;
```

#### Ahora se calcula la suma de hora y de millas por cada conductor.

```
Select driverID, sum(hours_logged), sum(miles_logged) FROM timesheet GROUP BY driverID;
```

#### Por último se va 




