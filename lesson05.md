# PIVOT, UNPIVOT and MERGE in Oracle 21c and analogs in PostgreSQL

## Load example data for PIVOT

[Скрипты для загрузки данных](lesson05_sql.md)


## PIVOT in Oracle

### Example 1

```sql
select clients.lastname as lastname, payments.service_id as serv, payments.amount as amount
from scott.clients inner join scott.payments on clients.client_id=payments.client_id;
```

```sql
select lastname, Electric_sum/100, Gas_sum/100, ColdWater_sum/100, HotWater_sum/100 from (
select clients.lastname as lastname, payments.service_id as serv, payments.amount as amount
from scott.clients inner join scott.payments on clients.client_id=payments.client_id) 
PIVOT (sum(amount) sum for serv in (1 as Electric, 2 as Gas, 3 as ColdWater, 4 as HotWater));
--в названии столбца сверху добавляется суффикс из _ и алиаса аггрегирующего столбца
```

### Example 2

```sql
select clients.lastname as lastname, payments.service_id as serv, payments.amount as pmnt_amount, charges.amount chg_amount
from scott.clients inner join scott.payments on clients.client_id=payments.client_id
inner join scott.charges on clients.client_id=charges.client_id 
and payments.period=charges.period;
```

```sql
select lastname, Electric_pmntsum/100, Gas_pmntsum/100, ColdWater_pmntsum/100, HotWater_pmntsum/100,
Electric_chgsum/100, Gas_chgsum/100, ColdWater_chgsum/100, HotWater_chgsum/100 from (
select clients.lastname as lastname, payments.service_id as serv, payments.amount as pmnt_amount, charges.amount chg_amount
from scott.clients inner join scott.payments on clients.client_id=payments.client_id
inner join scott.charges on clients.client_id=charges.client_id 
and payments.period=charges.period)
PIVOT (sum(pmnt_amount) pmntsum, sum(chg_amount) chgsum  for serv in (1 as Electric, 2 as Gas, 3 as ColdWater, 4 as HotWater))
;
```

## CASE in Oracle

```sql
select lastname,
    sum(case when serv = 1 then amount else 0 end)/100 as Electic_sum,
    sum(case when serv = 2 then amount else 0 end)/100 as Gas_sum,
    sum(case when serv = 3 then amount else 0 end)/100 as ColdWater_sum,
    sum(case when serv = 4 then amount else 0 end)/100 as HotWater_sum
from 
(select clients.lastname as lastname, payments.service_id as serv, payments.amount as amount
from scott.clients inner join scott.payments on clients.client_id=payments.client_id)
group by lastname;
```

## CASE in PostgreSQL

### Example 1

```sql
select clients.lastname as lastname, payments.service_id as serv, payments.amount as amount
from clients inner join payments on clients.client_id=payments.client_id;
```

```sql
select lastname,
    sum(case when serv = 1 then amount else 0 end)/100 as Electic_sum,
    sum(case when serv = 2 then amount else 0 end)/100 as Gas_sum,
    sum(case when serv = 3 then amount else 0 end)/100 as ColdWater_sum,
    sum(case when serv = 4 then amount else 0 end)/100 as HotWater_sum
from 
(select clients.lastname as lastname, payments.service_id as serv, payments.amount as amount
from clients inner join payments on clients.client_id=payments.client_id) as t
group by lastname;
```
PS: В отличии от Oracle в PosgreSQL необходимо указать алиас вложенного запроса.

### Example 2

```sql
select clients.lastname as lastname, payments.service_id as serv, payments.amount as amount_pmnt, charges.amount as amount_chg
from clients inner join payments on clients.client_id=payments.client_id
 inner join charges  on clients.client_id=charges.client_id;
```

