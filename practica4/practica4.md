# Práctica 4
## Comprobar el rendimiento de servidores web

Para esta práctica hemos utilizado 1 máquina virtual nueva **user** más las otras máquinas virtuales **Server1 -> (192.168.1.100), server2 -> (192.168.1.101) y balanceador -> (192.168.1.102)**
Mostramos ejemplos de una ejecución, con la media de 10 ejecuciones por cada uso de herramienta/servidor.

Para instalar ab, usaremos el siguiente comando:

```bash
sudo apt-get install apache2-utils
```
Y hemos utilizado el siguiente comando:

```bash
ab -n 1000 -c 10 http://192.168.1.102/index.html
```
En el que mandamos 1000 peticiones de 10 en 10 de forma concurrente a esa dirección.

Hemos modificado la página del servidor añadiendo una imagen en la página web

En la siguiente foto podemos ver el resultado de la ejecución:


![Resultado de la ejecución del Apache Benchmark](https://github.com/pavocejudo/SWAP1516/blob/master/practica4/imagenes/foto1.png)

![Resultado de la ejecución del Apache Benchmark](https://github.com/pavocejudo/SWAP1516/blob/master/practica4/imagenes/foto2.png)



| ab Servidor Solo | Time Taken for Test (s) | Failed requests | Request per second (/s) |
|------------------|:-----------------------:|:---------------:|:-----------------------:|
| Medición 1       |                  0,755  |            332  |                 1324,98 |
| Medición 2       |                  0,752  |            334  |                 1329,56 |
| Medición 3       |                  0,803  |            667  |                 1244,98 |
| Medicion 4       |                  0,747  |            333  |                 1338,95 |
| Medicion 5       |                  1,012  |            334  |                  988,03 |
| Medición 6       |                  0,746  |            333  |                 1339,97 |
| Medición 7       |                  0,762  |            334  |                 1311,55 |
| Medición 8       |                  0,741  |            667  |                 1349,82 |
| Medicion 9       |                  1,020  |            333  |                  980,23 |
| Medicion 10      |                  1,025  |            333  |                  975,19 |
|   **Media**      |      **0,8363**         |  **400**        |    **1218,326**         |
|**Desviacion**    |      **0,127**          |  **140,72**     |      **166,21**         |


Estas mediciones son el resultado tras la ejecución del Apache Benchmark 10 veces con un balanceador Nginx.




| ab Servidor Solo | Time Taken for Test (s) | Failed requests | Request per second (/s) |
|------------------|:-----------------------:|:---------------:|:-----------------------:|
| Medición 1       |                  0,531  |            0    |                 1882,88 |
| Medición 2       |                  0,626  |            0    |                 1598,47 |
| Medición 3       |                  0,629  |            0    |                 1589,27 |
| Medicion 4       |                  0,530  |            0    |                 1888,06 |
| Medicion 5       |                  0,614  |            0    |                 1628,03 |
| Medición 6       |                  0,569  |            0    |                 1756,42 |
| Medición 7       |                  0,620  |            0    |                 1613,00 |
| Medición 8       |                  0,630  |            0    |                 1588,53 |
| Medicion 9       |                  0,523  |            0    |                 1910,54 |
| Medicion 10      |                  0,640  |            0    |                1563,47  |
|   **Media**      |      **0,5912**         |    **0**        |    **1701,867**         |
|**Desviacion**    |      **1,4025**         |    **0**        |      **142,467**        |

Estas mediciones son el resultado tras la ejecución del Apache Benchmark 10 veces sin un balanceador, directamente al **server1**.


## Comparativa de resultados en Apache Benchmark


|          -          |      1 sola máquina     |   Granja Nginx  |
|---------------------|:-----------------------:|:---------------:|
| Time Taken for test |        0,8363           |      0,5912     |               
| Failed Requests     |         400             |         0       |              
| Requests per second |        1218,326         |     1701,867    |

Podemos comprobar, al ejecutarlos en máquinas virtuales distintas, como las mediciones sin balanceador son mejores que la de las que tienen el balanceador              



![Gráficas Comparativa](https://github.com/pavocejudo/SWAP1516/blob/master/practica4/imagenes/Time%20Taken.png)
![Gráfica Comparativa](https://github.com/pavocejudo/SWAP1516/blob/master/practica4/imagenes/Request%20per%20second.png)
![Gráfica Comparativa](https://github.com/pavocejudo/SWAP1516/blob/master/practica4/imagenes/Failed%20Requests.png)


## Medir los rendimientos con Siege

Siege es muy parecido a Apache Benchmark, el procedimiento es el mismo, lo único que varía es la sintaxis a utilizar en los parámetros
