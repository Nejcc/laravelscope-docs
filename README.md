# Create new Admin route
Inside routes folder make new Admin.php rout file

#### RouteServiceProvider
[https://laravel.com/docs/8.x/routing](Laravel documentation 8.x)

```php
public function boot()
{
    $this->configureRateLimiting();

    $this->routes(function () {
        Route::prefix('api')
            ->middleware('api')
            ->namespace($this->namespace)
            ->group(base_path('routes/api.php'));

        Route::middleware('web')
            ->namespace($this->namespace)
            ->group(base_path('routes/web.php'));

        <span class='green'>//Adding new custom route here</span>

    });
}
```

#### Append new route group

##### Simple route
```php
//Adding new custom route
Route::middleware(['web', 'auth'])
->namespace($this->namespace)
->prefix('admin')
->name('admin.')
->group(base_path('routes/admin.php'));
```


##### Advanced route with Roles
```php
Route::middleware(['web', 'auth', 'role:admin|super-admin'])
->namespace($this->namespace)
->prefix('admin')
->name('admin.')
->group(base_path('routes/admin.php'));
```

##### Create new Admin route
```
touch routes/Admin.php
```

##### Create your first index route name
Create new controller
``` 
php artisan make:controller Admin/DashboardController 
```

##### Add new route to Admin route
```php
Route::get('/', [App\Http\Controllers\Admin\DashboardController::class, 'index'])->name('dashboard'); 
```
