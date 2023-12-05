# Radno okruženje


>[!question]- Koje su prednosti, a koji nedostatci VI editora?
>Prednosti su napredne funkcije i mogućnost korištenja UNDO
>Nedostatci su težina korištenja i fokus na korištenju tipkovnice

>[!question]- Koja je svrha kontrole verzija u razvoju softvera?
>Kontrola verzije u razvoju nam omogućava da pratimo tijek razvoja naše aplikacije, lakše implementiramo promjene (ili odbacujemo iste) te mogućnost rada u timovima

>[!question]- Što je Apache?
>Apache je besplatan open-source web server koji omogućava posluživanje web stranica koristeći HTTP protokol

>[!question]- Kako restartamo Apache2 server?
>systemctl restart apache2

>[!question]- Što je MySQL?
>MySQL je besplatan, open-source relacijski sustav upravljanja bazama podataka 

>[!question]- Kako se ulogiramo u MySQL?
>mysql -u user -p lozinka ime-baze-podataka

>[!question]- Što je Composer?
>Composer je alat koji nam omogućava da instaliramo ovisnosti (dependencies) za naše web aplikacije putem različitih paketa

>[!question]- Koja je razlika između composer.lock i composer.json?
>composer.json je datoteka u kojoj su zapisane sve korištene zavisnosti dok je composer.lock datoteka u kojoj su zapisane sve potrebne verzije zavisnosti kako bi web aplikacija normalno radila.

>[!question]- Što trebamo upisati da bi instalirai verziju "2.1" paketa "vendor/paket" pomoću Composera?
>`composer require vendor/paket:2.1`

>[!question]- Kako možemo instalirati određenu verziju paketa koristeći Composer?
>Korištenjem naredbe `composer require ime/paketa:verzija`
## Linux

>[!question]- Koja se naredba koristi za stvaranje novog direktorija u Linuxu?
>`mkdir`

>[!question]- Koja je naredba za pokretanje MySQL poslužitelja?
>`sudo start mysqld`

>[!question]- Kako možemo provjeriti trenutno instaliranu verziju PHP-a u terminalu?
>`php -i`

>[!question]- Kako se može provjeriti trenutni radni direktorij u terminalu na Linuxu?
>`pwd`

>[!question]- Koji je osnovni naredbeni redak za stvaranje novog direktorija u Linuxu?
>`mkdir`

>[!question]- Kako se može prikazati popis datoteka u trenutnom direktoriju?
>`ls`
>`ls -l` za detaljan ispis uključujući vlasnike i ovlasti
>`ls -a` za prikaz skrivenih datoteka

>[!question]- Koja je naredba za kopiranje datoteka u Linux terminalu?
>`cp datoteka lokacija`

>[!question]- Kako se dodjeljuju dozvole (permissions) datotekama ili direktorijima?
>naredbom `chmod`
>primjer: `sudo chmod u+w direktorij`
>gdje je:
>	`chmod `nardeba
>	`u/g/o` oznaka za usera/grupu/other
>	`+/-` označava micanje ili dodavanje ovlasti
>	`w/r/x` označava tip ovlasti
>	`direktorij` direktorij na kojeg primjenjujemo promjenu
>	
>Ukoliko želimo rekurzivno dodijeliti cijeli direktorij i sve foldere unutar koristimo `chmod -R ..`.

>[!question]- Kako se može promijeniti vlasnik datoteke ili direktorija?
>naredbom `chown`
>
>primjer `sudo chown username folder`

>[!question]- Koja je naredba za prikazivanje informacija o sustavu i kernelu?
>`uname -r` za prikaz informacija o kernelu
>`uname -a` za prikaz informacija o sustavu

>[!question]- Kako se može izvršiti skripta ili program u terminalu
>upisom njenog imena u terminalu, na primjer da bi izvršili php skriptu `radi.php` upisujemo
>`php radi.php`

>[!question]- Kako se može koristiti `sudo` za izvođenje naredbi s administratorskim ovlastima?
>`sudo naredba`

