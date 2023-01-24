---
layout: default
title: Configs
nav_order: 3
---
# Config

Config file is located in ```./app/Config/config```

Default configs:
```php
[
    'namespace' => 'MustRename',
    'version' => '1.0.0',
    'plugin'  => [
        'name' => 'must_rename'
    ],
    'api' => [
        'namespace' => 'wpl'
    ],
    'path' => [
        'plugin-file-path'  => REALTYNA_MUST_RENAME_BASE_PATH . 'plugin.php',
        'validator-messages' => REALTYNA_MUST_RENAME_BASE_PATH . 'assets/langs/validation.php',
        'phinx' => [
            'conf'  => REALTYNA_MUST_RENAME_BASE_PATH . 'app/Config/phinx.php'
        ],
        'assets' => [
            'css' => plugin_dir_url(REALTYNA_MUST_RENAME_BASE_PATH . 'plugin.php') . '/assets/css',
            'js' => plugin_dir_url(REALTYNA_MUST_RENAME_BASE_PATH . 'plugin.php') . '/assets/js',
        ],
        'plugin_dir' => REALTYNA_MUST_RENAME_BASE_PATH,
        'view' => REALTYNA_MUST_RENAME_BASE_PATH . 'templates',
    ],
    'jwt_secret' => REALTYNA_JWT_SECRET,
]
```

These are required configs for plugin to work properly. You can
change them based on your need (not recommended at all), but you can't remove them.

You should only change configs that were mentioned in [Get Started](/mvc-core-docs/docs/get_started.html).

---
## Usage
By accessing Config class you can get a config using:
```php
//you must not initialize new object of Config class
//In classes that extend part of CORE you can access config object
//through main object like so:
$config = $this->main->config;

//or you can use plugin global variable
//if your plugin.name is realtyna_crm2 in config file
$config = $realtyna_crm2->config;

$config->get('namespace');
```

You can access multidimensional array in config file using dot(.)
```php
$config->get('plugin.name');
```

**Avoid defining constants and use config file**