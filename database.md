---


---

<h2 id="crear-una-base-de-datos-llamada-call_list">Crear una base de datos llamada call_list</h2>
<pre><code>CREATE DATABASE call_list;
\c call_list;

             List of databases
   Name    |  Owner   | Encoding |   Collate   |    Ctype    |   Access privileges   
-----------+----------+----------+-------------+-------------+-----------------------
 call_list | lumijavi | UTF8     | en_US.UTF-8 | en_US.UTF-8 | 
 lumijavi  | postgres | UTF8     | en_US.UTF-8 | en_US.UTF-8 | 
 movies    | lumijavi | UTF8     | en_US.UTF-8 | en_US.UTF-8 | 
 postgres  | postgres | UTF8     | en_US.UTF-8 | en_US.UTF-8 | 
 template0 | postgres | UTF8     | en_US.UTF-8 | en_US.UTF-8 | =c/postgres          +
           |          |          |             |             | postgres=CTc/postgres
 template1 | postgres | UTF8     | en_US.UTF-8 | en_US.UTF-8 | =c/postgres          +
           |          |          |             |             | postgres=CTc/postgres
(6 rows)
</code></pre>
<h2 id="en-la-base-de-datos-recien-creada-crear-la-tabla-users-con-los-campos-id-clave-primaria-first_name-email.">En la base de datos recien creada, crear la tabla users con los campos id (clave primaria), first_name, email.</h2>
<pre><code>CREATE TABLE users ( id SERIAL PRIMARY KEY, first_name VARCHAR(20), email VARCHAR(20));
</code></pre>
<h2 id="ingresar-un-usuario-llamado-carlos-el-resto-de-los-datos-deben-inventarlos.">Ingresar un usuario, llamado Carlos (el resto de los datos deben inventarlos).</h2>
<pre><code>INSERT INTO users (first_name, email) VALUES ('Carlos', 'carlos@gmail.com');

SELECT * FROM users;

 id | first_name |      email       
----+------------+------------------
  1 | Carlos     | carlos@gmail.com
(1 row)
</code></pre>
<h2 id="ingresar-un-usuario-llamada-laura-el-resto-de-los-datos-deben-inventarlos.">Ingresar un usuario, llamada Laura (el resto de los datos deben inventarlos).</h2>
<pre><code>INSERT INTO users (first_name, email) VALUES ('Laura', 'laura@gmail.com');

SELECT * FROM users;

 id | first_name |      email       
----+------------+------------------
  1 | Carlos     | carlos@gmail.com
  2 | Laura      | laura@gmail.com
(2 rows)
</code></pre>
<h2 id="crear-una-tabla-llamada-calls-con-los-campos-id-clave-primaria-phone-date-user_id-foreign-key-relacionado-a-users-y-length-para-guardar-la-duración-de-la-llamada-como-un-número-entero.">Crear una tabla llamada calls con los campos id (clave primaria), phone, date, user_id (foreign key relacionado a users) y length (para guardar la duración de la llamada) como un número entero.</h2>
<pre><code>CREATE TABLE calls ( id SERIAL PRIMARY KEY, phone VARCHAR(20), date DATE, user_id INTEGER REFERENCES users(id), lenght INTEGER);

SELECT * FROM calls;

 id | phone | date | user_id | lenght 
----+-------+------+---------+--------
</code></pre>
<h2 id="agregar-a-la-tabla-users-el-campo-last_name.">Agregar a la tabla users el campo last_name.</h2>
<pre><code>ALTER TABLE users ADD COLUMN last_name VARCHAR(20);

SELECT * FROM users;

 id | first_name |      email       | last_name 
----+------------+------------------+-----------
  1 | Carlos     | carlos@gmail.com | 
  2 | Laura      | laura@gmail.com  | 
