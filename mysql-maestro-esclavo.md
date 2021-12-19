# servidor

### se debe tener permisos root

## Instalamos mysql y lo iniciamos
´´´
apt install mysql-server -y
systemctl start mysql
systemctl enable mysql
´´´
## Ya instalado debemos poner contraseña root

´´´
mysql_secure_installation 
´´´

 ### Pondremos la contraseña seleccionamos 'y' le damos al 2, ponemos la nueva contraseña y le daremos 'y' al resto de las opciones hasta que sala el mensaje "all done"
 
 ## tocaremos el siguiente fichero de configuracion
 
´´´
nano /etc/mysql/mysql.conf.d/mysqld.cnf
´´´

y añadiremos lo siguiente:

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

una vez añadido reiniciamos

´´´
systemctl restart mysql
´´´
## Entramos en mysql con root
´´´
mysql -u root -p
´´´
## Ahora ponemos la informacion del cliente
la ip de la maquina servidora es 192.168.1.111
´´´
mysql> create user replica@192.168.1.111 identified with mysql_native_password by 'Pass@123';

mysql> grant replication slave on *.* to replica@192.168.1.111;

mysql> flush privileges;

mysql> show grants for replica@192.168.1.111;
´´´
![mysqlserver](https://github.com/jaimeod010/servidor-de-aplicaciones/blob/main/imagenes/mysqlserver.png)
