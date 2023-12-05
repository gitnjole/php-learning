# **HYPERTEXT PREPROCESOR**

```php
<?php

?>
```

Ako se u datoteci nalazi isključivo PHP kod, ne koristimo tag `?>` za zatvaranje.

## Ispis

echo
```php
echo "string";

echo "{$string}";

echo 'string';
```
	ako želimo koristiti {} za variable parsing, obavezno moramo imati "", a ne ''

```php
echo "{$_POST['name']}";

$query = "SELECT * FROM users WHERE id = '2' ";
```
	koristimo '' ako trebamo navoditi tekst unutar navodnika koda

print
```php
print "string";
```

print_r
```php
print_r($string)
```
	generalno se koristi za ispisivanje arraya ili objekata
	
> [!info]- Razlika između echo i print
> echo je generalno brži i troši manje resursa te nema return value
> print uvijek vraća 1 tako da se može koristiti u izrazima te je neznatno sporiji

var_dump
koristi se za debugging te pruža detaljan pogled na varijablu

```php
$array = [1,2,3];
var_dump($array);
```
Output:
```bash
array(3) {
  [0]=>
  int(1)
  [1]=>
  int(2)
  [2]=>
  int(3)
}
```

> [!warning] echo se ne koristi prije var_dump, ta funkcija sama po sebi radi ispis!

die ili exit
nemoj koristiti ako nije potreban.
terminira skriptu i izbacuje poruku

```php
$error_message = "An error occured!";

die($error_message);
//exit($error_message);
```

> [!warning] nemoj koristiti ako nije potrebno radi preuranjene terminacije skripte!

### Komentari

```php
<?php
#komentar

//komentar

/*komentar*/

/*
	Jedan redak komentara
	Drugi redak komentara
	.
	.
	.
	N-ti redak komentara
*/

```
	`ctrl shift A` na onzačeni tekst čini komentar, ako se radi o više redaka koda napravi se redak kao na zadnjem primjeru


## Tipovi podataka

### string
	tekst
```php
$var = "string";
```

### int
	broj
```php
$var = 32;
```

### float
	decimalan broj
```php
$var = 3.14;
```

### boolean
	sadržava jedino true ili false
	može se koristiti i kao 1 ili 0
```php
$condition = true;
```
### array
	niz
```php
$array = [1,2, 'Marko'];
```

Članovima nizova pristupamo putem indeksa
```php
echo $array[0].PHP_EOL;

echo $array[2].PHP_EOL;
```
>[!info] PHP_EOL je konstanta koja zamjenjuje "\\n", označava novu liniju u ispisu

>[!info] PHP_EOL neće pravilno raditi na web stranicama jer HTML drugačije interpretira \\n

Output:
```bash
1
Marko
```

>[!warning] Indeks započinje s 0, a ne 1!


Naredbe za rad s nizovima:
	count() - vraća broj elemenata
	sort() - sortira niz u rastućem redoslijedu
	rsort() - sortira niz u padajućem redoslijedu
	array_push() - dodaje novi element na **kraj** niza
	array_pop() - uklanja zadnji element niza i **vraća ga kao vrijednost**
	array_rand() - miješa listu i vraća određeni broj članova **kao ključeve niza**
```php
$niz = array();
print_r($niz);

array_push($niz, "prvi", "drugi", "treći", "četvrti", "mjau");
print_r($niz);

$pop = array_pop($niz);
echo "popped element: {$pop}".PHP_EOL;
print_r($niz);

$random = array_rand($niz, 2);
echo $niz[$random[0]].PHP_EOL;
```
Output:
```bash
Array
(
)

Array
(
    [0] => prvi
    [1] => drugi
    [2] => treći
    [3] => četvrti
    [4] => mjau
)

popped element: mjau

Array
(
    [0] => prvi
    [1] => drugi
    [2] => treći
    [3] => četvrti
)

treći
```


### null
	odsutnost bilo kakve vrijednosti, odnosno nepostojeća vrijednost
