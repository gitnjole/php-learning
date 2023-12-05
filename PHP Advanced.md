# Objektno orijentirano programiranje

Pristup programiranju koji se temelji na objektima i njihovim međusobnim interakcijama.
Objekti su instance klasa u PHP-u.

OOP koristi koncepte apstrakcije, enkapsulacije, nasljeđivanja i polimorfizma.
>[!info]- Apstrakcija
>proces sakrivanja složenosti i prikazivanja samo bitnih karakteristika sustava

>[!info]- Enkapsulacija
>odnosi se na omatanje podataka (atributa) i metoda koji rade s tim podacima u jednu cjelinu, tj. klasu

>[!info]-  Nasljeđivanje
>omogućava stvaranje novih klasa temeljenih na već postojećim klasama. Novonastale klase nasljeđuju atribute i metode roditeljske klase

>[!info]- Polimorfizam
>omogućava korištenje istog imena metode ili funkcije na različite načine, ovisno o kontekstu

## Klase
	definiraju svojstva (varijable) i metode (funkcije), a objekti su njihove konkretne implementacije.
```php
class Product
{
	public $name;
	protected $price;

	public function __construct($name, $price) {
		$this->name = $name;
		$this->price = $price;
	}

	public function getPrice () {
		return $this->price;
	}

}


class Appliances extends Product
{
	//code specific for appliances
}

class Condiments extends Product
{
	//code specific for condiments
}
```

### Nasljeđivanje klase

```php
class ParentClass 
{ 
	public static function someMethod() { 
		echo "Parent class method."; 
	} 
} 

class ChildClass extends ParentClass 
{ 
	public static function someMethod() { 
		parent::someMethod(); echo "Child class method."; 
	} 
} 

// Calling the overridden method in the child class 
ChildClass::someMethod();
```
>[!warning]+ Nasljeđivanje
>Klasa ne može naslijediti više podklasa, ali klasa može implementirati više sučelja, što omogućava višestruko nasljeđivanje funkcionalnosti.

### Vidljivost

Možemo postaviti tri razine vidljivosti:
	`public` gdje možemo pristupiti varijablama/metodama bilo gdje iz programa
	`protected` gdje možemo pristupiti varijablama/metodama samo iz parent klase i bilo koje klase koja nasljđuje `protected` člana
	`private` gdje možemo pristupiti varijablama/metodama samo unutar klase gdje je `private` deklariran

### Metode

#### Apstraktna metoda
	metoda koja nema tijelo (implementaciju) u samoj klasi, već se ostavlja za implementaciju u izvedenim klasama
```php
abstract class Oblik
{
	abstract public function izracunajPovrsinu();
}

class Pravokutnik extends Oblik
{
	private $duzina;
	private $sirina;

	public function izracunajPovrsinu() {
		return $this->duzina * $this->povrsina
	}
}
```

#### Statična metoda
	metoda koja pripada klasi, a ne instanci objekta. Za razliku od običnih (instance) metoda, statične metode mogu se pozvati izravno putem imena klase, bez potrebe za stvaranjem instance objekta
```php
class Operacije
{
	public static function zbroj($broj1, $broj2) {
		return $broj1 + $broj2;
	}
}

echo Operacije::zbroji(5,3);
```
>[!important] Kada zovemo statične metode koristimo Klasa::imeMetode
>

## Objekti
	instance klasa koje mogu imati svojstva i metode.

Kreiraju se korištenjem riječi `new` nakon koje slijedi naziv klase.
Svojstvima pristupamo korištenjem operatora `->` iza kojeg slijeda naziv svojstva.
```php
$newProduct = new Product('Towel', 32);
echo $newProduct->getPrice();
```

## Apstraktne klase
	nacrt za ostale klase koje ju nasljeđuju
```php
abstract class PrijevoznoSredstvo 
{
	abstract public function vrijemeDolaksa();
}

class HrvatskeZeljeznice extends PrijevoznoSredstvo {
	public function vrijemeDolaksa() {
		return date();
	}
}


$putovanje = new HrvatskeZeljeznice();
echo "Vrijeme dolaska vlaka: " . $putovanje->vrijemeDolaska();
```

## Interface
	apstraktni nacrt za grupu metoda koje klasa mora implementirati
```php
interface Radnik {
	public function radi();
	public function odmara();
}


class Zaposlenik implements Radnik 
{
	public function radi() {
		echo "Zaposlenik radi.";
	}

	public function odmara() {
		echo "Zaposlenik odmara.";
	}
}
```


## Autoloader (cont.)

```php
function my_autoloader($class_name) {
	include 'Classes/' . $class_name . '.php';
}

//registriranje autoloadera
spl_autoload_register('my_autolodaer');


$student = new Student ('Marko', 'Marulić', '12345');
$student->poloziIspit('Programiranje');
```
	'$class_name' - ime klase koja će biti automatski učitana
	'Classes/' - folder u kojem se nalaze klase, često nazivan i Core

	'spl_autoload_register' registrira funkciju kao autoloader
S obzirom da na početku koda nismo naglasili da koristimo klasu Student, kada pozovemo klasu putem `new Student` ili neku njenu metodu poput `poloziIspit()` PHP će automatski iskoristiti našu autoloader funkciju `my_autoloader` da pokuša pronaći klasu Student u putanji Classes/Student.php .


## Try-catch
	omogućuje rukovanje iznimkama koje se javljaju tijekom izvođenja koda

