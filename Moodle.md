# Instrucciones para la instalacion de Aula Vea a Moodle 3.3.1

## Requerimientos
La lista de requerimientos se pueden ver dando [clic aqui](https://docs.moodle.org/all/es/Notas_de_Moodle_3.3).

### 1. Requerimientos del Servidor
* Versión de PHP: minimo PHP 5.6.5 (¡importante! la versión mínima de PHP se ha incrementado desde Moodle 3.1)
* Las extensiones PHP openssl y fileinfo ahora son necesarias en Moodle 3.3 (eran recomendadas en 3.2)
* Soporte unicode completo para los detalles en MySQL/MariaDB. Puede ver las instruccines [dando clic aqui](https://docs.moodle.org/all/es/MySQL_soporte_unicode_completo)

Incluir lo siguiente en su **my.cnf**:

```
[client]
default-character-set = utf8mb4

[mysqld]
innodb_file_format = Barracuda
innodb_file_per_table = 1
innodb_large_prefix

character-set-client-handshake = FALSE
character-set-server = utf8mb4
collation-server = utf8mb4_unicode_ci

[mysql]
default-character-set = utf8mb4
```
Luego reiniciar el servidor mysql.
Tambien se recomienda crear la base de datos incluyendo el soporte total unicode, como sigue (suponiendo que su base de datos se llama "educacion"") [Mas informacion aqu](https://docs.moodle.org/33/en/MySQL#Creating_Moodle_database):

```mysql
CREATE DATABASE educacion DEFAULT CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
```

#### Requisitos de la Base de Datos
Moodle soporta los siguientes servidores de Base de Datos. Una vez más, los números de las versiones son las versiones mínimas soportadas. Se recomendienda correr la versión estable más reciente de cualquier software.

Base de datos | Minima | Recomendada
--- | --- | ---
PostgreSQL | 9.3 | La mas reciente
**MySQL** | **5.5.31** | **La mas reciente**
MariaDB | 5.5.31 | La mas reciente
MS SQL Server | 2008 | La mas reciente
Oracle DB | 10.2 | La mas reciente

### 2. Requerimientos del Cliente
#### Soporte para navegador

###### Computador de escritorio
* Chrome
* Firefox
* Safari
* Edge
* Internet Explorer
* Mobile:

###### Mobile
* Safari
* Google Chrome

**Nota: Navegadores antiguos que tienen problemas conocidos de compatibilidad con Moodle 3.3:**

* Internet Explorer 10 e inferiores
Safari 7 e inferiores

### 3. Adicional
#### HTTPS
Moodle sugiere que se use un servidor SSL (Google tambien lo recomienda y empezara a poner advertencias a partir de octubre de 2017)

#### Sobre advertencia de PHP iconv
Si bien es cierto, Moodle sugiere que se use este modulo de PHP, el mismo ha quedado obsoleto desde su version 5.6.0. Puede leer las notas [ingresando aqui](http://php.net/manual/es/migration56.deprecated.php)



Acciones preliminares

Se ha eliminado el lenguaje es_ar de la data y de la base de datos
Se ha procedido a eliminar los plugins y temas rotos para la siguiente version
Se ha instalado PHP 5.5.38
Se ha usado MySQL 5.7.18
Se ha creado la base de datos con soporte UTF8
create database educacion; 
ALTER DATABASE educacion DEFAULT CHARACTER SET utf8 COLLATE utf8_unicode_ci;

Se ha importado la base de datos facilitada
mysql -u root -p educacion < /PATH/DEL/ARCHIVO.sql

Se ha procedido con la actualización desde linea de comando
$ sudo /usr/bin/php admin/cli/maintenance.php --enable
$ sudo /usr/bin/php admin/cli/upgrade.php
$ sudo /usr/bin/php admin/cli/maintenance.php --disable

Una vez concluida la actualización de la base de datos
Se actualizaron los temas y módulos que requerian atención
Se migraron las tareas al modulo de la siguiente versión que no se migraron correctamente
Se instala PHP 5.6.31 (Aunque Mooddle sugiere 5.6.5, ha funcionado bien)
Acá es necesario actualizar el soporte de mysql a MySQL soporte unicode completo [https://docs.moodle.org/all/es/MySQL_soporte_unicode_completo]
Se cambia el my.cnf con los siguientes valores:
[client]
default-character-set = utf8mb4

[mysqld]
innodb_file_format = Barracuda
innodb_file_per_table = 1
innodb_large_prefix

character-set-client-handshake = FALSE
character-set-server = utf8mb4
collation-server = utf8mb4_unicode_ci

[mysql]
default-character-set = utf8mb4

Además Moodle sugiere que se active el módulo intl de PHP
Sugiere además que tu sitio esté tenga cifrado SSL

Se corre la actualización nuevamente
Y sale un error cnfiguraciones iniciales [https://tracker.moodle.org/browse/MDL-55757?focusedCommentId=451220&page=com.atlassian.jira.plugin.system.issuetabpanels%3Acomment-tabpanel#comment-451220]

```mysql
INSERT INTO `mdl_config` (`name`, `value`) 
VALUES 
('defaultpreference_maildisplay', '2'), 
('defaultpreference_mailformat', '1'), 
('defaultpreference_maildigest', '0'), 
('defaultpreference_autosubscribe', '1'), 
('defaultpreference_trackforums', '0'); 
```