```php
$unkown = null;
```
>[!danger] null nije isto što i 0 ili prazan string " " !


## Varijable

### globalne varijable

Definirane su izvan funkcije i mogu se koristiti unutar bilo koje funkcije. One su dostupne u cijelom programu. Deklariranje globalne varijable koristimo `$GLOBALS['variable_name'];`
```php
$globalna_varijabla = "GLOOOOOOOBBBBAAAAAAALLLLLL";

function ispis ()
{
	global $globalna_varijabla;
	echo $globalna_varijabla;
}
```

### superglobalne varijable

Superglobalne varijable u PHP-u su globalne varijable koje su dostupne unutar svih dijelova skripte, bez obzira na opseg u kojem su definirane. One su automatski globalne i može im se pristupiti bilo gdje u kodu. 

1. **$_GET:**
    
    - Sadrži podatke poslane preko HTTP GET zahtjeva, obično putem URL parametara.
    
1. **$_POST:**
    
    - Sadrži podatke poslane preko HTTP POST zahtjeva, obično kroz forme.

3. **$_REQUEST:**
    
    - Sadrži podatke poslane preko HTTP GET, POST i COOKIES metoda. Ova varijabla se može koristiti za pristup podacima bez obzira na način slanja.

4. **$_SESSION:**
    
    - Sadrži podatke o sesiji, koji se mogu koristiti za pohranjivanje informacija između različitih zahtjeva na istoj sesiji.

5. **$_COOKIE:**
    
    - Sadrži podatke poslane od klijenta (browsera) putem HTTP kolačića.

6. **$_SERVER:**
    
    - Sadrži informacije o serveru i izvršavanju trenutnog skriptnog zahtjeva, kao što su putanja datoteke, metoda HTTP zahtjeva i mnoge druge informacije.

7. **$_FILES:**
    
    - Sadrži informacije o datotekama koje su poslane putem HTTP POST zahtjeva, obično kroz formu za prijenos datoteka (file upload).

8. **$_ENV:**
    
    - Sadrži informacije o okolini, tj. varijable okoline koje su postavljene na serveru.


```php
$username = $_POST['username'];

var_dump($_SERVER['PWD']);
```
Output:
```bash
string(14) "/home/compiler"
```

## Rad s podacima

" = " pridodaje desnu vrijednost lijevoj varijabli
" == " uspoređuje samo vrijednosti
" === " uspoređuje i vrijednosti i tipove podataka

```php
$a = "5";
$b = 4;

if ($a == $b) {
	echo "{$a} je jednak broj kao {$b}";
} 
else {
	echo "{$a} nije jednak broj kao {$b}";
}
/*
	Output:
	5 nije jednak broj kao 4
*/

$a = "4";
if ($a === $b) {
	echo "{$a} je jednak broj i tip podatka kao {$b}";
} 
else {
	echo "{$a} nije jednak broj ili tip podatka kao {$b}";
}
/*
	Output:
	4 nije jednak broj ili tip podatka kao 4
*/
```

## Petlje

### if, else if, else

```php
$a = 10;
$b = 20;

if ($a == $b) {
	echo "{$a} je jednako {$b}";
}
else if ($a > $b) {
	echo "{$a} je veće od {$b}";
}
else {
	echo "{$b} je veće od {$a}";
}
```
Output:
```bash
20 je veće od 10
```

### while
	dokle god je uvjet istinit, prolazi kroz petlju

```php
$number = 10;

while($number >= 0) {
    echo $number.PHP_EOL;
    $number--;
}
```


### do while
	isto kao while, ali do nam osigurava da će se petlja izvršiti barem jedanput
	
```php
$i = 0;  
do {  
	echo $i;  
} while ($i > 0);
```

### for
```php
for ($i = 0; $i <= 10; $i++) {
	echo $i.PHP_EOL;
}
```

> [!question]- Kada koristimo for, a kada while petlju?
> for petlju koristimo kada znamo točan broj iteracija koje želimo odraditi, dok while koristimo kada nismo sigurno koliko puta trebamo iterirati kroz petlju.