>[!question]- Kako se može koristiti `chmod` za promjenu dozvola datoteke u Linuxu?
>`chmod` možemo koristiti tako da navedemo na koga se odnosi promjena u/g/o, zatim dodajemo li mu ili oduzimamo prava s +/-, zatim slovo prava w za write, x za execute i r za read te na kraju datoteku / direktorij na kojeg želimo primjeniti naredbu
>
>`sudo chmod u+r datoteka.txt`

# PHP Basics

>[!question]- Što označava PHP
>Hypertext Preprocessor
    
 > [!question]- Kako započeti komentar u PHP-u?
 > možemo ga započeti s //  ili #
 > ako treba biti kroz više linija možemo koristiti
 > /*
 > */
    
 > [!question]- Koja je razlika između `echo` i `print` funkcija u PHP-u?
 > obje ispisuju tekst/varijable, `echo` je marginalno brži i troši manje resursa za izvršavanje dok `print` uvijek vraća 1 pa se može koristiti u petljama
    
 > [!question]- Kako se definira varijabla u PHP-u?
 > znakom `$`
    
 > [!question]- Koja je razlika između `==` i `===` operatora u PHP-u?
 > znak `==` označava uspoređivanje dvije varijable te se gleda je li njihova vrijednost jednaka, dok `===` uspoređuje vrijednost varijabli i jesu li istog tipa
    
 > [!question]- Kako se koristi `if` izjava u PHP-u?
 > `if (uvjet)
 > {
 > 	kod
 > }
 > `
    
 > [!question]- Što su PHP asocijativni nizovi?
 > Asocijativni nizovi koriste nazive ključeva umjesto numeričkih indeksa
 > Primjer:
 > `$osobe = array("ime" => "Ana", "prezime" => "Horvat", "dob"=>21);`
    
 > [!question]- Kako se izvodi petlja `foreach` u PHP-u?
 > `foreach ($array as $key)
 > {
 > 	//neki kod
 > }`
    
 > [!question]- Kako se povezuju podatkovni tipovi u PHP-u?
 > Povezuju se i pretvaraju automatski ovisno o kontekstu izraza
 > Primjer:
 >`$broj = "3";`
 >`(int)$broj++;`
 > `echo $broj;`
 > Output:
 > `4`
    
> [!question]- Kako se koristi `include` i `require` u PHP-u?
> `include 'datoteka.php'`
    
 > [!question]- Što je funkcija u PHP-u i kako se definira?
 > definira se s `function imefunkcije () {};`
 > funkcija je blok koda koji odrađuje neki zadatak
    
 > [!question]- Što je i kako se koristi superglobalna varijabla `$_GET`?
 > Koristi se tako što dohvaćuje vrijednosti iz URL paramtera
 > `$name = $_GET['name'];`
    
> [!question]- Kako se rukuje greškama u PHP-u?
> Koriste se try-catch blokovi, ini_set ili bilo koja druga funkcija za generalno dohvaćanje errora
    
> [!question]- Kako se koristi `mysqli` za izvršavanje SQL upita u PHP-u?
> `mysqli` se koristi s predefiniram funkcijama poput `mysqli_connect()`, `mysqli_fetch_assoc()`, `mysqli_close()`

>[!question]- Kako deklarirati PHP funkciju koja prihvaća promjenjivi broj argumenata?
>`function funkcija (...$args) {};`

>[!question]- Kako zatvoriti datoteku u PHP-u?
>`fclose($datoteka);`
>>[!info] moramo navesti varijablu kao resurs, ne možemo navesti dolsovno ime datoteke koju zatvaramo.

>[!question]- Kako se stvara niz u PHP-u?
>`$niz = array();`
>`$niz = [];`


# Bullshit teorija

>[!question]- Što je MVC arhitekturni obrazac i kako se sastoji?
>MVC obrazac je način rada s web aplikacijama pomoću kojeg je olakšano stvaranje web aplikacija. Sastoji se od modela, viewa i controllera gdje su modeli zaduženi za funkcije operacije i interakciju s bazom podataka, view je ono što se korisniku prikazuje na ekranu, a controller preuzima input od korisnika, prerađuje ga i šalje modelu za daljnju obradu/stavljanje u bazu

