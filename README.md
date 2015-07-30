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

```sql
select
  pes_codigo,
  pes_nome,
  pes_cidade
from
  pessoas
where
  pes_cidade = 'CANELINHA'
```

* Listar a emissão, descrição, código da pessoa e valor dos compromissos emitidos em 08/07/2015 para a pessoa 103454.

```sql
select
  comp_emissao,
  comp_descricao,
  pes_codigo,
  comp_vlrnominal
from
  compromissos
where
  comp_emissao = '08.07.2015' and
  pes_codigo = 103454
```

* Listar todas as pessoas modificadas pelo usuário 11.

```sql
select
  pes_codigo,
  pes_nome,
  pes_alt_usuario
from
  pessoas
where
  pes_alt_usuario = 11
```

* Listar todas as pessoas modifcadas no dia 27/05/2015.

```sql
select
  pes_codigo,
  pes_nome,
  pes_alt_tempo
from
  pessoas
where
  pes_alt_tempo >= '27.05.2015 00:00:00' and
  pes_alt_tempo <= '27.05.2015 23:59:59'
```

ou

```sql
select
  pes_codigo,
  pes_nome,
  pes_alt_tempo
from
  pessoas
where
  pes_alt_tempo >= '27.05.2015' and
  pes_alt_tempo < '28.05.2015'
```

### Apelidos

```sql
select
  p.pes_codigo,
  p.pes_nome
from
  pessoas p
```

ou

```sql
select
  pessoas.pes_codigo,
  pessoas.pes_nome
from
  pessoas
```

### Join

```sql
select
  p.pes_codigo,
  p.pes_nome,
  p.cid_codigo,
  c.cid_nome,
  c.uf_codigo
from
  pessoas p
  join
    cidades c
  on
    p.cid_codigo = c.cid_codigo
```

```sql
select
  g.grup_codigo,
  g.grup_nome,
  s.subg_codigo,
  s.subg_nome
from
  subgrupos s
  join
    grupos g
  on
    s.grup_codigo = g.grup_codigo
```

#### Desafios

* Listar o código do produto, nome do produto, código do subgrupo e nome do subgrupo dos produtos.

* Listar o código da venda, data de emissão e nome do cliente das vendas de fevereiro de 2015.






### What's next

* left join
* order by
* like