```sql
select lastname,
  	sum(case when serv = 1 then amount_pmnt else 0 end)/100 as Electic_sum_pmnt,
    sum(case when serv = 2 then amount_pmnt else 0 end)/100 as Gas_sum_pmnt,
    sum(case when serv = 3 then amount_pmnt else 0 end)/100 as ColdWater_sum_pmnt,
    sum(case when serv = 4 then amount_pmnt else 0 end)/100 as HotWater_sum_pmnt,
  	sum(case when serv = 1 then amount_chg else 0 end)/100 as Electic_sum_chg,
    sum(case when serv = 2 then amount_chg else 0 end)/100 as Gas_sum_chg,
    sum(case when serv = 3 then amount_chg else 0 end)/100 as ColdWater_sum_chg,
    sum(case when serv = 4 then amount_chg else 0 end)/100 as HotWater_sum_chg
from 
(select clients.lastname as lastname, payments.service_id as serv, payments.amount as amount_pmnt, charges.amount as amount_chg
from clients inner join payments on clients.client_id=payments.client_id
 inner join charges  on clients.client_id=charges.client_id) as t
group by lastname;
```

## Load example data for UNPIVOT

### Load in Oracle DB

```sql
create table scott.favorite_cities (client_name varchar2(100) not null, city_1 varchar2(100), city_2 varchar2(100), city_3 varchar2(100));
insert into scott.favorite_cities values ('Савельев','Москва','Сочи','Санкт-Петербург');
insert into scott.favorite_cities values ('Ветров','Омск','Новосибирск','Иркутск');
insert into scott.favorite_cities values ('Липатов','Санкт-Петербург','Иркутск','Сочи');
insert into scott.favorite_cities values ('Астафьев','Сочи','Новосибирск','Москва');
commit;
```

### Load in PostgreSQL

```sql
create table favorite_cities (client_name varchar(100) not null, city_1 varchar(100), city_2 varchar(100), city_3 varchar(100));
insert into favorite_cities values ('Савельев','Москва','Сочи','Санкт-Петербург');
insert into favorite_cities values ('Ветров','Омск','Новосибирск','Иркутск');
insert into favorite_cities values ('Липатов','Санкт-Петербург','Иркутск','Сочи');
insert into favorite_cities values ('Астафьев','Сочи','Новосибирск','Москва');
```

## UNPIVOT Oracle

```sql
select * from scott.favorite_cities;
```

```sql
select client_name, city, rank from scott.favorite_cities
UNPIVOT
(city for rank in (city_1 as 1, city_2 as 2, city_3 as 3));
```

## UNION ALL Oracle

```sql
with all_cities as 
(select client_name, city_1 as city, 1 as rank from scott.favorite_cities
 union all
 select client_name, city_2 as city, 2 as rank from scott.favorite_cities
 union all
 select client_name, city_3 as city, 3 as rank from scott.favorite_cities)
select * from all_cities order by client_name, rank;
```

## UNION ALL PostgreSQL

```sql
with all_cities as 
(select client_name, city_1 as city, 1 as rank from favorite_cities
 union all
 select client_name, city_2 as city, 2 as rank from favorite_cities
 union all
 select client_name, city_3 as city, 3 as rank from favorite_cities)
select * from all_cities order by client_name, rank;
```

## Настройки sqlplus для красивого вывода

```sql
SET PAGESIZE 1000
SET LINESIZE 200
col lastname format a10
col client_name format a15
col city format a15
col city_1 format a15
col city_2 format a15
col city_3 format a15
```


### Plans

#### Plan for PIVOT Oracle

```sql
explain plan for 
select lastname, Electric_sum/100, Gas_sum/100, ColdWater_sum/100, HotWater_sum/100 from (
select clients.lastname as lastname, payments.service_id as serv, payments.amount as amount
from scott.clients inner join scott.payments on clients.client_id=payments.client_id) 
PIVOT (sum(amount) sum for serv in (1 as Electric, 2 as Gas, 3 as ColdWater, 4 as HotWater));
```

```sql
SELECT * FROM TABLE(DBMS_XPLAN.DISPLAY(format => 'ALL'));
```

