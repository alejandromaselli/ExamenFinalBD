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

Veremos la posició del Bateador que sería el 
