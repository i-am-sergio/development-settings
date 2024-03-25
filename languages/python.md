## Pyhton Projects Settings
[Click here for Django Settings](python.md)
1. Install python (3 o higher)
2. Install pip:
    - Linux (debian):
    ```bash
    sudo apt install pip
    ```
3. Install virtualenv:
    - Linux (debian):
    ```bash
    sudo apt install python3-virtualenv
    ```
    - Fedora and Windows:
    ```bash
    pip install virtualenv
    ```
4. Create virtual environment
    ```bash
    mkdir myproject && cd myproject
    virtualenv venv
    ```
    - *Activate virtual environment:*
      - Windows:
        ```bash
        venv\Scripts\activate
        ```
      - Linux and MacOS:
        ```bash
        source venv/bin/activate
        ```
    - *Exit virtual environment:*
      - Linux and MacOS:
        ```bash
        deactivate
        ```
6. Install Django (into venv):
    - Linux (debian):
    ```bash
    pip install django
    ```
7. Create new application:
    ```bash
    python manage.py startapp myapp
    ```
9. Run application
    ```bash
    python manage.py runserver
    ```
