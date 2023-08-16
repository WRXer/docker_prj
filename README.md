# docker_prj
Задание 1
Complete

Задание 2 и Задание 3
Создать Docker network:

docker network create my-network
Связываем контейнеры в сеть:

docker run -d --name django_app --network my-network -p 8000:8000 -it -v C:\Users\wrx\work\tmp\pgdata:/var/lib/postgresql/data python bash
docker run -d --name postgres-container --network my-network -p 5432:5432 -e POSTGRES_PASSWORD=postgres -e POSTGRES_DB=lab -e POSTGRES_HOST_AUTH_METHOD=md5 -v C:\Users\wrx\work\tmp\pgdata:/var/lib/postgresql/data postgres



pip install django
pip install psycopg2

django-admin startproject app

Настраиваем бд
apt-get update
apt-get install nano
nano app/settings.py
./manage.py migrate
./manage.py runserver




##docker run --name db_django -p 5432:5432 -e POSTGRES_PASSWORD=777Nokia13 -e POSTGRES_DB=public -e POSTGRES_HOST_AUTH_METOD=md5 postgres
###docker run --name django_db -e POSTGRES_PASSWORD=<password> -p 5432:5432 -v C:\Users\wrx\work\tmp\pgdata:/var/lib/postgresql/data postgres


_______________________________________________________
1. docker network create my-network
2. docker run -d --name django_app --network my-network -p 8000:8000 -it python bash
3. docker run -d --name postgres-container --network my-network -p 5432:5432 -e POSTGRES_PASSWORD=postgres -e POSTGRES_DB=lab -e POSTGRES_HOST_AUTH_METHOD=md5 postgres
4. Захожу в постгрес docker exec -it <айди контейнера> psql -U postgres
5. Создаю там бд create database mydb
6. Захожу в джанго
7.  пип инсталлы + nano
8. Создаю проект
9. НАстройки
   ALLOWED_HOSTS = ['127.0.0.1']
   
   DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'mydb',
        'USER': 'postgres',
        'PASSWORD': 'postgres',
        'HOST': 'postgres-container',  # Имя контейнера PostgreSQL
        'PORT': '5432',
    }
}
12. Миграции
13. перезапуск докеров
14. запуск через ./manage.py runserver 0.0.0.0:8000