>[!question]- Koje su glavne odgovornosti sloja Modela u MVC arhitekturi?
>Interakcija s bazama podataka, izvršavanje CRUD operacija nad bazom podataka

>[!question]- Kako Controller upravlja komunikacijom između Modela i Viewa?
>Controller dobiva input od korisnika preko viewa (npr neka forma), validira input te ga šalje modelu za daljnju obradu nad tim podacima 

>[!question]- Kako View prikazuje informacije korisnicima u MVC arhitekturi?
>Najčešće putem HTML datoteke u kojoj su po potrebi ubačeni JS i PHP (na primjer ako treba ispisati petljom sve rekorde iz baze podataka korisniku)

>[!question]- Kako se izvodi proces implementacije u kontekstu PHP backend developmenta?
>Analiza, Postavljanje radnog okvira, razvoj funkcionalnosti, rad s bazama podataka, sigurnost, testiranje, optimizacija koda, dokumentacija, deployment, održavanje

>[!question]- Kako se koristi GIT za prijenos projekta, i koji su osnovni koraci?
>git push na udaljeni repozitorij, git pull za dohvaćanje.
>Osnovni koraci su izrada računa na nekom od servisa koji hosta udaljene repozitorije, prijenos podataka na GIT te deployment istih
>>[!info] [[Bullshit teorija]]
>

>[!question]- Što je MySQL migracija i koji su koraci u procesu migracije podataka?
>[[Bullshit teorija]]

>[!question]- Što je DNS i koja mu je svrha u kontekstu internetskog komuniciranja?
>Domain Name System mijenja domenu u ljudski čitljiv oblik (umjesto IP adrese u npr algebra.hr)

>[!question]- Koje su razlike između Shared hostinga, VPS hostinga i Dedicated hostinga?
>Shared hosting znači da se na jednom serveru odvojeno više korisnika koji dijele resurse tog servera,
>VPS hosting znači da se jedan server dijeli na virtualne privatne servere za više korisnika
>Dedicated hosting znači da se jedan server koristi isključivo za potrebe jednog korisnika / jedne web aplikacije

>[!question]- Kako se koristi FTP (File Transfer Protocol) za prijenos datoteka preko interneta?
>putem uključene funkcije `ftp_connect`

>[!question]- Kako kontinuirana integracija (CI) doprinosi razvoju softvera i koje su neki popularni CI alati?
>Doprinosi produktivnosti zato što omogućava neometan razvoj kada više ljudi doprinosi razvoju aplikacije radi automatskih testova koji se brinu o stabilnosti softvera, popularni alati: Jenkins i GitLab

# ER dijagrami

>[!question]- Kako definirate entitet u kontekstu baze podataka i ER dijagrama?
>Entitet predstavla objekt, stvar ili pojavu u stvarnom svijetu koji je relevantan za modeliranje baze podataka

>[!question]- Što predstavlja atribut entiteta, i kako se razlikuje od entiteta?
>atribut entiteta predstavlja svojstva entieta npr. vanjski ključeva te kao takav ne definira nikakav objekt unutar baze podataka nego samo svojstva nekog objekta

>[!question]- Koje su glavne vrste veza između entiteta u ER dijagramu?
>jedan-na-jedan, jedan-na-mnogo, mnogo-na-jedan, mnogo-na-mnogo

>[!question]- Kako označavate kardinalnost veza između entiteta (jedan prema jedan, jedan prema više, više prema više) u ER dijagramu?
>brojevima 1 , 0 ili N

>[!question]- Što je kompozitni atribut i kako se koristi u ER dijagramu?
>Atribut sastavljen od više dijelova ili komponenti gdje svaki dio može imati svoje vlastite atribute

>[!question]- Koja je svrha primarnog ključa (Primary Key) u entitetu baze podataka?
>osigurava unikatnost i red unutar baze podataka