(2 rows)
</code></pre>
<h2 id="modelar-la-base-de-datos-agregar-print-de-pantalla-utilizar-httpswww.draw.io.">Modelar la base de datos (agregar print de pantalla [utilizar <a href="https://www.draw.io/">https://www.draw.io/</a>]).</h2>

<table>
<thead>
<tr>
<th>users &lt;==&gt;&gt;</th>
<th>&lt;==&gt;&gt; calls</th>
</tr>
</thead>
<tbody>
<tr>
<td>ID : serial PK</td>
<td>ID : serial PK</td>
</tr>
<tr>
<td>first_name : varchar</td>
<td>phone : varchar</td>
</tr>
<tr>
<td>email : varchar</td>
<td>date : date</td>
</tr>
<tr>
<td>last_name : varchar</td>
<td>user_id integer FK(users)</td>
</tr>
<tr>
<td>-</td>
<td>length : integer</td>
</tr>
</tbody>
</table><h2 id="ingresar-el-apellido-del-usuario-carlos.">Ingresar el apellido del usuario Carlos.</h2>
<pre><code>UPDATE users SET last_name = 'Perez' WHERE id = 1;

SELECT * FROM users;

 id | first_name |      email       | last_name 
----+------------+------------------+-----------
  2 | Laura      | laura@gmail.com  | 
  1 | Carlos     | carlos@gmail.com | Perez
(2 rows)
</code></pre>
<h2 id="ingresar-el-apellido-del-usuario-laura.">Ingresar el apellido del usuario Laura.</h2>
<pre><code>UPDATE users SET last_name = 'Jara' WHERE id = 2;

SELECT * FROM users;

 id | first_name |      email       | last_name 
----+------------+------------------+-----------
  1 | Carlos     | carlos@gmail.com | Perez
  2 | Laura      | laura@gmail.com  | Jara
(2 rows)
</code></pre>
<h2 id="ingresar-6-llamadas-asociadas-al-usuario-laura.">Ingresar 6 llamadas asociadas al usuario Laura.</h2>
<pre><code>INSERT INTO calls (phone, date, user_id, lenght) VALUES ('+569 89221414', NOW(), 2, 120);
INSERT INTO calls (phone, date, user_id, lenght) VALUES ('+569 89221415', NOW(), 2, 40);
INSERT INTO calls (phone, date, user_id, lenght) VALUES ('+569 89221416', NOW(), 2, 55);
INSERT INTO calls (phone, date, user_id, lenght) VALUES ('+569 89221417', NOW(), 2, 44);
INSERT INTO calls (phone, date, user_id, lenght) VALUES ('+569 89221418', NOW(), 2, 36);
INSERT INTO calls (phone, date, user_id, lenght) VALUES ('+569 89221419', NOW(), 2, 78);

`SELECT * FROM calls;`

 id |     phone     |    date    | user_id | lenght 
----+---------------+------------+---------+--------
  1 | +569 89221414 | 2019-08-02 |       2 |    120
  2 | +569 89221415 | 2019-08-02 |       2 |     40
  3 | +569 89221416 | 2019-08-02 |       2 |     55
  4 | +569 89221417 | 2019-08-02 |       2 |     44
  5 | +569 89221418 | 2019-08-02 |       2 |     36
  6 | +569 89221419 | 2019-08-02 |       2 |     78
(6 rows)
</code></pre>
<h2 id="ingresar-4-llamadas-asociadas-al-usuario-carlos.">Ingresar 4 llamadas asociadas al usuario Carlos.</h2>
<pre><code>INSERT INTO calls (phone, date, user_id, lenght) VALUES ('+569 87671411', NOW(), 1, 15);
INSERT INTO calls (phone, date, user_id, lenght) VALUES ('+569 87671412', NOW(), 1, 12);
INSERT INTO calls (phone, date, user_id, lenght) VALUES ('+569 87671413', NOW(), 1, 6);
INSERT INTO calls (phone, date, user_id, lenght) VALUES ('+569 87671414', NOW(), 1, 17);

`SELECT * FROM calls;`

 id |     phone     |    date    | user_id | lenght 
----+---------------+------------+---------+--------
  1 | +569 89221414 | 2019-08-02 |       2 |    120
  2 | +569 89221415 | 2019-08-02 |       2 |     40
  3 | +569 89221416 | 2019-08-02 |       2 |     55
  4 | +569 89221417 | 2019-08-02 |       2 |     44
  5 | +569 89221418 | 2019-08-02 |       2 |     36
  6 | +569 89221419 | 2019-08-02 |       2 |     78
  7 | +569 87671411 | 2019-08-02 |       1 |     15
  8 | +569 87671412 | 2019-08-02 |       1 |     12
  9 | +569 87671413 | 2019-08-02 |       1 |      6
 10 | +569 87671414 | 2019-08-02 |       1 |     17
(10 rows)
</code></pre>
<h2 id="crear-un-nuevo-usuario.">Crear un nuevo usuario.</h2>
<pre><code>INSERT INTO users (first_name, email, last_name) VALUES ('Pepe', 'pepe@gmail.com', 'Velasco');

SELECT * FROM users;

 id | first_name |      email       | last_name 
----+------------+------------------+-----------
  1 | Carlos     | carlos@gmail.com | Perez
  2 | Laura      | laura@gmail.com  | Jara
  3 | Pepe       | pepe@gmail.com   | Velasco
(3 rows)
</code></pre>
<h2 id="seleccionar-la-cantidad-de-llamados-de-cada-uno-de-los-usuarios-nombre-de-usuario-y-cantidad-de-llamadas.">Seleccionar la cantidad de llamados de cada uno de los usuarios (nombre de usuario y cantidad de llamadas).</h2>
<pre><code>SELECT users.id, first_name, count(calls.id) FROM calls right JOIN users ON (users.id = calls.user_id) GROUP BY users.id;

 id | first_name | count 
----+------------+-------
  2 | Laura      |     6
  1 | Carlos     |     4
  3 | Pepe       |     0
(3 rows)
</code></pre>
<h2 id="obtener-el-usuario-con-mayor-número-de-llamada">Obtener el usuario con mayor número de llamada</h2>
<pre><code>SELECT users.id, first_name, count(calls.id) FROM calls right JOIN users ON (users.id = calls.user_id) GROUP BY users.id ORDER BY count(calls.id) DESC LIMIT 1;

 id | first_name | count 
----+------------+-------
  2 | Laura      |     6
(1 row)
</code></pre>
<h2 id="seleccionar-los-llamados-del-usuario-llamado-carlos-ordenados-por-fecha-en-orden-descendente.">Seleccionar los llamados del usuario llamado Carlos ordenados por fecha en orden descendente.</h2>
<pre><code>SELECT * FROM calls WHERE (calls.user_id = 1) ORDER BY date DESC;

 id |     phone     |    date    | user_id | lenght 
----+---------------+------------+---------+--------
  7 | +569 87671411 | 2019-08-02 |       1 |     15
  8 | +569 87671412 | 2019-08-02 |       1 |     12
  9 | +569 87671413 | 2019-08-02 |       1 |      6
 10 | +569 87671414 | 2019-08-02 |       1 |     17
(4 rows)
</code></pre>
<h2 id="mostrar-el-nombre-del-usuario-que-haya-hecho-la-llamada-más-larga">Mostrar el nombre del usuario que haya hecho la llamada más larga</h2>
<pre><code>SELECT users.id, first_name, max(calls.lenght) FROM calls LEFT JOIN users ON (users.id = calls.user_id) GROUP BY users.id ORDER BY max(calls.lenght) DESC LIMIT 1;

 id | first_name | max 
----+------------+-----
  2 | Laura      | 120
(1 row)
</code></pre>
<h2 id="mostrar-todos-los-usuarios-junto-con-la-suma-total-de-largo-de-llamadas">Mostrar todos los usuarios junto con la suma total de largo de llamadas</h2>
<pre><code>SELECT users.id, first_name, sum(calls.lenght) FROM calls LEFT JOIN users ON (users.id = calls.user_id) GROUP BY users.id ORDER BY sum(calls.lenght) DESC;

 id | first_name | sum 
----+------------+-----
  2 | Laura      | 373
  1 | Carlos     |  50
(2 rows)
</code></pre>
<h2 id="mostrar-todos-los-usuarios-que-hayan-hecho-menos-de-5-llamadas.">Mostrar todos los usuarios que hayan hecho menos de 5 llamadas.</h2>
<pre><code>SELECT users.id, first_name, count(calls.id) FROM calls right JOIN users ON (users.id = calls.user_id) GROUP BY users.id HAVING count(*) &lt; 5;

 id | first_name | count 
----+------------+-------
  1 | Carlos     |     4
  3 | Pepe       |     0
(2 rows)
</code></pre>
<h1 id="nuevos-cambios-solicitados-por-cliente.">Nuevos cambios solicitados por cliente.</h1>
<h2 id="necesito-agregar-a-la-base-una-tabla-de-auditoría-que-registre-el-motivo-del-borrado-de-una-llamada-y-el-usuario-que-lo-efectuó.">Necesito agregar a la base una tabla de auditoría que registre el motivo del borrado de una llamada y el usuario que lo efectuó.</h2>
<pre><code>CREATE TABLE auditoria ( id SERIAL PRIMARY KEY, motivo VARCHAR(150), user_id INTEGER REFERENCES users(id), call_id INTEGER REFERENCES calls(id));

select * from auditoria;
 id | motivo | user_id | call_id 
----+--------+---------+---------
(0 rows)
</code></pre>

