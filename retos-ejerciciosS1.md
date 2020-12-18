# Sesión 1: Fundamentos de SQL
## Reto 1: Estructura de una tabla
### 1. 
| Tipo   | Descripción |
|---|---|
|  int | numero entero  |
|  varchar | cadena de caracteres  |
|  Double  | Número con coma flotante o decimal  |
|  timestamp | Formato de fecha  |

## Reto 2
### 1. ¿Cuál es el nombre de los empleados con el puesto 4?
```sql
SELECT nombre
FROM empleado
WHERE id_puesto = 4;
```
### 2. ¿Qué puestos tienen un salario mayor a $10,000?
```sql
SELECT *
FROM puesto
WHERE salario > 10000;
```
### 3. ¿Qué articulos tienen un precio mayor a $1,000 y un iva mayor a 100?
```sql
SELECT *
FROM articulo
WHERE precio > 1000
    AND iva > 100;
```
### 4. ¿Qué ventas incluyen los artículos 135 o 963 y fueron hechas por los empleados 835 o 369?
```sql
SELECT * 
FROM venta
WHERE id_articulo IN (135, 963)
    AND id_empleado IN (835, 369);
```
## Reto 3: Ordenamientos y Límites
### 1. Usando la base de datos tienda, escribe una consulta que permita obtener el top 5 de puestos por salarios.
```sql
SELECT *
FROM puesto
ORDER BY salario DESC
LIMIT 5;
```

# Ejercicios Sesión 1
```sql
# 1
USE classicmodels;
DESCRIBE employees;

# 2
SELECT lastName
FROM employees;

# 3
SELECT lastName, firstName, jobTitle
FROM employees;

# 4
SELECT *
FROM employees;

#5
SELECT lastName, firstName, jobTitle
FROM employees 
WHERE jobTitle = 'Sales Rep';

#6
SELECT lastName, firstName, jobTitle, officeCode
FROM employees 
WHERE jobTitle = 'Sales Rep' 
    AND officeCode = 1;

#7
SELECT lastName, firstName, jobTitle, officeCode
FROM employees 
WHERE jobTitle = 'Sales Rep' 
    OR officeCode = 1;

#8
SELECT lastName, firstName, officeCode
FROM employees 
WHERE officeCode IN (1, 2, 3);

#9
SELECT lastName, firstName, jobTitle
FROM employees 
WHERE NOT jobTitle = 'Sales Rep';
 # OR
SELECT lastName, firstName, jobTitle
FROM employees 
WHERE jobTitle <> 'Sales Rep';

#10
SELECT lastName, firstName, officeCode
FROM employees 
WHERE officeCode > 5; 

#11
SELECT lastName, firstName, officeCode
FROM employees 
WHERE officeCode <= 4; 

#12
SELECT customerName, country, state
FROM customers 
WHERE country = 'USA' 
    AND state = 'CA'; 

#13
SELECT customerName, country, state, creditLimit
FROM customers
WHERE creditLimit > 100000;

#14
SELECT customerName, country
FROM customers
WHERE country IN ('USA', 'France');

#15
SELECT customerName, country, creditLimit 
FROM customers
WHERE country IN ('USA','France')
    AND creditLimit > 100000;

#16
SELECT officeCode, city, phone, country
FROM offices 
WHERE country IN ('USA', 'France');

#17
SELECT officeCode,city,phone,country 
FROM offices 
WHERE country != 'USA' AND country != 'France';

#18
SELECT orderNumber, customerNumber, status, shippedDate 
FROM orders 
WHERE orderNumber IN (10165, 10287, 10310);

#19
SELECT contactLastName, customerName
FROM customers
ORDER BY contactLastName;

#20
SELECT contactFirstName, customerName
FROM customers
ORDER BY contactFirstName DESC;

#21
SELECT contactLastName, contactFirstName 
FROM customers ORDER BY contactLastName DESC; 

SELECT contactLastName, contactFirstName 
FROM customers 
ORDER BY contactFirstName;

#22
SELECT customerNumber, customerName, creditLimit
FROM customers
ORDER BY creditLimit DESC
LIMIT 5;

#23
SELECT customerNumber, customerName, creditLimit
FROM customers
WHERE creditLimit != 0
ORDER BY creditLimit LIMIT 5;
```