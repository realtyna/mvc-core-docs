---
layout: default
title: API
parent: Basic Usage
nav_order: 4
---
# API
API is future of programming, and thankfully WordPress is working
on this subject.

You register you API endpoints in ```api``` method of ```Main``` class.

We have defined a method to register endpoints that you should use it for
each one of your APIControllers.
## addAPI method
```addAPI``` method is defined as so:
```php
public function addAPI(string $version, string $baseRoute, $class, array $callbacks)
{
    foreach ($callbacks as $callback) {
        $this->apis [$version][$baseRoute][$class][] = $callback;
    }
}
```
You should use this method like so:
```php
$this->addAPI();
```

## addAPI Parameters
Pass the version on API that you are working on to ```$version```. Example: ```v4```

If you want to create endpoints ```users``` your ```$baseRoute``` will
be: ```users```.

```$class``` parameter is your APIController class.

For cleaner structure you should create your APIControllers in
```./app/Controller/API``` folder.

I recommend create a sub folder based on your versions, so if you want to add
an endpoint to api ```v4``` you should create the APIController class in this path:
```./app/Controllers/API/V4```

And your version as prefix to Controller name for example if I want
to add ```UserAPIController``` for ```v3``` API I name it like so:
```V3UserAPIController```.

You should extend ```Realtyna\MvcCore\API``` in the APIController.

now for ```$callbacks``` parameter you should pass an array that represent your methods
in the APIController class.

For example my ```$callbacks``` array for ```V3UserAPIController``` will be:
```php
[
    'login',
    'register',
    'forgetPassword'
]
```

By doing this you should create 3 public methods called ```login``` & 
```register``` & ```forgetPassword``` inside ```V3UserAPIController```.

So you have something like this:
```php
$this->addAPI('v3', 'user', V3UserAPIController::class, [
    'login',
    'register',
    'forgetPassword'
])
```

Finally in each of this method you use ```register_rest_route``` method.

for example in ```login``` method I register my endpoint like so:

```php
public function login()
    {
        register_rest_route($this->namespace . '/' . $this->version, $this->baseRoute . '/user', array(
            'methods'  => [WP_REST_Server::CREATABLE],
            'callback' => [$this, 'loginRouteCallback'],
            'args'     => [
                'email'  => [
                    'description' => 'E-Mail',
                ],
                'password'  => [
                    'description' => 'Password',
                ]
            ]
        ));
    }
```

```$this->namespace``` is coming from configs.
**We have defined ```wpl``` as our default namespace, try not to change it.** 

```$this->verion``` & ```$this->baseRoute``` is coming from addAPI Parameters.
>We will add an easier helper to register endpoints but by with this approach you are not limited at all.

---
## Validator

When you extend ```Realtyna\MvcCore\API``` you have access to validator.

For validating incoming request you should define your rules first.
For example, I want to validate ```login``` request. so my rules array will be:
```php
$rules = [
    'email' => ['required', 'email'],
    'password' => ['required'],
];
```

Complete list of rules are:
```php
[
    "array",
    "between",
    "boolean",
    "confirmed",
    "date",
    "date_format",
    "digits",
    "digits_between",
    "email",
    "exists",
    "unique",
    "file",
    "filled",
    "image",
    "json",
    "mimes",
    "mimetypes",
    "numeric",
    "regex",
    "required",
    "size",
    "string",
    "timezone",
    "url",
    "min"
];
```

As you know you have access to ```WP_REST_REQUEST $request``` in your endpoint
callback. so finally to validate a request you do so:
```php
$rules = [
    'email' => ['required', 'email'],
    'password' => ['required'],
];
$validation = $this->validator->validate($request, $rules);
if(!$validation['valid']){
    $this->returnValidationErrorMessages($validation['errors']);
}
```

Validation errors are stored in ```assets/langs/validation.php```. Try not to change them.


## Public routes
By default, all routes are guarded that means you should pass
Authorization header in your request.

We use JWT Auth for Authorization.

But if you want to create a public endpoint, you should create a property
called ```$publicRoutes``` in your APIController.

For our example ```login``` endpoint should be public so I add this
to my ```V3UserAPIController```:
```php
public array $publicRoutes = [
    'user/login'
];
```

## sendResponse method
Of course you need to return a response for your endpints.
To do so you can use ```sendResponse``` method that accepts 
3 parameters:
- success (boolean)
- data (array)
- statusCode (int)

Example:
```php
$this->sendResponse(true, ['token'=> 'asdasdasd'], 200);
```

