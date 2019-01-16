##### Yarn
Arrancar Yarn
```
start-yarn.sh
```
Gestionar cluster desde navegador nombre-maquina:puerto
```
nodo1:8088
```
Crear histórico de hadoop para futuras consultar
```
mr-jobhistory-daemon.sh start historyserver
```
Ejecutar un proceso
```
hadoop jar hadoop-mapreduce-examplexxx.jar wordcount /ruta-origen /ruta-salida
```
Ejemplo de compilado y lanzamiento de un fichero java contra el cluster hadoop  
```
#Con la clase que nos proporciona java crear clases .class del fichero Contarpalabras.java
hadoop com.sun.tools.javac.Main Contarpalabras.java 

#crear fichero Contarpalabras.jar con todas las clases .class
jar cf Contarpalabras.jar Cont*.class 

#Usar la clase Contarpalabras que se encuentra dentro de Contarpalabras.jar sobre prueba.txt y guardar salida en hdfs 
hadoop jar Contarpalabras.jar Contarpalabras /ruta-hdfs/prueba.txt /ruta-salida-en-hdfs 
```
