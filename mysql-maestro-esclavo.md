# servidor

### se debe tener permisos root

## Instalamos mysql y lo iniciamos
```
apt install mysql-server -y
systemctl start mysql
systemctl enable mysql
```
## Ya instalado debemos poner contraseña root

```
mysql_secure_installation 
```

 ### Pondremos la contraseña seleccionamos 'y' le damos al 2, ponemos la nueva contraseña y le daremos 'y' al resto de las opciones hasta que sala el mensaje "all done"
 
 ## tocaremos el siguiente fichero de configuracion
 
```
nano /etc/mysql/mysql.conf.d/mysqld.cnf
```

y añadiremos lo siguiente:
```
default_authentication_plugin=mysql_native_password
pid-file = /var/run/mysqld/mysqld.pid
socket = /var/run/mysqld/mysqld.sock
datadir = /var/lib/mysql
log-error = /var/log/mysql/error.log
server-id = 1
log-bin = /var/log/mysql/mysql-bin.log
tmpdir = /tmp
binlog_format = ROW
max_binlog_size = 500M
sync_binlog = 1
expire-logs-days = 7
slow_query_log
```
una vez añadido reiniciamos

```
systemctl restart mysql
´´´
## Entramos en mysql con root
```
mysql -u root -p
```
## Ahora ponemos la informacion del cliente
```
la ip de la maquina servidora es 192.168.2.88

mysql> create user replica@192.168.1.111 identified with mysql_native_password by 'Pass@123';

mysql> grant replication slave on *.* to replica@192.168.2.88;

mysql> flush privileges;

mysql> show grants for replica@192.168.2.88;
```
```
![mysqlserver](https://github.com/jaimeod010/servidor-de-aplicaciones/blob/main/IMAGENES/MASTERMYSQL.png)

# Esclavo
## Instalamos mysql

```apt-get update && sudo apt-get install mysql-client mysql-server
service mysql status

```
## Añadimos estas lineas al archivo de configuracion de mysql

```
nano /etc/mysql/mysql.conf.d/mysqld.cnf
```

```
default_authentication_plugin=mysql_native_password
log_bin = /var/log/mysql/mysql-bin.log
server-id = 2
read_only = 1
tmpdir = /tmp
binlog_format = ROW
max_binlog_size = 500M
sync_binlog = 1
expire-logs-days = 7
slow_query_log = 1
```

## Ahora reiniciamos el servicio

```
 systemctl restart mysql
```

## Entramos a mysql 
```
mysql -u root -p
```
## 1.- Paramos el servicio

```
mysql> STOP SLAVE;

```
## 2.- Ponemos los datos del servidor
```
mysql> CHANGE MASTER TO MASTER_HOST='192.168.2.173', MASTER_USER='replica', MASTER_PASSWORD='Pass@123', MASTER_LOG_FILE='mysql-bin.000003', MASTER_LOG_POS=1050;
```

## 3.- Iniciamos el servicio

```
mysql> START SLAVE;

```

## 4.- Comprobamos el estado del esclavo
```
SHOW SLAVE STATUS\G
```

![esclavo](https://github.com/jaimeod010/servidor-de-aplicaciones/blob/main/IMAGENES/ESCLAVOMYSQL.png)
