# CODE REFERENCE — Student Management System

This file contains the code for the activity. In **STUDENT_GUIDE_REVISED.md**, each coding step tells you which section to open here. Find the matching file path, copy the code inside the block, and paste it into the same file in GitHub Codespaces. Do not copy the heading or the three backticks. Save after pasting.

**Important:** Use the short `devcontainer.json` from Step 3 of the guide first. Replace it with the full version here only after you have created the `scripts` files. Keep the three original Laravel migrations.

## Find the code you need

- `.devcontainer/Dockerfile`
- `.devcontainer/devcontainer.json`
- `composer.json`
- `.env.example`
- `.gitignore`
- `app/Models/Student.php`
- `database/migrations/2026_11_02_000001_create_students_table.php`
- `database/migrations/2026_11_02_000002_protect_server_tables.php`
- `app/Http/Controllers/StudentController.php`
- `routes/web.php`
- `resources/views/layouts/app.blade.php`
- `resources/views/students/index.blade.php`
- `resources/views/students/form.blade.php`
- `resources/views/students/show.blade.php`
- `config/database.php`
- `app/Providers/AppServiceProvider.php`
- `scripts/configure-codespace.php`
- `scripts/setup.sh`
- `scripts/start.sh`
- `scripts/verify-connection.php`
- `phpunit.xml`
- `tests/Feature/ExampleTest.php`
- `tests/Feature/StudentCrudTest.php`
- `.github/workflows/tests.yml`

---

## .devcontainer/Dockerfile

```text
FROM mcr.microsoft.com/devcontainers/php:1-8.3-bookworm
USER root
RUN rm -f /etc/apt/sources.list.d/yarn.list /etc/apt/sources.list.d/yarn.sources \
    && apt-get update && apt-get install -y --no-install-recommends libpq-dev libzip-dev libicu-dev postgresql-client \
    && docker-php-ext-install pdo_pgsql pgsql bcmath intl zip \
    && rm -rf /var/lib/apt/lists/*
COPY --from=composer:2 /usr/bin/composer /usr/local/bin/composer
WORKDIR /workspaces/studManagement
```

## .devcontainer/devcontainer.json

```json
{
  "name": "Student Management · PHP 8.3",
  "build": { "dockerfile": "Dockerfile" },
  "remoteUser": "vscode",
  "forwardPorts": [8000],
  "portsAttributes": { "8000": { "label": "Student Management", "onAutoForward": "notify", "protocol": "http" } },
  "postCreateCommand": "bash scripts/setup.sh",
  "postStartCommand": "bash scripts/start.sh",
  "customizations": { "vscode": { "settings": { "php.validate.executablePath": "/usr/local/bin/php" } } }
}
```

## composer.json

```json
{
    "$schema": "https://getcomposer.org/schema.json",
    "name": "laravel/laravel",
    "type": "project",
    "description": "The skeleton application for the Laravel framework.",
    "keywords": ["laravel", "framework"],
    "license": "MIT",
    "require": {
        "php": "~8.3.0",
        "ext-pdo_pgsql": "*",
        "laravel/framework": "^12.0",
        "laravel/tinker": "^2.10.1"
    },
    "require-dev": {
        "fakerphp/faker": "^1.23",
        "laravel/pail": "^1.2.2",
        "laravel/pint": "^1.13",
        "laravel/sail": "^1.41",
        "mockery/mockery": "^1.6",
        "nunomaduro/collision": "^8.6",
        "phpunit/phpunit": "^11.5.3"
    },
    "autoload": {
        "psr-4": {
            "App\\": "app/",
            "Database\\Factories\\": "database/factories/",
            "Database\\Seeders\\": "database/seeders/"
        }
    },
    "autoload-dev": {
        "psr-4": {
            "Tests\\": "tests/"
        }
    },
    "scripts": {
        "post-autoload-dump": [
            "Illuminate\\Foundation\\ComposerScripts::postAutoloadDump",
            "@php artisan package:discover --ansi"
        ],
        "post-update-cmd": [
            "@php artisan vendor:publish --tag=laravel-assets --ansi --force"
        ],
        "post-root-package-install": [
            "@php -r \"file_exists('.env') || copy('.env.example', '.env');\""
        ],
        "post-create-project-cmd": [
            "@php artisan key:generate --ansi",
            "@php -r \"file_exists('database/database.sqlite') || touch('database/database.sqlite');\"",
            "@php artisan migrate --graceful --ansi"
        ],
        "dev": [
            "Composer\\Config::disableProcessTimeout",
            "npx concurrently -c \"#93c5fd,#c4b5fd,#fb7185,#fdba74\" \"php artisan serve\" \"php artisan queue:listen --tries=1\" \"php artisan pail --timeout=0\" \"npm run dev\" --names=server,queue,logs,vite"
        ]
    },
    "extra": {
        "branch-alias": {
            "dev-master": "12.x-dev"
        },
        "laravel": {
            "dont-discover": []
        }
    },
    "config": {
        "optimize-autoloader": true,
        "preferred-install": "dist",
        "sort-packages": true,
        "allow-plugins": {
            "pestphp/pest-plugin": true,
            "php-http/discovery": true
        }
    },
    "minimum-stability": "dev",
    "prefer-stable": true
}
```

