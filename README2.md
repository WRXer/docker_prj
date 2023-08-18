1. Создаем джанго проект или заходим в имеющийся
2. Создаем внутри проекта docker/Dockerfile:
  FROM python:3

  WORKDIR /app
  
  COPY ../requirements.txt /app/
  
  RUN pip install -r requirements.txt
  
  COPY .. /app/
  
  RUN sed -i "s/\r$//g" ./entrypoint
  
  RUN chmod u+x ./entrypoint
  
  ENTRYPOINT ["/app/entrypoint"]

3. Создаем docker-compose.yml:
  version: '3'

  services:
    db:
      image: postgres
      container_name: db_app
      env_file:
        - .env
      volumes:
        - ./data/db:/var/lib/postgresql/data
      ports:
        - '5432:5432'
      healthcheck:
        test: ['CMD-SHELL', 'pg_isready']
        interval: 10s
        timeout: 5s
        retries: 5
  
    redis:
      image: redis:7.0.2-alpine
      container_name: redis_app
      command: redis-server --save 20 1 --loglevel warning
      ports:
        - '6379:6379'
      volumes:
        - ./data/cache:/data
  
  
    app:
      build:
        context: .
        dockerfile: ./docker/Dockerfile
      network_mode: host
      image: app
      container_name: app_container
      depends_on:
        db:
          condition: service_healthy
        redis:
          condition: service_started
      env_file:
        - .env
      ports:
        - '8000:8000'
      volumes:
        - .:/app
      command: python manage.py runserver 0.0.0.0:8000

4. Создаем entrypoint для применения миграций
    #!/bin/bash

    set -o errexit
    set -o pipefail
    set -o nounset
    
    
    python manage.py collectstatic --no-input
    python manage.py migrate --no-input
   
    exec '$@'
5. Создаем докер игнор файл и прописываем в нём /venv
6. docker-compose build      # в терминале приложения собираем образ
7. docker-compose up также    # в терминале запускаем образ

