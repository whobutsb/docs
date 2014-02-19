#Laravel 

Alias has been written for `php artisan` as `art`

##Links
[Laravel Cheat Sheet](http://cheats.jesse-obrien.ca/)', '

##Commands
[Laravel Command Docs](http://laravel.com/docs/commands)

__To create a new command__ 
- `art command:make CommandName`
- Commands are written to the `app/commands` directory. 
- Then register the command in: `app/start/artisan.php`. 
- `Artisan::add(new CommandName);`

__To Dump The Auto Classes__

    art dump-autoload

##CLI Interaction 
    $ art tinker

- `art routes` Gives all the routes in the application.


Get help on a function

    art help controller:make



##Routes 

Handing get variables

    Route::get('user/{username}', function($username){
        $user = User::whereUsername($username)->first(); 
        //select * from users where username = $username limit 1; 

        return View::make('users.show', ['user' => $username]); 
        //users.show == users/show == app/view/users/show
    }); 

Simple Get Route

    Route::get('users', 'UsersController@index'); 

Route with a variable 
    
    Route::get('users/show/{id}', UsersController@show); 

__Named Routes__, can be used to reference where to go. 
    
    Route::get('user/profile', array('as' => 'profile', 'uses' => 'UserController@showProfile'));

Later on in the application, can be referenceds.

    $url = URL::route('profile'); //http://localhost/user/profile
    $redirect = Redirect::route('profile'); //Redirects the page to the route. 


__Resource URLs__
Creates all of the possible HTTP Verbs for the UserController. Use `art routes` to see the output. Used for RESTful style of development.
    
    Route::resource('users', 'UsersController'); 

Excluding Routes
    
    Route::resource('users', 'UsersController', ['except' => ['create', 'store', 'update']]); 

Specifying Routes
    
    Route::resource('users', 'UsersController', ['only' => ['create', 'show']]); 

Specifying Route Names
Route::resource('users', 'UsersController', ['names' => ['create' => 'user.build']]); 

##Controllers

Simple Controller with variable

    public function show($id){
        $user = User::find($id); 
        return View::make('users.show', ['user' => $user]); 
    }


###Input

Get the all input POST or GET variables

    Input::all();

Get a specific input

    Input::get('field'); 

###Validation

Setup the validation and the rules

    $validation = Validatior::make(Input::all(), ['username' => 'required', 'password' => 'required']); 

Check the validation and reutrn to the previous controller with the input and with the errors.

    if($validation->fails()){
        return Redirect::back()->withInput()->withErrors($validation->messages()); // $validation->messages() could be whatever
    }


##Models

Stop Laravel from expecting timestamps in the model with `public $timestamps = false;`

`protected $fillable = array(columns, in database'); ` Fields that can be mass assigned in the database. 

`protected $guarded = array(columns, in, database`  Fields that should be guarded from mass assignment. 

To Output just the data of a class for easy viewing: 
    
    $user = User::find(1); 
    dd($user->toArray()); 

###DB Class

    $users = DB::table('users')->where('username', '!=', 'Steve')->get(); 
    $users = DB::select('select * from users where username != "Steve"''); 
    //select * from users where username != 'Steve'

###Eloquent

__Select__
    
    $users = User::where('username', '!=', 'Steve')->get(); 
    //select * from users where username != 'Steve'

    $users = $User::all()
    //select * from users; 

    $user = $User::find(10); 
    //select * from users where id = 10; 

    //select * from users orderby username asc; 
    $users = User::orderBy('username', 'asc')->get(); 

    //select * from users orderby username asc limit 2; 
    $users = User::orderBy('useranme', 'asc')->take(2)->get(); 

    //Select * from posts where id != 1 and id != 2; 
    return Post::where(function($query){
        $query->where('id', '!=', 1); 
        $query->where('id', '!=', 2); 
    }); 

    //select DATE(created_at) as day, count(*) as post_count from posts group by day order_by day asc;
    return Post::groupBy('day')->get([
        DB::raw('DATE(created_at) as day'), 
        DB::raw('count(*) as post_count')
    ]); 

__Create__
    
    $user = new User; 
    $user->username = 'Steve'; 
    $user->password = Hash::make('password'); 
    $user->save(); 

    User::create([
        'username' => 'Steve', 
        'password' => Hash::make('password')
    ]);

__Update__
    
    $user = User::find(2); 
    $user->username = 'Bob'; 
    $user->save(); 

__Delete__
    
    $user = User::find(2); 
    $user->delete(); 

__Count__
    
    $User::count(); 



##Views

Passing in view data within the controller or router

    $users = User::all(); 
    return View::make('users/index', ['users => $users']); 


###Forms

Specifying a Route Name or Controller Method

    echo Form::open(['route' => 'route.name']); 
    echo Form::open(['action' => 'Controller@method']); 

Adding in Parameters

    echo Form::open(['route' => ['route.name', $user->id]]); 



Form 

###Blade

###Helper Functions 

- `link_to('controller/method', 'Text Link')` - <a href="controller/method">Text Link</a>
- `dd` dump and die. 









