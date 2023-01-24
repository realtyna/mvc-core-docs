---
layout: default
title: Actions
parent: Basic Usage
nav_order: 2
---
# Action
One of the most important part of plugin development in WordPress is
**Actions**.

You can add actions in ```init``` & ```onAdmin``` methods.

## addAction method
```addAction``` method is defined as so:
```php
public function addAction(string $hook, array $callback, int $priority = 10, int $accepted_args = 1)
    {
        $this->validateCallback($callback);
        $this->actions[] = $this->getHook($hook, $callback, $priority, $accepted_args);
    }
```

## addAction parameters
```$hook``` & ```$priority``` &  ```$accepted_args``` does not need
any explanation.

But for callbacks you need to create a controller first.

You can create your controllers in ```./app/Controllers```.
controller is a class that you write your login in it.

after creating you class in given folder you should add it under this namespace:
```namespace Realtyna\YOUR-PLUGIN-NAMESPACE\Controllers;```

after creating your controller class for example ```UserController```, create a public method for example: ```index```

now you can register your action like so:
```php
$this->addAction('example-hookname', [UserController::class, 'index'], 5, 1);
```

You can also create sub folders for your controllers but be careful about their namespaces.
for example, you create your controller like so:
```php
./app/Controllers/Admin/Pages/ExampleController.php
```
so your namespace will be:
```namespace Realtyna\YOUR-PLUGIN-NAMESPACE\Controllers\Admin\Pages;```

