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
9. Devuelve un listado con todos los productos de los fabricantes Asus, Hewlett-Packardy Seagate. Utilizando el operador IN.
```sql
select producto.nombre as Producto, fabricante.nombre as Fabricante
from producto
join fabricante
on producto.id_fabricante = fabricante.id
where fabricante.nombre in ('Asus', 'Hewlett-Packard', 'Seagate');
```
10. Devuelve un listado con el nombre y el precio de todos los productos de los fabricantes cuyo nombre termine por la vocal e.
```sql
select producto.nombre as Producto, producto.precio, fabricante.nombre as Fabricante
from producto
join fabricante
on producto.id_fabricante = fabricante.id
where fabricante.nombre like '%e';
```
11. Devuelve un listado con el nombre y el precio de todos los productos cuyo nombre de fabricante contenga el carácter w en su nombre.
```sql
select producto.nombre as Producto, precio, fabricante.nombre as Fabricante
from producto
join fabricante
on producto.id_fabricante = fabricante.id
where fabricante.nombre like '%w%';
```
12. Devuelve un listado con el nombre de producto, precio y nombre de fabricante, de todos los productos que tengan un precio mayor
o igual a 180€. Ordene el resultado en primer lugar por el precio (en orden descendente) y en segundo lugar por el nombre (en orden ascendente)
```sql
select producto.nombre as Producto, precio, fabricante.nombre as Fabricante
from producto
join fabricante
on producto.id_fabricante = fabricante.id
where precio >= 180
order by 2 desc, 3 asc;
```
13. Devuelve un listado con el identificador y el nombre de fabricante, solamente de aquellos fabricantes 
que tienen productos asociados en la base de datos.
```sql
select id, nombre
from fabricante
where id in (select producto.id_fabricante from producto);

select id, nombre
from fabricante
where exists (select producto.id_fabricante from producto
where fabricante.id = producto.id_fabricante);

SELECT f.id, f.nombre -- se puede poner tambien Distinct y quitamos el group by
FROM fabricante f
JOIN producto p ON f.id = p.id_fabricante
GROUP BY f.id, f.nombre;
```
**1.1.5 Consultas multitabla (Composición externa)**
Resuelva todas las consultas utilizando las cláusulas LEFT JOIN y RIGHT JOIN.
1. Devuelve un listado de todos los fabricantes que existen en la base de datos, junto con los productos que tiene cada uno de ellos. 
El listado deberá mostrar también aquellos fabricantes que no tienen productos asociados.
```sql
select fabricante.nombre as Fabricante, producto.nombre as Producto
from fabricante
left join producto
on fabricante.id = producto.id_fabricante 
```
2. Devuelve un listado donde sólo aparezcan aquellos fabricantes que no tienen ningún producto asociado.
```sql
select fabricante.nombre as Fabricante, producto.nombre as Producto
from fabricante
left join producto
on fabricante.id = producto.id_fabricante 
where producto.id is null;

select fabricante.nombre as Fabricante
from fabricante
where not exists (select 1 from producto -- se puede poner 1 o * lo reconoce automaticamente
where fabricante.id = producto.id_fabricante);
```
3. Pueden existir productos que no estén relacionados con un fabricante? Justifique su respuesta.
```sql
select fabricante.nombre as Fabricante, producto.nombre as Producto
from producto
left join fabricante
on fabricante.id = producto.id_fabricante 
where fabricante.id is null;
```
 **1.1.6 Consultas resumen**
