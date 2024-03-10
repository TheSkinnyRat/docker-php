# GETTING STARTED
## Requirements
- Docker
## How to run this?
1. Go to folder you want to run. For example:
```bash
cd php-nginx-composer
```
2. Run docker compose
```bash
docker compose up -d
```
## How about the database?
MariaDB in Docker is available in this repository: https://github.com/TheSkinnyRat/docker-mariadb

# FAQ
## How to run multiple version of PHP?
> [!IMPORTANT]  
> Make sure your php version is available in PHP Docker. You can check it [here](https://hub.docker.com/_/php).
1. Copy folder and rename
```bash
cp -r php-nginx-composer php74-nginx-composer
```
2. Go to destination folder
```bash
cd php74-nginx-composer
```
3. Change the `.env` file
```env
...
CONTAINER_NAME=php74
PHP_VERSION=7.4
NGINX_PORT=8081
...
```
4. Run docker compose
```bash
docker compose up -d
```

## How to add PHP Extension?
> [!IMPORTANT]  
> Make sure your extension is available in PHP. You can check it [here](https://pecl.php.net/).
### New Container
1. Go to folder you want to run. For example:
```bash
cd php-nginx-composer
```
2. Add `PHP_EXTENSIONS` in `.env` file with your extension name. For example:
```env
...
PHP_EXTENSIONS="zip pdo_mysql pdo_pgsql"
...
```
3. Run docker compose
```bash
docker compose up -d
```
### Existing Container
1. Exec to exiting container
```bash
docker exec -it [container_name] sh
```
2. Install your extension
```bash
docker-php-ext-install pdo_pgsql
```

## How to add Linux (Alpine) Package?
> [!IMPORTANT]  
> Make sure your package is available in Alpine. You can check it [here](https://pkgs.alpinelinux.org/packages).
### New Container
1. Go to folder you want to run. For example:
```bash
cd php-nginx-composer
```
2. Add `APK_PACKAGES` in `.env` file with your package name. For example:
```env
...
APK_PACKAGES="libzip libzip-dev libpq"
...
```
3. Run docker compose
```bash
docker compose up -d
```
### Existing Container
1. Exec to exiting container
```bash
docker exec -it [container_name] sh
```
2. Install your package
```bash
apk add libpq
```