```sql
Plan hash value: 375224469
 
-----------------------------------------------------------------------------------------------
| Id  | Operation                     | Name          | Rows  | Bytes | Cost (%CPU)| Time     |
-----------------------------------------------------------------------------------------------
|   0 | SELECT STATEMENT              |               |       |       |     7 (100)|          |
|   1 |  HASH GROUP BY PIVOT          |               |     5 |   145 |     7  (29)| 00:00:01 |
|   2 |   MERGE JOIN                  |               |   120 |  3480 |     6  (17)| 00:00:01 |
|   3 |    TABLE ACCESS BY INDEX ROWID| PAYMENTS      |   120 |  1320 |     2   (0)| 00:00:01 |
|   4 |     INDEX FULL SCAN           | PAYMENTS_CLID |   120 |       |     1   (0)| 00:00:01 |
|*  5 |    SORT JOIN                  |               |     5 |    90 |     4  (25)| 00:00:01 |
|   6 |     TABLE ACCESS FULL         | CLIENTS       |     5 |    90 |     3   (0)| 00:00:01 |
-----------------------------------------------------------------------------------------------
```

#### Plan for CASE Oracle

```sql
explain plan for 
select lastname,
    sum(case when serv = 1 then amount else 0 end)/100 as Electic_sum,
    sum(case when serv = 2 then amount else 0 end)/100 as Gas_sum,
    sum(case when serv = 3 then amount else 0 end)/100 as ColdWater_sum,
    sum(case when serv = 4 then amount else 0 end)/100 as HotWater_sum
from 
(select clients.lastname as lastname, payments.service_id as serv, payments.amount as amount
from scott.clients inner join scott.payments on clients.client_id=payments.client_id)
group by lastname;
```

```sql
SELECT * FROM TABLE(DBMS_XPLAN.DISPLAY(format => 'ALL'));
```

```sql
Plan hash value: 1455264812
 
----------------------------------------------------------------------------------------------------------
| Id  | Operation                                | Name          | Rows  | Bytes | Cost (%CPU)| Time     |
----------------------------------------------------------------------------------------------------------
|   0 | SELECT STATEMENT                         |               |       |       |     6 (100)|          |
|   1 |  HASH GROUP BY                           |               |     5 |   365 |     6  (34)| 00:00:01 |
|   2 |   MERGE JOIN                             |               |     5 |   365 |     5  (20)| 00:00:01 |
|   3 |    TABLE ACCESS BY INDEX ROWID           | CLIENTS       |     5 |    90 |     2   (0)| 00:00:01 |
|   4 |     INDEX FULL SCAN                      | SYS_C006863   |     5 |       |     1   (0)| 00:00:01 |
|*  5 |    SORT JOIN                             |               |     5 |   275 |     3  (34)| 00:00:01 |
|   6 |     VIEW                                 | VW_GBC_5      |     5 |   275 |     2   (0)| 00:00:01 |
|   7 |      HASH GROUP BY                       |               |     5 |    55 |     2   (0)| 00:00:01 |
|   8 |       TABLE ACCESS BY INDEX ROWID BATCHED| PAYMENTS      |   120 |  1320 |     2   (0)| 00:00:01 |
|   9 |        INDEX FULL SCAN                   | PAYMENTS_CLID |   120 |       |     1   (0)| 00:00:01 |
----------------------------------------------------------------------------------------------------------
```

#### Plans CASE PostgreSQL

```sql
explain
select lastname,
    sum(case when serv = 1 then amount else 0 end)/100 as Electic_sum,
    sum(case when serv = 2 then amount else 0 end)/100 as Gas_sum,
    sum(case when serv = 3 then amount else 0 end)/100 as ColdWater_sum,
    sum(case when serv = 4 then amount else 0 end)/100 as HotWater_sum
from 
(select clients.lastname as lastname, payments.service_id as serv, payments.amount as amount
from clients inner join payments on clients.client_id=payments.client_id) as t
group by lastname;
```

