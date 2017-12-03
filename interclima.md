## Cono actualizar SPIP 2 a 3

Esta documentación se refiere a la transición a la última versión estable de SPIP : SPIP 3.2.0 hasta la fecha.

Esto es para actualizar a la última versión de SPIP versión 2 (o anterior).

El método propuesto le permite ir en una base saludable haciendo una gran limpieza en los archivos SPIP y comenzando de cero en los nuevos complementos (SPIP 3 le permite instalar complementos muy rápidamente).

## Resumen

- Backup antes de la migración
- Comprobando la codificación antes de la migración
- Preparándose para la migración
- Comprobación de complementos
- Actualización de los archivos del sitio
- Actualiza la base
- En caso de problema instalación de complementos y esqueletos casa
- Actualización actual de Spip 3
- Acerca de esta documentación
- Backup antes de la migración

## Copia de seguridad de la base de datos 
- Si tiene la posibilidad, es aconsejable hacer una copia de seguridad de la base de datos MySQL a través de PHPMyAdmin, disponible en muchos alojamientos. 
- SPIP también ofrece un sistema de respaldo

elige una copia de seguridad comprimida
Obtenga el archivo generado por formato ftp: xml para spip2, en tmp / dump (o write / data para un spip antiguo)
Copia de seguridad de carpetas personales 
- Recuperar por ftp los directorios:

IMG
config (para un spip muy antiguo, obtenga los códigos de su base de datos)
posiblemente esqueletos si su contenido podría ser reutilizado
Con la copia de seguridad de su base de datos y la carpeta IMG (que contiene todos los documentos e imágenes adjuntos a su sitio), sus contenidos se guardan. config contiene información de inicio de sesión de la base de datos y esqueletos de sus esquemas de personalizaciones. Tenga en cuenta la versión exacta del spip utilizado (antes de esta migración).

Comprobando la codificación antes de la migración

Si su sitio es lo suficientemente reciente (sitio en utf-8) o si la codificación de este ya está en utf-8, puede continuar con el siguiente paso.

Para averiguarlo, mira la configuración de idioma.

Si la codificación está en iso-8859-1, es aconsejable cambiar su sitio a utf-8. Tal procedimiento se propone en el spip 2 (ver a continuación el spip 3):

haga una copia de seguridad de la base de datos (en principio ya tiene una)
en la página de gestión del idioma, haga clic en el enlace propuesto a "la página de conversión a utf-8" (url: write /? exec = convert_utf8)
luego ejecuta la página: write /? exec = sql_convert_utf8
Comprobación de complementos

Recuerde actualizar sus complementos para limitar las incompatibilidades.

Para sitios bajo SPIP 3.0 y superior, existe el complemento Comprobar sus complementos que le permite revisar los complementos compatibles o no con la versión que desea instalar

Los complementos no compatibles se desactivarán durante la instalación de la nueva versión.

Preparándose para la migración

