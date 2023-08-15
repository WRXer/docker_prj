# docker_prj
Задание 1
Complete

Задание 2

docker run -it --name django-project -p 8000:8000 -v C:\Users\wrx\work\tmp\pgdata:/var/lib/postgresql/data python bash

pip install django
pip install psycopg2

django-admin startproject app

Настраиваем бд
apt-get update
apt-get install nano
nano app/settings.py




3 задание:
Создаем контейнер с постгрес с сохранением на винде
docker run --name db_django -p 5432:5432 -e POSTGRES_PASSWORD=777Nokia13 -e POSTGRES_DB=public -e POSTGRES_HOST_AUTH_METOD=md5 postgres
###docker run --name django_db -e POSTGRES_PASSWORD=<password> -p 5432:5432 -v C:\Users\wrx\work\tmp\pgdata:/var/lib/postgresql/data postgres

./manage.py migrate
./manage.py runserver

Подключаемся к постгрес
docker exec -it 995cd8cbd363 psql -U postgres

