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
