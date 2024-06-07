__Задание: 1__
Добавить в таблицу PC следующую модель:
code: 20
model: 2111
speed: 950
ram: 512
hd: 60
cd: 52x
price: 1100

__Решение:__
```sql
INSERT INTO pc
VALUES (20, 2111, 950, 512, 60, '52x', 1100)
```
__Задание: 2__
Добавить в таблицу Product следующие продукты производителя Z:
принтер модели 4003, ПК модели 4001 и блокнот модели 4002

__Решение:__
```sql
INSERT INTO Product VALUES
('Z', 4003, 'Printer'),
('Z', 4001, 'PC'),
('Z', 4002, 'Laptop') 
```
__Задание 3__
Добавить в таблицу PC модель 4444 с кодом 22, имеющую скорость процессора 1200 и цену 1350.

__Решение:__
```sql
INSERT INTO pc (model, code, speed, price)
VALUES (4444,22,1200,1350)
```

__Задание 4:__

Для каждой группы блокнотов с одинаковым номером модели добавить запись в таблицу PC со следующими характеристиками:
код: минимальный код блокнота в группе +20;
модель: номер модели блокнота +1000;
скорость: максимальная скорость блокнота в группе;
ram: максимальный объем ram блокнота в группе *2;
hd: максимальный объем hd блокнота в группе *2;
cd: значение по умолчанию;
цена: максимальная цена блокнота в группе, уменьшенная в 1,5 раза.
Замечание. Считать номер модели числом.

__Решение:__
```sql
INSERT INTO pc (code, model, speed, ram, hd, price)
SELECT min(code)+20,
       model+1000,
       max(speed),
       max(ram)*2,
       max(hd)*2,
       max(price)/1.5
FROM laptop
GROUP BY model
```

__Задание 5:__

Удалить из таблицы PC компьютеры, имеющие минимальный объем диска или памяти.

__Решение:__
```sql
DELETE
FROM pc
WHERE ram =
    (SELECT min(ram)
     FROM pc)
  OR hd =
    (SELECT min(hd)
     FROM pc)
```

__Задание 6:__

Удалить все блокноты, выпускаемые производителями, которые не выпускают принтеры.

__Решение:__
```sql
DELETE
FROM laptop
WHERE model not in
    (SELECT model
     FROM product
     WHERE maker in
         (SELECT maker
          FROM product
          WHERE TYPE = 'Printer'))
```

__Задание 7:__

Производство принтеров производитель A передал производителю Z. Выполнить соответствующее изменение.

__Решение:__
```sql
UPDATE product
SET maker = 'Z'
WHERE maker = 'A'
  AND TYPE = 'Printer'
```

__Задание 8:__

Удалите из таблицы Ships все корабли, потопленные в сражениях.

__Решение:__
```sql

DELETE
FROM ships
WHERE name in
    (SELECT ship
     FROM outcomes
     WHERE RESULT = 'sunk')

```

__Задание 9:__

Измените данные в таблице Classes так, чтобы калибры орудий измерялись в
сантиметрах (1 дюйм=2,5см), а водоизмещение в метрических тоннах (1
метрическая тонна = 1,1 тонны). Водоизмещение вычислить с точностью до
целых.

__Решение:__
```sql
UPDATE classes
SET bore = bore *2.5,
    displacement = round(displacement/1.1, 0)

```
__Задание 10:__

Добавить в таблицу PC те модели ПК из Product, которые отсутствуют в таблице PC.

При этом модели должны иметь следующие характеристики:

1. Код равен номеру модели плюс максимальный код, который был до вставки.

2. Скорость, объем памяти и диска, а также скорость CD должны иметь максимальные характеристики среди всех имеющихся в таблице PC.

3. Цена должна быть средней среди всех ПК, имевшихся в таблице PC до вставки.
   
__Решение:__
```sql
INSERT INTO pc (code, model, speed, ram, hd, cd, price)
SELECT
  (SELECT MAX(code)
   FROM PC) + model AS code,
       model,

  (SELECT MAX(speed)
   FROM PC) AS speed,

  (SELECT MAX(ram)
   FROM PC) AS ram,

  (SELECT MAX(hd)
   FROM PC) AS hd,
       CAST(
              (SELECT MAX(CAST (SUBSTRING(cd, 1, LEN(cd) - 1) AS int))
               FROM PC) AS VARCHAR) + 'x' AS cd,

  (SELECT AVG(price)
   FROM PC) AS price
FROM product
WHERE TYPE = 'PC'
  AND model not IN
    (SELECT model
     FROM pc)

```

__Задание:__


__Решение:__
```sql

```


----

__Задание:__


__Решение:__
```sql

```
