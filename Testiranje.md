# Test driven development

Pristup razvoju softvera koji se fokusira na pisanje testova prije pisanja samog koda.

Osigurava ispravno ponašanje softvera u svim mogućim scenarijima.

## Jedinično testiranje

1. Napišemo test za funkcionalnost koja bi trebala omogućiti mački da dohvati mišta
```php
test('Mačka uspješno lovi miša', function() {
	//setup testa
	$mouse = new Mouse();
	$cat = new Cat();
	//action pozivanje metode
	$cat->hunt($mouse);
	//assertion provjera rezultata
	except($mouse->isCaught())->toBeTrue();
});
```

2. Zatim implementiramo funkciju `hunt` u klasi `Cat` 
```php
class Cat
{
	public function hunt(Mouse $mouse) {
		$mouse->catch();
	}
}
```

3. Pokrenemo test i viidmo da "ne prolazi" jer klasa Mouse nema implementiranu funkciju `catch`
```php
class Mouse
{
	private $isCaught = false;

	public function catch() {
		$this->isCaught = true;
	}

	public function isCaught() {
		return $this->isCaught;
	}
}
```


> [!question]- Kako bi izgledao test za uspoređivanje stvarnog dolaska vlaka s očekivanim?
> ```php
> use PHPUnit\Framework\TestCase;
> 
> class HrvatskeZeljezniceTest extends TestCase {
> 	public function testVrijemeDolaskaKasnjenje() {
> 		
> 		//stvaramo objekt HrvatskeZeljeznice koji kasni
> 		$putovanje = new HrvatskeZeljeznice(true);
> 	
> 		//očekujemo dolazak vlaka tri sata kasnije
> 		$ocekivanoVrijeme = date('H:i',  strtotime('+3 hours'));
> 		
> 		$this->assertEquals($ocekivanoVrijeme, $putovanje->vrijemeDolaska(), "Iznenađenje bi bilo da je došao na vrijeme!");
> 	}	
> }
> ```

## PHPUnit

Framework za jedinično testiranje u PHP-u.
Koristi se za testiranje funkcija/metoda kako bi se osigurala njihova ispravnost.

### assertTrue()
	provjerava da je uvjet istinit (true)
```php
use PHPUnit\Framework\TestCase; 
class TrueAssertionTest extends TestCase 
{ 
	public function testTrueAssertion() { 
		$value = true; 
		$this->assertTrue($value); 
	} 
}
```

### assertFalse()
	provjerava da je uvjet lažan (false)
```php
use PHPUnit\Framework\TestCase;

class FalseAssertionTest extends TestCase 
{ 
    public function testFalseAssertion() {
        $value = false;

        $this->assertFalse($value);
    }
}
```

### assertEquals()
	provjerava da su očekivana i stvarna vrijednost jednake
```php
use PHPUnit\Framework\TestCase;

class EqualsAssertionTest extends TestCase 
{  
    public function testEqualsAssertion() {
        $expected = 42;
        $actual = 42;

        $this->assertEquals($expected, $actual);
    }
}
```

### assertSame()
	provjerava da su očekivana i stvarna vrijednost istog tipa i vrijednosti
```php
use PHPUnit\Framework\TestCase;

class SameAssertionTest extends TestCase 
{    
    public function testSameAssertion() {
        $expected = "42";
        $actual = "42";

        $this->assertSame($expected, $actual);
    }
}
```


Stvorimo klasu `Calculator` koja će sadržavati neke metode:
```php
class Calculator 
{
	public function add($a, $b) {
		return $a + $b;
	}
}
```