>[!question]- Kako se razlikuju entiteti i veze u ER dijagramu?
>Entiteti predstavljaju nekakav objekt odnosno pojam u bazi podataka, dok veza predstavlja odnos između identiteta
>
>Entiteti mogu biti `član` ili `knjiga`, dok su veze `posudio`

>[!question]- Što su vanjski ključevi (Foreign Keys) i kako se koriste u vezama između entiteta?
>Vanjski ključevi služe za uspostavljanje veze između dvije tablice. Vanjski ključ referencira na primarni ključ u jednoj tablici te s time omogućava stvaranje veze između podataka u tim tablicama

>[!question]- Kako označavate oznake direktnog i neizravnog participacije entiteta u vezi?
>DIrektan:
>A ---------◆--------- B
>
>Neizravan:
>A ---------◆--------- B
>        /
>      ◆
>         \
>           C
>           

>[!question]- Kako biste predstavili naslijeđivanje između entiteta u ER dijagramu?
>Naslijeđivanje između entiteta u ER dijagramu obično se predstavlja pomoću generalizacije/specijalizacije, gdje jedan entitet (podskup) dijeli zajedničke atribute s drugim entitetom (nadblok).

# PHP Advanced

>[!question]- Što je objektno orijentirano programiranje (OOP) i koje su njegove glavne karakteristike?
>Način izrade koda, glavna karakteristika je korištenje objekta i klasa

>[!question]- Kako se definira klasa u PHP-u, i koje su osnovne komponente klase?
>Klasa se definira kao osnovna podloga za stvaranje objekta te definiranje njihovog ponašanja, osnovne komponente klase su metode i svojstva

>[!question]- Koja su četiri osnovna koncepta objektno orijentiranog programiranja?
>Nasljeđivanje, polimorfizam, enkapsulacija, apstrakcija

>[!question]- Što znači apstrakcija u kontekstu OOP-a?
>Apstrakcija označuje sakrivanje složenosti i prikaz samo jednostavnih, relevantnih dijelova sustava

>[!question]- Kako se postiže enkapsulacija u PHP-u, i zašto je važna?
>Postiže se izoliranjem procesa i varijabli tako da se dobije kontrolirani sustav. Važno je radi sigurnosti, skalabilnosti i olakšane održivosti koda

>[!question]- Što je nasljeđivanje u OOP-u, i kako se koristi u PHP-u?
>Nasljeđivanje je kada jedna klasa naslijedi svojstva i metode svoje `parent` klase radi podjele klasa u podklase sa svojim specifičnim svojstvima i metodama.
>
>`class Book extends Product {}`

>[!question]- Kako se postiže polimorfizam u OOP-u, i možete li dati primjer iz PHP-a?
>Postiže se spajanjem apstrakcije i nasljeđivanja. Polimorfizam omogućuje objektima da se ponašaju na različite načine ovisno o kontekstu podataka s kojim rade

>[!question]- Koja je svrha konstruktor metode u PHP klasama?
>Inicijalizira objekt s početnim svojstvima. Osigurava da će objekt biti pravilno inicijaliziran te da će imati punu predviđenu funkciju.

>[!question]- Kako se deklarira privatni član klase i što znači?
>`private function radi()` ili `private $var`
>Znači da tim metodama/svojstvima možemo pristupiti isključivo unutar klase u kojoj su definirani

>[!question]- Kako se koristi apstraktna klasa i apstraktne metode u PHP-u?
>Apstraktna metoda nam omogućuje da stvorimo okvir funkcionalnosti kojeg možemo razraditi u različitim podklasama.
>
>`abstract class Oblik` ili `abstract public function funkcija()`

>[!question]- Što su statičke metode u PHP-u i kako ih pozivamo?
>Statičke metode pripadaju klasi, a ne instanci klase, što znači da se statičke metode mogu pozivati na klasi, a ne putem objekta. Pozivamo ih ovako:
>`Klasa::statickaMetoda()` umjesto `$objekt->statickaMetoda()`

