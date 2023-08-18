1. Создаем джанго проект или заходим в имеющийся
2. Создаем внутри проекта docker/Dockerfile:

    FROM python:3
    FROM python:3
    
    WORKDIR /code
    
    COPY ./requirements.txt .
    
    RUN pip install -r requirements.txt
    
    COPY . .



3. Создаем docker-compose.yml:

  version: '3'

  services:
  
    db:
    
      image: postgres
      
      environment:
      
        POSTGRES_PASSWORD: 777Nokia13
        PGDATA: /var/lib/postgresql/data/pgdata
  
  
    app:
      build: .
      depends_on:
        - db
      ports:
        - '8000:8000'
      command: python manage.py runserver 0.0.0.0:8000

4. docker-compose build # в терминале приложения собираем образ

5. docker-compose up также # в терминале запускаем образ

6. docker-compose exec app python manage.py migrate    #применяем миграции

