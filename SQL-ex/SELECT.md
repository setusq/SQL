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
__Задание 31:__
Для классов кораблей, калибр орудий которых не менее 16 дюймов, укажите класс и страну.
__Решение:__
```sql
SELECT DISTINCT class, country
FROM classes
WHERE bore >= 16
```
__Задание 32:__
Одной из характеристик корабля является половина куба калибра его главных орудий (mw). С точностью до 2 десятичных знаков определите среднее значение mw для кораблей каждой страны, у которой есть корабли в базе данных.
__Решение:__
```sql
SELECT country, cast(avg((power(bore, 3)/2)) AS numeric(6,2)) AS mw
FROM 
    (SELECT country, classes.class, bore, name 
     FROM classes 
     LEFT JOIN ships ON classes.class = ships.class
     UNION ALL
     SELECT DISTINCT country, class, bore, ship AS name 
     FROM classes c
     LEFT JOIN outcomes o ON c.class = o.ship
     WHERE ship = class AND ship NOT IN (SELECT name FROM ships)) a
WHERE name IS NOT NULL 
GROUP BY country

```
__Задание 33:__
Укажите корабли, потопленные в сражениях в Северной Атлантике (North Atlantic). Вывод: ship.
__Решение:__
```sql
SELECT ship
FROM outcomes
WHERE battle = 'North Atlantic'
  AND RESULT = 'sunk'
```
__Задание 34:__
По Вашингтонскому международному договору от начала 1922 г. запрещалось строить линейные корабли водоизмещением более 35 тыс.тонн. Укажите корабли, нарушившие этот договор (учитывать только корабли c известным годом спуска на воду). Вывести названия кораблей.
__Решение:__
```sql
SELECT DISTINCT name 
FROM ships s 
JOIN classes c ON c.class = s.class 
WHERE type = 'bb' 
AND displacement > 35000 
AND launched >= 1922

```
__Задание 35:__
В таблице Product найти модели, которые состоят только из цифр или только из латинских букв (A-Z, без учета регистра).
Вывод: номер модели, тип модели.
__Решение:__
```sql
select model, type from product
WHERE model NOT LIKE '%[^a-zA-Z]%'
or model NOT LIKE '%[^0-9]%'
```
__Задание 36:__
Перечислите названия головных кораблей, имеющихся в базе данных (учесть корабли в Outcomes).

__Решение:__
```sql
SELECT DISTINCT ship
FROM outcomes o
JOIN classes c ON c.class = o.ship
UNION
SELECT DISTINCT name
FROM ships s
JOIN classes c ON c.class = s.name
```
__Задание 37:__
Найдите классы, в которые входит только один корабль из базы данных (учесть также корабли в Outcomes).

__Решение:__
```sql
SELECT CLASS
FROM
  (SELECT DISTINCT CLASS,
                   ship
   FROM classes c
   JOIN outcomes o ON c.class = o.ship
   UNION SELECT DISTINCT c.class,
                         name
   FROM classes c
   JOIN ships s ON c.class = s.class) a
GROUP BY CLASS
HAVING count(*)=1
```
__Задание 38:__
Найдите страны, имевшие когда-либо классы обычных боевых кораблей ('bb') и имевшие когда-либо классы крейсеров ('bc').

__Решение:__
```sql
SELECT country
FROM classes
WHERE TYPE = 'bb' INTERSECT
  SELECT country
  FROM classes WHERE TYPE = 'bc'
```
__Задание 39:__
Найдите корабли, `сохранившиеся для будущих сражений`; т.е. выведенные из строя в одной битве (damaged), они участвовали в другой, произошедшей позже.

__Решение:__
```sql
SELECT DISTINCT o1.ship
FROM outcomes o1
JOIN battles b1 ON b1.name = o1.battle
WHERE o1.result = 'damaged'
AND EXISTS (
    SELECT 1
    FROM outcomes o2
    JOIN battles b2 ON b2.name = o2.battle
    WHERE o2.ship = o1.ship
    AND b2.date > b1.date
)
```
__Задание 40:__
Найти производителей, которые выпускают более одной модели, при этом все выпускаемые производителем модели являются продуктами одного типа.
Вывести: maker, type
__Решение:__
```sql
SELECT maker, MIN(type) AS type
FROM product
GROUP BY maker
HAVING COUNT(*) > 1 AND COUNT(DISTINCT type) = 1

```
__Задание 41:__
Для каждого производителя, у которого присутствуют модели хотя бы в одной из таблиц PC, Laptop или Printer,
определить максимальную цену на его продукцию.
Вывод: имя производителя, если среди цен на продукцию данного производителя присутствует NULL, то выводить для этого производителя NULL,
иначе максимальную цену.
__Решение:__
```sql
SELECT maker,
       CASE 
           WHEN COUNT(price) <> COUNT(*) THEN NULL
           ELSE MAX(price)
       END AS max_price
FROM (SELECT p.maker, pc.price
    FROM Product p
    JOIN PC pc ON p.model = pc.model
    UNION ALL
    SELECT p.maker, l.price
    FROM Product p
    JOIN Laptop l ON p.model = l.model
    UNION ALL
    SELECT p.maker, pr.price
    FROM Product p
    JOIN Printer pr ON p.model = pr.model) a
GROUP BY maker

```
__Задание 42:__
Найдите названия кораблей, потопленных в сражениях, и название сражения, в котором они были потоплены.
__Решение:__
```sql
SELECT ship,
       battle
FROM outcomes
WHERE RESULT = 'sunk'
```
__Задание 43:__

__Решение:__
```sql

```
__Задание 44:__
Найдите названия всех кораблей в базе данных, начинающихся с буквы R.
__Решение:__
```sql
SELECT name
FROM ships
WHERE name like 'R%'
UNION
SELECT ship
FROM outcomes
WHERE ship like 'R%'
```
__Задание 45:__
Найдите названия всех кораблей в базе данных, состоящие из трех и более слов (например, King George V).
Считать, что слова в названиях разделяются единичными пробелами, и нет концевых пробелов
__Решение:__
```sql
SELECT name
FROM ships
WHERE name like '% % %'
UNION
SELECT ship
FROM outcomes
WHERE ship like '% % %'

```
__Задание 46:__

__Решение:__
```sql

```
__Задание 47:__

__Решение:__
```sql

```
__Задание 48:__

__Решение:__
```sql

```
__Задание 49:__
Найдите названия кораблей с орудиями калибра 16 дюймов (учесть корабли из таблицы Outcomes).
__Решение:__
```sql
SELECT name
FROM ships s
JOIN classes c ON c.class = s.class
WHERE bore = 16
UNION
SELECT ship
FROM outcomes o
JOIN classes c ON c.class = o.ship
WHERE bore = 16
```
__Задание 50:__
Найдите сражения, в которых участвовали корабли класса Kongo из таблицы Ships.
__Решение:__
```sql
SELECT DISTINCT battle
FROM outcomes o
JOIN ships s ON o.ship = s.name
JOIN classes c ON c.class = s.class
WHERE c.class = 'Kongo'
```
-------------------------------------------------------------------------
__Задание :__

__Решение:__
```sql

```

