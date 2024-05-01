## Docker setup

#### The configuration is based on the [package](https://laravel.com/docs/9.x/sail). Please read the documentation for a better understanding
#### Make sure you have installed docker and docker-compose

### Available services:
- app (php, yarn, composer)
- mysql
- phpmyadmin (available on the localhost:8085)
- redis
- redis-commander (available on the localhost:8081)
- elasticsearch
- minio (web ui available on the localhost:8900)
- mailhog (web ui available on the localhost:8025)

------
**Notes**:

**Redis-Commander** - is a node.js web application used to view, edit, and manage a Redis Database

**MinIO** - provides an S3 compatible API that you may use to develop locally using Laravel's s3 file storage driver without creating "test" storage buckets in your production S3 environment.

**MailHog** - intercepts emails sent by your application during local development and provides a convenient web interface so that you can preview your email messages in your browser

------

#### Before the first launch make sure that you have created an .env file

```
cp .env.docker .env
```
And fill configs:
```
DOCKER_APP_NAME={project_name}
DB_DATABASE={your_database_name}
```

------

#### Now we can do the first init

At the root of the project there is a `Makefile` with several help commands

First
```
make init
```

After successful initialization we need to build a frontend

Available commands to build:
```
make yarn_hot
make yarn_dev
make yarn_watch
```

Then, Going to the browser you should get your working project
http://localhost 
Login with `super-admin@app.com` and password `password`.

------

#### PHP_CodeSniffer
[The basic concept of setup is described here](./php_cs.md)

For the docker setup we should configure `cli interpreter` in the PhpStorm settings

**1.** Go `Settings/Preferences` -> `PHP` -> `CLI interpreter` -> `...` -> `+` -> `From Docker` -> `Docker-compose` -> `service = app`
![](img/docker_1.png)

**2.** Save settings

**3.** Go to `Quality Tools` -> `PHP_CodeSniffer` -> `...` -> `+`

Select new created interpreter, then enter path to `phpcs` - `/opt/project/vendor/bin/phpcs`

Click **Validate**. It should display the version of the package
![](img/docker_2.png)

Go to `PHP_CodeSniffer inspection` settings and specify path to the `ruleset.xml`:
`{path_to_project}/code_review/php_cs/ruleset.xml`

[As described in basic concept #6](./php_cs.md)

Save settings and check the functionality in the `.php` files 
