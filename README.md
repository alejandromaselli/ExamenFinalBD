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

Primero Filtrar los equipos para poder identificar el deseado

`
SELECT * FROM `teams` where name LIKE 'Boston%' and name LIKE '%Sox';
SELECT teamID FROM `teams` where name LIKE 'Boston%' and name LIKE '%Sox';
`
