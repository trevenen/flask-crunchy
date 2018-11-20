Flask-Crunchy

Flask-Crunchy is a boilerplate framework on top of flask for developing large api backend applications quickly using flask. Built in support for CLI, celery, websocket, eventlet, mongoengine orm, swagger-ui api docs and sphinx docs.

Usage
-----
Flask-Crunchy requires  minimum **python 3.6**. 

Before you clone this make sure you have completed the Pre-required Setup Tasks: 

* git 
* Python3 / pip3 https://www.digitalocean.com/community/tutorials/how-to-install-python-3-and-set-up-a-local-programming-environment-on-centos-7
* MongoDB https://www.digitalocean.com/community/tutorials/how-to-install-mongodb-on-centos-7
* Redis (Remember to secure Redis to private ip) https://www.linode.com/docs/databases/redis/install-and-configure-redis-on-centos-7/ or https://www.digitalocean.com/community/tutorials/how-to-install-secure-redis-centos-7

For Centos 6.10 min install


.. code:: shell

    yum update -y
    yum groupinstall -y "development tools"
    yum install -y wget ntp zlib-devel bzip2-devel openssl-devel ncurses-devel sqlite-devel readline-devel tk-devel gdbm-devel db4-devel libpcap-devel xz-devel expat-devel
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
    git clone https://github.com/trevenen/flask-crunchy.git
    cd flask-crunchy (rename repository directory to desired value)
    pip3 install -r requirements.txt


For Centos 7


.. code:: shell

    yum -y groupinstall development
    yum -y install https://centos7.iuscommunity.org/ius-release.rpm    
    yum -y install epel-release
    yum -y update
    yum -y install ntp vim screen yum-utils mongodb redis monit
    timedatectl set-timezone America/Boise
    systemctl enable ntpd
    systemctl start ntpd
    less /etc/ntp.conf
    systemctl start monit
    systemctl enable monit
    less /etc/monitrc
    firewall-cmd --permanent --new-zone=redis
    firewall-cmd --permanent --zone=redis --add-port=6379/tcp
    firewall-cmd --permanent --zone=redis --add-source=127.0.0.1
    firewall-cmd --reload
    systemctl start redis.service
    systemctl enable redis
    systemctl status redis.service
    redis-cli ping
    vim /etc/redis.conf ; \# edit to bind your private ip, normally 127.0.0.1 and requirepass foobared
    firewall-cmd --permanent --new-zone=redis
    firewall-cmd --permanent --zone=redis --add-port=6379/tcp
    firewall-cmd --permanent --zone=redis --add-source=127.0.0.1
    firewall-cmd --reload
    systemctl restart redis.service
    redis-cli
    auth your_redis_password
    set key1 10
    get key1
    quit
    ls -l /var/lib | grep redis
    chmod 770 /var/lib/redis
    chown redis:redis /etc/redis.conf
    chmod 660 /etc/redis.conf
    ls -l /etc/redis.conf
    service redis-server restart  
    yum -y install python36u \; \#(has a slightly lower minor release number than the EPEL one)
    python3.6 -V
    yum -y install python36u-pip
    yum -y install python36u-devel
    python3.6 -m venv fc
    cd fc
    source bin/activate
    pip install --upgrade pip
    git clone https://github.com/trevenen/flask-crunchy.git
    cd flask-crunchy (rename repository directory to desired value)
    pip3 install -r requirements.txt


For Ubuntu 18.04 LTS desktop or server, 


.. code:: shell

    python3 -m venv fc
    cd fc
    git clone https://github.com/trevenen/flask-crunchy.git
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
