# Examen Final Bases de Datos I

## Equipo a evaluar

### Boston Red Sox

```
Posiciones
  - Lanzador (Pitcher)
  - Receptor (Catcher)
```

Primero Filtrar los equipos para poder identificar el deseado

```
SELECT * FROM `teams` where name LIKE 'Boston%' and name LIKE '%Sox';
SELECT teamID FROM `teams` where name LIKE 'Boston%' and name LIKE '%Sox';
```
