# Installation

- [About Aldrumo](#about-aldrumo)
- [Installation](#installation)
    - [Requirements](#requirements)
    - [Setup](#setup)
    
<a name="about-aldrumo"></a>
## About Aldrumo

Born out of a failed side-project, Aldrumo is one of the first TALL stack Content Management Systems. Built upon the latest technologies, Aldrumo's mission is to provide a great experience for both the developer and the end user.

Built upon a standard Laravel and Livewire installation, Aldrumo lives as tested packages meaning you still get the full power of Laravel, with no compromise. This, along with growing extensive documentation makes for a great developer experience when building your site.

With an amazing WYSIWYG editor and the SPA feel thanks to Livewire, Aldrumo also aims to give the end user a fantastic and easy to use way to manage their website!

<a name="installation"></a>
## Installation

Before getting started setting up your first site with Aldrumo, we recommend you become familiar with the process of setting up an instance of the [Laravel Framework](https://laravel.com/docs/8.x/installation#your-first-laravel-project).

<a name="requirements"></a>
### Requirements

Apart from needing a MySQL database, Aldrumo has no extra requirements other than those required to run the Laravel Framework, requirements include:

- PHP >= 7.3
- BCMath PHP Extension
- Ctype PHP Extension
- Fileinfo PHP Extension
- JSON PHP Extension
- Mbstring PHP Extension
- OpenSSL PHP Extension
- PDO PHP Extension
- Tokenizer PHP Extension
- XML PHP Extension

You can read more on Laravel's requirements [here](https://laravel.com/docs/8.x/deployment#server-requirements).

<a name="setup"></a>
### Setup

While installing Aldrumo into an existing project is possible, we currently recommend that a fresh Laravel installation be used.

Before starting make sure you have a MySQL database setup and have the connection details ready.

Assuming you have the [Laravel Installer](https://laravel.com/docs/8.x/installation#the-laravel-installer) configured, create a fresh Laravel installation.

```bash
laravel new mysite
```

Then navigate into the newly created directory and simply use composer to require `aldrumo/core`.

```bash
cd ./mysite
composer require aldrumo/core
```

Lastly, run the Aldrumo's installation command via artisan.

```bash
php artisan aldrumo:install
```

You will be asked a series of questions, for your site name / url, as well as database connection details and the initial admin user details.

Once complete, Aldrumo will be setup and installed! Simply navigate in your browser to your sites url to view the default page. 

![Screenshot of Aldrumo Default Page](/screenshots/docs/default-page.png "Screenshot of Aldrumo Default Page")

From here, you can click to access the admin area and login using the details you just entered during installation.
