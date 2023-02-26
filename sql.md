
postgres=# \! chcp 1251
Текущая кодовая страница: 1251
postgres=# \c skypro
Вы подключены к базе данных "skypro" как пользователь "postgres".
skypro=# insert into hw_sql(
skypro(# first_name, last_name, gender, age)
skypro-# VALUES ('SHPAK','IRA ', 'F', 55);
INSERT 0 1
skypro=# insert into hw_sql(
skypro(# first_name, last_name, gender, age)
skypro-# VALUES ('Byk',' Vania', 'M', 23);
INSERT 0 1
skypro=# insert into hw_sql(
skypro(# first_name, last_name, gender, age)
skypro-# VALUES ('Romashka','Lesya','F',42);
INSERT 0 1
skypro=# select first_name AS Фамилия,
skypro-# last_name AS Имя
skypro-# FROM hw_sql;
Фамилия  |  Имя
----------+--------
RAK      | DIMA
Hyk      | Olia
SHPAK    | IRA
Byk      |  Vania
Romashka | Lesya
(5 строк)

skypro=# SELECT * FROM hw_sql
skypro-# WHERE age>30 AND age<50;
id | first_name | last_name | gender | age
----+------------+-----------+--------+-----
6 | Romashka   | Lesya     | F      |  42
(1 строка)

skypro=# SELECT * FROM hw_sql
skypro-# WHERE age<30 OR age>50;
id | first_name | last_name | gender | age
----+------------+-----------+--------+-----
2 | RAK        | DIMA      | M      |  25
1 | Hyk        | Olia      | F      |  67
4 | SHPAK      | IRA       | F      |  55
5 | Byk        |  Vania    | M      |  23
(4 строки)

skypro=# SELECT * FROM hw_sql
skypro-# ORDER BY first_name DESC;
id | first_name | last_name | gender | age
----+------------+-----------+--------+-----
4 | SHPAK      | IRA       | F      |  55
6 | Romashka   | Lesya     | F      |  42
2 | RAK        | DIMA      | M      |  25
1 | Hyk        | Olia      | F      |  67
5 | Byk        |  Vania    | M      |  23
(5 строк)

skypro=# SELECT * FROM hw_sql
skypro-# WHERE CHAR_LENGTH(last_name)>4;
id | first_name | last_name | gender | age
----+------------+-----------+--------+-----
2 | RAK        | DIMA      | M      |  25
5 | Byk        |  Vania    | M      |  23
6 | Romashka   | Lesya     | F      |  42
(3 строки)


TASK_2;


skypro=# UPDATE hw_sql SET last_name='DIMA' where id=5;
UPDATE 1
skypro=# UPDATE hw_sql SET last_name='IRA' where id=1;
UPDATE 1
skypro=# SELECT * FROM hw_sql;
id | first_name | last_name | gender | age
----+------------+-----------+--------+-----
4 | SHPAK      | IRA       | F      |  55
6 | Romashka   | Lesya     | F      |  42
5 | Byk        | DIMA      | M      |  23
2 | RAK        | DIMA      | M      |  25
1 | Hyk        | IRA       | F      |  67
(5 строк)

skypro=# UPDATE hw_sql SET last_name='IRA' where id=4;
UPDATE 1
skypro=# SELECT last_name AS Имя,
skypro-# COUNT(last_name) AS Cуммарный_возраст
skypro-# FROM hw_sql
skypro-# GROUP BY Имя;
Имя  | cуммарный_возраст
-------+-------------------
Lesya |                 1
DIMA  |                 2
IRA   |                 2
(3 строки)

skypro=# SELECT  last_name, age
skypro-# FROM hw_sql
skypro-# WHERE age=(
skypro(# SELECT MIN(age)
skypro(# FROM hw_sql
skypro(# );
last_name | age
-----------+-----
DIMA      |  23
(1 строка)

skypro=# SELECT last_name AS Имя, age AS Самый_максимальный_возраст
skypro-#
skypro-# FROM hw_sql
skypro-# WHERE NOT last_name='Lesya'
skypro-# ORDER BY Имя, Самый_максимальный_возраст ASC;
Имя  | Самый_максимальный_возраст
------+----------------------------
DIMA |                         23
DIMA |                         25
IRA  |                         55
IRA  |                         67
(4 строки)
