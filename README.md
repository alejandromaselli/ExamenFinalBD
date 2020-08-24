# ANALYSIS OF THE THREE MOST SUITABLE PLAYERS PER POSITION
## Team to be evaluated:

### Boston Red Sox

Posiciones:
-Pitcher
-Catcher
-First baseman
-Second baseman
-Third baseman
-Short stop
-Left fielder
-Center fielder
-Right fielder

![posiciones](https://github.com/alejandromaselli/ExamenFinalBD/blob/master/images/Baseball_positions.svg)

First Filter the teams to be able to identify the teamID of the desired team

```SQL
SELECT * FROM `teams` where name LIKE 'Boston%' and name LIKE '%Sox';
```
```SQL

SELECT teamID FROM `teams` where name LIKE 'Boston%' and name LIKE '%Sox';
```
We can see that the teamID is **BOS**

Usamos la tabla `Appereances` como la palabra lo indica son "Apariciones" y esta tabla nos dice la posición en la que juega el jugador en diferentes posiciones con los siguientes campos:





| G_p | G_c | G_1b | G_2b | G_3b | G_ss | G_lf | G_cf | G_rf | G_of|           
| ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |		
|Games as pitcher|Games as catcher|Games as firstbaseman|Games as secondbaseman|Games as thirdbaseman|Games as shortstop|Games as leftfielder|Games as centerfielder|Games as right fielder|Games as outfielder|

```SQL
SELECT * FROM Appereances;
```
We will make a **`JOIN`** with the people table to get information about the player with his **Name Given**.

```SQL
SELECT * FROM appearances a
INNER JOIN people p
ON a.playerID = p.playerID
```

Then we will filter the players and add the `WHERE` clause and as a conditional it has to be all the records related to our team with the `teamID = 'BOS'` and we add aliases to the two tables to be able to manipulate them better in the future.

```SQL
SELECT * FROM appearances a
INNER JOIN people p
ON a.playerID = p.playerID
WHERE teamID = 'BOS'
```

It should be noted that for this we must go to the table 'AwardsPlayer' as it records the awards that have won the best players throughout history

```SQL
SELECT * FROM AwardsPlayer;
```

Then with the previous **`JOIN`** we add a new **JOIN** with the table `AwardsPlayer` we add their respective alias and then we get the prize players of our team.

```SQL
SELECT * FROM appearances a
INNER JOIN people p
on a.playerID = p.playerID
INNER JOIN awardsplayers ap
on p.playerID = ap.playerID
WHERE a.teamID = 'BOS'
```

We add a **`JOIN`** with the `Batting` table where we have these fields:

| playerID| yearID|
| ---- | ---- |
| Player ID code | Year|

**JOIN *result:***

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

Then we filter the three complete **JOINS** taking into account the `Name Given`,`pitcher`, `catcher`, `firstbaseman`, `secondbaseman`, `thirdbaseman`, `shortstop`, `leftfielder`, `centerfielder`, `right_fielder`, `outfielder`, `designated_hitter`, `pinch_hitter`, `pinch_runner`, `Home Runs`.

Also we'll take some other fields in the join such as the defense, putouts, Assistances, errors, batting. The purpose of these fields is to make an average. The ideal player will have a lower average of errors, relatively a higher average of assistances, and higher average of putouts. Finally we would filter three times all the resulting query to get the best 3 players for each position:


### 1. Catcher -> a.G_c

```SQL
select *  FROM
(
	select *  FROM
	(
		select *  FROM
		(
			SELECT 
			p.nameGiven as Name_Given,
			ap.yearID as Year, 
			ap.awardID,  
			a.G_c as catcher,
			a.G_defense as Defense,
			AVG(f.PO) as putouts_Average,
			AVG(f.A) as Assists_Average,
			AVG(f.E) as errores_Average
			FROM appearances a
			INNER JOIN people p
			on a.playerID = p.playerID
			inner join awardsplayers ap
			on p.playerID = ap.playerID
			INNER JOIN batting b
			ON ap.playerID = b.playerID
			INNER JOIN fielding f
			on p.playerID = f.playerID
			WHERE a.teamID = 'BOS' AND
			a.G_c <> 0
			GROUP BY p.nameGiven
			ORDER BY a.G_c DESC
			LIMIT 20
			) as t1
		ORDER BY errores_Average DESC
		LIMIT 10
		) as t2
	ORDER BY putouts_Average DESC
	LIMIT 5
	) as t3
ORDER BY Assists_Average DESC
LIMIT 3
```


### 2. First Base Man -> a.G_1b

```SQL
select *  FROM
(
	select *  FROM
	(
		select *  FROM
		(
			SELECT 
			p.nameGiven as Name_Given,
			ap.yearID as Year, 
			ap.awardID,  
			a.G_1b as firstbaseman,
			a.G_defense as Defense,
			AVG(f.PO) as putouts_Average,
			AVG(f.A) as Assists_Average,
			AVG(f.E) as errores_Average
			FROM appearances a
			INNER JOIN people p
			on a.playerID = p.playerID
			inner join awardsplayers ap
			on p.playerID = ap.playerID
			INNER JOIN batting b
			ON ap.playerID = b.playerID
			INNER JOIN fielding f
			on p.playerID = f.playerID
			WHERE a.teamID = 'BOS' AND
			a.G_1b <> 0
			GROUP BY p.nameGiven
			ORDER BY a.G_1b DESC
			LIMIT 20
			) as t1
		ORDER BY errores_Average DESC
		LIMIT 10
		) as t2
	ORDER BY putouts_Average DESC
	LIMIT 5
	) as t3
ORDER BY Assists_Average DESC
LIMIT 3
```


### 3. Second Base Man -> a.G_2b

```SQL
select *  FROM
(
	select *  FROM
	(
		select *  FROM
		(
			SELECT 
			p.nameGiven as Name_Given,
			ap.yearID as Year, 
			ap.awardID,  
			a.G_2b as secondbaseman,
			a.G_defense as Defense,
			AVG(f.PO) as putouts_Average,
			AVG(f.A) as Assists_Average,
			AVG(f.E) as errores_Average
			FROM appearances a
			INNER JOIN people p
			on a.playerID = p.playerID
			inner join awardsplayers ap
			on p.playerID = ap.playerID
			INNER JOIN batting b
			ON ap.playerID = b.playerID
			INNER JOIN fielding f
			on p.playerID = f.playerID
			WHERE a.teamID = 'BOS' AND
			a.G_2b <> 0
			GROUP BY p.nameGiven
			ORDER BY a.G_2b DESC
			LIMIT 20
			) as t1
		ORDER BY errores_Average DESC
		LIMIT 10
		) as t2
	ORDER BY putouts_Average DESC
	LIMIT 5
	) as t3
ORDER BY Assists_Average DESC
LIMIT 3
```


### 4. Third Base Man

```SQL
select *  FROM
(
	select *  FROM
	(
		select *  FROM
		(
			SELECT 
			p.nameGiven as Name_Given,
			ap.yearID as Year, 
			ap.awardID,  
			a.G_3b as thirdbaseman,
			a.G_defense as Defense,
			AVG(f.PO) as putouts_Average,
			AVG(f.A) as Assists_Average,
			AVG(f.E) as errores_Average
			FROM appearances a
			INNER JOIN people p
			on a.playerID = p.playerID
			inner join awardsplayers ap
			on p.playerID = ap.playerID
			INNER JOIN batting b
			ON ap.playerID = b.playerID
			INNER JOIN fielding f
			on p.playerID = f.playerID
			WHERE a.teamID = 'BOS' AND
			a.G_3b <> 0
			GROUP BY p.nameGiven
			ORDER BY a.G_3b DESC
			LIMIT 20
			) as t1
		ORDER BY errores_Average DESC
		LIMIT 10
		) as t2
	ORDER BY putouts_Average DESC
	LIMIT 5
	) as t3
ORDER BY Assists_Average DESC
LIMIT 3
```


### 5. Short Stop -> a.G_ss

```SQL
select *  FROM
(
	select *  FROM
	(
		select *  FROM
		(
			SELECT 
			p.nameGiven as Name_Given,
			ap.yearID as Year, 
			ap.awardID,  
			a.G_ss as shortstop,
			a.G_defense as Defense,
			AVG(f.PO) as putouts_Average,
			AVG(f.A) as Assists_Average,
			AVG(f.E) as errores_Average
			FROM appearances a
			INNER JOIN people p
			on a.playerID = p.playerID
			inner join awardsplayers ap
			on p.playerID = ap.playerID
			INNER JOIN batting b
			ON ap.playerID = b.playerID
			INNER JOIN fielding f
			on p.playerID = f.playerID
			WHERE a.teamID = 'BOS' AND
			a.G_ss <> 0
			GROUP BY p.nameGiven
			ORDER BY a.G_ss DESC
			LIMIT 20
			) as t1
		ORDER BY errores_Average DESC
		LIMIT 10
		) as t2
	ORDER BY putouts_Average DESC
	LIMIT 5
	) as t3
ORDER BY Assists_Average DESC
LIMIT 3
```


### 6. Left Fielder -> Left Fielder -> a.G_lf

```SQL
select *  FROM
(
	select *  FROM
	(
		select *  FROM
		(
			SELECT 
			p.nameGiven as Name_Given,
			ap.yearID as Year, 
			ap.awardID,  
			a.G_lf as leftfielder,
			a.G_defense as Defense,
			AVG(f.PO) as putouts_Average,
			AVG(f.A) as Assists_Average,
			AVG(f.E) as errores_Average
			FROM appearances a
			INNER JOIN people p
			on a.playerID = p.playerID
			inner join awardsplayers ap
			on p.playerID = ap.playerID
			INNER JOIN batting b
			ON ap.playerID = b.playerID
			INNER JOIN fielding f
			on p.playerID = f.playerID
			WHERE a.teamID = 'BOS' AND
			a.G_lf <> 0
			GROUP BY p.nameGiven
			ORDER BY a.G_lf DESC
			LIMIT 20
			) as t1
		ORDER BY errores_Average DESC
		LIMIT 10
		) as t2
	ORDER BY putouts_Average DESC
	LIMIT 5
	) as t3
ORDER BY Assists_Average DESC
LIMIT 3
```


### 7. Center Fielder -> a.G_cf

```SQL
select *  FROM
(
	select *  FROM
	(
		select *  FROM
		(
			SELECT 
			p.nameGiven as Name_Given,
			ap.yearID as Year, 
			ap.awardID,  
			a.G_cf as centerfielder,
			a.G_defense as Defense,
			AVG(f.PO) as putouts_Average,
			AVG(f.A) as Assists_Average,
			AVG(f.E) as errores_Average
			FROM appearances a
			INNER JOIN people p
			on a.playerID = p.playerID
			inner join awardsplayers ap
			on p.playerID = ap.playerID
			INNER JOIN batting b
			ON ap.playerID = b.playerID
			INNER JOIN fielding f
			on p.playerID = f.playerID
			WHERE a.teamID = 'BOS' AND
			a.G_cf <> 0
			GROUP BY p.nameGiven
			ORDER BY a.G_cf DESC
			LIMIT 20
			) as t1
		ORDER BY errores_Average DESC
		LIMIT 10
		) as t2
	ORDER BY putouts_Average DESC
	LIMIT 5
	) as t3
ORDER BY Assists_Average DESC
LIMIT 3
```


### 8. Right Fielder -> a.G_rf

```SQL
select *  FROM
(
	select *  FROM
	(
		select *  FROM
		(
			SELECT 
			p.nameGiven as Name_Given,
			ap.yearID as Year, 
			ap.awardID,  
			a.G_rf as rightfielder,
			a.G_defense as Defense,
			AVG(f.PO) as putouts_Average,
			AVG(f.A) as Assists_Average,
			AVG(f.E) as errores_Average
			FROM appearances a
			INNER JOIN people p
			on a.playerID = p.playerID
			inner join awardsplayers ap
			on p.playerID = ap.playerID
			INNER JOIN batting b
			ON ap.playerID = b.playerID
			INNER JOIN fielding f
			on p.playerID = f.playerID
			WHERE a.teamID = 'BOS' AND
			a.G_rf <> 0
			GROUP BY p.nameGiven
			ORDER BY a.G_rf DESC
			LIMIT 20
			) as t1
		ORDER BY errores_Average DESC
		LIMIT 10
		) as t2
	ORDER BY putouts_Average DESC
	LIMIT 5
	) as t3
ORDER BY Assists_Average DESC
LIMIT 3
```


### 9. Out Fielder -> a.G_of

```SQL
select *  FROM
(
	select *  FROM
	(
		select *  FROM
		(
			SELECT 
			p.nameGiven as Name_Given,
			ap.yearID as Year, 
			ap.awardID, 
			a.G_of as outfielder,
			a.G_defense as Defense,
			AVG(f.PO) as putouts_Average,
			AVG(f.A) as Assists_Average,
			AVG(f.E) as errores_Average
			FROM appearances a
			INNER JOIN people p
			on a.playerID = p.playerID
			inner join awardsplayers ap
			on p.playerID = ap.playerID
			INNER JOIN batting b
			ON ap.playerID = b.playerID
			INNER JOIN fielding f
			on p.playerID = f.playerID
			WHERE a.teamID = 'BOS' AND
			a.G_of <> 0
			GROUP BY p.nameGiven
			ORDER BY a.G_of DESC
			LIMIT 20
			) as t1
		ORDER BY errores_Average DESC
		LIMIT 10
		) as t2
	ORDER BY putouts_Average DESC
	LIMIT 5
	) as t3
ORDER BY Assists_Average DESC
LIMIT 3
```
