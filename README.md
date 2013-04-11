# PHP Database Connector

This package is simply a fork of [http://github.com/illuminate/database](illuminate/database) to just provide the connectors.

[![Build Status](https://secure.travis-ci.org/robclancy/db-connector.png)](http://travis-ci.org/robclancy/db-connector)

## Installation

Add the following to the "require" section of your `composer.json` file:

```json
	"robclancy/db-connector": "1.0.x"
```

## Basic Usage

You will need a config array, the following shows what can be used...

```php
$config = array(

	'fetch' => PDO::FETCH_CLASS,

	// SQLite
	'database' => __DIR__.'/../database/production.sqlite',
	'prefix'   => '',

	// MySQL
	'host'      => 'localhost',
	'database'  => 'database',
	'username'  => 'root',
	'password'  => '',
	'charset'   => 'utf8',
	'collation' => 'utf8_unicode_ci',
	'prefix'    => '',

	// Postgres SQL
	'host'     => 'localhost',
	'database' => 'database',
	'username' => 'root',
	'password' => '',
	'charset'  => 'utf8',
	'prefix'   => '',
	'schema'   => 'public',

	// SQL Server
	'driver'   => 'sqlsrv',
	'host'     => 'localhost',
	'database' => 'database',
	'username' => 'root',
	'password' => '',
	'prefix'   => '',
);
```

And then to make your connection...

```php

$connector = new Robbo\DbConnector\MysqlConnector;

$pdo = $connector->connect($config);
```

To make things a little easier and more flexible for applications that support multiple database types you can use a factory method to connect.
The config stays the same however you add a driver as well. For example...

```php

$config = array(
	'driver' 	=> 'mysql', // For other types this is 'pgsql', 'sqlite' or 'sqlsrv'
	
	'host'      => 'localhost',
	'database'  => 'database',
	'username'  => 'root',
	'password'  => '',
	'charset'   => 'utf8',
	'collation' => 'utf8_unicode_ci',
	'prefix'    => '',
);
```

Then use the factor like so...

```php
 
$connector = Robbo\DbConnector\Connector::create($config); // Instance of Robbo/DbConnector/MySqlConnector
$pdo = $connector->connect($config);

// You can also have the factory connect for you by passing true as the second parameter, so...
$pdo = Robbo\DbConnector\Connector::create($config, true);

```