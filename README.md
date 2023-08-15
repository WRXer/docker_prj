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



