#  Описание

## О проекте

Kittygram - это социальная пдатформа, созданная для любителей кошек. Она позволяет создавать и просматривать фотографии кошек, добавлять им описание, цвет и достиения которые добились питомцы.
Автор backend части проекта Рубанов Валентин Сергеевич Контакты: Телеграм - https://t.me/valiksht Email - rubanov.valentin@ya.ru

Backend часть проекта написана на языке python 3.9.13 с использованием таких библотек как: 
Django 3.2.3  
djangorestframework 3.12.4 
djoser 2.1.0 
PyJWT 2.1.0 
Pillow 9.0.0 
PyYAML 6.0 
gunicorn 20.1.0 
webcolors 1.11.1 
gunicorn 20.1.0 
psycopg2-binary 2.9.3

## Клонирование репозитория
Клонирование репозитория командой в терминале:
git clone https://github.com/Valiksht/kittygram_final.git
или
git clone git@github.com:Valiksht/kittygram_final.git

## CD/CI
### код CD/CI для развертывания находится в папке .github/workflows в файле main.yml
для работы CD/CI необходимо установить следующие секреты в hithub:
ALLOWED_HOSTS_URL - юрл адрес сайта
DJANGO_SECRET_KEY - секретный ключ для django
DOCKER_PASSWORD - пароль от аккаунта Docker
DOCKER_USERNAME - логин от аккаунта Docker
HOST - id адрес сервера
USER - имя пользователя для доступа к серверу
SSH_KEY - ssh ключ для доступа к серверу
SSH_PASSPHRASE - пароль от ssh ключа
TELEGRAM_TO - id аккаунта телеграм для отправки уведомлений
TELEGRAM_TOKEN - токен телеграм бота

### После развертывания проекта для доступа в admin зону необходимо создать суперпользователя:
Находясь в папке с проектом kittygram/ (корневой папки проекта, в которой находится файл docker-compose) необходимо выполнить команду:
sudo docker compose -f docker-compose.production.yml exec backend python manage.py createsuperuser


## Создание файла .env
### в папке с проектом kittygram/ (корневой папки проекта, в которой находится файл docker-compose) необходимо создать файл .env с переменными окружения:
POSTGRES_DB = логин для базы данных
POSTGRES_USER = логин пользователя базы данных
POSTGRES_PASSWORD = пароль пользователя базы данных
DB_NAME = название бызы данных
DB_HOST = db
DB_PORT = порт для базы данных, по умолчанию - 5432
DJANGO_SECRET_KEY='ключ для django'
ALLOWED_HOSTS_ID='id сервера'
ALLOWED_HOSTS_URL='url адрес сайта'
DEBUG_STATUS=статус отладки, по умолчанию - False

## Запуск проекта локально через docker conteiner
### для запуска проекта локально через docker conteiner необходимо находясь в корневой папке выполнить команды:
docker-compose build
docker-compose up
### копирование и перенос статики:
docker compose exec backend python manage.py collectstatic
docker composeexec backend cp -r /app/collected_static/. /backend_static/static/
### создание суперпользователя:
docker-compose exec backend python manage.py createsuperuser

## Запуск проекта локально без docker conteiner
### создание виртуального окружения:
python3 -m venv venv
### активация виртуального окружения:
source venv/bin/activate
### перейти в папку с backend проектом:
cd backend
### установка зависимостей:
pip install -r requirements.txt
### создание суперпользователя:
python manage.py createsuperuser
### создание миграций:
python manage.py makemigrations
### Применение миграций:
python manage.py migrate
### запуск проекта:
python manage.py runserver