## .env.example

```text
APP_NAME="Student Management"
APP_ENV=local
APP_KEY=
APP_DEBUG=true
APP_URL=http://localhost

APP_LOCALE=en
APP_FALLBACK_LOCALE=en
APP_FAKER_LOCALE=en_US

APP_MAINTENANCE_DRIVER=file
# APP_MAINTENANCE_STORE=database

PHP_CLI_SERVER_WORKERS=4

BCRYPT_ROUNDS=12

LOG_CHANNEL=stack
LOG_STACK=single
LOG_DEPRECATIONS_CHANNEL=null
LOG_LEVEL=debug

DB_CONNECTION=pgsql
DB_HOST=YOUR_SESSION_POOLER_HOST
DB_PORT=5432
DB_DATABASE=postgres
DB_USERNAME=postgres.YOUR_PROJECT_REFERENCE
DB_PASSWORD=

SESSION_DRIVER=file
SESSION_LIFETIME=120
SESSION_ENCRYPT=false
SESSION_PATH=/
SESSION_DOMAIN=null

BROADCAST_CONNECTION=log
FILESYSTEM_DISK=local
QUEUE_CONNECTION=sync

CACHE_STORE=file
# CACHE_PREFIX=

MEMCACHED_HOST=127.0.0.1

REDIS_CLIENT=phpredis
REDIS_HOST=127.0.0.1
REDIS_PASSWORD=null
REDIS_PORT=6379

MAIL_MAILER=log
MAIL_SCHEME=null
MAIL_HOST=127.0.0.1
MAIL_PORT=2525
MAIL_USERNAME=null
MAIL_PASSWORD=null
MAIL_FROM_ADDRESS="hello@example.com"
MAIL_FROM_NAME="${APP_NAME}"

AWS_ACCESS_KEY_ID=
AWS_SECRET_ACCESS_KEY=
AWS_DEFAULT_REGION=us-east-1
AWS_BUCKET=
AWS_USE_PATH_STYLE_ENDPOINT=false

VITE_APP_NAME="${APP_NAME}"

DB_SSLMODE=require
```

## .gitignore

```text
/.phpunit.cache
/node_modules
/public/build
/public/hot
/public/storage
/storage/*.key
/storage/pail
/vendor
/source-bundle.json
.env
.env.backup
.env.production
.phpactor.json
.phpunit.result.cache
Homestead.json
Homestead.yaml
npm-debug.log
yarn-error.log
/auth.json
/.fleet
/.idea
/.nova
/.vscode
/.zed
```

## app/Models/Student.php

```php
<?php
namespace App\Models;
use Illuminate\Database\Eloquent\Model;
class Student extends Model
{
    protected $fillable = [
        'student_number',
        'first_name',
        'last_name',
        'email',
        'course',
        'year_level',
    ];
}
```

## database/migrations/2026_11_02_000001_create_students_table.php

```php
<?php
use Illuminate\Database\Migrations\Migration;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema;
use Illuminate\Support\Facades\DB;
return new class extends Migration {
    public function up(): void {
        Schema::create('students', function (Blueprint $table) {
            $table->id();
            $table->string('student_number',30)->unique();
            $table->string('first_name',100);
            $table->string('last_name',100);
            $table->string('email')->unique();
            $table->string('course',120);
            $table->unsignedSmallInteger('year_level');
            $table->timestamps();
        });
        if (DB::getDriverName() === 'pgsql') {
            DB::statement('ALTER TABLE students ENABLE ROW LEVEL SECURITY');
            DB::statement('ALTER TABLE students ADD CONSTRAINT students_year_check CHECK (year_level BETWEEN 1 AND 6)');
        }
    }
    public function down(): void { Schema::dropIfExists('students'); }
};
```

