# Table generator

[![Latest Version on Packagist](https://img.shields.io/packagist/v/advicepharma/tablegenerator.svg?style=flat-square)](https://packagist.org/packages/advicepharma/tablegenerator)
[![Total Downloads](https://img.shields.io/packagist/dt/advicepharma/tablegenerator.svg?style=flat-square)](https://packagist.org/packages/advicepharma/tablegenerator)

A package to create a structured jason that should be consumed with a react component.

## Requirements

You have to install:

- spatie query builder (<https://spatie.be/docs/laravel-query-builder/v3/introduction>)

## Installation

You can install the package via composer:

```bash
composer require advicepharma/tablegenerator
```

## Basic Usage

```php
use Advicepharma\Tablegenerator\Tablegenerator;
use Advicepharma\Tablegenerator\Elements\Action;
use Advicepharma\Tablegenerator\Elements\Column;
use Advicepharma\Tablegenerator\Elements\ActionColumn;
use Spatie\QueryBuilder\QueryBuilder;

$users = QueryBuilder::for(App\Models\User::class);

$table = new Tablegenerator;
$table->query($users)
        ->paginate()
        ->addFilter()
        ->addSorts()
        ->table()
        ->addColumn(
            [
                (new Column)
                    ->field('id')
                    ->label('ID')
                    ->filtrable()
                    ->sortable(),

                (new Column)
                    ->field('name')
                    ->label('Name')
                    ->filtrable()
            ]
        );
```

## Column object

`label(<string>)` column label (header)
`field(<string>)` display the field in `QueryBuilder` object
`filtrable()` set the column filtrable
`sortable()` set the column sortable

## Adding column

Adding column accpets array of `Column` or `Column` object.

```php
$table->->table()
        ->addColumn(
            [
                (new Column)
                    ->field('name')
                    ->label('Name'),
                (new Column)
                    ->field('email')
                    ->label('Email')
            ]
        )
```

or:

```php
$table->->table()
        ->addColumn(
            (new Column)
                ->field('name')
                ->label('Name')
                ->filtrable()
                ->sortable()
        )
```

<<<<<<< HEAD
=======
## Action column

Action column are used to render actions in the table.
Default action are edit and delete:

```php
(new ActionColumn)
    ->label('')
    ->addAction(
        (new Action)
            ->type(Action::ACTION_EDIT)
            ->properties(
                [
                    'link_to' => '/account/users/#id#'
                ]
            )
    )
    ->addAction(
        (new Action)
            ->type(Action::ACTION_DELETE)
            ->properties(
                [
                    'confirm' => true,
                    'confirm_message' => 'Do you really want to delete this user?',
                    'link_to' => route('user.destroy', '#id#', false)
                ]
            )
    )
```

`type` can be whatever you want: this two are the default one.

`properties` can contains all the properties that are going to be consumed by frontend

>>>>>>> 4988002 (Update README.md)
## Pagination

Pagination is super easy: you have to add `->paginate()` to create default pagination structure.
If you want, you can specify the pagesize passing an integer value `->paginate(100)`

## Api resource

If you want to use ApiResource feature, you can add it with

```php
$table->->table()
    ->withResource(YourResource::class)
```

## Relationship column

If you are working with a QueryBuilder with relationship, like:

```php
QueryBuilder::for(App\Models\Post::class)->with('user');
```

Al you need to do is to specify the colum field with dot notation:

```php
(new Column)->field('user.name')->label('User Name')
```

__Unforturnately sorting a relation field is not yet supported__

### Testing

```bash
composer test
```

### Changelog

Please see [CHANGELOG](CHANGELOG.md) for more information what has changed recently.

## Contributing

Please see [CONTRIBUTING](CONTRIBUTING.md) for details.

### Security

If you discover any security related issues, please email giacomo.garavaglia@advicepharma.com instead of using the issue tracker.

## Credits

- [Giacomo Garavaglia](https://github.com/advicepharma)

## License

The MIT License (MIT). Please see [License File](LICENSE.md) for more information.

## Laravel Package Boilerplate

This package was generated using the [Laravel Package Boilerplate](https://laravelpackageboilerplate.com).
