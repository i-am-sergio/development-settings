## PHP - Laravel


1. Install php (Choose version 8 o higher)
    - Linux (debian):
    ```bash
    sudo apt install php php-curl
    ```
2. Install composer
    - Linux (debian):
     ```bash
     sudo apt install composer
     ```
3. Create Laravel project
     ```bash
     composer create-project --prefer-dist laravel/laravel project-name
     ```
4. Run Application
    ```bash
    cd example-app
    php artisan serve
    ```

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
