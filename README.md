# PHP Config

[![Build Status](https://travis-ci.org/byjg/config.svg?branch=master)](https://travis-ci.org/byjg/config)

A very basic and minimalist component for config management and dependency injection.

## How it Works?


### Setup files:

Create in your project root at the same level of the vendor directory a folder called `config`. 

Inside this folders create files called "config-dev.php", "config-test.php" where dev, test, live, etc
are your environments. 

Your folder will look like to:

```
<project root>
    |
    +-- config
           |
           + config-dev.php
           + config-homolog.php
           + config-test.php
           + config-live.php
   +-- vendor
   +-- composer.json
```

### Create environment variable

You need to setup a variable called "MACHINE_ENV" before start your server. 

This can be done using nginx:

```
fastcgi_param   APPLICATION_ENV  dev;
```

Apache:

```
SetEnv APPLICATION_ENV dev
```

Or Docker-Compose

```
environment:
    APPLIACTION_ENV: dev
```

### Use in your PHP Code

The code below will get a property from the defined environment:

```php
<?php
$property = \ByJG\Util\Config::get('property');
```

By default if the property does not exists an error will be throwed.
If you want to get null instead throw an error use:

```php
<?php
$property = \ByJG\Util\Config::get('property', false);
```

### The `config-xxxx.php` file

```php
<?php

return [
    'property1' => 'string',
    'property2' => true,
    'property3' => function () {
        return xxxxxx;
    },
];
```

You can inherit properties from another environment:

```php
<?php

$config = \ByJG\Util\Config::inherit('homolog');

$config['property2'] = false;

return $config;
```

## Install

```
composer require "byjg/config=1.0.*"
```

## Tests

```
phpunit
```