1. Calcula el número total de productos que hay en la tabla productos.
```sql
select COUNT(id) as Numero_Productos
from producto
```
2. Calcula el número total de fabricantes que hay en la tabla fabricante.
```sql
select COUNT(id) as Total_Fabricantes
from fabricante;
```
3. Calcula el número de valores distintos de identificador de fabricante aparecen en la tabla productos.
```sql
select COUNT( distinct id_fabricante) as Valores_Distintos
FROM producto;
```
4. Calcula la media del precio de todos los productos.
```sql
select ROUND (AVG(precio), 2) as Media_Productos
from producto;
```
5. Calcula el precio más barato de todos los productos.
```sql
select MIN(precio) as Barato
from producto;
```
6. Calcula el precio más caro de todos los productos.
```sql
select Max(precio) as Barato
from producto;
```
7. Lista el nombre y el precio del producto más barato.
```sql
select top 1 nombre, precio
from producto
order by 2;

select nombre, precio
from producto
where precio = ( select MIN(precio) from producto);
```
8. Lista el nombre y el precio del producto más caro.
```sql
select top 1 nombre, precio
from producto
order by 2 desc;

select nombre, precio
from producto
where precio = ( select Max(precio) from producto);
```
9. Calcula la suma de los precios de todos los productos.
```sql
select SUM(precio) as Suma_Productos
from producto;
```
10. Calcula el número de productos que tiene el fabricante Asus.
```sql
select fabricante.nombre, COUNT(producto.id) as Numero_asus
from producto
join fabricante
on producto.id_fabricante = fabricante.id
where fabricante.nombre = 'Asus'
group by fabricante.nombre;
```
11. Calcula la media del precio de todos los productos del fabricante Asus.
```sql
select AVG(precio) as media_asus
from producto
join fabricante
on producto.id_fabricante = fabricante.id
where fabricante.nombre = 'asus';
```
12. Calcula el precio más barato de todos los productos del fabricante Asus.
```sql
select MIN(precio) as Barato_asus
from producto
join fabricante
on producto.id_fabricante = fabricante.id
where fabricante.nombre = 'asus';
```
13. Calcula el precio más caro de todos los productos del fabricante Asus.
```sql
select Max(precio) as Barato_asus
from producto
join fabricante
on producto.id_fabricante = fabricante.id
where fabricante.nombre = 'asus';
```
14. Calcula la suma de todos los productos del fabricante Asus.
```sql
select fabricante.nombre,  SUM(precio) as Suma_Asus
from producto
join fabricante
on producto.id_fabricante = fabricante.id
where fabricante.nombre = 'asus'
group by fabricante.nombre;
```
15. Muestra el precio máximo, precio mínimo, precio medio y el número total de productos que tiene el fabricante Crucial.
```sql
select fabricante.nombre, MAX(precio) as Precio_Max, MIN(precio) as Precio_Minimo, AVG(precio) as Promedio, COUNT(precio) as Numero_Productos
from producto
join fabricante
on producto.id_fabricante = fabricante.id
where fabricante.nombre = 'crucial'
group by fabricante.nombre;
```
16. Muestra el número total de productos que tiene cada uno de los fabricantes.  El listado también debe incluir los fabricantes que no tienen ningún producto.
El resultado mostrará dos columnas, una con el nombre del fabricante y otra con el número de productos que tiene. Ordene el resultado descendentemente por el número de productos.
```sql
select fabricante.nombre, 
COUNT(producto.id) as Numero_Productos
from fabricante
left join producto
on fabricante.id = producto.id_fabricante
group by fabricante.nombre
order by 2 desc;
```
17. Muestra el precio máximo, precio mínimo y precio medio de los productos de cada uno de los fabricantes. El resultado mostrará el nombre del fabricante
junto con los datos que se solicitan.
```sql
select fabricante.nombre as Fabricante,
MAX(precio) as Precio_Maximo,
MIN(precio) as Precio_Minimo,
AVG(precio) as Promedio
from producto
join fabricante
on producto.id_fabricante = fabricante.id
group by fabricante.nombre;
```
18. Muestra el precio máximo, precio mínimo, precio medio y el número total de productos de los fabricantes que tienen un precio medio superior a 200€.
No es necesario mostrar el nombre del fabricante, con el identificador del fabricante es suficiente.
```sql
select fabricante.nombre as Fabricante, fabricante.id,
MAX(precio) as Precio_Maximo,
MIN(precio) as Precio_Minimo,
AVG(precio) as Promedio,
COUNT(producto.id) as Numero_Productos
from producto
join fabricante
on producto.id_fabricante = fabricante.id
group by fabricante.nombre, fabricante.id
having AVG(precio) > 200;
```
19. Muestra el nombre de cada fabricante, junto con el precio máximo, precio mínimo, precio medio y el número total de productos de los fabricantes
que tienen un precio medio superior a 200€. Es necesario mostrar el nombre del fabricante.
```sql
select fabricante.nombre as Fabricante, 
MAX(precio) as Precio_Maximo,
MIN(precio) as Precio_Minimo,
AVG(precio) as Promedio,
COUNT(producto.id) as Numero_Productos
from producto
join fabricante
on producto.id_fabricante = fabricante.id
group by fabricante.nombre
having AVG(precio) > 200;
```
20. Calcula el número de productos que tienen un precio mayor o igual a 180€.
```sql
select producto.nombre, precio,
COUNT(id) as Numero_Producto
from producto
where precio >= 180
group by  producto.nombre, precio;
```
21. Calcula el número de productos que tiene cada fabricante con un precio mayor o igual a 180€.
```sql
select fabricante.nombre, 
COUNT(producto.id) as Numero_Producto
from producto
join fabricante
on producto.id_fabricante = fabricante.id
where precio >= 180
group by  fabricante.nombre;
```
22. Lista el precio medio los productos de cada fabricante, mostrando solamente el identificador del fabricante.
```sql
select fabricante.id as Fabricante,
round (AVG(precio), 2) as Promedio
from  producto
join fabricante
on producto.id_fabricante = fabricante.id
group by fabricante.id;
```
23. Lista el precio medio los productos de cada fabricante, mostrando solamente el nombre del fabricante.
```sql
select fabricante.nombre,
round (AVG(precio), 2) as Promedio
from  producto
join fabricante
on producto.id_fabricante = fabricante.id
group by fabricante.nombre;
```
24. Lista los nombres de los fabricantes cuyos productos tienen un precio medio mayor o igual a 150€.
```sql
select fabricante.nombre, 
AVG(precio) as promedio
from fabricante
join producto
on fabricante.id = producto.id_fabricante
group by fabricante.nombre
having AVG(precio) >= 150;
```
25. Devuelve un listado con los nombres de los fabricantes que tienen 2 o más productos.
```sql
select fabricante.nombre,
COUNT(producto.id) as Numero_Producto
from fabricante
join producto
on fabricante.id = producto.id_fabricante
group by fabricante.nombre
having COUNT(producto.id) >= 2;
```
26. Devuelve un listado con los nombres de los fabricantes y el número de productos que tiene cada uno con un precio superior
o igual a 220 €. No es necesario mostrar el nombre de los fabricantes que no tienen productos que cumplan la condición.
```sql
select fabricante.nombre,
COUNT(producto.id) as Numero_Producto
from fabricante
join producto
on fabricante.id = producto.id_fabricante
where precio >= 220
group by fabricante.nombre
```
27. Devuelve un listado con los nombres de los fabricantes y el número de productos que tiene cada uno con un precio superior
o igual a 220 €. El listado debe mostrar el nombre de todos los fabricantes, es decir, si hay algún fabricante que no tiene productos
con un precio superior o igual a 220€ deberá aparecer en el listado con un valor igual a 0 en el número de productos.
```sql
select fabricante.nombre, 
COUNT(producto.id) as Numero_Productos
from fabricante
left join producto
on fabricante.id = producto.id_fabricante
and precio >= 220
```
28. Devuelve un listado con los nombres de los fabricantes donde la suma del precio de todos sus productos es superior a 1000 €.
```sql
select fabricante.nombre,
sum(precio) as Suma
from fabricante
join producto
on fabricante.id = producto.id_fabricante
group by fabricante.nombre
having sum(precio) > 1000;
```
29. Devuelve un listado con el nombre del producto más caro que tiene cada fabricante. El resultado debe tener tres columnas:
nombre del producto, precio y nombre del fabricante. El resultado tiene que estar ordenado alfabéticamente de menor a mayor
por el nombre del fabricante.
```sql
select fabricante.nombre as Fabricante, producto.nombre as Producto, Precio
from fabricante
join producto
on fabricante.id = producto.id_fabricante
where precio = (select max(precio) from producto
where fabricante.id = producto.id_fabricante)
order by 1;
```
**1.1.7 Subconsultas (En la cláusula WHERE)**
**1.1.7.1 Con operadores básicos de comparación**
1. Devuelve todos los productos del fabricante Lenovo. (Sin utilizar INNER JOIN)
```sql
select nombre
from producto
where producto.id_fabricante in (select id from fabricante
where fabricante.nombre = 'lenovo');
```
2. Devuelve todos los datos de los productos que tienen el mismo precio que el producto más caro del fabricante Lenovo. 
(Sin utilizar INNER JOIN).
```sql
select *
from producto
where precio = ( select MAX(precio) from producto 
where producto.id_fabricante in (select fabricante.id from fabricante
where fabricante.nombre = 'lenovo'));
```
3. Lista el nombre del producto más caro del fabricante Lenovo.
```sql
select nombre
from producto
where precio = (select MAX(precio) from producto
where producto.id_fabricante in (select fabricante.id from fabricante
where fabricante.nombre = 'lenovo'));
```
4. Lista el nombre del producto más barato del fabricante Hewlett-Packard.
```sql
select nombre
from producto
where precio in (select MIN(precio) from producto
where producto.id_fabricante in (select fabricante.id from fabricante
where fabricante.nombre = 'Hewlett-Packard'));
```
5. Devuelve todos los productos de la base de datos que tienen un precio mayor o igual al producto más caro del fabricante Lenovo.
```sql
select nombre, precio
from producto
where precio >= (select MAX(precio) from producto
where producto.id_fabricante in (select fabricante.id from fabricante
where fabricante.nombre = 'lenovo'))
```
6. Lista todos los productos del fabricante Asus que tienen un precio superior al precio medio de todos sus productos.
```sql
select fabricante.nombre as Fabricante, producto.nombre
from fabricante
join producto
on fabricante.id = producto.id_fabricante
where fabricante.nombre = 'asus' --  Lista todos los productos del fabricante Asus
 and 
precio > (select AVG(precio) from producto -- que tienen un precio superior al precio medio de todos sus productos.
where producto.id_fabricante in (select fabricante.id from fabricante
where fabricante.nombre = 'asus'));
```
**1.1.7.2 Subconsultas con ALL y ANY**
7. Devuelve el producto más caro que existe en la tabla producto sin hacer uso de MAX, ORDER BY ni LIMIT.
```sql
SELECT nombre, precio
FROM producto p1
WHERE precio >= ALL (
    SELECT precio
    FROM producto p2
    WHERE p2.precio <> p1.precio
);
```
8. Devuelve el producto más barato que existe en la tabla producto sin hacer uso de MIN, ORDER BY ni LIMIT.
```sql
SELECT nombre, precio
FROM producto p1
WHERE precio <= ALL (
    SELECT precio
    FROM producto p2
    WHERE p2.precio <> p1.precio);
```
9. Devuelve los nombres de los fabricantes que tienen productos asociados. (Utilizando ALL o ANY).
```sql
select nombre
from fabricante
where fabricante.id = any (select producto.id_fabricante from producto);
```
10. Devuelve los nombres de los fabricantes que no tienen productos asociados
```sql
select nombre
from fabricante
where fabricante.id != all (select producto.id_fabricante from producto);
```

