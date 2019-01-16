#### Instalación de Hadoop  

- Descargar hadoop y copiar en /opt/hadoop/
- Instalar Java
- Configurar variables de entorno en /home/usuario/.bashrc   
    ```
    export HADOOP_HOME=/opt/hadoop  
    export JAVA_HOME=/usr/java/jdk1.8.0_191-amd64  
    export PATH=$PATH:$HADOOP_HOME/bin:$HADOOP_HOME/sbin 
    ```
- Editar /etc/hosts y apuntar nuestra ip a nuestra maquina  
   10.0.2.15 nodo1  
- Configurar ssh para que los nodos se comuniquen  
   ssh-keygen para crear clave pública y privada de cada nodo  
   Se crean las claves públicas y se comparten con los otros nodos dentro de autorized_keys  


" ficheros de configuración "   

/opt/hadoop/etc/hadoop  
 - core-site.xml: Configuración del cluster  
 - hdfs-site.xml: Configuración de HDFS  
 - mapred-site.xml: Configuración de MapReduce  
 - yarn-site.xml: Configuración de trabajo de Yarn  
 
 
Este es un ejemplo de "código en línea"
