---
layout: post
title: C#
author: rafcio
tags: c# language programing
---

<p>Baza pytań dotycząca C# jakie można usłyszeć</p>

### 1. Wyjaśnij różnice pomiędzy klasą a obiektem.
<p>Klasa jest definicją obiektu, a obiekt jest instancją klasy.</p>

<p>Klasa jest szablonem obiektu. Opisuje wszystkie właściwości, metody, stany, zachowania, które obiekt będzie miał. 
Obiekt jest instancją klasy i klasa nie stanie się obiektem, dopóki nie zostanie zainicjalizowana. 
Może być więcej instancji obiektu bazujących na jednej klasie. 
Każda z nich będzie miała jednak inne stany wynikające z różnicy wartości właściwości.</p>

### 2. Wyjaśnij różnice pomiędzy typem wartościowym a typem referencyjnym.
<p>Typ referencyjny przetrzymuje zbiór informacji, który określamy obiektem. 
Natomiast typ wartościowy przetrzymuje jedną wartość.</p>

<p>Typ referencyjny można porównać do całej kartki papieru, 
w której można umieścić wiele danych w zależności od tego, jak wygląda jego klasa. 
Natomiast typ wartościowy w takim wypadku reprezentowałby jedną wartość cyfrową, bitową albo logiczną.</p>

<p>Różnica ta jest widoczna przy przypisywaniu zmiennych</p>

```csharp
int a = 1;
int b = a; //kopiowanie

a = a + 12; //  13
b = b - 12; // -11

Demo d1 = new Demo();
Demo d2 = d1; 
// referencja do tego samego obiektu
```

### 3. Wyjaśnij różnicę pomiędzy pętlą while a pętlą for
<p>Obie pętle są używane do wykonywania bloku kodu, który zostanie wykonany wielokrotnie. 
Pętla for przydaje się wtedy, gdy wiesz ile dokładnie iteracji będzie potrzebne. 
Natomiast pętla while określa ile raz coś ma być wykonane, dopóki pewien warunek jest prawdziwy.</p>

<p>Składnia pętli while.</p>

```csharp
bool boolean = true;
int i = 0;

while (boolean)
{
    if (i >= 9)
        boolean = false;


    Console.WriteLine(i);
    i++;
}
```

<p>Składnia pętli for.</p>

```csharp
for (zmienna ; warunek ; iterator)
{
  // blok kodu
}

for (int i = 0; i < 10; i++)
{
    Console.WriteLine(i);
}
```

### 4. Wyjaśnij wypakowanie i pakowanie wartości tzw. boxing i unboxing
<p>Pakowanie jest to proces, w którym typ wartościowy jest konwertowany na typ obiektowy. 
Wypakowywanie jest to proces pobrania typu wartościowego z obiektu. 
Pakowanie jest niejawne. Natomiast wypakowywanie jest jawne.</p>

```csharp
int i = 21;
object myObj = i;     // boxing 
i = (int)myObj;    // unboxing 
```

### 5. Wyjaśnij różnicę pomiędzy stałą a wartością tylko do odczytu
<p>Stałe i wartości do odczytu posiadają wiele cech wspólnych, natomiast ważne są różnice.</p>

* Stałe są skompilowane do biblioteki. Wartości tylko do odczytu są ustawiane tylko raz przy starcie aplikacji.
* Stałe wspierają tylko typy wartościowe. Wartości tylko do odczytu mogą przetrzymywać referencję do obiektów
* Stałe powinny być używane, gdy ich wartość nigdy się nie zmieni. Wartości tylko do odczytu powinny być używane wtedy, 
gdy chcemy je ustawić raz w trakcie wykonywania programu.

<p>Oto fragment kodu potwierdzający wszystko to, co napisałem</p>

```csharp
public class Demo
{
    public const double Pi = 3.13;

    public readonly Point Point = new Point();

    public readonly int Random = new Random().Next(100);
}
```

### 6. Co to jest LINQ?
<p>LINQ jest to akronim od Language Intergrated Query. Został on przedstawiony w .NET 3.5 i w C# 3.0.</p>

<p>LINQ zawiera zbiór funkcjonalności i składni, która pozwala na tworzenia zapytań do zbiorów danych niezależnie od ich źródła. 
Źródła danych są następujące: bazy dane SQL Server, DataSet ADO.NET, dokumenty XML oraz każda kolekcja, 
która dziedziczy i wspiera interfejsy IEnumerable i IEnumerable&lt;T&gt;.</p>

<p>Dodatkowo dzięki LINQ do C# zostały wprowadzone metody rozszerzeniowe oraz wyrażenia lambda.(To może być osobne pytanie)</p>

### 7. Czym jest Garbage Collector i jak on działa?
Garbage Collection jest to ukryty proces w każdej .NET aplikacji, który automatycznie zarządza pamięcią. Za każdym razem, gdy nowy obiekt zostaje utworzony ten obiekt alokowany w pamięci na stercie.

Tak długo, jak pamięć jest wolna aplikacja może działać. Każdy nowy obiekt zostanie umieszczony w pamięci. Pamięć oczywiście nie jest nieskończona.  Dlatego trzeba coś z pamięci także usuwać.

Garbage Collector sprawdza więc jakie obiekty nie są już używane. Jeśli nie ma zmiennych referujących się do obiektu oznacza to, że nie jest on już potrzebny. Jest on wtedy usuwany z pamięci.