> [!info]- Ukoliko se blok sastoji od samo jedne linije, ne moramo koristiti vitičaste {} zagrade
> if ($a > $b) echo "a > b";
> else echo "a < b";
> 
> for ($i = 0; $i < 5; $i++) echo $i.PHP_EOL;

### ternarna operacija
	korisna kada testiramo jednostavne uvjete 

```php
if ($number >= 50) {
	$result = 'Not to fifty!';
}
else {
	$result = 'It could be worse';
}
```

**uvjet ? rezultat1 : rezultat2**

```php
$result = $number > 20 ? 'Not to fifty!' : 'It could be worse';
```

>[!warning] u stvarnom pisanju koda uvijek se preferira korištenje prave if / else petlje radi čitljivosti koda!


## Rad s datotekama

#### include / require
Koristimo `include` ili `require` kako bi smo rekli programu da uključi i izvrši kod iz vanjske datoteke.

```php
<?php

require 'function.php';
include 'output.php';
```
>[!info]+ Razlika između include i require:
>`include` generira samo upozerenje ako datoteka nije pronađena, dok `require` generira fatalnu grešku.

#### use
	uvoz namespacea ili traitova
Kada se `use` koristi unutar klase, funkcije ili namespace-a, omogućava lakši pristup klasama i trait-ovima unutar tog konteksta, čime se izbjegava potreba za punim putanjama do klasa svaki put kad se koriste.

Primjer uvoza namespacea
```php
use Namespace\Podnamespace\Klasa;

$objekt = new Klasa;
```

Primjer uvoza traita
```php
use TraitNamespace\TraitName;

class MojaKlasa
{
	use TraitName;

	//kod
}
```

Primjer korištenja aliasa
```php
use Namespace\DugackiNamespace\ImeDugeKlase as KraceIme;

$objekt = new KraceIme();
```

#### autoloading
Omogućava automatsko uključivanje klasa po potrebi. 

```php
spl_autoload_register(function ($class) { 
	include 'classes/' . $class . '.class.php'; 
});
```
#### fopen

Čitanje iz datoteke:
```php
$datoteka = fopen("putanja/do/tvoje/datoteke.txt", "r"); 
 
if ($datoteka) { 
	while (!feof($datoteka)) { 
		$redak = fgets($datoteka); 
		echo $redak; 
	} 
	
	fclose($datoteka); 
} 
else { 
	echo "Nije moguće otvoriti datoteku."; 
}
```
	fopen otvara datoteku; 
		prvi argument mora biti ime datoteke s ekstenzijom (ukoliko se datoteka nalazi u nekom drugom folderu potrebna nam je cijela putanja do te datoteke) 
		drugi argument mora biti način rada s datotekom:
			"r" - read only
			"r+" - read/write (od početka datoteke)
			"w" - write only
			"w+" - read/write (stvara novu datoteku ako već ne postoji)
			"a" - append (zapisuje na kraj datoteke te stvara novu ako već ne postoji)
			"a+" - read/append
			"x" - write (stvara novu datoteku, ako već postoji vraća FALSE)
			"x+" - read/write (isto kao x)
			"c" - write (stvara novu datoteku ako već ne postoji, stavlja pointer na početak)
			"c+" - read/write (isto kao c)
	
	feof testira postoji li end-of-file znak
	fgets dobiva jedan redak iz datoteke
	fclose zatvara stream

Upisivanje u datoteku: 
```php
$datoteka = fopen("putanja/do/tvoje/datoteke.txt", "w+"); 
 
if ($datoteka) { 

	fwrite($datoteka, "Novi redak teksta.");
	fclose($datoteka); 
} 
else { 
	echo "Nije moguće otvoriti datoteku."; 
}
```
	fwrite zapisuje u datoteku;
		prvi argument je datoteka u koju se zapisuje
		drugi argument je content koji se upisuje

