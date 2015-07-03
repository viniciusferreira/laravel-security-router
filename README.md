#Security Router - Service

[Readme em Português](https://github.com/resultsystems/laravel-security-router/blob/master/README-pt_BR.md).

## Installation

### 1. Dependency

Using <a href="https://getcomposer.org/" target="_blank">composer</a>, execute the following command to automatically update your `composer.json`:

```shell
composer require resultsystems/laravel-security-router
```

or manually update your `composer.json` file

```json
{
    "require": {
        "resultsystems/laravel-security-router": "1.*"
    }
}
```

### 2. Provider

You need to update your application configuration in order to register the package, so it can be loaded by Laravel. Just update your `config/app.php` file adding the following code at the end of your `'providers'` section:

```php
// file START ommited
    'providers' => [
        // other providers ommited
        'ResultSystems\SecurityRouter\Providers\SecurityRouterServiceProvider',
    ],
// file END ommited
```

###Made use:

Create your config file config/PACOTE.php

####Exemple:

```php
    'security'     => [
        'create'     =>   [
            'protected'  =>  false,
            'middleware' =>  [],
            'defender'   =>   [
                'load'       =>  true,
                'middleware' =>  ['sua-middware'],
                'can'        =>  ['product.create','product.store'],
                'any'        =>  true,
                'is'         =>  null,
            ],
         ],
        'store'     =>   [
            'protected'  =>  false,
            'middleware' =>  [],
            'defender'   =>   [
                'load'       =>  true,
                'middleware' =>  ['sua-middware'],
                'can'        =>  ['product.store'],
                'any'        =>  false,
                'is'         =>  null,
            ],
         ],
        'update'     =>   [
            'protected'  =>  false,
            'middleware' =>  [],
            'defender'   =>   [
                'load'       =>  true,
                'middleware' =>  ['sua-middware'],
                'can'        =>  ['product.store'],
                'any'        =>  false,
                'is'         =>  null,
            ],
         ],
    ],
```

####Use:

```php
$security=$this->app['security.router'];

$security=$security
    ->setFixedSecurity(['as'=>'index'])
    ->getConfig('storehouse-product', 'create');

Router::get('/product/create', $security,function (){
    return 'Eu estou protegido';
});

$security=$security
    ->setFixedSecurity(['as'=>'store'])
    ->getConfig('storehouse-product', 'store');

Router::post('product', $security,function (){
    return 'Eu estou protegido';
});

$security=$security
    ->setFixedSecurity(['as'=>'update','Uses'=>'Controller@update'])
    ->getConfig('storehouse-product', 'update');

Router::put('product', $security);

```