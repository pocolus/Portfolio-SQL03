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






