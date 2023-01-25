---
layout: default
title: Database
parent: Basic Usage
nav_order: 6
---
# Database
We are using Phinx for managing database.

There are 2 phinx config files in ```app/Config/```.
```phinx.php``` is for the client host so do not change it.

now open ```phinx-local.php``` and right credentials for your mysql server.

**You need to have pdo_mysql installed**

For running phinx commands in your terminal you need it like so:

```bash
vendor/bin/phinx <COMMAND> -c app/Config/phinx-local.php
```

for more information about Phinx read its documentation on 
[Phinx](https://book.cakephp.org/phinx/0/en/intro.html)

---
## Migrations
You need to create a migration file for each table you want to create or alter.

You can create new migrations like so:
```bash
 vendor/bin/phinx create -c app/Config/phinx-local.php CreateNewExampleTable
```

Migration files are located in ```app/Database/migrations```

---
## Seeds

You can create new migrations like so:
```bash
 vendor/bin/phinx seed:create -c app/Config/phinx-local.php MyExampleSeeder
```

Migration files are located in ```app/Database/seeds```

Keep it in mind you should check if data already exists then insert it.

Read more on Phinx documentations.