Try blok sadrži kod koji treba biti izvršen, a catch blok hvata iznimke koje su izbačene tijekom izvođenja koda unutar try bloka.
 ```php
class FileReader {
    private $filePath;

    public function __construct($filePath) {
        $this->filePath = $filePath;
    }

    public function readFileContents() {
        try {
            // Attempt to read the contents of the file
            $contents = file_get_contents($this->filePath);

            // Check for read errors
            if ($contents === false) {
                throw new Exception("Error reading file: " . error_get_last(                            ['message']);
            }

            echo "File contents: $contents\n";
        } catch (Exception $e) {
            // Handle any exceptions that occurred during file reading
            echo "File reading error: " . $e->getMessage() . "\n";
        }
    }
}

// Example usage:
$fileReader = new FileReader('example.txt');

// Attempt to read the file contents
$fileReader->readFileContents();

```


## MySQLi
>[!warning] MySQLi se koristi za proceduralne svrhe te ako je baza vrsta MySQL, dok PDO koristimo kako bi mogli raditi s više vrsta baza.

Omogućuje komunikaciju s bazama podataka.

Za povezivanje koristimo funkciju `mysqli_connect()`.
```php
$dbc = mysqli_connect('hostname', 'username', 'password', 'dbname');
```
	mysqli_connect vraća MySQLi objekt veze s bazom podataka

Nakon uspješne konekcije možemo izvršavati upite uz pomoć postojećih funkcija poput:
`mysqli_query()` - izvršava SQL upite
```php
$result = mysqli_query($dbc, "SELECT * FROM studenti");
```
`mysqli_fetch_assoc()` - vraća samo jedan redak rezultata iz baze
```php
while ($row = mysqli_fetch_assoc($result)) {
	echo "Name: ". $row['name'] .", Age: ". $row['age'].PHP_EOL;
}
```
	uzima $result upita kao parametar
	vraća asocijativan niz čiji su ključevi imena stupaca, a vrijednosti su vrijednosti tih stupaca
	
`mysqli_fetch_array()` - vraća jedan redak iz baze podataka kao niz
```php
while ($row = mysqli_fetch_array($result, MYSQLI_ASSOC)) { 
	echo "Name: " . $row['name'] . ", Age: " . $row['age']; 
}
```
	uzima dva parametra:
		$result kao parametar
		$resulttype kao opcionalni parametar gdje se naglašava kakav niz biva vraćen (npr 'MYSQLI_ASSOC', 'MYSQLI_NUM', 'MYSQLI_BOTH')

Za provjeru grešaka (npr. da provjerimo je li konekcija bila uspješna) koristimo `mysqli_connect_error`.
```php
if (!$dbc) {
	echo "Connection failed: ". mysqli_connect_error();
}
else {
	echo "Connection successful!";
}
```

Kada smo gotovi zatvaramo vezu s `mysqli_close()`.
```php
mysqli_close($dbc);
```


## PDO 
	PHP data objects

Ekstenzija koja omogućuje povezivanje na različite vrste baza uključujući Oracle, PostgreSQL itd...
Nudi konzistentno sučelje za rad

>[!info]- Glavna prednost PDO
>može se upotrijebiti built-in prepared statement mehanizam za izbjegavanje SQL injection napada ; `prepare()` i `execute()`

>[!info] PDO veze se automatski zatvaraju kada skripta završi.

```php
$dsn = "mysql:host=$host;dbname=$dbname;charset=$charset";

try {
	$pdo = new PDO($dsn, $username, $password);
	$pdo->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);	
} catch (PDOException $e) {
	echo "Neuspješno spajanje na bazu: ". $e->getMessage();
	exit();
}
```


## Singleton
	design pattern
	osigurava da postoji samo jedna instanca određene klase u cijeloj aplikaciji
	sastoji se od jedne klase koja ima statičku metodu za vraćanje jedine instance klase
	stvara novu instancu klase ako još nije postojala, a vraća postojeću instancu

```php
class Singleton
{
	private static $instance;
	private function __construct() {
		
	}

	public static function getInstance() {
		if (!isset(self::$instance)) {
			self::$instance = new self();
		}
		return self::$intance;
	}

	public function showMessage() {
		echo "Hello from Singleton!";
	}
}


$singletonInstance1 = Singleton::getInstance();
$singletonInstance1->showMessage();

$singletonInstance2 = Singleton::getInstance
```
	privatan konstruktor spriječava stvaranje više instanci
	kada pozovemo metodu getInstance, koja jedina može započeti instancu, Singleton prvo provjerava je li postavljena instanca, ako nije kreira novu pomoću new, ako već postoji vraća ju

## Factory
	design pattern
	koristi se za kreiranje objekata bez eksplicitnog navođenja njihove klase

Koristimo factory pattern kada: 
	- Koristimo više implementacija istog sučelja, a ne želimo da korisnik mora izravno instancirati objekte
	-Želimo da se klijentski kod bavi samo sučeljem, a ne pojedinim implementacijama

```php
interface Animal
{
	public function makeSound();
}

class Dog implements Animal
{
	public function makeSound() {
		echo "Vau vau";#(?)
	}
}

class Cat implements Animal {
	public function makeSound() {
		echo "Mijau mijau";
	}
}

class Mouse implements Animal {
	public function makeSound() {
		echo "Cvrc cvrc";
	}

}
```

Kreiramo factory klasu koja će stvoriti životinje an temelju proslijeđenog tipa
```php
class AnimalFactory 
{
	public static function createAnimal ($type) {
		switch ($type) {
			case 'dog':
				return new Dog();
				break;
			case 'cat':
				return new Cat();
				break;
			case 'mouse'
				return new Mouse();
				break;
			default:
				throw new Exception("Unsupported animal type.");
		}
	}
}
```

Korištenje factory predloška
```php
$dog = AnimalFactory::createAnimal('dog');
$cat = AnimalFactory::createAnimal('cat');
$mouse = AnimalFactory::createAnimal('mouse');

$dog->makeSound();
```
Output:
```bash
Vau vau
```


