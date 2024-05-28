__Задание: 1__
Найдите номер модели, скорость и размер жесткого диска для всех ПК стоимостью менее 500 дол. Вывести: model, speed и hd.

__Решение:__
```sql
SELECT model, speed, hd
FROM PC
WHERE price < 500
```
__Задание: 2__
Найдите производителей принтеров. Вывести: maker.

__Решение:__
```sql
SELECT DISTINCT maker
FROM   product
WHERE  type = 'Printer' 
```
__Задание 3:__
Найдите номер модели, объем памяти и размеры экранов ПК-блокнотов, цена которых превышает 1000 дол.

__Решение:__
```sql
SELECT model,
       ram,
       screen
FROM   laptop
WHERE  price > 1000 

```
__Задание 4:__
Найдите все записи таблицы Printer для цветных принтеров.

__Решение:__
```sql
SELECT *
FROM   printer
WHERE  color = 'y' 
```
__Задание 5:__
Найдите номер модели, скорость и размер жесткого диска ПК, имеющих 12x или 24x CD и цену менее 600 дол.

__Решение:__
```sql
SELECT model,
       speed,
       hd
FROM   pc
WHERE  cd IN ( '12x', '24x' )
       AND price < 600 
```
__Задание 6:__
Для каждого производителя, выпускающего ПК-блокноты c объёмом жесткого диска не менее 10 Гбайт, найти скорости таких ПК-блокнотов. Вывод: производитель, скорость.

__Решение:__
```sql
SELECT DISTINCT maker,
                speed
FROM   product
       JOIN laptop
         ON product.model = laptop.model
WHERE  hd >= 10 
```
__Задание 7:__
Найдите номера моделей и цены всех имеющихся в продаже продуктов (любого типа) производителя B (латинская буква).
__Решение:__
```sql
SELECT product.model,
       price
FROM   product
       JOIN pc
         ON product.model = pc.model
WHERE  maker = 'B'
UNION
SELECT product.model,
       price
FROM   product
       JOIN printer
         ON product.model = printer.model
WHERE  maker = 'B'
UNION
SELECT product.model,
       price
FROM   product
       JOIN laptop
         ON product.model = laptop.model
WHERE  maker = 'B' 
```
__Задание 8:__
Найдите производителя, выпускающего ПК, но не ПК-блокноты.
__Решение:__
```sql
SELECT DISTINCT maker
FROM            product
WHERE           type = 'pc'
EXCEPT
SELECT DISTINCT maker
FROM            product
WHERE           type = 'laptop'
```
__Задание 9:__
Найдите производителей ПК с процессором не менее 450 Мгц. Вывести: Maker

__Решение:__
```sql
SELECT DISTINCT product.maker
FROM pc
INNER JOIN product ON pc.model = product.model
WHERE pc.speed >= 450
```
__Задание 10:__
Найдите модели принтеров, имеющих самую высокую цену. Вывести: model, price

__Решение:__
```sql
SELECT model,
       price
FROM   printer
WHERE  price = (SELECT Max(price)
                FROM   printer) 
```
__Задание :__

__Решение:__
```sql

```
__Задание :__

__Решение:__
```sql

```
__Задание :__

__Решение:__
```sql

```

__Задание :__

__Решение:__
```sql

```
__Задание :__

__Решение:__
```sql

```
__Задание :__

__Решение:__
```sql

```
__Задание :__

__Решение:__
```sql

```
__Задание :__

__Решение:__
```sql

```
__Задание :__

__Решение:__
```sql

```
__Задание :__

__Решение:__
```sql

```
__Задание :__

__Решение:__
```sql

```
__Задание :__

__Решение:__
```sql

```
__Задание :__

__Решение:__
```sql

```
__Задание :__

__Решение:__
```sql

```
__Задание :__

__Решение:__
```sql

```
__Задание :__

__Решение:__
```sql

```
__Задание :__

__Решение:__
```sql

```

__Задание :__

__Решение:__
```sql

```

