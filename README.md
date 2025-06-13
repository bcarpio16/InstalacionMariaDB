# 💻 Instalación de la Base de Datos - MariaDB

## 🔄 Actualización del Sistema Operativo

Antes de iniciar la instalación de cualquier servicio, es recomendable actualizar todos los paquetes del sistema para contar con las últimas versiones disponibles:

``` 
dnf -y update
```

## 📥 Configuración del Repositorio de MariaDB

Para instalar MariaDB desde su repositorio oficial, accedemos a la página:

➡️ https://mariadb.org

1. Hacemos clic en Download.
2. Seleccionamos la opción MariaDB Server Repositories.
3. Elegimos el sistema operativo: Red Hat Enterprise Linux 9.
4. Seleccionamos la versión del motor (por ejemplo, 11.8) y el mirror deseado.
5. Se generará automáticamente la configuración del repositorio.

<p align="center">
  <img src="https://github.com/user-attachments/assets/6b6e2257-9ae8-4c3e-937e-706255b2cf67" width="600" height="300">
</p>

A continuación, en el servidor, accedemos al directorio de repositorios:

```
cd /etc/yum.repos.d/
```

Creamos el archivo del repositorio:

```
vim MariaDB.repo
```

Y pegamos el contenido generado, por ejemplo:

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

## 📦 Instalación de MariaDB

Una vez configurado el repositorio, procedemos a instalar el servidor y el cliente de MariaDB:

```
 dnf install MariaDB-server MariaDB-client
```
## 🔧 Activación del Servicio

Después de instalar MariaDB, habilitamos y arrancamos el servicio:

```
systemctl enable mariadb
systemctl start mariadb
systemctl status mariadb
```

## 🔐 Configuración Segura de MariaDB

Para asegurar la instalación, ejecutamos el script:

```
mariadb-secure-installation
```

A continuación, con el asistente de instalación debemos realizar lo siguiente:

Vamos a tener lo siguiente:

- 🔑 Autenticación actual del usuario root

Se solicita la contraseña actual del usuario root de MariaDB. Si no disponemos de una, presionamos Enter.

```
Enter current password for root (enter for none):
OK, successfully used password, moving on...

Setting the root password or using the unix_socket ensures that nobody
can log into the MariaDB root user without the proper authorisation.

You already have your root account protected, so you can safely answer 'n'.
```

  - 🧩 Cambio al método de autenticación unix_socket

Permite que el usuario root del sistema acceda a MariaDB sin necesidad de contraseña, siempre desde el entorno local:

```
Switch to unix_socket authentication [Y/n] y
Enabled successfully!
Reloading privilege tables..
 ... Success!
```

  - 🔐 Cambio de contraseña del usuario root

Se crea o actualiza la contraseña del usuario root de MariaDB:

```
Change the root password? [Y/n] y
New password:
Re-enter new password:
Password updated successfully!
Reloading privilege tables..
 ... Success!
```

  - 👤 Eliminar usuarios anónimos

Se eliminan los usuarios sin nombre que permiten acceso sin autenticación:

```
By default, a MariaDB installation has an anonymous user, allowing anyone
to log into MariaDB without having to have a user account created for
them.  This is intended only for testing, and to make the installation
go a bit smoother.  You should remove them before moving into a
production environment.

Remove anonymous users? [Y/n] y
 ... Success!

Normally, root should only be allowed to connect from 'localhost'.  This
ensures that someone cannot guess at the root password from the network.
```

  - 🌐 Bloquear acceso remoto para root

Desactiva la posibilidad de que el usuario root se conecte de forma remota:

```
Disallow root login remotely? [Y/n] y
 ... Success!

By default, MariaDB comes with a database named 'test' that anyone can
access.  This is also intended only for testing, and should be removed
before moving into a production environment.
```
  - 🧪 6. Eliminar la base de datos test

Se elimina la base de datos test, accesible por cualquier usuario:

```
Remove test database and access to it? [Y/n] y
 - Dropping test database...
 ... Success!
 - Removing privileges on test database...
 ... Success!

Reloading the privilege tables will ensure that all changes made so far
will take effect immediately.
```

  - 🔁 7. Recargar las tablas de privilegios

Para aplicar los cambios de inmediato:

```
Reload privilege tables now? [Y/n] y
 ... Success!

Cleaning up...
```
  - ✅ 8. Finalización

Si el proceso salió exitosamente mostrara el mensaje 

```
All done!  If you've completed all of the above steps, your MariaDB
installation should now be secure.

Thanks for using MariaDB!
```

## ✅ Verificación del Acceso

Podemos probar el acceso al servidor MariaDB con el siguiente comando:

```
mysql -u root -p
```
Se solicitará la contraseña definida anteriormente.



