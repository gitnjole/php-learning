# MVC

MVC (Model-View-Controller) je arhitektonski obrazac koji se koristi za organiziranje i strukturiranje PHP web aplikacija.

Konceptualno, MVC razdvaja aplikaciju na tri glavna dijela: **Model**, **View** i **Controller**.

1. Model
	- sloj koji se bavi poslovnom logikom aplikacije i podacima
	- ovdje se obično nalaze klase koje predstavljaju entitete i pristupaju bazi podataka
2. Controller
	- sloj koji upravlja komunikacijom modela i viewa
	- ovdje se obično nalaze PHP skripte koje obrađuju ulazne podatke, a zatim koriste model kako bi dohvatili, ažurirali ili brisali podatke
	- nakon toga controller generira odgovarajući view koji korisniku prikazuje informacije
3. View
	- view se koristi za prikazivanje informacija korisnicima
	- obično se sastoji od HTML-a i CSS-a
	- ovdje se također nalaze predlošsci (templates) koji predstavljaju strukture prikaza (npr. `for` petlja za ispis svih rekorda u bazi podataka)

# Prijenos podataka na produkcijsko okruženje

Implementacija u kontekstu PHP backend developmenta se odnosi na proces u kojem se kod koji je razvijen u fazi razvoja prenosi i postavlja na produkcijsko okruženje (web server).

Proces implementacije uključuje sljedeće korake:
	1. **Postavljanje produkcijskog okruženja**
		- potrebno je postaviti server na kojem će se aplikacija izvoditi i provjeriti jesu li sve potrebne konfiguracije ispunjene 
	2. **Postavljanje koda na server**
		- kod se kopira na server, najčešće putem FTP-a ili nekog drugog sustava za upravljenje datotekama
	3. **Konfiguracija aplikacije**
		- aplikacija se konfigurira za rad na produkcijskom okruženju 
      4. **Konfiguracija aplikacije**
		- aplikacija se konfigurira za rad na produkcijskom okruženju 
	5. **Testiranje**
		- nakon što je aplikacija postavljena na server potrebno ju je temeljito testirati
	6. **Puštanje u rad**
		- nakon uspješnog testiranja aplikacije se pušta u rad i postaje dostupna korisnicima

## Prijenos projekta putem GIT-a

1. Stvorimo račun na GIT hosting platformi: GitHub, Bitbucket, GitLab...
2. Stvorimo novi repozitorij
3. Incijaliziramo GIT repozitorij na lokalnom računalu `git init` 
4. Dodamo datoteke u repozitorij `git add`
5. Napravimo commit s promjenama `git commit`
6. Dodamo udaljeni repozitorij
	1. `git remote add <naziv-repozitorija> <URL-repozitorija>` 
7. Pushamo promjene `git push`
8.  Ostali članovi tima mogu povući najnoviju verziju projekta i nastaviti s radom na projektu


## MySQL migracija

Proces prebacivanja podataka s jedne MySQL baze podataka na drugu

1. Planiranje
	1. planiramo strategiju migracije
		1. identificiramo izvorne i ciljne baze podataka
		2. odlučujemo koje podatke migriramo
		3. testiramo procesa migracije u razvojnom okruženju
2. Izvoz podataka
	1. izvoz podataka iz izvorne baze podataka
		1. koristimo razne alate poput `mysqldump` koji stvara teksutalnu datoteku koja sadrži SQL izjave koje se mogu koristiti za ponovno stvaranje strukture i podataka baze
3. Transformacija podataka
	1. opcionalno, transformacija podataka prije migracije
		1. Konverzija vrste podataka,
		2. promjena kodiranja
		3. filtriranje određenih podataka
4. Uvoz podataka
	1. uvoz u ciljnu bazu podataka pomoću različitih metoda
		1. MySQL-ova ugrađena naredba za naredbeni redak
		2. LOAD DATA INFILE izjava
		3. third party alati poput Navicat, MySQL Workbench...
