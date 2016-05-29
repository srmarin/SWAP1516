## Práctica 3. Balanceo de carga

Una vez terminada la instalación de una tercera máquina virtual. Pasamos a la instalación del software encargado de *balancear la carga* a los distintos servidores, nginx.

```
cd /tmp/

wget http://nginx.org/keys/nginx_signing.key

rm -f /tmp/nginx_signing-key

```
Previamente a la instalación debemos añadir el repositorio al fichero /etc/apt/sources.list, que haremos con:

```
sudo nano /etc/apt/sources.list
```
![Añadiendo repositorios al final del archivo](https://github.com/pavocejudo/SWAP1516/blob/master/practica3/3.png)

```
sudo apt-get install nginx
```
![instalación de nginx](https://github.com/pavocejudo/SWAP1516/blob/master/practica3/6.png)

Para el perfecto uso de esta herramientas, debemos modificar el archivo */etc/nginx/nginx.conf*

```
sudo nano /etc/nginx/nginx.conf
```
Dejándolo tal que así:

![Modificar archivo](https://github.com/pavocejudo/SWAP1516/blob/master/practica3//nueva.jpg)

Para comprobar su funcionamiento, accedemos a la IP y vemos cómo carga alternativamente ambas máquinas.

![](https://github.com/pavocejudo/SWAP1516/blob/master/practica3/balaceador.png)

Añadiendo el parámetro *weight* cambiamos el "peso" que tiene cada servidor:
(dentro del archivo )

```
upstream apaches {

  server 192.168.1.100 weight=1;
  server 192.168.1.101 weight=2;
}
```
![balanceador con peso](https://github.com/pavocejudo/SWAP1516/blob/master/practica3/9.jpg)


# Configurar e instalar haproxy como balanceador de carga

Procedemos a instalar la herramienta necesaria:

```
sudo apt-get install haproxy
```

Pasamos a editar el archivo:

```
sudo nano /etc/haproxy/haproxy.cfg
```
Quedando tal que así:

![Archivo modificado](https://github.com/pavocejudo/SWAP1516/blob/master/practica3/7.jpg)

Finalmente hacemos funcionar el programa

```
/usr/sbin/haproxy -f /etc/haproxy/haproxy.cfg
```
![Programa funcionando](https://github.com/pavocejudo/SWAP1516/blob/master/practica3/8.jpg)
