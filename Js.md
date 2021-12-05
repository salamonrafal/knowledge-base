---
layout: post
title: JavaScript
author: rafcio
tags: javascript js programming 
---
# 

<p>Baza pytań dotycząca JavaScriptu jakie można usłyszeć</p>

### 1. Co to jest scope? Zakres zmiennych w JavaScript

Scope, czyli zakres zmiennych od ECMAScript 6 został dość mocno rozbudowany. Zakres poszczególnych zmiennych jest zależny od sposobu, w jaki zostaną zadeklarowane.

**let**  
Przy pomocy słowa kluczowego let deklarujemy lokalne zmienne w ramach bloku kodu (block scope local variable). Zmienne tego typu zachowują się podobnie jak w innych językach, np. w Javie. Ich zakres jest ograniczony tylko do bloku kodu, w którym zostały zadeklarowane.

```js
function f() {
    if (true) {
        let var1 = 1;
        console.log(typeof var1); // number
    }
    console.log(typeof var1); // undefined
}

f();

console.log(typeof var1); // undefined
```

Wyrażenie typeof var1 w drugim i trzecim przypadku zwróciło undefined, co oznacza, że zmienna w tym miejscu nie jest już widoczna.

**const**  
Słowo kluczowe const służy do deklarowania stałych. Ich zakres jest analogiczny do zmiennych zadeklarowanych przy pomocy let.

Jedyna różnica polega na tym, że raz przypisana do stałej wartość nie może zostać już zmodyfikowana.

Poniższe wywołanie zakończy się błędem:

```js
const const1 = 1;
const1 = 2;
```

**var**  
Zakres tych zmiennych ograniczony jest do funkcji, w której zostały zadeklarowane lub do przestrzeni globalnej, jeżeli były zadeklarowane poza funkcją.

```js
function f() {
    if (true) {
        var var1 = 1;
        console.log(typeof var1);  // number
    }
    
    console.log(typeof var1);  // number
}

f();

console.log(typeof var1);  // undefined
```

**brak modyfikatora**  
Deklaracja zmiennej bez żadnego modyfikatora równoznaczna jest z przypisaniem jej do globalnej przestrzeni.

```js
function f() {
    if (true) {
        var1 = 1;
        console.log(typeof var1);  // number
    }
    
    console.log(typeof var1);  // number
}

f();

console.log(typeof var1);  // number
```

### 2. Czy JavaScript wspiera dziedziczenie? Jeżeli tak, to w jaki sposób?

JavaScript w przeciwieństwie do wielu innych języków, np. Javy nie ma dedykowanego mechanizmu dla klas.

W JS wszystko jest obiektem, nawet funkcje. W efekcie czego można zaimplementować mechanizm dziedziczenia, opierając się na prototypach.

```js
function Base(name) {
    this.name = name;
}

function Child(name) {
    Base.call(this, name);
}

Child.prototype = new Base();

Base.prototype.getName = function () {
    return 'Hello ' + this.name;
}

var base = new Base('Java');
var child = new Child('Java8');

alert(base.getName());
alert(child.getName());
```

Jest to tylko jeden z możliwych sposobów implementacji dziedziczenia w JavaScript oparty o przypisanie obiektu klasy rodzica, do prototypu klasy dziecka.

### 3. Jak rozszerzyć wbudowany obiekt w JavaScript i czemu to zły pomysł?
Wbudowane obiekty można rozszerzyć dzięki mechanizmowi prototypów.

Zróbmy to na przykładzie Stringa.

```js
String.prototype.stormIT = function(){
alert('StormIT');
}
''.stormIT();
```

Wszystkie metody dodane w ten sposób, od tego momentu będą dostępne z poziomu każdego ciągu znaków w aplikacji.

Nie jest to jednak najlepszy sposób, ponieważ biblioteki od różnych dostawców mogą próbować wykorzystać te same nazwy i dojdzie wtedy do konfliktów.

### 4. Jak w JavaScript zrobić tablicę asocjacyjną?

Można to zrobić wykorzystując do tego deklarację obiektu:

