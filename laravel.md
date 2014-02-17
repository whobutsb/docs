#Laravel 

Alias has been written for `php artisan` as `art`

##Commands
[Laravel Command Docs](http://laravel.com/docs/commands)

__To create a new command__ 
- `art command:make CommandName`
- Commands are written to the `app/commands` directory. 
- Then register the command in: `app/start/artisan.php`. 
- `Artisan::add(new CommandName);`


##CLI Interaction 
    $ art tinker

    