Garbage Collector wtedy zatrzymuje wszystkie wątki znajduje obszar alokacji i kasuje obiekt. Przestrzeń w pamięci może być potem ponownie wykorzystana.

Można wymusić sprzątanie kodu poprzez komendę

System.GC.Collect();

Nie jest to jednak zalecane, ponieważ proces ten zazwyczaj działa jak najlepiej może.


### 8. Co to jest IL, JIT, CLI?
Oto pytanie z kategorii : myślałem, że będą mnie pytać tylko o kod.

IL jest to skompilowany kod przykładowo języka C#. Nie jest to jednak jeszcze ten kod asemblera.  Kod IL zostanie później skompilowany do kodu natywnego maszyny, używając obecnego środowiska innego kompilatora Just-In-Time (JIT).

JIT tłumaczy więc kod IL na kod asemblera. Kod asemblera będzie używany przez procesor.

CLI albo Commmon Language Infrastructure jest to specyfikacja stworzona przez Microsoft. To ten mechanizm zajmuje się tworzeniem i wersjonowaniem bibliotek w systemie Windows.

W .NET mamy typy CLI : proces EXE, oraz biblioteki DLL.  CLI umieszcza więc kod do tych dwóch typów.

Ułóżmy to w sensowną kolejność

Skompilowany kod C# jest kodem IL.
* Kompilator JIT generuje kod maszynowy na podstawie kodu IL
* CLI umieszcza ten kod w odpowiedniej formie
* Potem komputer wykonuje kod na podstawie kodu maszynowego zapisanego jako EXE albo DLL.

### 9. Wyjaśnij czym jest dziedziczenie i jakie ma zalety?
Dziedziczenie jest to jedno z najbardziej popularnych koncepcji w języku obiektowym razem z hermetyzacją oraz polimorfizmem. Dziedziczenie pozwala programistom na tworzenie nowych klas i na ponownym ich używaniu, rozszerzaniu i modyfikowaniu zachowań klas już istniejących.

Co można ponownie użyć: konstruktory, metody i właściwości z klasy pochodnej.

```csahrp
public class Parent
{
    public int MyProperty { get; set; }

    public Parent(int a)
    {
        MyProperty = a;
    }

    public Parent()
    {}
}

public class Child : Parent
{
    public Child() : base(12)
    {}

    public Child(int a) :
        base(a)
    {}
}
```

### 10. Wyjaśnij różnicę pomiędzy Interfejsem a klasą abstrakcyjną?
Interfejs deklaruje kontrakt lub zachowanie, które dana klasa implementująca ten interfejs musi mieć. Interfejs może deklarować tylko właściwości, metody oraz zdarzenia bez modyfikatorów dostępu, ponieważ wszystko będzie publiczne.

Wszystkie elementy z interfejsu muszą być zaimplementowane.

Klasa abstrakcyjna może dać tylko częściową implementację z funkcjonalnością oraz abstrakcyjne metody właściwości, które będą musiały zostać określone w klasie dziedziczącej. Klasa abstrakcyjna i interfejs nie może zostać utworzony.

```csharp
public interface IA
{
   int MyProperty { get; set; }

   void Methdo();
}

public abstract class Aa
{
    public abstract int MyProperty { get; set; }

    //ok
    public  int MyProperty2 { get; set; }

    public abstract void Methdo();

    public void Methdo2()
    { 
        //kod
    }
}
```

### 11. Czym jest delegata?
Delegata w .NET jest podobna do wskaźnika z C lub C++. Używając delegaty pozwalasz programiście przesłać referencję do metody, która będzie przetrzymywana przez obiekt. Obiekt delegaty może być potem przesyłany dalej. Na poziomie kompilacji ani ty, ani kompilator nie musicie wiedzieć jaka metoda zostanie wykonana w tej delegacie.

Więcej o delegatach jest w tym wpisie.

<!--- https://cezarywalenciuk.pl/blog/programing/rozmowa-kwalifikacyjna-sharp1---programista-csharp -->

### 12. Co to jest .NET i .NET Core?
.NET Framework, w skrócie .NET to platforma programistyczna opracowana przez Microsoft, obejmująca środowisko uruchomieniowe (Common Language Runtime – CLR) oraz biblioteki klas dostarczające standardowej funkcjonalności dla aplikacji. Technologia ta nie jest związana z żadnym konkretnym językiem programowania, a programy mogą być pisane w jednym z wielu języków – na przykład C++/CLI, C#, F#, J#, Delphi 8 dla .NET, Visual Basic .NET. Zadaniem platformy .NET Framework jest zarządzanie różnymi elementami systemu: kodem aplikacji, pamięcią i zabezpieczeniami.

W środowisku tym można tworzyć oprogramowanie działające po stronie serwera internetowego (IIS) oraz pracujące na systemach, na które istnieje działająca implementacja tej platformy. Z racji jej pochodzenia najpełniej obsługiwane są systemy z rodziny Microsoft Windows, jednak ponieważ zasadnicza część platformy została zgłoszona jako standard ECMA, powstają także jego niezależne wdrożenia, np. Mono i dotGNU.

Wersja 4.8 jest ostateczną wersją tego frameworka, jednak wciąż będzie otrzymywać poprawki zabezpieczeń i niezawodności. Do tworzenia nowych aplikacji Microsoft zaleca użycie następcy, otwartoźródłowego i wieloplatformowego - .NET

