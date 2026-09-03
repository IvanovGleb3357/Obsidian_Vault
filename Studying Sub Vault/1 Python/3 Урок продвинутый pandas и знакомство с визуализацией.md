[[Курс Аналитик Данных karpov.course]]

## Метод .unique() и .nunique()
Возвращает уникальные значения в колонке, а второй - их кол-во.

## Метод .median(), mean()
Возвращает медиану и ср. знач колонки.

## Анонимные функции lamda
	df is a dataframe as usual
	df = df.rename(columns=lambda c: c.upper().replace('-', '_'))

## Объединение датафреймов через merge
	df1.merge(df2, how='inner', on='id')
	
	![[Pasted image 20230725111800.png]]


Датафрейм обладает index и columns, обратившись к ним можем получить информацию о датафрейме:

			![[Pasted image 20230725112045.png]]
	df.index
	Index(['easy', 'executive', 'group'], dtype='object')

	df.columns
	Index(['journey_id', 'driver_id'], dtype='object')

## Удаление индекса у датафрейма .reset_index()
					![[Pasted image 20230725112202.png]]

Также есть аругмент drop, который отвечает за удаление или оставление исходного индекса.
	Если .reset_index(drop=True) - то индекс удалится, и вместо него будет столбец с нумерацией инексов
	Если .reset_index(drop=False) - то индекс останется и добавится столбец с нумерацией индексов.

## Метод .isna() в связвке с .sum()
С помощью метода .isna() можно проверить ячейку на пустоту. Если в ячейке нет значения то туда занесетя True если есть, то False. Следовательно если к колонке применить .isna().sum() - то мы получим кол-во пустых значений.

## taxi.source.value_counts(normalize=True)
Позволяет посчитать в процентах кол-во встречание определнного типа.


## stack() and unstack()
