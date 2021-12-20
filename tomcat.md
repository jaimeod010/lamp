# Instalacion tomcat
```
 apt install tomcat9 tomcat9-common tomcat9-user tomcat9-docs tomcat9-examples  tomcat9-admin -y
 ```
### modificamos la configuracion para poder entrar desde administrador
```
nano /etc/tomcat9/tomcat-users.xml

```
### Añadimos las siguientes lineas dentro de la etiqueta tomcat-users

```
<role rolename="manager-gui"/>

<user username="tomcat" password="s3cret" roles="manager-gui"/>

```

![tomcat](https://github.com/jaimeod010/servidor-de-aplicaciones/blob/main/IMAGENES/tomcat.png)