## database/migrations/2026_11_02_000002_protect_server_tables.php

```php
<?php

use Illuminate\Database\Migrations\Migration;
use Illuminate\Support\Facades\DB;

return new class extends Migration
{
    public function up(): void
    {
        if (DB::getDriverName() !== 'pgsql') {
            return;
        }
        // Laravel accesses these tables through its server-side database role.
        // No anonymous Supabase Data API access is needed.
        foreach (['users', 'password_reset_tokens', 'sessions', 'cache', 'cache_locks', 'jobs', 'job_batches', 'failed_jobs', 'migrations'] as $table) {
            DB::statement('ALTER TABLE "'.$table.'" ENABLE ROW LEVEL SECURITY');
        }
    }

    public function down(): void
    {
        // Keep server tables protected when rolling back application migrations.
    }
};
```

## app/Http/Controllers/StudentController.php

```php
<?php
namespace App\Http\Controllers;
use App\Models\Student;
use Illuminate\Http\Request;
use Illuminate\Validation\Rule;
class StudentController extends Controller
{
    public function index(Request $request) {
        $search = trim((string) $request->query('search',''));
        $students = Student::query()->when($search !== '', function ($query) use ($search) {
            $query->where(function ($query) use ($search) {
                foreach (['student_number','first_name','last_name','email','course'] as $column) {
                    $query->orWhereRaw('LOWER('.$column.') LIKE ?', ['%'.mb_strtolower($search).'%']);
                }
            });
        })->orderBy('last_name')->orderBy('first_name')->paginate(10)->withQueryString();
        return view('students.index', compact('students','search'));
    }
    public function create() { return view('students.form',['student'=>new Student]); }
    public function show(Student $student) { return view('students.show',compact('student')); }
    public function edit(Student $student) { return view('students.form',compact('student')); }
    public function store(Request $request) {
        $student = Student::create($this->validated($request));
        return to_route('students.show',$student)->with('success','Student created successfully.');
    }
    public function update(Request $request, Student $student) {
        $student->update($this->validated($request,$student));
        return to_route('students.show',$student)->with('success','Student updated successfully.');
    }
    public function destroy(Student $student) {
        $student->delete();
        return to_route('students.index')->with('success','Student deleted successfully.');
    }
    private function validated(Request $request, ?Student $student=null): array {
        $request->merge(collect($request->only(['student_number','first_name','last_name','email','course']))->map(fn($v)=>is_string($v)?trim($v):$v)->all());
        return $request->validate([
            'student_number'=>['required','string','max:30',Rule::unique('students')->ignore($student)],
            'first_name'=>['required','string','max:100'],
            'last_name'=>['required','string','max:100'],
            'email'=>['required','email','max:255',Rule::unique('students')->ignore($student)],
            'course'=>['required','string','max:120'],
            'year_level'=>['required','integer','between:1,6'],
        ]);
    }
}
```

## routes/web.php

```php
<?php

use Illuminate\Support\Facades\Route;
use App\Http\Controllers\StudentController;

// Open the student list when visiting the homepage.
Route::redirect('/', '/students');
Route::resource('students', StudentController::class);
```

## resources/views/layouts/app.blade.php

