## mysqldump - Guía práctica


Entrar por consola a al admin de mysql:


```sh
# mysql -uroot -p
# use mysql;

mysqldump [opciones] nombre_bd [nombre_tabla1 nombre_tabla2 ...] > respaldo.sql
mysqldump [opciones] --databases nombre_bd1 nombre_bd2 > respaldo.sql
mysqldump [opciones] --all-databases > respaldo.sql
```
Ejemplo:


```
mysqldump -root -p --all-databases > respaldo.YYYYMMDD.sql

```


Respaldo de una sola base de datos completa
```
mysqldump clientes > clientes.sql   
```
Respaldo de una sola base de datos con dos tablas
```
mysqldump clientes saldos facturas  > clientes.sql   
```
Respaldo completo de base de datos clientes y ventas
```
mysqldump --databases clientes ventas > respaldo_cli_ven_sep_2011.sql   
```

Respaldamos la base de datos clientes pero ignoramos las tablas 'temporal' y 'basura' (Obligatorio indicar base.tabla)

```
mysqldump clientes --ignore-table=clientes.temporal --ignore-table=clientes.basura > respaldo_clientes_2011.sql   
```
Respaldo completo de todas las bases de datos
```
mysqldump --all-databases > respaldo_full_sep_2011.sql   
```
Si se tiene contraseña (como debe ser) se indica usuario y que pregunte por el password
```
mysqldump -u root -p --all-databases  > respaldo_full_sep_2011.sql   
```
No muy buena idea, pero se puede indicar el password directamente, además nos aseguramos que se indiquen las opciones por defecto más comunes
```
mysqldump -u root -psecreto --all-databases --opt  > respaldo_full_sep_2011.sql   
```
Respaldo de una base de datos transaccional tipo InnoDB o BDB asegurando su consistencia
```
mysqldump -u root -p --single-transaction --quick ventas  > respaldo_ventas_2011.sql   
```
Todas las bases de datos del host 192.168.0.100 y agregamos los procedemientos almacenados que sean respaldados también.
```
mysqldump -h 192.168.1.100 -u root -p --routines --all-databases  > respaldo_ventas_2011.sql   
```
Respaldo de las bases de datos clientes y pedidos, con todas las opciones específicas para re-crear las tablas, además añadimos 'drop database' para asegurarnos que en la restauración se creé desde cero el respaldo, además ignoramos errores..
```
mysqldump -u root -p --create-options --add-drop-database --force --databases clientes pedidos  > respaldo_ven_ped_2011.sql   
```
Respaldo completo de un servidor MySQL maestro en replicación, indicando en el respaldo la posición para sincronización con servidores esclavos, además añadimos insertar completos que incluyen los nombres de columnas en sentencias INSERT
```
mysqldump -u root --password=secreto --all-databases --master-data  --complete-insert  > respaldo_2011.sql   
```
Respaldamos solo el esquema de clientes sin registros
```
mysqldump --no-data clientes > respaldo_esquema_clientes_2011.sql   
```
Se produce una salida compatible para restaurar la base de datos en Oracle
```
mysqldump --compatible=oracle --databases clientes > respaldo_clientes_oracle_2011.sql   
```