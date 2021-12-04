---
layout: post
title: REST
author: rafcio
tags: rest api
---

<p>Baza pytań dotycząca RESTa, jakie można usłyszeć</p>

### 1. Co to jest JSON?

JSON jest to  lekki format wymiany danych komputerowych. JSON jest formatem tekstowym, bazującym na podzbiorze języka JavaScript. Typ MIME dla formatu JSON to application/json.

Pomimo nazwy, JSON jest formatem niezależnym od konkretnego języka. Wiele języków programowania obsługuje ten format danych przez dodatkowe pakiety bądź biblioteki. Wśród nich są ActionScript, C, C++, C#, ColdFusion, E, Java, JavaScript, ML, Objective CAML, Perl, PHP, Python, R, REBOL oraz Ruby.

### 2. Co to jest REST?
Representational State Transfer – styl architektury oprogramowania, opierający się o zbiór wcześniej określonych reguł opisujących jak definiowane są zasoby, a także umożliwiających dostęp do nich. Został on zaprezentowany przez Roya Fieldinga w 2000 roku.

### 3. Omów komunikację HTTP klient-serwer

1. Klient preparuje zapytanie w postaci odpowiedniego adresu (endpoint),
2. Klient wysyła przygotowane zapytanie (request),
3. System otrzymuje zapytanie klienta i przygotowuje odpowiedź (response),
4. System zwraca odpowiedź na zapytanie klienta,
5. Klient otrzymuje i przetwarza odpowiedź.


### 4. Jakich typów żądań w REST i do czego służą?
* **GET** – jak samam nazwa mówi służy do pobierania danych. Tutaj wystarczy podać odpowiedni endpoint, ewentualnie zmodyfikować nagłówki (headers) oraz parametry (query params) zapytania. Przykładowe zapytanie możę wyglądać następująco http://example.com/api/resource?per_page=10&page=2. Bardzo częstym przypadkiem użycia metody GET jest weryfikacja czy dany zasób istnieje czy też nie. Jednak moim zdaniem zdecydowanie lepszym pomysłem w tej sytuacji jest skorzystanie z metody HEAD. Główną różnicą pomiędzy tymi metodami jest to, że odpowiedź na zapytanie HEAD zawiera tylko nagłówk, które w opisanym przypadku są wystarczające. Jedyne co tak naprawdę potrzebujemy to kod odpowiedzi, na przykład 200 w przypadku gdy zasób istnieje lub 404 gdy podany zasób nie istnieje.
* **POST** – służy tworzeniu i przesłaniu nowych danych. W tym przypadku konieczne jest już stworzenie ciała (body), w którym przekażemy dane do naszego REST API. W odpowiedzi powinien zostać zwrócony nagłówek HTTP Location z adresem do nowo utworzonego zasobu.
* **PUT** – bardzo podobna do metody POST. Główną cechą odróżniającą PUT jest to, że zapytanie PUT musi wskazywać na konkretny zasób. PUT jest używany głównie do aktualizowania istniejących zasobów. Wartym wspomnienia jest fakt, że PUT nadpisuje cały zasób – dla częściowego nadpisania służy metoda PATCH.
* **DELETE** – metoda służąca do usuwania danych. W tym momencie chcę wspomnieć o technice tak zwanego soft-delete o którym na moim blogu powstał wpis Co nieco o soft delete przy użyciu Node.js i MongoDB. Mówiąc skrótem polega to na tym, że kasując dane za pomocą API tak naprawdę tylko dodajemy do encji informację o tym, że została ona usunięta. W rezultacie dane pozostają nadal w bazie, lecz nie są one dostępne z poziomu API. Mechanizm ten należy już zaimplementować w samym API i nie ma on nic wspólnego z HTTP.

### 5. Jakie są zasady tworzenia API RESTowego?
1. **Odseparowanie interfejsu użytkownika od operacji na serwerze**. Klient poprzez „wydawanie poleceń” nie ma wpływu na to co się dzieje po stronie serwera. Działa to również w drugą stronę – serwer daje klientowi jedynie odpowiedź i nie ma prawa ingerować w UI. Pozwala to na korzystanie z jednego REST API w wielu niezależnych od siebie aplikacjach, a dane pozostaną spójne.
2. **Bezstanowość** – mówi się że REST jest stateless – oznacza to, że każde zapytanie od klienta musi zawierać komplet informacji oraz, że serwer nie przechowuje stanu o sesji użytkownika po swojej stronie. W REST nie istnieją takie pojęcia jak chociażby stany czy sesje.
3. **Cacheability** – odpowiedź, którą użytkownik otrzyma z REST API musi jasno definiować, czy ma ona być cacheable czy non-cacheable. Ma to znaczenie przy danych, które bardzo szybko stają się nieaktualne oraz przy danych, które aktualizują się relatywnie rzadko – nie ma sensu na przykład cache’ować współrzędnych geograficznych pędzącego samolotu, natomiast już jego kolor czy nazwę już tak.
4. **Endpointy**, czyli adresy zasobów, powinny jednoznacznie wskazywać do jakiego zasobu się odwołują. Z ich budowy powinniśmy wiedzieć jaki konkretnie zasób otrzymamy. Co ważne – dane otrzymywane w API powinny być niezależne w żaden sposób od schematu bazy danych w jakiej są przetrzymywane. Oczywiście nie ma przeciwwskazań, aby struktura danych wyglądała identycznie jak schemat bazy danych – niemniej jednak struktura w żaden sposób nie powinna zależeć od tego schematu.
5. **Separacja warstw** – powinniśmy oddzielić warstwy dostępu do danych, logiki biznesowej oraz prezentacji. Żadna z warstw nie powinna bezpośrednio oddziaływać na inne warstwy. Użycie (implementacja) pośrednich i zewnętrznych API powinny być ukryte. Przykładem może być wcześniej wspomniany samolot. Dla przykładu, informacja o kolorze może pochodzić z zupełnie innego API – klient nie musi o tym wiedzieć.
6. Możliwość udostępniania adapterów i skryptów użytkownikom. Jest to opcjonalna reguła, aczkolwiek zdecydowanie warto rozważyć jej zastosowanie. Jeśli wiemy, że klienci będą wykonywać konkretne operacje na konkretnych danych możemy im udostępnić gotowe do tego rozwiązania.

### 6. Co znaczy słowo API?
API – Application Programming Interface – zestaw reguł definiujący komunikację pomiędzy systemami komputerowymi oraz pomiędzy systemem komputerowym a człowiekiem.