```php
<!doctype html>
<html lang="en"><head><meta charset="utf-8"><meta name="viewport" content="width=device-width, initial-scale=1"><title>@yield('title','Students') · Student Management</title>
<style>
*{box-sizing:border-box}body{margin:0;background:#f3f6fb;color:#18263c;font:16px/1.55 system-ui,sans-serif}header{background:#14294a;color:white;padding:24px 6%}header a{color:white;text-decoration:none;font-weight:750;font-size:22px}header p{margin:4px 0;color:#b9cbe5;font-size:14px}main{max-width:1160px;margin:36px auto;padding:0 24px}.card{background:white;border:1px solid #dfe6ef;border-radius:14px;padding:28px}.toolbar{display:flex;align-items:center;justify-content:space-between;gap:16px;flex-wrap:wrap}h1{margin:0 0 8px;font-size:30px}.muted{color:#62718a}.button,button{display:inline-block;background:#245bd5;color:white;padding:10px 17px;border:0;border-radius:7px;font:inherit;font-weight:600;text-decoration:none;cursor:pointer}.secondary{background:#eaf0fb;color:#244579}.danger{background:#b32c3c}.actions{display:flex;gap:10px;align-items:center;flex-wrap:wrap}a{color:#245bd5}input,select{width:100%;padding:11px;border:1px solid #bbc8da;border-radius:6px;font:inherit;background:white}label{display:block;font-weight:600;margin-bottom:6px}.grid{display:grid;grid-template-columns:1fr 1fr;gap:20px}.field{margin-bottom:18px}.error{color:#a21d32;font-size:14px}.alert{padding:14px 18px;background:#e4f5e9;color:#195c34;border-radius:8px;margin-bottom:22px}.errors{background:#fff0f1;color:#92233b}.table-wrap{overflow-x:auto}table{width:100%;border-collapse:collapse;margin-top:24px}th,td{text-align:left;padding:15px 12px;border-bottom:1px solid #e4eaf3}th{font-size:12px;text-transform:uppercase;color:#62718a}.empty{text-align:center;padding:55px 20px}dl{display:grid;grid-template-columns:160px 1fr;gap:16px}dt{color:#62718a}dd{margin:0;overflow-wrap:anywhere}nav[role=navigation]{margin-top:24px}svg{width:20px;height:20px}@media(max-width:650px){.grid{grid-template-columns:1fr}.card{padding:18px}main{padding:0 12px;margin:20px auto}dl{grid-template-columns:1fr;gap:6px}dd{margin-bottom:12px}}
.search{margin-top:24px;max-width:720px}.search input{flex:1;min-width:180px;width:auto}
</style></head><body><header><a href="{{ route('students.index') }}">Student Management</a><p>Student records · Academic administration</p></header><main>@if(session('success'))<div class="alert" role="status">{{ session('success') }}</div>@endif @yield('content')</main></body></html>
```

## resources/views/students/index.blade.php

```php
@extends('layouts.app')
@section('content')
<section class="card"><div class="toolbar"><div><h1>Students</h1><span class="muted">{{ $students->total() }} {{ Str::plural('record', $students->total()) }}</span></div><a class="button" href="{{ route('students.create') }}">+ Add student</a></div>
<form class="actions search" method="get" action="{{ route('students.index') }}"><input aria-label="Search students" name="search" value="{{ $search }}" placeholder="Search name, number, email or course"><button>Search</button>@if($search)<a href="{{ route('students.index') }}">Clear</a>@endif</form>
<div class="table-wrap"><table><thead><tr><th>Student</th><th>Number</th><th>Course</th><th>Year</th><th>Actions</th></tr></thead><tbody>@forelse($students as $student)<tr><td><strong>{{ $student->first_name }} {{ $student->last_name }}</strong><br><span class="muted">{{ $student->email }}</span></td><td>{{ $student->student_number }}</td><td>{{ $student->course }}</td><td>{{ $student->year_level }}</td><td><div class="actions"><a href="{{ route('students.show',$student) }}">View</a><a href="{{ route('students.edit',$student) }}">Edit</a></div></td></tr>@empty<tr><td colspan="5" class="empty"><h2>{{ $search ? 'No matching students' : 'Your student directory starts here' }}</h2><p class="muted">{{ $search ? 'Try another search.' : 'Add your first student to begin managing records.' }}</p></td></tr>@endforelse</tbody></table></div>{{ $students->links() }}</section>
@endsection
```

## resources/views/students/form.blade.php

