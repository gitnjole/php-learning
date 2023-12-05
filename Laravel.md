# Laravel

Open source PHP framework

Podržava PostgreSQL, SQLite i MySQL baze
## prednosti
	1. Snažan sustav za rutiranje
	2. Ugrađena autentikacija
	3. Eloquent ORM
	4. Blade templating engine
	5. Velika zajednica

## novi Laravel projekt

### instaliramo PHP i Composer
```bash
sudo apt install php

sudo php composer-setup.php
```

### instaliramo Laravel putem Composer-a
```bash
composer create-project laravel/laravel ime-projekta
```

### konfiguriramo bazu podataka
	Laravel dolazi s predloškom datoteke .env koja sadrži postavke baze podataka
Ako planiramo koristiti bazu podataka potrebno je pokrenuti migracije
```bash
php artisan migrate
```

### kreiramo modele, kontrolere i rute
Izradimo web aplikaciju

## artisan naredbe

#### pokretanje ugrađenog web servera
```bash
php artisan serve
```
	default http://localhost:8000/
#### stvaranje novog modela
```bash
php artisan make:model naziv-modela
```
	ova naredba stvara novi model u direktoriju app/Models
#### stvaranje novog kontrolera
```bash
php artisan make:controller naziv-kontrolera
```
	ova naredba stvara novi kontroler u direktoriju app/Http/Controllers
#### migracija baze podataka
```bash
php artisan make:migration naziv-migracije
```
	ova naredba stvara novu migraciju u direktoriju database/migrations

#### pokretanje migracija
```bash
php aritsan migrate
```

#### pokretanje Tinkera
```bash
php artisan tinker
```
	Tinker je interaktivno sučelje za rad s aplikacijom; Omogućuje testiranje naredbi i funkcionalnosti

#### popis svih ruta u aplikaciji
```bash
php artisan route:list
```

#### dodavanje novog middlewarea
```bash
php artisan make:middleware naziv-middlewarea
```
	ova naredba stvara novi middleware u direktoriju app/Htpp/Middleware
	Middleware se koristi za dodavanje funkcionalnosti na zahtjev

## middleware
	izvršni sloj koji se nalazi između zahtjeva i odgovora

