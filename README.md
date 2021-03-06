# CrudGen Laravel (Laravel 5.2 and above)

CrudGen Laravel is a package that you can integrate in your Laravel to create a REAL CRUD (controller filled, views, model with relationships, request file with rules and the migration file).

## Install

CrudGen Laravel uses Package Auto-Discovery, so doesn't require you to manually add the ServiceProvider.

Run composer command:

``` composer require mrdebug/crudgen ```

## Laravel 5.5+

If you don't use auto-discovery :

2\. Add service provider to app.php config file.
```php 
'providers' => [
    //... 
    Mrdebug\Crudgen\CrudgenServiceProvider::class,
]
```

3\. If you don't use Laravel Collective Form package in your project, install it:

``` composer require laravelcollective/html ```

and add it to app.php config file :
```php
'providers' => [
    //... 
    Collective\Html\HtmlServiceProvider::class,
]

'aliases' => [
    //...
    'Form' => Collective\Html\FormFacade::class,
    'Html' => Collective\Html\HtmlFacade::class,
]
```

4\. Publish config file and default-theme directory for views

``` php artisan vendor:publish ```


## Usage

### Creating Crud

``` php artisan make:crud nameOfYourCrud "column1:type, column2" ```

Available options:

- column is the name of your column sql (ID field is already present)
- type is optional and it's the sql type of your column (by default is "string"). 3 choices are available :
    - string is varchar in sql and converted by an input type text in html
    - text is text in sql and converted by a textarea in html
    - integer is int in sql and converted by an input type text in html


### Migration

A migration file is created in your **database\migrations** directory. If necessary edit it and run :
   
``` php artisan migrate ```

### Routes

Create your routes for this new controller, you can do this :

``` Route::resource('url', 'YourController'); ```

### Controller

A controller file is created in your **app\Http\Controllers** directory. All default methods (index, create, store, show, edit, update, destroy) are filled with your fields.

### Request

A request file is created in your **app\Http\Requests** directory. By default, all fields are required, you can edit it according to your needs.

### Views

A views directory is created in your **resources/views** directory. By default, all views extends a template called "default". And the content is in a section called "content".
You can change it in the config file: config/crudgen.php. 2 config options are available:

##### views_style_directory
Is the directory name in resources/crudgen/views, you want to use. A "default-theme" directory is added when you publish vendor assets. 
You can duplicate/remove it and add multiple themes according your needs.

##### separate_style_according_to_actions
Each 4 views (index, create, edit, show) can have different @extends and @section options

You can create views independently of the CRUD generator with :
``` php artisan make:views nameOfYourDirectoryViews "column1:type, column2" ```

## Remove a CRUD

You can delete all files created by the make:crud command at any time (you don't need to remove all files by hand)

``` php artisan remove:crud nameOfYourCrud --force ```

--force (optional) can delete all files without confirmation


## License

This package is licensed under the [license MIT](http://opensource.org/licenses/MIT).