```php
@extends('layouts.app')
@section('title',$student->exists ? 'Edit student' : 'Add student')
@section('content')
<section class="card"><h1>{{ $student->exists ? 'Edit student' : 'Add student' }}</h1><p class="muted">All fields are required.</p>@if($errors->any())<div class="alert errors" role="alert">Please correct the highlighted fields.</div>@endif
<form method="post" action="{{ $student->exists ? route('students.update',$student) : route('students.store') }}">@csrf @if($student->exists) @method('PUT') @endif
<div class="grid">@foreach(['student_number'=>'Student number','first_name'=>'First name','last_name'=>'Last name','email'=>'Email','course'=>'Course'] as $field=>$label)<div class="field"><label for="{{ $field }}">{{ $label }}</label><input id="{{ $field }}" name="{{ $field }}" type="{{ $field==='email' ? 'email' : 'text' }}" value="{{ old($field,$student->$field) }}" required maxlength="{{ ['student_number'=>30,'first_name'=>100,'last_name'=>100,'course'=>120,'email'=>255][$field] }}">@error($field)<div class="error">{{ $message }}</div>@enderror</div>@endforeach
<div class="field"><label for="year_level">Year level</label><select id="year_level" name="year_level" required><option value="">Select year</option>@for($year=1;$year<=6;$year++)<option value="{{ $year }}" @selected(old('year_level',$student->year_level)==$year)>Year {{ $year }}</option>@endfor</select>@error('year_level')<div class="error">{{ $message }}</div>@enderror</div></div><div class="actions"><button>Save student</button><a class="button secondary" href="{{ route('students.index') }}">Cancel</a></div></form></section>
@endsection
```

## resources/views/students/show.blade.php

```php
@extends('layouts.app')
@section('title',$student->first_name.' '.$student->last_name)
@section('content')
<section class="card"><div class="toolbar"><h1>{{ $student->first_name }} {{ $student->last_name }}</h1><a class="button" href="{{ route('students.edit',$student) }}">Edit student</a></div><dl>@foreach(['student_number'=>'Student number','email'=>'Email','course'=>'Course','year_level'=>'Year level'] as $field=>$label)<dt>{{ $label }}</dt><dd>{{ $student->$field }}</dd>@endforeach</dl><div class="actions"><a class="button secondary" href="{{ route('students.index') }}">Back to students</a><form method="post" action="{{ route('students.destroy',$student) }}" onsubmit="return confirm('Delete this student record? This cannot be undone.')">@csrf @method('DELETE')<button class="danger">Delete student</button></form></div></section>
@endsection
```

## config/database.php

