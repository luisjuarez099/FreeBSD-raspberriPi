

# Instalamos FreeBSD en raspberry Pi 

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

### Conexiones 

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
Al final la instalacion ejecuta 

```bash
cowsay "Hola desde freebsd"
```
Resultado: 

![cowsay](https://github.com/luisjuarez099/FreeBSD-raspberriPi/assets/83623972/1f1bf579-9e54-46a6-aad3-30f28ff1bac7)

## Configuracion de usuario usando sudo.

> [!NOTE]
> **sudo** es una herramienta muy valiosa para la administración segura y eficiente de sistemas. Proporciona una capa adicional de seguridad y control que puede ser muy beneficiosa, especialmente en entornos multiusuario o cuando varias personas necesitan realizar tareas administrativas.

Vamos a ejecutar este comando:

```bash
adduser
```
Estas son las configuraciones que se llevan acabo para poder crear usuarios y darles permiso de [wheel](http://www.freebsdwiki.net/index.php/Wheel)

![adduser](https://github.com/luisjuarez099/FreeBSD-raspberriPi/assets/83623972/4cd4cb4f-43dc-47ce-b06d-709fdc141e8c)


