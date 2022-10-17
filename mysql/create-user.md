## Create User with All privileges


Entrar por consola a al admin de mysql:


```sh
# mysql -uroot -p
# use mysql;

CREATE USER 'user'@'%' IDENTIFIED BY 'password';
GRANT ALL PRIVILEGES ON * . * TO 'user'@'%';
GRANT GRANT OPTION ON *.* TO 'user'@'%';
FLUSH PRIVILEGES;
```