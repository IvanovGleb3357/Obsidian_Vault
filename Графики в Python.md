[[Курс Аналитик Данных karpov.course]]

**Seaborn, Matplotlib, Pandas** - самые популярные библиотеки для графиков. Для их нормального оторбражения необходимо написать %matplotlib inline.

## Pandas
Самый простой способ визуализировать данные — вызвать метод `plot` у датафрейма (или его колонки). Например, гистограмма значений в колонке `orders`:
	![[Pasted image 20230725112931.png]]
Bins - кол-во диапазонов, на которые разделяем нашу дату.

## Seaborn
Гистограмма:
	![[Pasted image 20230725113052.png]]

Боксплот:
	![[Pasted image 20230725113107.png]]

Барплот:
	![[Pasted image 20230725113122.png]]
**Countplot**
	sns.countplot(data=taxi, x='icon') - барплот, но не нужно сильно париться с осями.
	Есть параметр hue - позволяющий сделать разбивку стобцов по типу.

**Lineplot**
Line chart – линейная диаграмма. По оси x и y откладываются значения точек, эти точки соединяются. Аргумент `hue` принимает имя колонки, по значениям которой идёт разделение на цвета:
			![[Pasted image 20230727121236.png]]

**Heatmap**
Удобный тип графика, когда есть множество значений с двумя категориальными признаками (обычно это индекс и колонки в датафрейме). По осям откладываются значения этих категориальных переменных, каждая ячейка — значение, которое мы визуализируем. Интенсивность ячейки пропорциональна значению.

			![[Pasted image 20230727121334.png]]

## Способы кастомизации графиков
Первый

	ax = conversion_df.plot()  # create plot
	ax.set_xlabel('Date of orders')  # Label of x axis
	ax.set_ylabel('Conversion rate')  # Label of y axis
	ax.set_title('Conversion rate by date')  # Title of the plot
	y_labels = [str(int(i * 100)) + '%' for i in ax.get_yticks()]  # Prepare custom labels of axis values
	ax.set_yticklabels(y_labels)  # Set new labels
	ax.set_xticklabels(labels=conversion_df.index, rotation=90)  # Same just for x axis and totate labels to perpendicular configuration
	sns.despine()  # Get rid of axis on the plot

Второй

	ax = conversion_df.plot()
	plt.xlabel('Date of orders')
	plt.ylabel('Conversion rate')
	plt.title('Conversion rate by date')
	y_labels = [str(int(i * 100)) + '%' for i in ax.get_yticks()]
	ax.set_yticklabels(y_labels)
	ax.set_xticklabels(labels=conversion_df.index, rotation=90)
	sns.despine()





## Matplotlip
Базовая библиотека для рисования в питоне. На ней построены более продвинутые и простые в использовании типа `seaborn`. Через `matplotlib` можно нарисовать что угодно, но часто на это уходит слишком много строк кода, и её в основном используют для тонкой настройки графиков и их сохранения.

	import matplotlib.pyplot as plt

			![[Pasted image 20230725113308.png]]

Сохранение графика - ![[Pasted image 20230725113333.png]]


## Библиотека для создания интерактивных графиков
	import plotly.express as px
	px.line(conversion_df, conversion_df.index, conversion_df['Conversion_rate'])

![[Pasted image 20230728172606.png]]

