# Проект Foodgram
![example workflow](https://github.com/NIK-TIGER-BILL/foodgram-project-react/actions/workflows/foodgram_workflow.yml/badge.svg)  
  
[![Python](https://img.shields.io/badge/-Python-464646?style=flat-square&logo=Python)](https://www.python.org/)
[![Django](https://img.shields.io/badge/-Django-464646?style=flat-square&logo=Django)](https://www.djangoproject.com/)
[![Django REST Framework](https://img.shields.io/badge/-Django%20REST%20Framework-464646?style=flat-square&logo=Django%20REST%20Framework)](https://www.django-rest-framework.org/)
[![PostgreSQL](https://img.shields.io/badge/-PostgreSQL-464646?style=flat-square&logo=PostgreSQL)](https://www.postgresql.org/)
[![Nginx](https://img.shields.io/badge/-NGINX-464646?style=flat-square&logo=NGINX)](https://nginx.org/ru/)
[![gunicorn](https://img.shields.io/badge/-gunicorn-464646?style=flat-square&logo=gunicorn)](https://gunicorn.org/)
[![docker](https://img.shields.io/badge/-Docker-464646?style=flat-square&logo=docker)](https://www.docker.com/)
[![GitHub%20Actions](https://img.shields.io/badge/-GitHub%20Actions-464646?style=flat-square&logo=GitHub%20actions)](https://github.com/features/actions)
[![Yandex.Cloud](https://img.shields.io/badge/-Yandex.Cloud-464646?style=flat-square&logo=Yandex.Cloud)](https://cloud.yandex.ru/)



Foodgram проект для публиуации и просмотра рецептов блюд.

## Подготовка и запуск проекта
### Склонировать репозиторий на локальную машину:
```
Сделать fork репозитория.
Склонировать репозиторий:
git clone https://github.com/<ваш-username-github>/foodgram-project-react
```
## Для работы с удаленным сервером (на ubuntu):
* Выполните вход на свой удаленный сервер

* Установите docker на сервер:
```
sudo apt install docker.io 
```
* Установите docker-compose на сервер:
```
sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```
* Локально отредактируйте файл infra/nginx.conf и в строке server_name впишите свой IP и адрес сайта.
* Замение username docker-hub, в docker-compose.yml на свои данные.
* Скопируйте файлы docker-compose.yml и nginx.conf из директории infra на сервер:
```
scp docker-compose.yml <username>@<host>:/home/<username>/docker-compose.yml
scp nginx.conf <username>@<host>:/home/<username>/nginx.conf
```

* Cоздайте .env файл и впишите:
    ```
    DEBUG=True or False
    SECRET_KEY=Django_secret_key
    ALLOWED_HOSTS=your_hosts
    CSRF_TRUSTED_ORIGINS=your_hosts
    POSTGRES_USER=postgres_username
    POSTGRES_PASSWORD=postgres_password
    POSTGRES_DB=django
    DB_NAME=django
    DB_HOST=db
    DB_PORT=5432
    ```
* Для работы с Workflow добавьте в Secrets GitHub переменные окружения для работы:
    ```
    DOCKER_PASSWORD=<пароль от DockerHub>
    DOCKER_USERNAME=<имя пользователя>

    USER=<username для подключения к серверу>
    HOST=<IP сервера>
    SSH_PASSPHRASE=<пароль для сервера, если он установлен>
    SSH_KEY=<ваш SSH ключ (для получения команда: cat ~/.ssh/id_rsa)>

    TELEGRAM_TO=<ID чата, в который придет сообщение>
    TELEGRAM_TOKEN=<токен вашего бота>
    ```
    Workflow состоит из трёх шагов:
     - Проверка кода на соответствие PEP8
     - Сборка и публикация образа бекенда на DockerHub.
     - Автоматический деплой на удаленный сервер.
     - Отправка уведомления в телеграм-чат.  
  
* Отправка на сервер:
```
git add .
git commit -m "Комментарий коммита."
git push
```
* После успешной сборки на сервере выполните команды (только после первого деплоя) на сервере в папке проекта:

    - Создать суперпользователя Django:
    ```
    sudo docker-compose exec backend python manage.py createsuperuser
    ```

    Для загрузки ингридиентов:
     - Перейдите по адресу ваш-сайт/admin
     - Авторизуйтесь под суперюзером
     - Перейдите во вкладку ингридиенты
     - Нажимте импорт, выберите файл с ингридиентом, нажмие подтвердить импорт.

## Проект в интернете
Проект запущен и доступен по [адресу](http://iofakh-foodgram.sytes.net/)
