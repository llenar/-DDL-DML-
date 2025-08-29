## Задание 1

1.1. Поднимите чистый инстанс MySQL версии 8.0+. Можно использовать локальный сервер или контейнер Docker.

1.2. Создайте учётную запись sys_temp.

1.3. Выполните запрос на получение списка пользователей в базе данных. (скриншот)

1.4. Дайте все права для пользователя sys_temp.

1.5. Выполните запрос на получение списка прав для пользователя sys_temp. (скриншот)

1.6. Переподключитесь к базе данных от имени sys_temp.

Для смены типа аутентификации с sha2 используйте запрос:
```
ALTER USER 'sys_test'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
```
1.7. По ссылке https://downloads.mysql.com/docs/sakila-db.zip скачайте дамп базы данных.

1.8. Восстановите дамп в базу данных.

1.9. При работе в IDE сформируйте ER-диаграмму получившейся базы данных. При работе в командной строке используйте команду для получения всех таблиц базы данных. (скриншот)

## Ответ 1

1.1. Поднимите чистый инстанс MySQL версии 8.0+. Можно использовать локальный сервер или контейнер Docker.

<img width="1129" height="426" alt="image" src="https://github.com/user-attachments/assets/25793e7d-0087-4429-84ec-c2a35f13626f" />

<img width="1065" height="307" alt="image" src="https://github.com/user-attachments/assets/7ded76ca-93a4-4772-b3da-b33c51025d3f" />

1.2. Создайте учётную запись sys_temp.

```
CREATE USER 'sys_temp'@'localhost' IDENTIFIED BY '1234567';
```

<img width="853" height="63" alt="image" src="https://github.com/user-attachments/assets/1144bdc2-351c-4eee-a802-bcbd17e9023e" />

1.3. Выполните запрос на получение списка пользователей в базе данных. (скриншот)

```
SELECT user FROM mysql.user;
```

<img width="410" height="296" alt="image" src="https://github.com/user-attachments/assets/bf8fdd8d-6cd0-41d9-8b92-4e14b4c6a668" />

1.4. Дайте все права для пользователя sys_temp.

```
GRANT ALL PRIVILEGES ON *.* TO 'sys_temp'@'localhost' WITH GRANT OPTION;
```

<img width="862" height="66" alt="image" src="https://github.com/user-attachments/assets/b350e9c1-dc3b-431c-aa39-36763506eb93" />

1.5. Выполните запрос на получение списка прав для пользователя sys_temp. (скриншот)

```
SELECT * FROM information_schema.user_privileges WHERE GRANTEE="'sys_temp'@'localhost'";
```

<img width="398" height="659" alt="image" src="https://github.com/user-attachments/assets/b02098fa-73fe-4e76-88e8-4061f377c8d8" />

1.6. Переподключитесь к базе данных от имени sys_temp.

```
SYSTEM mysql -u sys_temp -p
SELECT user();
```

<img width="572" height="349" alt="image" src="https://github.com/user-attachments/assets/66c1bcfc-4753-4b56-83fd-9117c6dc4515" />

1.7. По ссылке https://downloads.mysql.com/docs/sakila-db.zip скачайте дамп базы данных.

```
wget https://downloads.mysql.com/docs/sakila-db.zip
unzip sakila-db.zip
```
<img width="1199" height="344" alt="image" src="https://github.com/user-attachments/assets/672a9049-10d3-4abf-9a94-7a4156e0a770" />



1.8. Восстановите дамп в базу данных.

```
source /home/vboxuser/Рабочий стол/sakila-db/sakila-schema.sql
source /home/tverdyakov/sakila-db/sakila-data.sql
SHOW DATABASES;
```

<img width="709" height="452" alt="image" src="https://github.com/user-attachments/assets/b25b7d8c-9e56-4d18-9eb2-9d1478397230" />

<img width="608" height="431" alt="image" src="https://github.com/user-attachments/assets/63a1200d-88fc-4610-a9a7-c13fff1fc400" />

<img width="789" height="214" alt="image" src="https://github.com/user-attachments/assets/f32cac3b-a725-479c-8642-64105cea582e" />

1.9. При работе в IDE сформируйте ER-диаграмму получившейся базы данных. При работе в командной строке используйте команду для получения всех таблиц базы данных. (скриншот)

```
SHOW TABLES;
```

<img width="306" height="534" alt="image" src="https://github.com/user-attachments/assets/cb494a63-bafa-4d67-b54e-2a3e7ed0091f" />

<img width="1771" height="909" alt="image" src="https://github.com/user-attachments/assets/0559bf8d-9354-40d5-9534-f58d7c3cd0a0" />

## Задание 2

Составьте таблицу, используя любой текстовый редактор или Excel, в которой должно быть два столбца: в первом должны быть названия таблиц восстановленной базы, во втором названия первичных ключей этих таблиц. Пример: (скриншот/текст)

```
Название таблицы | Название первичного ключа
customer         | customer_id
```

## Ответ 2

```
SELECT TABLE_NAME, COLUMN_NAME FROM INFORMATION_SCHEMA.key_column_usage WHERE table_schema = 'sakila' AND CONSTRAINT_NAME = 'PRIMARY';
+---------------+--------------+
| TABLE_NAME    | COLUMN_NAME  |
+---------------+--------------+
| actor         | actor_id     |
| address       | address_id   |
| category      | category_id  |
| city          | city_id      |
| country       | country_id   |
| customer      | customer_id  |
| film          | film_id      |
| film_actor    | actor_id     |
| film_actor    | film_id      |
| film_category | film_id      |
| film_category | category_id  |
| film_text     | film_id      |
| inventory     | inventory_id |
| language      | language_id  |
| payment       | payment_id   |
| rental        | rental_id    |
| staff         | staff_id     |
| store         | store_id     |
+---------------+--------------+
```

<img width="900" height="465" alt="image" src="https://github.com/user-attachments/assets/fd80ef9d-c47c-4b66-acd9-2563be4ffa49" />