.NET Core to wolne i otwarte oprogramowanie pozwalające tworzyć i uruchamiać wysoce wydajne aplikacje na platformach Windows, Linux, macOS. Framework ten umożliwia programowanie aplikacji przeznaczonych dla chmury obliczeniowej oraz IoT, aplikacji internetowych z użyciem wzorca MVC, bibliotek, aplikacji klasycznych, a nawet rozwiązań opartych na uczeniu maszynowym[6], czy obliczeniach kwantowych. Programy w środowisku .NET mogą być tworzone m.in. przy użyciu języków C#, F#, czy Visual Basic.

### 13. Czym jest C#?
C# jest nowoczesnym, w pełni obiektowym językiem programowania opracowanym przez firmę Microsoft. 
Programy napisane w języku C# są kompilowane do języka pośredniego CIL (Common Intermediate Language), 
który jest wykonywany przez środowisko uruchomieniowe .NET Framework. 
W systemie, w którym takie środowisko nie jest zainstalowane, nie ma możliwości wykonania tak skompilowanego programu. 
Nazwa języka powstała w analogiczny sposób do języka C++. 
Operator używany w języku C, C++ czy C# jakim jest '++' oznacza zwiększenie o jeden. Można zatem powiedzieć, 
że C++ to więcej niż C. W przypadku języka C# wykorzystano podobny pomysł. 
Symbol kratki przypomina połączone ze sobą dwa operatory '++'.

### 14. Czym są tablice 'Jagged Array' w języku C#?
Jagged Array(tj. tablica postrzępiona) to tablica w tablicy. Tablica taka może zostać zainicjowana w poniższy sposób:

`int[][] scores = new int[2][]{new int[]{71,72,73},new int[]{32,33,34,35}};`

Tablica `scores` zawiera w sobie dwie tablice liczb całkowitych. 
Pierwszy element `scores[0]` jest tablicą 3 liczb całkowitych, element drugi `scores[1]` jest tablicą 4 liczb całkowitych.

### 15. Na ile sposobów można przekazać parametry do metody?
* Parametry typu wartościowego(value parameters) - sposób ten pozwala na skopiowane aktualnej wartości argumentu i przekazanie jej w formie parametru do wnętrza metody. W tym przypadku zmiany parametru dokonane wewnątrz funkcji nie wpływają na argument. Oznacza to, iż do metody przekazaliśmy jedynie kopię tej wartości stąd zmiany dokonywane na niej nie mają wpływu na zmianę parametru, który przekazaliśmy do metody;
* Parametry typu referencyjnego(reference parameters) - sposób ten kopiuje odniesienie do parametru w postaci adresu w pamięci do wnętrza funkcji. Oznacza to, iż zmiany wprowadzone wewnątrz tej funkcji będą miały wpływ na wartość argumentu;
* Parametry typu wyjściowego(output parameters) - metoda ta pozwala na zwrócenie więcej niż jednej wartości.

Różnice pomiędzy ref i out :
    
REF:
    
* Przekazanie zmiennej przez adres a nie przez wartość (tak jak out);
* Zmienna przekazana przez ref musi być wcześniej zainicjalizowana.

OUT

* Przekazanie zmiennej przez adres a nie przez wartość (tak jak ref);
* Zmienna przekazana przez out nie musi być wcześniej zainicjalizowana(ale może być).
* Zmienna przekazana przez out musi być za to zainicjalizowana w ciele metody.

### 16. Czy można zwrócić wiele wartości z funkcji w C#?
Tak! W tym celu należy wykorzystać parametry wyjściowe (out). 
Instrukcja `return` pozwala na zwrócenie tylko jednej wartości podczas gdy użycie `out` pozwala na zwrócenie wielu parametrów.

### 17. Czym są przestrzenie nazw (namespace) w C#?
Przestrzenie nazw zostały zaprojektowane po to aby zachować odrębność jednych nazw od drugich. Nazwy klas zadeklarowane w jednej przestrzeni nazw nie są w konflikcie z takimi samymi nazwami klas zdeklarowanymi w innej przestrzeni nazw.

### 18. Jaki jest cel używania słowa kluczowego using w C#?
`Using` pozwala na dodanie przestrzeni nazw do naszego projektu. Na ogół program używa wielu takich instrukcji.
Z drugiej strony pozwala na tzw. „szybkie wykorzystanie obiektu”. Po wyjściu z bloku using obiekt taki zostaje automatycznie usunięty.

### 19. Czym są typy wartościowe w C#?
Typy wartościowe to typy do których wartość może zostać przypisana bezpośrednio. Dziedziczą one z klasy `System.ValueType`.

Typy wartościowe zawierają dane bezpośrednio. Zaliczamy do nich m.in. **int**, **char**, **float**, **double**, **long**, **byte**, **bool** oraz typy wyliczeniowe jak **enum**, **struct**. W momencie deklaracji zmiennych pamięć rezerwuje miejsce na przechowywanie tych danych.

### 20. Czym są typy referencyjne w C#?
Typy referencyjne nie przechowują rzeczywistych wartości a jedynie odniesienia(referencje) do zmiennych.

Do typu referencyjnych zaliczamy elementy rozszerzające klasę `System.Object` oraz `System.String`. Są nimi np. **klasy**, **delegaty**, **interfejsy**, **tablice**, zmienne **string**. Typów takich nie da się kopiować korzystając z operatora przypisania.

