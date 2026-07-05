# Расширенные возможности SQL

## Задание 1

Задание 1

Одним запросом получите информацию о магазине, в котором обслуживается более 300 покупателей, и выведите в результат следующую информацию:

 * фамилия и имя сотрудника из этого магазина;
 * город нахождения магазина;
 * количество пользователей, закреплённых в этом магазине.

## Решение
```
SELECT
    staff.last_name AS 'Last name',
    staff.first_name AS 'First name',
    city.city AS 'City store',
    COUNT(customer.customer_id) AS 'Buyers'
FROM store 
JOIN staff ON staff.store_id = store.store_id
JOIN customer ON customer.store_id = store.store_id
JOIN address ON address.address_id = store.address_id
JOIN city ON city.city_id = address.city_id
GROUP BY store.store_id, staff.staff_id, staff.last_name, staff.first_name, city.city
HAVING COUNT(customer.customer_id) > 300;
```
```
+-----------+------------+------------+--------+
| Last name | First name | City store | Buyers |
+-----------+------------+------------+--------+
| Hillyer   | Mike       | Lethbridge |    326 |
+-----------+------------+------------+--------+
1 row in set (0.00 sec)
```
![task_3_1.png](screenshots/task_3_1.png)

## Задание 2

Получите количество фильмов, продолжительность которых больше средней продолжительности всех фильмов.

## Решение
```
SELECT COUNT(*) AS 'Number of films'
FROM film
WHERE length > (SELECT AVG(length) FROM film);
```
```
+-----------------+
| Number of films |
+-----------------+
|             489 |
+-----------------+
1 row in set (0.00 sec)
```
![task_3_2.png](screenshots/task_3_2.png)

## Задание 3