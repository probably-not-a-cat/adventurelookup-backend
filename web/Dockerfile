FROM python:latest

ENV WORKERS=2
ENV DJANGO_PROJECT_NAME=adventurelookup

RUN apt-get update && apt-get install --no-install-recommends -y \
		gcc \
		gettext \
		mysql-client libmysqlclient-dev \
		postgresql-client libpq-dev \
		sqlite3 \
	&& apt-get clean

VOLUME /app
WORKDIR /app

COPY requirements.txt ./
RUN pip install gunicorn && pip install --no-cache-dir -r requirements.txt

EXPOSE 8000

CMD /usr/local/bin/gunicorn $DJANGO_PROJECT_NAME.wsgi:application --workers $WORKERS --forwarded-allow-ips="*" --bind 0.0.0.0:8000