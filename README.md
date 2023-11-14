
# Kittygram

[![Main Kittygram workflow](https://github.com/Dmitry8815585/kittygram_final/actions/workflows/main.yml/badge.svg)](https://github.com/Dmitry8815585/kittygram_final/actions/workflows/main.yml)

Kittygram - сервис для публикации данных о котиках.

## Описание

Основная идея проекта заключается в запуске проекта Kittygram в контейнерах с 

автоматическим тестированием и деплоем этого проекта на удалённый сервер.

## Требования

Прежде чем начать, убедитесь, что у вас установлены следующие инструменты:

- Docker: [установка Docker](https://docs.docker.com/get-docker/)
- Docker Compose: [установка Docker Compose](https://docs.docker.com/compose/install/)
- Node.js: [установка Node.js](https://nodejs.org/)


## Установка

1. Клонировать репозиторий:

    git clone https://github.com/good8815585/kittygram.git
    cd kittygram

2. Установить зависимости бэкенда:

    docker-compose -f docker-compose.production.yml run backend python manage.py migrate

3. Установить зависимости фронтенда:

    docker-compose -f docker-compose.production.yml run frontend npm install

4. Собрать статические файлы и собрать Docker-образы:

    docker-compose -f docker-compose.production.yml build

## Запуск

Нужно скопировать содержимое .env.example в локальный файл .env и проставить нужные значения вместо CHANGE_ME


Запустить Docker-контейнеры:

    docker-compose -f docker-compose.production.yml up -d

        Провести миграции и собрать статические файлы:

            docker-compose -f docker-compose.production.yml exec backend python manage.py migrate
            docker-compose -f docker-compose.production.yml exec backend python manage.py collectstatic
            docker-compose -f docker-compose.production.yml exec backend cp -r /app/collected_static/. /backend_static/static/


## Тестирование

    Запустить тесты бэкенда:

        docker-compose -f docker-compose.production.yml exec backend python manage.py test

    Запустить тесты фронтенда:

        docker-compose -f docker-compose.production.yml exec frontend npm run test

## Деплой

    Проект автоматически деплоится при пуше в ветку main с использованием GitHub Actions.
    После успешного выполнения придет сообщение в Telegram.