```js
var arr = {key1: 'value1'};
alert(arr.key1);
```

### 5. Jaka jest różnica między == i ===?

Podwójny znak równości przed porównaniem danych próbuje je przekonwertować do tego samego typu, a potrójny znak równości porównuje jeszcze dodatkowo zgodność typów.

```js
alert(1 == '1');  // true
alert(1 === '1'); // false
```

### 6. Co to jest hoisting?
Hoisting to wbudowany w JavaScript mechanizm wynoszący wszystkie deklaracje zmiennych na początek funkcji. Najlepiej przedstawić to na przykładzie:

```js
function hoistingExample(){
    console.log(var1); // undefined
    
    if(true){
        var var1 = 1;
    }
    
    console.log(var1); // 1
}
hoistingExample();
```
Mimo iż deklaracja zmiennej jest w instrukcji if, możemy się do niej odwołać już na samym początku funkcji.

Ponieważ wynoszone są tylko deklaracje zmiennych, bez ich inicjowania, pierwsza próba wyświetlenia zmiennej pokaże undefined, a druga już jej konkretną wartość.

Dzięki mechanizmowi hoistingu powyższy kod zostanie zinterpretowany jak poniższy:

```js
function hoistingExample(){
    var var1;
    console.log(var1);
    
    if(true){
        var1 = 1;
    }
    
    console.log(var1);
}
```
Poleganie na hoistingu nie jest jednak najlepszą praktyką. Dużo lepszym wyjściem jest ręczna deklaracja zmiennych na początku funkcji, dzięki czemu kod staje się bardziej czytelny i można uniknąć dziwnych błędów.

### 7. Mechanizm domknięcia polega na zdefiniowaniu jednej funkcji wewnątrz drugiej.

Wewnętrzna funkcja ma dostęp do zmiennych globalnych, swoich zmiennych lokalnych i również do zmiennych rodzica.

```js
var globalVar = 'globalVar';

function parent() {
    var parentVar = 'parentVar';
    
    function closure() {
        var closureVar = 'closureVar';
        
        console.log(globalVar);
        console.log(parentVar);
        console.log(closureVar);
    }
    
    closure();
}

parent();
```

### 8. Co to jest funkcja natychmiastowa (IIFE – Immediately Invoked Function Expression)?
Funkcja natychmiastowa jest wywoływana automatycznie bezpośrednio po jej odczytaniu.

Uzyskujemy ją przez deklarację funkcji anonimowej (bez nazwy) w nawiasach okrągłych, przez co taka konstrukcja jest traktowana jako wyrażenie. Po wyrażeniu dodajemy kolejne dwa nawiasy, przez co jest ono automatycznie wywoływane.

```js
(function () {
    console.log('invoked');
})();
```
Do wyrażenia można również przekazać własne argumenty:

```js
(function (name) {
    console.log(name);
})('Java');
```

### 9. Do czego wykorzystywane są funkcje natychmiastowe?
Dzięki wykorzystaniu funkcji natychmiastowych ograniczamy zakres (scope) zmiennych tylko do tej metody.

Zmniejsza to tym samym potencjalne konflikty z innymi bibliotekami.

### 10. Jak w JavaScript zrobić unikatową przestrzeń nazw dla funkcji?

Można zasymulować mechanizm podobny do pakietów w Javie:

```js
var PL = PL || {};
PL.STORMIT = PL.STORMIT || {};
PL.STORMIT.APPNAME = PL.STORMIT.APPNAME || {};
PL.STORMIT.APPNAME.exampleFunction = function(){
    alert('Hello!');
}
PL.STORMIT.APPNAME.exampleFunction();
```

### 11. Na czym polega Wzorzec Modułu (Revealing Module Pattern)?
Revealing Module Pattern jest to kolejny sposób na uzyskanie unikatowej przestrzeni nazw, polega on na wykorzystaniu funkcji natychmiastowej.

