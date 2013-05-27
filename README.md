# PHP Unoconv

[![Build Status](https://secure.travis-ci.org/alchemy-fr/PHP-Unoconv.png?branch=master)](http://travis-ci.org/alchemy-fr/PHP-Unoconv)

An Object Oriented library which allow easy to use file conversion with Unoconv.

## Install

The recommended way to install PHP-Unoconv is [through composer](http://getcomposer.org).

```JSON
{
    "require": {
        "php-unoconv/php-unoconv": "~0.2"
    }
}
```

## Documentation

Documentation available at http://php-unoconv.readthedocs.org/

## API Usage

To instantiate Unoconv driver, the easiest way is :

```php
$unoconv = Unoconv\Unoconv::create();
```

You can customize your driver by passing a `Psr\Log\LoggerInterface` or
configuration options.

Available options are :

 - timeout : the timeout for the underlying process

```php
$unoconv = Unoconv\Unoconv::create($logger, array('timeout' => 42));
```

To transcode a file, use the `transcode` method. For the complete format list
supported by unoconv, refer to the unoconv CLI.

```php
$unoconv->transcode('document.docx', 'pdf', 'document.pdf');
```

You can optionaly transcode a given page range using the fourth argument :

```php
// pages 1 to 14
$unoconv->transcode('document.docx', 'pdf', 'document.pdf', '1-14');
```

## Silex Service Provider

A [Silex](silex.sensiolabs.org) Service Provider is available, all parameters
are optionals :

```php
$app = new Silex\Application();
$app->register(new Unoconv\UnoconvServiceProvider(), array(
    'unoconv.logger'  => $app->share(function () { return $app['monolog']; }), // use Monolog service provider
    'unoconv.binary'  => '/path/to/custom/binary',
    'unoconv.timeout' => 42,
));
```

## License

Released under the MIT license
