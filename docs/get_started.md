---
layout: default
title: Get Started
nav_order: 2
---

# Get Started

---
## Installation

Go to WordPress plugins folder and run this command in terminal:
``` bash  
composer create-project realtyna/plugin-structure <NAME OF YOURPLUGIN>
```
for example:
```bash  
composer create-project realtyna/plugin-structure realtyna-api
```  

By running this command a folder named "realtyna-api" will be created in your plugins folder

Go into created folder:

```bash  
cd realtyna-api
```  

Run composer update:

```bash  
composer update
```


then you should set up plugin name and namespace. for that you can 
simply run the following command in your terminal:

```bash
php realtyna.php setup:plugin
```

This command will ask you 3 questions:
- What is your plugin name(For Example: Realtyna Home Valuation)
  - This will be used for plugin name in the comment section
  - Make sure you enter the full name that will be shown in the WordPress dashboard and include **Realtyna** in your name
- What is your plugin namespace(Insert CamelCase, for example: HomeValuation)
  - **Realtyna** is already included in the namespace so just enter your product namespace
- What is your plugin API namespace(for example: home-valuation)
  - namespaces are already prefixed with **realtyna/** so just enter your application api namespace without any version
---  
## define REALTYNA_JWT_SECRET
you should define ```REALTYNA_JWT_SECRET``` in ```wp-config.php```:
```php  
define('REALTYNA_JWT_SECRET', 'YOUR SECRET');  
```  
If this constant is already defined don't change it.

---  
## Change version option name
>We will create a CLI command to do this automatically in next versions

In ```Main.php``` is two function called ```activation``` and ```onUpdate``` that are setting an option  
called ```realtyna_must_rename_version```. You should change ```must_rename```.

---
## Config 
change following configs:

**```plugin.name``` should be under_scored, do not use dash (-) for it.**
```php
[
    'namespace' => 'MustRename',
    'plugin' => [
        'name' => 'must_rename'
    ]
]
```
---  
## Activate your plugin
You are all set, activate your plugin and enjoy your MVC based plugin.