---
layout: default
title: Components
parent: Basic Usage
nav_order: 5
---
# Components
We have created a way to create different modules in your plugin.

You can register your components in ```components``` method in ```Main``` class by using:
```php
$this->addComponent()
```


## addComponent Method
```addComponent``` is defined as so:
```php
public function addComponent($component): void
{
    $this->components [] = $component;
}
```

And you should pass your component class as its parameter.

Components should be created in ```./app/Components```.

For creating a new component create a class in ```./app/Components```, which that class
extends ```Realtyna\MvcCore\Component``` class from the core.

In your component class you have to define ```register()``` method.

## Usage concept
Components are used to create cleaner and more structured plugins. So you should try to
contain of all of your logic in its own component with no 
dependency to other components. of course sometimes these dependencies are
unavoidable.

For example, you want to
add a menu to admin dashboard, in this case I create my component class in:
```./app/Components/Admin/Menu``` and I call my Component ```BaseMenu```.

In ```register``` method of ```BaseMenu``` I'll add my actions:
```php
public function register()
{
    add_action('admin_menu', array($this, 'add_admin_pages'));
}
```

and I define my callbacks in this class too, for example:
```php
public function add_admin_pages()
{
    add_menu_page(
        __('Test menu page for presentation', 'raeltyna-test-mvc'),
        __('Test menu page for presentation', 'raeltyna-test-mvc'),
        'manage_options',
        $this::$menu_slug,
        array($this, 'page_callback'),
        'dashicons-phone',
        10
    );
}

public function page_callback()
{
    realtyna_get_template_part('admin/index', '', true);
}
```

```realtyna_get_template_part``` method is explained in [Views](/mvc-core-docs/docs/basic-usage/views.html).

finally we have a component that add a menu to WordPress admin dashboard.


Another example:
I want to add Phone number field to users, so I create ```PhoneNumber``` class in:
```./app/Components/CustomFields/User/PhoneNumber.php```

and my class will be:

```php

class PhoneNumber extends Component
{

    public function register()
    {
        add_filter('user_contactmethods',array($this, 'add_custom_field'),10,1);
    }

    function add_custom_field( $contactmethods ) {
        $contactmethods['phone_number'] = __('Phone Number', 'realtyna-text-domain');
        return $contactmethods;
    }
}
```