# Docker Magento 2

```Rootless containers```,
```Docker```,
```Magento 2```,
```Nginx```,
```MySQL```,
```PHP-FPM```,
```Adminer```,
```Redis```,
```Redis Admin```,
```RabbitMQ```,
```Elastic Search```,
```Kibana```

## Currently supported versions of Magento

- 2.4.0, 2.4.1, 2.4.2, 2.4.3, 2.4.4

## Setup

__Add following to etc/hosts__
- 127.0.0.1	magento.local
- 127.0.0.1	kibana.magento.local
- 127.0.0.1	redis.magento.local
- 127.0.0.1	rabbitmq.magento.local
- 127.0.0.1	adminer.magento.local

__A) Create brand new Magento project__

1) Run ```bin/new-project/create <version>```
	- Requires Magento version as an argument
	- Make sure "magento" folder exists and is owned by current user before you bind it to the container by running the script above, otherwise it will be created by Docker and owned by root.
	- Keys can be found in https://marketplace.magento.com/customer/accessKeys/ and you can opt-in to store your keys (login and password) to /home/docker/.composer/auth.json, which is bind mounted to docker/php-fpm/auth.json
	- Magento default settings - these can be edited in bin/new-project/create
		- ```base-url=http://magento.local```
		- ```db-host=mysql```
		- ```db-name=magento```
		- ```db-user=magento```
		- ```db-password=magento```
		- ```admin-firstname=admin```
		- ```admin-lastname=admin```
		- ```admin-email=admin@admin.com```
		- ```admin-user=admin```
		- ```admin-password=admin123```
		- ```language=en_US```
		- ```currency=USD```
		- ```timezone=America/Chicago```
		- ```use-rewrites=1```
		- ```elasticsearch-host=elasticsearch```
		- ```session-save=redis```
		- ```session-save-redis-host=redis```
		- ```session-save-redis-db=0 --session-save-redis-password=""```
		- ```cache-backend=redis```
		- ```cache-backend-redis-server=redis```
		- ```cache-backend-redis-db=1```
		- ```page-cache=redis```
		- ```page-cache-redis-server=redis```
		- ```page-cache-redis-db=2```
		- ```amqp-host="rabbitmq"```
		- ```amqp-port="5672"```
		- ```amqp-user="guest"```
		- ```amqp-password="guest"```
		- ```amqp-virtualhost="/"```

__B) Run already existing Magento project__

1) Run ```bin/docker/start```

2) Add existing project
	- Paste your existing Magento project to magento folder  

__Setup Xdebug in IDE__

1) Run ```bin/ide/xdebug debug```
	- You can turn off Xdebug by running ```bin/ide/xdebug off``` and turn it on again with ```bin/ide/xdebug debug```, you can also use this command to set all other Xdebug modes (https://xdebug.org/docs/all_settings#mode)  
2) PhpStorm should offer you automatic setup after you add breakpoint and make http request (open magento.local in a browser) and correct settings should be similar to this:

Preferences - PHP - Debug

![Preferences - PHP - Debug](https://i.ibb.co/BZJ4hjz/phpstorm-2.jpg "Preferences - PHP - Debug")

Preferences - PHP - Servers

![Preferences - PHP - Servers](https://i.ibb.co/GVqfVs5/phpstorm.jpg "Preferences - PHP - Servers")

__Setup Nginx and Magento logs in Kibana__

1) TODO

__Cleanup__
- Stop and remove all containers, images and volumes of the project
	- Run ``` bin/docker/cleanup```

## Useful information

- Reference for bin/magento setup:config:set command
	- https://devdocs.magento.com/guides/v2.4/config-guide/prod/config-reference-sens.html
	
## Troubleshooting

- TODO