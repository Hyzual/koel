# Helpful commands for contributors

How to start the development containers:
Start by filling the `docker.env` file as follows:

```
MYSQL_ROOT_PASSWORD=<generate a password>
MYSQL_PASSWORD=<second password>
DB_PASSWORD=<second password>

```

All the following commands must be run at the koel repository root.

```sh
# Start the web and db containers:
docker-compose up -d --build
# Install PHP dependencies
composer install
# Install front-end dependencies
yarn install
(cd resources/assets && yarn install)
# Compile dependencies for development
yarn run dev
# Connect to the web container and init koel
docker exec -it koel_web_1 bash
# The next command is run inside the container
$ php artisan koel:init
```

Finally, you can access koel at http://localhost

### How to connect to the web container ?

```sh
docker exec -it koel_web_1 bash
```

### How to connect to the mysql DB ?

```sh
docker exec -it koel_database_1 mysql -uroot -p
# Then paste the password for MYSQL_ROOT_PASSWORD
```
