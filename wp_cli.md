# Comandos a ejecutar


## Obtenemos el sitio
```
wp option get siteurl

```

## reemplazamos con la nueva URL
```
wp search-replace 'http://url-antigua' 'http://url-nueva' --all-tables-with-prefix --verbose
```

#### Ejemplo

wp search-replace 'http://cambioclimatico.minam.gob.pe/wp' 'http://minam.dev/cambioclimatico' --all-tables-with-prefix --verbose

## Damos los permisos a la ruta de la instalacion y entramos en ella
sudo chmod -R 755 /directio-de-instalacion && cd /directio-de-instalacion

## Buscamos y damos permisos a los directorios
find . -type d -exec sudo chmod 755 {} \;

## Damos permisos a los ficheros
find . -type f -exec sudo chmod 644 {} \;

## Damos permiso a la carpeta uploads
sudo chmod -R 775 wp-content/uploads/

## Damos permisos al .htaccess
sudo chmod 777 .htaccess 

## Listamos los plugins
wp plugin list

## Actualizamos los plugins
wp plugin update --all

## Listamos los themes
wp theme list

## Actualizamos los themes
wp theme update --all --allow-root

## Actualizamos el core
wp core update

## Actualizamos las traducciones dispobibles
wp core language update

## Sacamos backup de la base de datos
mysqldump -u root -p db > path 

## Cambiando los prefijos de la BBDD
RENAME table `wp_commentmeta` TO `cc_commentmeta`;
RENAME table `wp_comments` TO `cc_comments`;
RENAME table `wp_links` TO `cc_links`;
RENAME table `wp_options` TO `cc_options`;
RENAME table `wp_postmeta` TO `cc_postmeta`;
RENAME table `wp_posts` TO `cc_posts`;
RENAME table `wp_terms` TO `cc_terms`;
RENAME table `wp_termmeta` TO `cc_termmeta`;
RENAME table `wp_term_relationships` TO `cc_term_relationships`;
RENAME table `wp_term_taxonomy` TO `cc_term_taxonomy`;
RENAME table `wp_usermeta` TO `cc_usermeta`;
RENAME table `wp_users` TO `cc_users`;