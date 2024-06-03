__Задание: 1__
Дима и Миша пользуются продуктами от одного и того же производителя.
Тип Таниного принтера не такой, как у Вити, но признак "цветной или нет" - совпадает.
Размер экрана Диминого ноутбука на 3 дюйма больше Олиного.
Мишин ПК в 4 раза дороже Таниного принтера.
Номера моделей Витиного принтера и Олиного ноутбука отличаются только третьим символом.
У Костиного ПК скорость процессора, как у Мишиного ПК; объем жесткого диска, как у Диминого ноутбука; объем памяти, как у Олиного ноутбука, а цена - как у Витиного принтера.
Вывести все возможные номера моделей Костиного ПК.


__Решение:__
```sql
SELECT DISTINCT k.model
FROM   (SELECT maker, screen, hd
        FROM   laptop l
               JOIN product p
                 ON l.model = p.model) d,
       (SELECT maker, price, speed
        FROM   pc
               JOIN product p
                 ON pc.model = p.model) m,
       (SELECT price, type, color
        FROM   printer) t,
       (SELECT model, type, color, price
        FROM   printer) v,
       (SELECT model, ram, screen
        FROM   laptop) o,
       (SELECT speed, hd, ram, price, model
        FROM   pc) k
WHERE  d.maker = m.maker
       AND t.type <> v.type
       AND t.color = v.color
       AND d.screen = o.screen + 3
       AND m.price = 4 * t.price
       AND Stuff(v.model, 3, 1, '') = Stuff(o.model, 3, 1, '')
       AND k.speed = m.speed
       AND k.hd = d.hd
       AND k.ram = o.ram
       AND k.price = v.price 
```
__Задание: 2__

Для каждого месяца (с учетом года) из таблицы Battles посчитать сколько раз повторяется каждый день недели в этом месяце.
Вывод: месяц (в формате "YYYY-ММ"), количество понедельников, вторников, ...воскресений.

__Решение:__
```sql

SELECT
    FORMAT(date, 'yyyy-MM') AS month,
    DATEDIFF(WEEK, DATEADD(DAY, -((1 + 1) % 7), FORMAT(date, 'yyyy-MM') + '-01'),
             DATEADD(DAY, -((1 + 1) % 7), DATEADD(MONTH, 1, FORMAT(date, 'yyyy-MM') + '-01'))) AS Mon,
    DATEDIFF(WEEK, DATEADD(DAY, -((2 + 1) % 7), FORMAT(date, 'yyyy-MM') + '-01'),
             DATEADD(DAY, -((2 + 1) % 7), DATEADD(MONTH, 1, FORMAT(date, 'yyyy-MM') + '-01'))) AS Tue,
    DATEDIFF(WEEK, DATEADD(DAY, -((3 + 1) % 7), FORMAT(date, 'yyyy-MM') + '-01'),
             DATEADD(DAY, -((3 + 1) % 7), DATEADD(MONTH, 1, FORMAT(date, 'yyyy-MM') + '-01'))) AS Wed,
    DATEDIFF(WEEK, DATEADD(DAY, -((4 + 1) % 7), FORMAT(date, 'yyyy-MM') + '-01'),
             DATEADD(DAY, -((4 + 1) % 7), DATEADD(MONTH, 1, FORMAT(date, 'yyyy-MM') + '-01'))) AS Thu,
    DATEDIFF(WEEK, DATEADD(DAY, -((5 + 1) % 7), FORMAT(date, 'yyyy-MM') + '-01'),
             DATEADD(DAY, -((5 + 1) % 7), DATEADD(MONTH, 1, FORMAT(date, 'yyyy-MM') + '-01'))) AS Fri,
    DATEDIFF(WEEK, DATEADD(DAY, -((6 + 1) % 7), FORMAT(date, 'yyyy-MM') + '-01'),
             DATEADD(DAY, -((6 + 1) % 7), DATEADD(MONTH, 1, FORMAT(date, 'yyyy-MM') + '-01'))) AS Sat,
    DATEDIFF(WEEK, DATEADD(DAY, -((7 + 1) % 7), FORMAT(date, 'yyyy-MM') + '-01'),
             DATEADD(DAY, -((7 + 1) % 7), DATEADD(MONTH, 1, FORMAT(date, 'yyyy-MM') + '-01'))) AS Sun
FROM
    Battles
GROUP BY
    FORMAT(date, 'yyyy-MM')
```

