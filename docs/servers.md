# Overview

Servers collection holds all your Forge Servers in one place.

# Initialize Collection

You can start use collection by instantiating `Laravel\Forge\Forge` class. Make sure you've created `Laravel\Forge\ApiProvider` instance - `Forge` depends on it.

```php
<?php

use Laravel\Forge\ApiProvider;
use Laravel\Forge\Forge;

$api = new ApiProvider('token');
$forge = new Forge($api);
```

# Usage

Since `Forge` implements `ArrayAccess` and `Iterator` interfaces, you have several methods to access your servers.

## Access existed servers

You can iterate through entire collection:

```php
<?php

foreach ($forge as $server) {
  // Each $server variable holds instance of `Laravel\Forge\Server` class.
  echo $server->name();
}
```

Or use it as array:

```php
<?php

$server = $forge['server-name'];
echo $server->name();
```

> Lazy Loading
>
> ArrayAccess and Iterator implementations uses lazy loading.
> This means `Forge` class won't load any data until you
> start iterating or performing array operations.

## Get single server

Additionally, `Forge` class can be used to retrieve single server by ID:

```php
<?php

$serverId = 12345;
$server = $forge->get($serverId);

// Force a reload of the server details, overwriting the cached version
$reload = true;
$server = $forge->get($serverId, $reload);
```

## Create new Server

Or create new server via fluent servers builder:

```php
<?php

$oceanCredentialId = 1234;

$droplet = $forge->create()
    ->droplet('my-droplet-name')
    ->usingCredential($oceanCredentialId)
    ->withSizeId(1)
    ->runningPhp('7.1')
    ->withMariaDb('my-database-name')
    ->save();
```

Code sample above will create new 1GB droplet on DigitalOcean with MariaDb and PHP 7.1. Also this will create database `my-database-name`.

[Back to Table of Contents](./readme.md)
