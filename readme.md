## Homestead-Laravel-Heroku-Nginx

A base Laravel 4.2.11 which can be used in a Homestead [multi-site setup](http://scotch.io/tutorials/php/getting-started-with-laravel-homestead) for both local development and to deploy into production on Heroku.

### Additions for simple deployment on Heroku

- /nginx_app.conf - to provide the gubbins to make the Laravel resource routing work correctly on Heroku's nginx server
- /Procfile - to reference the nginx_app.conf file and set /public as webserver root
- /app/config/database.php - addition of lines 3-8, and change of lines 75-78 to support pgsql in both dev and production on heroku via [DATABSE_URL environment variable](https://devcenter.heroku.com/articles/getting-started-with-php#provision-a-database)
- /generators/example.sh - a simple bash script to make it a little easier to type long db migration in the generator scaffold provided by [way/generators](https://github.com/JeffreyWay/Laravel-4-Generators) which is added to require of /composer.json - if added to require-dev, it breaks the build in Heroku, and I don't have time to work out how to make a buildpack to fix this.
- addition of the Heroku buildpack to require-dev in /composer.json for installing in local Homestead environment. I do not know whether this is a good or bad thing; it isn't required; I do not know if it has any affect on making the local deployment more similar to the Heroku deployment, but it doesn't seem to have broken anything thus far...

- /env.local.php with the default homestead pgsql connection details for the local db - NOTE: Although this is now in the repo, this is not included in the .gitignore, as per the Laravel convention to not push .env.*.php files between deployments

Don't forget that if you are using this repo with Homestead to develop a project locally, you will need to add the site to the Homestead.yaml and then re-provision the VM:

```yaml
sites:
    - map: homestead-laravel-heroku-nginx.local
      to: /home/vagrant/projects/homestead-laravel-heroku-nginx/public
```

Note: do not use underscores in the URLs, otherwise this will throw Exceptions in Laravel, as they are not valid with [filter_var($url, FILTER_VALIDATE_URL)](http://forumsarchive.laravel.io/viewtopic.php?pid=19972)

and then:

```bash
> vagrant reload --provision
```

## Laravel PHP Framework

[![Build Status](https://travis-ci.org/laravel/framework.svg)](https://travis-ci.org/laravel/framework)
[![Total Downloads](https://poser.pugx.org/laravel/framework/downloads.svg)](https://packagist.org/packages/laravel/framework)
[![Latest Stable Version](https://poser.pugx.org/laravel/framework/v/stable.svg)](https://packagist.org/packages/laravel/framework)
[![Latest Unstable Version](https://poser.pugx.org/laravel/framework/v/unstable.svg)](https://packagist.org/packages/laravel/framework)
[![License](https://poser.pugx.org/laravel/framework/license.svg)](https://packagist.org/packages/laravel/framework)

Laravel is a web application framework with expressive, elegant syntax. We believe development must be an enjoyable, creative experience to be truly fulfilling. Laravel attempts to take the pain out of development by easing common tasks used in the majority of web projects, such as authentication, routing, sessions, and caching.

Laravel aims to make the development process a pleasing one for the developer without sacrificing application functionality. Happy developers make the best code. To this end, we've attempted to combine the very best of what we have seen in other web frameworks, including frameworks implemented in other languages, such as Ruby on Rails, ASP.NET MVC, and Sinatra.

Laravel is accessible, yet powerful, providing powerful tools needed for large, robust applications. A superb inversion of control container, expressive migration system, and tightly integrated unit testing support give you the tools you need to build any application with which you are tasked.

## Official Documentation

Documentation for the entire framework can be found on the [Laravel website](http://laravel.com/docs).

### Contributing To Laravel

**All issues and pull requests should be filed on the [laravel/framework](http://github.com/laravel/framework) repository.**

### License

The Laravel framework is open-sourced software licensed under the [MIT license](http://opensource.org/licenses/MIT)
