Laravel-FTP
===========

A simple Laravel 6 ftp service provider.

 

Installation
------------

Add the package to your `composer.json` and run `composer update`.

    {
        "require": {
            "uar-daniel-gafitescu/ftp":"dev"
        }
    }
> 

Add the service provider in `config/app.php`:

    'Anchu\Ftp\FtpServiceProvider',

Configuration
------------
Run `php artisan vendor:publish --tag=config` and modify the config file(`config/ftp.php`) with your ftp connections.

You can add dynamic FTP connections with following syntax

```php
Config::set('ftp.connections.key', array(
           'host'   => '',
           'username' => '',
           'password'   => '',
           'passive'   => false,
           'secure'   => false,
));
```

Accessing connections
---------------------
You can access default FTP connection via the `FTP::connection` method:
```php
FTP::connection()->getDirListing(...);
```

When using multiple connections you can access each specific ftp connection by passing connection name:
```php
FTP::connection('foo')->getDirListing(...);
```

Sometimes you may need to reconnect to a given ftp:
```php
FTP::reconnect('foo');
```

If you need to disconnect from a given ftp use the disconnect method:
```php
FTP::disconnect('foo');
```

Basic usage examples
------------
```php
// With custom connection
$listing = FTP::connection('my-ftp-connection')->getDirListing();

// with default connection
$listing = FTP::connection()->getDirListing();
$status = FTP::connection()->makeDir('directory-name');
```