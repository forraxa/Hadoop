#### Ejemplo de carga y tratamiento de datos desde Hive

Descarga de dataset desde terminal local
```
wget https://raw.githubusercontent.com/hortonworks/data-tutorials/master/tutorials/hdp/how-to-process-data-with-apache-hive/assets/driver_data.zip
unzip driver_data.zip
```
driver_data.zip: 

drivers.csv 

driverID | name | ssn | location | certified | wage-plan  
---------|------|---- |----------|-----------|--------



timesheet.csv  

driverID | week | hours-logged | miles-logged
-|-|-|-  

truck_event_text_partition.csv  

driverID | truckID | eventTime | eventType | longitude | latitude | eventKey | correlationID | driverName | routeID | routeName | eventDate
-|-|-|-|-|-|-|-|-|-|-|-



