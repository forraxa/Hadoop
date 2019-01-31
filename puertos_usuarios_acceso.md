#### Puertos de acceso aplicaciones HDP

http://192.168.2.129:4200 #Shell  

http://192.168.2.129:8080 #Ambari  

http://192.168.2.129:50070 #HDFS  

http://192.168.2.129:9995 #Zeppelin  

http://192.168.2.129:30800 #Data Analitics  

http://192.168.2.129:9089 #Superset

http://192.168.2.129:8088/ui2 #YARN


#### Usuarios y roles:  
https://es.hortonworks.com/tutorial/learning-the-ropes-of-the-hortonworks-sandbox/


#### Reset password admin
```
ambari-admin-password-reset
```

#### Conexión con sandbox desde terminal local
```
user@hostname -p port. For example: ssh root@sandbox-hdp.hortonworks.com -p 2222
```

#### Transferir fichero desde maquina local a sandbox
```
scp -P 2222 <local_directory_file> root@sandbox-hdp.hortonworks.com:<sandbox_directory_file>
```

#### Transferir fichero desde sandbox a maquina local
```
scp -P 2222 root@sandbox-hdp.hortonworks.com:<sandbox_directory_file> <local_directory_file> 
```
