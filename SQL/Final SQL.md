тото, тото

## Составьте запрос, который выведет имя вида с наименьшим id

```SELECT species_name FROM species
WHERE species_id = (SELECT MIN(species_id) FROM species);```



SELECT species_name FROM species
WHERE species_amount > 1800;

SELECT species_name FROM species
WHERE species_name LIKE 'п%' AND type_id = 5;

SELECT species_name FROM species
WHERE species_name LIKE '%са'OR species_amount = 5;


2
SELECT species_name FROM species
WHERE date_start > '2022-12-31';

SELECT sp.species_name FROM species as sp JOIN species_in_places as sip
ON sp.species_id = sip.species_id
WHERE species_status = 'absent' AND place_id = 3;

SELECT species_name FROM species as sp 
JOIN species_in_places as sip ON sp.species_id = sip.species_id
JOIN places as pl ON sip.place_id = pl.place_id
WHERE pl.place_name = 'дом' AND to_char(sp.date_start,'MM') = '05';

SELECT species_name FROM species
WHERE species_name LIKE '% %';


3
SELECT sp1.species_name FROM species as sp1
JOIN species as sp2 ON sp1.date_start = sp2.date_start AND sp1.species_name != sp2.species_name
WHERE sp2.species_name = 'малыш';

SELECT species_name FROM species as sp 
JOIN species_in_places as sip ON sp.species_id = sip.species_id
JOIN places as pl ON sip.place_id = pl.place_id
WHERE pl.place_name = 'дом' OR pl.place_name = 'сарай'
ORDER BY pl.place_size DESC LIMIT 1;
	
SELECT sp.species_name FROM species as sp
JOIN species_in_places as sip ON sp.species_id = sip.species_id
JOIN places as pl ON pl.place_id = sip.place_id
WHERE pl.place_name = 'дом'
ORDER BY species_amount DESC LIMIT 1 OFFSET 4;

SELECT species_name FROM species as sp LEFT JOIN species_in_places as sip
ON sp.species_id = sip.species_id
WHERE place_id IS NULL;