# Veremos como hacer que nuestro dominio tenga ssl 

## Usaremos [cerbot](https://certbot.eff.org/)
### Desde la pagina de cerbot se puede especificar el software y el SO que vamos a usar
```
sudo snap install core; sudo snap refresh core

```
```
sudo snap install --classic certbot

sudo ln -s /snap/bin/certbot /usr/bin/certbot
```
## Yo lo voy a instalar en apache
```
sudo certbot --apache
```

```
sudo certbot certonly --apache


sudo certbot renew --dry-run
```
