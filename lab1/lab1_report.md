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

Выполнена команда:

```powershell
docker --version
```

Команда использовалась для проверки установленной версии Docker.

![Проверка версии Docker](images/2.png)

Шаг 3. Запуск тестового контейнера

Выполнена команда:

```powershell
docker run hello-world
```

Был загружен образ hello-world и запущен тестовый контейнер.

![Запуск hello-world](images/3.png)

Шаг 4. Просмотр образов и контейнеров

Выполнены команды:

```powershell
docker images
docker ps
docker ps -a
```

Команды использовались для просмотра образов, работающих и остановленных контейнеров.

![Просмотр образов и контейнеров](images/4.png)

Шаг 5. Загрузка образа Ubuntu

Выполнена команда:

```powershell
docker pull ubuntu:latest
```

Образ Ubuntu был загружен из Docker Hub.

![Загрузка Ubuntu](images/5.png)

Шаг 6. Запуск контейнера Ubuntu

Выполнена команда:

```powershell
docker run -it ubuntu bash
```

Был создан интерактивный контейнер Ubuntu и открыт Bash.

![Запуск контейнера Ubuntu](images/6.png)

Шаг 7. Обновление списка пакетов

Внутри контейнера выполнена команда:

```bash
apt update
```

Была обновлена информация о доступных пакетах Ubuntu.

![Обновление списка пакетов](images/7.png)

Шаг 8. Установка curl

Выполнена команда:

```bash
apt update && apt install -y curl
```

Утилита curl была установлена внутри контейнера Ubuntu.

![Установка curl](images/8.png)

![Процесс установки curl](images/9.png)

![Завершение установки curl](images/10.png)

Шаг 9. Проверка установки curl

Выполнена команда:

```bash
curl --version
```

После проверки выполнен выход из контейнера:

```bash
exit
```

![Проверка curl](images/11.png)

Шаг 10. Запуск веб-сервера nginx

Выполнена команда:

```powershell
docker run -d -p 8080:80 --name web-server nginx:alpine
```

Для проверки работающего контейнера использована команда:

```powershell
docker ps
```

![Запуск nginx](images/12.png)

Шаг 11. Проверка работы nginx

В браузере открыт адрес:

```text
http://localhost:8080
```

Появилась стандартная страница Welcome to nginx!, что подтвердило успешную работу веб-сервера.

![Проверка nginx](images/13.png)

Шаг 12. Просмотр логов nginx

Выполнена команда:

```powershell
docker logs web-server
```

В логах были отображены запросы браузера к веб-серверу.

![Логи nginx](images/14.png)

Шаг 13. Подключение к контейнеру nginx

Выполнена команда:

```powershell
docker exec -it web-server sh
```

Была открыта командная оболочка внутри работающего контейнера.

После проверки выполнена команда:

```bash
exit
```

![Подключение к контейнеру](images/15.png)

Шаг 14. Управление контейнерами

Для просмотра контейнеров выполнены команды:

```powershell
docker ps
docker ps -a
```

Контейнер был остановлен:

```powershell
docker stop web-server
```

После этого контейнер был повторно запущен:

```powershell
docker start web-server
```

Результат проверен командой:

```powershell
docker ps
```

![Управление контейнером](images/16.png)

Шаг 15. Удаление контейнера и образа nginx

Контейнер был остановлен и удалён:

```powershell
docker stop web-server
docker rm web-server
```

Образ nginx был удалён:

```powershell
docker rmi nginx:alpine
```

Результат проверен командами:

```powershell
docker ps -a
docker images
```

![Удаление контейнера и образа](images/17.png)

Шаг 16. Создание Docker Volume

Создан Docker Volume:

```powershell
docker volume create my-volume
```

Проверен список томов:

```powershell
docker volume ls
```

Создан контейнер с подключённым томом:

```powershell
docker run -it --name volume-test -d -v my-volume:/data ubuntu bash
```

Выполнено подключение к контейнеру:

```powershell
docker exec -it volume-test bash
```

Внутри контейнера создан файл:

```bash
echo "Hello from volume" > /data/test.txt
```

Проверено его содержимое:

```bash
cat /data/test.txt
```

Результат:

```text
Hello from volume
```

После этого выполнен выход:

```bash
exit
```

![Создание Docker Volume](images/18.png)

Шаг 17. Проверка сохранения данных в Docker Volume

Первый контейнер был остановлен и удалён:

```powershell
docker stop volume-test
docker rm volume-test
```

Проверено, что Volume сохранился:

```powershell
docker volume ls
```

Создан новый контейнер с тем же Volume:

```powershell
docker run -it --name volume-test-2 -d -v my-volume:/data ubuntu bash
```

Выполнено подключение:

```powershell
docker exec -it volume-test-2 bash
```

Проверено содержимое ранее созданного файла:

```bash
cat /data/test.txt
```

Результат:

```text
Hello from volume
```

Файл сохранился после удаления первого контейнера.

![Проверка Docker Volume](images/19.png)

Шаг 18. Проверка контейнеров в Docker Desktop

Созданные контейнеры были проверены через графический интерфейс Docker Desktop.

![Контейнеры Docker Desktop](images/20.png)

Вывод

В ходе лабораторной работы были изучены основные команды Docker, работа с образами и контейнерами, запуск веб-сервера nginx, управление контейнерами и использование Docker Volumes для сохранения данных.