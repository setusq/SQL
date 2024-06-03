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
__Задание 11:__
Найдите среднюю скорость ПК.

__Решение:__
```sql
SELECT avg(speed)
FROM pc 
```
__Задание 12:__

Найдите среднюю скорость ПК-блокнотов, цена которых превышает 1000 дол.
__Решение:__
```sql
SELECT avg(speed)
FROM laptop
WHERE price>1000
```
__Задание 13:__
Найдите среднюю скорость ПК, выпущенных производителем A.

__Решение:__
```sql
SELECT avg(speed)
FROM pc
JOIN product
    ON product.model = pc.model
WHERE maker = 'A'
```

__Задание 14:__
Найдите класс, имя и страну для кораблей из таблицы Ships, имеющих не менее 10 орудий.

__Решение:__
```sql
SELECT ships.class,
         name,
         country
FROM ships
JOIN classes
    ON ships.class = classes.class
WHERE numGuns >=10 
```
__Задание 15:__

Найдите размеры жестких дисков, совпадающих у двух и более PC. Вывести: HD.
__Решение:__
```sql
SELECT hd
FROM pc
GROUP BY  hd
HAVING count(hd)>=2 
```
__Задание 16:__
Найдите пары моделей PC, имеющих одинаковые скорость и RAM. В результате каждая пара указывается только один раз, т.е. (i,j), но не (j,i), Порядок вывода: модель с большим номером, модель с меньшим номером, скорость и RAM.
__Решение:__
```sql
SELECT DISTINCT p1.model,
                p2.model,
                p1.speed,
                p1.ram
FROM pc p1,
     pc p2
WHERE p1.speed = p2.speed
  AND p1.ram = p2.ram
  AND p1.model>p2.model
```
__Задание 17:__
Найдите модели ПК-блокнотов, скорость которых меньше скорости каждого из ПК.
Вывести: type, model, speed
__Решение:__
```sql
SELECT DISTINCT TYPE,
                l.model,
                speed
FROM laptop l
JOIN product p ON p.model = l.model
WHERE speed < ALL
    (SELECT speed
     FROM pc)
```
__Задание 18:__
Найдите производителей самых дешевых цветных принтеров. Вывести: maker, price
__Решение:__
```sql
SELECT DISTINCT maker,
                price
FROM product
JOIN printer ON product.model = printer.model
WHERE color = 'y'
  AND price =
    (SELECT min(price)
     FROM printer
     WHERE color = 'y')
```
__Задание 19:__
Для каждого производителя, имеющего модели в таблице Laptop, найдите средний размер экрана выпускаемых им ПК-блокнотов.
Вывести: maker, средний размер экрана.
__Решение:__
```sql
SELECT maker,
       avg(screen)
FROM product p
JOIN laptop l ON l.model = p.model
GROUP BY maker
```
__Задание 20:__
Найдите производителей, выпускающих по меньшей мере три различных модели ПК. Вывести: Maker, число моделей ПК.
__Решение:__
```sql
SELECT DISTINCT maker,
                count(*) AS cnt
FROM product
WHERE TYPE = 'pc'
GROUP BY maker
HAVING count(*)>=3
```
__Задание 21:__
Найдите максимальную цену ПК, выпускаемых каждым производителем, у которого есть модели в таблице PC.
Вывести: maker, максимальная цена.
__Решение:__
```sql
SELECT maker,
       max(price)
FROM product
JOIN pc ON product.model = pc.model
GROUP BY maker
```
__Задание 22:__
ля каждого значения скорости ПК, превышающего 600 МГц, определите среднюю цену ПК с такой же скоростью. Вывести: speed, средняя цена.
__Решение:__
```sql
SELECT speed,
       avg(price)
FROM pc
WHERE speed>600
GROUP BY speed
```
__Задание 23:__
Найдите производителей, которые производили бы как ПК
со скоростью не менее 750 МГц, так и ПК-блокноты со скоростью не менее 750 МГц.
Вывести: Maker
__Решение:__
```sql
SELECT DISTINCT maker
FROM product
JOIN pc ON product.model = pc.model
WHERE speed>=750 INTERSECT
  SELECT DISTINCT maker
  FROM product
  JOIN laptop ON product.model = laptop.model WHERE speed>=750
```
__Задание 24:__
Перечислите номера моделей любых типов, имеющих самую высокую цену по всей имеющейся в базе данных продукции.
__Решение:__
```sql
WITH all_base AS
  (SELECT model,
          price
   FROM pc
   UNION SELECT model,
                price
   FROM laptop
   UNION SELECT model,
                price
   FROM printer)
SELECT DISTINCT model
FROM all_base
WHERE price =
    (SELECT max(price)
     FROM all_base)
```
__Задание 25:__
Найдите производителей принтеров, которые производят ПК с наименьшим объемом RAM и с самым быстрым процессором среди всех ПК, имеющих наименьший объем RAM. Вывести: Maker
__Решение:__
```sql
SELECT DISTINCT maker
FROM product
WHERE TYPE = 'printer'
  AND maker in
    (SELECT maker
     FROM product
     JOIN pc ON product.model = pc.model
     WHERE speed =
         (SELECT max(speed)
          FROM pc
          WHERE ram =
              (SELECT min(ram)
               FROM pc))
       AND ram =
         (SELECT min(ram)
          FROM pc))
```
__Задание 26:__
Найдите среднюю цену ПК и ПК-блокнотов, выпущенных производителем A (латинская буква). Вывести: одна общая средняя цена.
__Решение:__
```sql
SELECT AVG(price) 
FROM (
    SELECT price
    FROM pc
    JOIN product ON product.model = pc.model
    WHERE product.maker = 'A'
    UNION ALL
    SELECT price
    FROM laptop
    JOIN product ON product.model = laptop.model
    WHERE product.maker = 'A'
) AS all_price

```
__Задание 27:__
Найдите средний размер диска ПК каждого из тех производителей, которые выпускают и принтеры. Вывести: maker, средний размер HD.
__Решение:__
```sql
SELECT maker,
       avg(hd)
FROM pc
JOIN product ON pc.model = product.model
WHERE maker in
    (SELECT maker
     FROM product
     WHERE TYPE = 'printer')
GROUP BY maker
```
__Задание 28:__
Используя таблицу Product, определить количество производителей, выпускающих по одной модели.
__Решение:__
```sql
SELECT count(maker)
FROM product
WHERE maker in
    (SELECT maker
     FROM product
     GROUP BY maker
     HAVING count(model) = 1)
```
__Задание 29:__
В предположении, что приход и расход денег на каждом пункте приема фиксируется не чаще одного раза в день [т.е. первичный ключ (пункт, дата)], написать запрос с выходными данными (пункт, дата, приход, расход). Использовать таблицы Income_o и Outcome_o.
__Решение:__
```sql
SELECT i.point,
       i.date,
       inc,
       OUT
FROM income_o i
LEFT JOIN outcome_o o ON i.point = o.point
AND i.date = o.date
UNION
SELECT o.point,
       o.date,
       inc,
       OUT
FROM income_o i
RIGHT JOIN outcome_o o ON i.point = o.point
AND i.date = o.date
```
__Задание 30:__
В предположении, что приход и расход денег на каждом пункте приема фиксируется произвольное число раз (первичным ключом в таблицах является столбец code), требуется получить таблицу, в которой каждому пункту за каждую дату выполнения операций будет соответствовать одна строка.
Вывод: point, date, суммарный расход пункта за день (out), суммарный приход пункта за день (inc). Отсутствующие значения считать неопределенными (NULL).

__Решение:__
```sql
WITH i AS
  (SELECT point, date, sum(inc) AS inc
   FROM income
   GROUP BY point, date),
     o AS
  (SELECT point, date, sum(out) AS out
   FROM outcome
   GROUP BY point, date)
SELECT i.point,
       i.date,
       o.out outcome,
       i.inc income
FROM i
LEFT JOIN o ON i.point = o.point
AND i.date = o.date
UNION
SELECT o.point,
       o.date,
       o.out Outcome,
       i.inc Income
FROM i
RIGHT JOIN o ON i.point = o.point
AND i.date = o.date
```
-------------------------------------------------------------------------
__Задание :__

__Решение:__
```sql

```

