# JDBC

Allows ClickHouse to connect to external databases via JDBC.

To implement JDBC connection, ClickHouse uses the separate program `clickhouse-jdbc-bridge`. You should run it as a demon.

This engine supports the [Nullable](../../data_types/nullable.md) data type.

## Creating a Table

```
CREATE TABLE [IF NOT EXISTS] [db.]table_name [ON CLUSTER cluster]
(
    name1 [type1] [DEFAULT|MATERIALIZED|ALIAS expr1] [TTL expr1],
    name2 [type2] [DEFAULT|MATERIALIZED|ALIAS expr2] [TTL expr2],
    ...
    INDEX index_name1 expr1 TYPE type1(...) GRANULARITY value1,
    INDEX index_name2 expr2 TYPE type2(...) GRANULARITY value2
) ENGINE = ODBC()
[SETTINGS name=value, ...]
```

See the detailed description of [CREATE TABLE](../../query_language/create.md#create-table-query) query.

**Engine Parameters**


**Query clauses**

- `ENGINE` — Name and parameters of the engine. `ENGINE = ODBC()`. `ODBC` engine does not have parameters.

- `SETTINGS` — Additional parameters that control the behavior of the `MergeTree`:

    - `url` — Database URL.

        Format: `jdbc:<driver_name>://<host_name>:<port>/?user=<username>&password=<password>`.
        Example for MySQL: `jdbc:mysql://localhost:3306/?user=root&password=root`.

    - `schema` — .
    - `table` — Table name in the external database.

**Example of sections setting**

```
ENGINE ODBC() SETTINGS
```

## Peculiarities and recommendations

Recommendations for usage

## Example of Use

Example of interaction with MySQL:

```
mysql> CREATE TABLE `test`.`test` (
    ->   `int_id` INT NOT NULL AUTO_INCREMENT,
    ->   `int_nullable` INT NULL DEFAULT NULL,
    ->   `float` FLOAT NOT NULL,
    ->   `float_nullable` FLOAT NULL DEFAULT NULL,
    ->   `double` DOUBLE NOT NULL,
    ->   `double_nullable` DOUBLE NULL DEFAULT NULL,
    ->   `timestamp` TIMESTAMP NOT NULL,
    ->   `timestamp_nullable` TIMESTAMP NULL DEFAULT NULL,
    ->   `date` DATE NOT NULL,
    ->   `date_nullable` DATE NULL DEFAULT NULL,
    ->   PRIMARY KEY (`int_id`));
Query OK, 0 rows affected (0,09 sec)

mysql> insert into test (`int_id`, `float`, `double`, `timestamp`, `date`) VALUES (1,2,3, '2018-01-02 03:04:05', '2019-05-06');Query OK, 1 row affected (0,00 sec)

mysql> select * from test;
+--------+--------------+-------+----------------+--------+-----------------+---------------------+--------------------+------------+---------------+
| int_id | int_nullable | float | float_nullable | double | double_nullable | timestamp           | timestamp_nullable | date       | date_nullable |
+--------+--------------+-------+----------------+--------+-----------------+---------------------+--------------------+------------+---------------+
|      1 |         NULL |     2 |           NULL |      3 |            NULL | 2018-01-02 03:04:05 | NULL               | 2019-05-06 | NULL          |
+--------+--------------+-------+----------------+--------+-----------------+---------------------+--------------------+------------+---------------+
1 row in set (0,00 sec)
```

From clickhouse-client:

```
DESCRIBE TABLE jdbc('jdbc:mysql://localhost:3306/?user=root&password=root', 'test', 'test')

┌─name───────────────┬─type───────────────┬─default_type─┬─default_expression─┐
│ int_id             │ Int32              │              │                    │
│ int_nullable       │ Nullable(Int32)    │              │                    │
│ float              │ Float32            │              │                    │
│ float_nullable     │ Nullable(Float32)  │              │                    │
│ double             │ Float64            │              │                    │
│ double_nullable    │ Nullable(Float64)  │              │                    │
│ timestamp          │ DateTime           │              │                    │
│ timestamp_nullable │ Nullable(DateTime) │              │                    │
│ date               │ Date               │              │                    │
│ date_nullable      │ Nullable(Date)     │              │                    │
└────────────────────┴────────────────────┴──────────────┴────────────────────┘

10 rows in set. Elapsed: 0.031 sec.

SELECT *
FROM jdbc('jdbc:mysql://localhost:3306/?user=root&password=root', 'test', 'test')

┌─int_id─┬─int_nullable─┬─float─┬─float_nullable─┬─double─┬─double_nullable─┬───────────timestamp─┬─timestamp_nullable─┬───────date─┬─date_nullable─┐
│      1 │         ᴺᵁᴸᴸ │     2 │           ᴺᵁᴸᴸ │      3 │            ᴺᵁᴸᴸ │ 2018-01-02 03:04:05 │               ᴺᵁᴸᴸ │ 2019-05-06 │          ᴺᵁᴸᴸ │
└────────┴──────────────┴───────┴────────────────┴────────┴─────────────────┴─────────────────────┴────────────────────┴────────────┴───────────────┘

1 rows in set. Elapsed: 0.055 sec.
```
