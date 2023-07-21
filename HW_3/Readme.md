# Введение в Docker #

*Порядок выполнения практического задания N1:*

Изучаем инструкцию по адресу [mysql](https://hub.docker.com/_/mysql)

Сделаем запуск экземпляра MySQL  
Где some-mysql - имя, которое присваивается контейнеру,
mypw - пароль, который устанавливается для пользователя MySQL root,
и tag - тег, указывающий нужную версию MySQL.

>docker run --name some-mysql -e MYSQL_ROOT_PASSWORD=mypw -d mysql:8.0.33  

Заходим в интерактивный режим bash нашего контейнера:

>docker exec -it some-mysql bash

Подключаемся к MySql:

>mysql -u root -pmypw

Создаем БД:

>create database gbdb;

Проверяем, что создалось:

>show databases;

Переходим на использование БД:

>USE gbdb;

Создаем в БД таблицу:

>CREATE TABLE sales  
(  
id INT NOT NULL PRIMARY KEY AUTO_INCREMENT,  
order_date DATE NOT NULL,  
bucket INT  
);

Заполняем созданную таблицу данными:

>INSERT INTO sales(order_date, bucket)  
VALUES  
(DATE '2023-05-1', 151),  
(DATE '2023-05-2', 171),  
(DATE '2023-05-3', 21),  
(DATE '2023-05-4', 121),  
(DATE '2023-05-5', 351),  
(DATE '2023-05-6', 167),  
(DATE '2023-05-7', 187),  
(DATE '2023-05-8', 37),  
(DATE '2023-05-9', 147),  
(DATE '2023-05-10', 367),  
(DATE '2023-05-11', 125),  
(DATE '2023-05-12', 155),  
(DATE '2023-05-13', 25),  
(DATE '2023-05-14', 125),  
(DATE '2023-05-15', 345);

Проверяем через браузер, что данные добавились:  
Для этого создаем еще один контейнер с phpmyadmin и устанавливаем связь с контейнером, где лежит база данных.  
Эта команда запускает контейнер phpMyAdmin с именем "myphp", связывает его с контейнером MySQL "some-mysql" и пробрасывает порт 8081 для доступа к phpMyAdmin через веб-браузер на хостовой машине.

>docker run --name myphp -d --link some-mysql:db -p 8081:80 phpmyadmin/phpmyadmin


## Логи: ##

root@dmitry-vb:/# docker images  
REPOSITORY   TAG       IMAGE ID   CREATED   SIZE  
root@dmitry-vb:/# docker ps  
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES  
root@dmitry-vb:/# docker ps -a  
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES  
root@dmitry-vb:/#  
root@dmitry-vb:/# docker run --name some-mysql -e MYSQL_ROOT_PASSWORD=mypw -d mysql:8.0.33  
Unable to find image 'mysql:8.0.33' locally  
8.0.33: Pulling from library/mysql  
e2c03c89dcad: Pull complete  
68eb43837bf8: Pull complete  
796892ddf5ac: Pull complete  
6bca45eb31e1: Pull complete  
ebb53bc0dcca: Pull complete  
2e2c6bdc7a40: Pull complete  
6f27b5c76970: Pull complete  
438533a24810: Pull complete  
e5bdf19985e0: Pull complete  
667fa148337b: Pull complete  
5baa702110e4: Pull complete  
Digest: sha256:232936eb036d444045da2b87a90d48241c60b68b376caf509051cb6cffea6fdc  
Status: Downloaded newer image for mysql:8.0.33  
df0d86c5ffe66d3e9cb280b781bca714eae3af5a29383d2d418d97fbd1a27206  
root@dmitry-vb:/# docker ps -a  
CONTAINER ID   IMAGE          COMMAND                  CREATED              STATUS              PORTS                 NAMES  
df0d86c5ffe6   mysql:8.0.33   "docker-entrypoint.s…"   About a minute ago   Up About a minute   3306/tcp, 33060/tcp   some-mysql  
root@dmitry-vb:/# mysql -u root -p mypw  
Enter password:  
ERROR 1049 (42000): Unknown database 'mypw'  
root@dmitry-vb:/# docker exec -it some-mysql bash  
bash-4.4# mysql -u root -p mypw  
Enter password:  
ERROR 1049 (42000): Unknown database 'mypw'  
bash-4.4# mysql -u root  
ERROR 1045 (28000): Access denied for user 'root'@'localhost' (using password: NO)  
bash-4.4# mysql -u root -pmypw  
mysql: [Warning] Using a password on the command line interface can be insecure.  
Welcome to the MySQL monitor.  Commands end with ; or \g.  
Your MySQL connection id is 10  
Server version: 8.0.33 MySQL Community Server - GPL  
  
Copyright (c) 2000, 2023, Oracle and/or its affiliates.  

Oracle is a registered trademark of Oracle Corporation and/or its  
affiliates. Other names may be trademarks of their respective  
owners.  
  
Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.  
  
mysql> show databases;  
+--------------------+  
| Database           |  
+--------------------+  
| information_schema |  
| mysql              |  
| performance_schema |  
| sys                |  
+--------------------+  
4 rows in set (0.01 sec)  
  
mysql> create database gbdb;  
Query OK, 1 row affected (0.02 sec)  
  
mysql> show databases;  
+--------------------+  
| Database           |  
+--------------------+  
| gbdb               |  
| information_schema |  
| mysql              |  
| performance_schema |  
| sys                |  
+--------------------+  
5 rows in set (0.01 sec)  
  
mysql> USE gbdb;  
Database changed  
mysql> CREATE TABLE sales  
-> (  
-> id INT NOT NULL PRIMARY KEY AUTO_INCREMENT,  
->     order_date DATE NOT NULL,  
->     bucket INT  
-> );  
Query OK, 0 rows affected (0.03 sec)  

mysql> INSERT INTO sales(order_date, bucket)  
-> VALUES  
-> (DATE '2023-05-1', 151),  
-> (DATE '2023-05-2', 171),  
-> (DATE '2023-05-3', 21),  
-> (DATE '2023-05-4', 121),  
-> (DATE '2023-05-5', 351),  
-> (DATE '2023-05-6', 167),  
-> (DATE '2023-05-7', 187),  
-> (DATE '2023-05-8', 37),  
-> (DATE '2023-05-9', 147),  
-> (DATE '2023-05-10', 367),  
-> (DATE '2023-05-11', 125),  
-> (DATE '2023-05-12', 155),  
-> (DATE '2023-05-13', 25),  
-> (DATE '2023-05-14', 125),  
-> (DATE '2023-05-15', 345);  
Query OK, 15 rows affected (0.02 sec)  
Records: 15  Duplicates: 0  Warnings: 0  
mysql> exit  
Bye  
bash-4.4# exit  
exit  
root@dmitry-vb:/# docker run --name myphp -d --link some-mysql:db -p 8081:80 phpmyadmin/phpmyadmin  
Unable to find image 'phpmyadmin/phpmyadmin:latest' locally  
latest: Pulling from phpmyadmin/phpmyadmin  
f1f26f570256: Pull complete  
ee0a4e40ccac: Pull complete  
5ca9fb408faa: Pull complete  
5baa808a48ff: Pull complete  
6e8d74e4d8ee: Pull complete  
fac8e70fcf67: Pull complete  
b3b7906fb177: Pull complete  
cb4935bbeb83: Pull complete  
c9e00ef337e3: Pull complete  
cfe495c8d695: Pull complete  
dcc3fd107f0c: Pull complete  
fe3c587d1f07: Pull complete  
677f27d94442: Pull complete  
4d778a8cb653: Pull complete  
5f0f7b557ecd: Pull complete  
6ad259d60f7c: Pull complete  
41acd705cbc4: Pull complete  
912204d5a7e6: Pull complete  
Digest: sha256:ed87921184b59f7d8fc85c6a5f041c22758a4d4419c0ee3bac38eb7e133eaed3  
Status: Downloaded newer image for phpmyadmin/phpmyadmin:latest  
4194068728fbe86b27b50c3364d3c0d8f34c76511100ef721161815a6c68d3fe  
root@dmitry-vb:/#  


## История (history): ##

284  docker images  
285  docker ps  
286  docker ps -a  
287  docker run --name some-mysql -e MYSQL_ROOT_PASSWORD=mypw -d mysql:8.0.33  
288  docker ps -a  
289  mysql -u root -p mypw  
290  docker exec -it some-mysql bash  
291  docker run --name myphp -d --link some-mysql:db -p 8081:80 phpmyadmin/phpmyadmin  

## Скриншот: ##

![runMysql.jpg](img%2FrunMysql.jpg)

![mysqlConnect.jpg](img%2FmysqlConnect.jpg)

![runPhpmyadmin.jpg](img%2FrunPhpmyadmin.jpg)

![phpmyadminConnect.jpg](img%2FphpmyadminConnect.jpg)


*Порядок выполнения практического задания N1:*

Создаtv папку, которую будем монтировать в контейнер:

>mkdir hw_test  
cd hw_test/  
mkdir folder  
cd folder/  

В этой папке создаем файл test.txt и наполняем его данными:

>vim test.txt

В домашней директории создаем файл test.txt и наполняем другими данными:

>cd /home/roddg  
vim test.txt

Создаем контейнер из образа ubuntu:22.10, и запусаем его в интерактивном режиме:  
С именем gb-test.  
C hostname GB.  

Добавляем папки с файлами:

>docker run -it -h GB --name gb-test -v /hw_test/folder:/otherway -v /home/roddg/test.txt:/otherway/test.txt ubuntu:22.10

Проверяем добавленный файл:

>cat test.txt

## Логи: ##

root@dmitry-vb:/# mkdir hw_test  
root@dmitry-vb:/# cd hw_test/  
root@dmitry-vb:/hw_test# mkdir folder  
root@dmitry-vb:/hw_test# ls  
folder  
root@dmitry-vb:/hw_test# cd folder/  
root@dmitry-vb:/hw_test/folder# vim test.txt  
root@dmitry-vb:/hw_test/folder# cd /home/roddg  
root@dmitry-vb:/home/roddg# ls  
100.sh             Dockerfile    example3.c    example.sh   lines_count.txt   nginx_signing.key   text.txt    Загрузки      Общедоступные  
deltempfiles.sh    example2.c    example3.sh   GB           name_user.sh      skript1.sh          Видео       Изображения  'Рабочий стол'  
developer_folder   example2.sh   example.c     hello.py     nano              snap                Документы   Музыка        Шаблоны  
root@dmitry-vb:/home/roddg# vim test.txt  
root@dmitry-vb:/home/roddg# docker run -it -h GB --name gb-test -v /hw_test/folder:/otherway -v /home/roddg/test.txt:/otherway/test.txt ubuntu:22.10  
root@GB:/# cd otherway/  
root@GB:/otherway# ls  
test.txt  
root@GB:/otherway# cat test.txt  
Совершенно другие данные  
root@GB:/otherway#  

## История (history): ##

344  mkdir hw_test
345  cd hw_test/
346  mkdir folder
347  ls
348  cd folder/
349  vim test.txt
350  cd /home/roddg
351  ls
352  vim test.txt
353  docker run -it -h GB --name gb-test -v /hw_test/folder:/otherway -v /home/roddg/test.txt:/otherway/test.txt ubuntu:22.10
354  history

## Скриншот: ##

![testFolder.jpg](img%2FtestFolder.jpg)


