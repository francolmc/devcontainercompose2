# devcontainercompose2
Ejemplo de proyecto con devcontainer y docker-compose en vscode

El proyecto contiene la configuración del directorio .devcontainer considerando el uso de docker-compose en VS Code. Para probar el ejemplo se se ha creado un proyecto con laravel (configurado con autenticación) y mysql.

Requisitos

- VSCode
- Extension Remote - Containers
- Docker Desktop

Después de descargar el proyecto

- Abrir carpeta con VSCode y editar el archivo docker-compose.yaml ubicado en el directorio .devcontainer, tanto la password de root mysql y laravel_user

  ```
  version: '3.7'
  services:
      app:
          container_name: devcontainercompose2_app
          build: .
          ports:
              - 8000:8000
          volumes:
              - ../app:/app
          tty: true
          depends_on:
              - mysql
      mysql:
          container_name: devcontainercompose2_mysql
          image: mysql:5.7
          ports:
              - 3306:3306
          environment:
              MYSQL_ROOT_PASSWORD: <definir password para root de mysql>
              MYSQL_USER: laravel_user
              MYSQL_PASSWORD: <definir password para el usuario laravel_user>
              MYSQL_DATABASE: laravel_db
          volumes:
              - ../data:/var/lib/mysql
  ```

  

- Abrir la paleta de comandos en VSCode en el menu View > Command Palette... y ejecutar ">Remote-Containers: Reopen in Container"

  En caso de aparecer una venta con las opciones "Rebuild" o "Ingnore", preseionar "Rebuild" para que tome los cambios de las claves en el archivo docker-compose.yaml.

- Abrir un terminal en VSCode y ejecutar 

  ```
  composer install
  ```

  Esto para la instalar los paquetes de laravel.

- Copiar archivo .env

  ```
  cp .env.example .env 
  ```

- Configurar archivo .env

  ```
  DB_CONNECTION=mysql
  DB_HOST=mysql
  DB_PORT=3306
  DB_DATABASE=laravel_db
  DB_USERNAME=laravel_user
  DB_PASSWORD=<password definida para el usuario laravel_user en el archivo docker-compose.yaml>
  ```

- Crear la key de la aplicación

  ```
  php artisan key:generate
  ```

- Generar proceso de migración en la base de datos.

  ```
  php artisan migrate
  ```

- Ejecutar el servidor de laravel

  ```
  php artisan serve --host 0.0.0.0
  ```

  Abrir en el navegador http://localhost:8000