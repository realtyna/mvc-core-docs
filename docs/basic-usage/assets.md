---
layout: default
title: Assets
parent: Basic Usage
nav_order: 1
---
# Assets
When it comes to enqueueing or registering assets, we are talking about JS & CSS files.
 There is 2 methods that you can use in ```init``` & ```onAdmin``` methods:
- [addStyle](#addStyle)
- [addScript](#addScript)

## addStyle {#addStyle}
```addstyle``` method is defined as so:
```php
public function addStyle(
        string $handler,
        string $path,
        array $dep = [],
        bool $isAdmin = false,
        bool $enqueue = true,
        string $version = null
    ) {
        $this->styles[] = [
            'handler' => $handler,
            'path' => $path,
            'dep' => $dep,
            'is_admin' => $isAdmin,
            'enqueue' => $enqueue,
            'version' => $version
        ];
    }
```

You should use this method like so:
```php
$this->addStyle();
```

### addStyle Parameters
```$handler``` parameter does not need any explanation because you already know.

for ```$path``` parameter you only need to pass file name of your css.
Because it will automatically load it from assets folder that is defined in config folder.

For example if you create a CSS file named ```main.css``` in ```./assets/css``` you only need to
pass ```main.css``` as ```$path``` parameter. You can also create sub folders, for example you create
a CSS file like so: ```./assets/css/admin/listings/base.css```. In
this case your ```$path``` parameter will be ```admin/listing/base.css```

```$dep``` parameter does not need any explanation too.

```$is_admin``` is deciding to register given style with which hook
```wp_enqueue_scripts``` or ```admin_enqueue_scripts```.

If you pass ```true``` as ```$enqueue``` parameter (which it's default value is ```true```) it will
enqueue style for you but if you pass ```false``` it will only 
register it for you and you use it's ```handler``` as ```dep``` for other styles you
will add.

```$version``` parameter does not need any explanation because you already know.

---
## addScript {#addScript}
```addScript``` method is defined as so:
```php
public function addScript(
        string $handler,
        string $path,
        array $dep = [],
        bool $isAdmin = false,
        bool $inFooter = false,
        bool $enqueue = true,
        string $version = null
    ) {
        $this->scripts[] = [
            'handler' => $handler,
            'path' => $path,
            'dep' => $dep,
            'enqueue' => $enqueue,
            'in_footer' => $inFooter,
            'is_admin' => $isAdmin,
            'version' => $version
        ];
    }
```

### addScript Parameters
There is only 1 difference from addStyle method:
```#in_footer``` parameter which decides to enqueue this script in footer
or not.
