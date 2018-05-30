<a name="data_type-nullable"></a>

# Nullable(TypeName)

Позволяет хранить в таблице значение `NULL` вместо значения типа `TypeName`.

Поле типа `Nullable` нельзя включать в индексы.

## Пример

```
:) CREATE TABLE t_null(x Int8, y Nullable(Int8)) engine TinyLog

CREATE TABLE t_null
(
    x Int8,
    y Nullable(Int8)
)
ENGINE = TinyLog

Ok.

0 rows in set. Elapsed: 0.012 sec.

:) INSERT INTO t_null VALUES (1, NULL)

INSERT INTO t_null VALUES

Ok.

1 rows in set. Elapsed: 0.007 sec.

:) SELECT x+y from t_null

SELECT x + y
FROM t_null

┌─plus(x, y)─┐
│         \N │
└────────────┘

1 rows in set. Elapsed: 0.009 sec.

```
