# What is this project?
<span><img src="https://img.shields.io/badge/Django-092E20?style=flat&logo=django&logoColor=green" /></span>
<span><img src="https://img.shields.io/badge/Docker-2CA5E0?style=flat&logo=docker&logoColor=white" /></span>
<span><img src="https://img.shields.io/badge/PostgreSQL-316192?style=flat&logo=postgresql&logoColor=white" /></span>

This is a boilerplate to start a django project with postgresql as database running on docker.
<br>
<br>

1 - Create a Virtual Environment in project Directory => python -m venv venv<br>
2 - Active Virtual Environment => .\venv\Scripts\activate<br>
3 - Install Django in project => pip install django<br>
4 - Create a config file => django-admin startproject config .<br>
5 - Migrate project => python manage.py migrate<br>
6 - Now test your project => python manage.py runserver<br>
7 - Create requirements.txt => pip freeze > requirements.txt<br>
8 - Create Docker File => new > Dockerfile<br>

    FROM python:3.10.6

    ENV PYTHONDONTWRITEBYTECODE 1
    ENV PYTHONUNBUFFERED 1
    
    WORKDIR /code
    
    COPY requirements.txt /code/
    RUN pip install -r requirements.txt
    
    COPY . /code/
9 - Create .docker ignore file => new > .dockerignore<br>

    venv
10 - Run command "docker build ." in terminal <br>
11 - Create docker-compose file => new > docker-compose.yml 
    
    version: '2.12.0'
    
    services:
      web:
        build: .
        command: python /code/manage.py runserver 0.0.0.0:8000
        volumes:
          - .:/code
        ports:
          - 8000:8000

12 - run command "docker-compose up" in terminal <br>
13 - Container for postgres = > go to docker-compose.yml : 

    db:
        image: postgres:15
        environment:
            - "POSTGRES_HOST_AUTH_METHOD=trust"

14 - Run :
- docker-compose up



15 - Connect to Postgres :
- config > settings.py > DATABASES :
    

        DATABASES = {
            'default': { 
                'ENGINE': 'django.db.backends.postgresql',
                'NAME': 'postgres',
                'USER': 'postgres',
                'PASSWORD': 'postgres',
                'HOST': 'db',
                'PORT': 5432,
            }
        }
16 - Install psycopg2 Package : 
- docker-compose exec web pip install psycopg2-binary
<br>
<br>

17 - Stop docker-compose : 
- ctrl + c

<br>

18 - add psycopg2 to requirements.txt :
- pip install psycopg2
- pip freeze > requirements.txt 

<br>

19 - Run : 
- docker-compose up --build 

<br>

20 - Migrate project :
<h4><b>Send to Postgresql</h4>
- docker-compose exec web python manage.py migrate</b>

<br>
<br>


21 - Create superuser : 
- docker-compose exec web python manage.py createsuperuser

<br>

Now the project is connected to Postgresql 😍💗
- 

