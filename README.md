# Startup Kit

## Specs
```text
Laravel 10
PHP 8.2
InertiaJs
Breeze
Vite
DaisyUI
Vue3
```

## How to Use
- Clone this repo
- If you don't have composer only docker in your host machine, run this command inside the folder:
```text
docker run --rm \
    -u "$(id -u):$(id -g)" \
    -v "$(pwd):/var/www/html" \
    -w /var/www/html \
    laravelsail/php82-composer:latest \
    composer install --ignore-platform-reqs
```
- If you have composer and docker, you can just run:
```text
composer install
```
- Fix your `.env` file by copying `.env.example`
- Run this command `./vendor/bin/sail build`
- Run this command `./vendor/bin/sail up -d`
