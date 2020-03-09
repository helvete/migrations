Nextras Migrations
==================

[![Build Status](https://travis-ci.org/nextras/migrations.svg?branch=master)](https://travis-ci.org/nextras/migrations)
[![Downloads this Month](https://img.shields.io/packagist/dm/nextras/migrations.svg?style=flat)](https://packagist.org/packages/nextras/migrations)
[![Stable Version](https://poser.pugx.org/nextras/migrations/v/stable)](https://packagist.org/packages/nextras/migrations)
[![Code coverage](https://img.shields.io/coveralls/nextras/migrations.svg?style=flat)](https://coveralls.io/r/nextras/migrations)

For more information read **[documentation](https://nextras.org/migrations/docs)**.

**Supported databases:**
* PostgreSQL
* MySQL

**Supported DBALs:**
* [Nextras DBAL](https://github.com/nextras/dbal)
* [Nette Database](https://github.com/nette/database)
* [Doctrine DBAL](https://github.com/doctrine/dbal)
* [dibi](https://github.com/dg/dibi)


License
-------

*Based on [Clevis\Migration](https://github.com/Clevis/Migration) by Petr Procházka and further improved.*

New BSD License. See full [license](license.md).

Differences over Nextras
-------

1. Allow to set effective role under which the migrations are run against the database. This change is essential to support postgres group ACL mode.
1. Allow out-of-order migrations execution. This alteration is useful in case of many environments having various branch lifetime while vast majority of migrations is simply additive.