```js
var obj = (function (name) {
    var privateVar = 'StormIT';
    
    var privateMethod = function(){
        return privateVar;
    }
    
    var publicMethod = function(){
        return privateMethod();
    }  
    
    return {
        publicMethod : publicMethod
    };
})();

console.log(obj.publicMethod());
```
Dzięki powyższej konstrukcji udało się uzyskać prywatną zmienną i metodę oraz wystawić API w postaci publicznej metody.

W ten sposób należy wystawiać tylko publiczne metody, a nie zmienne. Podczas zwracania tablicy wynikowej jej zawartość jest kopiowana, przez co zwrócone zmienne nie będą działały zgodnie z oczekiwaniami.

### 12. Jak można zmienić kontekst wywołania funkcji?
Możliwość zmiany kontekstu wywołania funkcji jest dość nietypową operacją, zwłaszcza jeżeli ktoś przez większość czasu programuje w Javie. Chodzi przecież o pobranie metody z jednej klasy i wywołanie jej na obiekcie całkiem innej klasy. W JavaScript jednak wszystko jest możliwe 🙂

Zobaczmy to na przykładzie. Zaczniemy od deklaracji 2 różnych obiektów i jednej metody:

```js
var obj1 = {
    name: 'Java',
    sayHello: function (value) {
        alert(value + this.name);
    }
};
var obj2 = {
    name: 'Java8'
};
obj1.sayHello('function: ');
```
Ponieważ metoda sayHello jest zdefiniowana w obj1, nie ma problemu z jej wywołaniem na tym obiekcie. Jak jednak wywołać tę metodę na obiekcie obj2?

Możemy to zrobić poprzez podmianę wskaźnika this.

**Metoda call**
```js
obj1.sayHello.call(obj2, 'call: ');
```

**Metoda apply**
```js
obj1.sayHello.apply(obj2, ['apply: ']);
```

**Metoda bind**
```js
var binded = obj1.sayHello.bind(obj2, 'bind: ');
binded();
```

### 13. Co to są Obietnice (Promises)?
Obiekty Promise zostały wprowadzone od ECMAScript 6 jako natywne wsparcie dla operacji asynchronicznych. Dzięki nim można niejako odłożyć wykonanie pewnej logiki na bok i zająć się głównym przepływem aplikacji.

Przetwarzanie metody asynchronicznej może zakończyć się powodzeniem – wtedy wywołujemy metodę resolve() lub porażką – wtedy metodę reject();

```js
function asyncOperation() {
    return new Promise(function (resolve, reject) {
        // success
        setTimeout(function(){
            resolve("It's OK");
        }, 1000 + Math.random() * 1000);
        
        // error
        setTimeout(function(){
            reject(Error("Error message"));
        }, 1000 + Math.random() * 1000);
    });
}
```
W powyższym przykładzie przygotowałem metodę zwracającą obiekt Promise. Przyjmuje on jako argument funkcję z dwoma argumentami w postaci wspomnianych wcześniej metod: resolve i reject.

Logika została zaimplementowana w tej sposób, żeby losowo metoda raz kończyła się powodzeniem, a raz porażką. Metoda setTimeout dodatkowo symuluje czas potrzebny na dłuższe wykonywanie obliczeń.

Po definicji metody asynchronicznej możemy ją wywołać:

```js
asyncOperation().then(function(result) {
    console.log(result);
}).catch(function(error) {
    console.log(error);
});

console.log('Next operation');
```
Na obiekcie Promise zwróconym przez metodę możemy wywołać dwie metody:

**then**  
odpowiedzialną za przetwarzanie udanego wywołania;
**catch**  
odpowiedzialną za obsługę błędów.

W przykładzie jest również wywołanie kolejnej metody (Next operation) demonstrujące, że aplikacja nie czeka na wykonanie operacji asynchronicznych, tylko przechodzi bezpośrednio do kolejnych wywołań.

### 14. Co to jest funkcja wywołania zwrotnego (callback) ?
Wykorzystanie mechanizmu funkcji zwrotnych polega na przekazaniu fragmentu logiki (funkcji) jako argument do innej funkcji. Funkcja zwrotna może zostać wywołana lub nie w zależności od konkretnej sytuacji.

