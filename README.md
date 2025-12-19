<h3 align='center'> Redis </h3>

Redis is a super-fast, in-memory data store mainly used to make applications faster, more scalable, and more reliable.

Think of it like this:

Database (PostgreSQL/MySQL) = permanent storage (slower)
Redis = lightning-fast temporary storage (RAM-based)

###Background Jobs & Queues

Redis is often used with task queues.

Examples:

    -Email sending
    -SMS notifications
    -Payment confirmation
    -Image processing
Laravel → Queues + Redis

installs Predis, which is a PHP client library for Redis:

    In simple words:

    Redis = the server
    Predis = PHP code that lets your app talk to Redis

Command:

    composer require predis/predis

<h3 align='center'> Install Redis </h3>

link: https://redis.io/docs/latest/operate/oss_and_stack/install/archive/install-redis/install-redis-on-windows/


Open project in WSL mode 

Install WSL extension

    i) Ctrl + Shift + P

Type:

    ii) WSL: Reopen Folder in WSL
Now your terminal prompt will look like:

    username@DESKTOP:~/laravel_redis$

Now you can run:

    sudo apt update
    sudo apt install redis-server -y
    redis-cli ping

Correct Way to Start / Stop Redis (WSL):

Start:

    sudo service redis-server start
Stop:

    sudo service redis-server stop
Restart:

    sudo service redis-server restart
HOW TO CHECK IF REDIS IS RUNNING:

    redis-cli ping
If you see:

    PONG
➡ Redis is running ✔

<h3 align='center'> Config file settings </h3>

config/database.php: (predis)

    'redis' => [

        'client' => env('REDIS_CLIENT', 'predis'),

        'options' => [
            'cluster' => env('REDIS_CLUSTER', 'redis'),
            'prefix' => env('REDIS_PREFIX', Str::slug((string) env('APP_NAME', 'laravel')).'-database-'),
            'persistent' => env('REDIS_PERSISTENT', false),
        ],

config/app.php:

    'Redis'->Illuminate\Support\Facades\Redis::class,
<h3 align='center'> Making Controller </h3>

    $ php artisan make:controller RedisController
inside controller:

    <?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;
use Illuminate\Support\Facades\Redis;
class RedisController extends Controller:

    {
         public function index(){
        
             Redis::set('user:1:first_name','Mike');
             Redis::set('user:3:first_name','John');
             Redis::set('user:2:first_name','Dop');
            }
        }

indside route:

    Route::get('/redis',[RedisController::class,'index']);

Use Redis for Sessions Instead of MySQL:

    SESSION_DRIVER=redis
    REDIS_HOST=127.0.0.1
    REDIS_PASSWORD=null
    REDIS_PORT=6379
RedisInsight:

<p align='center'><img width="48%"  src="https://github.com/user-attachments/assets/c286993c-461c-46a4-80f4-09a190fcd1c3" />
 </p>


