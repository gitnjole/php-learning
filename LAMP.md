# LAMP
## Radno okruženje

Radno okruženje je **skup alata**,
**programa i postavki** koje se koriste
za obavljanje određenog posla ili
zadatka na računalu.

VI editor ima dva načina rada: 
	**naredbeni način**
	**način umetanja**

> [!question]- Koje su prednosti, a koji nedostaci VI editora?
> Prednosti: UNDO, brzina, keyboard-oriented
> Nedostaci: težina učenja 

#### izlazak iz vima
```vim
:q
```

#### zlazak bez spremanja
```vim
:q!
```

#### spremanje i izlazak
```vim
:wq
```

#### ulazak u način rada za ureživanje teksta
```vim
i
```

## Version control

> [!question]- Koja je svrha kontrole verzija?
> Svrha je praćenje promjena u izvnornom kodu kako bi se omogućilo
> lakše upravljanje timom, praćenje promjena i vraćanje na prethodne verzije

### GIT

#### Inicijalizacija novog repozitorija
```bash
git init
```

#### Dodavanje datoteke u staging area
```bash
git add 
```

#### Commit
```bash
git commit -m "Commit message"
```

#### Log
```bash
git log
```

#### Nova grana u gitu
```bash
git branch new-branch
```

#### Prebacivanje u novu granu
```bash
git checkout new-branch
```

#### Slanje promjena na udaljeni repozitorij
```bash
git push 
```

```bash
git push origin -all
```

#### Povlačenje promjena sa udaljenog repozitorija
```bash
git pull
```

#### git ignore

```bash
touch .gitignore
```

	Zatim se u tu datoteku upiše cijeli path datoteke koja se ignoria
	Za cijeli directory se koristi /direktorij

## Apache

Konfiguracija Apache-a se nalazi u direktoriju
```bash
/etc/apache2/httpd.conf
```

>[!info]- Changes in configuration options!
>Per https://help.ubuntu.com/lts/serverguide/httpd.html all configuration options have been moved to subdirectories.
>Example default site 000-default.conf is in
>/etc/apache2/sites-available/000-default.conf

Root web direktorij
```bash
/var/www/html/
```

Start apache
```bash
sudo systemctl start apache2
```

Restart apache
```bash
sudo systemctl restart apache2
```

Stop apache
```bash
sudo systemctl stop apache2
```



## MySQL

### STRUCTURED QUERY LANGUAGE!

Open source relacijski sustav za upravljanje bazama podataka

Start mysql
```bash
start mysqld
```

### Normalizacije
	Norme za postizanje efikasnosti, fleksibilnosti i integriteta podataka

#### 1NF
	Ako tablica nema ponavljajućih nizova i grupa

#### 2NF
	Svaka tablica mora imati primarni ključ, a svi ostali atributi u tablici moraju ovisiti o njemu

#### 3NF
	Svaki atribut koji nije dio primarnog ključa treba ovisi samo o primarnom ključu, a ne drugim atributima

### Naredbe

#### DML naredbe 
	Data manipulation language

SELECT
```SQL
SELECT * FROM customers;
```

INSERT
```SQL
INSERT INTO customers (contact_name, string) VALUES ('Tony', 'gabagool');
```

UPDATE
```SQL
UPDATE customers SET contact_name = 'Tony Soprano' WHERE customer_id = '1';
```

DELETE
```SQL
DELETE FROM customers WHERE customer_id = '1';
```

>[!example]- Kupovina cipela
```SQL
-- CREATE
INSERT INTO shopping_bag (item, price, date) VALUES ('cipele', 100, NOW() );
-- READ
SELECT item, price, date FROM shopping_bag WHERE item = 'cipele';
-- UPDATE
UPDATE shopping_bag SET price = 120 WHERE item = 'cipele';
-- DELETE
DELETE FROM shopping_bag WHERE item = 'cipele';
```


#### DCL naredbe
	Data control language

GRANT
```SQL
GRANT privileges ON object TO user;
```

REVOKE
```SQL
REVOKE privileges ON object TO user;
```

CREATE USER 
```SQL
CREATE USER njole IDENTIFIED BY password123;
```

DROP USER
```SQL
DROP USER njole;
```

ALTER USER 
```SQL
ALTER USER njole WITH NAME antonio;
```

