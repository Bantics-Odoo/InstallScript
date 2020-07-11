# [Odoo](https://www.odoo.com "Odoo's Homepage") Install Script

Este script esta basado en " https://github.com/Yenthe666/InstallScript" el cual asimismo, salio desde el de André Schenkels (https://github.com/aschenkels-ictstudio/openerp-install-scripts) pero trataremos de ir acomodandolo a las necesidades de Argentina.
Se trabajará sobre la versión de odoo_install_debian.sh ya que es la distribución que mas usamos en la cooperativa, tanto en entornos de desarrollo como de producción.

Se sacaron las opciones de deploy en servidor, como la creacion de usuario especifico, e instalacion como servicio, centrandonos en el entorno de desarrollo.
Se saco tambien lo referido a la version enterprise.

Basicamente, va a hacer un update de apt y una actualización del sistema.
Luego instala PostgreSQL y crea el usuario definido como OE_USER.
Instala paquetes basicos del sistema, como python3, pip, git, wget, entre otros, como asi tambien npm y Wkhtmltopdf en caso de haberlo configurado.





This script will also give you the ability to define an xmlrpc_port in the .conf file that is generated under /etc/
This script can be safely used in a multi-odoo code base server because the default Odoo port is changed BEFORE the Odoo is started.

## Installing Nginx
If you set the parameter ```INSTALL_NGINX``` to ```True``` you should also configure workers. Without workers you will probably get connection loss issues. Look at [the deployment guide from Odoo](https://www.odoo.com/documentation/13.0/setup/deploy.html) on how to configure workers.

## Procedimiento de instalación

##### 1. Bajar el script:
```
sudo wget https://raw.githubusercontent.com/Bantics-Odoo/InstallScript/13.0B/odoo_install_debian.sh
```
##### 2. Modifica los parametros con nano, de lo que creas necesario.
There are a few things you can configure, this is the most used list:<br/>
```OE_USER``` Es el parametro $1 (ejecucion de readme es TU Usuario) sera el  username para el usuario de sistema. Este usuario debe existir en tu equipo  <br/>
```GENERATE_RANDOM_PASSWORD``` if this is set to ```True``` the script will generate a random password, if set to ```False```we'll set the password that is configured in ```OE_SUPERADMIN```. Por defecto el valor es ```False``` y el script usara el valor dado en ```OE_SUPERADMIN```.<br/>
```INSTALL_WKHTMLTOPDF``` set to ```False``` if you do not want to install Wkhtmltopdf, if you want to install it you should set it to ```True```.<br/>
```OE_PORT``` is the port where Odoo should run on, for example 8069.<br/>
```OE_VERSION``` is the Odoo version to install, for example ```13.0``` for Odoo V13.<br/>
```OE_SUPERADMIN``` is the master password for this Odoo installation.<br/>
```INSTALL_NGINX``` is set to ```False``` by default. Set this to ```True``` if you want to install Nginx.<br/>
```WEBSITE_NAME``` Set the website name here for nginx configuration<br/>
```WEBSITE_NAME``` Set the website name here for nginx configuration<br/>
```ENABLE_SSL``` Set this to ```True``` to install [certbot](https://github.com/certbot/certbot) and configure nginx with https using a free Let's Encrypted certificate<br/>
```ADMIN_EMAIL``` Email is needed to register for Let's Encrypt registration. Replace the default placeholder with an email of your organisation.<br/>
```INSTALL_NGINX``` and ```ENABLE_SSL``` must be set to ```True``` and the placeholder in ```ADMIN_EMAIL``` must be replaced with a valid email address for certbot installation<br/>
  _By enabling SSL though Let's Encrypt you agree to the following [policies](https://www.eff.org/code/privacy/policy)_ <br/>

#### 3. Asegurate que el script sea ejecutable
```
sudo chmod +x odoo_install_debian.sh
```
##### 4. Ejecutar el script:
```
sudo ./odoo_install_debian.sh $(whoami)

```

## Donde deberia hostear Odoo?
La verdad hay muchos servicios de hosting buenos para deployar odoo.
Nosoros recomendamos que, salvo que tengas experiencia como devops y tiempo para dedicarle, contactes a alguien para que pueda asegurarte una disponibilidad del sistema, tanto en el deploy en producción, como en el mantenimiento cotidiano del servicio, backups de tus datos, etc.
En Bantics Cooperativa, tenemos años de experiencia trabajando con sistemas de gestión y facturación, y sabemos que es un servicio fundamental en tu empresa.
Contactanos si estas en Argentina, para poder conversar sobre tus necesidades!

## Minimal server requirements
While technically you can run an Odoo instance on 1GB (1024MB) of RAM it is absolutely not advised. A Linux instance typically uses 300MB-500MB and the rest has to be split among Odoo, postgreSQL and others. If you install an Odoo you should make sure to use at least 2GB of RAM. This script might fail with less resources too.
There are known issues on DigitalOcean for example where the installation crashes on 1GB RAM machines. See https://github.com/Yenthe666/InstallScript/issues/243