>[!question]- Što je sučelje (interface) u PHP-u, i kako se koristi?
>Interface definira svojstva ili metode koja sve klase moraju uključiti, definira se putem `interface Sucelje {}`
>
>te se nadodaje klasi `class Klasa implements Sucelje`

>[!question]- Kako se implementira Singleton uzorak u PHP-u, i koja je njegova svrha?
>Singleton osigurava da će se postojati samo jedna instanca tokom cijelog izvođenja programa
>Rješenje: [[Rješenja | #singleton ]]

>[!question]- Objasnite Factory uzorak i kako se koristi u PHP-u?
>Factory uzorak nam automatski stvara nove instance objekta
>Rješenje: [[Rješenja | #factory]]

>[!question]- Kako se stvara veza s MySQL bazom podataka koristeći MySQLi u PHP-u?
>`$dbc = mysqli_connect("hostname", "username", "password", "dbname");`

>[!question]- Koja je prednost korištenja PDO u odnosu na MySQLi za rad s bazama podataka u PHP-u?
>PDO pristupa objektno orijentarnom pristupu te se podaci iz baze podataka predstavljaju kao objekti što nam olakšava rad ako u ostatku aplikacije koristimo objektno orijentirani pristup

>[!question]- Kako se rukuje iznimkama u PHP-u pomoću try-catch blokova?
>Try {
>
>}catch (Exception $e) {
>	echo $e->getMessage();	
>}
>
>Kod unutar try funkcije će se izvršiti te umjesto da se aplikacija crasha, dobivamo error kojeg pospremamo u exception $e

>[!question]- Kako se koristi autoloader funkcija u PHP-u, i koja je njena svrha?
>autoloader nam dinamički učitava klase prilikom njihovog prvog korištenja umjesto da ručno uključujemo klase.
>Rješenje: [[Rješenja | #autoloader ]]

>[!question]- Kako se stvara veza s bazom podataka pomoću PDO u PHP-u?
>`$dsn = "mysql:host=localhost;dbname=ime_baze";`
>`$pdo = new PDO($dsn, $username, $password);`
>
>upiti:
>`$stmt = $pdo->query("UPIT");`
>`while ($row = $stmt->fetch())`




# Laravel

>[!question]- Koje su prednosti Laravel frameworka koje ističeš?
>Jednostavnost upravljanja ruta, unaprijed ponuđena rješenja itd.

>[!question]- Kako se koristi Composer za instalaciju novog Laravel projekta?
>`composer create-project laravel/laravel ime-projekta`

>[!question]- Kako konfigurirati bazu podataka u Laravelu?
>putem predloška datoteke u .env

>[!question]- Kako koristiti migracije u Laravelu za promjene u bazi podataka?
>php artisan migrate

>[!question]- Što su seederi u Laravelu i kako ih koristiti?
>Seeder je mehanizam koji omogućava ispunjavanje baze podataka s početnim podacima.
>Za pokretanje određenog seedera koristimo
>`php artisan db:seed --class=seeder-name`

>[!question]- Kako postaviti relacije između modela u Laravel Eloquent ORM-u?

>[!question]- Što je Eloquent ORM i kako olakšava rad s bazama podataka?

>[!question]- Kako dohvatiti podatke iz baze pomoću Eloquent metoda?

>[!question]- Kako kreirati novi redak u bazi pomoću Eloquent modela?

>[!question]- Kako ažurirati podatke u bazi pomoću Eloquent modela?

>[!question]- Kako obrisati redak iz baze pomoću Eloquent modela?

>[!question]- Kako koristiti Artisan naredbe za upravljanje Laravel projektom?

>[!question]- Što su middleware-ovi i kako se koriste u Laravelu?

>[!question]- Kako definirati rute u Laravelu i što predstavljaju?

>[!question]- Koja je svrha migracija u Laravelu?

>[!question]- Kako koristiti Laravel DB facadu za izvođenje SQL upita?

>[!question]- Kako selektirati podatke iz baze pomoću Laravel DB facada?

>[!question]- Kako ubaciti nove podatke u bazu pomoću Laravel DB facada?

>[!question]- Kako ažurirati podatke u bazi pomoću Laravel DB facada?

>[!question]- Kako obrisati podatke iz baze pomoću Laravel DB facada?

>[!question]- Što je ThrottleRequests middleware i kako se koristi?

>[!question]- Kako definirati belongsTo relaciju u Laravel Eloquent modelu?

>[!question]- Kako koristiti Eloquent hasManyThrough relaciju?

# Testiranje

>[!question]- Kako se instalira PHPUnit u Laravel projektu?

>[!question]- Kako se pokreću PHPUnit testovi u Laravelu?

>[!question]- Kako definirati PHPUnit test u Laravel aplikaciji?

>[!question]- Kako testirati rutu u Laravel Dusku pomoću PHPUnit-a?

>[!question]- Kako koristiti Mock objekte u PHPUnit testovima u Laravel Dusku?

>[!question]- Kako testirati kontrolere u Laravel Dusku pomoću PHPUnit-a?

>[!question]- Kako testirati modele u Laravel Dusku koristeći PHPUnit?

>[!question]- Kako koristiti TestCase klasu u Laravel Dusku za testiranje?

>[!question]- Kako simulirati HTTP zahtjeve u PHPUnit testovima za Laravel Dusk?

>[!question]- Kako konfigurirati PHPUnit.xml datoteku za Laravel Dusk testove?

# Praktični zadaci

>[!todo] Napiši kratki PHP kod koji koristi do-while petlju za ispisvanje brojeva od 40 do 19.

>[!todo] Napiši kratki PHP kod koji koristi while petlju za ispisivanje neparnih brojeva od 14 do 34.

>[!todo] Napiši kratki PHP kod koji koristi for petlju za ispis svih brojeva od 1-100 koji su djeljivi sa 7 ili 9, ali preskoči brojeve 63, 70 i 90.

>[!todo] Napiši PHP funkciju koja prima dva parametra: broj brojeva koji se generiraju i s kojim brojem bi trebali biti djeljivi. Funkcija dodaje generirane brojeve na kraj polja te vraća `$niz_brojeva`.

>[!todo] Napravi klasu `HrvatskeZeljeznice` koja ima metodu `vozi()` i svojstvo `kasnjenje`.

>[!todo] Koristeći prošlo pitanje kreiraj objekt tipa `HrvatskeZeljeznice`

## AI generated pitanja

>[!todo] Objektno orijentirano programiranje (PHP): Napiši PHP klasu koja predstavlja automobil s atributima poput modela, boje i godine proizvodnje. Dodaj metodu koja ispisuje informacije o automobilu.

>[!todo] Objektno orijentirano programiranje (PHP): Kreiraj dvije klase, jednu koja predstavlja voće (npr. jabuka) i drugu koja predstavlja voćnjak. Implementiraj nasljeđivanje tako da voće ima zajedničke atribute poput boje, a voćnjak ima metodu za brojanje ukupnog voća.

>[!todo] Laravel: Stvori Laravel rutu koja vraća tekst "Hello, Laravel!".

>[!todo] Laravel: Kreiraj kontroler u Laravelu koji ima metodu za dohvaćanje svih korisnika iz baze podataka. Iskoristi Eloquent model.

>[!todo] Singleton: Implementiraj Singleton uzorak u PHP-u. Stvori klasu koja predstavlja jedinstvenu konfiguraciju sustava i omogući pristup toj konfiguraciji iz različitih dijelova koda.

>[!todo] Factory: Napiši Factory metodu za kreiranje objekata u PHP-u. Primjerice, stvori Factory metodu koja dinamički generira različite vrste vozila.

>[!todo] Laravel Dusk testiranje: Napiši Laravel Dusk test koji provjerava je li naslov stranice ispravan.

>[!todo] Laravel Dusk testiranje: Koristeći Laravel Dusk, simuliraj unos podataka u formu i provjeri je li rezultat ispravan.

>[!todo] Laravel Eloquent: Koristeći Eloquent, stvori model za knjige s atributima poput naslova, autora i godine izdanja. Dodaj metodu koja vraća sve knjige koje su izdate nakon određene godine.

>[!todo] Laravel Eloquent: Napravi Eloquent upit koji dohvaća sve korisnike koji imaju više od 25 godina.

>[!todo] Objektno orijentirano programiranje (PHP): Kreiraj apstraktnu klasu koja predstavlja oblik geometrijskog lika. Implementiraj dvije izvedene klase koje predstavljaju pravokutnik i krug te dodaj metode za izračun površine.

>[!todo] Objektno orijentirano programiranje (PHP): Definiraj sučelje (interface) koje predstavlja funkcionalnost mjesta na karti (npr. latitude i longitude). Implementiraj klasu koja koristi to sučelje.

>[!todo] Laravel: Stvori Laravel migraciju za stvaranje tablice koja će pohranjivati informacije o knjigama. Tablica treba imati polja poput naslova, autora i godine izdanja.

>[!todo] Laravel: Napiši Laravel Seed klasu koja će popuniti tablicu knjiga s nekoliko uzoraka podataka.

>[!todo] Singleton: Razvij klasu koja predstavlja logger. Implementiraj Singleton uzorak kako bi osigurao jedinstveno dijeljenje logger instance među različitim dijelovima koda.

>[!todo] Factory: Stvori Factory metodu koja generira nasumične podatke o korisnicima poput imena, e-mail adresa i godina rođenja.

>[!todo] Laravel Dusk testiranje: Koristeći Laravel Dusk, provjeri je li korisničko sučelje registracijskog obrasca ispravno. Simuliraj unos podataka i provjeri rezultat.

>[!todo] Laravel Dusk testiranje: Napiši Dusk test koji simulira pregledavanje nekoliko stranica unutar aplikacije i provjeri je li navigacija ispravna.

>[!todo] Laravel Eloquent: Stvori model za studente s atributima poput imena, prezimena i broja indeksa. Dodaj metodu koja vraća sve studente koji su upisani na određeni smjer.

>[!todo] Laravel Eloquent: Napravi Eloquent upit koji dohvaća sve knjige koje su napisane određenim autorom.

>[!todo] Objektno orijentirano programiranje (PHP): Implementiraj polimorfizam kroz sučelje i klase koje predstavljaju različite oblike prijevoznih sredstava. Svako prijevozno sredstvo treba imati metodu za prikaz informacija.

>[!todo] Objektno orijentirano programiranje (PHP): Stvori apstraktnu klasu koja predstavlja oblik voća. Implementiraj nasljeđene klase za različite vrste voća (npr. jabuka, banana) s dodatnim atributima.

>[!todo] Laravel: Definiraj Laravel rutu koja prima parametar (npr. ID knjige) i vraća informacije o odabranoj knjizi.

>[!todo] Laravel: Kreiraj Laravel kontroler koji ima metodu za dodavanje nove knjige u bazu podataka.

>[!todo] Singleton: Napravi Singleton logger koji zapisuje poruke u tekstualnu datoteku. Implementiraj metodu za zapisivanje poruka.

>[!todo] Factory: Razvij Factory metodu za stvaranje nasumičnih podataka o proizvodima poput naziva, cijene i opisa.

>[!todo] Laravel Dusk testiranje: Koristi Laravel Dusk za testiranje funkcionalnosti koja uključuje unos podataka u formu i provjeru je li rezultat ispravan.

>[!todo] Laravel Dusk testiranje: Napiši Dusk test koji provjerava funkcioniranje korisničke prijave. Simuliraj unos ispravnih korisničkih podataka.

>[!todo] Laravel Eloquent: Stvori model za predavanja s atributima poput naslova, opisa i vremena održavanja. Dodaj metodu koja vraća sva predavanja zakazana za određeni datum.

>[!todo] Laravel Eloquent: Kreiraj Eloquent upit koji dohvaća sve korisnike koji su stariji od 30 godina i imaju određeni status.
