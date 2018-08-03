## Host Machine
```bash
docker pull ubuntu:16.04
docker run --name ubuntu_16_test -it -p 3306:3306 -p 80:80 ubuntu:16.04 /bin/bash
```

## Docker Container
```bash
nano /etc/mysql/mysql.conf.d/mysqld.cnf
-> bind-address: 0.0.0.0

mysql -uroot -p
-> CREATE USER 'yaqing'@'localhost' IDENTIFIED BY 'yaqing';
-> GRANT ALL PRIVILEGES ON *.* TO 'monty'@'localhost' WITH GRANT OPTION;
-> CREATE USER 'yaqing'@'%' IDENTIFIED BY 'yaqing';
-> GRANT ALL PRIVILEGES ON *.* TO 'monty'@'%' WITH GRANT OPTION;
```