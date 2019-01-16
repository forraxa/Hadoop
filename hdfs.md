#### HDFS  
Arrancar hdfs:  
```
/opt/hadoop/sbin/start-dfs.sh
```
Parar hdfs
```
stop-dfs.sh
```
Ver procesos java que están en uso
```
jps -l
```
Inspeccionar hdfs desde el navegador web (hadoop 3.x)
```
nodo1:9870
```
Dentro de /datos/namenode/current se almacenan los ficheros:
  - edits_000xxx: Los cambios que se van produciendo
  - edits_inprogress_xxx: Los cambios que se están produciendo en este momento
  - fsimage_000xxx: Foto o copia del sistema de fichero

**Lista de comandos HDFS**  

dfs: Muy útil para interacturar con el sistema de ficheros  

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
mkdir, cp, rm, get...
```

```
hdfs dfsadmin #Listar comandos administrativos
hdfs dfsadmin - report #obtener un reporte
hdfs fsck / #realizar un check
hdfs dfsadmin -printTopology #identificar número de nodos y en que rack está
```
Snapshot
```
hdfs dfsadmin -allowSnapshot /ruta-hdfs #permitir crear snapshot
hdfs dfs -createSnapshot /ruta-hdfs snap1 #Crear snapshot y darle el nombre snap1
hdfs dfs -cp /ruta-hdfs.snapshot/snap1/prueba.txt /ruta-hdfs #recuperar fichero prueba
```

