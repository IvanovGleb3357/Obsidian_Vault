6. Напишите запрос, который выведет количество инструментов (столбец instrument_id), у которых есть ограничение на обращение (столбец has_restriction_circulation).

7. Напишите запрос, который найдет инструменты (столбец instrument_id), у которых дата регистрации (столбец registry_date) позже даты принятия решения о выпуске (столбец decision_date).

8. Напишите запрос, который выведет максимальное количество выпущенных ценных бумаг (столбец issue_amount) для каждой категории инструментов (столбец instrument_category).

9. Напишите запрос, который найдет инструменты (столбец instrument_id), у которых процентная ставка по купонам (столбец coupon_percent) выше среднего значения по всей таблице.

10. Напишите запрос, который определит, сколько инструментов (столбец instrument_id) имеют решение о выпуске (столбец decision_date) после 01.01.2021 года и имеют статус ПИФа (столбец pif_status).


Вот ещё одна пачка
1. Напишите запрос, который выведет суммарное количество записей по каждой категории инструмента (instrument_category) из таблицы moex_sec.
2. Напишите запрос, который покажет количество записей по каждому emitent_full_name, у которого количество записей больше 100.
3. Напишите запрос, который выведет список инструментов (instrument_id) и их средний номинал (nominal) за каждый год (год из datestamp).
4. Напишите запрос, который покажет список инструментов (instrument_id), у которых есть дефолт по безопасности (security_has_default), и сумму выпущенных ими бумаг (issue_amount).
5. Напишите запрос, который покажет список инструментов (instrument_id), у которых есть решение по дате (decision_date), и процент купона (coupon_percent) больше 5%.
6. Напишите запрос, который выведет список инструментов (instrument_id), у которых есть ограничение на обращение (has_restriction_circulation), и дату регистрации (registry_date).
7. Напишите запрос, который покажет список инструментов (instrument_id), у которых есть решение по дате (decision_date), и процент купона (coupon_percent) меньше 3%.
8. Напишите запрос, который выведет список инструментов (instrument_id) и их средний номинал (nominal) за каждый месяц (месяц из datestamp).
9. Напишите запрос, который покажет список инструментов (instrument_id), у которых есть решение по дате (decision_date), и процент купона (coupon_percent) равен 0.
10. Напишите запрос, который выведет список инструментов (instrument_id) и общее количество записей для каждого из них, отсортированных по убыванию количества записей.

6.
select
	COUNT(distinct instrument_id)
from
	team_a_lz.moex_sec ms
where
	has_restriction_circulation = '+'

7.
select

instrument_id

from

team_a_lz.moex_sec ms

where

to_date(registry_date, 'DD.MM.YYYY HH24:MI:SS') > to_date(decision_date, 'DD.MM.YYYY HH24:MI:SS')

8.

select

instrument_category,

MAX(replace(issue_amount, ',', '.')::DECIMAL) as max_issue_amount

from

team_a_lz.moex_sec ms

where

issue_amount ~ '\d'

group by

instrument_category

9.

with cte as (

select

instrument_id,

replace(replace(coupon_percent, ',', '.'), '%', '')::FLOAT as coupon_percent,

AVG(replace(replace(coupon_percent, ',', '.'), '%', '')::FLOAT) over () as avg_coupon_percent

from

team_a_lz.moex_sec ms

where

coupon_percent ~ '\d+%'

)

select

instrument_id

from

cte

where

coupon_percent > avg_coupon_percent

10.
select

instrument_id,

to_Date(decision_date, 'DD.MM.YYYY HH24:MI:SS') as decision_date,

pif_status

from

team_a_lz.moex_sec ms

where

to_Date(decision_date, 'DD.MM.YYYY HH24:MI:SS') > '01.01.2021'

and

pif_status ~ '\w'

11.
select

instrument_category,

COUNT(instrument_category)

from

team_a_lz.moex_sec ms

group by

instrument_category

12.
select

emitent_full_name,

COUNT(emitent_full_name) as count_emitent_full_name

from

team_a_lz.moex_sec ms

group by

emitent_full_name

having

COUNT(emitent_full_name) > 100

13.
select

instrument_id,

Date_part('year', to_date(datestamp, 'DD.MM.YYYY HH24:MI;SS')) as date_year,

AVG(replace(nominal, ',', '.')::float)

from

team_a_lz.moex_sec ms

where

nominal ~ '\d'

group by

instrument_id,

Date_part('year', to_date(datestamp, 'DD.MM.YYYY HH24:MI;SS'))

14.
select

instrument_id,

security_has_default,

issue_amount

from

team_a_lz.moex_sec ms

where

security_has_default != ''

15.
select

instrument_id,

decision_date,

replace(replace(coupon_percent, '%', ''), ',', '.')::float as coupon_percent

from

team_a_lz.moex_sec ms

where

decision_date is not null

and

coupon_percent ~ '\d%'

and

replace(replace(coupon_percent, '%', ''), ',', '.')::float > 5

16.
select

instrument_id,

registry_date,

has_restriction_circulation

from

team_a_lz.moex_sec ms

where

has_restriction_circulation = '+'

17.
select

instrument_id,

decision_date,

replace(replace(coupon_percent, '%', ''), ',', '.')::float as coupon_percent

from

team_a_lz.moex_sec ms

where

decision_date != ''

and

coupon_percent ~ '\d%'

and

replace(replace(coupon_percent, '%', ''), ',', '.')::float < 3

18.
select

date_part('month', to_date(datestamp, 'DD.MM.YYYY HH24:MI:SS')) as date_month,

instrument_id,

AVG(replace(nominal, ',', '.')::float) as avg_nominal

from

team_a_lz.moex_sec ms

where

nominal ~ '\d'

group by

date_part('month', to_date(datestamp, 'DD.MM.YYYY HH24:MI:SS')),

instrument_id

19.
select

instrument_id,

decision_date,

replace(replace(coupon_percent, '%', ''), ',', '.')::float as coupon_percent

from

team_a_lz.moex_sec ms

where

coupon_percent ~ '\d+%'

and

decision_date is not null

and

replace(replace(coupon_percent, '%', ''), ',', '.')::float = 0

20.
select

instrument_id,

COUNT(instrument_id) as instrument_id_count

from

team_a_lz.moex_sec ms

group by

instrument_id

order by
instrument_id_count DESC