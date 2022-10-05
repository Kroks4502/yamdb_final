# Проект YaMDb
![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54) ![DjangoREST](https://img.shields.io/badge/DJANGO-REST-ff1709?style=for-the-badge&logo=django&logoColor=white&color=ff1709&labelColor=gray)

Учебный проект освоения принципов REST API. Представляет собой блог-систему
с возможностью регистрации и публикации отзывов на произведения. Создан Docker-файл (api_yamdb/Dockerfile) и 
инструкции по развёртыванию проекта в файле infra/docker-compose.yaml

## Возможности API
- Самостоятельная регистрация пользователей.
- Назначение ролей пользователям.
- Получение опубликованных произведений, жанров, отзывов и комментариев к ним с пагинацией.

## Технологии
В целях реализации практики были использованы:
- Python 3.7.9
- Django Framework v2.2.16
- Django REST framework v3.12.4
- Simple JWT v4.7.2
- python-dotenv v0.20.0
- gunicorn v20.0.4
- asgiref v3.2.10
- sqlparse v0.3.1
- Хранение базы данных на базе образа postgres:13.0-alpine
- Сервер на базе образа Docker nginx:1.21.3-alpine

## Запуск проекта:

В проекте подготовлена инструкция по развёртыванию проекта в файле infra/docker-compose.yaml. 
Для запуска проекта на вашем сервере должен быть развернут [Docker](https://www.docker.com/).

Создайте файл .env в директории infra/, заполнив следующие переменные среды:

```
SECRET_KEY=<ваш-ключ>
ALLOWED_HOSTS='["127.0.0.1", "localhost", "web"]'
DB_ENGINE=django.db.backends.postgresql
DB_NAME=postgres
POSTGRES_USER=postgres
POSTGRES_PASSWORD=postgres
DB_HOST=db
DB_PORT=5432
```

Из директории api_yamdb/ соберите контейнер, командой

```
docker-compose up -d
```

Выполните миграции в контейнере web:

```
docker-compose exec web python manage.py migrate
docker-compose exec web python manage.py createsuperuser
docker-compose exec web python manage.py collectstatic --no-input
```

## Примеры запросов:

После запуска проекта перейдите по адресу: http://127.0.0.1/redoc/, где вы найдёте документацию проекта.

## Лицензия:

Данный опубликован под лицензией MIT.
