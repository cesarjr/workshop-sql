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

#### Desafios

* Listar o código, o documento, o vencimento e o valor dos compromissos que vencem em março de 2015.

```sql
select
  comp_codigo,
  comp_documento,
  comp_vencimento,
  comp_vlrnominal
from
  compromissos
where
  comp_vencimento >= '01.03.2015' and
  comp_vencimento <= '31.03.2015'
```

* Listar todas as pessoas de CANELINHA.
* Listar a emissão, descrição, código da pessoa e valor dos compromissos emitidos em 08/07/2015 para a pessoa 103454.
* Listar todas as pessoas modificadas pelo usuário 11.
* Listar todas as pessoas modifcadas no dia 27/05/2015.
