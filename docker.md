## Host Machine
```bash
docker pull ubuntu:16.04
docker run --name ubuntu_16_test -it -p 3306:3306 -p 80:80 ubuntu:16.04 /bin/bash

docker start ubuntu_16_test
docker exec -it ubuntu_16_test /bin/bash
```

## Docker Container
```bash
apt-get update
apt-get upgrade

# db mysql
apt-get install nano mysql-server

nano /etc/mysql/mysql.conf.d/mysqld.cnf
-> bind-address: 0.0.0.0

mysql -uroot -p
-> CREATE USER 'yaqing'@'localhost' IDENTIFIED BY 'yaqing';
-> GRANT ALL PRIVILEGES ON *.* TO 'monty'@'localhost' WITH GRANT OPTION;
-> CREATE USER 'yaqing'@'%' IDENTIFIED BY 'yaqing';
-> GRANT ALL PRIVILEGES ON *.* TO 'monty'@'%' WITH GRANT OPTION;

service mysql restart

# app nginx + gunicorn + flask
apt-get install nginx supervisor python-pip python-virtualenv
pip install pip -U
mkdir /home/xxx
cd /home/xxx
virtualenv .env
source .env/bin/activate
pip install Flask

nano app.py
-> from flask import Flask
->
-> app = Flask(__name__)
->
-> @app.route('/')
-> def index():
->     return "Hello World"
->
-> if __name__ == '__main__':
->     app.run(debug=True)

pip install gunicorn
gunicorn -w 4 app:app &
nano /etc/nginx/conf.d/xxx.conf
-> server {
->    listen       80;
->    server_name  your_public_dnsname_here;
->
->    location / {
->        proxy_pass http://127.0.0.1:8000;
->    }
-> }

nano /etc/nginx/sites-enabled/default
-> comment everything in the default file

nginx -t
service nginx restart
```