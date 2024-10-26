FROM python:3.12.7-alpine3.20

WORKDIR /app

ENV TZ=Europe/Oslo

RUN apk update \
    && apk add --virtual build-deps gcc python3-dev musl-dev \
    && apk add --no-cache mariadb-dev nano

RUN pip install --upgrade pip

RUN pip install django cryptography sqlalchemy pymysql \
                mysqlclient markdown pygments django-debug-toolbar \
                python-decouple django-taggit==5.0.1 psycopg==3.1.18 \
                Pillow==10.3.0

RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# Create a non-root user
RUN adduser -D django

# Change ownership of the application directory
RUN chown -R 1000:1000 /app

# Switch to the non-root user
USER django

CMD python manage.py runserver 0.0.0.0:8000