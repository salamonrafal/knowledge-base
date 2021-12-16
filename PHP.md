---
layout: post
title: PHP
author: rafcio
tags: php
---

<p>Baza pytań dotycząca PHP, jakie można usłyszeć</p>

### 1. Co to są reguły SOLID? Podaj i scharakteryzuj jedną z nich.

SOLID jest to zbiór ogólnych zasad opisujących pięć podstawowych założeń programowania obiektowego, przestrzeganie tych reguł ma na celu wytwarzanie poprawnego, przejrzystego i łatwo rozszerzalnego kodu, który jest bardziej odporny na błędy i z którym się łatwiej i wydajniej pracuje. Zasady te to:

* [S] Single Responsibility Principle (SRP)
* [O] Open/Closed Principle (OCP)
* [L] Liskov Substitution Principle (LSP)
* [I] Interface Segregation Principle (ISP)
* [D] Dependency Inversion Principle (DIP)

**Single Responsibility Principle** – zasada pojedynczej odpowiedzialności mówi o tym, że klasa powinna mieć tylko jedną odpowiedzialność (nigdy nie powinien istnieć więcej niż jeden powód do modyfikacji klasy). Innymi słowy chodzi o to aby klasa realizowała jedno i tylko jedno zadanie.

### 2. Jakie znasz wzorce projektowe? Krótko scharakteryzuj wybrane dwa.

* Fabryka – Factory
* Singleton
* Adapter
* Fasada – Facade
* Metoda Szablonowa – Template Method
* Strategia – Strategy
* Budowniczy – Builder
* Prototyp – Prototype
* Dekorator – Decorator
* Kompozyt – Composite
* Łańcuch Odpowiedzialności / Zobowiązań – Chain of Responsibility
* Polecenie – Command
* Obserwator – Observer
* Stan – State

**Adapter** – Strukturalny wzorzec projektowy wykorzystywany do połączenia dwóch niekompatybilnych ze sobą interfejsów, tak aby możliwa była współpraca pomiędzy różnymi, nie dostosowanymi do siebie obiektami.  
Wzorzec ten szczególnie wykorzystywany jest gdy chcemy wykorzystać zewnętrzną bibliotekę, której interfejs nie jest dostosowany do naszej aplikacji.

**Fasada** – Strukturalny wzorzec projektowy, którego zadaniem jest dostarczenie ujednoliconego, uproszczonego i uporządkowanego interfejsu programistycznego do złożonego systemu. Innymi słowy wzorzec fasada agreguje elementy złożonego systemu, tworząc większą całość oraz udostępniając łatwy w użyciu interfejs.

### 3. Co to jest Singleton? Przedstaw najważniejsze cechy oraz jak i kiedy się go stosuje?

**Singleton** jest to wzorzec projektowy, nazywany również antywzorcem. Idea tego wzorca jest taka, że dana klasa może mieć wyłącznie jedną instancję. Cechy:

* prywatny konstruktor – tak żeby nie można było utworzyć obiektu z klasy singleton
* prywatna funkcja __clone – tak żeby nie można było utworzyć kopii obiektu
* statyczna metoda, jednorazowo tworząca i zwracająca instancję danej klasy singleton

### 4. Wymień znane Ci ataki i zagrożenia bezpieczeństwa oraz krótko scharakteryzuj zagrożenia i ataki w bezpieczeństwie oraz jak się przed nimi chronić?

* Cross-Site Scripting (XSS)
* SQL Injection
* Cross Site Request Rorgery (XSRF/CSRF)
* Session Hijacking
* Distributed Denial of Service (DDoS)
* Brute Force Attack, Dictionary Attack
* Phishing Attack

**SQL Injection** – atak polegający na wstrzyknięcie obcego kodu SQL do zapytania. Atakujący może zmienić lub usunąć dane w bazie, poprzez wysłanie zapytania z kodem SQL licząc na uruchomienie tego kodu na serwerze. Obrona przed takim atakiem polega na walidacji przychodzących od użytkownika danych oraz „ucieczka” wszystkich parametrów dodawanych do zapytań bazy danych.

### 5. Jakie są metody magiczne w klasie PHP? Wymień kilka i scharakteryzuj.

