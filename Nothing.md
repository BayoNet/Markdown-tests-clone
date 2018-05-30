<a name="format-nothing"></a>

# Nothing

Служебный тип данных для [массивов](array.md#data_type-array), объявленных без типа.

```bash
:) SELECT toTypeName(array())

SELECT toTypeName([])

┌─toTypeName(array())─┐
│ Array(Nothing)      │
└─────────────────────┘

1 rows in set. Elapsed: 0.062 sec.
```
