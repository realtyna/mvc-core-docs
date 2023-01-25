---
layout: default
title: Models
parent: Basic Usage
nav_order: 7
---
# Models
We are using Laravel Eloquent for our models. So when you
are creating a model class in ```app/Models``` you should
extend ```Realtyna\MvcCore\Model```.

[Eloquent documentation](https://laravel.com/docs/9.x/eloquent)

You only need to know how to query and create models in database.


## Default table
By default, Eloquent will look for table name that matches
model name(with prefix). For example if your model name is ```User``` it will
look for ```wp_users```.

To change this default behavior you can override ```$table``` property in
your model class.
```php
    protected $table = 'wpl_users';
```
In this case it will look for: ```wp_wpl_users```

## API
You can also retrieve data from WordPress rest APIs internally.

for example if we have a model called ```User```, and we want to
get data from ```wp-json/wpl/v4/users/list``` this is how you do it:
```php
User::api('/wpl/v4/users/list')->method('GET')->send(true);
```

This code will create a GET request to ```wp-json/wpl/v4/users/list``` internally then return the response to you.

### where method
You can also set query params or body params for your request
using ```where()``` method.

Example:
```php
User::api('/wpl/v4/users/list')->method('GET')->where('state', 'LA')->send(true);
```

in ```GET``` method this is like calling:
```
https://example.com/wp-json/wpl/v4/users/lists?state=LA
```

in ```POST``` method it will set ```state=LA``` as body params.

### Header method
By using ```header()``` method you can set an array of custom
headers.

Example:
```php
$headers = [
    'test'  => 'value',
    'test2'  => 'value2',
];
User::api('/wpl/v4/users/list')->method('GET')->header($headers)->where('state', 'LA')->send(true);
```

## toObject method
if you chain ```toObject``` method as last method of your request
it will try to return the response as ```Collection``` or ```Model```(your model: ```User```).

You can't use this method if you used ```send(true)```, it
will only work with ```send()```.

if response is a single object it will return an object of ```User```.

if response is more than one user it will return an object of ```Collection```

Read about [Collection](https://laravel.com/docs/9.x/collections).


Example:
```php
User::api('/wpl/v4/users/list')->method('GET')->where('state', 'LA')->send()->toObject();
```

