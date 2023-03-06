# Описание

Проект `YaMDb` собирает отзывы пользователей на произведения из категорий: «Книги», «Фильмы», «Музыка».
![my badge](https://github.com/YuliaKhalaeva/yamdb_final/actions/workflows/main.yml/badge.svg) </p>
[admin panel](http://158.160.10.58/admin/), [redoc](http://158.160.10.58/redoc/) и [api/v1/titles](http://158.160.10.58/api/v1/titles).<p></p>
# Функционал

- Произведения делятся на категории. Список категорий может быть расширен администратором;
- Произведения, фильмы и музыка не хранятся в приложении;
- В каждой категории есть произведения: книги, фильмы или музыка;
- Произведению может быть присвоен жанр из списка предустановленных. Новые жанры может создавать только администратор;
- Пользователи могут оставлять отзывы и ставить оценку произведениям. Из пользовательских оценок формируется рейтинг. На одно произведение можно оставить только один отзыв..

# Stack
- Python
- Django
- Django REST Framework
- Postgres
- Simple JWT
- Docker
- Gunicorn
- Nginx
- Github actions

# Деплой
## Локальный деплой
- Если хотите сделать деплой локально, пожалуйста клонируйте репозиторий https://github.com/YuliaKhalaeva/yamdb_final.
- Создайте .env файл и заполните его данными Postgres которые необходимы в файле settigs.py.
- Установите docker
- Перейдите в yamdb_final\api_yamdb.
- Откройте коммандную строку или git bash и запустите docker-compose up -d --build
- Когда будет необходимо выполните команду apply migrations: docker-compose exec web python manage.py migrate
- После это выполните команду collect static: docker-compose exec web python manage.py collectstatic --no-input
- Наконец создайте superuser and доступ к admin panel: docker-compose exec web python manage.py createsuperuser

## Редеплой на существующем сервере
- Перезапустите jobs в Github Actions или командой push загрузите новую версию кода
- Откройте локальный терминал yamdb_final\api_yamdb\static 
- Запустите scp redoc.yaml name@your-public-ip:/home/name/
- Вернитесь в yamdb_final folder, свяжитесь заново с сервером
- Запустите sudo docker cp redoc.yaml CONTAINER_ID:/app/static
- Запустите sudo docker exec -it CONTAINER_ID /bin/bash и проверьте все ли файлы здесь (ls, cd static, ls)
- В браузере перейдите на ваш-публичный-ip/admin и ваш-публичный-ip/redoc/ для проверки какой проект доступен.

## Деплой на новом сервере
- Выберете Ubuntu при создании нового сервера
- Запустите cat ~/.ssh/id_rsa.pub и вставьте ваш публичный ключ в 'SSH-key' во время создания сервера
- Сделайте ваш публичный ip статическим
- Клонируйте проект с https://github.com/YuliaKhalaeva/yamdb_final.
- Перейдите в yamdb_final, откройте git bash или командную строку и подключитесь к серверу (ssh name@your-public-ip)
- Выполните sudo apt update
- Выполните sudo apt upgrade -y
- Выполните sudo apt install python3-pip python3-venv git -y
- Сгенирируйте пару ssh ключей (во время нахождения на сервере)
- Запустите cat ~/.ssh/id_rsa.pub и вставьте ваш публичный ключ в настройках Github
- Запустите pip install gunicorn 
- Запустите sudo systemctl start gunicorn
- Запустите sudo systemctl enable gunicorn
- Запустите sudo apt install nginx -y 
- Запустите sudo ufw allow 'Nginx Full'
- Запустите sudo ufw allow OpenSSH 
- Запустите sudo ufw enable
- Запустите sudo apt install postgresql postgresql-contrib -y
- Запустите pip install psycopg2-binary==2.8.6 
- Запустите pip install python-dotenv
- Запустите sudo apt install docker.io
- Запустите sudo apt-get update
- Запустите sudo apt-get install docker-compose-plugin
- Обновите secrets в Github Actions
- Перезапустите jobs в Github Actions или запушьте новую версию кода
- Запустите pip3 install -r requirements.txt --no-cache-dir
- Запуститет sudo docker-compose exec web python manage.py migrate
- Запустите sudo docker-compose exec web python manage.py createsuperuser
- Запустите sudo docker-compose exec web python manage.py collectstatic --no-input
- Откройте локальный терминал в yamdb_final\api_yamdb\static 
- Запустите scp redoc.yaml name@your-public-ip:/home/name/
- Вернитесь на yamdb_final folder, переподключитесь к серверу
- Запустите sudo docker cp redoc.yaml CONTAINER_ID:/app/static
- Запустите sudo docker exec -it CONTAINER_ID /bin/bash and check whether the file is there (ls, cd static, ls)
- в браузере,перейдите на ваш-публичный-ip/admin и ваш-публичный-ip/redoc/ чтобы проверить что проект доступен.

