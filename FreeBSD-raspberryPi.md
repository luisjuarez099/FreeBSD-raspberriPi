

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

