<a name="format-nothing"></a>

<span id="lala"></span>

<h1 id="nothing">Nothing</h1>

Служебный тип данных для [массивов](array.md#data_type-array), объявленных без типа.

```bash
:) SELECT toTypeName(array())

SELECT toTypeName([])

┌─toTypeName(array())─┐
│ Array(Nothing)      │
└─────────────────────┘

1 rows in set. Elapsed: 0.062 sec.
```

