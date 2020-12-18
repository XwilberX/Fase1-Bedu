# Busqueda de patrones 
## Reto 1
### 1. ¿Qué artículos incluyen la palabra Pasta en su nombre?
```sql
SELECT *
FROM articulo;

SELECT * 
FROM  articulo
WHERE nombre LIKE '%Pasta%';
```

### 2. ¿Qué artículos incluyen la palabra Cannelloni en su nombre?
```sql
SELECT *
FROM  articulo;

SELECT *
FROM articulo
WHERE nombre LIKE '%Cannelloni%';
```

### 3. ¿Qué nombres están separados por un guión (-) por ejemplo Puree - Kiwi?
```sql
SELECT * 
FROM articulo;

SELECT * 
FROM articulo
WHERE nombre LIKE '% - %';
```

## Reto 2
### 1. ¿Cuál es el promedio de salario de los puestos?
```sql
SELECT * 
FROM puesto;

SELECT AVG(salario) as promedio
FROM puesto;
```

### 2. ¿Cuántos artículos incluyen la palabra Pasta en su nombre?

```sql
SELECT * 
FROM  articulo;

SELECT count(*) as total
FROM articulo
WHERE nombre LIKE '%pasta%';
```

### 3. ¿Cuál es el salario mínimo y máximo?
```sql
SELECT *
FROM puesto;

SELECT MAX(salario) as maximo, MIN(salario) as minimo
FROM puesto;
```

### 4. Cuál es la suma del salario de los últimos cinco puestos agregados?
```sql
SELECT *
FROM puesto;

SELECT max(id_puesto) - 5
FROM puesto;

SELECT SUM(salario)
FROM puesto
WHERE id_puesto BETWEEN 996 AND 1000;
```
## Reto 3
### 1. ¿Cuántos registros hay por cada uno de los puestos?
```sql
SELECT *
FROM puesto;

SELECT nombre, COUNT(*) as cantidad
FROM puesto
GROUP BY nombre;
```

### 2. ¿Cuánto dinero se paga en total por puesto?
```sql
SELECT *
FROM puesto;

SELECT nombre, SUM(salario) total
FROM puesto
GROUP BY nombre;
```

### 3. ¿Cuál es el número total de ventas por vendedor?
```sql
SELECT *
FROM venta;

SELECT id_empleado , COUNT(clave) as total_ventas 
FROM venta
GROUP BY id_empleado;
```
### 4. ¿Cuál es el número total de ventas por artículo?
```sql
SELECT *
FROM venta;

SELECT id_articulo, COUNT(*) as total_ventas 
FROM venta 
GROUP BY id_articulo;
```

## Reto 4
### 1. ¿Cuál es el nombre de los empleados cuyo sueldo es menor a $10,000?
```sql
SELECT id_puesto 
FROM puesto 
WHERE salario > 10000

SELECT CONCAT(nombre, ' ', apellido_paterno, ' ', apellido_materno) as nombre_completo
FROM empleado
WHERE id_puesto IN
	(SELECT id_puesto 
	 FROM puesto 
	 WHERE salario > 10000);
```

### 2. ¿Cuál es la cantidad mínima y máxima de ventas de cada empleado?
```sql
SELECT clave, id_empleado , COUNT(*) as total_ventas 
FROM venta
GROUP BY clave, id_empleado;

# al parecer creo que con consultas similares, me quede con un poco de dudas

SELECT clave, id_empleado , COUNT(clave) as total_ventas 
FROM venta
GROUP BY clave, id_empleado;

SELECT id_empleado, MIN(total_ventas), MAX(total_ventas) 
FROM 
	(SELECT clave, id_empleado , COUNT(*) as total_ventas 
	 FROM venta
	 GROUP BY clave, id_empleado) AS subq
GROUP BY id_empleado;
```

### 3. ¿Cuál es el nombre del puesto de cada empleado? 
```sql
SELECT CONCAT(nombre,' ', apellido_paterno, ' ', apellido_materno) AS nombre_completo, 
	  (SELECT nombre FROM puesto WHERE id_puesto = e.id_puesto) AS puesto
FROM empleado e;
```
# Ejercicios Sesión 2
### 1. Dentro de la tabla employees, obten el número de empleado, apellido y nombre de todos los empleados cuyo nombre empiece con A.
```sql
use classicmodels;

SELECT employeeNumber, lastName, firstName
FROM employees
WHERE firstName LIKE 'A%';
```
### 2. Dentro de la tabla employees, obten el número de empleado, apellido y nombre de todos los empleados cuyo apellido termina con on.
```sql
SELECT employeeNumber, lastName, firstName 
FROM employees 
WHERE lastName LIKE '%on';
```
### 3. Dentro de la tabla employees, obten el número de empleado, apellido y nombre de todos los empleados cuyo nombre incluye la cadena on.
```sql
SELECT employeeNumber, lastName, firstName
FROM employees 
WHERE firstName LIKE '%on%';
```
### 4. Dentro de la tabla employees, obten el número de empleado, apellido y nombre de todos los empleados cuyos nombres tienen seis letras e inician con G.
```sql
SELECT employeeNumber, lastName, firstName
FROM employees
WHERE firstName LIKE 'G_____';
```
### 5. Dentro de la tabla employees, obten el número de empleado, apellido y nombre de todos los empleados cuyo nombre no inicia con B.
```sql
SELECT employeeNumber, lastName, firstName
FROM employees
WHERE firstName NOT LIKE 'B%';
```
### 6. Dentro de la tabla products, obten el código de producto y nombre de los productos cuyo código incluye la cadena _20.
```sql
SELECT id_articulo, nombre
FROM articulo
WHERE id_articulo LIKE '%_20%'; 
```
### 7. Dentro de la tabla orderdetails, obten el total de cada orden.
```sql
SELECT SUM(priceEach) AS TOTAL 
FROM orderdetails 
GROUP BY orderNumber;
```
### 8. Dentro de la tabla orders obten el número de órdenes por año.
```sql
SELECT year(orderDate) as year, count(orderNumber)
FROM orders
GROUP BY year
ORDER BY year;
```
### 9. Obten el apellido y nombre de los empleados cuya oficina está ubicada en USA.
```sql
SELECT lastName, firstName
FROM employees
WHERE officeCode IN 
	(SELECT officeCode 
	FROM offices
	WHERE country = 'USA');
```
### 10. Obten el número de cliente, número de cheque y cantidad del cliente que ha realizado el pago más alto.
```sql
SELECT customerNumber, checkNumber, amount
FROM payments
WHERE amount = 
	(SELECT max(amount) 
	 FROM payments);
```
### 11. Obten el número de cliente, número de cheque y cantidad de aquellos clientes cuyo pago es más alto que el promedio.
```sql
SELECT customerNumber, checkNumber, amount
FROM payments
WHERE amount > 
	(SELECT avg(amount) 
	 FROM payments);
```
### 12. Obten el nombre de aquellos clientes que no han hecho ninguna orden.
```sql
SELECT customerName
FROM customers
WHERE customerNumber NOT IN 
	(SELECT customerNumber 
	 FROM orders);
```
### 13. Obten el máximo, mínimo y promedio del número de productos en las órdenes de venta.
```sql
SELECT MAX(quantityOrdered), MIN(quantityOrdered), AVG(quantityOrdered)
FROM orderdetails;
```
### 14. Dentro de la tabla orders, obten el número de órdenes que hay por cada estado.
```sql
SELECT status, count(*)
FROM orders
GROUP BY status;
```
