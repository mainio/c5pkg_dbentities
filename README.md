# IMPORTANT UPDATE AFTER CONCRETE5.7.4

We got all the functionality provided by this package merged into the core,
so this is no longer required for using Doctrine entities within your packages.
Please see our [reference implementation](https://github.com/mainio/c5_entities_example)
on how to use Doctrine entities within a concrete5 package if that is what you
are looking for.

This all works out of the box for all concrete5 versions after 5.7.4.


# Doctrine Entities for concrete5 Packages

This package provides simple classes to enable the use of Doctrine entities
within concrete5 package context. This only works within the concrete5 context
which means that this cannot be used as a standalone package. It is always
required that these classes are used in the concrete5 context.

This is provided as an example implementation of how this could be done within
the concrete5 package context. We have no plans to publish this into Packagist
since we hope the functionality that this provides will become part of the
concrete5 core at some point. But for now (concrete5.7.2), we need some
external solution to make this possible. And we use this solution currently
ourselves until the core will provide similar functionality.


## About the classes


### Mainio\C5\Entity\Entity
The Entity class provided within this package is a simple class that allows
accessing the entity variables from outside of the class. All package's entity
classes should extend this class. It also allows protecting certain class
variables to be read or written (or both) from outside of that Entity class.
Please see the class comments for further information.


### Mainio\C5\Entity\Package
The Package class is a base package class that extends the concrete5's internal
Package class. This class provides additional functionality related to the
package's entity management. This functionality includes providing a package
specific EntityManager and automatic installation for database tables of the
entities and automatic migrations of the database during package upgrades. The
class also provides functionality to automatically generate the package proxy
classes during the development phase of the package.


## How to use

First of all, add this library through this git repo to the composer.json of
your concrete5 package (located at the root of your package folder). In its
simplest form, your compser.json could look like this when including this
library through this git repo:
```json
{
    "repositories": [
        {
            "type": "git",
            "url": "https://github.com/mainio/c5pkg_dbentities.git"
        }
    ],
    "config": {
        "optimize-autoloader": true
    },
    "require": {
        "php": ">=5.3.3",
        "mainio/c5-dbentities": "dev-master"
    }
}
```

After that, do this:

1. Run `composer install` in the root of your package folder to install the
   composer dependencies into the `vendor` directory of your concrete5 package
2. Make your Package class extend \Mainio\C5\Entity\Package
3. Create your package entities within the /src/Entities directory within your
   package folder
4. Add the following configuration to your /config/app.php:
```php
return array(
    // ...
    'package_dev_mode' => true,
    // ...
);
```

The last configuration enables the automatic entity proxy class generation for
your development machine. This does not need to happen in the final version of
the package as it might cause some problems regarding the directory level
permissions required for it to happen.

An example on how to use this package is available as a reference
implementation in the following repository:

https://github.com/mainio/c5_entities_example


## License

Licensed under the MIT license. See LICENSE for more information.

Copyright (c) 2014 Mainio Tech Ltd.
