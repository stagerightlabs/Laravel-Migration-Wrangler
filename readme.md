# Migration Wrangler

Sometimes you may find that you want to port a migrations table from one database to another.   This might occur if you are refactoring your migrations and want to update your production database migrations table to allow future migration tasks to remain in sync with your development database.   This tool provides three artisan commands that should make that process easier.

## Installation

```bash
composer require srlabs/migration-wrangler
```

This package uses automatic [Package Discovery](https://laravel.com/docs/5.5/packages#package-discovery); once your composer installation is complete, you should be good to go.  If not, you may need to manually register the service provider.

## Usage

There are three new artisan commands provided by this package:

### migrations:export

This command takes data from an existing migrations table and writes it to a json file.

Options:
    - database: The name of the database connection you want to pull data from
    - filepath: The destination folder for the generated json file
    - pretty: Optionally write the json in an easily readable format.

### migrations:import

This command takes a json file generated by the export command and uses it to populate the migrations table, replacing the existing data.  You must specify a path to the json file as the first argument to this command.

Options:
    - database: The name of the database connection you want to insert data into
    - pretend: Attempt the import process without making any actual changes to the database.

### migrations:generate

This command traverses your migrations folder and generates a json file based on the migrations found there.  It will automatically put each migration into a separate [batch](https://laravel.com/docs/5.5/migrations#rolling-back-migrations).

Options:
    - path: The location of the migrations folder you want to inspect
    - filepath: The destination folder for the generated json file
    - pretty: Optionally write the json in an easily readable format.