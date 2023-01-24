---
layout: default
title: Filters
parent: Basic Usage
nav_order: 3
---
# Filters
Filters are one most used concepts in WordPress like actions.

You can add filters in ```init``` & ```onAdmin``` methods.

## addFilter method
```addFilter``` method is defined as so:
```php
public function addFilter(string $hook, array $callback, int $priority = 10, int $accepted_args = 1)
    {
        $this->validateCallback($callback);
        $this->filters[] = $this->getHook($hook, $callback, $priority, $accepted_args);
    }
```

## addFilter parameters
There is no difference between addFilter and addAction parameters so read [Actions](/mvc-core-docs/docs/basic-usage/actions.html)