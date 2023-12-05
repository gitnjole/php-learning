#singleton
```php
class Singleton
{
    private static $instance;
    
    private function __construct()
    {
        //inicijalizacija
    }

    public static function getInstance() {
        if (!isset(self::$instance)) {
            self::$instance = new self();
        }
        return self::$instance;
    }
}

$instance1 = Singleton::getInstance();
```
>[!info] Proces:
>Prvo definiramo klasu Singleton
>Drugo definiramo `private static $instance` te privatan konstrukt
>Treće definiramo javnu metodu `getInstance()` koja provjera postoji li već instance putem `self::$instance`
>Četvrto implementiramo da ako ne postoji instanca stvori se nova, a ukoliko već postoji onda se jednostavno vrati korisniku

#factory
```php
// Sučelje koje definira metodu za stvaranje objekta
interface Produkt {
    public function operacija();
}

// Konkretna implementacija sučelja
class KonkretniProdukt implements Produkt {
    public function operacija() {
        return "Operacija konkretnog proizvoda";
    }
}

// Klasa koja sadrži tvorničku metodu
class Tvornica {
    public function stvoriProizvod() {
        return new KonkretniProdukt();
    }
}

// Korištenje Factory uzorka
$tvornica = new Tvornica();
$proizvod = $tvornica->stvoriProizvod();
echo $proizvod->operacija();
```
>[!info] 
>U ovom primjeru, `Tvornica` klasa ima tvorničku metodu `stvoriProizvod()` koja stvara i vraća novi objekt tipa `KonkretniProdukt`. Ovaj pristup omogućuje jednostavnu zamjenu tipa proizvoda bez utjecaja na kod koji koristi tu tvornicu.

#autoloader
```php
function my_autoloader($class_name) {
	include 'Classes/' . $class_name . '.php';
}

//registriranje autoloadera
spl_autoload_register('my_autolodaer');


$student = new Student ('Marko', 'Marulić', '12345');
$student->poloziIspit('Programiranje');
```
>[!info] 
>Vidi PHP Advanced.


# Algebra praktični zadaci

#do-while
```php
$i = 41;
do{
    echo --$i.PHP_EOL;
}while($i > 19);
```

#while
```php
$i = 14;
while($i <= 34) {
    if ($i%2 != 0) echo $i.PHP_EOL;
    $i++;
}
```

#for 
```php
for ($i = 1; $i <= 100; $i++) {
    if (($i == 63) || ($i == 70) || ($i == 90)) continue;
    if (($i % 7 == 0) || ($i % 9 == 0)) echo $i.PHP_EOL;
}
```

#HŽ
```php
class HrvatskeZeljeznice
{
    protected $kasnjenje;
    public function vozi()
    {
        
    }
}
```

```php
$noviVoz = new HrvatskeZeljeznice;
```

# AI generirani zadaci

#objektno-orijentirano-programiranje
```php
class Automobil
{
	protected $model;
	protected $boja;
	protected $godina;

	public function __construct($model, $boja, $godina)
	{
		$this->model = $model;
		$this->boja = $boja;
		$this->godina = $godina;
	}

	public function getInfo()
	{
			echo 'Model: '. $this->model .PHP_EOL.'Boja: '. $this->boja .PHP_EOL.'Godina: '. $this->godina.PHP_EOL;
	}
}


$auto = new Automobil ('CRX', 'bijela', 1999);
$auto->getInfo();
```