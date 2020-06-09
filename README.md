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
Haremos un **JOIN** con la tabla people para obtener información del jugador cono su "Nombre Dado" o **Name Given**

```SQL
SELECT * FROM appearances a
INNER JOIN people p
on a.playerID = p.playerID
```

Luego filtraremos los jugadores y añadiremos la cláusula `WHERE` y como condicional tiene que resultar todos los registros relacionados a nuestro equipo  con el `teamID = 'BOS'`

```SQL
SELECT * FROM appearances a
INNER JOIN people p
on a.playerID = p.playerID
WHERE teamID = 'BOS'
```

Cabe destacar que para ello debemos irnos a la tabla `AwardsPlayer` ya que esta registra los premios que han ganado los mejores jugadores a lo largo de 