```php
<?php

use Illuminate\Support\Str;

return [

    /*
    |--------------------------------------------------------------------------
    | Default Database Connection Name
    |--------------------------------------------------------------------------
    |
    | Here you may specify which of the database connections below you wish
    | to use as your default connection for database operations. This is
    | the connection which will be utilized unless another connection
    | is explicitly specified when you execute a query / statement.
    |
    */

    'default' => env('DB_CONNECTION', 'sqlite'),

    /*
    |--------------------------------------------------------------------------
    | Database Connections
    |--------------------------------------------------------------------------
    |
    | Below are all of the database connections defined for your application.
    | An example configuration is provided for each database system which
    | is supported by Laravel. You're free to add / remove connections.
    |
    */

    'connections' => [

        'sqlite' => [
            'driver' => 'sqlite',
            'url' => env('DB_URL'),
            'database' => env('DB_DATABASE', database_path('database.sqlite')),
            'prefix' => '',
            'foreign_key_constraints' => env('DB_FOREIGN_KEYS', true),
            'busy_timeout' => null,
            'journal_mode' => null,
            'synchronous' => null,
        ],

        'mysql' => [
            'driver' => 'mysql',
            'url' => env('DB_URL'),
            'host' => env('DB_HOST', '127.0.0.1'),
            'port' => env('DB_PORT', '3306'),
            'database' => env('DB_DATABASE', 'laravel'),
            'username' => env('DB_USERNAME', 'root'),
            'password' => env('DB_PASSWORD', ''),
            'unix_socket' => env('DB_SOCKET', ''),
            'charset' => env('DB_CHARSET', 'utf8mb4'),
            'collation' => env('DB_COLLATION', 'utf8mb4_unicode_ci'),
            'prefix' => '',
            'prefix_indexes' => true,
            'strict' => true,
            'engine' => null,
            'options' => extension_loaded('pdo_mysql') ? array_filter([
                PDO::MYSQL_ATTR_SSL_CA => env('MYSQL_ATTR_SSL_CA'),
            ]) : [],
        ],

        'mariadb' => [
            'driver' => 'mariadb',
            'url' => env('DB_URL'),
            'host' => env('DB_HOST', '127.0.0.1'),
            'port' => env('DB_PORT', '3306'),
            'database' => env('DB_DATABASE', 'laravel'),
            'username' => env('DB_USERNAME', 'root'),
            'password' => env('DB_PASSWORD', ''),
            'unix_socket' => env('DB_SOCKET', ''),
            'charset' => env('DB_CHARSET', 'utf8mb4'),
            'collation' => env('DB_COLLATION', 'utf8mb4_unicode_ci'),
            'prefix' => '',
            'prefix_indexes' => true,
            'strict' => true,
            'engine' => null,
            'options' => extension_loaded('pdo_mysql') ? array_filter([
                PDO::MYSQL_ATTR_SSL_CA => env('MYSQL_ATTR_SSL_CA'),
            ]) : [],
        ],

        'pgsql' => [
            'driver' => 'pgsql',
            'url' => env('DB_URL'),
            'host' => env('DB_HOST', '127.0.0.1'),
            'port' => env('DB_PORT', '5432'),
            'database' => env('DB_DATABASE', 'laravel'),
            'username' => env('DB_USERNAME', 'root'),
            'password' => env('DB_PASSWORD', ''),
            'charset' => env('DB_CHARSET', 'utf8'),
            'prefix' => '',
            'prefix_indexes' => true,
            'search_path' => 'public',
            'sslmode' => env('DB_SSLMODE', 'require'),
        ],

        'sqlsrv' => [
            'driver' => 'sqlsrv',
            'url' => env('DB_URL'),
            'host' => env('DB_HOST', 'localhost'),
            'port' => env('DB_PORT', '1433'),
            'database' => env('DB_DATABASE', 'laravel'),
            'username' => env('DB_USERNAME', 'root'),
            'password' => env('DB_PASSWORD', ''),
            'charset' => env('DB_CHARSET', 'utf8'),
            'prefix' => '',
            'prefix_indexes' => true,
            // 'encrypt' => env('DB_ENCRYPT', 'yes'),
            // 'trust_server_certificate' => env('DB_TRUST_SERVER_CERTIFICATE', 'false'),
        ],

    ],

    /*
    |--------------------------------------------------------------------------
    | Migration Repository Table
    |--------------------------------------------------------------------------
    |
    | This table keeps track of all the migrations that have already run for
    | your application. Using this information, we can determine which of
    | the migrations on disk haven't actually been run on the database.
    |
    */

    'migrations' => [
        'table' => 'migrations',
        'update_date_on_publish' => true,
    ],

    /*
    |--------------------------------------------------------------------------
    | Redis Databases
    |--------------------------------------------------------------------------
    |
    | Redis is an open source, fast, and advanced key-value store that also
    | provides a richer body of commands than a typical key-value system
    | such as Memcached. You may define your connection settings here.
    |
    */

    'redis' => [

        'client' => env('REDIS_CLIENT', 'phpredis'),

        'options' => [
            'cluster' => env('REDIS_CLUSTER', 'redis'),
            'prefix' => env('REDIS_PREFIX', Str::slug(env('APP_NAME', 'laravel'), '_').'_database_'),
            'persistent' => env('REDIS_PERSISTENT', false),
        ],

        'default' => [
            'url' => env('REDIS_URL'),
            'host' => env('REDIS_HOST', '127.0.0.1'),
            'username' => env('REDIS_USERNAME'),
            'password' => env('REDIS_PASSWORD'),
            'port' => env('REDIS_PORT', '6379'),
            'database' => env('REDIS_DB', '0'),
        ],

        'cache' => [
            'url' => env('REDIS_URL'),
            'host' => env('REDIS_HOST', '127.0.0.1'),
            'username' => env('REDIS_USERNAME'),
            'password' => env('REDIS_PASSWORD'),
            'port' => env('REDIS_PORT', '6379'),
            'database' => env('REDIS_CACHE_DB', '1'),
        ],

    ],

];
```

## app/Providers/AppServiceProvider.php

```php
<?php

namespace App\Providers;

use Illuminate\Support\ServiceProvider;

class AppServiceProvider extends ServiceProvider
{
    /**
     * Register any application services.
     */
    public function register(): void
    {
        //
    }

    /**
     * Bootstrap any application services.
     */
    public function boot(): void
    {
        if (getenv('CODESPACE_NAME')) {
            $domain = getenv('GITHUB_CODESPACES_PORT_FORWARDING_DOMAIN') ?: 'app.github.dev';
            $url = 'https://'.getenv('CODESPACE_NAME').'-8000.'.$domain;
            config(['app.url' => $url]);
        }
        // Artisan serve reloads .env and filters inherited environment variables.
        // The startup script also persists APP_URL so HTTP requests use it.
        $url = config('app.url');
        if (str_starts_with($url, 'https://')) {
            config(['session.secure' => true]);
            \Illuminate\Support\Facades\URL::forceRootUrl($url);
            \Illuminate\Support\Facades\URL::forceScheme('https');
        }
    }
}
```