#### DDL naredbe
	Data definition language

CREATE
```SQL
CREATE TABLE persons (  
    person_id int,  
    last_name varchar(255),  
    first_name varchar(255),  
    address varchar(255),  
    city varchar(255)  
);
```

>[!info]+ Data types
>CHAR fiksna duljina
>VARCHAR varijabilna duljina
>INT cijeli brojevi
>FLOAT i DOUBLE decimalni brojevi
>DATE, TIME, DATETIME, TIMESTAMP pohrana vremena i datuma
>TEXT i BLOB velika količina teksta ili binarnih podataka
>BOOLEAN true ili false

ALTER
```SQL
ALTER TABLE persons ADD zip_code INT;
```

DROP
```SQL
DROP TABLE persons;
```

TRUNCATE 
```SQL
TRUNCATE TABLE persons;
```

	Briše podatke, ali ne tablicu

>[!info]+ ALTER, MODIFY, UPDATE
>ALTER radimo promjene na strukturi databaze/tablice (dodavanje, brisanje itd.)
>MODIFY mijenjamo tipkove podataka stupova
>UPDATE mijenjamo postojeće podatke u tablici


### JOIN

#### INNER JOIN
	Vraća samo one retke koji imaju podudaranja u oba tablice koje se spajaju.

#### LEFT JOIN
	Vraća sve retke iz lijeve tablice i pripadajuće podudarajuće retke iz desne tablice.

#### RIGHT JOIN
	Vraća sve retke iz desne tablice i pripadajuće podudarajuće retke iz lijeve tablice.

#### FULL OUTER JOIN
	Vraća sve retke iz obje tablice i pripadajuće podudarajuće retke. Ako ne postoji podudaranje, za tablicu za koju ne postoji podudaranje postavljaju se NULL vrijednosti.

#### CROSS JOIN
	Vraća sve moguće kombinacije između retka iz lijeve tablice i retka iz desne tablice.

### Funkcije

#### Agregatne funkcije

COUNT
```SQL
SELECT COUNT(column_name) FROM table_name;
```

AVG
```SQL
SELECT AVG(column_name) FROM table_name;
```

SUM
```SQL
SELECT SUM(column_name) FROM table_name;
```

MIN / MAX
```SQL
SELECT MIN(column_name) FROM table_name;
SELECT MAX(column_name) FROM table_name;
```

#### Datum i vrijeme

NOW
```SQL
SELECT NOW();
```

TIME
```SQL
SELECT TIME(column_name) FROM table_name;
```

#### String funkcije

CONCAT
```SQL
SELECT CONCAT(column1, ' ', column2) AS concatenated_columns FROM table_name;
```
	CONCAT (stringA, stringB, stringN...) 
	Ako želimo space između stringova dodajemo novi string koji nam služi kao separator
	npr ' '

LENGTH
```SQL
SELECT LENGTH(column_name) FROM table_name;
```

#### Matematičke funkcije

ABS (absolute value)
```SQL
SELECT ABS(column_name) FROM table_name;
```

RAND
```SQL
SELECT RAND() AS random_number;
```

#### Logičke funkcije

IF, IFNULL i NULLIF
```SQL
SELECT column_name, 
       IF(column_name > 10, 'Greater than 10', 'Less than or equal to 10') AS result 
FROM table_name;


SELECT column1, IFNULL(column2, 'Default Value') AS result FROM table_name;


SELECT NULLIF(column1, column2) AS result FROM table_name;
```


### Transkacije

Transakcija se izvodi kao jedna logička cjelina a to znači da se sve radnje izvršavaju ili ne izvršavaju u cijelosti.

U slučaju da se dogodi bilo kakva **pogreška** tijekom transakcije, sve izmjene se **vraćaju na stanje prije početka transakcije**.

START TRANSACTION
	početak
COMMIT
	potvrda svih promjena
ROLLBACK
	poništavanje svih promejna tijekom transakcije i vraćanje na stanje prije početka transakcije
SAVEPOINT
	točka spremanja na koju se može vratiti