Głównym różnicą pomiędzy tymi typami jest to, że w przypadku typów referencyjnych nigdy nie wiemy ile miejsca będzie zajmować klasa. W przypadku typów wartościowych ta wartość jest znana.

Tworząc typy referencyjny kompilator wrzuca na stos referencje, która wskazuje na konkretną lokalizację w pamięci. Obiekt taki może się zmieniać w trakcie działania programu przez co może się również zmieniać jego rozmiar w pamięci. Nad takimi operacjami czuwa `Garbage Collector` który działy w osobnym wątku naszej aplikacji.

### 21. Czym jest boxing w C#?
Boxing jest operacją w której typ wartościowy jest konwertowany na typ obiekt(object).

```csharp
int i = 123;
// Poniższa linijka dokonuje operacji boxing
object o = i;
```

### 22. Czym jest unboxing w C#?
Unboxing jest operacją w której typ obiekt(object) jest konwertowany na typ wartościowy.

```csharp
o = 123;
i = (int)o; // unboxing
```

### 23. Czym są typy dynamiczne w C#?
W typach dynamicznych można przechowywać każdy rodzaj wartości. Typ przechowywanej wartości będzie dopiero sprawdzany w momencie wykonywania aplikacji.

Składnia typów dynamicznych jest następująca:

`dynamic nazwa_zmiennej = value;`

### 24. Jaka jest różnica pomiędzy typami dynamicznymi a wartościowymi?
Typy dynamiczne są podobne do typów wartościowych z tą różnicą, że sprawdzenie typów wartościowych odbywa się w trakcie kompilacji kodu a sprawdzenie typów dynamicznych odbywa się w trakcie wykonywania aplikacji.

### 25. Czym są wskaźniki(pointer) w C#?
Na wstępie warto powiedzieć, że język C# obsługuje wskaźniki ale w ograniczonym zakresie. Wskaźnik jest niczym innym niż zmienna, która przechowuje adres pamięci dla innego typu. Jednakże w języku C# wskaźnik może trzymać adres jedynie dla typów wartościowych i tablic.

Przykład użycia:
`int* ptr;`

Deklarujemy wskaźnik zmiennej ptr która składuje adres dla zmiennej typu int. Operator odniesienia(reference operator) – ‘&’ może być użyty do pobrania adresu w pamięci.

`int x = 100;`

Wyrażenie &x zwraca nam adres pamięci zmiennej x, którą możemy przypisać do zmiennej wskaźnikowej.

`int *ptr = &x;`

Podsumowanie:
```
Console.WriteLine((int)ptr); // Wyświetla adres pamięci
Console.WriteLine(*ptr); // Wyświetla wartość przechowywaną w pamięci
```

Należy również zaznaczyć, że używanie wskaźników w języku C# wymaga użycia tzn. unsafe context. 
Polecenia takie wykonywane są poza kontrolą `Garbage Collector`.

### 26. Co należy wiedzieć o Garbage Collector?
W C# **Garbage Collector** wykonuje mnóstwo czynności za nas. Zajmuje się automatycznym czyszczeniem pamięci przez co można odnieść wrażenie, że w wielu firmach zamiast dążenia do optymalizacji kodu dokłada się po prostu pamięć RAM do serwerów i tyle. Ma to oczywiście swoje plusy, taka aplikacja jest prostsza i czytelniejsza ale za cenę ignorancji w sprawy związane z pamięcią.

GC(Garbage Collector) traktuje wszystkie obiekty jako niepotrzebne o ile nie zostało zaznaczone inaczej. Zakłada, że wszystkie obiekty na stercie są krótkotrwałe. Oznacza to, iż szybciej zostanie usunięty obiekt, który krócej przebywa na stercie niż ten który znajduje się tam dłużej.

**Czym jest zatem sterta?**

Sterta jest częścią pamięci wirtualnej jaka jest przydzielana aplikacji podczas uruchamiania. Sterta jest oddzielna dla każdej uruchamianej aplikacji.
Wszystkie obiekty, które trafiają do pamięci są umieszczane w 2 miejscach na stosie i/lub stercie. Stos z kolei jest o wiele szybszy niż sterta, lądują na niego zmienne oraz parametry przekazywane do funkcji. Jest on czyszczony, gdy kończy się dana metoda. O to dba CLR (Common Language Runtime), czyli środowisko uruchomieniowe dla platformy .NET. Środowisko CLR kompiluje i wykonuje kod zapisany w języku pośrednim (CIL).

Gdyby w .NET nie było GC każdy z nas musiałby sam zajmować się nieużywanymi obiektami i zarządzaniem pamięcią – tak jak ma to miejsce np. w języku C++.
Za każdym wywołaniem GC sprawdza on, które obiekty na stosie mają powiązania z polem klasy, zmienną w metodzie czy globalną zmienną. Po sprawdzeniu stosu, elementy, które mają jakieś referencję są zbierane razem a reszta obiektów jest usuwana z pamięci.

Garbage Collector uruchamia się przynajmniej w 2 momentach. W momencie gdy kończy się pamięć na stercie lub gdy OS zwraca informację o braku pamięci.

### 27. Jaki jest cel używania operatora is w C#?
Operator _is_ jest operatorem rzutowania. Zwraca flagę true jeżeli rzutowanie się powiedzie. Zwraca flagę false jeżeli rzutowanie będzie niepoprawne. Operator ten zwykle znajduje zastosowanie podczas sprawdzania typów w instrukcji warunkowej if

Przykład użycia:

