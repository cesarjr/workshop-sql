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

```sql
select
  p.prod_codigo,
  p.prod_nome,
  s.subg_codigo,
  s.subg_nome
from
  produtos p
  join
    subgrupos s
  on
    p.subg_codigo = s.subg_codigo
```

* Listar o código da venda, data de emissão e nome do cliente das vendas de fevereiro de 2015.

```sql
select
  v.ven_codigo,
  v.ven_emissao,
  p.pes_nome
from
  vendas v
  join
    pessoas p
  on
    p.pes_codigo = v.pes_codigo_cliente
where
  v.ven_emissao >= '01.02.2015' and
  v.ven_emissao < '01.03.2015'
```

### Join: Ligando várias tabelas ao mesmo tempo

> Exemplo 1: A tabela de produtos liga-se as tabelas de cores e de tamanhos.
>
> Produtos -> Cores
>
> Produtos -> Tamanhos

```sql
select
  p.prod_codigo,
  p.prod_nome,
  c.cor_codigo,
  c.cor_nome,
  t.tam_codigo,
  t.tam_nome
from
  produtos p
  join
    cores c
  on
    c.cor_codigo = p.cor_codigo
  join
    tamanhos t
  on
    t.tam_codigo = p.tam_codigo
```

> Exemplo 2: A tabela de produtos liga-se a tabela de subgrupos. E a tabela de subgrupos liga-se a tabela de grupos.
>
> Produtos -> Subgrupos -> Grupos

```sql
select
  p.prod_codigo,
  p.prod_nome,
  s.subg_nome,
  g.grup_nome
from
  produtos p
  join
    subgrupos s
  on
    p.subg_codigo = s.subg_codigo
  join
    grupos g
  on
    s.grup_codigo = g.grup_codigo
```

#### Desafio

* Use a pesquisa acima e filtre pelo grupo 1.

* Liste a emissão da venda, o nome do cliente, o nome do produto e a quantidade do produto vendido para as vendas emitidas no mês de 04/2015.

> Dica:
>
> vendas -> pessoas
>
> vendas -> vendas_itens
>
> vendas_itens -> produtos

```sql
select
  v.ven_emissao,
  p.pes_nome,
  vi.venit_quantidade,
  pr.prod_nome
from
  vendas v
  join
    pessoas p
  on
    v.pes_codigo_cliente = p.pes_codigo
  join
    vendas_itens vi
  on
    v.ven_codigo = vi.ven_codigo
  join
    produtos pr
  on
    vi.prod_codigo = pr.prod_codigo
where
  v.ven_emissao >= '01.04.2015' and
  v.ven_emissao < '01.05.2015'
```

### Order by

```sql
select
  p.prod_codigo,
  p.prod_nome
from
  produtos p
order by
  p.prod_codigo

select
  c.cor_codigo,
  c.cor_nome
from
  cores c
order by
  c.cor_codigo desc
```

```sql
select
  v.ven_emissao,
  v.pes_codigo_cliente,
  p.pes_nome
from
  vendas v
  join
    pessoas p
  on
    v.pes_codigo_cliente = p.pes_codigo
order by
  p.pes_nome, v.ven_emissao desc
```

#### Desafio

* Listar o código e o nome do produto. Ordenar pelo nome de forma descendente.

* Listar o código e o nome da pessoa, a cidade e a uf (vindas da tabela de cidades) e ordenar primeiro pela uf e depois pela cidade.

* Listar quem nasceu no ano de 1978.

* Listar os itens orçados cancelados. Os campos devem ser o código do cliente, o nome do ciente, o código do produto, nome do produto, quantidade orçada.

* Liste a árvore de operações: código do centro, nome do centro, código do grupo financeiro, nome do grupo financeiro, código da categoria, nome da categoria, código da subcategoria, nome da subcategoria, código da operação, nome da operação. A ordenação deve ser por: nome do centro, nome do grupo, nome da categoria, nome da subcategoria e nome da operação.

```sql
select
  o.cen_codigo,
  cen.cen_nome,
  o.gruf_codigo,
  gruf.gruf_nome,
  o.cat_codigo,
  cat.cat_nome,
  o.subc_codigo,
  subc.subc_nome,
  o.ope_codigo,
  o.ope_nome
from
  operacoes o
  join
    centros_custos cen
  on
    o.cen_codigo = cen.cen_codigo
  join
    grupos_financeiros gruf
  on
    o.gruf_codigo = gruf.gruf_codigo
  join
    categorias cat
  on
    o.cat_codigo = cat.cat_codigo
  join
    subcategorias subc
  on
    o.subc_codigo = subc.subc_codigo
order by
  cen.cen_nome,
  gruf.gruf_nome,
  cat.cat_nome,
  subc.subc_nome,
  o.ope_nome
```

### Count

* Quantas pessoas temos no banco de dados?

```sql
/* O sistema contará a quantidade    */
/* de p.pes_codigo que ele encontrar */
/* no banco de dados.                */

select
  count(p.pes_codigo)
from
  pessoas p
```

* Quantos produtos temos no banco de dados?
```sql
select
  count(p.prod_nome)
from
  produtos p
```

#### Desafios

* Quantas cores temos cadastradas no sistema?
* Quantos produtos da cor "ABACATE" temos no sistema?
* Quantas pessoas temos no sistema que são do sexo masculino e que são clientes?
* Quantas pessoas temos no sistema que são do sexo feminino e que são clientes?
* Quantos fornecedores temos cadastrados no sistema?

### Campos calculados

Você pode fazer contas no seu select. Veja só:

```sql
select
  p.prod_codigo,
  p.prod_codigo + 10 codigo_soma_10,
  p.prod_codigo * 2 codigo_vezes_2,
  ((p.prod_codigo * 3)+5)/2 conta_louca
  (p.prod_codigo * p.prod_codigo) produto_ao_quadrado
from
  produtos p
```

#### Desafio

* Listar o nome do produto, a quantidade, o valor unitário (preço de venda) e o valor total de cada item vendido em 28/05/2015. Nomeie os campos para quantidade, unitario e total respectivamente. Ordene do maior valor total para o menor. Dica: o valor total = quantidade * valor unitário.

### Sum, max e min

```sql
select
  max(p.prod_codigo) maior_codigo,
  min(p.prod_codigo) menor_codigo,
  sum(p.prod_codigo) soma_dos_codigos,
  count(p.prod_codigo) quantidade_de_codigos
from
  produtos p
```

#### Desafio
* Qual foi o valor total vendido em 28/05/2015?
* Quantas vendas canceladas ocorreram entre 05/04/2015 e 13/04/2015?
* Qual o produto mais caro do cadastro?
* Qual o produto mais barato do cadastro?
* Quantas parcelas a receber existem no sistema?
* Qual o valor total a receber?
* Qual o valor total a pagar?
* Quanto for recebido em janeiro de 2014?

### What's next

* left join
* like
* group by
  * count
  * sum
  * max
  * min
* subselect
* select from select
* extract (data)
* order by por número do campo
