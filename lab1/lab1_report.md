Лабораторная работа №1. Основы работы с Docker

University: ITMO University
Faculty: FICT
Course: Введение в веб-технологии
Year: 2025/2026
Group: U4225
Author: Angelina Diachkova
Lab: Lab1
Date of create: 08.09.2026
Date of finished: —

Цель работы

Изучить основные возможности Docker: работу с образами и контейнерами, запуск веб-сервера, управление контейнерами и использование Docker Volumes.

Ход работы

Шаг 1. Установка Docker Desktop

Для выполнения лабораторной работы был установлен Docker Desktop для Windows.

![Docker Desktop](images/1.png)

Шаг 2. Проверка версии Docker


![Проверка версии Docker](images/2.png)

Шаг 3. Запуск тестового контейнера
Docker скачал готовый образ hello-world, создал из него контейнер и запустил его.

![Запуск hello-world](images/3.png)

Шаг 4. Просмотр образов и контейнеров
Были выполнены команды:

docker images
docker ps
docker ps -a
![Просмотр образов и контейнеров](images/4.png)
docker ps показывает только контейнеры, которые сейчас работают.

docker ps -a показывает все контейнеры, в том числе остановленные

Шаг 5. Загрузка образа Ubuntu
Команда скачала готовый образ Ubuntu.
![Загрузка Ubuntu](images/5.png)

Шаг 6. Запуск контейнера Ubuntu
Была выполнена команда:

docker run -it ubuntu bash
Из образа Ubuntu был создан новый контейнер
![Запуск контейнера Ubuntu](images/6.png)

Шаг 7. Обновление списка пакетов
Внутри Ubuntu была выполнена команда:

apt update

![Обновление списка пакетов](images/7.png)

Шаг 8. Установка curl
Была выполнена команда:

apt update && apt install -y curl

![Установка curl](images/8.png)

![Процесс установки curl](images/9.png)

![Завершение установки curl](images/10.png)
В контейнер Ubuntu была установлена программа curl.

curl позволяет выполнять сетевые запросы через терминал.

-y означает автоматическое подтверждение установки


Шаг 9. Проверка установки curl

Была выполнена команда:

curl --version

После этого был выполнен выход из контейнера:

exit


![Проверка curl](images/11.png)

Шаг 10. Запуск веб-сервера nginx
docker run -d -p 8080:80 --name web-server nginx:alpine
После этого работа контейнера была проверена:
docker ps

Был создан контейнер с веб-сервером nginx

![Запуск nginx](images/12.png)

Шаг 11. Проверка работы nginx
В браузере был открыт адрес:

http://localhost:8080

Появилась стандартная страница Welcome to nginx!
![Проверка nginx](images/13.png)

Шаг 12. Просмотр логов nginx

Была выполнена команда:

docker logs web-server

![Логи nginx](images/14.png)

Шаг 13. Подключение к контейнеру nginx
Была выполнена команда:
docker exec -it web-server sh

После проверки был выполнен выход:
exit

![Подключение к контейнеру](images/15.png)
docker exec позволяет выполнить команду внутри уже работающего контейнера.

Шаг 14. Управление контейнерами

Были выполнены команды:

docker ps
docker ps -a
docker stop web-server
docker ps
docker ps -a
docker start web-server
docker ps
![Управление контейнером](images/16.png)
docker stop web-server останавливает контейнер, но не удаляет его.

После остановки он исчезает из docker ps, потому что там показываются только работающие контейнеры.

В docker ps -a он остаётся.

docker start web-server снова запускает этот же контейнер.

Шаг 15. Удаление контейнера и образа nginx

docker stop web-server
docker rm web-server
docker ps -a
docker rmi nginx:alpine
docker images

![Удаление контейнера и образа](images/17.png)
docker rm web-server удаляет сам контейнер.

docker rmi nginx:alpine удаляет образ nginx.

Шаг 16. Создание Docker Volume
Была выполнена команда:
docker volume create my-volume

Для проверки:
docker volume ls

После этого был создан контейнер с подключённым Volume:
docker run -it --name volume-test -d -v my-volume:/data ubuntu bash

Для входа в контейнер:
docker exec -it volume-test bash

Внутри контейнера был создан файл:
echo "Hello from volume" > /data/test.txt

Затем его содержимое было проверено:
cat /data/test.txt

![Создание Docker Volume](images/18.png)

Шаг 17. Проверка сохранения данных в Docker Volume

Первый контейнер был остановлен и удалён
Создан новый контейнер с тем же Volume

Файл сохранился после удаления первого контейнера

![Проверка Docker Volume](images/19.png)

Шаг 18. Проверка контейнеров в Docker Desktop

Созданные контейнеры были проверены через графический интерфейс Docker Desktop.

![Контейнеры Docker Desktop](images/20.png)

Вывод

В ходе лабораторной работы были изучены основные команды Docker, работа с образами и контейнерами, запуск веб-сервера nginx, управление контейнерами и использование Docker Volumes для сохранения данных.
