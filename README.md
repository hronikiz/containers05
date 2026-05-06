Лабораторная работа №5: WordPress в Docker (Apache + PHP + MariaDB)
📌 Название лабораторной работы

Запуск веб-приложения WordPress в контейнере Docker с использованием Apache HTTP Server, PHP и MariaDB

🎯 Цель работы
Освоить работу с Docker-контейнерами
Научиться разворачивать веб-стек Apache + PHP + MariaDB
Установить и настроить WordPress
Понять работу баз данных в контейнерах
Получить практический опыт работы с веб-приложениями в Docker
📌 Задание
Создать Docker-образ с Apache, PHP и MariaDB
Установить WordPress в контейнер
Настроить базу данных MariaDB
Создать пользователя для базы данных
Подключить WordPress к базе данных
Запустить и проверить работу сайта
Завершить установку WordPress
🧪 Описание выполнения работы
1. Создание проекта

mkdir containers05
cd containers05

📌 Создана директория проекта.

2. Создание Dockerfile

FROM debian:latest

RUN apt-get update &&
apt-get install -y apache2 php libapache2-mod-php php-mysql mariadb-server supervisor curl &&
apt-get clean

📌 Установлены:
Apache2
PHP
MariaDB
Supervisor
curl

3. Сборка Docker-образа

docker build -t apache2-php-mariadb .

📌 Создан Docker-образ.

(вставь скрин сборки)

4. Запуск контейнера

docker run -d -p 8000:80 --name apache2-php-mariadb apache2-php-mariadb

📌 Контейнер запущен, сайт доступен на http://localhost:8000

(вставь скрин docker ps)

5. Проверка Apache

Открыть в браузере:
http://localhost:8000

📌 Отображается Apache Default Page

(вставь скрин страницы)

6. Установка WordPress

cd /var/www/html
curl -o wp.tar.gz https://wordpress.org/latest.tar.gz

tar -xvzf wp.tar.gz
mv wordpress/* .
rm -rf wordpress wp.tar.gz

📌 WordPress установлен в /var/www/html

(вставь скрин файлов)

7. Настройка базы данных MariaDB

CREATE DATABASE wordpress;
CREATE USER 'wordpress'@'%' IDENTIFIED BY 'wordpress';
GRANT ALL PRIVILEGES ON wordpress.* TO 'wordpress'@'%';
FLUSH PRIVILEGES;

📌 Создана база данных и пользователь

(вставь скрин MariaDB)

8. Проверка подключения

mysql -u wordpress -p

📌 Подключение к базе успешно

(вставь скрин)

9. Запуск WordPress

http://localhost:8000

📌 Появился мастер установки WordPress

(вставь скрин установки)

10. Завершение установки

Заполнены данные:
Site Title
Username
Password
Email

📌 WordPress успешно установлен

(вставь финальный скрин)

📊 Вывод

В ходе лабораторной работы:

изучена работа Docker
развернут веб-стек Apache + PHP + MariaDB
установлена CMS WordPress
создана база данных и пользователь
выполнена настройка подключения
получен практический опыт работы с веб-приложением в контейнерах