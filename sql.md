

postgres=# \! chcp 1251
Текущая кодовая страница: 1251
postgres=# \c skypro
Вы подключены к базе данных "skypro" как пользователь "postgres".
skypro=# CREATE TABLE city(
skypro(# city_id BIGSERIAL NOT NULL PRIMARY KEY,
skypro(# city_name VARCHAR(120)
skypro(# );
CREATE TABLE

skypro=# ALTER TABLE hw_sql
skypro-# ADD city_id INT;
ALTER TABLE
skypro=# ALTER TABLE hw_sql ADD FOREIGN KEY (city_id) REFERENCES city (city_id);
ALTER TABLE
skypro=# INSERT INTO city (city_name)
skypro-# VALUES ('Brest'),('Minsk'),('Pinsk'),('Homel'),('Vitebsk');
INSERT 0 5
skypro=# SELECT*from city;
city_id | city_name
---------+-----------
1 | Brest
2 | Minsk
3 | Pinsk
4 | Homel
5 | Vitebsk
(5 строк)


skypro=# SELECT*from hw_sql;
id | first_name | last_name | gender | age | city_id
----+------------+-----------+--------+-----+---------
3 | Romashka   | Lesya     | F      |  42 |
5 | Byk        | DIMA      | M      |  23 |
2 | RAK        | DIMA      | M      |  25 |
1 | Hyk        | IRA       | F      |  67 |
4 | SHPAK      | IRA       | F      |  55 |
(5 строк)


skypro=# UPDATE hw_sql SET city_id=id;
UPDATE 5


skypro=# SELECT first_name AS Имя, last_name AS Фамилия, city_name AS Город
skypro-# FROM hw_sql
skypro-# INNER JOIN city
skypro-# ON hw_sql.city_id=city.city_id;
Имя    | Фамилия |  Город
----------+---------+---------
Byk      | DIMA    | Vitebsk
RAK      | DIMA    | Minsk
Hyk      | IRA     | Brest
SHPAK    | IRA     | Homel
Romashka | Lesya   | Pinsk
(5 строк)


skypro=# INSERT INTO city (city_name)
skypro-# VALUES ('Hlobin');
INSERT 0 1
skypro=# SELECT*from city;
city_id | city_name
---------+-----------
1 | Brest
2 | Minsk
3 | Pinsk
4 | Homel
5 | Vitebsk
6 | Hlobin
(6 строк)



skypro=# SELECT city_name AS Город, first_name AS Имя, last_name AS Фамилия
skypro-# FROM hw_sql
skypro-# FULL JOIN city
skypro-# ON hw_sql.city_id=city.city_id;
Город  |   Имя    | Фамилия
---------+----------+---------
Vitebsk | Byk      | DIMA
Minsk   | RAK      | DIMA
Brest   | Hyk      | IRA
Homel   | SHPAK    | IRA
Pinsk   | Romashka | Lesya
Hlobin  |          |
(6 строк)


skypro=# SELECT first_name AS Имя,city_name AS Город
skypro-# FROM hw_sql
skypro-# FULL JOIN city
skypro-# ON hw_sql.city_id=city.city_id;
Имя    |  Город
----------+---------
Byk      | Vitebsk
RAK      | Minsk
Hyk      | Brest
SHPAK    | Homel
Romashka | Pinsk
| Hlobin
(6 строк)



skypro=# SELECT first_name AS Имя,city_name AS Город
skypro-# FROM city
skypro-# CROSS JOIN hw_sql;
Имя    |  Город
----------+---------
Byk      | Brest
RAK      | Brest
Hyk      | Brest
SHPAK    | Brest
Romashka | Brest
Byk      | Minsk
RAK      | Minsk
Hyk      | Minsk
SHPAK    | Minsk
Romashka | Minsk
Byk      | Pinsk
RAK      | Pinsk
Hyk      | Pinsk
SHPAK    | Pinsk
Romashka | Pinsk
Byk      | Homel
RAK      | Homel
Hyk      | Homel
SHPAK    | Homel
Romashka | Homel
Byk      | Vitebsk
RAK      | Vitebsk
Hyk      | Vitebsk
SHPAK    | Vitebsk
Romashka | Vitebsk
Byk      | Hlobin
RAK      | Hlobin
Hyk      | Hlobin
SHPAK    | Hlobin
Romashka | Hlobin
(30 строк)