Sada možemo krenuti testirati u PHPUnitu:
```php
use PHPUnit\Framework\TestCase;

class CalculatorTest extends TestCase 
{    
    public function testAddition() {
        $calculator = new Calculator();

        // assertTrue example
        $this->assertTrue($calculator->add(2, 2) == 4);

        // assertFalse example
        $this->assertFalse($calculator->add(2, 2) == 5);

        // assertEquals example
        $this->assertEquals(4, $calculator->add(2, 2));

        // assertSame example
        $this->assertSame("4", $calculator->add(2, 2));
    }
}
```
	assertTrue - zbroj 2 i 2 iznosi 4, tako da će ovaj testi proći
	assertFalse - zbroj 2 i 2 nije jednak 5, tako da će ovaj test proći
	assertEquals - zbroj 2 i 2 iznosi 4, tako da će ovaj test proći
	assertSame - zbroj 2 i 2 iznosi 4, ali očekujemo string "4" dok nam test vraća integer 4 tako da ovaj test pada

### assertGreaterThan()
	provjerava da je stvarna vrijednost veća od očekivane vrijednosti
```php
use PHPUnit\Framework\TestCase;

class GreaterThanTest extends TestCase
{
    public function testSuccess()
    {
        $this->assertGreaterThan(10, 20); // Passes, as 20 is greater than 10
    }

    public function testFailure()
    {
        $this->assertGreaterThan(10, 5); // Fails, as 5 is not greater than 10
    }
}
```

### assertLessThan()
	provjerava da je stvarna vrijednost manja od očekivane vrijednosti
```php
use PHPUnit\Framework\TestCase;

class LessThanTest extends TestCase
{
    public function testSuccess()
    {
        $this->assertLessThan(10, 5); // Passes, as 5 is less than 10
    }

    public function testFailure()
    {
        $this->assertLessThan(10, 20); // Fails, as 20 is not less than 10
    }
}
```

### assertArrayHaskey()
	provjerava da ključ postoji u nizu
```php
use PHPUnit\Framework\TestCase;

class ArrayHasKeyTest extends TestCase
{
    public function testSuccess()
    {
        $this->assertArrayHasKey('foo', ['foo' => 'bar']); // Passes, as the array has the key 'foo'
    }

    public function testFailure()
    {
        $this->assertArrayHasKey('foo', ['bar' => 'baz']); // Fails, as the array does not have the key 'foo'
    }
}
```

### assertContains()
	provjerava da se vrijednost nalazi u nizu
```php
use PHPUnit\Framework\TestCase;

class ContainsTest extends TestCase
{
    public function testSuccess()
    {
        $this->assertContains('bar', ['foo', 'bar', 'baz']); // Passes, as the array contains the value 'bar'
        $this->assertContains('bar', 'foobarbaz'); // Passes, as the string contains the substring 'bar'
    }

    public function testFailure()
    {
        $this->assertContains('bar', ['foo', 'baz', 'qux']); // Fails, as the array does not contain the value 'bar'
        $this->assertContains('bar', 'foobazqux'); // Fails, as the string does not contain the substring 'bar'
    }
}
```

### assertEmpty()
	provjerava da je vrijednost prazna
```php
use PHPUnit\Framework\TestCase;

class EmptyTest extends TestCase
{
    public function testSuccess()
    {
        $this->assertEmpty([]); // Passes, as an empty array is empty
        $this->assertEmpty(0); // Passes, as zero is empty
        $this->assertEmpty(''); // Passes, as an empty string is empty
        $this->assertEmpty(null); // Passes, as null is empty
    }

    public function testFailure()
    {
        $this->assertEmpty(['foo']); // Fails, as a non-empty array is not empty
        $this->assertEmpty(1); // Fails, as a non-zero number is not empty
        $this->assertEmpty('foo'); // Fails, as a non-empty string is not empty
        $this->assertEmpty(true); // Fails, as true is not empty
    }
}
```

### assertNotEmpty()
	provjerava da vrijednost nije prazna
