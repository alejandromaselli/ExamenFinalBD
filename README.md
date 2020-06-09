# Examen Final Bases de Datos I

## Equipo a evaluar:

### Boston Red Sox

Posiciones:
- Lanzador (Pitcher)
- Receptor (Catcher)
- Primera base (First baseman)
- Segunda base (Second baseman)
- Tercera base (Third baseman)
- Campocorto o parador en corto (Short stop)
- Jardinero izquierdo (Left fielder)
- Jardinero central (Center fielder)
- Jardinero derecho (Right fielder)

![posiciones](https://github.com/alejandromaselli/ExamenFinalBD/blob/master/images/Baseball_positions.svg)

Primero Filtrar los equipos para poder identificar el teamID del equipo deseado

```SQL
SELECT * FROM `teams` where name LIKE 'Boston%' and name LIKE '%Sox';
SELECT teamID FROM `teams` where name LIKE 'Boston%' and name LIKE '%Sox';
```
Podemos ver que el teamID es **BOS**

Veremos la posició del Bateador que sería el 