Compruebe la versión de PHP que se ejecuta en su servidor (por ejemplo, a través de http://www.misitio.org/ecrire/?exec=info ). SPIP 3 requiere PHP al menos la versión 5.1 (mientras que SPIP 2 todavía se ejecuta en PHP 4.x). Si es necesario, consulte con su anfitrión cómo usar una versión reciente de PHP 5.3 o 5.4, por ejemplo).

Para ejecutar SPIP 3.2, necesita PHP 5.4 mínimo.

Entonces dos posibilidades:


Solución 1

Descargue la última versión de SPIP ( http://www.spip.net/fr_article2670.html ) y luego descomprima el archivo en una carpeta de spip en su computadora
Cree directorios ftp en la raíz de su sitio, en el servidor: / spip3 y / formerSpip
Transfiera los directorios y archivos de la carpeta local de spip en su computadora a la carpeta remota spip3 en el sitio
Su archivo / spip3 debe contener:

archivos php: index.php, spip.php
carpetas: escribir, tmp, local, skeletons-dist, plugins-dist, privado e IMG y config (vacío)
algunos archivos .txt y .png

Solución 2

Obtenga el archivo spip_loader.php (o simplemente copie su contenido) en su computadora desde http://www.spip.net/en_article2670.html#spip_loader
Coloque este archivo en la raíz de su sitio, por FTP
¡No lo ejecutes todavía!
Actualización de los archivos del sitio

Transfiera los archivos y archivos desde su sitio SPIP a / formerSpip (excepto las carpetas para mantener absolutamente: IMG y config). Para esto, en FTP:

1. en su sitio remoto, seleccione todo (incluida la carpeta / complementos!) EXCEPTO

oldSpip ,
spip3 ,
IMG ,
config
y archivos o carpetas que no conciernen a SPIP (a veces tiene documentos u otros archivos en su sitio, independientemente de SPIP, estos archivos pueden referirse a otras aplicaciones como grr, cdt, pmb, ...).
el archivo spip_loader.php si optó por la solución 2
2. Arrastra / suelta el resto de la selección en / oldSpip

Su sitio, en este momento, ya no es funcional. No durará mucho, puedes estar seguro ;-). Por otro lado, es importante mover / eliminar de la raíz del servidor las carpetas write , private , extensions o plugins-dist , skeletons-dist . De hecho, estos archivos contienen archivos eliminados en SPIP 3 y que podrían causar conflictos si no se eliminan.

si optó por la solución 1

Siempre en FTP:

Ir a la carpeta / spip3
transfiere los contenidos de / spip3 al siguiente nivel (la raíz del sitio). Por eso :
- * Ctrl + a para seleccionar todos los elementos de / spip3 
- * arrastre y suelte la selección en .. 
- * la carpeta / spip3 está vacía, elimínela.

si optó por la solución 2

Visite su sitio con su navegador habitual y abra la página spip_loader.php, vaya a la dirección de estilo: http://www.mysite.org/spip_loader.php y siga las instrucciones.
Actualiza la base

Según el tipo de actualización, se ofrecerá un procedimiento de actualización de la base de datos accediendo al área privada. Sigue las indicaciones

Consulte su sitio. Normalmente, debería aparecer (bajo la apariencia de los esqueletos SPIP predeterminados)
Conéctese en la interfaz privada de SPIP con una cuenta de administrador (en caso de dificultad, vaya al sitio URL / escritura).
Siga el procedimiento de mantenimiento propuesto.
Luego ve a la página de administración de complementos (en configuración)
Verifica que el sitio funcione.
En caso de problema

Si es necesario (si ya no puede acceder al área privada del sitio, si se muestran errores recurrentes), también puede ser útil restablecer algunos archivos SPIP temporales.

Esto es para vaciar el directorio tmp, excepto posiblemente los archivos adjuntos, sesiones y visitas de los subdirectorios.

Para esta operación: vaya a la carpeta tmp y borre todo excepto las carpetas de volcado y visitas. Necesitarás reconectarte.

Instalación de complementos y esqueletos

Crea las siguientes carpetas en la raíz de tu sitio:

/ plugins (luego en esta carpeta, crea la carpeta automática)
/ lib
/ esqueletos
Adapte los derechos de estas carpetas para que el servidor pueda escribirles.

Vaya a la interfaz de administración de complementos y, en "depósitos", use el repositorio propuesto ( importante para la implementación de la nueva administración de complementos ).

Instale los complementos necesarios (búsquelos en el motor de búsqueda) para operar su sitio. Verifique que el sitio público se esté ejecutando (opcionalmente, vacíe el directorio cache o tmp como se explicó anteriormente). Revise la configuración del complemento (haga clic en el icono de configuración después de activarlos).

Si es necesario, restablezca las personalizaciones de esqueleto poniendo gradualmente los archivos html en su carpeta de esqueleto. Verifique que todos estén produciendo el resultado deseado.

casa

Cuando todo está terminado:

Verifique que las otras aplicaciones instaladas en el alojamiento estén funcionando.
verifique el contenido de la carpeta / oldSpip . Solo debe contener carpetas y archivos de su antiguo SPIP ( escritura , local , tmp , skeletons-dist o dist , extensiones y algunos archivos)
finalmente elimine la carpeta / oldSpip .
Actualización actual de Spip 3

Para una actualización simple en la misma rama (por ejemplo, de SPIP 3.0.N a SPIP 3.0.N + 1) utilice el método de "spip_loader", que es más rápido y simple. Este archivo está reservado para webmasters conectados, puede dejarlo en su hosting.

El esquema es lo suficientemente simple para una actualización:

copia de seguridad antes de la actualización (a través de la interfaz de Spip)
realizar la actualización (método spip_loader)
copia de seguridad después de la actualización (a través de la interfaz de Spip)

## Plugins en la version 2.1
drwxr-xr-x  8 apache apache 4096 dic  5  2016 ADXmenu
drwxr-xr-x  4 apache apache 4096 dic  5  2016 ancres_douces
drwxrwxrwx  2 apache apache 4096 dic  5  2016 auto
drwxr-xr-x 12 apache apache 4096 dic  5  2016 cfg
drwxr-xr-x  2 apache apache 4096 dic  5  2016 cimobile
drwxr-xr-x 13 apache apache 4096 dic  5  2016 contact
drwxr-xr-x 14 apache apache 4096 dic  5  2016 couteau_suisse
drwxr-xr-x 11 apache apache 4096 dic  5  2016 enluminures_typographiques_v3
drwxr-xr-x 12 apache apache 4096 dic  5  2016 itwx_cimobile_3_2
drwxr-xr-x  7 apache apache 4096 dic  5  2016 jquery_ui
drwxr-xr-x  7 apache apache 4096 dic  5  2016 mediabox
drwxr-xr-x  7 apache apache 4096 dic  5  2016 nuage
drwxr-xr-x  7 apache apache 4096 dic  5  2016 porte_plume_partout
drwxr-xr-x 14 apache apache 4096 dic  5  2016 saisies
drwxr-xr-x 17 apache apache 4096 dic  5  2016 spip-bonux
drwxr-xr-x 19 apache apache 4096 dic  5  2016 spip-listes_1_9_3


## Plugins en la version

drwxr-xr-x  8 apache apache 4096 nov 30 14:46 ADXmenu
drwxr-xr-x  4 apache apache 4096 nov 30 15:16 ancres_douces
drwxr-xr-x  2 apache apache 4096 nov 30 14:46 auto
drwxr-xr-x  2 apache apache 4096 nov 30 14:46 cimobile
drwxr-xr-x 13 apache apache 4096 nov 30 14:56 contact
drwxr-xr-x 12 apache apache 4096 nov 30 15:05 enluminures_typographiques_v3
drwxr-xr-x  7 apache apache 4096 nov 30 15:08 nuage
drwxr-xr-x 16 apache apache 4096 nov 30 15:00 saisies
drwxr-xr-x 11 root   root   4096 nov 30 15:03 spip-bonux-3


## SPIP actualizado a la version 3.2

Se comparten las imagenes en los recursos.