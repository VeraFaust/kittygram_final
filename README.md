### Как запустить проект:

# Клонировать репозиторий и перейти в него в командной строке:
1) git clone git@github.com:VeraFaust/kittygram_final.git
2) cd kittygram_final

# Установить Docker Desktop. Убедиться, что он запущен:
На Linux: sudo systemctl status docker.
На Windows: должно быть открыто десктопное приложение.

# Билдим образы: 
cd frontend
docker build -t ваш_никнейм/kittygram_frontend .
cd ../backend
docker build -t ваш_никнейм/kittygram_backend .
cd ../nginx
docker build -t ваш_никнейм/kittygram_gateway .

# Пушим образы на DockerHub:
docker push ваш_никнейм_на_докерхаб/kittygram_frontend
docker push ваш_никнейм_на_докерхаб/kittygram_backend
docker push ваш_никнейм_на_докерхаб/kittygram_gateway

# Копируем docker-compose.production.yml и .env на сервер.

# Создаём папку проекта на сервере и выполняем докер-компоуз:
sudo docker-compose -f путь_до_директории_проекта/docker-compose.production.yml up -d

# Создаём миграции:
sudo docker-compose -f путь_до_директории_проекта/docker-compose.production.yml exec backend python manage.py migrate

# Собираем статику: 
sudo docker-compose -f путь_до_директории_проекта/docker-compose.production.yml exec backend python manage.py collectstatic
sudo docker-compose -f путь_до_директории_проекта/docker-compose.production.yml exec backend cp -r /app/collected_static/. /static/collected_static/
