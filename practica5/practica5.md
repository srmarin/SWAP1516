# Práctica 5
## Replicación de bases de datos MySQL

Esta práctica se ha realizado con 2 máquinas virtuales **server1 -> 192.168.1.100** y **server2 -> 192.168.1.101**

# Completar base de datos

Antes de nada debemos de tener algunos datos que copiar, a la hora de crear una nueva base de datos MySQL. Introducimos los siguientes datos:

![Datos introducidos en la BD]()

# Backup manual

Una vez tenemos datos para poder copiar, volcamos la base de datos con el comando:
```bash
mysqldump
```
Y cargarlo en la máquina esclava. Primero bloqueamos las tablas de la máquina maestra y volcamos el contenido en un archivo, para volver a desbloquear las tablas. En última instancia copiamos el dump al esclvo y se lo pasamos a mysql

```
mysql>FLUSH TABLES WITH READ LOCK;
```
```bash
mysqldump prueba -u root -p "pass"
```
```bash
ssh 192.168.1.101 mysql -u root -p "pass"
```
```bash
mysql>UNLOCK TABLES;
```
```bash
mysql -u root -p "pass"
```

## Backup Automático

Para realizar esto debemos editar el archivo /etc/mysql/my.cnf y modificando los siguientes campos:

```bash
#bind-address 127.0.0.1
log_error = /var/log/mysql/error.log
server-id = 1
log_bin = var/log/mysql/mysql-bin.log
```
Seguidamente reiniciamos el servicio

```bash
/etc/init.d/mysql restart
```
