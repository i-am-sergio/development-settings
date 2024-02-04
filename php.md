# PHP - Laravel

## Settings
- Database Connection
  - Install Sql drive (Example: mysql):
    ```bash
    sudo apt intall php-mysql
    ```
  - Edit *.env* according to the sql database (This is Mysql sample)
    ```env
    DB_CONNECTION=mysql
    DB_HOST=roundhouse.proxy.rlwy.net
    DB_PORT=59739
    DB_DATABASE=railway
    DB_USERNAME=root
    DB_PASSWORD=G3c1FbAA2EHeBF62gaC3H-HB-52bgf-F
    ```
  - Create Migration
    ```bash
    php artisan make:model NameClassModel -m
    ```
  - Apply Migrations
    ```bash
    php artisan migrate
    ```
