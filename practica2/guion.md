# PRÁCTICA 2: Clonar información de su sitio web

**Instalación y uso de la herramienta rsync**

Nuestra máquina por defecto tiene instalada ésta herramienta, pero en el caso de no tenerla, ejecutaríamos en la terminal:

```
sudo apt-get install rsync
```


## Clonar archivos con rsync

Para probar el funcionamiento de la herramienta rsync introducimos el comando:

```
rsync -avz -e ssh root@192.168.1.100:/var/www /var/www

```


![funcionamiento rsync](https://github.com/pavocejudo/SWAP1516/blob/master/practica2/rsync1.png)

Como vemos en la imagen, en el server1 nos pide una contraseña que es la del usuario root del server2
Los parámetros -avz comprimen los datos y los manda en modo archivo.

-e especifica el comando SHELL a usar, en este caso *ssh root@192.168.1.100:/var/www /var/www*

El acceso con root es importante para asegurarse de que no existe ningún problema con los permisos, aunque no los modificará. Para que ssh nos permita el acceso root modificaremos el parámetro PermitRootLogin en /etc/ssh/sshd_config

## Conexión entre servidores mediante ssh

ssh es un programa que nos permite controlar máquinas remotas y ejecutar comandos en ellas.

Para instalarlo:

```
sudo apt-get install ssh
```
Para poder acceder a una máquina remota basta con ejecutar la sentencia:

```
ssh <usuario>@<direccionIP>
```
Cada vez que queramos acceder a la máquina remota deberemos poner la contraseña del usuario.
Para evitar esto, generamos una clave con el comando:
```
ssh-keygen -t dsa
```
La opción -t es para el tipo de clave, en este caso dsa.

Esto nos mostrará lo siguiente:

![Funcionamiento ssh-keygen](https://github.com/pavocejudo/SWAP1516/blob/master/practica2/ssh-keygen.jpg)


Al acceder, comprobamos que no nos pide la contraseña


## Establecer un cron para actualizar el contenido de */var/www* entre las dos máquinas

Debemos de añadir la siguiente línea en el archivo:

```
0 * * * * rsync -avz --delete -e ssh root@192.168.1.100:/var/www/ /var/www/
```
















Una de las formas para clonar archivos por SSH es redirigiendo el contenido del archivo a ssh para que lo envíe al destino
