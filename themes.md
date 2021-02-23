# Themes

- [About Themes](#about-themes)
- [Service Provider](#service-provider)
- [Theme Base](#theme-base)
- [Views](#views)
    - [Templates](#templates)
- [Installation](#installation)    
    - [Composer](#composer)
    - [Manual](#manual)
- [Change Theme](#change-theme)

<a name="about-themes"></a>
## About Themes

Themes within Aldrumo are essentially a Composer Package with Laravel integration. 

Themes have a standard Laravel Service Provider that extends a base Service Provider the Aldrumo Theme Manager provides. This Service Provider should not be used by the Theme to register or boot anything into Laravel. 

This Service Provider is simply to register the Theme's existence with Aldrumo and this is covered by the base Service Provider that the Theme extends.

A Theme should also ship with a "Theme Base". The Theme Base file is essentially another Service Provider that also extends a Theme Base file provided by the Theme Manager. 

This Theme Base is the file that should be used to define any register or boot data. This is because the Theme Base file is only called and run for the Active Theme, this prevents unnecessary registering and booting of data if a theme is not in use.

<a name="service-provider"></a>
## Service Provider

The standard Laravel Service Provider is used to register the Theme's existence to Aldrumo. This is done by registering the [Theme Base](#theme-base) into the Container with a tag.

When creating your own Theme, simply extend the base Service Provider from the Theme Manager. 

Don't forget to also set your own namespace for your theme.

```php 
<?php
namespace AldrumoThemes\Aldrumo21;

use Aldrumo\ThemeManager\Theme\ThemeServiceProvider;

class Aldrumo21ServiceProvider extends ThemeServiceProvider
{
    //
}
```

> {tip} The name of this Service Provider also dictates the name of your Theme. Aldrumo will remove "ServiceProvider" from this class name to get your Theme Name.

### Composer

If you are planning on distributing your Theme via Composer, don't forget to add your Service Provider to the auto-discovery section of the theme's composer.json.

```json 
{
    ...
    
    "extra": {
        "laravel": {
            "providers": [
                "AldrumoThemes\\Aldrumo21\\Aldrumo21ServiceProvider"
            ]
        }
    }
}
```

<a name="theme-base"></a>
## Theme Base

The Theme Base file is essentially another Service Provider. This file is however only called, along with the register and boot methods if it's part of the Active Theme.

It should be called the same as the Theme Name, which in the above examples was `Aldrumo21`.

```php 
<?php

namespace AldrumoThemes\Aldrumo21;

use Aldrumo\ThemeManager\Theme\ThemeBase;

class Aldrumo21 extends ThemeBase
{
   //
}
```

### Register and Boot

If you need to register anything to the container for your theme to work or boot anything then it should be done in this file. 

If you do need to register or boot anything, make sure you call the parent method first. The Theme Base class that is extended performs some setup automatically for you.

```php 
<?php

namespace AldrumoThemes\Aldrumo21;

use Aldrumo\ThemeManager\Theme\ThemeBase;

class Aldrumo21 extends ThemeBase
{
    public function register(): void
    {
        parent::register();

        // your code here
    }

    public function boot(): void
    {
        parent::boot();

        // your code here
    }
}
```

### Options

Within the Theme Base file, 2 options are also available to easily configure the location for your views and templates.

The views path is relative to the Theme Base file and the templates path is relative from the views path.

Below is an example showing the property names, and the default values for these properties.

```php 
<?php

namespace AldrumoThemes\Aldrumo21;

use Aldrumo\ThemeManager\Theme\ThemeBase;

class Aldrumo21 extends ThemeBase
{
    /** @var string */
    protected $viewsPath = '/../resources/views';

    /** @var string */
    protected $templatesFolder = '/templates';
}
```

### Service Provider

Within the Theme Base file, there is also a reference to the main Service Provider for your Theme. This opens up access to certain options and functionality that Laravel Service Providers grant.

To access the Service Provider, use `$this->serviceProvider` within your Theme Base file.

<a name="views"></a>
## Views

If your theme is following the same structure that is followed by the default theme Aldrumo21, then you should not need to manually register your views.

All views, will be automatically made available within Laravel in a [Blade Namespace.](https://laravel.com/docs/8.x/packages#views). The namespace will be your theme's name.

Continuing to use our example of the default Aldrumo theme, `Aldrumo21`. In a standard Laravel application all our views would then be accessible via `Aldrumo21::`, e.g.

```php
return view('Aldrumo21::foo.bar.template');
```

When developing your theme, remember any layout, or view you include will need to be prefixed with the Theme namespace before including. e.g.

```php 
@extends('Aldrumo21::layouts.app')

@include('Aldrumo21::partials.header');
```

<a name="templates"></a>
### Templates

Templates are simply a sub-folder of views within your theme. These views however are the ones that are made available to the user when they create a new page.

Aldrumo will take the filename minus `.blade.php`, as the text to show in the dropdown menu. So make sure your template filenames are descriptive enough to tell the user which template they are selecting.

#### Blocks

When creating your templates, you will need to make use of Blocks. These are the way in which you tell Aldrumo which parts of your template should be editable by the user.

You create an editable block by simply defining a block renderer tag within your template and provide it a key.

```php 
<x-Blocks::renderer key="article-title"></x-Blocks::renderer>
```

The key is used to identify it and allow Aldrumo to show the correct content in the right place.

You can also provide a default value for this editable content.

```php 
<x-Blocks::renderer key="article-title">
  This is a default title
</x-Blocks::renderer>
```

Care should be taken with where, and how you place the blocks. Remember that while the user will be given access to apply styles and edit the look of the content, wrapping your block in certain styles may create a situation which prevents the user from editing the content as they wish.

```php 
<p class="leading">
  <x-Blocks::renderer key="article-body">
    This is a default title
  </x-Blocks::renderer>
</p>
```

<a name="installation"></a>
## Installation

<a name="composer"></a>
### Composer

If you have created your theme as a package and is available in a vcs repository, you can simply composer require your theme into your Aldrumo website.

Make sure you have included the Service Provider in the "auto-discovery" option in your theme's `composer.json` file.

<a name="manual"></a>
### Manual

If your theme is not available for installation via composer then you can still install it manually.

Simply create a sub-folder within the `Themes` folder at the root of your Aldrumo website. Place all the files for your theme in here.

The php namespace for your Service Provider / Theme Base and any other files should be set to `AldrumoThemes`.

You then need to enter the theme's Service Provider into the Laravel Service Provider array found in `config/app.php`.

```php 
    /*
    |--------------------------------------------------------------------------
    | Autoloaded Service Providers
    |--------------------------------------------------------------------------
    |
    | The service providers listed here will be automatically loaded on the
    | request to your application. Feel free to add your own services to
    | this array to grant expanded functionality to your applications.
    |
    */

    'providers' => [

        /*
         * Laravel Framework Service Providers...
         */
         
        /*
         * Package Service Providers...
         */
         
         // place your service provider here
         // e.g.
         AldrumoThemes\MyTheme\MyThemeServiceProvider::class,

        /*
         * Application Service Providers...
         */
   ]         
```

<a name="change-theme"></a>
## Change Themes

Currently there is no GUI for changing the theme with the Aldrumo Admin Panel.

To manually change the theme for your Aldrumo website, open your favourite Database Manager (TablePlus, SequelPro etc...) and open the Aldrumo database.

Find the `settings` table and there should be a row on the table with a `slug` of `activeTheme`. Simply change the `setting_data` column to match your theme's name.

Once saved, the active theme will now be set. Depending on your theme's set up, you may now need to run a "vendor publish" in order to make your theme's assets available.

```bash 
php artisan vendor:publish --force
```

Run that and find your theme to publish the assets.
