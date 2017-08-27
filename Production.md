# Acciones a realizar para la puesta en marcha

## 1. En la base de datos
Acciones a realizar en la base de datos:

#### 1.1. Creacion de la base de datos
Creamos la base de datos con coporte unicode UTF8. Cambiar **db_name** por el nombre de su base de datos.

Accedemos por consola.

```
mysql -u root -p
```

```mysql
CREATE DATABASE db_name DEFAULT CHARACTER SET utf8 COLLATE utf8_unicode_ci;
```

#### 1.2. Creacion del usuario que iteractuara con la base de datos
Creamos el usuario con el ambito deseado (en el ejemplo, solo a **localhost**)

```mysql
CREATE USER 'user_name'@'127.0.0.1' IDENTIFIED BY 'hard_password';
```
Cambiamos **user_name** por el nombre de usuario en produccio. Lo mismo con **127.0.0.1** con el IP del servidor que contiene a la apliacion. Cambiamos finalmente, **hard_password** por la clave del usuario.

#### 1.3. Asignamos privilegios del usuario sobre la base de datos
Asignamos los permisos con acceso a todas las tablas de la **db_name**, creada en el paso **1.1**.

```mysql
GRANT ALL PRIVILEGES ON db_name.* TO 'user_name'@'127.0.0.1';
```

Aqui estoy dando todos los privilegios en la base de datos. Pueden elegir los que deseen.

Refrescamos los privilegios.

```mysql
FLUSH PRIVILEGES;
```

Y verificamos los privilegios dados al usuario.

```mysql
SHOW GRANTS FOR 'user_name'@'127.0.0.1';
```

Salimos a la consola.

```
exit;
```

#### 1.3. Volcamos el respaldo en nuestra base de dados recien creada 
Suponiendo que el archivo **dbeducacion20170826-33-final.sql** se encuentre en **FILE/PATH**.

```
mysql -u root -p db_name < FILE/PATH/dbeducacion20170826-33-final.sql
```

Con eso tenemos la base de datos lista y se ha concluido con esa parte del procedimiento.

## 2. En la aplicacion
Suponiendo que los archivos descargados y dezipeados se encuentran en **FILE/PATH** y que **WEB/PATH** es la direccion de sus carpeta web de su Apache Tomcat.

#### 2.1 Hacemos una copia pero manteniendo los permisos de los archivos
Usamos para ello, los comandos scp.

```
scp -r  FILE/PATH/educacionmoodle WEB/PATH/
```

```
scp -r  FILE/PATH/educacionmoodledata WEB/PATH/
```
#### 2.2. Verificar los permisos y owners
Las carpetas de educacionmoodle deben tener permisos 755 y la de educacionmoodledata, 777. Los owners de ambas carpetas debe ser el usuario apache.

```
ll WEB/PATH
```

De no estar correctos los owners, corregimos con:

```
sudo chown -R apache:apache WEB/PATH/educacionmoodle
sudo chown -R apache:apache WEB/PATH/educacionmoodledata
```

De no estar correctos los permisos, corregimos con:

```
sudo chmod -R 755 WEB/PATH/educacionmoodle
sudo chmod -R 777 WEB/PATH/educacionmoodledata
```

#### 2.3. Cambiar el archivo de configuracion
Cambiar los valores por los suyos y segun la configuracion de la base de datos y su servidor en **WEB/PATH/educacionmoodle/config.php**

#### 2.4. Desactivar el Modo Mantenimiento desde consola
```
/usr/bin/php admin/cli/maintenance.php --disable
```

