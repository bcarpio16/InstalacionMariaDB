# 💻 Instalación de la Base de Datos - MariaDB

- Actualización del Sistema Operativo

Antes de realizar cualquier instalación se debe actualizar todos los paquetes instalados en el servidor, para lo cual vamos a utilizar el comando 
``` 
dnf -y update
```

- Descargar el Repositorio de la Base de Datos

Para instalar el motor de base de datos MariaDB, vamos a ir a la siguiente url: https://mariadb.org/.

En sitio web, nos dirigimos a la opción **Download**, en este caso vamos a ir a la opción **MariaDB Server Repositories**, seleccionamos la distribucion del servidor o equipo donde vamos a instalar, en nuestro caso el Sistema Operativo va a ser **Red Hat Enterprise Linux 9**, seleccionamos la versión del motor de base de datos y el **Mirror** donde vamos a descargar.
Una vez realizado esto, nos va a desplegar la informacion del repositorio, como se puede ver en la imagen.

<p align="center">
  <img src="https://github.com/user-attachments/assets/6b6e2257-9ae8-4c3e-937e-706255b2cf67" width="600" height="300">
</p>


Copiamos el repositorio y nos vamos a dirigir a la siguiente ruta en el servidor.
```
cd /etc/yum.repos.d/
```
Creamos el repositorio **MariaDB.repo** y vamos a pegar el repositorio
```
vim MariaDB.repo
```
Nos va a quedar algo así 

```
# MariaDB 11.8 RedHatEnterpriseLinux repository list - created 2025-06-13 16:03 UTC
# https://mariadb.org/download/
[mariadb]
name = MariaDB
# rpm.mariadb.org is a dynamic mirror if your preferred mirror goes offline. See https://mariadb.org/mirrorbits/ for details.
# baseurl = https://rpm.mariadb.org/11.8/rhel/$releasever/$basearch
baseurl = https://mirror.insacom.cl/mariadb/yum/11.8/rhel/$releasever/$basearch
# gpgkey = https://rpm.mariadb.org/RPM-GPG-KEY-MariaDB
gpgkey = https://mirror.insacom.cl/mariadb/yum/RPM-GPG-KEY-MariaDB
gpgcheck = 1

```
Procedemos a instalar el servicio MariaDB y los paquetes del cliente.
 dnf install MariaDB-server MariaDB-client

 Una vez instalado vamos a habilitar e iniciar el servicio 

systemctl enable mariadb
systemctl start mariadb
systemctl status mariadb

se procede a inciar el servicio 

mariadb-secure-installation

Enter current password for root (enter for none):
OK, successfully used password, moving on...

Setting the root password or using the unix_socket ensures that nobody
can log into the MariaDB root user without the proper authorisation.

You already have your root account protected, so you can safely answer 'n'.

Switch to unix_socket authentication [Y/n] y
Enabled successfully!
Reloading privilege tables..
 ... Success!


You already have your root account protected, so you can safely answer 'n'.

Change the root password? [Y/n] y
New password:
Re-enter new password:
Password updated successfully!
Reloading privilege tables..
 ... Success!


By default, a MariaDB installation has an anonymous user, allowing anyone
to log into MariaDB without having to have a user account created for
them.  This is intended only for testing, and to make the installation
go a bit smoother.  You should remove them before moving into a
production environment.

Remove anonymous users? [Y/n] y
 ... Success!

Normally, root should only be allowed to connect from 'localhost'.  This
ensures that someone cannot guess at the root password from the network.

Disallow root login remotely? [Y/n] y
 ... Success!

By default, MariaDB comes with a database named 'test' that anyone can
access.  This is also intended only for testing, and should be removed
before moving into a production environment.

Remove test database and access to it? [Y/n] y
 - Dropping test database...
 ... Success!
 - Removing privileges on test database...
 ... Success!

Reloading the privilege tables will ensure that all changes made so far
will take effect immediately.

Reload privilege tables now? [Y/n] y
 ... Success!

Cleaning up...

All done!  If you've completed all of the above steps, your MariaDB
installation should now be secure.

Thanks for using MariaDB!


Verificamos el servicio 

mysql -u root -p