```sql
HashAggregate  (cost=19.05..21.45 rows=120 width=250)
  Group Key: clients.lastname
  ->  Hash Join  (cost=13.82..16.35 rows=120 width=224)
        Hash Cond: (payments.client_id = clients.client_id)
        ->  Seq Scan on payments  (cost=0.00..2.20 rows=120 width=8)
        ->  Hash  (cost=11.70..11.70 rows=170 width=220)
              ->  Seq Scan on clients  (cost=0.00..11.70 rows=170 width=220)
```

#### Plan for UNPIVOT Oracle

```sql
explain plan for 
select client_name, city, rank from scott.favorite_cities
UNPIVOT
(city for rank in (city_1 as 1, city_2 as 2, city_3 as 3));
```

```sql
SELECT * FROM TABLE(DBMS_XPLAN.DISPLAY(format => 'ALL'));
```

```sql
Plan hash value: 638632602
 
---------------------------------------------------------------------------------------
| Id  | Operation           | Name            | Rows  | Bytes | Cost (%CPU)| Time     |
---------------------------------------------------------------------------------------
|   0 | SELECT STATEMENT    |                 |    12 |  1284 |     5   (0)| 00:00:01 |
|*  1 |  VIEW               |                 |    12 |  1284 |     5   (0)| 00:00:01 |
|   2 |   UNPIVOT           |                 |       |       |            |          |
|   3 |    TABLE ACCESS FULL| FAVORITE_CITIES |     4 |   264 |     3   (0)| 00:00:01 |
---------------------------------------------------------------------------------------
```

#### Plan for UNION Oracle

```sql
explain plan for
with all_cities as 
(select client_name, city_1 as city, 1 as rank from scott.favorite_cities
 union all
 select client_name, city_2 as city, 2 as rank from scott.favorite_cities
 union all
 select client_name, city_3 as city, 3 as rank from scott.favorite_cities)
select * from all_cities order by client_name, rank;
```

```sql
SELECT * FROM TABLE(DBMS_XPLAN.DISPLAY(format => 'ALL'));
```

```sql
Plan hash value: 1534314425
 
----------------------------------------------------------------------------------------
| Id  | Operation            | Name            | Rows  | Bytes | Cost (%CPU)| Time     |
----------------------------------------------------------------------------------------
|   0 | SELECT STATEMENT     |                 |    12 |  1284 |    10  (10)| 00:00:01 |
|   1 |  SORT ORDER BY       |                 |    12 |  1284 |    10  (10)| 00:00:01 |
|   2 |   VIEW               |                 |    12 |  1284 |     9   (0)| 00:00:01 |
|   3 |    UNION-ALL         |                 |       |       |            |          |
|   4 |     TABLE ACCESS FULL| FAVORITE_CITIES |     4 |   128 |     3   (0)| 00:00:01 |
|   5 |     TABLE ACCESS FULL| FAVORITE_CITIES |     4 |   136 |     3   (0)| 00:00:01 |
|   6 |     TABLE ACCESS FULL| FAVORITE_CITIES |     4 |   132 |     3   (0)| 00:00:01 |
----------------------------------------------------------------------------------------
```

#### Plan for UNION PostgreSQL

```sql
explain
with all_cities as 
(select client_name, city_1 as city, 1 as rank from favorite_cities
 union all
 select client_name, city_2 as city, 2 as rank from favorite_cities
 union all
 select client_name, city_3 as city, 3 as rank from favorite_cities)
select * from all_cities order by client_name, rank;
```

```sql
Sort  (cost=44.95..45.63 rows=270 width=440)
  Sort Key: favorite_cities.client_name, (1)
  ->  Append  (cost=0.00..34.05 rows=270 width=440)
        ->  Seq Scan on favorite_cities  (cost=0.00..10.90 rows=90 width=440)
        ->  Seq Scan on favorite_cities favorite_cities_1  (cost=0.00..10.90 rows=90 width=440)
        ->  Seq Scan on favorite_cities favorite_cities_2  (cost=0.00..10.90 rows=90 width=440)
```

