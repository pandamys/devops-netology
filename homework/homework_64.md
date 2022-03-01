# Задание 1
- вывода списка БД - \l
- подключения к БД - \c
- вывода списка таблиц - \dt
- вывода описания содержимого таблиц - \dt+
- выхода из psql - \q

# Задание 2
Берём строки относящиеся к нашей таблице и сортируем их по среднему в обратном порядке.
Получается столбец title
```doctest
test_database=# select * from pg_stats where tablename = 'orders' order by avg_width desc;
 schemaname | tablename | attname | inherited | null_frac | avg_width | n_distinct | most_common_vals | most_common_freqs |                                                                 histogram_bounds
                                                             | correlation | most_common_elems | most_common_elem_freqs | elem_count_histogram
------------+-----------+---------+-----------+-----------+-----------+------------+------------------+-------------------+--------------------------------------------------------------------------------------
-------------------------------------------------------------+-------------+-------------------+------------------------+----------------------
 public     | orders    | title   | f         |         0 |        16 |         -1 |                  |                   | {"Adventure psql time",Dbiezdmin,"Log gossips","Me and my bash-pet","My little databa
se","Server gravity falls","WAL never lies","War and peace"} |  -0.3809524 |                   |                        |
 public     | orders    | id      | f         |         0 |         4 |         -1 |                  |                   | {1,2,3,4,5,6,7,8}
                                                             |           1 |                   |                        |
 public     | orders    | price   | f         |         0 |         4 |     -0.875 | {300}            | {0.25}            | {100,123,499,500,501,900}
                                                             |   0.5952381 |                   |                        |
(3 rows)
```

# Задание 3
Создаём таблицу на основе запроса
```doctest
test_database=# create table orders_1 as select * from orders where price > 499;
SELECT 3
test_database=# create table orders_2 as select * from orders where price <= 499;
SELECT 5
```

Избежать данной ситуации можно было создав изначально партиционную таблицу и на её части повесить условие CHECK, которое проверяло бы price по заданному условию.

# Задание 4
При создание таблицы в файле дампа, я бы поправил, что данный столбец имеет уникальные значения
```doctest
title character varying(80) NOT NULL UNIQUE,
```