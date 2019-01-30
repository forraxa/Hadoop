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

#### crear la tabla temp_drivers  

Lo más práctico sería declarar la tabla con las variables que contendrá y rellenarla con "LOAD DATA INPATH..." pero para este caso práctico se declarará con una sóla variable de tipo STRING para posteriormente poder ver la selección de texto utilizando patrones mediante **regexp_extract**  
```
CREATE TABLE temp_drivers (col_value STRING) STORED AS TEXTFILE
```







