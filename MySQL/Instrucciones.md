
# Instrucciones para la creación de la basa de datos para este ejercicio 


En este archivo se muestran los pasos a seguir para el uso de mysql en el el flow denominado clima por API-Base de datos 


Se muestra a demas como emplear el visual studio code como plataforma de edición y creación de un archivo para lo cual es necesario 
1. Abrir github en el navegador 
2. Crear un nuevo Repositorio 
3. Con ayuda de github desktop se colona dicho repositorio posterior 
4. Se abre visual studio code donde se abre la carpeta github 
5. En esta carpeta se crea dentro del repositorio clima-mysql una nueva carpeta denominada MySQL 
6. Una vez creada se abre el archivo para iniciar su edición 
Nota. Es importante colocar la extensión del archivo de trabajo  que puede ser para el caso del previsualizador .md o en su defecto .txt 


# PROCEDIMIENTO PARA INSTALACION DE MySQL

1. instalar mysql server con el comando `sudo apt install mysql-server`
2. Entrar a MySQL 
   - con el comando 
            `sudo mysql`


# Notas 

 Una vez abierto MySQL en terminal se probara el primer comando el cual permite consultar las bases de datos creadas 

  - mysql> show databases; "Es importante terminar cada linea con ; para evitar errores de sintaxis 

   
    +--------------------+
| Database           |
+--------------------+
| codigoIoT          |
| information_schema |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
5 rows in set (0.27 sec)

3. A continuación es necesario crear una nueva base de datos con el siguiente codigo 

- mysql> create database codigoIoT_1; 
Query OK, 1 row affected (0.06 sec)

- se puede comprobar con el comando show databases mostrando lo siguiente 

    mysql> show databases; 
+--------------------+
| Database           |
+--------------------+
| codigoIoT          |
| codigoIoT_1        |
| information_schema |
| mysql              |
| performance_schema |
| sys                |
+--------------------+

En este caso se muestran dos ya que el ejercicio fue realizado una primera vez 

5. Seleccionar una base de datos de la creada anteriormente empleando los siguientes comandos `use codigoIoT_1`


  - mysql> show databases; 
Este debe mostrar un mensaje como el siguiente: Database changed

6. Crear tabla en base de datos 

Usar la instrucción: 

- id, fecha, nombre, temperatura, humedad 

- `creat table clima(id INT (6)UNSIGNED AUTO_INCREMENT PRIMARY KEY, fecha TIMESTAMP DEFAULT CURRENT_TIMESTAMP, nombre CHAR (248)NOT NULL, temperatura FLOAT (4.2), humedad INT (3));`


# Notas 
Para mostrar las tablas contenidas se puede emplear la instrucción `show tables` 

- en la primera compilación mostrará que no existe: 

    "mysql> show tables;
Empty set (0.01 sec)"

Para mostrar el contenido de dicha tabla se usa el comando `describe clima`
donde muestra la estructura de la misma 

Es necesario previo a trajar con clima por API- base de datos respaldar los nodos descargandolo en formato JSON el archivo creado se debe almacenar el github creando una nueva carpeta en la misma 

7. Agregar nodos MySQL
  - Para realizarlo hay que dirigirse al simbolo de hamburgesa y selecccionar manage pallet de ahi buscar en la pestaña install la paqueteria de nodos node-red-node-mysql eligiendo la más actual y de versión más reciente 
  - Una vez agregada la paqueteria se busca el nodo mysql y se agrega al flow clima por API anexando un node de nota con el nombre base de datos para una nueva sección 

  8. Para modificar los parámetros se da doble click sobre el nodo y se debe anexar un usuario y un password 


  Para ello se emplea el siguiente código 


  - `CREATE USER 'newuser'@'localhost' IDENTIFIED BY 'password';`

  - `CREATE USER 'Sesenes'@'localhost' IDENTIFIED BY 'dilomi2508';`

9. Agregar un nodo de función en el cual es necesario colocar la siguiente instrucción en message 

`msg.topic = "INSERT INTO clima (`nombre`,`temperatura`,`humedad`) VALUES ('Sesenes',"+ global.get("tempAPI") +"," +global.get("humAPI") +");";
return msg;`



#Nota 




Observese que el contedio a almacenar en msd.topic debe ser de tipo string por ello se coloca entre paréntesis, es neceario ademas contar con las variables globales creadas en previos ejercicios que son tempAPI y humAPI 

10. Una vez configurado el nodo de función y mysql se requere agregar un nodo inject y dar en deployd. Sin embargo al hacerlo marcará un error debido a que es necesario dar privilegios al usuario creado 

Se debe emplear el siguiente codigo: 

`GRANT ALL PRIVILEGES ON * . * TO 'newuser'@'localhost';`

modificado debe de quedar como se muestra a continuación: 

`GRANT ALL PRIVILEGES ON * . * TO 'Sesenes'@'localhost';`


se pueden observar las modificaciones a la tabla clima con el código: 


 `SELECT *FROM clima;` 


donde se observa la siguiente tabla 


mysql> SELECT *FROM clima; 
+----+---------------------+---------+-------------+---------+
| id | fecha               | nombre  | temperatura | humedad |
+----+---------------------+---------+-------------+---------+
|  1 | 2022-09-11 14:32:40 | Sesenes |       33.72 |      50 |
|  2 | 2022-09-11 14:46:49 | Sesenes |       33.72 |      49 |
|  3 | 2022-09-11 14:46:52 | Sesenes |       33.72 |      49 |
|  4 | 2022-09-11 14:47:57 | Sesenes |       33.72 |      49 |
|  5 | 2022-09-11 14:47:59 | Sesenes |       33.72 |      49 |
|  6 | 2022-09-11 14:48:00 | Sesenes |       33.72 |      49 |
|  7 | 2022-09-11 14:48:23 | Sesenes |       33.72 |      49 |
|  8 | 2022-09-11 14:48:27 | Sesenes |       33.72 |      49 |
|  9 | 2022-09-11 14:48:27 | Sesenes |       33.72 |      49 |
| 10 | 2022-09-11 14:48:28 | Sesenes |       33.72 |      49 |
| 11 | 2022-09-11 14:48:28 | Sesenes |       33.72 |      49 |
| 12 | 2022-09-11 14:49:29 | Sesenes |       33.72 |      49 |
| 13 | 2022-09-11 14:49:31 | Sesenes |       33.72 |      49 |
| 14 | 2022-09-11 14:49:31 | Sesenes |       33.72 |      49 |
| 15 | 2022-09-11 14:51:26 | Sesenes |       31.43 |      49 |
| 16 | 2022-09-11 14:51:27 | Sesenes |       31.43 |      49 |
| 17 | 2022-09-11 14:51:51 | Sesenes |       31.43 |      49 |
| 18 | 2022-09-11 14:51:52 | Sesenes |       31.43 |      49 |
| 19 | 2022-09-11 14:51:53 | Sesenes |       31.43 |      49 |
| 20 | 2022-09-11 15:00:02 | Sesenes |       31.43 |      49 |
| 21 | 2022-09-11 15:00:05 | Sesenes |       31.43 |      49 |
+----+---------------------+---------+-------------+---------+









    


