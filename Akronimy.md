---
layout: post
title: Dobre praktyki programowania
author: rafcio
tags: rest api
---
# Akronimy

<p>Baza pytań dotycząca akronimów jakie można usłyszeć</p>

### 1. Co to jest S.O.L.I.D.?

S.O.L.I.D to zbiór zasad opisujący podstawowe założenia programowania obiektowego.

Zasady solid składają się z 5 założeń:
* Single Responsibility Principle - zasada jednej odpowiedzialności,
* Open-Close Principle - zasada otwarte-zamknięte,
* Liskov Substitution Principle - zasada podstawienia Liskov,
* Interface Segregation Principle - zasada separacji interfejsów,
* Dependency Inversion Principle - zasada odwrócenia zależności.

### 2. Co to jest GRASP?
GRASP to zbiór 9 zasad określających, jaką odpowiedzialność powinno się przypisywać określonym obiektom i klasom w systemie. Każda zasada wyjaśnia inny problem dotyczący ustalania odpowiedzialności obiektu.

Struktura GRASP:
* Creator – kiedy obiekt powinien tworzyć inny obiekt?
* Information Expert - jak ustalać zakres odpowiedzialności obiektu?
* Controller – jak część systemu odpowiedzialna za logikę biznesową programu powinna komunikować się z interfejsem użytkownika?
* Low Coupling – jak ograniczyć zakres zmian w systemie w momencie zmiany fragmentu systemu?
* High Cohesion – jak ograniczać zakres odpowiedzialności obiektu?
* Polymorphism – co zrobić, gdy odpowiedzialność różni się w zależności od typu?
* Pure Fabrication – komu delegować zadania, gdy nie można zidentyfikować do kogo należy podany zbiór operacji?
* Indirection – jak zorganizować komunikację między obiektami, aby mocno ich nie wiązać?
* Protected Variations – jak przypisywać odpowiedzialność, aby zmiana w jednej części systemu nie powodowała niestabilności innych elementów?

### 3. Co to jest DRY?
Nie powtarzaj się to wzorzec, który mówi, że należy unikać powtarzania tych samych części kodu w różnych miejscach. Pozwala to na uniknięcie kopiowania lub kopiowania i delikatnego zmieniania części kodu w inne miejsca. Główną zaletą DRY (Don't repeat yourself) jest uniknięcie błędów popełnianych w trakcie kopiowania powtarzających się fragmentów kodu. Pozwala to zaoszczędzić czas, który tracimy, aby wprowadzić mało znaczące zmiany do kopiowanego kodu a następnie czas, który tracimy na szukanie zmian, które przeoczyliśmy w trakcie kopiowania. W zasadzie DRY chodzi również o unikanie powtórzeń czynności, które są wykonywane przez programistów. Takie czynności powinny być robione poprzez generatory kodu lub skrypt automatyzujące pracę.

### 4. Co to jest KISS?
Keep It Simple, Stupid (czyli tłumacząc: nie komplikuj, głupku) jest to reguła mówiąca, że nie należy na siłę komplikować prostych rzeczy, aby przykładowo wykorzystać niepotrzebne w danym momencie wzorce projektowe. Nie należy szukać rozwiązania dłużej niż możesz na tym zaoszczędzić. Do czasu pracy należy doliczyć czas spędzony na szukaniu lepszego rozwiązania i porównać z przewidywanym czasem poświeconym na rozwiązanie danego problemu w tradycyjny najprostszy sposób.

### 5. Co to jest ROT?
Zasada KISS jest ściśle powiązana z zasadą DRY. W niektórych sytuacjach łatwiej jest przekopiować kilka linijek niż stosować regułę DRY. Dlatego została wymyślona kolejna zasada ROT (Rule of Three). Zasada ta mówi, że jeśli istnieją 3 kopie tego samego kodu należy zastosować regułę DRY i połączyć kod. Pozwala to uchronić program przed wprowadzaniem zmian w 3 miejscach, co może spowodować duża ilość nowych problemów.

### 6. Co to jest SoC?
Separacja zagadnień polega na podziale programu na odrębne moduły, które pokrywają się funkcjonalnością tak mało jak to tylko możliwe. Taką budowę programu nazywamy modułową. Każdy element systemu powinien mieć swoje rozłączne i osobliwe zastosowanie. Celem SoC (Separation of Concern) jest stworzenie systemu, w którym każda część pełni znaczącą role przy zachowaniu możliwości maksymalnej adaptacji do zmian. SoC nie odnosi się tylko do architektury systemu, ale do różnych zagadnień np. do podziału aplikacji na warstwy (prezentacji, logiki biznesowej, dostępu do danych, bazy danych).

### 7. Jaka jest różnica między SoC (Separation of Concern) a SRP (Single Responsibility Principle)?
Separacja zagadnień (SoC) i zasada pojedynczej odpowiedzialności (SRP) wydają sie bardzo podobne jednak są pomiędzy nimi pewne różnice. SRP każe oddzielać każdą funkcjonalność do osobnej klasy, która ma się zajmować tylko jedną rzeczą, natomiast SoC każe dzielić zagadnienie (nie koniecznie program) na moduły, które w jak najmniejszym stopniu pokrywają się funkcjonalnością. W pewnych sytuacjach SoC kłóci się z SRP, należy wtedy wybrać odpowiednie rozwiązanie w zależności od rodzaju problemu. W żadnym przypadku nie istnieje idealne rozwiązanie, dlatego należy wybrać rozwiązanie najlepsze z dostępnych.

### 8. Co to jest YAGNI?
Zasada YAGNI (ang. You Ain't Gonna Need It) "Nie będziesz tego potrzebował" mówi, że nie należy pisać oprogramowania, które nie jest potrzebne, ale wydaje się, że może się kiedyś przydać. Nie należy patrzeć zbyt daleko w przyszłość, ponieważ po pewnym czasie może się okazać, że tracimy czas na coś, co się nie przyda. W trakcie rozwoju projektu praktycznie zawsze zmieniają sie założenia, co powoduje, że wcześniejsze koncepcje należy zweryfikować lub całkowicie odrzucić.

### 9. Co to jest MoSCoW?

MoSCoW (M – Must have it, S – Should have it, C – Could have if not affecting other things, W – Won’t have this time) jest to metoda, która zaleca podział wymagań klienta na kilka podgrup:
* te, które musi mieć (M),
* te, które powinien mieć (S),
* te, które może mieć, jeżeli nie zaszkodzą tworzeniu gotowych funkcjonalności (C),
* te, których nie uda się zaimplementować w danym terminie (W).

W nazwie MoSCoW litery 'o' zostały dodane, aby było łatwiej wymówić nazwę. A przestrzegać zasady YAGNI dobrą praktyką jest, wykorzystanie metody MoSCoW dla uporządkowania priorytetów zadań.