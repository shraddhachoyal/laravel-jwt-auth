<h3>Step 1: Create a New Laravel 13 Project</h3>
composer create-project laravel/laravel laravel-jwt-auth

<b>Move into the project:</b>

cd laravel-jwt-auth

<h3>Step 2: Install JWT Package</h3>
<b></Install JWT api package: <b>
php artisan install:api

<b>Install JWT Auth:</b>
composer require tymon/jwt-auth

<b>Publish the package configuration:</b>

php artisan vendor:
publish --provider="Tymon\JWTAuth\Providers\LaravelServiceProvider"

<b>Generate the JWT secret key:</b>

php artisan jwt:secret

<b>This adds a key to your .env file:</b>

JWT_SECRET=your_generated_secret_key

<h3>Step 3: Configure Authentication Guard</h3>

Update guards in config/auth.php:

'guards' => [
    'api' => [
        'driver' => 'jwt',
        'provider' => 'users',
    ],
],

<h3>Step 4: Configure User Model</h3>

Open app/Models/User.php Modify:

use Illuminate\Foundation\Auth\User as Authenticatable;

use Tymon\JWTAuth\Contracts\JWTSubject;

class User extends Authenticatable implements JWTSubject<br/>
{<br/>
    public function getJWTIdentifier()
    {<br/>
        return $this->getKey();<br/>
    }

    public function getJWTCustomClaims()
    {
        return [];
    }
}

<h3>Step 5: Configure Database</h3>

Run migrations:
php artisan migrate

<h3>Step 6: Create Auth Controller</h3>

Create controller:
php artisan make:controller AuthController

Make your apis named register, login, profile, refresh, respondWithToken in AuthController    

<h3>Step 7: Add API Routes</h3>
