# Sesión 8: Query Competition
## Reto 2: Pandemia A (H1N1)
- ### ¿Cuál fue el país con mayor número de muertes?
```json
{
 filter: {
  Deaths: {
   $ne: null
  },
  Country: {
   $ne: 'Grand Total'
  }
 },
 sort: {
  Deaths: -1
 },
 limit: 1
}
```
- ### ¿Cuál fue el país con menor número de muertes?
```json
{
 filter: {
  Deaths: {
   $ne: NaN
  },
  Country: {
   $ne: 'Grand Total'
  }
 },
 sort: {
  Deaths: 1
 },
 limit: 1
}
```
- ### ¿Cuál fue el país con el mayor número de casos?
```json
{
 filter: {
  Cases: {
   $ne: NaN
  },
  Country: {
   $ne: 'Grand Total'
  }
 },
 sort: {
  Cases: -1
 },
 limit: 1
}
```
- ### ¿Cuál fue el país con el menor número de casos?
```json
{
 filter: {
  Cases: {
   $ne: NaN
  },
  Country: {
   $ne: 'Grand Total'
  }
 },
 sort: {
  Cases: 1
 },
 limit: 1
}
```
- ### ¿Cuál fue el número de muertes promedio?
```json
[{$match: {
  Deaths: {$ne: null},
  Deaths: {$ne: NaN},
  Country: {$ne: "Grand Total"}
}}, {$group: {
  _id: null,
  promedio: {
    $avg: {$sum: "$Deaths"}
  }
}}]
```
- ### ¿Cuál fue el número de casos promedio?
```json
[{$match: {
  Cases: {$ne: null},
  Cases: {$ne: NaN},
  Country: {$ne: "Grand Total"}
}}, {$group: {
  _id: null,
  promedio: {
    $avg: {$sum: "$Cases"}
  }
}}]
```
- ### Top 5 de países con más muertes
```json
{
 filter: {
  Deaths: {
   $ne: NaN
  },
  Country: {
   $ne: 'Grand Total'
  }
 },
 project: {
  _id: 0,
  Country: 1
 },
 sort: {
  Deaths: -1
 },
 limit: 5
}
```

- ### Top 5 de países con menos muertes

```json
{
 filter: {
  Deaths: {
   $ne: NaN
  },
  Country: {
   $ne: 'Grand Total'
  }
 },
 project: {
  _id: 0,
  Country: 1
 },
 sort: {
  Deaths: 1
 },
 limit: 5
}
```
