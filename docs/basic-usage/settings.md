---
layout: default
title: Views
parent: Basic Usage
nav_order: 9
---
# Settings
We are using Carbon fields to generate plugin setting pages.

Read [Carbon fields](https://docs.carbonfields.net/) for more information.

**You can use this package for several usages:**
- Post meta
- Term Meta
- Widgets (read [Widgets](/mvc-core-docs/docs/basic-usage/widgets.html))
- Nav menu item options

## How to add setting page
Setting page classed are located in ```app/Settings```. 

You should register them using ```addSetting()``` method in
```Main.php``` in ```settings()``` method.

Example:

```php
public function settings()
{
    $this->addSetting(Setting::class);
}
```

My Setting class is:
```php
namespace Realtyna\MustRename\Settings;

use Carbon_Fields\Container;
use Carbon_Fields\Field;

class Setting extends \Realtyna\MvcCore\Setting
{

    public static function registerPluginOptions()
    {
        Container::make('theme_options', __('Realtyna Sample setting page'))
            ->add_tab( __( 'General' ), array(
                Field::make( 'text', 'crb_first_name', __( 'First Name' ) )->set_required(true),
            ) );
    }
}
```

the Realtyna Sample setting page is already registered when
you create new plugin, so Just change it.