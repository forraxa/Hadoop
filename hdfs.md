#### HDFS  

**Lista de comandos HDFS**  

hdfs dfs: Para ficheros que apuntan a todos tipo de ficheros FS locales, HFTP FS, S3 FS y otros (incluido HDFS).  

hdfs fs: Para ficheros que apuntan exclusivamente a ficheros HDFS. 


Listar de comandos:
```
hdfs dfs
```
Subir un archivo a hdfs
```
hdfs dfs -put /ruta/prueba.txt /ruta-hdfs
```
Inspeccionar contenido
```
hdfs dfs -cat /ruta-hdfs/prueba.txt
```
Otros comandos
```
hdfs dfs -mkdir /ruta-hdfs/data  #crear directorio
hdfs dfs -cp /ruta-hdfs/prueba.txt /ruta-hdfs/data/  #copiar archivo dentro de HDFS
hdfs dfs rm /ruta-hdfs/prueba.txt  #eliminar archivo o directorio vacío
hdfs dfs rmr /ruta-hdfs/prueba.txt  #eliminar directorio recursivamente (incluso no vacíos)
hadoop dfs -get /ruta-hdfs/Samplefile.txt /home/  #copia de HDFS a local  
hadoop dfs -tail /ruta-hdfs/prueba.txt #ver las últimas lineas de un archivo
```

```
hdfs dfsadmin #Listar comandos administrativos
hdfs dfsadmin - report #obtener un reporte
hdfs fsck / #realizar un check
hdfs dfsadmin -printTopology #identificar número de nodos y en que rack está
hdfs dfs -du -h / #lista los directorios y el tamaño ocupado
hdfs dfs -du -h -s / #indica el tamaño ocupado total de ese directorio
```
Snapshot
```
hdfs dfsadmin -allowSnapshot /ruta-hdfs #permitir crear snapshot
hdfs dfs -createSnapshot /ruta-hdfs snap1 #Crear snapshot y darle el nombre snap1
hdfs dfs -cp /ruta-hdfs.snapshot/snap1/prueba.txt /ruta-hdfs #recuperar fichero prueba
```