Kada klijent šalje zahtjev (request on prvo prolazi kroz middleware koji ga obrađuje, a nakon toga se generira odgovor.

Middleware se koristi za filtriranje, autorizaciju, manipulaciju zahtjeva itd...
Middleware se može dodijeliti pojedinačnim rutama ili grupama ruta, a može se također primijeniti globlano na sve rute u aplikaciji.

### često korišteni middleware

#### Authenticate
```php
Auth::login()
```
	provjera autentičnosti korisnika

#### ThrottleRequests
	koristi se za ograničavanje broja zahtjeva po vremenskom periodu

#### VerifyCsrfToken
	koristi se za provjeru CSRF tokena

#### EncryptCookies
	koristi se za enkripciju kolačića

#### Cors
	koristi se za omogućavanje Cross-Origin Resource Sharing-a (CORS)

#### Cache
	koristi se za spremanje izračunatih vrijednosti u predmemoriju kako bi se smanjilo vrijeme odaziva aplikacije

## rute
	mehanizam za mapiranje URL adresa na odgovarajuće kontrolere i metode

```php
redirect()
```
	metoda za preusmjeravanje korisnika na drugi URL u Laravel kontroleru

```php
{param}
```
	metoda za definiranje parametra rute

```phjp
Route::prefix()

Route::middleware()

Route::group()
```
	metode za grupiranje ruta

Definiraju se u datoteci `routes/web.php` za rute web aplikacije i u datoteci `routes/api.php` za API rute.

### primjer GET rute 

```php
Route::prefix('api')
	->middleware('auth')->name('algebra')
	->group(function () {
		Route::get('/algebra', 'AlgebraController@index')
			->with('studentID', 1234)
			->name('index');
	});
```
>[!info] Ova ruta će omogućiti pristup metodi `index` u `AlgebraController`-u preko URL adrese `/api/algebra`, a imenovana je `algebra.index`.
>
>Varijabla `studentID` će biti poslana s vrijednosti `1234`, također middleware `auth` osigurava da samo autentificirani korisnici mogu pristupiti ovoj ruti.

> [!example]- Detaljan opis rute
> Ukratko, ovaj kod definira grupu ruta s prefiksom 'api', primjenjuje 'auth' middleware, dodjeljuje naziv 'algebra' grupi te specificira jednu rutu unutar grupe s URI-em '/algebra' koja se mapira na 'index' metodu 'AlgebraController'-a.
> 
> `Route::prefix('api')` postavlja prefiks za sve rute unutar grupe, u osvom slučaju prefiks je `api` tako da će sve rute unutar ove grupe imati URL koji počinje s `/api`
> 
> `->middleware('auth')` primjenjuje `auth` middleware na sve rute unutar grupe
> 
> `->name('algebra')` dodjeljuje naziv cijeloj grupi ruta, u ovom slučaju naziva se `algebra`
> 
> `->group(function () {...})` definira grupu ruta koje dijele određene atribute, poput prefiksa, middleware-a i naziva
> 
> `Route::get('/algebra', 'AlgebraController@index')` definira specifičnu rutu unutar grupe. Ovo je HTTP GET ruta s URI-em `/algebra`. Kada se pristupi ovoj ruti pozvat će se metoda `index` u `AlgebraController`u
> 
> `->with('studentID', 1234` u ovom kontektsu nema izravnog utjecaja na rutu jer se metoda `with` obično koristi za slanje podataka pogledima, a ne rutama
> 
> `->name('index')` dodjeluje naziv specifičnoj ruti, naziv `index` je različit od naziva grupe


## migracije

Migracija sadrži upute za promjene u bazi podataka

Primjer migracije za stvaranje `users` tablice
```php
use Illuminate\Database\Migrations\Migration;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema

class CreateUsersTable extends Migration
{
	public function up()
	{
		Schema::create('users', function (Blueprint table) {
			$table->id();
			$table->string('name');
			$table->string('email')->unique();
			$table->string('password');
			$table->timestamps();
		});
	}

	public function down()
	{
		Schema::dropIfexists('users');
	}
}
```
> [!info] Ova migracija se može izvršiti pokretanjem `php artisan migrate`


Ukoliko je potrebno, migracije se mogu poništiti pomoću naredbe
```bash
php artisan migrate::rollback
```

>[!info] Migracije se također mogu stvoriti pomoću naredbe `php artisan make:migration` (vidi Artisan naredbe) 

## Seederi

Laravel Seeder je mehanizam koji omogućava ispunjavanje baze podataka s početnim podacima.

Za pokretanje određenog seedera koristimo
```bash
php artisan db:seed --class=seeder-name
```

Primjer korištenja Seedera
```php
use Illuminate\Database\Seeder;
use App\Models\User;

class UserSeeder extends Seeder
{
	public function run()
	{
		User::insert([
			['name' => 'Sopranos',
			 'email' => 'tony@example.com',
			 'password' => bcrypt('password')],
			 
			['name' => 'Janica',
			 'email' => 'janica@example.com',
			 'password' => bcrypt('password')],		
		]);
	}
}
```


## Model

Konvencija dizajna softvera koja predstavlja tablicu u bazi podataka. Modeli se koriste za izvršavanje operacija na bazi podataka, kao što su čitanje, stvaranje, ažuriranje i brisanje podataka.

```php
use Illuminate\Database\Eloquent\Model;

class User extends Model
{
	protected $fillable = ['name', 'email', 'password'];
}
```
	samo polja name, email i password mogu se popuniti masovno
	sva ostala polja kao što su ID i join_date bit će ignorirana

## Relacije modela

U Laravelu, relacije se koriste za povezivanje različitih modela i omogućavanje izvođenja složenih upita koji uključuju podatke iz više modela.

### belongsTo
```php
public function author()
{
	return $this->belongsTo('App\Author');
}
```
	koristi se kada jedan model pripada drugom modelu

### hasOne
```php
public function profile()
{
	return $this->hasOne('App\Profile');
}
```
	koristi se kada jedan model ima samo jedan povezani model

### hasMany
```php
public function posts()
{
	return $this->hasMany('App\Post');
}
```
	koristi se kada jedan modle ima više povezanih modela

### belongsToMany
```php
public function roles()
{
	return $this->belongsToMany('App\Role');
}
```
	koristi se kada jedan model može imati više povezanih modela i obrnuto

### hasManyThrough
```php
public function posts ()
{
	return $this->hasManyThrough('App\Post', 'App\User');
}
```
	koristi se kada imamo tri modela i želimo dohvatiti podatke iz trećeg modela preko prvog i drugog modela

## Eloquent 
	Eloquent ORM (Object Relational Mapping)
Omogućava programerima da rade s bazama podataka koristeći objekte i metode umjesto SQL upita.


>[!important] metode poput `find(), delete(), where()` su uključene s Eloquent tako da ih ne trebamo sami stvarati
>
### dohvaćanje
```php
$users = User::all();

$user = User::find(1);

$activeUsers = User::where('status', 'active')->get();
```
>[!info]- ::find()
>primarno dizajniran za pretraživanje po primarnim ključevima, stoga je dovoljno samo unesti ID korisnika kojeg tražimo.

### stvaranje
```php
$newUser = new User();
$newUser->name = "John Doe";
$newUser->email = 'johndoe@gmail.com';
$newUser->password = bcrypt('secret');
$newUser->save();
```
>[!info]- save()
>zadržava promjene napravljene na instanci modela u odgovarajuću tablicu baze podataka

### ažuriranje
```php
$userToUpdate = User::find(1);

$userToUpdate->name = "New Name";
$userTopUpdate->save();
```

### brisanje
```php
$userToDelete = User::find(1);

$userToDelete->delete();
```


## DB

Predstavlja centralnu pristupnu točku za interkaciju s bazom podataka.
Ova klasa omogućuje izvršavanje SQL upita nad bazom podataka bez potrebe za korištenjem modela ili Eloquent ORM-a.

### selekcija
```php
$students = DB::table('student')->get();

/*
foreach ($students as $student)
{
	echo $student->ime;
}
*/

//Selekcija samo imena i prezimena
$students = DB::table('student')->select('ime', 'prezime')->get();

//Selekcija studenata koji pohađaju smjer "Programiranje" ascending
$students = DB::table('student')
	->where('smjer', 'Programiranje')
	->orderBy('ime', 'asc')
	->get();
```
	koristimo get metodu za izvršavanje upita i dohvat svih podataka iz baze podataka

### ubacivanje
```php
DB::table('studenti')->insert([
	'ime' => 'Marko',
	'prezime' => 'Marulić',
	'JMBAG' => 12345
]);
```

### ažuriranje
```php
DB::table('studenti')
	->where('JMBAG', 12345)
	->update(['ime' => 'Tony Soprano']);
```

### brisanje
```php
DB::table('studenti')->where('JMBAG', 12345)->delete();
```

# Laravel testiranje

Za Laravel testiranje pogledaj [[Testiranje]]