#### JSON

Čitanje JSON datoteke:
```php
$jsonString = file_get_contents('putanja/do/tvoje/datoteke.json'); 

$data = json_decode($jsonString, true); 

if ($data === null && json_last_error() !== JSON_ERROR_NONE) { 
	echo 'Greška pri čitanju JSON datoteke.'; 
}
else { 
	print_r($data);
} 
```


Upisivanje u JSON datoteku:
```php
$data = [ 
	'ime' => 'John', 
	'prezime' => 'Doe', 
	'dob' => 30 
];

$jsonString = json_encode($data, JSON_PRETTY_PRINT);

file_put_contents('putanja/datoteke.json', $jsonString);

echo 'Podaci su uspješno spremljeni u JSON datoteku.';
```

#### unlink
	 briše datoteku na navednoj putanji
```php
unlink('datoteka.txt');
```

## Funkcije

Funkcija je blok koda koji se može pozivati iz drugih dijelova programa kako bi se izvršile određene radnje.

Kako bi vratili vrijednost iz PHP funkcije koristimo `return $value;`

```php
function write($string) {
	echo $string.PHP_EOL;
}

write("Hello!");
```
### varijabilne funkcije
	funkcija koja prihvaća promjenjivi broj argumenata
	
```php
function varijabilnaFunkcija (...$args) {
	foreach ($args as $arg) {
		echo $arg . ' ';
	}
}

varijabilnaFunkcija('arg1', 'arg2', 'arg2');
```
Output:
```bash
arg1 arg2 arg2 
```

>[!info]+ Značenje ...
>... označuje "splat" ili operator otpakiravanja koji nam dopušta da uvedemo proizvoljan broj argumenata 

### rekurzivne funkcije
	funkcija koja poziva samu sebe

```php
function faktorijel($n) {
	if ($n == 0) {
		return 1;
	}
	else {
		return $n * faktorijel($n - 1);
	}
}

echo faktorijel(8);
```
Output:
```bash
40320
```

## Rad sa sesijama

### Cookies
Male tekstualne datoteke koje se pohranjuju na računalu korisnika kada korisnik posjeti web stranicu.

Za inicijaliziranje korisitmo `setcookie()`;
Za čitanje vrijednosti koristimo superglobalnu varijablu `$_COOKIE['username']`
Za brisanje trebamo postaviti vrijeme isteka u prošlost

```php
setcookie('user', 'John Doe', time() + 3600, '/');
```
	setcookie - postavlja cookie
	user - ime vrijednosti cookija
	John Doe - vrijednost cookija
	time() + 3600 - vrijeme isteka cookija, zapisuje se u sekundama
	'/' - putanja na serveru gdje će cookie biti dostupan, '/' označava da će cookie biti dostupan kroz cijelu domenu
```php
$username = $_COOKIE['user'] ?? null;

if ($username !== null) {
	echo "Welcome, back {$username}!";
}
else {
	echo "Welcome, guest!";
}
```
>[!info]- zašto ''??''
> `??` imena nulti operator spajanja provjerava je li varijabla postavljena te ukoliko nije, postavlja ju. U ovom slučaju ako ne postoji cookie imena `user` označujemo da nema vrijednost s `null`.

Brisanje cookija:
```php
setcookie('user', '', time() - 3600);
```
	stavljamo ga u 1 sat u prošlost, te vrijednost usera stavljamo kao empty string

### Sessions
Omogućavaju očuvanje podataka između različitih zahtjeva korisnika na web stranici.
Sesije se koriste za pohranu privremenih podataka, poput korisničkih postavki, prijavljenog statusa i drugih informacija, tijekom trajanja posjete korisnika na web mjestu
>[!warning] Ukoliko korisnik zatvori browser, sesija se briše!

Za inicijaliziranje koristimo `session_start();`
Za postavljanje vrijednosti koristimo `$_SESSION['username'] = 'john_doe';`
Za uništavanje sesije koristimo `session_destroy();`
