# Задача 1
Информация о БД
```doctest
mysql> status
--------------
mysql  Ver 8.0.28 for Linux on x86_64 (MySQL Community Server - GPL)

Connection id:          10
Current database:
Current user:           user@localhost
SSL:                    Not in use
Current pager:          stdout
Using outfile:          ''
Using delimiter:        ;
Server version:         8.0.28 MySQL Community Server - GPL
Protocol version:       10
Connection:             Localhost via UNIX socket
Server characterset:    utf8mb4
Db     characterset:    utf8mb4
Client characterset:    latin1
Conn.  characterset:    latin1
UNIX socket:            /var/run/mysqld/mysqld.sock
Binary data as:         Hexadecimal
Uptime:                 5 min 55 sec

Threads: 2  Questions: 5  Slow queries: 0  Opens: 117  Flush tables: 3  Open tables: 36  Queries per second avg: 0.014
--------------
```

Нашлась одна запись
```doctest
mysql> select count(*) from orders where price > 300;
+----------+
| count(*) |
+----------+
|        1 |
+----------+
1 row in set (0.00 sec)
```

# Задача 2
```doctest
mysql> select * from INFORMATION_SCHEMA.USER_ATTRIBUTES where user = "test";
+------+------+----------------------------------------+
| USER | HOST | ATTRIBUTE                              |
+------+------+----------------------------------------+
| test | %    | {"name": "James", "surname": "Pretty"} |
+------+------+----------------------------------------+
1 row in set (0.00 sec)
```

# Задача 3
Изначальный движок InnoDB
```doctest
mysql> SELECT TABLE_NAME,
    ->        ENGINE
    -> FROM   information_schema.TABLES
    -> WHERE  TABLE_SCHEMA = 'test_db';
+------------+--------+
| TABLE_NAME | ENGINE |
+------------+--------+
| orders     | InnoDB |
+------------+--------+
1 row in set (0.00 sec)
```

Переключение движков
```doctest
mysql> alter table orders ENGINE=MyISAM;
Query OK, 5 rows affected (0.08 sec)
Records: 5  Duplicates: 0  Warnings: 0

mysql> alter table orders ENGINE=InnoDB;
Query OK, 5 rows affected (0.06 sec)
Records: 5  Duplicates: 0  Warnings: 0
```

# Задача 4
Добавленные параметры
```doctest
innodb_flush_log_at_trx_commit = 2
innodb_file_per_table = ON
innodb_log_buffer_size = 1M
innodb_buffer_pool_size = 300M
innodb_log_file_size = 100M
```