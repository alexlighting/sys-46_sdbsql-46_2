# Домашнее задание к занятию "`Работа с данными (DDL/DML)`" - `Деркачев Александр`


## Задание 1
```SQL
CREATE USER 'sys_temp'@'localhost' IDENTIFIED BY 'password';
```
```SQL
select * from mysql.user;
```
   ![Список пользователей MySQL](/img/user_list.png)

```SQL
GRANT ALL PRIVILEGES ON *.* TO 'sys_temp'@'localhost';
SELECT * FROM mysql.user;
```
   ![Список пользователей MySQL](/img/user_list_2.png)


### ER-Диаграмма
   ![ER-диаграмма базы Sakil](/img/sakila.png)
   
## Задание 2 Список таблиц базы Sakila

|Таблица|PrimaryKey|
|---|---|---|
|Actor|Actor_id|
|Address|Address_id|
|Category|Category_id|
|city|city_id|
|country|country_id|
|customer|customer_id|
|film|film_id|
|film_actor|actor_id, film_id|
|film_category|film_id, category_id|
|film_text|film_id|
|inventory|inventory_id|
|language|language_id|
|payment|payment_id|
|rental|rental_id|
|staff|staff_id|
|store|store_id|

## Задание 3 Удаление прав доступа

С этим заданием возникли сложности, из-за чего я не смог разобраться, ошибки в запросе я не нашел, но резульат выполнения странный. 
Началоссь все с того что у пользователя sys_temp не было прав на БД Sakila, ее я разворачивал уже после того как установил права пользователю, поэтому предположив что на новую БД права ему автоматом не подтянулись я добавил эти права явно

```SQL
GRANT ALL PRIVILEGES ON sakila.* TO 'sys_temp'@'localhost';
```
После этого я убрал права на добалвение, изменение и удаление

```SQL
REVOKE INSERT, Update, DELETE ON sakila.* FROM 'sys_temp'@'localhost';
```
Команда отработала без ошибок
 ![Результат выполнения команды](/img/revoke_1.png)

 Однако когда я посмотрел средствами DBeaver состояние прав для sys_temp то увидел следующую картину

 ![Результат выполнения команды](/img/revoke_2.png)

 Принудительное обновление привилегий 
 ```SQL
 FLUSH PRIVILEGES;
 ```
 ситуацию не изменило. 

## Dump всех команд
```SQL
CREATE USER 'sys_temp'@'localhost' IDENTIFIED BY 'password';

FLUSH PRIVILEGES;

select * from mysql.user;


GRANT ALL PRIVILEGES ON *.* TO 'sys_temp'@'localhost';

ALTER USER 'sys_temp'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';

GRANT ALL PRIVILEGES ON sakila.* TO 'sys_temp'@'localhost';

REVOKE INSERT, Update, DELETE ON sakila.* FROM 'sys_temp'@'localhost';
```
