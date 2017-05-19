FROM python:2

# installation de mongodb 3.2
RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv EA312927 \
	&& echo "deb http://repo.mongodb.org/apt/debian jessie/mongodb-org/3.2 main" | tee /etc/apt/sources.list.d/mongodb-org-3.2.list \
	&& mkdir -p /data/db \
	&& mkdir -p /data/db/log \
	&& apt-get update \
    && apt-get install -y mongodb-org \
	&& rm -rf /var/lib/apt/lists/*

# installation de l'application Aidevig
WORKDIR /usr/src/aidevig
RUN git clone https://github.com/Aidevig/Map.git
WORKDIR /usr/src/aidevig/Map
RUN pip install -r requirements.txt
RUN python manage.py migrate

EXPOSE 8000
# CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]
CMD ["./start.sh"]
# le script start.sh se termine par un wait afin de rester en execution