## scripts/configure-codespace.php

```php
<?php

$name = getenv('CODESPACE_NAME');
if (!$name) {
    exit(0);
}
$domain = getenv('GITHUB_CODESPACES_PORT_FORWARDING_DOMAIN') ?: 'app.github.dev';
$url = 'https://'.$name.'-8000.'.$domain;
$path = __DIR__.'/../.env';
if (!is_file($path)) {
    exit(0);
}
$contents = file_get_contents($path);
$line = 'APP_URL='.$url;
$contents = preg_match('/^APP_URL=/m', $contents)
    ? preg_replace('/^APP_URL=.*$/m', $line, $contents)
    : $contents."\n".$line."\n";
file_put_contents($path, $contents);
echo 'Application URL configured: '.$url.PHP_EOL;
```

## scripts/setup.sh

```bash
#!/usr/bin/env bash
set -euo pipefail
cd "$(dirname "$0")/.."
composer install --no-interaction --prefer-dist
test -f .env || cp .env.example .env
if ! grep -q '^APP_KEY=base64:' .env; then php artisan key:generate --force; fi
php artisan config:clear
php -r 'foreach (["pdo_pgsql","mbstring","xml","curl","zip","intl","bcmath"] as $extension) { if (!extension_loaded($extension)) { fwrite(STDERR, "Missing PHP extension: $extension\n"); exit(1); } }'
bash scripts/start.sh
```

## scripts/start.sh

```bash
#!/usr/bin/env bash
set -euo pipefail
cd "$(dirname "$0")/.."
test -f vendor/autoload.php || exit 0
export XDEBUG_MODE=off
unset PHP_CLI_SERVER_WORKERS
php scripts/configure-codespace.php
php artisan config:clear
if ! php -r '$socket = @fsockopen("127.0.0.1", 8000); if ($socket) { fclose($socket); exit(0); } exit(1);'; then
    # Use Laravel's own development router directly, without an intermediate
    # Artisan process tied to the devcontainer lifecycle shell.
    (cd public && setsid -f php -S 0.0.0.0:8000 ../vendor/laravel/framework/src/Illuminate/Foundation/resources/server.php >../storage/logs/server.log 2>&1 </dev/null)
    echo 'Started Student Management on port 8000.'
else
    echo 'Student Management is already listening on port 8000.'
fi
for attempt in {1..30}; do
    if curl --max-time 2 --silent --fail http://127.0.0.1:8000/up >/dev/null; then
        echo 'Student Management health check passed.'
        exit 0
    fi
    sleep 1
done
tail -20 storage/logs/server.log
echo 'Student Management failed to become ready.' >&2
exit 1
```

## scripts/verify-connection.php

```php
<?php

require __DIR__.'/../vendor/autoload.php';
$app = require __DIR__.'/../bootstrap/app.php';
$app->make(Illuminate\Contracts\Console\Kernel::class)->bootstrap();
$db = config('database.connections.pgsql');
$process = new Symfony\Component\Process\Process(
    ['psql', '--no-psqlrc', '--command=\\conninfo'],
    null,
    ['PGHOST' => $db['host'], 'PGPORT' => (string) $db['port'],
        'PGDATABASE' => $db['database'], 'PGUSER' => $db['username'],
        'PGPASSWORD' => $db['password'], 'PGSSLMODE' => 'require'],
);
$process->setTimeout(30);
$process->run();
echo $process->getOutput();
fwrite(STDERR, $process->getErrorOutput());
exit($process->getExitCode());
```

## phpunit.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<phpunit xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:noNamespaceSchemaLocation="vendor/phpunit/phpunit/phpunit.xsd"
         bootstrap="vendor/autoload.php"
         colors="true"
