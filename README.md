# Лабораторная работа №5: WordPress в Docker (Apache + PHP + MariaDB)

## Название лабораторной работы
Запуск веб-приложения WordPress в Docker-контейнере с использованием Apache HTTP Server, PHP и MariaDB

---

## Цель работы
- Освоить работу с Docker-контейнерами  
- Развернуть стек Apache + PHP + MariaDB  
- Установить и настроить WordPress  
- Научиться работать с базой данных MariaDB  
- Получить практику работы с веб-приложениями в контейнерах  

---

## Задание
1. Создать Docker-образ с Apache, PHP и MariaDB  
2. Запустить контейнер  
3. Установить WordPress  
4. Настроить базу данных MariaDB  
5. Создать пользователя базы данных  
6. Подключить WordPress к базе данных  
7. Проверить работу сайта  

---

## Описание выполнения работы

### 1. Создание проекта
```bash
mkdir containers05
cd containers05
````

Создана рабочая директория проекта.

---

### 2. Создание Dockerfile

```dockerfile
FROM debian:latest

RUN apt-get update && \
    apt-get install -y apache2 php libapache2-mod-php php-mysql mariadb-server supervisor curl && \
    apt-get clean
```

Установлены компоненты:

* Apache2
* PHP
* MariaDB
* Supervisor

<img width="322" height="352" alt="Снимок экрана 2026-05-06 185940" src="https://github.com/user-attachments/assets/3a1c651d-fc48-4299-9d07-53ac603d1e70" />

---

### 3. Сборка образа

```bash
docker build -t apache2-php-mariadb .
```

Docker-образ успешно собран.

---

### 4. Запуск контейнера

```bash
docker run -d -p 8000:80 --name apache2-php-mariadb apache2-php-mariadb
```

Контейнер запущен.
---

### 5. Проверка Apache

Открыть:

[http://localhost:8000](http://localhost:8000)

Отображается стандартная страница Apache (Debian Default Page).

<img width="1919" height="1079" alt="Снимок экрана 2026-05-06 135643" src="https://github.com/user-attachments/assets/8d34ed8d-2dfd-42ed-a93d-7671c28c363a" />

---

### 6. Установка WordPress

```bash
cd /var/www/html

curl -o wp.tar.gz https://wordpress.org/latest.tar.gz

tar -xvzf wp.tar.gz

mv wordpress/* .

rm -rf wordpress wp.tar.gz
```

WordPress установлен в директорию `/var/www/html`.

<img width="1919" height="1079" alt="Снимок экрана 2026-05-06 140438" src="https://github.com/user-attachments/assets/0517d81d-038d-481c-8b3f-6358cbb1e072" />

---

### 7. Создание базы данных

```sql
CREATE DATABASE wordpress;

CREATE USER 'wordpress'@'%' IDENTIFIED BY 'wordpress';

GRANT ALL PRIVILEGES ON wordpress.* TO 'wordpress'@'%';

FLUSH PRIVILEGES;
```

Созданы база данных и пользователь.

---

### 8. Проверка подключения

```bash
mysql -u wordpress -p
```

Подключение к базе данных успешно.

---

### 9. Запуск WordPress

Открыть:

[http://localhost:8000](http://localhost:8000)

Появляется установка WordPress.

<img width="1919" height="1079" alt="Снимок экрана 2026-05-06 143659" src="https://github.com/user-attachments/assets/ce6aeb86-eda8-4c6f-94ff-93b6888ed819" />

---

### 10. Завершение установки

Заполнены поля:

* Site Title
* Username
* Password
* Email

WordPress успешно установлен.

---

## Вывод

В ходе работы:

* изучен Docker
* развернут стек Apache + PHP + MariaDB
* установлен WordPress
* создана база данных
* выполнена настройка подключения
* получен опыт работы с веб-приложением в контейнере

```