* __construct(…) – konstruktor, inicjowanie właściwości, ustawianie obiektu podczas tworzenia instancji
* __destruct(void) – destruktor, usuwa obiekt, wywołuje końcowe metody i logikę
* __get($name) – wywołuje się podczas próby pobrania nieistniejącej właściwości
* __set($name, $value) – wywołuje się podczas ustawiania nieistniejącej metody
* __isset($name) – wywołuje się podczas uruchamiania funkcji „isset” lub „empty” dla nieistniejącej właściwości
* __unset($name) – wywołuje się podczas uruchamiania funkcji „unset” dla nieistniejącej właściwości
* __sleep(void) – wywołuje się podczas uruchamiania funkcji „serialize” dla obiektu, pozwala na dodanie logiki serializacji, która będzie zwracała dane do serializacji, w ten sposób możemy zapisać cały obiekt np w bazie danych
* __wakeup(void) – wywołuje się podczas uruchamiania funkcji „unserialize” dla obiektu, pozwala na dodanie logiki która ustawia obiekt podczas odserializowania
* __toString() – metoda wywoływana gdy traktujemy obiekt jak string, metoda pozwala na wywołanie logiki, uruchamianej podczas traktowania obiektu jak zwykły string (np. przy wywołaniu „echo” na rzecz obiektu, ta funkcja zwróci naszą wiadomość)
* __invoke(…) – metoda wywoływana gdy traktujemy obiekt jak funkcję
* __clone() – metoda służąca do kopiowania obiektów, pozwala określić w jaki sposób właściwości obiektów będą sklonowane, umożliwia tzw. „deep cloning” (domyślnie przy użyciu „clone”, właściwości typu prostego są kopiowane, natomiast właściwości jako obiekty są przekazywane jako referncje)
* __set_state($parameters) – wywołuje się podczas użycia metody var_export($obiekt, $parametry)
* __call($name, $arguments) – wywołuje się podczas próby wywołania nieistniającej metody, $name – nazwa metody, $arguments – tablica parametrów
* __callStatic($name, $arguments) – to samo co powyżej ale dla metody statycznej

### 6. Co to jest trait i do czego służy?

Traits to mechanizm pozwalający na ponowne użycie kodu w językach, gdzie dozwolone jest pojedyncze dziedziczenie. Trait pozwala programiście na używanie tych samych metod oraz atrybutów przez kilka różnych klas. Po deklaracji trait-a przy pomocy słowa kluczowego „use” dodajemy kod do wybranej klasy.

### 7. Jak działa sesja i gdzie jest przechowywana?

Protokół HTTP jest protokołem bezstanowym, co oznacza że serwer WWW rozpatruje każde żądanie niezależnie od innych. Istotą działania sesji jest przechowywanie stanu aplikacji pomiędzy niezależnymi zapytaniami HTTP. W momencie pierwszego trafienia na stronę, na której jest zaimplementowana sesja, interpreter tworzy specjalny, losowy oraz unikalny identyfikator przesyłany między żądaniami za pomocą ciastek lub parametru PHPSESSID doklejanego automatycznie do adresów URL. Na podstawie tego identyfikatora odczytywany jest odpowiedni plik lub wpis w bazie z danymi sesji.

### 8.  Co to jest ciasteczko?

Niewielkie informacje zapisywane przez serwisy internetowe na komputerze użytkownika na określony lub nieokreślony czas. Pozwalają na przechowywanie informacji unikalnych dla pojedynczego użytkownika, np. jego preferencje, statystyki i inne.

### 9. Co to jest REST API? Jakie są najważniejsze cechy? Za co odpowiedzialne są poszczególne metody używane przy zapytaniu?

REST – Representational State Transfer – styl architektury oprogramowania opierający się o zbiór wcześniej określonych reguł opisujących jak definiowane są zasoby, a także umożliwiających dostęp do nich.

API – Application Programming Interface – zestaw reguł definiujący komunikację pomiędzy programami komputerowymi.

HTTP – Hypertext Transfer Protocol – bezstanowy protokół wykorzystywany do wysyłania zapytan i otrzymywania odpowiedzi w modelu Host – Server.

GET, POST, PUT i DELETE – metody wykorzystywane w API do pobierania, zapisywania, aktualizacji i usuwania zasobów.