```
int i = 3;
if(i is object) // Sprawdzenie czy 'i' jest objektem(object)- zwraca true
if(i is string) // Sprawdzenie czy 'i' jest zmienną typu string - zwraca false
```

### 28. Jaki jest cel używania operatora as w C#?
Operator _as_ dokonuje rzutowania bez zwracania wyjątku jeżeli rzutowanie się nie powiedzie.

Przykład użycia:

```
int i = 3;
string result = i as string;// Rzutowanie nieudane - result przyjmuje wartość null (nie zwraca wyjątku)
```

### 29. Czym jest enkapsulacja?
Enkapsulacja, inaczej hermetyzacja to termin oznaczający ukrywanie w obiektach tego do czego użytkownik nie powinien mieć dostępu. Idea nowoczesnego programowania obiektowego to idea pisania kodu jak najbardziej zamkniętego. Dzięki takiemu podejściu ograniczamy dostęp do części zmiennych, metod, które są wykonywane wewnątrz konkretnej klasy. Dostęp do tych elementów jest ograniczony „z zewnątrz”.

Aby wykorzystać hermetyzację należy zapoznać się z pojęciem modyfikatorów dostępu. Określają one dostępność do wskazanego elementu w naszym kodzie źródłowym.

Modyfikatory dostępu w C#:
* **Public** – brak ograniczeń. Składowe oznaczone tym słowem kluczowym są dostępne dla wszystkich metod wszystkich klas;
* **Private** – składowe te dostępne są tylko dla metod klas w której się znajdują;
* **Protected** – składowe chronione są dostępne dla klasy, w której się znajdują oraz dla klas dziedziczących w danej bibliotece;
* **Internal** – składowe wewnętrze są dostępne dla klasy znajdującej się w danej bibliotece;
* **Protected Internal** – w języku C# nie ma modyfikatora dostępu, który łączyłby kombinacje słów kluczowych protected lub internal. Klasa, która dziedziczy po tej klasie ma dostęp do tych pól nawet jeżeli znajduje się w innej bibliotece.

### 30. Czym są typy dopuszczające wartości puste (nullable types) C#?
Język C# dostarcza specjalne typy, tzw. typy dopuszczające wartości puste, do których można przypisać nominalny zakres wartości oraz wartości typu null.

Dla przykładu, możemy zapisać dowolną wartość z zakresu -2,147,483,648 – 2,147,483,647 lub wartość null w zmiennej:` Nullable<Int32>`. Podobnie do zmiennej `Nullable<bool>` możemy przypisać flagę true, false lub wartość null.

### 31. Jak używać operatorów ? oraz ?? w języku C#?
Operatory te stosuje się aby skrócić zapis często używanej konstrukcji if (..) then .. else .. .

Przykłady użycia:

`condition ? expression1 : expression2`

Jeżeli warunek jest prawdziwy zostanie zwrócona wartość expression1, w przeciwnym wypadeku wartość expression2.

Użycie kolejnego operatora(??) jeszcze bardziej skróci ten zapis. Operator ten zwróci wartość po swojej lewej stronie wtedy, gdy nie jest ona równa null. W przeciwnym wypadku zwróci wartość po stronie prawej.
Poniżej przykład zastosowania:

```
int CompareNumbers(int a, int b)
{
int? wynik = null;
return wynik ?? -1;
}
```

W przykładzie tym zostanie zwrócona liczba -1 ponieważ wartość po lewej stronie jest null'em.

### 32. Czy w języku C# można utworzyć metodę, która może przyjmować zmienną liczbę parametrów?
Tak, należy użyć słowa kluczowego params. Metoda taka może przyjąć zmienną liczbę parametrów. Liczba parametrów może być również zerowa.

Przykład użycia:
```
int SumParameters(params int[] values)
{
int sum = 0;
foreach (var item in values)
{
sum += item;
}
return sum;
}
```

Oraz przykładowe wywołania metody:
```
int params1 = SumParameters(1, 2, 3, 4);
int params2 = SumParameters(144, 21);
```

### 33. Używając słowa kluczowego params, czy możesz przekazać dodatkowe parametry?
Można, ale należy zwrócić uwagę, iż te parametry muszą wystąpić przed użyciem słowa kluczowego params.

Przykład poprawnego użycia:
```
int SumParameters(string example, params int[] values)
{
int sum = 0;
foreach (var item in values)
{
sum += item;
}
return sum;
}
```

Oraz przykładowe wywołania metody:
```
int params1 = SumParameters("DodatkowyParametr" 1, 2, 3, 4);
int params2 = SumParameters("DodatkowyParametr", 144, 21);
```

### 34. Która klasa jest klasą bazową dla wszystkich tablic (arrays) w języku C#?
Klasa **Array** jest klasą bazową dla wszystkich tablic w języku C#. Jest ona zdefiniowana w przestrzeni nazw **System**. Klasa **Array** dostarcza różne właściwości oraz metody do pracy z tablicami.

### 35. Sortowanie tablic w języku C#.
Należy wykorzystać metodę **Array.sort(array)**. Funkcja ta sortuję elementy jednowymiarowej tablicy używając implementacji **interfejsu ‘IComparable’** dla każdego elementu tablicy. Elementy takie zostaną posortowanie w kolejności rosnącej.
Jeżeli chcemy posortować elementy w kolejności malejącej należy użyć metody **Array.reverse(array)**.

