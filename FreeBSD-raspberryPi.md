

# Instalamos FreeBSD en raspberry Pi  :smiling_imp: :strawberry: 

![image-removebg-preview(6)](https://github.com/luisjuarez099/FreeBSD-raspberriPi/assets/83623972/4c2472e1-2dc5-45a1-a855-5028a58f3621)


## Ingresa a este link 

Busca la version de tu raspberry pi, en mi caso es la version **Pi 3 model B V.2**
> https://wiki.freebsd.org/arm/Raspberry%20Pi


![version-rasp](https://github.com/luisjuarez099/FreeBSD-raspberriPi/assets/83623972/fce280d0-6d2f-45fb-8b37-5a5f156c0bdc)

En mi caso despues de haber descargado la Imagen 

![descarga-archvio](https://github.com/luisjuarez099/FreeBSD-raspberriPi/assets/83623972/6aa21def-1f5e-4232-a10d-69c36fae26ea)

### Vamos a hacer el formateo de una SD para montar el sistema operativo FreBSD

1. Eligimos la version de nuestra raspberry pi

![imagen-rasp](https://github.com/luisjuarez099/FreeBSD-raspberriPi/assets/83623972/b7cfc121-733c-4fe9-afc1-9c5f4c10e220)

2. Eligimos **use custom** para seleccionar un OS (sistema operativo) que en nuestro caso es la version previamente descargada.

![use-custom](https://github.com/luisjuarez099/FreeBSD-raspberriPi/assets/83623972/a5c5f54c-3910-4a13-886b-5c221ea20647)


3.- Seleccionamos nuestra tarjeta de SD

![tarjeta-sd](https://github.com/luisjuarez099/FreeBSD-raspberriPi/assets/83623972/af79ba9c-0915-49da-b543-8fa6203b7e69)


<hr>

### Conexiones :accessibility: 

Material: Cable de red, HDMI, un alimentador para la raspberry pi y Teclado.

![WhatsApp Image 2024-06-24 at 10 40 26 AM](https://github.com/luisjuarez099/FreeBSD-raspberriPi/assets/83623972/bcc0f111-ae96-4f79-ba27-5339ab07e549)


Despues de haber logrado la conexion y previamnete haber insertado la SD a nuestra raspberry Pi se procedera a ejecutarse en automatico.

## Configuraciones 

Despues de haberse cargado lo requerido (esto se cargo de manera automatica) y ahora.


> [!IMPORTANT]
> llegara al final pidiendo ***Login:*** y **Password:** que por defecto son
> **root** en ambos.

![WhatsApp Image 2024-06-24 at 10 40 38 AM](https://github.com/luisjuarez099/FreeBSD-raspberriPi/assets/83623972/8f43b2cf-2536-405e-847e-3d30e2ad46e8)

aparecera como
```text
root@generic:~#
```
> [!NOTE]
> Eso significa que estamos como usarios **root**.


Lo primero que debemos de hacer es **actualizar los paquetes** y va a instalar la nueva version de  pkg, para eso vamos a ejecutar el siguinte comando:
```bash
pkg update && upgrade
```

![WhatsApp Image 2024-06-24 at 10 51 32 AM](https://github.com/luisjuarez099/FreeBSD-raspberriPi/assets/83623972/3d65abc7-5b05-4334-9c58-87265dc98509)


Al finalizar hemos de poder descargar paquetes, como prueba ejecuta los siguientes comandos:

```bash
pkg install cowsay
```
Al final la instalacion ejecuta 📄

```bash
cowsay "Hola desde freebsd"
```
Resultado: 

![cowsay](https://github.com/luisjuarez099/FreeBSD-raspberriPi/assets/83623972/1f1bf579-9e54-46a6-aad3-30f28ff1bac7)

## Configuracion de usuario usando sudo. 👩‍💻

> [!NOTE]
> **sudo** es una herramienta muy valiosa para la administración segura y eficiente de sistemas. Proporciona una capa adicional de seguridad y control que puede ser muy beneficiosa, especialmente en entornos multiusuario o cuando varias personas necesitan realizar tareas administrativas.

Vamos a ejecutar este comando:

```bash
adduser
```
Estas son las configuraciones que se llevan acabo para poder crear usuarios y darles permiso de [wheel](http://www.freebsdwiki.net/index.php/Wheel)
Yo user el nombre de ```fer``` pero como ejemplo uso el nombre de ```miprueba``` que tu puede elegir el de tu agrado :smile: 

![adduser2](https://github.com/luisjuarez099/FreeBSD-raspberriPi/assets/83623972/db6f638b-f8ec-4219-a08f-60a13e000d6b)



agregado el usuario vamos a darle los persmiso de super-user, para eso nos cambiamos a modo root 

```bash
su -
```

Ya una vez dentro vamos a instala ```sudo```

```bash
pkg install sudo
```
#### Configuramos sudo para el usuario

Vamos a editar el archivo ```sudoers``` por medio de ```visudo``` para configurar los permisos necesarios

```bash
visudo
```
Indica los root privilegios, siendo diferentes dependiendo como van procediendo las lineas 🌻

![root-priv](https://github.com/luisjuarez099/FreeBSD-raspberriPi/assets/83623972/bc8ddff9-14b6-49e5-9527-f8de7f07d84c)

Vamoa a agregar a nuestro usuario con los permisos necesarios para poder ejecutarlo por medio de ```sudo```

```bash
miprueba ALL=(ALL:ALL) ALL
```
> [!NOTE]
> Alternativamente, si deseas otorgar permisos de sudo a todos los usuarios en el grupo wheel, añade o descomenta la siguiente línea
>  ```# %wheel ALL=(ALL:ALL) ALL``` presionando la letra ```x```

### Probar sudo cambiando de cuenta

```bash
su - miprueba
```

![su-user](https://github.com/luisjuarez099/FreeBSD-raspberriPi/assets/83623972/3af52e3d-2558-4dfc-8320-6454c7f19192)

Excelente! Siguiendo estos pasos, deberías poder instalar y configurar sudo en tu Raspberry Pi con FreeBSD para un Usuario.

<hr>

## Install NGINX 

Nginx [engine x] es un servidor HTTP, proxy inverso y servidor proxy de correo escrito por Igor Sysoev. Es un servidor web ligero, licenciado bajo una licencia similar a BSD. Es el servidor web de más rápido crecimiento y uno de los más populares. 

Instalamos por medio del paquete pkg

```bash
pkg install nginx
```

El comando sysrc nginx_enable="YES" se utiliza en sistemas FreeBSD para configurar el sistema de inicio para que habilite y arranque el servicio Nginx automáticamente cada vez que el sistema se inicie.

```bash
sysrc nginx_enable="YES"
```

Iniciamos el sistema 

```bash
service nginx start
```

![nginx-ok](https://github.com/luisjuarez099/FreeBSD-raspberriPi/assets/83623972/b4d295ed-8ef9-4c93-96b5-3142dce7e761)

Terminado 

## Instalar mariadbxxx-server en FreeBSD 🙊

### Buscar maraidb para la instalacion: 
Buscaremos por medio del los paquetes (pkg)  para instalar mariadbxxx-server

```bash
  pkg search mariadb
```
![marisb-search](https://github.com/luisjuarez099/FreeBSD-raspberriPi/assets/83623972/7d13afea-4c8c-4395-b291-47d8df88d673)

### Instalacion  :point_down: 
Una vez visto los paquetes disponibles lo que vamos a hacer es seleccionar ```mariadb105-server``` esta es la version que queremos instalar 
para llevar acabo la instalacion por medio del administrador de paquetes ```pkg``` para esto vamos a ejecutar el comando:

```bash
  pkg install mariadb105-server
```
Aguardamos un momento a que se instale...Al finalizar muestra un mensaje como este: 

![mariadb-install](https://github.com/luisjuarez099/FreeBSD-raspberriPi/assets/83623972/94e637b5-c70c-49d4-98a1-37d418159680)


### Permisos a mysql :dolphin: 

>[!IMPORTANT]
>Existen casos que al instalar no se crea la carpeta, en ese caso vamoa a agregar al arhcivo ```/ect/rc.conf``` la siguiente linea ```mysql_enable="YES"```.
>Te saltas al paso para iniciar el sistema. :) 

El comando ```chown mysql /var/run/mysql``` se utiliza para cambiar el propietario del directorio /var/run/mysql al usuario mysql.

Cuando ejecutas chown mysql /var/run/mysql, estás asignando el control del directorio /var/run/mysql al usuario mysql. Esto es útil en entornos donde es importante que el servidor MySQL tenga acceso y control sobre sus propios archivos temporales, como los sockets utilizados para la comunicación interna.

Este es el comando que vamos a ejecutar
```bash
  chown mysql /var/run/mysql
```

### Mysql a boot del sistema. :dolphin: 

Al ejecutar ```sudo sysrc mysql_enable=YES```, el sistema modificará automáticamente el archivo ```/etc/rc.conf``` para asegurarse de que MySQL se inicie automáticamente cada vez que el sistema se inicie o se reinicie. Esto simplifica la administración del servicio, ya que no es necesario iniciar MySQL manualmente después de cada reinicio del sistema.

Comando:

```bash
sudo sysrc mysql_enable=yes
```

### Iniciamos el sistema :computer: 

Ya para arrancar el sistema, lo que vamos a hace es correr el siguinte comando 

```bash
service mysql-server start
```
y damos un ```status``` para conocer el PID donde se esta ejecutando

```bash
service mysql-server status
```
![mariadb-pid](https://github.com/luisjuarez099/FreeBSD-raspberriPi/assets/83623972/a19e3756-896f-4830-acec-729497b44d4c)


### Comprobamos que exista el acceso a local host  :computer:

```bash
sockstat -4 -6 | grep 3306
```
![maria-localhost](https://github.com/luisjuarez099/FreeBSD-raspberriPi/assets/83623972/cf31e521-1853-40c1-94c5-f6d85d0ccf9d)


### Ingresamos a mysql (mariadb) :dolphin: 

```bash
sudo mysql
```

![mysql_sudo](https://github.com/luisjuarez099/FreeBSD-raspberriPi/assets/83623972/4a878036-e6a7-4ff8-919b-095f81ac71fe)


## Uso de SCP para la transferencia de archvios o carpetas.

SCP (copia segura) es una utilidad de línea de comandos que permite copiar archivos y directorios de manera segura entre dos ubicaciones.


#### Archivo Local al servidor
Llevaremos la practica de un archivo local al usuario remoto y viceversa.

Este es el orden que debemos de usar para enviar los archivos 

```bash
scp archivo_local.txt usuario_remoto@direccion_servidor_remoto:directorio_destino
```
![screens](https://github.com/luisjuarez099/FreeBSD-raspberriPi/assets/83623972/9cfe17ae-f9c2-470d-b6d8-72c4878af871)

Identificamos el archivo que deseamos enviar a nuestro equipo remoto, en este caso nuestro archvio en un .txt pero puede ser cualquier extension.


![scplar](https://github.com/luisjuarez099/FreeBSD-raspberriPi/assets/83623972/a7ab59e3-a036-4168-8397-5b863eb411c6)


Es asi que enviamos nuestro archvio de local a un equipo remoto, ahora, lo podemos hacer de maner viceversa


# Asigancio de grupos y permisos en archivos como en MYSQL.

**¿Qué son los permisos en Linux?**

El **Propietario(owner)** es aquel que gestiona, crea archivos o carpetas y los modifica a su gusto, siempre en su directorio de trabajo HOME. **Grupos** hace alusión a un conjunto definido de usuarios mientras que **Otros** incluye cualquier usuario que no esté en grupo ni tampoco sea el propietario como tal.

Los permisos en Linux rigen a estos tres grupos, dándoles o privándoles de diferentes acciones sobre un archivo o una carpeta determinada. En concreto, existen tres tipos de permisos en Linux con los cuales son **lectura (r)**, **escritura (w)** y **ejecucion (x)**, de los cuales tiene un formato *octal* .

![permisos](https://github.com/luisjuarez099/FreeBSD-raspberriPi/assets/83623972/35a1a9d5-8637-4b4c-86ec-b32114ee4ff7)

para mas informacion conuslta [freebsd-permisos](https://docs.freebsd.org/en/books/handbook/basics/#permissions)

## AGREGAR GRUPOS 


Creamos un nuevo grupo, en nuestro caso lo llamamos `backend_bandits` , para esto creamos un nuevo grupo con el comando:

```bash
sudo pw groupadd backend_bandits
```

La manera en como se organiza la info. de los grupos es de esta manera

```
group_name:*:GID:user_list
```

- group_name: El nombre del grupo.
- *: El campo de la contraseña del grupo, que generalmente se deja como * ya que los grupos no suelen usar contraseñas.
- GID: El Group ID, un identificador único para el grupo.
- user_list: Una lista de usuarios que pertenecen a este grupo, separados por comas.

  
Comprobamos que se haya creado con el comando 

```bash
sudo cat /etc/group
```

![group-add](https://github.com/luisjuarez099/FreeBSD-raspberriPi/assets/83623972/16a469a9-afc2-4f9d-959a-6714bbaf27ab)



## Agregar usuarios al grupo

>[!IMPORTANT]
>Debes de crear a tus usuarios que van a paertenece a ese grupo.
>Pasos pasados veiamos como crear usuarios, en este caso NO LE ASIGNES PERMISOS DE SUDO, puesto que no es buena practica agegarles permisos de administrados
>a cada usuario creado.

Suponiendo que ya tienes a tus usarios creados es momento de agregarlos al grupo creado llamado ```backend_bandits```

Usamos el siguiente comando: 

```bash
 sudo pw groupmod backend_bandits -m yaser,antonio,richard
```

-  sudo: Ejecuta el comando como superusuario.
- pw: Usa la herramienta de administración de usuarios y grupos.
- groupmod: Modifica un grupo existente.
- backend_bandits: El nombre del grupo que estás modificando.
- -m: Indica que estás añadiendo miembros al grupo.
- yaser,antonio,richard: Los nombres de usuario que se añaden al grupo.

Volvemos a comprobar que se agegaron de manera correcta los usuarios al grupo y veamos a los usarios que pertenecen al grupo
:

```bash
sudo pw groupshow backend_bandits
```


![members-group](https://github.com/luisjuarez099/FreeBSD-raspberriPi/assets/83623972/acb79b15-f450-4764-a8cc-5572d41afa3e)


## Asignar usuarios y permisos al archido de MYSQL/db_unedl

Todos los archivos y directorios dentro de /var/db/mysql/db_unedl/ tendrán root como propietario y backend_bandits como grupo

```bash
sudo chown -R root:backend_bandits /var/db/mysql/db_unedl/
```

- sudo: Ejecuta el comando con privilegios de superusuario.
- chown: Comando para cambiar el propietario y el grupo de archivos o directorios.
- -R: Realiza el cambio de manera recursiva, aplicándose a todos los archivos y subdirectorios dentro del directorio especificado.
- root:backend_bandits: Cambia el propietario a root y el grupo a backend_bandits.

    - root: El nuevo propietario.
    - backend_bandits: El nuevo grupo.

- /var/db/mysql/db_unedl/: El directorio objetivo en el cual se aplicará el cambio de propiedad y grupo.

### Permisos 

Esto asegura que solo el propietario y los miembros del grupo ```backend_bandits``` puedan leer, escribir y ejecutar en el directorio de la base de datos.

```bash
sudo chmod 770 /var/db/mydatabase
```
> ![NOTE]
> Yo como PROPIERTARIO **root** puedo crear usuarios y asignarle permisos en la BD de datos.


Por ahora richard  **no tiene acceso a la bd ```db_unedl```

![no-db-user](https://github.com/luisjuarez099/FreeBSD-raspberriPi/assets/83623972/fcade113-82d1-4aa7-b7b6-b7ae28f41e59)


### Dando permisos en la bd

1. Creamos usuario (en caso no exista):

```sql
CREATE USER 'nuevo_usuario'@'localhost' IDENTIFIED BY 'tu_contraseña';
```

![create-user-sql](https://github.com/luisjuarez099/FreeBSD-raspberriPi/assets/83623972/4045c1c8-446d-4626-bd5e-b9162e727466)

2. Otrogamos permisos al usuario,en mi caso solo quiero que haga SELECT, INSERT y UPDATE.

   ```sql
   GRANT SELECT, INSERT, UPDATE ON nombre_base_de_datos.* TO 'nuevo_usuario'@'localhost';
   ```

   ![privilegies](https://github.com/luisjuarez099/FreeBSD-raspberriPi/assets/83623972/ffdb1dea-aa60-430e-bcd2-ee0fbd754f05)


Verificamos que el usuario ya tengo acceso a la bd llamada ```db_unedl```

para conectarnos usamos el comando

```bash
mysql -u richard -p
```
 y agregaos la contrasena que le asignamos al usuario.

 3. Verificamos que la tenga la base de datos que nosotros le asignamos.

    ![user-db](https://github.com/luisjuarez099/FreeBSD-raspberriPi/assets/83623972/ae92128d-4f2f-4eb0-a047-93e8916d6d3e)


4. Comprobamos que los permisos de otorgaron correctamente, puesto que richard no puede eliminar.

![delete](https://github.com/luisjuarez099/FreeBSD-raspberriPi/assets/83623972/9bbe5fe3-38ee-4651-844b-50f2ee1c1c81)

