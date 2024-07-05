docker-compose build
docker-compose up -d --build

in file app/public_htdocs/.htaccess comment line:
#php_value auto_prepend_file /mnt/efs/www/phpguard/scrub.php

in config.php:
 - change db hosts to dev-db
 - ssl not working yet so disable LOGIN_TO_HTTPS

create dbadmin user in mysql:

GRANT ALL ON *.* TO 'dbadmin'@'%' IDENTIFIED BY 'example';
FLUSH PRIVILEGES;

in case of problems with restoring db dumps:

Row size too large (> 8126).
Changing some columns to TEXT or BLOB may help. In current row format, BLOB prefix of 0 bytes is stored inline.

use {site}_data;
SET GLOBAL innodb_strict_mode=OFF;
SET SESSION innodb_strict_mode=OFF;

add site host names to hosts file:
for example:

127.0.0.1 test-dev.loc

and access different sites using urls like http://test-dev.loc
