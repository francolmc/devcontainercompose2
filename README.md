# devcontainercompose2
Ejemplo de proyecto con devcontainer y docker-compose en vscode

El proyecto contiene la configuracion del directorio .devcontainer considerando el uso de docker-compose en VS Code. Para probar el ejemplo se se ha creado un proyecto con gatsby.

Requisitos

- VSCode
- Extension Remote - Containers
- Docker Desktop

Despues de descargar el proyecto

- Al abrir el proyecto con VSCode realizar el proceso de abrir container ("Reopen in Container")

- Abrir un terminal en VSCode y ejecutar 

  ```
  yarn install
  ```

  

- Luego ejecutar 

  ```
  gatsby develop -H 0.0.0.0
  ```

  

- Abrir en el navegador http://localhost:3000