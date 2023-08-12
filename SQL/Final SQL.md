Запросы финального тестового задания по теме SQL

## Составьте запрос, который выведет имя вида с наименьшим id

```
SELECT species_name FROM species
WHERE species_id = (SELECT MIN(species_id) FROM species);
```

## Составьте запрос, который выведет имя вида с количеством представителей более 1800

```
SELECT species_name FROM species
WHERE species_amount > 1800;
```

## Составьте запрос, который выведет имя вида, начинающегося на «п» и относящегося к типу с type_id = 5

```
SELECT species_name FROM species
WHERE species_name LIKE 'п%' AND type_id = 5;
```

## Составьте запрос, который выведет имя вида, заканчивающегося на «са» или количество представителей которого равно 5

```
SELECT species_name FROM species
WHERE species_name LIKE '%са'OR species_amount = 5;
```

## Составьте запрос, который выведет имя вида, появившегося на учете в 2023 году

```
SELECT species_name FROM species
WHERE date_start > '2022-12-31';
```

## Составьте запрос, который выведет названия отсутствующего (status = absent) вида, расположенного вместе с place_id = 3

```
SELECT sp.species_name FROM species as sp JOIN species_in_places as sip
ON sp.species_id = sip.species_id
WHERE species_status = 'absent' AND place_id = 3;
```

## Составьте запрос, который выведет название вида, расположенного в доме и появившегося в мае, а также и количество представителей вида

```
SELECT species_name FROM species as sp 
JOIN species_in_places as sip ON sp.species_id = sip.species_id
JOIN places as pl ON sip.place_id = pl.place_id
WHERE pl.place_name = 'дом' AND to_char(sp.date_start,'MM') = '05';
```

## Составьте запрос, который выведет название вида, состоящего из двух слов (содержит пробел)

```
SELECT species_name FROM species
WHERE species_name LIKE '% %';
```

## Составьте запрос, который выведет имя вида, появившегося с малышом в один день

```
SELECT sp1.species_name FROM species as sp1
JOIN species as sp2 ON sp1.date_start = sp2.date_start AND sp1.species_name != sp2.species_name
WHERE sp2.species_name = 'малыш';
```

## Составьте запрос, который выведет название вида, расположенного в здании с наибольшей площадью

```
SELECT species_name FROM species as sp 
JOIN species_in_places as sip ON sp.species_id = sip.species_id
JOIN places as pl ON sip.place_id = pl.place_id
WHERE pl.place_name = 'дом' OR pl.place_name = 'сарай'
ORDER BY pl.place_size DESC LIMIT 1;
```

## Составьте запрос/запросы, которые найдут название вида, относящегося к 5-й по численности группе проживающей дома

```
SELECT sp.species_name FROM species as sp
JOIN species_in_places as sip ON sp.species_id = sip.species_id
JOIN places as pl ON pl.place_id = sip.place_id
WHERE pl.place_name = 'дом'
ORDER BY species_amount DESC LIMIT 1 OFFSET 4;
```

## Составьте запрос, который выведет сказочный вид (статус fairy), не расположенный ни в одном месте

```
SELECT species_name FROM species as sp LEFT JOIN species_in_places as sip
ON sp.species_id = sip.species_id
WHERE place_id IS NULL;
```