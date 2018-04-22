---
title: Obtendo Informações de Outras Linhas no Mesmo Select
date: 2018-04-22 13:41:30
tags: 
    - SQL
    - DB
header-img: img/sql-next-rows.jpg
subtitle: Como saber o valor da linha anterior e da próxima
author: Humberto Machado
comments: true
permalink: sql-next-rows
---

# Obter Informações de Outras Linhas no Mesmo Select

Tendo um banco de dados para controle de despesas:

```sql
select * from despesas
```

| id  | valor   | descricao     
|-----|---------|----------------
| 1   | 12,00   | Almoço         
| 2   | 150,00  | Gasolina       
| 3   | 30,00   | Jantar         
| 4   | 61,00   | Conta de água  
| 5   | 180,00  | Conta de Luz   
| 6   | 100,00  | Internet    

Agora queremos exibir na mesma consulta, a despesa anterior, a atual e a próxima despesa do mês.
Para isso precisamos saber qual o valor da linha anterior e o valor da linha posterior do select.

Para isso precisamos fazer LEFT JOIN com a própria tabela. Veja o exemplo:

```sql
select 
    prev.descricao as DESPESA_ANTERIOR,
    main.descricao DESPESA_ATUAL,
    next.descricao as DESPESA_POSTERIOR
from 
    despesas main 
    left join despesas next on main.id = next.id - 1
    left join despesas prev on main.id = prev.id + 1
    order by main.dia;
```

Resultado:

|DESPESA_ANTERIOR | DESPESA_ATUAL | DESPESA_POSTERIOR
|-----------------|---------------|------------------
|(null)           |Almoço         |Gasolina
|Almoço           |Gasolina       |Jantar
|Gasolina         |Jantar         |Conta de água
|Jantar           |Conta de água  |Conta de luz
|Conta de água    |Conta de luz   |Internet
|Conta de luz     |Internet       |(null)
   
Para saber as despesas anterioes e posteriores ao dia 3:

```sql
select 
    prev.descricao as DESPESA_ANTERIOR,
    main.descricao DESPESA_ATUAL,
    next.descricao as DESPESA_POSTERIOR
from 
    despesas main 
    left join despesas next on main.id = next.id - 1
    left join despesas prev on main.id = prev.id + 1
    where
        main.dia = 3
    order by main.dia;
```

Resultado:

|DESPESA_ANTERIOR | DESPESA_ATUAL | DESPESA_POSTERIOR
|-----------------|---------------|------------------
|Gasolina         |Jantar         |Conta de água

