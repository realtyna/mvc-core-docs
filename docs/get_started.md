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
---  
## Namespace
>We will create a CLI command to do this automatically in next versions

Open ```composer.json``` and change ```MustRename``` namespace under ```psr-4``` section.

Choose you namespace carefully to avoid conflicts.

For example if your plugin name is realtyna-crm-2 your namespace should something like: ```CRM2```

Now you have change namespaces and constants and config file.

Then open ```plugin.php``` and use correct namespace for ```Main``` class.

You should change ```Main``` class namespace too so go to ```app/Main.php``` and change the namespace.

At last run the following command in you terminal:
```bash  
composer dump-autoload
```  
---  
## Base path constant
>We will create a CLI command to do this automatically in next versions

There is constant defined in ```plugin.php``` that represent plugin base path.

Change ```MUST_RENAME``` in ```REALTYNA_MUST_RENAME_BASE_PATH```.

For example change it to ```REALTYNA_MVC2_BASE_PATH```.  
then go to ```./app/Config/config.php``` and use new constant instead of the old one.
 
---  
## define REALTYNA_JWT_SECRET
>We will create a CLI command to do this automatically in next versions

you should define ```REALTYNA_JWT_SECRET``` in ```wp-config.php```:
```php  
define('REALTYNA_JWT_SECRET', 'YOUR SECRET');  
```  
If this constant is already defined don't change it.

---  
## Change version option name
In ```Main.php``` is two function called ```activation``` and ```onUpdate``` that are setting an option  
called ```realtyna_must_rename_version```. You should change ```must_rename```.

---  
## Activate your plugin
You are all set, activate your plugin and enjoy your MVC based plugin.