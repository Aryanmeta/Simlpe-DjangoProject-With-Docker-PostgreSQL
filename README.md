    Create new Django project with Docker
<br><br>
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