## 5 Генераторы списков Python | List comprehension
1. a = [i for i in range(7)]
	print(a)
	0, 1, 2, 3, 4, 5, 6
2. a = [i**2 for i in range(10)]
	print(a)
3. a = [i for i in "hello"]
	print(a)
4. a = [ord(i) for i in "hello"]
	print(a)
5. from random import randint
	a = [randint(-10, 10) for i in range(10)]
	print(a)
	
Способ ввода:
1. a = input().split()
	a = [int(i) for i ina a]
	print(a)
2. a = map(int, input().split())

Более сложный пример:
1.	from random import randint
	a = [randint(-10, 10) for i in range(10)]
	print(a)
	b = [abs(elem) for elem in a]
	print(b)
2. from random import randint
	a = [randint(-10, 10) for i in range(10)]
	print(a)
	a = [elem+1 for elem in a]
	print(a)
Создание матрицы:
1. n = 5
	m = 4
	a = [[0]*m for i in range(n)]
	print(f)
	for i in a:
		print(i)

Также можно добавить условие, в данном случае релазиуется поиск делителей:
	n = int(input())
	a = [i for i in range(1, n + 1) if n % i == 0]
	print(a)


[[Инди-курс python stepik]]