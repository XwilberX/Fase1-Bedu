# Sesión 4: Configuración de Bases de Datos Locales
## Reto 1
### 1. Definir los campos y tipos de datos para la tabla movies haciendo uso de los archivos movies.dat y README.
```
id INT PRIMARY KEY
titulo VARCHAR(90)
generos VARCHAR(150)
```
### 2. Crear la tabla movies (recuerda usar el mismo nombre del archivo sin la extensión para vincular nombres de tablas con archivos).
```sql
CREATE TABLE IF NOT EXISTS movies (
   id INT PRIMARY KEY, 
   titulo VARCHAR(90), 
   genero VARCHAR(150)
);
```
### 3. Definir los campos y tipos de datos para la tabla ratings haciendo uso de los archivos ratings.dat y README.
```
userid INT
movieid INT
rating INT
time_stamp BIGINT
```
### 4. Crear la tabla ratings (recuerda usar el mismo nombre del archivo sin la extensión para vincular nombres de tablas con archivos)
```sql
CREATE TABLE IF NOT EXISTS ratings (
   rating INT, 
   time_stamp BIGINT,
   userid INT, 
   movieid INT,
   FOREIGN KEY (userid) REFERENCES users(id),
   FOREIGN KEY (movieid) REFERENCES movies(id)
);
```
## Reto 2
---
### 1. Agregamos el encabezado correspondiente a movies.dat y reemplazamos el símbolo :: por ,. Guardamos el archivo como movies.csv
![img1](/img/movies.png)

### 2. Usando como base el archivo ratings.dat, limpiarlo e importar los datos en la tabla ratings creada en el Reto 2.
![img2](/img/raiting.png)
### 3. Finalmente, añade un registro en cada tabla usando INSERT INTO.
```sql
INSERT INTO movies(id,titulo,genero) VALUES (4000,'Interestelar', 'Ciencia-ficcion');

INSERT INTO ratings(userid,movieid,rating,time_stamp) VALUES (7000,4000,1,745105478);
```
## Reto 3
---
### 1. Crear la colección movies
 ![img3](/img/mongouser.png)
### 2. Importar datos a la colección movies desde el archivo movies.csv
![img4](/img/mongomovies.png)
### 3. Crear la colección ratings
![img3](/img/mongouser.png)
### 4. Importar datos a la colección ratings desde el archivo ratings.csv
![img5](/img/mongorating.png)

# Ejercicios
## 1. Agregar los siguientes registros en formato CSV a la Colección movies
![img6](/img/mongoinsert.png)
## 2. Modificar el documento con id=4001 en la Colección movies para que contenga la siguiente información:
![img7](/img/mongoedit.png)


