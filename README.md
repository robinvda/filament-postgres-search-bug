## Requirements
Tested with:
- PHP 8.4.1
- Laravel 12.37.0
- Livewire 3.6.4
- PostgreSQL 17.5 (see docker-compose.yml)

## Setup

- `composer install`
- `php artisan migrate --seed`
- Open your browser to http://localhost:8000/admin
- Login with `test@example.com`|`admin`
- Go to *Customers* page
- Search for anything
- An error like this will pop up: `Illuminate\Database\QueryException` `SQLSTATE[42703]: Undefined column: 7 ERROR: column ""name"::text" does not exist LINE 1: ...ect count(*) as aggregate from "customers" where ("""name"":... ^ (Connection: pgsql, SQL: select count(*) as aggregate from "customers" where ("""name""::text"::text like %a%))`

## Additional notes
Only happens when using `searchable()` on the `Table`, not on the `Column`s.

```php
return $table
    ->columns([
        TextColumn::make('name')
            ->searchable(), // This is fine
    ])
    ->searchable([ // This causes the error
        'name'
    ]);
```
