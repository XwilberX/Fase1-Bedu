# Sesión 3: Joins y Vistas
## Reto 1
### 1. ¿Cuál es el nombre de los empleados que realizaron cada venta?
```sql
SELECT v.clave, CONCAT(e.nombre, ' ', e.apellido_paterno) AS nombre
FROM venta v
JOIN empleado e
  ON v.id_empleado = e.id_empleado
ORDER BY clave;
```
### 2. ¿Cuál es el nombre de los artículos que se han vendido?
```sql
SELECT v.clave, a.nombre
FROM venta v
JOIN articulo a
  ON v.id_articulo = a.id_articulo
ORDER BY clave;
```
### 3. ¿Cuál es el total de cada venta?
```sql
SELECT v.clave, ROUND(SUM(a.precio),2) AS total
FROM venta v
JOIN articulo a
  ON v.id_articulo = a.id_articulo
GROUP BY clave
ORDER BY clave;
```
## Reto 2
---
### 1. Obtener el puesto de un empleado.
```sql
CREATE VIEW puestos_empleados_321 AS
SELECT CONCAT(e.nombre, ' ', e.apellido_paterno, ' ', e.apellido_materno) AS empleado, p.nombre
FROM empleado e
JOIN puesto p
  ON e.id_puesto = p.id_puesto;
```
### 2. Saber qué artículos ha vendido cada empleado.
```sql 
CREATE VIEW ventas_empleado_321 AS
SELECT v.clave, CONCAT(e.nombre, ' ', e.apellido_paterno, ' ', e.apellido_materno) AS nombre_completo, a.nombre AS articulo
FROM venta v
JOIN empleado e
  ON v.id_empleado = e.id_empleado
JOIN articulo a
  ON v.id_articulo = a.id_articulo
ORDER BY v.clave;
```
### 3. Saber qué puesto ha tenido más ventas.
```sql
CREATE VIEW puesto_ventas_321 AS
SELECT p.nombre, COUNT(v.clave) total
FROM venta v
JOIN empleado e
  ON v.id_empleado = e.id_empleado
JOIN puesto p
  ON e.id_puesto = p.id_puesto
GROUP BY p.nombre;

# y de esa vista cresda hacemos una nueva consulta

SELECT *
FROM puesto_ventas_321
ORDER BY total DESC
LIMIT 1;
```
# Ejercicios Sesión 3
