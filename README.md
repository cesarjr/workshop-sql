# Firebird SQL - Mini workshop

### SELECT

```sql
select
  *
from
  pessoas
```

```sql
select
  pes_codigo,
  pes_nome
from
  pessoas
```

```sql
select
  pes_codigo codigo,
  pes_nome nome
from
  pessoas
```

### WHERE

```sql
select
  *
from
  pessoas
where
  pes_codigo = 431
```

```sql
select
  *
from
  pessoas
where
  pes_codigo > 600
```

```sql
select
  *
from
  pessoas
where
  pes_codigo > 600 and
  pes_codigo < 1000
```

```sql
select
  *
from
  pessoas
where
  pes_codigo in (431, 1092, 866)
```

```sql
select
  *
from
  pessoas
where
  pes_codigo = 431 or
  pes_codigo = 1092 or
  pes_codigo = 866
```

```sql
select
  ven_codigo,
  ven_emissao
from
  vendas
where
  ven_emissao >= '01.02.2015' and
  ven_emissao <= '20.02.2015'
```
