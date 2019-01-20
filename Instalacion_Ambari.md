## Instalación de un cluster básico Hadoop con Ambari   

#### Crear red interna con los nodos requeridos (Centos7)  
  - Declarar nodos en /etc/hosts    
      192.168.0.101 nodo1  
      192.168.0.102 nodo2  
      192.168.0.103 nodo3  
  - Crear authorized_keys desde usuario root para conectar por ssh entre nodos sin contraseña  
      ```
      #desde nodo1
      ssh-keygen
      cd /root/.ssh
      cp id_rsa.pub authorized_keys
      scp authorized_keys nodo2:/root/.ssh
      
      #desde nodo2
      ssh-keygen
      cd /root/.ssh
      cat id_rsa.pub >> authorized_keys
      scp authorized_keys nodo3:/root/.ssh
      
      #desde nodo3
      ssh-keygen
      cd /root/.ssh
      cat id_rsa.pub >> authorized_keys
      scp authorized_keys nodo2:/root/.ssh
      scp authorized_keys nodo1:/root/.ssh
      
      ```
#### Instalación de Ambari  
```
#insertar repo de ambari
wget -nv http://public-repo-1.hortonworks.com/ambari/centos7/2.x/updates/2.7.3.0/ambari.repo -O /etc/yum.repos.d/ambari.repo

#listado
yum repolist

#instalación del servidor
yum install ambari-server

#configuración del servidor, -s:desatendida aceptando valores por defecto
ambari-server setup -s

#iniciar servidor
ambari-server start

#desde navegador web para entrar a la interface
localhost:8080
user:admin
pass:admin
```
      
      
