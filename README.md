
# Kittygram

[![Main Kittygram workflow](https://github.com/Dmitry8815585/kittygram_final/actions/workflows/main.yml/badge.svg)](https://github.com/Dmitry8815585/kittygram_final/actions/workflows/main.yml)

Kittygram - сервис для публикации данных о котиках.

На сервере размещён и Taski-docker (https://github.com/Dmitry8815585/taski-docker). 
Сервер Nginx, уже развёрнутый на сервере, переадресовывает запросы по назначению — в Taski или в Kittygram.

## Описание

Основная идея проекта заключается в запуске проекта Kittygram в контейнерах с 
автоматическим тестированием и деплоем этого проекта на удалённый сервер.

Мои задачи включали в себя настройку WSGI-сервера (Gunicorn) для эффективной работы с бэкенд-приложением проекта, а также настройку веб-сервера Nginx . Я обеспечил шифрование запросов по протоколу HTTPS, написал Dockerfile для создания образов и реализовал запуск таск-менеджера в контейнерах. Дополнительно, процессы тестирования и деплоя проекта были автоматизированы с использованием GitHub Actions.

## Стек проекта: Docker, Nginx, Gunicorn, workflow, GitHub Actions, CI/CD, Linux

## Требования

Прежде чем начать, убедитесь, что у вас установлены следующие инструменты:

- Docker: [установка Docker](https://docs.docker.com/get-docker/)
- Docker Compose: [установка Docker Compose](https://docs.docker.com/compose/install/)
- Node.js: [установка Node.js](https://nodejs.org/)


## Установка

Нужно скопировать содержимое .env.example в локальный файл .env и проставить нужные значения вместо CHANGE_ME

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