Interfejs **IComparable** umożliwia sortowanie obiektów niestandardowych gdy zostanie zaimplementowany. Kiedy klasa implementuje ten interfejs należy dodać metodę publiczną **CompateTo(T)**. Możemy zaimplementować swoje własne sortowanie dla klasy, która implementuje ten interfejs.

### 36. Czym są struktury w C#?
Struktura w języku C# to wartościowy typ danych(value type). Struktura pozwala na utworzenie pojedynczej zmiennej, która może przechowywać dane różnych typów. Do utworzenia struktury używamy słowa kluczowego **struct**.

Struktury używamy do reprezentacji rekordu.

### 37. Jakie są różnice pomiędzy klasą a strukturą w C#?
Główne różnice pomiędzy klasą a strukturą to:
* klasy są typem referencyjnym a struktury są typem wartościowym;
* struktury nie mogą dziedziczyć po sobie;
* struktury nie mogą mieć domyślnego konstruktora.

### 38. Czym jest typ wyliczeniowy (enum) w języku C#?
Typ wyliczeniowy to zbiór nazwanych, stałych liczb całkowitych. Typ wyliczeniowy jest deklarowany za pomocą słowa kluczowego **enum**.

Jest to wartościowy typ danych. Innymi słowy, jest to typ, który ma własne wartości i nie może on dziedziczyć po innych typach wyliczeniowych.

Typy wyliczeniowe są często używany do opisu obecnego stanu aplikacji:

```
enum ApplicationStatus
{
    Save = 1,
    SaveAs = 2,
    Suspend = 5,
    Delete = 99
}
```

W powyższym przykładzie wartości zostały dodane przez użytkownika. W momencie jeżeli statusy te nie zostaną zdefiniowane zostaną one dodane automatycznie. Pierwszy element w strukturze będzie posiadał wartość 0. W wypadku używania struktur, możemy posługiwać się zarówno zbiorem nazw jak i zdefiniowanym zbiorem liczb całkowitych. Dobrym przykładem może być logowanie do systemu oraz nadawanie uprawnień użytkownikowi. Posiadając zdefiniowany typ wyliczeniowy oraz nadając coraz wyższe numery wyższym prawą dostępu możemy robić proste sprawdzenia za pomocą instrukcji warunkowej if, kto ma dostęp do jakiego modułu.

### 39. Jaki jest domyślny modyfikator dostępu dla klasy?
Domyślny modyfikator dostępu dla klasy to **internal** - składowe wewnętrze są dostępne dla klasy znajdującej się w danej bibliotece.

### 40. Jaki jest domyślny modyfikator dostępu dla składników klasy?
Składniki klasy w C# to elementy, które reprezentują dane oraz zachowanie klasy.
Domyślny modyfikator dostępu to **private** - składowe te dostępne są tylko dla metod klas w której się znajdują.

### 41. Czym jest dziedziczenie w C#?
Dziedziczenie jest kluczowym mechanizmem obiektowości. Pozwala na powielenie funkcjonalność wobec różnych klas dzięki czemu nie musimy ciągle powielać tego samego kodu.

Prostym i często przedstawianym przykładem jest przykład Ssaków, jako dużej kategorii zwierząt, w której też zawiera się człowiek. Wszystkie ssaki mają swoje wspólne cechy, jak np. faza snu czy sposób karmienia. Jednakże każda z tych podgrup ma swoje specjalne cechy.

Kolejny często spotykany przykład to klasa Figury. Prostokąt, trójkąt, mają wspólne cechy, są figurami. Każda z nich ma jednak swoje cechy specjalne. Problem polega na tym, aby ustalić ich cechy wspólne, które zostaną wyodrębnione w postaci klasy bazowej. Nie chcemy dla każdej z tych powtarzać wspólnych cech. Jest to najkrótsze podsumowanie modelowania klas z uwzględnieniem dziedziczenia. Rozbudowa takiej aplikacji jest zdecydowanie prostsza gdyż dodają klasę dla kolejnej figury nie musimy kopiować/powielać wspólnych metod.

Klasa, która dziedziczy posiada wszystkie pola oraz metody klasy bazowej. Pojawia się pytanie, jak te pola są inicjowane i tak działa konstruktor w wypadku dziedziczenia? Wywołanie konstruktora klasy bazowej odbywa się za pomocą słowa kluczowego base, a w nim trzeba podać odpowiednie argumenty. Wywołanie takie będzie możliwe pod warunkiem, że konstruktor w klasie bazowej nie będzie prywatny.

### 42. Czy wielokrotne dziedzicznie klas jest możliwe w C#?
Nie! C# nie obsługuje wielokrotnego dziedziczenia klas.

### 43. Czym jest polimorfizm w C#?
Polimorfizm to jeden z czterech podstawowych założeń dotyczących programowania obiektowego. Mówiąc w największym uproszczeniu to zdolność obiektu do różnych zachowań zależnie od bieżącego wykonania programu.
Metody, które obsługują mechanizm polimorfizmu w C# to metody wirtualne oraz abstrakcyjne.

Warto nadmienić, że polimorfizm dzieli się na:
* statyczny (przeciążanie funkcji i operatorów)
* dynamiczny (funkcje wirtualne i funkcje abstrakcyjne)

