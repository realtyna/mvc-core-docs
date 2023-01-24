---
layout: default
title: Basic Usage
nav_order: 4
has_children: true
---

# Basic Usage

First I will introduce you to ```Main``` class and it's functions then we dig deeper in each function that you can use.

``Main`` class is located in ```./app/Main.php```.

This class is extending ```StartUp``` class, which is responsible for loading our plugin different parts.

In ```Main``` class you see these methods that are overriding ```StartUp``` class methods:

- [init](#init)
- [components](#components)
- [onAdmin](#onAdmin)
- [api](#api)
- [activation](#activation)
- [deactivation](#deactivation)
- [uninstallation](#uninstallation)

---
## init method {#init}
Codes that are written in ```init``` method, will be executed every where.

---
## components method {#components}
We use this method to register our components. read [Components](/mvc-core-docs/docs/components.html).

---
## onAdmin method {#onAdmin}
Codes written in this method will only be executed on admin area.

for example enqueueing an asset or adding an action.

---
## api method {#api}
We use this method to register our api endpoints. read [API](/mvc-core-docs/docs/basic-usage/api.html).

---
## activation method {#activation}
As you already guessed this is our activation method. By default, it will run migrations and seeds.
For more detail about migrations and seeders read [Database](/mvc-core-docs/docs/basic-usage/database.html).

You can add your custom activation codes between START & END comment section

---
## deactivation {#deactivation}
No explanation needed, You already know.

---
## uninstallation {#uninstallation}
By default, it will roll back all changes made to database using phinx read [Database](/mvc-core-docs/docs/basic-usage/database.html).