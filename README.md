# Лабораторная работа: Запуск WordPress в Docker (Apache + PHP + MariaDB)

---

## Название лабораторной работы
Развёртывание веб-приложения WordPress в Docker-контейнере с использованием Apache HTTP Server, PHP и MariaDB

---

## Цель работы
- Освоить работу с Docker-контейнерами  
- Научиться развертывать веб-стек Apache + PHP + MariaDB  
- Установить и настроить CMS WordPress  
- Научиться работать с базой данных MariaDB в контейнере  
- Получить практический опыт работы с веб-приложениями в Docker  

---

## Задание
1. Создать Docker-образ с Apache, PHP и MariaDB  
2. Запустить контейнер  
3. Установить WordPress  
4. Настроить базу данных MariaDB  
5. Создать пользователя базы данных  
6. Подключить WordPress к базе данных  
7. Проверить работу сайта в браузере  

---

## Описание выполнения работы

---

### 1. Создание проекта

```bash
mkdir containers05
cd containers05

Создана папка проекта для лабораторной работы.

2. Создание Dockerfile
FROM debian:latest

RUN apt-get update && \
    apt-get install -y apache2 php libapache2-mod-php php-mysql mariadb-server supervisor curl && \
    apt-get clean

Установлены:

Apache2
PHP
MariaDB
Supervisor
curl
3. Сборка Docker-образа
docker build -t apache2-php-mariadb .

Создан Docker-образ с веб-стеком.

4. Запуск контейнера
docker run -d -p 8000:80 --name apache2-php-mariadb apache2-php-mariadb

Контейнер запущен и доступен по адресу:

http://localhost:8000

5. Проверка работы Apache

В браузере открыть:

http://localhost:8000

Отображается стандартная страница Apache (Debian Default Page).

6. Установка WordPress

Внутри контейнера:

cd /var/www/html

curl -o wp.tar.gz https://wordpress.org/latest.tar.gz

tar -xvzf wp.tar.gz

mv wordpress/* .

rm -rf wordpress wp.tar.gz

WordPress установлен в директорию /var/www/html.

7. Создание базы данных MariaDB

Войти в MariaDB:

mysql

Выполнить команды:

CREATE DATABASE wordpress;

CREATE USER 'wordpress'@'%' IDENTIFIED BY 'wordpress';

GRANT ALL PRIVILEGES ON wordpress.* TO 'wordpress'@'%';

FLUSH PRIVILEGES;

Создана база данных и пользователь для WordPress.

8. Проверка работы базы данных
mysql -u wordpress -p

Подключение к базе данных успешно.

9. Запуск WordPress

Открыть в браузере:

http://localhost:8000

Появляется мастер установки WordPress.

10. Завершение установки WordPress

Ввести данные:

Site Title
Username
Password
Email

WordPress успешно установлен и работает.

Выводы
Изучена работа Docker-контейнеров
Развёрнут веб-стек Apache + PHP + MariaDB
Установлен WordPress в контейнере
Создана база данных и пользователь MariaDB
Настроено подключение WordPress к базе данных
Получен практический опыт работы с веб-приложениями в Docker
