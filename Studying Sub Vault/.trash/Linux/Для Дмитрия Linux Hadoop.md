	**scp** "C:\Users\ivano\Downloads\orders.csv" gl.ivanov@172.17.0.23:/home/gl.ivanov
2) Создать директорию и закинуть туда файл
	**mkdir** orders
	**mv** orders.csv orders
3) Создать копию файла с текущей датой
	**cp** orders.csv "orders_$(date +'%Y-%m_%H%M%S')"
4) Записать первые 10 строк в файл и последние 10
	**cat** orders.csv | {head; tail;}
	**head** orders.csv >> new_file. Если файл уже существует, то **>** перезапишет файл, **>>** добавит в конец строки 
	**sed** -n '2,20p' orders.csv >> new_file.
5) Добавить файл в домашнюю директорию 
	**hdfs dfs -put** orders.csv

## HIVE
1) Создать базу данных
	CREATE DATABASE  IF NOT EXISTS gl_ivanov
2) Создать таблицу
		![[Pasted image 20240314124010.png]]
	IN GENERAL:
		**CREATE EXTERNAL TABLE IF NOT EXISTS** gl_ivanov.orders
			(id INT,
			sum DOUBLE,
			desc STRING
			)
			**ROW FORMAT** DELIMITED
			**FIELDS TERMINATED** BY ','
			**LOCATION** '/user/gl.ivanov/orders'
			**STORED AS** TEXTFILE;
	Если LOCATION не указана до создается в /user/hive/warehouse/
3) Заполнить датой