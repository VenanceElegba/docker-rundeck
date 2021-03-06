# docker-rundeck

Rundeck is an open source automation service with a web console, command line tools and a WebAPI. It lets you easily run automation tasks across a set of nodes.


* Configure rundeck directly in the docker-compose.yml

```
MYSQL_DATABASE: rundeck #database for rundeck
MYSQL_USER: rundeck #user the database
MYSQL_PASSWORD: 641949548825f1f8c51d5f547ab88faa #password for rundeck


MYSQL_DATABASE: rundeck #use the same as above
MYSQL_USER: rundeck #use the same as above
MYSQL_PASSWORD: 641949548825f1f8c51d5f547ab88faa #use the same as above
HOST_RUNDECK: localhost #this variable is to generate the SSL certificate, so specify your domain name
SERVER_URL: https://localhost:4443 #if you use rundeck behind nginx/apache specfiy https://domain.name.com
PASSWORD: admin #default password for the rundeck admin user
```


```
mysql:
    image: mysql:5.7
    environment:
        MYSQL_DATABASE: rundeck
        MYSQL_USER: rundeck
        MYSQL_PASSWORD: 641949548825f1f8c51d5f547ab88faa
        MYSQL_RANDOM_ROOT_PASSWORD : 'true'
    volumes:
        - ./volume/mysql:/var/lib/mysql
rundeck:
    build: .
    environment:
        MYSQL_DATABASE: rundeck
        MYSQL_USER: rundeck
        MYSQL_PASSWORD: 641949548825f1f8c51d5f547ab88faa
        HOST_RUNDECK: localhost
        SERVER_URL: https://localhost:4443
        PASSWORD: admin
    ports:
        - "4443:4443"
    links:
        - mysql
    volumes:
        - ./volume/etc:/etc/rundeck
        - ./volume/rundeck:/var/rundeck
        - ./volume/lib:/var/lib/rundeck
        - ./volume/log:/var/log/rundeck

```

* three commands ;)

```
git clone https://github.com/remijouannet/docker-rundeck.git
cd docker-rundeck
docker-compose up
```

after that juste access the web ui with the following link :
* https://localhost:4443/
* login per default (if the variable was not change) : admin / admin
