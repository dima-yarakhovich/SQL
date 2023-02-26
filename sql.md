postgres=# \! chcp 1251
Текущая кодовая страница: 1251
postgres=# \c skypro;
Вы подключены к базе данных "skypro" как пользователь "postgres".
skypro=# create table hw_sql(
skypro(# id BIGSERIAL NOT NULL PRIMARY KEY,
skypro(# first_name VARCHAR(50) NOT NULL,
skypro(# last_name VARCHAR(50) NOT NULL,
skypro(# gender VARCHAR(6) NOT NULL,
skypro(# age INT NOT NULL
skypro(# );
CREATE TABLE
skypro=# insert into hw_sql(
skypro(# first_name, last_name, gender, age)
skypro-# VALUES ('Byk',' Vania', 'M', 23);
INSERT 0 1
skypro=# insert into hw_sql(
skypro(# first_name, last_name, gender, age)
skypro-# VALUES ('RAK','DIMA ', 'M', 25);
INSERT 0 1
skypro=# insert into hw_sql(
skypro(# first_name, last_name, gender, age)
skypro-# VALUES ('SHPAK','IRA ', 'F', 55);
INSERT 0 1
skypro=# SELECT * FROM hw_sql;
id | first_name | last_name | gender | age
----+------------+-----------+--------+-----
1 | Byk        |  Vania    | M      |  23
2 | RAK        | DIMA      | M      |  25
3 | SHPAK      | IRA       | F      |  55
(3 строки)


skypro=# UPDATE hw_sql SET first_name='Hyk',last_name='Olia', gender='F',age=67 where id=1;
UPDATE 1
skypro=# SELECT * FROM hw_sql;
id | first_name | last_name | gender | age
----+------------+-----------+--------+-----
2 | RAK        | DIMA      | M      |  25
3 | SHPAK      | IRA       | F      |  55
1 | Hyk        | Olia      | F      |  67
(3 строки)


skypro=# DELETE FROM hw_sql where id=3;
DELETE 1
skypro=# SELECT * FROM hw_sql;
id | first_name | last_name | gender | age
----+------------+-----------+--------+-----
2 | RAK        | DIMA      | M      |  25
1 | Hyk        | Olia      | F      |  67
(2 строки)