>[!example]+ Primjer transakcije
>```SQL
>START TRANSACTION;
>
>INSERT INTO users (name, email, password)
>VALUES ('Ivan Horvat', 'ivan@web.com', SHA('password123'));
>UPDATE account SET account_balance = account_balance - 100 WHERE user_id = 1;
>UPDATE account SET account_balance = account_balance + 100 WHERE user_id = 2;
>
>COMMIT;


### View

MySQL View je virtualna tablica koja se sastoji od upita koji se izvode na jednoj ili više postojećih tablica u bazi podataka.

	Preko pogleda se mogu mijenjati podaci.
	Pogledi se mogu spajati.
	Moguće je napraviti pogled od pogleda.

```SQL
CREATE VIEW DetailsView AS  
SELECT name, address  
FROM student_details  
WHERE student_id < 5;
```

### Index

Indeksi u MySQL-u su posebne strukture koje se koriste za poboljšanje performansi upita.
```SQL
CREATE INDEX ix_broj_kaveza
ON studenti (broj_kaveza)
COMMENT 'Indeks za brže pronalaženje studenata koji često bježe iz učionice(???)';
```

```SQL
ALTER TABLE studenti
DROP INDEX ix_broj_kaveza;
```


### Trigger

Pohranjena procedura koja se automatski izvršava kada se dogodi događaj u bazi podataka.

Okidač se izvršava kod sljedećih događaja.
	• Red je **umetnut** u tablicu.
	• Red je **izbrisan** iz tablice.
	• Redak je **ažuriran** u tablici.

OLD i NEW koriste se za referenciranje vrijednosti stupaca koji se mijenjaju.

Okidači se ne mogu koristiti za izmjenu podataka u istoj tablici u kojoj je okidač definiran.

```SQL
CREATE TRIGGER updateAmount
AFTER INSERT ON customer_order
FOR EACH ROW
BEGIN
	UPDATE product
	SET amount = amount - NEW.amount
	WHERE id = NEW.product_id;
END;
```

	updateAmount -> trigger name	
	customer_order, product -> table
	amount, id -> column 


## PHP

**HYPERTEXT PREPROCESOR**

	IDE
```php
php_info();
```
	
	terminal
```bash
php -i
```
	
	
PHP se obično izvršava na web poslužiteljima, a kôd PHP-a koristi se za generiranje dinamičkih web stranica koje se prikazuju u pregledniku.
### Composer

Alat za upravljanje ovisnostima u PHP-u(?)
Omogućuje programerima da lako dodaju i uklanjaju pakete (biblioteke, alate i sl.) u svoj projekt, zatim automatski riješi ovisnosti između tih paketa.

Da bi se isntalirao mora se pokrenuti lokalno u direktoriju projekta.

```bash
php composer-setup.php

composer --version
```

INIT
```bash
composer init
```
	Inicijalizira prazan JSON dokument za početak rada

INSTALL
```bash
composer install
```
	instalira ovisnosti specificirane u JSONu

REQUIRE
```bash
composer require vendor/package-name
```
	dodaje novi paket u projekt i updatea JSON dokument
	
```bash
composer require vendor/package-name:version
```

UPDATE
```bash
composer update
```

>[!question]- Kako možete instalirati određenu verziju paketa koristeći Composer?
>Pokretanjem naredbe composer require s nazivom paketa i brojem verzije.

> [!question]- Što trebate učiniti da biste instalirati verziju "1.0.0" paketa "vendor/package"?
> 1. Otvorimo terminal/cmd
> 2. Pomaknemo se do direktorija projekta gdje ćemo koristiti paket
> 3. Izvršimo naredbu
> ```bash
> composer require vendor/package:1.0.0
> ```

#### composer.json
	datoteka koja opisuje ovisnosti projekta

U njemu definiramo pakete i njihove verzije koje projekt zahtjeva za rad. Također se mogu navesti i drugi parametri vezani uz instalaciju paketa (npr. putanje do datoteka, skripte koje se izvršavaju nakon instalacije itd.).

#### composer.lock
	generirana datoteka koja sadrži točne verzije svih paketi koji su trenutno instalirani u projektu

Koristi se kako bi se osiguralo da se iste verzije paketa instaliraju i na drugim račualima ili serverima

>[!question]- Razlika između composer.json i composer.lock?
>`composer.json` se koristi za definiranje zavisnosti, dok `composer.lock` "čuva" točne verzije tih zavisnosti

