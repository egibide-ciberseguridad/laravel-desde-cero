# Laravel

Ejemplo de creación de una aplicación Laravel desde cero.

## Prerrequisitos

1. Descargar, instalar y arrancar [Dockerbox](https://github.com/ijaureguialzo/dockerbox).

2. Clonar este repositorio en la carpeta `sites`.

## Nuevo proyecto

### Generar un proyecto nuevo

1. Abrir un terminal en la carpeta `dockerbox` y entrar en el workspace:

    ```bash
    make workspace
    ```

2. Situarse en la carpeta `laravel-desde-cero`:

    ```bash
    cd laravel-desde-cero
    ```

3. Crear el proyecto:

    ```bash
    composer create-project laravel/laravel laravel
    ```

4. Salir del `workspace`:

    ```bash
    exit
    ```

5. Editar el fichero `app/Providers/AppServiceProvider.php` y añadir al método `boot()`:

    ```php
    public function boot()
    {
        \URL::forceScheme('https');
    }    
    ```

### Añadir el nuevo sitio web a Dockerbox

1. [Redirigir los dominios .test a localhost](https://github.com/ijaureguialzo/automatic-test-domains). Si no es
   posible, editar como root el fichero `/etc/hosts` (en macOS y Linux) o
   en [Windows](https://www.adslzone.net/esenciales/windows-10/editar-archivo-host/) y añadir una nueva línea:

   ```text
   127.0.0.1    laravel-desde-cero.dockerbox.test
   ```

2. Recargar los sitios web disponibles:

    ```bash
    make reload
    ```

3. Acceder al [nuevo sitio](https://laravel-desde-cero.dockerbox.test).

## Crear la base de datos

1. Acceder a [phpMyAdmin](https://phpmyadmin.dockerbox.test) y crear el usuario `laravel/12345Abcde` y marcar la
   opción para generar la base de datos asociada, que se llamará como el usuario.

2. Editar el `.env` de la aplicación:

    ```dotenv
    DB_CONNECTION=mysql
    DB_HOST=mariadb
    DB_PORT=3306
    DB_DATABASE=laravel
    DB_USERNAME=laravel
    DB_PASSWORD=12345Abcde
    ```

## Utilidades

### Lanzar comandos en el proyecto (composer, artisan, npm...)

Entrar al workspace y situarse en la carpeta que contiene la aplicación:

```bash
make workspace
```

```bash
cd laravel-desde-cero/laravel
```

Y después el comando que necesitemos. Por ejemplo:

```bash
php artisan tinker
```
