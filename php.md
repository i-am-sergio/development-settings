# PHP - Laravel

## Settings
- Database Connection
  1. Install Sql drive (Example: mysql):
    ```bash
    sudo apt intall php-mysql
    ```
  2. Edit *.env* according to the sql database (This is Mysql sample)
    ```env
    DB_CONNECTION=mysql
    DB_HOST=roundhouse.proxy.rlwy.net
    DB_PORT=59739
    DB_DATABASE=railway
    DB_USERNAME=root
    DB_PASSWORD=G3c1FbAA2EHeBF62gaC3H-HB-52bgf-F
    ```
  3. Apply Migrations
    ```bash
    php artisan migrate
    ```
