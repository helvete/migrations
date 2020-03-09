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


Sample application config
-------
```yaml
parameters:
    migrations:
        dbal: doctrine
        schema: 'application_schema_name'
        table: 'migrations'
        effectiveRole: 'postgres_acl_group_the_app_user_belongs_to'
        allowOutOfOrder: true  # falls back to false if directive missing
migrations:
    dir: %appDir%/../migrations
    driver: pgsql
    dbal: %migrations.dbal%
    withDummyData: false
    diffGenerator: %migrations.dbal%
    groups:
        structures:
            enabled: true
            directory: %appDir%/../migrations/structures
            dependencies: []
            generator: null
            allowOutOfOrder: %migrations.allowOutOfOrder%
        basic-data:
            enabled: true
            directory: %appDir%/../migrations/basic-data
            dependencies:
                - structures
            generator: null
            allowOutOfOrder: %migrations.allowOutOfOrder%
services:
    migrations.driver: Nextras\Migrations\Drivers\PgSqlDriver(
        @Nextras\Migrations\IDbal,
        %migrations.table%,
        %migrations.schema%,
        %migrations.effectiveRole%)
```