5. Testiranje
	1. temeljito testiranje nove baze podataka
6. Prebacivanje
	1. prebacivanje baze podataka u "aktivno" stanje, odnosno puštanje u rad

# DNS
	Domain Name System
Omogućuje pretvaranje ljudski čitljivih imena domena u IP adrese.
Funkcionira kao distribuirana baza podataka.
Pomoću njega korisnici pristupaju web stranicama koristeći razumljive nazive domena.

# Hosting

## Shared hosting

Vrsta hostinga u kojoj se više korisnika dijeli na istom fizičkom serveru, te svaki korisnik ima odvojeni dio resursa servera, ali koristi istu IP adresu i isti operativni sustav.

## VPS hosting

Virtual Private Server (VPS) je vrsta hostinga u kojoj se fizički server dijeli na virtualne servere, pri čemu svaki korisnik dobiva svoj odvojeni dio resursa.

## Dedicated hosting

Dedicated hosting je vrsta hostinga u kojoj se korisniku dodjeljuje cijeli fizički server, bez dijeljenja resursa s drugim korisnicima.

## FTP
	File Transfer Protocol
Protokol za prijenos datoteka preko interneta

### Prednosti
Prednosti FTP-a uključuju jednostavnost upotrebe i mogućnost prenosa velikih količina datoteka, kao i mogućnost pregleda i upravljanja datotekama na udaljenom serveru. FTP je također popularan i zbog svoje kompatibilnosti s većinom operativnih sustava.

### Nedostatci
Najveći problem s FTP-om je sigurnost, jer se korisničko ime i lozinka prenose preko mreže bez enkripcije, što znači da su osjetljive informacije poput lozinki vidljive drugim korisnicima na mreži. Alternativa FTP-u su sigurniji protokoli prijenosa datoteka kao što su SFTP (Secure File Transfer Protocol) i FTPS (FTP Secure), koji koriste enkripciju za sigurniji prijenos datoteka.

# Kontinuirana integracija
	Continuous Integration
	CI
Praksa u softverskom razvoju u kojoj se često integriraju promjene u kodu u zajednički repozitorij, a nakon toga se automatski provode testovi kako bi se osiguralo da se novi kod integrira bez poteškoća i ne ometa postojeći kod.

Proces kontinuirane integracije uključuje:
	1. Redovito ažuriranje zajedničkog repozitorija
	2. Automatsko generiranje izvršivih datoteka
	3. Automatsko pokretanje testova
	4. Automatsko slanje obavijesti o rezultatima

## Jenkins
Jenkins je open-source CI alat koji se može koristiti za automatiziranje procesa izgradnje, testiranja i isporuke softvera.

## Travis CI
Travis CI je popularni cloud-based CI alat za open-source projekte koji se izvode na GitHubu. Travis CI ima intuitivno sučelje i integrira se s velikim brojem različitih alata.

## Circle CI
CircleCI je cloud-based CI alat koji se može integrirati s različitim alatima za izgradnju, testiranje i isporuku softvera.

## GitLab CI/CD
GitLab CI/CD je integrirani CI/CD alat koji se koristi za automatiziranje procesa izgradnje, testiranja i
isporuke softvera. GitLab ima podršku za kontejnere, a veliki broj funkcija su dostupni u besplatnoj verziji.

# Kontinuirani razvoj
	Continuous Development
Praksa u softverskom razvoju u kojoj se timovi fokusiraju na kontinuirano isporučivanje softverskih rješenja kroz automatizaciju procesa od planiranja, razvoja, testiranja do isporuke u produkciju.

>[!question]- Objasnite životni ciklus izdanja softvera
>1. **Planiranje:** Definiranje zahtjeva za novom funkcionalnošću
>2. **Razvoj**
>3. **Testiranje**: Testiranje novih funkcionalnosti
>4. **Integracija**: Korištenjem alata poput Jenkins ili GitLab
>5. **Implementacija**: Postavljanje na produkcijski server
>6. **Održavanje** 


