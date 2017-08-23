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

