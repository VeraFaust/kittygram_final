# Kittygram

## Описание:
Kittygram - это социальная сеть.  
На сайте можно:
- создавать учётную запись;
- добавлять фотографии своих котиков и их краткую характеристику;
- редактировать/удалять свои записи.

## В проекте реализовано следующее:
- Настроен запуск проекта Kittygram в контейнерах;
- Настроено автоматическое тестирование и деплой этого проекта на удалённый сервер.  
Автоматизация настроена с помощью сервиса GitHub Actions.

## Технологии:
- Python;
- Django;
- Git;
- Docker;
- PostgreSQL;
- Gunicorn;
- Nginx;
- React;
- DRF;
- Djoser.

## Запуск проекта:
- Клонируйте репозиторий:
```
git clone https://github.com/VeraFaust/kittygram_final.git
```

- Установите и активируйте виртуальное окружение:
```
python -m venv venv
```
```
source venv/Scripts/activate
```

- Установите зависимости из файла requirements.txt:
```
py -m pip install --upgrade pip
```
```
pip install -r requirements.txt
```

- В папке с файлом manage.py запустите миграции:
```
py manage.py makemigrations
```
```
py manage.py migrate
```

- В папке с файлом manage.py создайте админа и запустите проект:
```
py manage.py createsuperuser
```
дописать

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