```php
use PHPUnit\Framework\TestCase;

class NotEmptyTest extends TestCase
{
    public function testSuccess()
    {
        $this->assertNotEmpty(['foo']); // Passes, as a non-empty array is not empty
        $this->assertNotEmpty(1); // Passes, as a non-zero number is not empty
        $this->assertNotEmpty('foo'); // Passes, as a non-empty string is not empty
        $this->assertNotEmpty(true); // Passes, as true is not empty
    }

    public function testFailure()
    {
        $this->assertNotEmpty([]); // Fails, as an empty array is empty
        $this->assertNotEmpty(0); // Fails, as zero is empty
        $this->assertNotEmpty(''); // Fails, as an empty string is empty
        $this->assertNotEmpty(null); // Fails, as null is empty
    }
}
```


## Laravel testiranje

Odnosi se na proces testiranja Laravel aplikacija kako bi se osigurala njihova funkcionalnost, izdržljivost i skalabilnost.

Laravel testiranje uključuje testiranje različitih dijelova aplikacije, uključujući rute, kontrolere, modele, migracije, seedere i druge dijelove aplikacije. Testovi se mogu pisati pomoću različitih tehnika testiranja, kao što su jedinično testiranje, funkcionalno testiranje i integracijsko testiranje.

#### pokretanje testiranja
```bash
php artisan test
```
	naredba koja pokreće sve testove u direktoriju "test"

#### pojedinačno pokretanja testiranja
```bash
php artisan test --filter <test-name>
```

### Laravel Dusk
	paket za testiranje koji se koristi za automatizirano testiranje web aplikacija

Koristi Selenium WebDriver za emuliranje interakcije korisnika sa web stranicom i provjeru dai li aplikacija ispravno.

>[!question]- Koja je razlika između alata Tinker i Laravel Dusk-a?
>Tinker se pokreće putem terminala te pruža interaktivan `shell` u kojem možemo testirati funkcije i metode. Use case mu je kada nam je potrebna brza eksperimentacija ili upit nad bazom podataka.
>
>Dusk je alat za automatizaciju koji je dizajniran za kompletno testiranje web aplikacije. Koristi emulirani web browser za simulaciju interakcija korisnika s aplikacijom. Use case mu je kada želimo automatizirati testiranje u pregledniku ili kada testiramo interaktivnost s aplikacijom.


#### visit($url)
```php
$this->browser(function ($browser) {
	$browser->visit('/profile')
	//napravi nešto
});
```
	otvara stranicu na zadanom URL-u
	
#### click()
```php
$this->browser(function ($browser) {
	$browser->visit('/dashboard')
			->click('.logout')
			->assertPathIS('/login');
});
```
	ova funkcija simulira klik na element

#### assertSee()
```php
$this->browse(function ($browser){
	$browser->visit('/dashboard')
			->assertSee('Welcome to the dashboard');
});
```
	ova funkcija provjerava nalazi li se određeni tekst na web stranici

#### screenshot
```php
$this->browser(function ($browser) {
	$browser->visit('/dashboard')
			->screenshot('dashboard.png');
});
```
	argument $filename, u ovom slučaju 'dashboard.png', predstavlja naziv datoteke u koju će slika biti spremljena

#### type($selector, $text)
```php
$this->browser(function ($browser) {
	$browser->visit('/dashboard')
			->type('email', 'user@example.com')
			->type('password', 'secret');
});
```
	ova funkcija traži zadano ime input fielda i ispunjava ga

#### press()
```php
$this->browser(function ($browser) {
	$browser->visit('/dashboard')
			->press('Submit');
});
```

#### seePageIs
```php
$this->browser(function ($browser) {
	$browser->visit('/dashboard')
			->seePageIs('/dashboard');
});
```
	ova funkcija provjerava nalazi li se na zadanoj stranici

#### assertTitle
```php
$this->browser(function ($browser) {
	$browser->visit('/dashboard')
			->assertTitle('Dashboard - New App Name');
});
```
	provjerava je li naslov stranice jednak zadanom
>[!info] Assert je u značenju da provjerava, a ne da nanosi nekakvu promjenu.
####  clickLink
```php
$this->browser(function ($browser) {
	$browser->visit('/dashboard')
			->cliclLink('Profile');
});
```
	simulira klik nad zadanim tekstom