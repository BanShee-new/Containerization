# Урок 1. Механизмы пространства имен #
Задание: необходимо продемонстрировать изоляцию одного и того же приложения (как решено на семинаре - командного интерпретатора) в различных пространствах имен.

Ссылка на [первую практическую работу](https://github.com/BanShee-new/Containerization/blob/main/HW_1/Readme.md) "Механизмы пространства имен")

# Урок 2. Механизмы контрольных групп #
1) запустить контейнер с ubuntu, используя механизм LXC
2) ограничить контейнер 256 Мб ОЗУ и проверить, что ограничение работает
Задание по желанию:
4) добавить автозапуск контейнеру, перезагрузить ОС и убедиться, что контейнер действительно запустился самостоятельно
5) при создании указать файл, куда записывать логи
6) после перезагрузки проанализировать логи

Ссылка на [вторую практическую работу](https://skillbox.ru/media/](https://github.com/BanShee-new/Containerization/tree/main/HW_2) "Репозиторий с файлами")

# Урок 3. Введение в Docker #
Задание:
1) запустить контейнер с БД, отличной от mariaDB, используя инструкции на сайте: https://hub.docker.com/
2) заполнить БД данными через консоль (по желанию) 
3) запустить phpmyadmin (в контейнере) и через веб проверить, что все введенные данные доступны

Задание
- Создать папку, которую мы будем готовы смонтировать в контейнер
- В этой папке создать файл test.txt и наполнить данными
- В домашней директории создать файл test.txt, который также необходимо будет смонтировать в контейнер и наполнить совершенно другими данными
- Создать контейнер из образа ubuntu:22.10
- Задать ему имя
- Задать hostname
- Смонтировать созданную ранее папку с хоста в контейнер
- Смонтировать созданный ранее текстовый файл внутрь смонтированной папки, чтобы он пересекался с созданным ранее файлом в этой папке. Просмотреть этот файл.

Ссылка на [третью практическую работу](https://skillbox.ru/media/](https://github.com/BanShee-new/Containerization/tree/main/HW_3) "Репозиторий с файлами")

# Урок 4. Dockerfile и слои #
Задание: необходимо создать Dockerfile, основанный на любом образе (вы в праве выбрать самостоятельно).
В него необходимо поместить приложение, написанное на любом известном вам языке программирования (Python, Java, C, С#, C++).
При запуске контейнера должно запускаться самостоятельно написанное приложение.

Ссылка на [четвертую практическую работу](https://skillbox.ru/media/](https://github.com/BanShee-new/Containerization/tree/main/HW_4) "Репозиторий с файлами")

# Урок 5. Docker Compose и Docker Swarm #
1) создать сервис, состоящий из 2 различных контейнеров: 1 - веб, 2 - БД (compose)
Задание со звездочкой - повышенной сложности..
2) необходимо создать 3 сервиса в каждом окружении (dev, prod, lab) (не обязательно)
3) по итогу на каждой ноде должно быть по 2 работающих контейнера (не обязательно)
4) выводы зафиксировать

Ссылка на [пятую (итоговую) практическую работу](https://skillbox.ru/media/](https://github.com/BanShee-new/Containerization/tree/main/HW_1) "Итоговая аттестация!")