Pozwala to na wydzielenie fragmentu wymiennej logiki poza główną funkcję.

```js
function division(a, b, successCallback, errorCallback) {
    if (b == 0) {
        return errorCallback("You can't divide by 0");
    }
    
    return successCallback(a / b);
}
```
W przykładzie zdefiniowałem funkcję dzielącą dwie liczby. Jako argument metoda przyjmuje również dwie funkcje odpowiedzialne za obsługę sukcesu oraz ewentualnego błędu.

```js
var errorCallback = function (error) {
    console.error(error);
};

division(1, 2, function (result) {
    console.log(result);
}, errorCallback);

division(1, 0, function (result) {
    console.log(result);
}, errorCallback);
```

Przekazując metodę zwrotną jako argument, możemy utworzyć nową funkcję inline lub wykorzystać już istniejącą, jak zrobiłem to w przypadku: errorCallback.

### 15. Do czego służy dyrektywa „use strict”?
Dyrektywa use strict pozwala przełączyć silnik JavaScript w strict mode. W efekcie czego parser JS jest dużo bardziej rygorystyczny i zgłosi błędy, które bez tej dyrektywy są ignorowane.

Korzystanie z tego trybu w większości przypadków jest polecane, ponieważ dzięki temu można szybciej wykryć niektóre błędy i napisać lepszy jakościowo kod.

Dyrektywę można dodać na początku funkcji lub całego pliku *.js:

Poniżej przykładowe operacje, które w tym trybie zwrócą błąd:

- wykorzystanie niezadeklarowanej wcześniej zmiennej
```js
'use strict';
var1 = 'Java';
```

- usunięcie zmiennej lub metody
```js
'use strict';
var var1 = 'Java';
delete var1;
```

- powielenie argumentów w metodzie
```js
'use strict';
function f(a, a){
}
```

- zarezerwowano również nowe słowa kluczowe
```js
'use strict';
var private = 1;
```

pozostałe zarezerwowane słowa to: implements, interface, let, package, private, protected, public, static, yield.

### 16. Jak działa timer w JavaScript (Timing Events)?
JavaScript daje możliwość wywołania funkcji z pewnym opóźnieniem.

Do dyspozycji mamie dwie główne metody:

    setTimeout(function, milliseconds)
    setInterval(function, milliseconds)

**setTimeout**  
Metoda setTimeout jako pierwszy argument przyjmuje funkcję zwrotną, która ma zostać wywołana, a jako drugi czas opóźnienia w milisekundach.

```js
setTimeout(function(){
alert('StormIT');
}, 1000);
```

Powyższy przykład wyświetli alert po 1 sekundzie.

**setInterval**  
Metoda setInterval działa podobnie do setTimeout, z tą różnicą, że wykonuje dany kod cyklicznie.

Metoda zwraca identyfikator, który można przechować i wykorzystać do zatrzymania timera przy pomocy metody clearInterval.

```js
var counter = 0;
var timer = setInterval(function () {
    console.log('StormIT ' + counter++);
    
    if (counter >= 3) {
        clearInterval(timer);
    }
}, 1000);
```

Powyższy kod 3 razy wyświetli na konsoli napis i zakończy swoje działanie.

17. Co to jest Arrow functions?
Mechanizm Arrow functions został wprowadzony w celu skrócenia zapisu funkcji anonimowych.

Ogólny wzorzec takiego wywołania wygląda następująco:

`(argument1, argument2, …) => {…}`

Zobaczmy to na przykładach:

```js
function executor(callback) {
    callback();
}

// 1
executor(function () {
    console.log('Normal function');
});

// 2
executor(() => console.log('Arrow function'));

// 3
executor(() => {
    console.log('Multiline');
    console.log('arrow function');
});

// 4
executor((a, b) => {
    console.log('Arguments: ' + a + ', ' + b);
});
```

1. Wywołanie klasycznej funkcji;
2. Proste wywołanie Arrow Function bez argumentów z jedną komendą;
3. Wywołanie Arrow Function z kilkoma komendami w bloku kodu;
4. Wywołanie Arrow Function z przekazaniem argumentów;