Zacznijmy od polimorfizmu statycznego. W danej klasie może istnieć wiele metod o tej samej nazwie, które różnią się tylko liczbą parametrów. Przeciążenie takie jest także nazywane polimorfizmem.
Polimorfizm ten zachodzi podczas kompilacji programu. Nie mamy wpływu na zachowanie takich metod w trakcie wykonywania programu. Metoda, która zostanie użyta została wybrana na etapie kompilacji a jej wybór zależy od ilości parametrów przekazanych do metody.

Wyjaśnimy teraz polimorfizm dynamiczny, tj. przesłanianie funkcji. Aby skorzystać z polimorfizmu dynamicznego musimy utworzyć w danej klasie metodę polimorficzną. Będzie to metoda wirtualna albo metoda abstrakcyjna. Metody polimorficzne przesłania się słowem kluczowym override.

Należy pamiętać, że metoda wirtualna może być przesłonięta w klasie pochodnej – ale nie musi. Jeżeli nie będzie przesłonięta zostanie wywołana metoda klasy bazowej.
W przypadku użycia metody abstrakcyjnej w klasie pochodnej musi ona zostać przesłonięta.

### 44. Czym jest przeciążanie metod w C#?
W danej klasie może znajdować się wiele metod o tej samej nazwie. Ich deklaracja musi się jednak różnić od siebie inną deklaracją typów i/lub ilością argumentów. Warto pamiętać, że nie można przeciążyć deklaracji metody, która różni się jedynie przez zwracany typ.

### 45. Modyfikator dostępu Sealed w C#.
Klasa opatrzona tym modyfikator dostępu mówi, iż klasa ta nie może być dziedziczona. Użycie modyfikatora może być związane z wydajnością. Należy pamietać, że wywoływanie metod wirtualnych jest trochę wolniejsze, gdyż należy sprawdzić, która dokładnie metoda ma zostać wywołana (polimorfizm). Warto również wspomnieć, iż modyfikator sealed może zostać zastosowany również do metod przeciążonych.

### 46. Jak utworzyć klasę abstrakcyjną opatrzoną modyfikatorem Sealed w C#?
Klasa opatrzona tym modyfikator dostępu mówi, iż klasa ta nie może być dziedziczona. Użycie modyfikatora może być związane z wydajnością. Należy pamietać, że wywoływanie metod wirtualnych jest trochę wolniejsze, gdyż należy sprawdzić, która dokładnie metoda ma zostać wywołana(polimorfizm). Warto również wspomnieć, iż modyfikator sealed może zostać zastosowany również do metod przeciążonych.

### 47. Czym są metody wirtualne w języku C#?
Metody wirtualne pozwalają nam na zastosowanie mechanizmu polimorfizmu dynamicznego. W klasie bazowej przygotowujemy metodę wirtualną(może być zaimplementowana lub nie). Następnie w klasach dziedziczących po klasie bazowej możemy przeciążyć tą metodę wymuszając implementację specyficzną dla danej klasy. Jeżeli metoda ta w klasie dziedziczącej nie zostanie przeciążona zostanie użyta domyślna implementacja z klasy bazowej.

### 48. Czym jest interfejs w C#?
Interfejs jest popularnym mechanizmem, który gwarantuje, że dana klasa lub struktura, który po nim dziedziczy obsługuje dane zachowania.
Klasa, która wykorzystuje dany interfejs musi udostępniać wszystkie elementy tego interfejsu. Interfejs nie zawiera żadnego kodu tylko specyfikacje metod i jej właściwości.

Ogólne zasady używania interfejsów:
* nie można dodawać pól, nawet statycznych;
* nie można definiować konstruktora;
* nie można dodawać modyfikatorów dostępu, wszystkie są publiczne
* nie można zagnieżdżać klas, struktur, typów wyliczeniowych i innych interfejsów wewnątrz interfejsu;
* nie można dziedziczyć po klasie. Interfejs może jednak dziedziczyć zachowanie po innym interfejsie. Dziedziczenie po klasie jest niemożliwe ponieważ zawiera ona implementacje kodu a to łamie główną zasadę interfejsów.

### 49. Czym są dyrektywy preprocesora w C#?
Dyrektywy te pozwalają na przekazanie instrukcji do kompilatora przez rozpoczęciem rzeczywistego procesu kompilacji.

Wszystkie dyrektywy rozpoczynają się od znaku #. Nie są ona traktowane jak deklaracje stąd nie muszą się kończyć znakiem średnika(;). Traktowane są jako pomoc przy warunkowej kompilacji.

Przykładowe i popularne dyrektywy:
* \#if, sposób użycia: $IF DEBUG … - możemy np. wyświetlać informacje w konsoli podczas sprawdzania naszego kodu;
* \#region oraz #endregion – pozwala na ukrywanie bloku kodu wraz z nadaniem mu nazwy. Czytelniejszy kod w przypadku wielu linii kodu, np. grupowanie metod;
* \#error – pozwala na wygenerowanie błędu w określonej przez programistę lokalizacji kodu;
* \#define, #undefine – tworzenie zmiennej typu boolean, która może być wykorzystywana w warunkowym sprawdzaniu kodu. #define nazwa_zmiennej określa flagę naszej zmiennej na true, w przypadku użycia dyrektywy #undef nazwa_zmiennej flaga będzie ustawiona na wartość false

### 50. Która klasa jest klasą bazową dla wszystkich wyjątków w C#?
Wyjątki w języku C# są reprezentowane przez klasy. Klasy te przeważnie dziedziczą pośrednio lub bezpośrednio z klasy **System.Exceptions**. Niektóre z klas, które dziedziczą po **System.Exceptions** to **System.ApplicationException** oraz **System.SystemException**.

