# What is ClickHouse?

ClickHouse это столбцовая база данных.

В "нормальной" базе:

Row | WatchID | JavaEnable | Title | GoodEvent | EventTime
--- | --- | --- | --- | --- | ---
#0 | 89354350662 | 1 | Investor Relations | 1 | 2016-05-18 05:19:20
#1 | 90329509958 | 0 | Contact us | 1 | 2016-05-18 08:10:20
#2 | 89953706054 | 1 | Mission | 1 | 2016-05-18 07:38:00
#N | ... | ... | ... | ... | ...

Другими словами...

Примеры: MySQL....
{: .grey }

В столбцовой базе...:

Row: | #0 | #1 | #2 | #N
--- | --- | --- | --- | ---
WatchID: | 89354350662 | 90329509958 | 89953706054 | ...
JavaEnable: | 1 | 0 | 1 | ...
Title: | Investor Relations | Contact us | Mission | ...
GoodEvent: | 1 | 1 | 1 | ...
EventTime: | 2016-05-18 05:19:20 | 2016-05-18 08:10:20 | 2016-05-18 07:38:00 | ...

Эти примеры...

Примеры DBMS: Vertica, Paraccel (Actian Matrix and Amazon Redshift), Sybase IQ, Exasol, Infobright, InfiniDB, MonetDB (VectorWise and Actian Vector), LucidDB, SAP HANA, Google Dremel, Google PowerDrill, Druid, and kdb+.
{: .grey }

## Ключевые особенности

- раз
- два
- три

![Row-oriented](../en/images/row_oriented.gif#)

Example

<details>
<p></p>
<pre>$ clickhouse-client
ClickHouse client version 0.0.52053.
Connecting to localhost:9000.
Connected to ClickHouse server version 0.0.52053.
</pre></details>

:) SELECT CounterID, count() FROM hits GROUP BY CounterID ORDER BY count() DESC LIMIT 20

:) SELECT CounterID, count() FROM hits GROUP BY CounterID ORDER BY count() DESC LIMIT 20

┌─CounterID─┬──count()─┐
│    114208 │ 56057344 │
│    115080 │ 51619590 │
│      3228 │ 44658301 │
│     38230 │ 42045932 │
│    145263 │ 42042158 │
│     91244 │ 38297270 │
│    154139 │ 26647572 │
│    150748 │ 24112755 │
│    242232 │ 21302571 │
│    338158 │ 13507087 │
│     62180 │ 12229491 │
│     82264 │ 12187441 │
│    232261 │ 12148031 │
│    146272 │ 11438516 │
│    168777 │ 11403636 │
│   4120072 │ 11227824 │
│  10938808 │ 10519739 │
│     74088 │  9047015 │
│    115079 │  8837972 │
│    337234 │  8205961 │
└───────────┴──────────┘

20 rows in set. Elapsed: 0.153 sec. Processed 1.00 billion rows, 4.00 GB (6.53 billion rows/s., 26.10 GB/s.)

:)

### CPU

```
#some_code_block
```

[cross_link](./operations/table_engines/merge_tree.md#merge_tree)
[cross_link](../a/b.md#b)
[external_link](https://wiki.org)
