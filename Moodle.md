# Instrucciones para la instalacion de Aula Vea a Moodle 3.3.1

## Requerimientos
La lista de requerimientos se pueden ver dando [clic aqui](https://docs.moodle.org/all/es/Notas_de_Moodle_3.3).

### 1. Requerimientos del Servidor
* Versión de PHP: minimo PHP 5.6.5 (¡importante! la versión mínima de PHP se ha incrementado desde Moodle 3.1)
* Las extensiones PHP openssl y fileinfo ahora son necesarias en Moodle 3.3 (eran recomendadas en 3.2)
* ~~Soporte unicode completo para los detalles en MySQL/MariaDB. Puede ver las instruccines [dando clic aqui](https://docs.moodle.org/all/es/MySQL_soporte_unicode_completo)~~

~~Incluir lo siguiente en su **my.cnf**:~~

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
~~Luego reiniciar el servidor mysql.~~
~~Tambien se recomienda crear la base de datos incluyendo el soporte total unicode, como sigue (suponiendo que su base de datos se llama "educacion"") [Mas informacion aqu](https://docs.moodle.org/33/en/MySQL#Creating_Moodle_database):~~

```mysql
CREATE DATABASE educacion DEFAULT CHARACTER SET utf8 COLLATE utf8_unicode_ci;
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



### 4. Acciones preliminares

- [x] Se ha eliminado el lenguaje es_ar de la data y de la base de datos
- [x] Se ha procedido a eliminar los plugins y temas rotos para la siguiente version
- [x] Se ha instalado PHP 5.5.38
- [x] Se ha usado MySQL 5.7.18
- [x] Se ha creado la base de datos con soporte UTF8
- [x] Se ha importado la base de datos facilitada
- [x] Se ha procedido con la actualización desde linea de comando

Una vez concluida la actualización de la base de datos

- [x] Se actualizaron los temas y módulos que requerian atención
- [x] Se migraron las tareas al modulo de la siguiente versión que no se migraron correctamente
- [x] Se instala PHP 5.6.31 (Aunque Mooddle sugiere 5.6.5, ha funcionado bien)
- [x] Acá es necesario actualizar el soporte de mysql a MySQL soporte unicode completo [https://docs.moodle.org/all/es/MySQL_soporte_unicode_completo]
- [x] ~~Se cambia el my.cnf con los siguientes valores:~~ 

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

- [x] ~~Además Moodle sugiere que se active el módulo intl de PHP~~
- [x] ~~Sugiere además que tu sitio esté tenga cifrado SSL~~
- [x] Se corre la actualización nuevamente
- [x] Y sale un error configuraciones iniciales [https://tracker.moodle.org/browse/MDL-55757?focusedCommentId=451220&page=com.atlassian.jira.plugin.system.issuetabpanels%3Acomment-tabpanel#comment-451220]

```mysql
INSERT INTO `mdl_config` (`name`, `value`) 
VALUES 
('defaultpreference_maildisplay', '2'), 
('defaultpreference_mailformat', '1'), 
('defaultpreference_maildigest', '0'), 
('defaultpreference_autosubscribe', '1'), 
('defaultpreference_trackforums', '0'); 
```

### 5. Error con el paquete de idiomas en español
https://moodle.org/mod/forum/discuss.php?d=246152&parent=1068809

```
UPDATE `mdl_config` SET value="es" WHERE name="lang"
UPDATE `mdl_user` SET lang="es" WHERE lang="es_ar"
```

## Proceso de Actualizacion

Se desempaqueta la ultima version de Moodle (3.4)

Se anade el ontetopic_format en la carpeta raiz/course/format

Luego agregamos los themes en la carpeta raiz/theme

Move your old Moodle software program files to another location. Do NOT copy new files over the old files.

Unzip or unpack the upgrade file so that all the new Moodle software program files are in the location the old files used to be in on the server. Moodle will adjust SQL and moodledata if it needs to in the upgrade.

Copy your old config.php file back to the new Moodle directory.

As mentioned above, if you had installed any plugins on your site you should add them to the new code tree now. It is important to check that you get the correct version for your new version of Moodle. Be particularly careful that you do not overwrite any code in the new version of Moodle.

Dont forget to also copy over your moodledata folder / directory. If you don't you will get a "fatal error $cfg- dataroot is not configured properly".


cp moodle.backup/config.php moodle
cp -pr moodle.backup/theme/mytheme moodle/theme/mytheme
cp -pr moodle.backup/mod/mymod moodle/mod/mymod