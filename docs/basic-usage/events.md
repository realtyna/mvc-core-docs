---
layout: default
title: Events
parent: Basic Usage
nav_order: 10
---
# Events
> You may find all these steps not useful, but keep it mind that we have great plans for this part
> of the core so **Use it**.

Events are very similar to **hooks** in WordPress itself. but there is difference between our events
and WordPress hooks(You'll see the difference in Runners section)

It's a good idea to know about [Event-driven architecture](https://en.wikipedia.org/wiki/Event-driven_architecture).

Let's create an event:

let's create a class that extends ```Realtyna\MvcCore\Event```, and we will create it in
```./app/Events```. There is only one thing to do in this class, you should define
```___construct``` method like so:
```php
<?php

namespace Realtyna\TestPlugin1\Events;

use Realtyna\MvcCore\Event;

class ContactCreated extends Event
{


    public function __construct($contact)
    {
        $this->contact = $contact;
    }
}
```

The ```__construct``` method can accept as many as parameters that you need. you will 
understand more about this in **Listeners**.

But keep it mind that these parameters will be passed to the runner to handle the event.

## Listeners

Now let's create a **listener**:
We will create a class in ```./app/Listeners``` that will extend ```Realtyna\MvcCore\Listener```.
All listeners have to have ```event()``` and ```handle()``` method.

Here is an example:
```php
<?php

namespace Realtyna\TestPlugin1\Listeners\ContactCreated;

use Realtyna\MvcCore\Listener;
use Realtyna\TestPlugin1\Events\ContactCreated;
use WP_REST_Request;

class Webhook extends Listener
{

    public function event(): string
    {
        return ContactCreated::class;
    }

    public function handle($args)
    {
        $request = new WP_REST_Request('POST', '/realtyna/api-connector-pack/v1/action/trigger');
        $request->set_query_params([
            'application' => 'APP1',
            'entity'      => 'contact',
            'action'      => 'create'
        ]);
        $request->set_body(json_encode($args));
        $response = rest_do_request($request);
        $server   = rest_get_server();
        $data     = $server->response_to_data($response, false);
        $json     = wp_json_encode($data);
    }
}
```

In the ```event()``` method we will return the event that this listener is related too.

In the ```handle()``` method we will code our logic and this method will accept an
array of the data that we saved in our event as property.

## Trigger
We should be able to fire an event in any part of our code. so when you created an event
you can fire it like so:
```php
Event::trigger(ContactCreated::class, $contact);
```
You can pass as many as parameters that your event will accept.

When you do this there will be a scheduled action that will execute ASAP.
> later you will be able to schedule your event to run for example in 5 minutes

## Runners
One of the best advantages of using this approach is that we are using
[Woocommerce Action Scheduler](https://github.com/woocommerce/action-scheduler).
 in **Trigger** section I mentioned that the action will be done ASAP.

This how it exactly works. When ever there is an event fired it will be stored in
a table in database and each time someone visits admin area of the WordPress, these
actions will run(We have a new service called Cron Job Server that will complete.).



