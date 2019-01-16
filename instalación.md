#### Instalación de Hadoop  

- Descargar hadoop y copiar en /opt/hadoop/
- Instalar Java
- Configurar variables de entorno en /home/usuario/.bashrc   
    ```
    export HADOOP_HOME=/opt/hadoop  
    export JAVA_HOME=/usr/java/jdk1.8.0_191-amd64  
    export PATH=$PATH:$HADOOP_HOME/bin:$HADOOP_HOME/sbin 
    ```
- Editar /etc/hosts y apuntar a la ip de nuestra maquina  
   10.0.2.15 nodo1  
- Configurar ssh para que los nodos se comuniquen  
   ssh-keygen para crear clave pública y privada de cada nodo  
   Se crean las claves públicas y se comparten con los otros nodos dentro de autorized_keys  

```
Ficheros de configuración: 

/opt/hadoop/etc/hadoop  
 - core-site.xml: Configuración del cluster  
 - hdfs-site.xml: Configuración de HDFS  
 - mapred-site.xml: Configuración de MapReduce  
 - yarn-site.xml: Configuración de trabajo de Yarn  
```

- Configurar core.site. xml y hdfs-site.xml  
core-site.xml:
```
<configuration>
	<property>
		<name>fs.defaultFS</name>
		<value>hdfs://nodo1:9000</value>
	</property>
</configuration>
``` 
hdfs-site.xml:  
```
<configuration>
	<property>
		<name>dfs.replication</name>
		<value>1</value>
	</property>
	<property>
		<name>dfs.namenode.name.dir</name>
		<value>/datos/namenode</value>
	</property>
	<property>
		<name>dfs.datanode.data.dir</name>
		<value>/datos/datanode</value>
	</property>
</configuration>
``` 
- Formatear hdfs para que inicializar  
```
hadoop namenode-format
```



