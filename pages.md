# Pages

- [About Pages](#about-pages)
- [Page URLs](#page-urls)
    - [Routing](#routing)

<a name="about-pages"></a>
## About Pages

Pages are generated by the end user from the Aldrumo admin panel. These pages are created by first selecting a relevant template that the selected Theme provides. 

Certain areas of that template will be editable via the WYSIWYG editor and the inline editor toolbar to create the page.

This method was chosen as it allows the Theme creators to steer the direction of how a page and website should look. In agency settings, designers spend a lot of time crafting the perfect designs for the website. Aldrumo aims to reduce the pain here by preventing end users from having "drag and drop" capabilities that can reduce the appeal of these designs if handled incorrectly.

<a name="page-urls"></a>
## URLs / Routing

> {note} Pages are still missing a lot of functionality. They are the main focus of early alpha development so improvements will be coming.

A page's url is generated upon saving the page and is generated from a "sluggable" version of the page title. Currently it cannot be edited, neither can the page title.

<a name="routing"></a>
### Routing

Laravel provides Aldrumo with a powerful router, as a result we let Laravels router handle as much of the routing as possible.

When an action is performed on a page, Aldrumo runs it's Route Loader package. This package generates fixed routes based on the current "Active" pages and saves them to a cache file. This is the cache file from Aldrumo.com.

```php 
<?php

use Illuminate\Support\Facades\Route;

Route::get('/', 'Aldrumo\Core\Http\Controllers\PageController')->name('route-1');
Route::get('features', 'Aldrumo\Core\Http\Controllers\PageController')->name('route-2');
Route::get('demo', 'Aldrumo\Core\Http\Controllers\PageController')->name('route-3');
```

When setting the routes, we also set the page id as part of the route name. This means once Laravel's router has matched a URL we can grab the route name from the request and load the page from the primary key rather than a slower "wildcard lookup" based on the slug.