>
    <testsuites>
        <testsuite name="Unit">
            <directory>tests/Unit</directory>
        </testsuite>
        <testsuite name="Feature">
            <directory>tests/Feature</directory>
        </testsuite>
    </testsuites>
    <source>
        <include>
            <directory>app</directory>
        </include>
    </source>
    <php>
        <env name="APP_ENV" value="testing"/>
        <env name="APP_MAINTENANCE_DRIVER" value="file"/>
        <env name="BCRYPT_ROUNDS" value="4"/>
        <env name="CACHE_STORE" value="array"/>
        <env name="DB_CONNECTION" value="sqlite" force="true"/>
        <env name="DB_DATABASE" value=":memory:" force="true"/>
        <env name="MAIL_MAILER" value="array"/>
        <env name="PULSE_ENABLED" value="false"/>
        <env name="QUEUE_CONNECTION" value="sync"/>
        <env name="SESSION_DRIVER" value="array"/>
        <env name="TELESCOPE_ENABLED" value="false"/>
    </php>
</phpunit>
```

## tests/Feature/ExampleTest.php

```php
<?php

namespace Tests\Feature;

// use Illuminate\Foundation\Testing\RefreshDatabase;
use Tests\TestCase;

class ExampleTest extends TestCase
{
    /**
     * A basic test example.
     */
    public function test_the_application_returns_a_successful_response(): void
    {
        $response = $this->get('/');

        $response->assertRedirect('/students');
    }
}
```

## tests/Feature/StudentCrudTest.php

```php
<?php
namespace Tests\Feature;
use App\Models\Student;
use Illuminate\Foundation\Testing\RefreshDatabase;
use Tests\TestCase;
class StudentCrudTest extends TestCase
{
    use RefreshDatabase;
    private function data(): array {
        return ['student_number'=>'TEST-001','first_name'=>'Test','last_name'=>'Student','email'=>'test@example.test','course'=>'Computer Science','year_level'=>2];
    }
    public function test_complete_student_lifecycle(): void {
        $this->get('/')->assertRedirect('/students');
        $this->get('/students')->assertOk()->assertSee('Your student directory starts here');
        $this->get('/students/create')->assertOk();
        $this->post('/students',$this->data())->assertSessionHasNoErrors();
        $student = Student::sole();
        $this->assertDatabaseHas('students',$this->data());
        $this->get('/students/'.$student->id)->assertOk()->assertSee('TEST-001');
        $this->get('/students/'.$student->id.'/edit')->assertOk();
        $this->put('/students/'.$student->id,array_replace($this->data(),['course'=>'Information Technology']))->assertRedirect(route('students.show',$student));
        $this->assertDatabaseHas('students',['id'=>$student->id,'course'=>'Information Technology']);
        $this->get('/students?search=information')->assertOk()->assertSee('TEST-001');
        $this->get('/students?search=missing')->assertOk()->assertDontSee('TEST-001');
        $this->delete('/students/'.$student->id)->assertRedirect(route('students.index'));
        $this->assertDatabaseMissing('students',['id'=>$student->id]);
        $this->get('/students/'.$student->id)->assertNotFound();
    }
    public function test_validation_and_unique_fields(): void {
        $this->post('/students',[])->assertSessionHasErrors(['student_number','first_name','last_name','email','course','year_level']);
        Student::create($this->data());
        $this->post('/students',$this->data())->assertSessionHasErrors(['student_number','email']);
        $this->post('/students',array_replace($this->data(),['student_number'=>'TEST-002','email'=>'bad','year_level'=>7]))->assertSessionHasErrors(['email','year_level']);
        $student = Student::sole();
        $this->put('/students/'.$student->id,$this->data())->assertSessionHasNoErrors();
        $this->assertDatabaseCount('students',1);
    }
    public function test_blade_escapes_user_content(): void {
        $student = Student::create(array_replace($this->data(),['first_name'=>'<script>alert(1)</script>']));
        $this->get('/students/'.$student->id)->assertOk()->assertDontSee('<script>alert(1)</script>',false)->assertSee('&lt;script&gt;',false);
    }
}
```

## .github/workflows/tests.yml

```yaml
name: Tests
on: [push, pull_request]
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: shivammathur/setup-php@v2
        with:
          php-version: '8.3'
          extensions: pdo_pgsql, pdo_sqlite, mbstring, intl, bcmath, zip
          coverage: none
      - run: composer install --no-interaction --prefer-dist
      - run: cp .env.example .env && php artisan key:generate
      - run: php artisan test
```
