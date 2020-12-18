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
## 1. Obtén la cantidad de productos de cada orden.
```sql
SELECT o.orderNumber, sum(quantityOrdered)
FROM orders o
JOIN orderdetails od
  ON o.orderNumber = od.orderNumber
GROUP BY o.orderNumber;
```
## 2. Obten el número de orden, estado y costo total de cada orden.
```sql
SELECT o.orderNumber, o.status, sum(quantityOrdered * priceEach) total
FROM orders o
JOIN orderdetails od
  ON o.orderNumber = od.orderNumber
GROUP BY o.orderNumber, o.status;
```
## 3. Obten el número de orden, fecha de orden, línea de orden, nombre del producto, cantidad ordenada y precio de cada pieza.
```sql
SELECT o.orderNumber, requiredDate, orderLineNumber, p.productName, quantityOrdered, priceEach
FROM orders o
JOIN orderdetails od
  ON o.orderNumber = od.orderNumber
JOIN products p
  ON od.productCode = p.productCode;
```
## 4. Obtén el número de orden, nombre del producto, el precio sugerido de fábrica (msrp) y precio de cada pieza.
```sql
SELECT o.orderNumber, p.productName, MSRP, priceEach
FROM orders o
JOIN orderdetails od
  ON o.orderNumber = od.orderNumber
JOIN products p
  ON od.productCode = p.productCode;
```
## 5. Obtén el número de cliente, nombre de cliente, número de orden y estado de cada orden hecha por cada cliente. ¿De qué nos sirve hacer LEFT JOIN en lugar de JOIN?
```sql
SELECT c.customerNumber, customerName, orderNumber, status
FROM customers c
LEFT JOIN orders o
  ON c.customerNumber = o.customerNumber;
```
## 6. Obtén los clientes que no tienen una orden asociada.
```sql
SELECT c.customerNumber, customerName
FROM customers c
LEFT JOIN orders o
  ON c.customerNumber = o.customerNumber
WHERE orderNumber IS NULL;
```

## 7. Obtén el apellido de empleado, nombre de empleado, nombre de cliente, número de cheque y total, es decir, los clientes asociados a cada empleado.
```sql
SELECT lastName, firstName, customerName, checkNumber, amount
FROM employees e
LEFT JOIN customers c 
ON e.employeeNumber = c.salesRepEmployeeNumber
LEFT JOIN payments ON 
    payments.customerNumber = c.customerNumber
ORDER BY customerName, checkNumber;
```
## 8. Repite los ejercicios 5 a 7 usando RIGHT JOIN. ¿Representan lo mismo? Explica las diferencias en un comentario. Para poner comentarios usa --.
```sql
#5
SELECT c.customerNumber, customerName, orderNumber, status
FROM customers c
RIGHT JOIN orders o
  ON c.customerNumber = o.customerNumber;
#6  
SELECT c.customerNumber, customerName
FROM customers c
RIGHT JOIN orders o
  ON c.customerNumber = o.customerNumber
WHERE orderNumber IS NULL;
#7 
SELECT lastName, firstName, customerName, checkNumber, amount
FROM employees e
RIGHT JOIN customers c 
ON e.employeeNumber = c.salesRepEmployeeNumber
LEFT JOIN payments ON 
    payments.customerNumber = c.customerNumber
ORDER BY customerName, checkNumber;
```
