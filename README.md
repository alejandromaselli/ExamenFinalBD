# Examen Final Bases de Datos I

## Equipo a evaluar:

### Boston Red Sox

Posiciones:
- 1 Lanzador (Pitcher)
- 2 Receptor (Catcher)
- 3 Primera base (First baseman)
- 4 Segunda base (Second baseman)
- 5 Tercera base (Third baseman)
- 6 Campocorto o parador en corto (Short stop)
- 7 Jardinero izquierdo (Left fielder)
- 8 Jardinero central (Center fielder)
- 9 Jardinero derecho (Right fielder)

![posiciones](https://github.com/alejandromaselli/ExamenFinalBD/blob/master/images/Baseball_positions.svg)

Primero Filtrar los equipos para poder identificar el teamID del equipo deseado

```SQL
SELECT * FROM `teams` where name LIKE 'Boston%' and name LIKE '%Sox';
```
```SQL

SELECT teamID FROM `teams` where name LIKE 'Boston%' and name LIKE '%Sox';
```
Podemos ver que el teamID es **BOS**

Usamos la tabla `Appereances` como la palabra lo indica son "Apariciones" y esta tabla nos dice la posición en la que juega el jugador en diferentes posiciones con los siguientes campos:

| G_p | G_c | G_1b | G_2b | G_3b | G_ss | G_lf | G_cf | G_rf | G_of|           
| ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |		
|Games as pitcher|Games as catcher|Games as firstbaseman|Games as secondbaseman|Games as thirdbaseman|Games as shortstop|Games as leftfielder|Games as centerfielder|Games as right fielder|Games as outfielder|

```SQL
SELECT * FROM Appereances;
```
Haremos un **`JOIN`** con la tabla people para obtener información del jugador cono su "Nombre Dado" o **Name Given**

```SQL
SELECT * FROM appearances a
INNER JOIN people p
ON a.playerID = p.playerID
```

Luego filtraremos los jugadores y añadiremos la cláusula `WHERE` y como condicional tiene que resultar todos los registros relacionados a nuestro equipo  con el `teamID = 'BOS'` y le añadimos alias a las dos tablas para poder manipularlas mejor enel futuro.

```SQL
SELECT * FROM appearances a
INNER JOIN people p
ON a.playerID = p.playerID
WHERE teamID = 'BOS'
```

Cabe destacar que para ello debemos irnos a la tabla `AwardsPlayer` ya que esta registra los premios que han ganado los mejores jugadores a lo largo de la historia

```SQL
SELECT * FROM AwardsPlayer;
```

Luego con el **`JOIN`** anterior  añadimos un nuevo **JOIN** con la tabla `AwardsPlayer` le añadimos su respectivo alias y entonces obtenemos los jugadores con premio de nuestro equipo.

```SQL
SELECT * FROM appearances a
INNER JOIN people p
on a.playerID = p.playerID
INNER JOIN awardsplayers ap
on p.playerID = ap.playerID
WHERE a.teamID = 'BOS'
```

Añadimos un **`JOIN`** con la tabla `Batting` donde tenemos estos campos:

| playerID| yearID|
| ---- | ---- |
| Player ID code | Year|

**JOIN *resultante:***

```SQL
SELECT * FROM
FROM appearances a
INNER JOIN people p
ON a.playerID = p.playerID
INNER join awardsplayers ap
ON p.playerID = ap.playerID
INNER JOIN batting b
ON ap.playerID = b.playerID
WHERE a.teamID = 'BOS'
```

Luego filtramos los tres **JOINS** completos teniendo en cuenta el `Name Given`,`pitcher`, `catcher`, `firstbaseman`, `secondbaseman`, `thirdbaseman`, `shortstop`, `leftfielder`, `centerfielder`, `right_fielder`, `outfielder`, `designated_hitter`, `pinch_hitter`, `pinch_runner`, `Home Runs`.

```SQL
SELECT p.nameGiven, 
ap.awardID, 
a.G_p  AS pitcher,
a.G_c  AS catcher,
a.G_1b AS firstbaseman,
a.G_2b AS secondbaseman,
a.G_3b AS thirdbaseman,
a.G_ss AS shortstop,
a.G_lf AS leftfielder,
a.G_cf AS centerfielder,
a.G_rf AS right_fielder,
a.G_of AS outfielder,
a.G_dh AS designated_hitter,
a.G_ph AS pinch_hitter,
a.G_pr AS pinch_runner,
b.HR
FROM appearances a
INNER JOIN people p
ON a.playerID = p.playerID
inner join awardsplayers ap
on p.playerID = ap.playerID
INNER JOIN batting b
ON ap.playerID = b.playerID
WHERE a.teamID = 'BOS'
```

Como el resultado del **`JOIN`** filtrado

![Tabla](https://github.com/alejandromaselli/ExamenFinalBD/blob/master/images/resul1.PNG)

Debido a que vemos celdas en donde el valor es 0 lo que significa que hubieron juegos en los que obviamente el jugador no ejerció en determinada posición.

Entonces hacemos un filtrado por posción donde el número sea diferente a `0` respecto a la posición

#### Pitcher -> a.G_p

```SQL
SELECT p.nameGiven, 
ap.awardID, 
a.G_p  as pitcher,
a.G_c  as catcher,
a.G_1b as firstbaseman,
a.G_2b as secondbaseman,
a.G_3b as thirdbaseman,
a.G_ss as shortstop,
a.G_lf as leftfielder,
a.G_cf as centerfielder,
a.G_rf as right_fielder,
a.G_of as outfielder,
a.G_dh as designated_hitter,
a.G_ph as pinch_hitter,
a.G_pr as pinch_runner,
b.HR
FROM appearances a
INNER JOIN people p
on a.playerID = p.playerID
inner join awardsplayers ap
on p.playerID = ap.playerID
INNER JOIN batting b
ON ap.playerID = b.playerID
WHERE a.teamID = 'BOS' AND
a.G_p <> 0
```
Vemos que sigue habiendo celdas con el numero `0` por lo que la *Query* la ajustaremos a cada posición

```SQL
SELECT p.nameGiven, 
ap.awardID, 
a.G_p  as pitcher,
b.HR
FROM appearances a
INNER JOIN people p
on a.playerID = p.playerID
inner join awardsplayers ap
on p.playerID = ap.playerID
INNER JOIN batting b
ON ap.playerID = b.playerID
WHERE a.teamID = 'BOS' AND
a.G_p <> 0
```

### Catcher -> a.G_c

```SQL
SELECT p.nameGiven, 
ap.awardID, 
a.G_c  as catcher,
b.HR
FROM appearances a
INNER JOIN people p
on a.playerID = p.playerID
inner join awardsplayers ap
on p.playerID = ap.playerID
INNER JOIN batting b
ON ap.playerID = b.playerID
WHERE a.teamID = 'BOS' AND
a.G_c <> 0
```

### First Base Man -> a.G_1b

```SQL
SELECT p.nameGiven, 
ap.awardID, 
a.G_1b as firstbaseman,
b.HR
FROM appearances a
INNER JOIN people p
on a.playerID = p.playerID
inner join awardsplayers ap
on p.playerID = ap.playerID
INNER JOIN batting b
ON ap.playerID = b.playerID
WHERE a.teamID = 'BOS' AND
a.G_1b <> 0
```

### Second Base Man -> a.G_2b

```SQL
SELECT p.nameGiven, 
ap.awardID, 
a.G_2b as secondbaseman,
b.HR
FROM appearances a
INNER JOIN people p
on a.playerID = p.playerID
inner join awardsplayers ap
on p.playerID = ap.playerID
INNER JOIN batting b
ON ap.playerID = b.playerID
WHERE a.teamID = 'BOS' AND
a.G_2b <> 0
```

### Third Base Man

```SQL
SELECT p.nameGiven, 
ap.awardID, 
a.G_3b as thirdbaseman,
b.HR
FROM appearances a
INNER JOIN people p
on a.playerID = p.playerID
inner join awardsplayers ap
on p.playerID = ap.playerID
INNER JOIN batting b
ON ap.playerID = b.playerID
WHERE a.teamID = 'BOS' AND
a.G_3b <> 0
```

### Short Stop -> a.G_ss

```SQL
SELECT p.nameGiven, 
ap.awardID, 
a.G_ss as shortstop,
b.HR
FROM appearances a
INNER JOIN people p
on a.playerID = p.playerID
inner join awardsplayers ap
on p.playerID = ap.playerID
INNER JOIN batting b
ON ap.playerID = b.playerID
WHERE a.teamID = 'BOS' AND
a.G_ss <> 0
```

### Left Fielder -> Left Fielder -> a.G_lf

```SQL
SELECT p.nameGiven, 
ap.awardID, 
a.G_lf as leftfielder,
b.HR
FROM appearances a
INNER JOIN people p
on a.playerID = p.playerID
inner join awardsplayers ap
on p.playerID = ap.playerID
INNER JOIN batting b
ON ap.playerID = b.playerID
WHERE a.teamID = 'BOS' AND
a.G_lf <> 0
```

### Center Fielder -> a.G_cf

```SQL
SELECT p.nameGiven, 
ap.awardID, 
a.G_cf as centerfielder,
b.HR
FROM appearances a
INNER JOIN people p
on a.playerID = p.playerID
inner join awardsplayers ap
on p.playerID = ap.playerID
INNER JOIN batting b
ON ap.playerID = b.playerID
WHERE a.teamID = 'BOS' AND
a.G_cf <> 0
```

### Right Fielder -> a.G_rf

```SQL
SELECT p.nameGiven, 
ap.awardID, 
a.G_rf as rightfielder,
b.HR
FROM appearances a
INNER JOIN people p
on a.playerID = p.playerID
inner join awardsplayers ap
on p.playerID = ap.playerID
INNER JOIN batting b
ON ap.playerID = b.playerID
WHERE a.teamID = 'BOS' AND
a.G_rf <> 0
```

### Out Fielder -> a.G_of

```SQL
SELECT p.nameGiven, 
ap.awardID, 
a.G_of as outfielder,
b.HR
FROM appearances a
INNER JOIN people p
on a.playerID = p.playerID
inner join awardsplayers ap
on p.playerID = ap.playerID
INNER JOIN batting b
ON ap.playerID = b.playerID
WHERE a.teamID = 'BOS' AND
a.G_of <> 0
```

### Out Fielder -> a.G_of

```SQL
SELECT p.nameGiven, 
ap.awardID, 
a.G_of as outfielder,
b.HR
FROM appearances a
INNER JOIN people p
on a.playerID = p.playerID
inner join awardsplayers ap
on p.playerID = ap.playerID
INNER JOIN batting b
ON ap.playerID = b.playerID
WHERE a.teamID = 'BOS' AND
a.G_of <> 0
```