**1.1.7.3 Subconsultas con IN y NOT IN**
11. Devuelve los nombres de los fabricantes que tienen productos asociados. (Utilizando IN o NOT IN).
```sql
select nombre
from fabricante
WHERE ID IN (select producto.id_fabricante from producto);
```
12. Devuelve los nombres de los fabricantes que no tienen productos asociados. (Utilizando IN o NOT IN).
```sql
select nombre
from fabricante
WHERE ID not IN (select producto.id_fabricante from producto);
```
**1.1.7.4 Subconsultas con EXISTS y NOT EXISTS**
13. Devuelve los nombres de los fabricantes que tienen productos asociados. (Utilizando EXISTS o NOT EXISTS).
```sql
select nombre
from fabricante
where exists (select producto.id_fabricante from producto
where fabricante.id = producto.id_fabricante);
```
14. Devuelve los nombres de los fabricantes que no tienen productos asociados. (Utilizando EXISTS o NOT EXISTS).
```sql
select nombre
from fabricante
where not exists (select producto.id_fabricante from producto
where fabricante.id = producto.id_fabricante);
```
**1.1.7.5 Subconsultas correlacionadas**
15. Lista el nombre de cada fabricante con el nombre y el precio de su producto más caro.
```sql
select fabricante.nombre, producto.precio
from fabricante
join producto
on fabricante.id = producto.id_fabricante
where precio = (select MAX(precio) from producto
where fabricante.id = producto.id_fabricante);
```
16. Devuelve un listado de todos los productos que tienen un precio mayor o igual a la media de todos los productos de su mismo fabricante.
```sql
SELECT p.nombre AS nombre_producto, p.precio, f.nombre AS nombre_fabricante
FROM producto p
JOIN fabricante f ON p.id_fabricante = f.id
WHERE p.precio >= (
    SELECT AVG(p2.precio)
    FROM producto p2
    WHERE p2.id_fabricante = p.id_fabricante
);
```
17. Lista el nombre del producto más caro del fabricante Lenovo.
```sql
select producto.nombre, precio, fabricante.nombre
from producto
join fabricante
on producto.id_fabricante = fabricante.id
where precio = (select MAX(precio) from producto
where producto.id_fabricante = (select fabricante.id from fabricante
where fabricante.nombre = 'lenovo'));
```
**1.1.8 Subconsultas (En la cláusula HAVING)**
18. Devuelve un listado con todos los nombres de los fabricantes que tienen el mismo número de productos que el fabricante Lenovo.
```sql
select distinct fabricante.nombre
from fabricante
join producto
 on fabricante.id = producto.id_fabricante
where  (select COUNT(*) from producto
where fabricante.id = producto.id_fabricante) =
(
SELECT COUNT(*)
    FROM producto 
    WHERE producto.id_fabricante = (
        SELECT id
        FROM fabricante
        WHERE nombre = 'Lenovo'));
```
