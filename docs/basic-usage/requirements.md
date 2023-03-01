---
layout: default
title: Requirements
parent: Basic Usage
nav_order: 2
---
# Requirements
Each plugin may have its own **requirements**.

By default, there is 2 requirement in MVC Core:
 
1. PDO
2. REALTYNA_JWT_SECRET


## requirements method
```requirements``` method is defined in ```Main.php```:

by default, it will check to see if Realtyna API plugin is installed or not.

```php
public function requirements(): bool
{
    $valid = true;
    if ( !is_plugin_active( 'realtyna-API/plugin.php' ) ) {
        $this->addNotice('<p><strong>Realtyna API plugin</strong> is not activated. you need to install and activate it.</p>');
        $valid = false;
    }
    return $valid;
}
```


if the mentioned method returns ```false```, it will prevent the plugin from running.

## addNotice method

This method is defiend like so:
```php
public function addNotice(string $message, string $type = 'error', bool $isDismissible = false)
{
    $this->notices[] = [
        'type' => $type,
        'message' => $message,
        'isDismissible' => $isDismissible,
    ];
}
```

```$message``` is self explaining.

```$type``` can be one of the followings:
- error (this is the default value)
- warning
- success
- info

If you pass ```true``` for ```$isDismissible``` it will add a close icon to the notice.

