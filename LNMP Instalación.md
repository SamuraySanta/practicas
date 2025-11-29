
GitHub link:
https://github.com/SamuraySanta/practicas

# 1. Instalación de Ubuntu Server

En esta guía utilizaremos **KVM** como software de virtualización y la imagen ISO **ubuntu-live-server-24.04**. Esta maquina es una clonación de la usada en LAMP.

Especificaciones de hardware:

- 4GB de RAM
- 2 vCPU
- 30GB de almacenamiento
- Controladores **VirtIO** para la NIC y el almacenamiento

![[Pasted image 20251027140511.png]]

**Nombre de host**: ubuserver-web  
**Usuario**: user  
**Contraseña**: qwer  

Instala **OpenSSH-server** durante el proceso de instalación marcando la casilla correspondiente.

![[Pasted image 20251027141304.png]]

Reinicia la máquina virtual al final de la instalación.

# 2. Instalar Nginx

Lo instalamos con el siguiente comando:

~~~bash
apt install nginx
~~~

![[Pasted image 20251126230119.png]]

Tras la instalación podemos añadir las reglas del firewall con el siguiente comando:

~~~bash
ufw allow 'Nginx HTTP'
~~~

Comprobamos la conexión desde el navegador conectándonos a la URL `http://[IP_SERVER]`.

![[Pasted image 20251126230507.png]]

Vamos a modificar la configuración por defecto de Nginx, sobrescribiendo el fichero `/etc/nginx/sites-available/default`:

~~~
server {  
    listen 80 default_server;  
    listen [::]:80 default_server;  
  
    root /var/www/html;  
    index index.php index.html index.htm index.nginx-debian.html;  
  
    server_name _;  
  
    location / {  
           index index.php index.html index.htm;  
       }  
  
    location ~ \.php$ {  
           fastcgi_pass unix:/run/php/php-fpm.sock;  
           fastcgi_index index.php;  
           fastcgi_param  SCRIPT_FILENAME  $document_root$fastcgi_script_name;  
           include fastcgi_params;  
       }  
}
~~~

Creamos un index en `/var/www/html/` y comprobamos la conexión en el navegador:

![[Pasted image 20251129171414.png]]

# 3. Instalación de MySQL-Server

Para instalar **MySQL-server**, ejecuta el siguiente comando en la terminal de la máquina virtual:

~~~bash
sudo apt install mysql-server -y
~~~

![[Pasted image 20251126231210.png]]

Ahora tenemos que habilitar el servicio **mysql.service** con el siguiente comando:

![[Pasted image 20251103131837.png]]

Comprobamos que el servicio esta ejecutandose correctamente con el comando: 

```bash
systemctl status mysql
```

Aplicaremos una configuración más segura a MySQL. Esto se puede hacer rápidamente ejecutando el script oficial `mysql_secure_installation`.

**Las siguientes capturas de pantalla** ilustran el proceso:

![[Pasted image 20251108192850.png]]

![[Pasted image 20251108192915.png]]


# 4. Instalación de PHP

Ejecuta el siguiente comando para instalar **PHP** y sus dependencias:

```bash
install php8.3-fpm php-mysql
```

Comprobamos la versión de PHP:

```bash
 php -v
```

Crear el primer fichero .php para comprobar que funciona:

1. Creamos el fichero:

~~~
sudo vim /var/www/html/phpinfo.php
~~~

2. Añadimos el siguiente contenido:

~~~
<?php echo phpinfo(); ?>
~~~

3. Reiniciamos el servicio:

```bash
systemctl restart php8.3-fpm
```

4. Nos conectamos al fichero con http:[IP_Server]/phpinfo.php

![[Pasted image 20251129170918.png]]
