### 51. Jaka jest różnica pomiędzy klasą System.ApplicationException oraz klasą System.SystemException?
Klasa **System.ApplicationException** obsługuje wyjątki wygenerowane przez aplikację. Stąd, wszystkie wyjątki zdefiniowane przez programistę będą pochodziły z tej klasy.

W przypadku klasy **System.SytemException** jest to klasa bazowa dla wszystkich wcześniej zdefiniowanych wyjątków systemowych.

<!--- https://www.plukasiewicz.net/Pytania_i_odpowiedzi/CSharpQA -->

### 52. Jaka jest różnica między var a dynamic?

**var**:
* dostępne od C\# 3.0
* statyczne typowanie – typ zmiennej deklarowanej jest określany przez kompilator w trakcie **kompilowania** kodu
* zmienna musi być zainicjowana w trakcie deklaracji
* błędy są wyłapywane w trakcie **kompilacji** – kompilator wie jakiego typu jest zmienna, dodatkowo posiada informacje o metodach czy właściwościach dlatego jest w stanie zwrócić błędy w trakcie kompilacji
* Intellisense jest dostępny dla zmiennej zdeklarowanej jako var
* **var** nie może zostać użyty jako parametr zwracany
* nie możemy przypisać wartości null

**dynamic**
* dostępne od C\# 4.0
* dynamiczne typowanie – typ zmiennej deklarowanej jest określany przez kompilator w **trakcie wykonywania**
* zmienna nie musi zainicjowana w trakcie deklaracji
* błędy są wyłapywane w trakcie **wykonywania** – dopiero w trakcie wykonywania kompilator uzyska informacje o rodzaju zadeklarowanej zmiennej dlatego też wszystkie ewentualne błędy będą wyłapywane w trakcie wykonywania programu
* Intellisense jest niedostępny dla zmiennej zdeklarowanej jako dynamic ponieważ jej typ zostanie poznany dopiero w trakcie wykonywania
* dynamic może zostać użyty jako parametr zwracany
* 	wartość null może zostać przypisana

### 53. Jaka jest różnica między typami prostymi a referencyjnymi?
Do typów prostych należą dane liczbowe takie jak: „int”, „float”, itd., a także typy wyliczeniowe oraz struktury („string” to struktura, a więc jest typem prostym). Przypisując do jednej zmiennej prostej jakąś wartość lub wartość z innej zmiennej prostej, tworzy się kopia.  W  przypadku referencji nie powstaje kopia danych, lecz kopiuje się tzw. wskaźnik na dane, czyli wskazanie na jakie dane zmienna wskazuje.

### 54. Jaka jest różnica między metodą wirtualną a abstrakcyjną?
Metoda abstrakcyjna nie ma implementacji i może być zadeklarowana tylko na klasie abstrakcyjnej. Wymusza to na klasie pochodnej dostarczenie implementacji. Metoda wirtualna zapewnia domyślną implementację i może istnieć zarówno w klasie abstrakcyjnej, jak i nieabstraktowej. Tak na przykład:

```
public abstract class myBase
{
    //If you derive from this class you must implement this method. notice we have no method body here either
    public abstract void YouMustImplement();

    //If you derive from this class you can change the behavior but are not required to
    public virtual void YouCanOverride()
    { 
    }
}

public class MyBase
{
   //This will not compile because you cannot have an abstract method in a non-abstract class
    public abstract void YouMustImplement();
}
```

### 55. Jaka jest różnica między lazy loading a eager loading?
**Lazy loading** (leniwe ładowanie) polega na każdorazowym odpytywaniu bazę danych o interesujące nas informacje (jeśli property nawigacyjne jest NULL). Jest domyślnym trybem w Entity.

**Eager loading** (chciwe ładowanie) ogranicza zapytania do bazy kosztem pobrania i przechowywania wszystkich danych z konkretnych tabel w pamięci.

### 56. Jaka jest różnica między ref a out?
Słowa kluczowe - **ref** oraz **out** używane są do przekazywania parametrów do funkcji.
W obu przypadkach parametry przekazywane są jako referencje (adres) a nie wartości.

* **ref** oznacza, że przekazany parametr ma już przypisaną wartość, która może być odczytana bądź zmieniona w wywołanej funkcji
* **out** oznacza, że przekazany parametr nie posiada przypisanej wartości i musi być ona nadana w wywołanej funkcji

**out** często jest używane w przypadku, gdy chcemy żeby funkcja zwracała więcej niż jeden parametr (out jako input nie przyjmuje żadnej wartości).

### 57. Jaka jest różnica między FileStream i MemoryStream?
Stream jest reprezentacją bajtów. Obie te klasy wywodzą się z klasy Stream, która z definicji jest abstrakcyjna.

Jak sama nazwa wskazuje, strumień plików czyta i zapisuje do pliku, podczas gdy strumień pamięci czyta i zapisuje do pamięci. Odnosi się więc do miejsca, w którym strumień jest przechowywany.

Teraz zależy, jak planujesz użyć obu z nich. Dla przykładu: załóżmy, że chcesz odczytać dane binarne z bazy danych, wejdziesz do MemoryStream. Jednak jeśli chcesz przeczytać plik w Twoim systemie, wejdziesz do strumienia plików.

Jedną z szybkich zalet MemoryStream jest to, że nie ma potrzeby tworzenia tymczasowych buforów i plików w aplikacji.