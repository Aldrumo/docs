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
