FROM ubuntu:16.04 AS base
WORKDIR /opt
RUN apt-get update && apt-get install -y python python-pip
COPY requirements.txt /opt
RUN pip install -r requirements.txt

FROM base as src
COPY . /opt

FROM src as test
COPY requirements.dev.txt /app
RUN pip3 install -r requirements.dev.txt
RUN python -m pytest


ENTRYPOINT FLASK_APP=/opt/app.py FLASK_RUN_PORT=8080 flask run --host=0.0.0.0
