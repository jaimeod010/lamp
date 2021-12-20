
# Apache

## Habilitar modulos

```
a2enmod dav_fs
a2enmod dav
```
## modificar archivo 000-default.conf

```
nano /etc/apache2/sites
```




# Nginx

## tenemos que tocar 2 archivos:

### /etc/nginx/nginx.conf

```
nano /etc/nginx/nginx.conf

```
y añadir las siguientes lineas debajo de http{

```
	upstream backend{

		server localhost;

		server jaime777.ddns.net;


```

### tenemos que crear el load balancer
```
cd /etc/nginx/conf.d

nano load-balancing.conf
```
 añadiremos lo siguiente :
 
 ```
 upstream backends{

        server 192.168.2.173;

        server 103.23.61.48;

    }

	

    server {

#        listen      80;

	listen	443;

        location / {

#	        proxy_redirect      off;

	        proxy_set_header    X-Real-IP $remote_addr;

	        proxy_set_header    X-Forwarded-For $proxy_add_x_forwarded_for;

	        proxy_set_header    Host $http_host;

	        proxy_set_header X-Forwarded-Proto $scheme;

		proxy_pass http://backend;

	}

}


```



