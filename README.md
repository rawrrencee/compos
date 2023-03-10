### Cheat Sheets

-   [Laravel Artisan](https://artisan.page/)
-   [Tailwind](https://tailwindcomponents.com/cheatsheet/)

### Technologies Used

-   Laravel (PHP)
    -   Jetstream
-   Vue 3 with InertiaJS
-   MySQL
-   Docker

### Setting Up on Windows

1.  Install WSL2 via `wsl --install` on Command Prompt
2.  Install Docker
3.  Create `.env` file by referencing the configuration below
4.  Configure Windows Console Host to use Ubuntu terminal
5.  Navigate to root folder and Run in WSL (e.g. Ubuntu) terminal
    >       docker run --rm \
    >           -u "$(id -u):$(id -g)" \
    >           -v "$(pwd):/var/www/html" \
    >           -w /var/www/html \
    >           laravelsail/php82-composer:latest \
    >           composer install --ignore-platform-reqs
6.  Navigate to root folder and run `./vendor/bin/sail up -d`
7.  Run `./vendor/bin/sail artisan migrate:fresh`
8.  Run `./vendor/bin/sail npm i`
9.  Run `./vendor/bin/sail npm run build`
10. Run `./vendor/bin/sail npm run dev` if you need hot reloading while editing code

### Deploying to Production (Shared Hosting)

1.  Update .htaccess file
    >       <IfModule mod_rewrite.c>
    >           <IfModule mod_negotiation.c>
    >               Options -MultiViews
    >           </IfModule>
    >
    >           RewriteEngine On
    >
    >           # Redirect Trailing Slashes...
    >           RewriteRule ^(.*)/$ /$1 [L,R=301]
    >
    >           # Handle Front Controller...
    >           RewriteCond %{REQUEST_FILENAME} !-d
    >           RewriteCond %{REQUEST_FILENAME} !-f
    >           RewriteRule ^ index.php [L]
    >       </IfModule>
2.  Install nvm and npm
    >       wget -qO- https://cdn.rawgit.com/creationix/nvm/master/install.sh | bash
    >       nvm install stable
3.  Install composer
    > Instructions from https://getcomposer.org/download/  
    >  FAQ (Hostinger) https://support.hostinger.com/en/articles/5792082-how-to-solve-the-most-common-composer-issues
4.  Run command `npm install`
5.  Run command `npm run build`
6.  Run command `./composer.phar self-update`
7.  Run command `./composer.phar install --optimize-autoloader --no-dev`
8.  Shift `public_html/domain/public/build/assets` folder to `public_html/domain/build` folder of the domain
    > Keep `assets/manifest.json` in the `public_html/domain/public/build/assets` folder
9.  Setup `.env` file
10. Run `php artisan migrate`

### .env File

>       APP_NAME=Laravel
>       APP_ENV=local
>       APP_KEY=base64:H55v8lpuXJsY3YOaFdGKIQwhpaBdlmqdATaH7JjmDOk=
>       APP_DEBUG=true
>       APP_URL=http://localhost
>
>       LOG_CHANNEL=stack
>       LOG_DEPRECATIONS_CHANNEL=null
>       LOG_LEVEL=debug
>
>       DB_CONNECTION=mysql
>       DB_HOST=mysql
>       DB_PORT=3306
>       DB_DATABASE=compos
>       DB_USERNAME=sail
>       DB_PASSWORD=password
>
>       BROADCAST_DRIVER=log
>       CACHE_DRIVER=file
>       FILESYSTEM_DISK=local
>       QUEUE_CONNECTION=sync
>       SESSION_DRIVER=database
>       SESSION_LIFETIME=120
>
>       MEMCACHED_HOST=127.0.0.1
>
>       REDIS_HOST=redis
>       REDIS_PASSWORD=null
>       REDIS_PORT=6379
>
>       MAIL_MAILER=smtp
>       MAIL_HOST=mailpit
>       MAIL_PORT=1025
>       MAIL_USERNAME=null
>       MAIL_PASSWORD=null
>       MAIL_ENCRYPTION=null
>       MAIL_FROM_ADDRESS="hello@example.com"
>       MAIL_FROM_NAME="${APP_NAME}"
>
>       AWS_ACCESS_KEY_ID=
>       AWS_SECRET_ACCESS_KEY=
>       AWS_DEFAULT_REGION=us-east-1
>       AWS_BUCKET=
>       AWS_USE_PATH_STYLE_ENDPOINT=false
>
>       PUSHER_APP_ID=
>       PUSHER_APP_KEY=
>       PUSHER_APP_SECRET=
>       PUSHER_HOST=
>       PUSHER_PORT=443
>       PUSHER_SCHEME=https
>       PUSHER_APP_CLUSTER=mt1
>
>       VITE_PUSHER_APP_KEY="${PUSHER_APP_KEY}"
>       VITE_PUSHER_HOST="${PUSHER_HOST}"
>       VITE_PUSHER_PORT="${PUSHER_PORT}"
>       VITE_PUSHER_SCHEME="${PUSHER_SCHEME}"
>       VITE_PUSHER_APP_CLUSTER="${PUSHER_APP_CLUSTER}"
>
>       SCOUT_DRIVER=meilisearch
>       MEILISEARCH_HOST=http://meilisearch:7700
