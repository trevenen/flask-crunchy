FROM ubuntu:16.04

LABEL maintainer="Thayne Trevenen <trevenen@gmail.com>"
LABEL description="Flask Crunchy Docker file"

ENV LANG='en_US.UTF-8' LANGUAGE='en_US:en' LC_ALL='en_US.UTF-8'

COPY . /srv/flask-crunchy
WORKDIR /srv/flask-crunchy

RUN apt-get update --fix-missing \
&& apt-get install --no-install-recommends -y locales git bash python3 python3-pip build-essential libssl-dev libffi-dev python3-dev \
&& locale-gen en_US.UTF-8 \
&& apt-get -o Dpkg::Options::="--force-confmiss" install --reinstall -y netbase \
&& pip3 install --no-cache-dir --upgrade pip==9.0.3 setuptools \
&& pip3 install --no-cache-dir -r requirements.txt \
&& pip3 install --no-cache-dir -r requirements_test.txt \
&& apt-get clean \
&& rm -r /root/.cache \
&& rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /root/.cache/*
