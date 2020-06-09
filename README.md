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

Usamos la tabla `Appereances` como la palabra lo indica son "Apariciones" y esta tabla nos dice la posición en la que juega el jugador

| TITULO1| TITULO2| Titulo3|
| ----- | ---- |
| CONTENIDO COLUMNA 1 | CONTENIDO COLUMNA 2 |

```SQL
SELECT * FROM Appereances;
```
Haremos un **JOIN** con la tabla people para obtener información del jugador cono su "Nombre Dado" o **Name Given**

```SQL
SELECT * FROM appearances a
INNER JOIN people p
on a.playerID = p.playerID
```

Luego filtraremos los jugadores y añadiremos la cláusula `WHERE` y como condicional tiene que resultar todos los registros relacionados a nuestro equipo  con el `teamID`

```SQL
SELECT * FROM appearances a
INNER JOIN people p
on a.playerID = p.playerID
WHERE teamID = 'BOS'
```
