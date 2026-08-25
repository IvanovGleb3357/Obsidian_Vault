## Функции
- LENGTH('KARPOV.COURSES') = 14
- UPPER('karpov.courses') = 'KARPOV.COURSE'
- LEFT('karpov.courses', 6) = 'karpov'
- SPLIT_PART('karpov.courses', '.', 2) = 'courses'
- CAST('100' AS INTEGER) = 100 (INT)
- CONCAT('SQL', ' ', 'SIMULATRO ', '2022') = SQL SUMILATOR 2022
- DATE_PART(part, column)

	  DATE_PART('year', DATE '2022-01-01') = 2022

- COALESCE(column, 'filler_value') - Вывоид первое не нулевое значение

	    COALESCE(CAST(DATE_PART('year', birth_date) AS VARCHAR), 'unknown') as birth_year

- ROUND(100.23, 1) = 100.2

- CASE

		CASE
		WHEN tra ta ta THEN to
		WHEN papapa THEN ro
		ELSE koko
		END as smth_new

- LIKE

		WHERE
		    name LIKE '%чай%', где
		    % - любое кол-во символов
		    _ - один символ

- IN

		WHERE column_1 IN ('product_1', 'product_2', 'product_3')

- BETWEEN

		WHERE column_2 BETWEEN 5 AND 10

## Агрегация данных

- DISTINCT - уникальные значения в столбце. Или если SELECT DISTINCT col_1., col_2 - то уникальные комбинации в столбцах
- COUNT() - количество не null значений в колонке или COUNT(*) - количество строк в таблице с учетом Null.* Также есть COUNT(DISTINCT user_id) - кол-во уникальных юзер айди
- SUM() 
- AVG()
- MIN()
- MAX()
- array_length(ARRAY[1, 2, 3], 1) = 3
- AGE(current_date, date) = разница между первой датой и второй. Также имеет смысл переводить в VARCHAR

- Агрегатное выражение с фильтрацией
В общем виде выглядит так:

	SELECT agg_function(column) FILTER (WHERE condition)
	FROM table

	SELECT AVG(price) FILTER (WHERE category = 'рыба') AS avg_fish_price
	FROM table

Еще пример, поиск кол-ва юзеров, которые никогда не отменяли заказы.

	SELECT
    COUNT(DISTINCT user_id) - COUNT(DISTINCT user_id) FILTER (WHERE action='cancel_order') as users_count
	FROM
	    user_actions

## JOIN-ы

- INNER JOIN
- LEFT/RIGHT JOIN
- FULL JOIN
- CROSS JOIN

Дефолтный JOIN

	SELECT table_1.column_1, table_2.column_2
	FROM table_1 
    JOIN table_2
    ON table_1.id = table_2.id

JOIN с USING

	SELECT a.column_1, b.column_2
	FROM table_1 a 
    JOIN table_2 b
    USING (id)

Несколько JOIN

	SELECT a.column_1, b.column_2
	FROM table_1 a 
     LEFT JOIN table_2 b
     ON a.user_id = b.user_id
     JOIN table_3 c
     ON b.order_id = c.order_id

INNER JOIN
1) Каждая строка первой таблицы сопостовляется с каждой строкой второй таблицы (берется декартово произведение)
2) Затем проверяется условие, прописанное в ON
3) Наконец откидываются строки, где условие не истина

LEFT JOIN (LEFT OUTER JOIN)
1) Каждая строка первой таблицы сопостовляется с каждой строкой второй таблицы (берется декартово произведение)
2) Затем проверяется условие, прописанное в ON
3) Наконец откидываются строки, где условие не истина
4) Затем к полученным строкам докидываются строки из левой таблицы, где условие не выполнилось. На место пропусков ставится NULL

FULL JOIN

- Каждая строка левой таблицы сопоставляется с каждой строкой правой таблиц (происходит декартово произведение)
- Затем проверяется условие, прописаное в ON
- После, этого, все объединенные строки, для которых условие истино - берутся в резуллтирующую таблицу
- Далее в результат добваляются те записи из левой и правой таблц, для которых условие оказалось ложным. Пустые поля заполняются NULL.


		SELECT A.id as id,
	       A.city as city,
	       B.country as country
		FROM table_A as A
	     FULL JOIN table_B as B
	     ON A.id = B.id

UNION, EXCEPT, INTERSECT
UNION - Объединение множеств
EXCEPT - Разница множеств (возвращает те значения, которые есть в первом, но нет во втором)
INTERSECT - Пересечение (Есть и в Первом и во Втором множестве)

	![[Pasted image 20231218235138.png]]

	SELECT column_1, column_2 
	FROM table_1 
	UNION
	SELECT column_1, column_2
	FROM table_2

Для работы этих операций необходимо, чтобы выполнялись следующие условия:

1. В каждом запросе в `SELECT` должно быть одинаковое количество столбцов.
2. Типы данных в столбцах должны быть совместимы.  
    

При этом количество столбцов в операторе `SELECT` может быть любым — главное, чтобы оно было одинаковым.
Например, этот запрос вернет пользователей, которые что-то покупали, но их нет в таблице юзерс.

	SELECT user_id
	FROM user_actions
	EXCEPT
	SELECT user_id
	FROM users

CROSS JOIN
На самом деле `CROSS JOIN` — это просто декартово произведение двух таблиц, то есть именно то, что происходит на первом этапе остальных джойнов. Важное отличие в синтаксисе `CROSS JOIN` состоит в том, что для него не нужно указывать условие для соединения:

	SELECT
	    A.city as city,
	    B.country as country
	FROM table_A as A
	     CROSS JOIN table_B as B



ОКОННЫЕ ФУНКЦИИ
	![[Pasted image 20231219023429.png]]

Параметры
- **UNBOUNDED PRECEDING** — указывает, что окно начинается с первой строки группы;
- **UNBOUNDED FOLLOWING** – с помощью данной инструкции можно указать, что окно заканчивается на последней строке группы;
- **CURRENT ROW** – инструкция указывает, что окно начинается или заканчивается на текущей строке;
- **BETWEEN** **«_граница окна_» AND «_граница окна_»** — указывает нижнюю и верхнюю границу окна;
- **«_Значение_»** **PRECEDING** – определяет число строк перед текущей строкой (не допускается в предложении RANGE).;
- **«_Значение_»** **FOLLOWING** — определяет число строк после текущей строки (не допускается в предложении RANGE).

UNBOUNDED PRECEDING
*значение* PRECEDING
CURRENT ROW
*значение* FOLLOWING
UNBOUNDED FOLLOWING
