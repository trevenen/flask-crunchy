Flask-Crunchy

Flask-Crunchy is a boilerplate framework on top of flask for developing large api backend applications quickly using flask. Built in support for CLI, celery, websocket, eventlet, mongoengine orm, swagger-ui api docs and sphinx docs.

Usage
-----
Flask-Crunchy requires  minimum **python 3.6**.

Before you clone this make sure you have completed the Pre-required Setup Tasks:

* git
* Python3 / pip3 /
* MongoDB
* Redis (Remember to secure Redis to private ip)

For Centos 6.10 min install


.. code:: shell

    yum update -y
    yum groupinstall -y "development tools"
    yum install -y wget zlib-devel bzip2-devel openssl-devel ncurses-devel sqlite-devel readline-devel tk-devel gdbm-devel db4-devel libpcap-devel xz-devel expat-devel
    cd /usr/src
    wget https://www.python.org/ftp/python/3.7.1/Python-3.7.1.tgz
    tar zxf Python-3.7.1.tgz 
    cd Python-3.7.1
    ./configure --enable-optimizations
    make altinstall
    rm /usr/src/Python-3.7.tgz
    python3.7 -V
    python3.7 -m venv fc
    cd fc
    git clone https@github.com:trevenen/flask-crunchy.git
    cd flask-crunchy (rename repository directory to desired value)
    pip3 install -r requirements.txt


For Centos 7


.. code:: shell

    yum -y update
    yum -y install yum-utils
    yum -y groupinstall development
    yum -y install https://centos7.iuscommunity.org/ius-release.rpm
    yum -y install python37u
    python3.7 -V
    yum -y install python37u-pip
    yum -y install python37u-devel
    python3.7 -m venv fc
    cd fc
    git clone https@github.com:trevenen/flask-crunchy.git
    cd flask-crunchy (rename repository directory to desired value)
    pip3 install -r requirements.txt


For Ubuntu 18.04 LTS desktop or server, 


.. code:: shell

    python3 -m venv fc
    cd fc
    git clone https@github.com:trevenen/flask-crunchy.git
    cd flask-crunchy (rename repository directory to desired value)
    pip3 install -r requirements.txt


To start server hit

.. code:: shell

    python3 manage.py run -p 8080

Server will start on port 8080. Hitting http://localhost:8080/ping/ on web browser should return {"message": "pong"}.

API Docs are powered by swagger ui and can be viewed by hitting http://localhost:8080/apidocs/ .

To start celery hit

.. code:: shell

    python3 manage.py celery

To start beat hit

.. code:: shell

    python3 manage.py beat

For available commands and options hit

.. code:: shell

    python manage.py



Structure
---------
.. code:: shell

    ├── CHANGES                     Change logs
    ├── README.rst
    ├── manage.py                   Management commands file
    ├── meta.conf                   App meta conf
    ├── requirements.txt            3rd party libraries libraries
    ├── requirements_test.txt       Testing 3rd libraries
    ├── temp                        Temp directory for storing logs
    ├── app
       ├── __init__.py              App starting point
       ├── app.py                   Main blueprint with before and after request handler
       ├── api_info.py              API level constants
       ├── choices.py               CHOICES constant dictionary
       ├── crons.py                 Crons dictionary file
       ├── exceptions.py            Custom exceptions
       ├── stats.py                 API stats
       ├── wsgi.py                  wsgi app
       ├── wsgi_aux.py              wsgi auxilary app
       ├── utils                    Utils
       │   ├── __init__.py
       │   ├── api_caller.py        Wrapper over requests which handles emits blinker signal over call
       │   ├── common_util.py       common utils
       │   ├── json_util.py         contains custom flask encodes
       │   ├── slack_util.py
       └── api
           └── v1
               └── ├── urls.py url routes
                   ├──demo_api  container one demo api


You can also use docker-compose. Hit below command to start server on port 8080.

.. code:: shell

    docker-compose build
    docker-compose up