Zasady REST:

* Odseparowanie interfejsu użytkownika od operacji na serwerze
* Bezstanowość
* Cacheability – odpowiedź, którą użytkownik otrzyma z REST API musi jasno definiować, czy ma jest cacheable czy non-cacheable
* Endpointy reprezentujące zasoby
* Separacja warstw

### 10. Co to jerst referencja?

Referencja to swego rodzaju alias dla zmiennej, tzn. że kilka nazw zmiennych wskazują na tą samą wartość w pamięci. W PHP przy tworzeniu referencji korzysta się z znaku ampersand „&”.

### 11.  Co to jest PSR?

**PHP Standard Recommendation** – zbiór dokumentów określających różne standardy używane w języku PHP, np.:

* PSR-1, PSR-2 – standardy dot. kodowania
* PSR-0, PSR-4 – standardy dot. autoloadingu

i inne

### 12. Jakie znasz metody hash-ujące oraz funkcje w PHP?

Algorytmy hash-ujące to np.: MD5, SHA-1, SHA-256, SHA-512, Blowfish, DES, itd.

Funkcje hash-ujące PHP to np.:

* hash(alg, data) – hash-uje dane za pomocą wybranego algorytmu
* md5(data), sha1(data)
* crypt(data, salt)
* password_hash(pass, alg, options) – hash-uje hasło użytkownika, do weryfikacji hashu używamy: password_verify(pass, hash)
* hash_hmac(alg, data, secret_key) – dobra funkcja do podpisywania wysyłanych danych
* mcrypt – biblioteka do hash-owania danych

Inne funkcje:

* hash_algos() – zwraca tablicę zarejestrowanych algorytmów hash-ujących
* hash_equals(known, to_check) – porównuje hashe

### 13. Co to są przestrzenie nazw i do czego służą?

Przestrzeń nazw deklaruje się za pomocą słowa kluczowego „namespace”. Ich najważniejsze funkcje to:

* dzielenie plików projektu w logiczną strukturę
* zapobieganie konfliktom nazewniczym
* wykorzystanie przy autoload-ingu klas

### 14. Do czego służy Composer? Co to są pliki composer.json i composer.lock oraz jaka jest różnica między nimi? Jak zainstalować i jak zaktualizować zależności?

Composer jest to narzędzie służące do instalacji, konfiguracji i zarządzania zależnościami w projekcie PHP.

composer.json:

* opis i metadane projektu
* lista zaleznożci
* autoload
* skrypty do uruchomienia
* pliki do załączenia

composer.lock:

* tworzy się automatycznie przy pierwszej instalacji
* zawiera opis wszystkich zależności
* instalując zależności po raz drugi, composer będzie używał tego pliku po to aby pobrac odpowiednie wersje bubliotek
* innymi słowy, composer.lock jest zabezpieczeniem przed instalacją innych wersji zależności niż te ustalone w projekcie

Polecenia:

instalacja zależności z composer.json lub composer.lock:

```shell
composer install
```

aktualizuja zależności do nowej wersji:

```shell
composer update
```

### 15. Czym się różni silnik bazodanowy InnoDB od MyISAM w bazie MySQL?

Cechy MyISAM:

* blokada podczas operacji: cała tabela
* limit wielkości tabeli: 256 TB
* przeznaczenie: odczyt i zapis
* indeksowanie Full-Text: tak
* transakcje: nie
* pamięć podręczna danych: nie
* pamięć podręczna indeksów tak
* pamięć podręczna zapytań tak

Cechy InnoDB:

* blokada podczas operacji: wiersz
* limit wielkości tabeli: 64 TB
* przeznaczenie: odczyt i modyfikacja
* indeksowanie Full-Text: tak
* transakcje: tak
* pamięć podręczna danych: tak
* pamięć podręczna indeksów: tak
* pamięć podręczna zapytań: tak

### 16. Co to jest Trigger w bazie danych?

Trigger to mechanizm automatycznego uruchamiania zapytań podczas wskazanych operacji w bazie danych (np. podczas aktualizacji lub zapisu danych).

### 17. Co znaczy słowo kluczowe „final” przed klasą?

Final ocznacza że klasę nie można rozszerzać, zapobiega to naspisywaniu funckjonalności klasy.
