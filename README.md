Сделал тебе аккуратную **GitHub-версию README.md**, чтобы выглядело “как у нормальных студентов/преподов” — без сломанного форматирования 👇

---

````md
# 📄 Лабораторная работа №5: WordPress в Docker (Apache + PHP + MariaDB)

---

## 📌 Название лабораторной работы
Запуск веб-приложения WordPress в контейнере Docker с использованием Apache HTTP Server, PHP и MariaDB

---

## 🎯 Цель работы
- Освоить работу с Docker-контейнерами  
- Научиться разворачивать веб-стек Apache + PHP + MariaDB  
- Установить и настроить WordPress  
- Понять работу баз данных в контейнерах  
- Получить практику работы с веб-приложениями в Docker  

---

## 📌 Задание
- Создать Docker-образ с Apache, PHP и MariaDB  
- Установить WordPress в контейнер  
- Настроить базу данных MariaDB  
- Создать пользователя для базы данных  
- Подключить WordPress к базе данных  
- Запустить и проверить работу сайта  
- Завершить установку WordPress  

---

# 🧪 Описание выполнения работы

---

## 1. Создание проекта

```bash
mkdir containers05
cd containers05
````

📌 Создана директория проекта.

---

## 2. Создание Dockerfile

```dockerfile
FROM debian:latest

RUN apt-get update && \
    apt-get install -y apache2 php libapache2-mod-php php-mysql mariadb-server supervisor curl && \
    apt-get clean
```

📌 Установлены:

* Apache2
* PHP
* MariaDB
* Supervisor
* curl

---

## 3. Сборка Docker-образа

```bash
docker build -t apache2-php-mariadb .
```

📌 Создан Docker-образ.

📸 Скрин: успешная сборка образа

---

## 4. Запуск контейнера

```bash
docker run -d -p 8000:80 --name apache2-php-mariadb apache2-php-mariadb
```

📌 Контейнер запущен, сайт доступен на `http://localhost:8000`.

📸 Скрин: `docker ps`

---

## 5. Проверка Apache

Открыть в браузере:

```
http://localhost:8000
```

📌 Отображается Apache Default Page.

📸 Скрин: Apache Default Page

---

## 6. Установка WordPress

В контейнере:

```bash
cd /var/www/html

curl -o wp.tar.gz https://wordpress.org/latest.tar.gz

tar -xvzf wp.tar.gz

mv wordpress/* .

rm -rf wordpress wp.tar.gz
```

📌 WordPress установлен в `/var/www/html`.

📸 Скрин: содержимое `/var/www/html`

---

## 7. Настройка базы данных MariaDB

В MariaDB:

```sql
CREATE DATABASE wordpress;

CREATE USER 'wordpress'@'%' IDENTIFIED BY 'wordpress';

GRANT ALL PRIVILEGES ON wordpress.* TO 'wordpress'@'%';

FLUSH PRIVILEGES;
```

📌 Создана база данных и пользователь.

📸 Скрин: создание БД

---

## 8. Проверка подключения к базе

```bash
mysql -u wordpress -p
```

📌 Подключение к базе успешно.

📸 Скрин: вход в MariaDB

---

## 9. Запуск WordPress

Открыть:

```
http://localhost:8000
```

📌 Появился мастер установки WordPress.

📸 Скрин: установка WordPress

---

## 10. Завершение установки

Заполнены данные:

* Site Title
* Username
* Password
* Email

📌 WordPress успешно установлен.

📸 Скрин: успешная установка WordPress

---

# 📊 Вывод

В ходе лабораторной работы:

* изучена работа Docker-контейнеров
* развернут веб-стек Apache + PHP + MariaDB
* установлена CMS WordPress
* создана база данных и пользователь
* выполнена настройка подключения
* получен опыт работы с веб-приложением в контейнерах

```
