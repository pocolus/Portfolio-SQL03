# Portfolio-SQL03

**•	NOTA:** Esta base de datos, hace parte de los Ejercicios: Realización de consultas SQL Apuntes de BD para DAW, DAM y ASIR José Juan Sánchez Hernández Curso 2023/2024. Disponibles en el [link](https://josejuansanchez.org/bd/ejercicios-consultas-sql/index.html#tienda-de-inform%C3%A1tica). Se utilizo con el objeto de poder practicar consultas del lenguaje SQL.

**•	TITULO: TIENDA INFORMATICA.**  

**•	DESCRIPCION DEL PROYECTO:** En esta base de datos podemos encontrar contenido de una tienda que vende productos para computadoras. Basicamente aca vemos la relacion de los diferentes productos, con los fabricantes de dichos productos. Esta base de datos almacena esta informacion, para poder conocer los fabricantes que mas productos manufacturan y sus costos que permitan tomar mejores decisiones para la tienda.

**•	OBJETIVOS:**
Monitoreo de inventarios y costos: Facilitar el control de inventarios y la gestión de costos, permitiendo obtener información sobre los productos disponibles y sus respectivos fabricantes.

Optimización de proveedores: Analizar qué fabricantes proveen productos más económicos o con mejor relación calidad-precio, ayudando a optimizar las relaciones comerciales con proveedores.

Identificar fabricantes más productivos: Analizar qué fabricantes tienen más productos asociados, permitiendo identificar los más activos en cuanto a volumen de manufactura.

**•	HERRAMIENTAS O LENGUAJES:** Básicamente para este proyecto utilizamos la herramienta SQL Server, en donde hicimos creacion de tablas, insercion de datos, consultas, subconsultas y joins.

**•	CONJUNTO DE DATOS:** Esta base de datos, se compone de dos tablas que son: Producto y fabricante. A pesar de contar solo con dos tablas, podemos hacer una analisis fuerte y robusto, para asi poder tener un mejor desarrollo para la tienda.

**•	DESARROLLO-EJECUCION:**

![Der](https://github.com/pocolus/Portfolio-SQL03/blob/main/Der.png)

**1. CREAMOS LA BASE DE DATOS**
```sql
DROP DATABASE IF EXISTS tienda;
CREATE DATABASE tienda;
USE tienda;
```

**2. CREACION DE TABLAS**
```sql
-- 2.1 CREAMOS LA TABLA FABRICANTE
DROP TABLE IF EXISTS fabricante;
CREATE TABLE fabricante (
  id INT identity (1,1) PRIMARY KEY, -- IDENTITY(1,1) reemplaza a AUTO_INCREMENT en sql server
  nombre VARCHAR(100) NOT NULL
);

-- 2.2 CREAMOS LA TABLA PRODUCTO
DROP TABLE IF EXISTS producto;
CREATE TABLE producto (
  id INT identity (1,1) PRIMARY KEY,
  nombre VARCHAR(100) NOT NULL,
  precio float NOT NULL, -- Float, en vez de double
  id_fabricante INT NOT NULL,
  FOREIGN KEY (id_fabricante) REFERENCES fabricante(id)
);
```

**3. INSERCION DE ARCHIVOS**
```sql
-- 3.1 INSERCION DE DATOS PARA LA TABLA FABRICANTE
SET IDENTITY_INSERT fabricante on; -- se usa porque use en la creacion de la tabla IDENTITY(1,1) reemplaza a AUTO_INCREMENT en sql server
INSERT INTO fabricante (id, nombre) VALUES(1, 'Asus');
INSERT INTO fabricante (id, nombre) VALUES(2, 'Lenovo');
INSERT INTO fabricante (id, nombre) VALUES(3, 'Hewlett-Packard');
INSERT INTO fabricante (id, nombre) VALUES(4, 'Samsung');
INSERT INTO fabricante (id, nombre) VALUES(5, 'Seagate');
INSERT INTO fabricante (id, nombre) VALUES(6, 'Crucial');
INSERT INTO fabricante (id, nombre) VALUES(7, 'Gigabyte');
INSERT INTO fabricante (id, nombre) VALUES(8, 'Huawei');
INSERT INTO fabricante (id, nombre) VALUES(9, 'Xiaomi');
SET IDENTITY_INSERT fabricante OFF; -- lo desactivamos

-- 3.2 INSERCION DE DATOS PARA LA TABLA PRODUCTO
SET IDENTITY_INSERT producto on; -- se usa porque use en la creacion de la tabla IDENTITY(1,1) reemplaza a AUTO_INCREMENT en sql server
INSERT INTO producto (id, nombre, precio, id_fabricante) VALUES(1, 'Disco duro SATA3 1TB', 86.99, 5);
INSERT INTO producto (id, nombre, precio, id_fabricante) VALUES(2, 'Memoria RAM DDR4 8GB', 120, 6);
INSERT INTO producto (id, nombre, precio, id_fabricante) VALUES(3, 'Disco SSD 1 TB', 150.99, 4);
INSERT INTO producto (id, nombre, precio, id_fabricante) VALUES(4, 'GeForce GTX 1050Ti', 185, 7);
INSERT INTO producto (id, nombre, precio, id_fabricante) VALUES(5, 'GeForce GTX 1080 Xtreme', 755, 6);
INSERT INTO producto (id, nombre, precio, id_fabricante) VALUES(6, 'Monitor 24 LED Full HD', 202, 1);
INSERT INTO producto (id, nombre, precio, id_fabricante) VALUES(7, 'Monitor 27 LED Full HD', 245.99, 1);
INSERT INTO producto (id, nombre, precio, id_fabricante) VALUES(8, 'Portátil Yoga 520', 559, 2);
INSERT INTO producto (id, nombre, precio, id_fabricante) VALUES(9, 'Portátil Ideapd 320', 444, 2);
INSERT INTO producto (id, nombre, precio, id_fabricante) VALUES(10, 'Impresora HP Deskjet 3720', 59.99, 3);
INSERT INTO producto (id, nombre, precio, id_fabricante) VALUES(11, 'Impresora HP Laserjet Pro M26nw', 180, 3);
SET IDENTITY_INSERT producto OFF; -- lo desactivamos
```

# Consultas Base De Datos Tienda Informatica

**1.1.3 Consultas sobre una tabla**
1. Lista el nombre de todos los productos que hay en la tabla producto
```sql
select nombre
from producto;
```
2. Lista los nombres y los precios de todos los productos de la tabla producto.
```sql
select nombre, precio
from producto;
```
3. Lista todas las columnas de la tabla producto
```sql
select *
from producto;
```
4. Lista el nombre de los productos, el precio en euros y el precio en dólares estadounidenses (USD).
```sql
select nombre, precio as Precio_Euros, precio * 1.15 as Precio_Us
from producto;
```
5. Lista el nombre de los productos, el precio en euros y el precio en dólares estadounidenses (USD). 
Utiliza los siguientes alias para las columnas: nombre de producto, euros, dólares.
```sql
select nombre as Nombre_Producto, precio as Euros, precio * 1.15 as Dolares
from producto;
```
6. Lista los nombres y los precios de todos los productos de la tabla producto, convirtiendo los nombres a mayúscula.
```sql
select UPPER (nombre) as nombre, precio
from producto;
```
7. Lista los nombres y los precios de todos los productos de la tabla producto, convirtiendo los nombres a minúscula.
```sql
select precio, LOWER (nombre) as Nombres
from producto; 
```
8. Lista el nombre de todos los fabricantes en una columna, y en otra columna obtenga en mayúsculas
los dos primeros caracteres del nombre del fabricante.
```sql
select nombre, UPPER(substring(nombre, 1,2)) as Iniciales_Mayusculas -- substring, sustraer
from producto;
```
9. Lista los nombres y los precios de todos los productos de la tabla producto, redondeando el valor del precio.
```sql
select nombre, ROUND (precio, 0) as precio_Redondeado
from producto;
```
10. Lista los nombres y los precios de todos los productos de la tabla producto, 
truncando el valor del precio para mostrarlo sin ninguna cifra decimal.
```sql
select nombre, round (precio, 0, 1) as Precio_Truncado -- 0 es sin decimal y el 1 truncar, mas no redondear
from producto;
```
11. Lista el identificador de los fabricantes que tienen productos en la tabla producto.
```sql
select id
from fabricante
where id  in (select id_fabricante from producto)

select distinct fabricante.id
from fabricante
join producto
on fabricante.id = producto.id_fabricante

select id
from fabricante
where exists (select id_fabricante from producto
where fabricante.id = producto.id_fabricante)
```
12. Lista el identificador de los fabricantes que tienen productos en la tabla producto, 
eliminando los identificadores que aparecen repetidos.
```sql
select distinct id_fabricante
from producto;
```
13. Lista los nombres de los fabricantes ordenados de forma ascendente.
```sql
select nombre
from fabricante
order by 1;
```
14. Lista los nombres de los fabricantes ordenados de forma descendente.
```sql
select nombre
from fabricante
order by 1 desc;
```
15. Lista los nombres de los productos ordenados en primer lugar por el nombre de forma ascendente
y en segundo lugar por el precio de forma descendente.
```sql
select nombre, precio
from producto
order by nombre asc, precio desc;
```
16. Devuelve una lista con las 5 primeras filas de la tabla fabricante.
```sql
select top 5 *
from fabricante;
```
17. Devuelve una lista con 2 filas a partir de la cuarta fila de la tabla fabricante. 
La cuarta fila también se debe incluir en la respuesta.
```sql
SELECT *
FROM fabricante
ORDER BY id
OFFSET 3 ROWS   -- Omite las primeras tres filas (comienza desde la cuarta fila)
FETCH NEXT 2 ROWS ONLY;  -- Trae las siguientes dos filas (incluye la cuarta y la quinta)
```
18. Lista el nombre y el precio del producto más barato. (Utilice solamente las cláusulas ORDER BY y LIMIT)
```sql
select top 1 nombre, precio
from producto
order by precio;
```
19. Lista el nombre y el precio del producto más caro. (Utilice solamente las cláusulas ORDER BY y LIMIT)
```sql
select top 1 nombre, precio
from producto
order by precio desc;
```
20. Lista el nombre de todos los productos del fabricante cuyo identificador de fabricante es igual a 2.
```sql
select nombre, id_fabricante
from producto
where id_fabricante = 2;
```
21. Lista el nombre de los productos que tienen un precio menor o igual a 120€.
```sql
select nombre, precio
from producto
where precio <= 120;
```
22. Lista el nombre de los productos que tienen un precio mayor o igual a 400€.
```sql
select nombre, precio
from producto
where precio >= 400;
```
23. Lista el nombre de los productos que no tienen un precio mayor o igual a 400€.
```sql
select nombre, precio
from producto
where not precio  >= 400
```
24. Lista todos los productos que tengan un precio entre 80€ y 300€. Sin utilizar el operador BETWEEN.
```sql
select nombre, precio 
from producto
where precio >= 80 and precio <= 300;
```
25. Lista todos los productos que tengan un precio entre 60€ y 200€. Utilizando el operador BETWEEN.
```sql
select nombre, precio
from producto
where precio between 60 and 200;
```
26. Lista todos los productos que tengan un precio mayor que 200€ y que el identificador de fabricante sea igual a 6.
```sql
select id_fabricante, nombre, precio
from producto
where precio > 200 and id_fabricante = 6;
```
27. Lista todos los productos donde el identificador de fabricante sea 1, 3 o 5. Sin utilizar el operador IN.
```sql
select *
from producto
where id_fabricante = 1 or id_fabricante= 3 or id_fabricante = 5
```
28 Lista todos los productos donde el identificador de fabricante sea 1, 3 o 5. Utilizando el operador IN.
```sql
select *
from producto
where id_fabricante in (1,3,5);
```
29. Lista el nombre y el precio de los productos en céntimos (Habrá que multiplicar por 100 el valor del precio). 
Cree un alias para la columna que contiene el precio que se llame céntimos.
```sql
select nombre, precio, precio * 100 as Centimos
from producto;
```
30. Lista los nombres de los fabricantes cuyo nombre empiece por la letra S.
```sql
select nombre
from fabricante
where nombre like 's%';
```
31. Lista los nombres de los fabricantes cuyo nombre termine por la vocal e.
```sql
select nombre
from fabricante
where nombre like '%e';
```
32. Lista los nombres de los fabricantes cuyo nombre contenga el carácter w.
```sql
select nombre
from fabricante
where nombre like '%w%'
```
33. Lista los nombres de los fabricantes cuyo nombre sea de 4 caracteres.
```sql
select nombre
from fabricante
where len (nombre) = 4; -- En mysql: CHAR_LENGTH(nombre) = 4;
```
34. Devuelve una lista con el nombre de todos los productos que contienen la cadena Portátil en el nombre.
```sql
select nombre
from producto
where nombre like '%Portátil%'
```
35. Devuelve una lista con el nombre de todos los productos que contienen 
la cadena Monitor en el nombre y tienen un precio inferior a 215 €.
```sql
select nombre, precio
from producto
where nombre like '%monitor%' and precio < 215;
```
36. Lista el nombre y el precio de todos los productos que tengan un precio mayor o igual a 180€. 
Ordene el resultado en primer lugar por el precio (en orden descendente) y en segundo lugar por el nombre (en orden ascendente).
```sql
select nombre, precio
from producto
where precio >= 180
order by precio desc, nombre asc;
```

**1.1.4 Consultas multitabla (Composición interna)**
1. Devuelve una lista con el nombre del producto, precio y nombre de fabricante de todos los productos de la base de datos.
```sql
select producto.nombre as Producto, precio, fabricante.nombre as Fabricante
from producto
inner join fabricante
on producto.id_fabricante = fabricante.id;
```
2. Devuelve una lista con el nombre del producto, precio y nombre de fabricante de todos los productos de la base de datos. 
Ordene el resultado por el nombre del fabricante, por orden alfabético.
```sql
select producto.nombre as Producto, precio, fabricante.nombre as Fabricante
from producto
inner join fabricante
on producto.id_fabricante = fabricante.id
order by 3;
```
3. Devuelve una lista con el identificador del producto, nombre del producto, identificador del fabricante y nombre del fabricante, 
de todos los productos de la base de datos.
```sql
select producto.id, producto.nombre as Producto, id_fabricante, fabricante.nombre as Fabricante
from producto
inner join fabricante
on producto.id_fabricante = fabricante.id;
```
4. Devuelve el nombre del producto, su precio y el nombre de su fabricante, del producto más barato.
```sql
select top 1 producto.nombre as Producto, precio, fabricante.nombre as Fabricante
from producto
inner join fabricante
on producto.id_fabricante = fabricante.id
order by precio;

select producto.nombre as Producto, precio, fabricante.nombre as Fabricante
from producto
inner join fabricante
on producto.id_fabricante = fabricante.id
where precio in (select MIN(precio) from producto);
```
5. Devuelve el nombre del producto, su precio y el nombre de su fabricante, del producto más caro.
```sql
select top 1 producto.nombre as Producto, precio, fabricante.nombre as Fabricante
from producto
inner join fabricante
on producto.id_fabricante = fabricante.id
order by precio desc;

select producto.nombre as Producto, precio, fabricante.nombre as Fabricante
from producto
inner join fabricante
on producto.id_fabricante = fabricante.id
where precio in (select max(precio) from producto);
```
6. Devuelve una lista de todos los productos del fabricante Lenovo.
```sql
select producto.nombre as Producto, fabricante.nombre as Fabricante
from producto
inner join fabricante
on producto.id_fabricante = fabricante.id
where fabricante.nombre = 'lenovo';
```
7. Devuelve una lista de todos los productos del fabricante Crucial que tengan un precio mayor que 200€.
```sql
select * 
from producto
join fabricante
on producto.id_fabricante = fabricante.id
where fabricante.nombre = 'crucial' and precio > 200;
```
8. Devuelve un listado con todos los productos de los fabricantes Asus, Hewlett-Packardy Seagate. Sin utilizar el operador IN.
```sql
select producto.nombre as Producto, fabricante.nombre as Fabricante
from producto
join fabricante
on producto.id_fabricante = fabricante.id
where fabricante.nombre = 'asus' or fabricante.nombre = 'Hewlett-Packard' or fabricante.nombre = 'seagate';
```









