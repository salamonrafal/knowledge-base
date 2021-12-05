---
layout: post
title: SQL
author: rafcio
tags: sql database data
---

<p>Baza pytań dotycząca SQLa jakie można usłyszeć</p>

### 1. Co to jest indeks w bazach danych?
Indeks to specjalna struktura danych mająca na celu zwiększenie prędkości wykonywania operacji na tabeli.

Indeks w bazie danych można porównać do spisu treści w książce. Zamiast przeszukiwać całą książkę kartka po kartce, można sprawdzić, na której dokładnie stronie znajduje się dane zagadnienie i przejść bezpośrednio do niego.

```sql
CREATE INDEX UsersAgeIndex ON Users (age);
```

### 2. Jakie są wady i zalety stosowania indeksów?
Ponieważ tworzenie i aktualizacja indeksów wymaga dodatkowych operacji na bazie danych, operacje dodawania (INSERT) i aktualizacji (UPDATE) są wolniejsze. Natomiast operacje pobierania danych (SELECT) mogą być szybsze, jeżeli do ich wykonania zostanie wykorzystany indeks.

### 3. Czy można założyć indeks na kilku kolumnach?
Można, robi się to analogicznie jak dla jednej kolumny.

```sql
CREATE INDEX UsersIdAgeIndex ON Users (id,age);
```

### 4. Jakie znasz funkcje agregujące i co to jest?
SQL udostępnia kilka funkcji agregujących, działających na całej grupie wartości zamiast na pojedynczym polu.

Funkcje tego typu działają na wszystkich wierszach ograniczonych przez klauzulę **WHERE** lub na każdej z podgrup osobno, jeżeli w zapytaniu jest klauzula **GROUP BY**.

- COUNT – ilość wierszy
Funkcja COUNT zlicza ilość wierszy zwróconą przez zapytanie.

```sql
SELECT COUNT(*)
FROM Users
WHERE age > 10
```

Powyższy przykład policzy użytkowników starszych niż 10 lat.

Funkcja może również przyjąć jako argument nazwę pola, np. COUNT(age), jednak wtedy zliczy tylko wiersze, dla których to pole jest różne od NULL.

- SUM – suma wszystkich wartości
Funkcja SUM wylicza sumę wszystkich wartości.

```sql
SELECT SUM(age)
FROM Users
```

Powyższy przykład policzy łączny wiek wszystkich użytkowników. W tym przykładzie widać również, że klauzula WHERE jest opcjonalna.

- AVG – średnia
Funkcja AVG wylicza średnią wartość dla zwróconych rekordów.

```sql
SELECT AVG(age)
FROM Users
GROUP BY city
```

To zapytanie wyliczy średni wiek użytkowników z każdego miasta.

### 5. Jakie są rodzaje złączeń?
Wyróżniamy dwa główne kategorie złączeń: wewnętrzne (inner) oraz zewnętrzne (outer).

  -  **inner join**  
    Jest to domyślny typ złączeń. Wyniki tych zapytań zawierają tylko wiersze, które spełniają warunek złączenia.
    
  -  **outer join**  
    W przypadku tego złączenia wiersze niespełniające wszystkich warunków są również dołączone do wyniku, a brakujące dane są uzupełnione wartościami pustymi (null’ami).



- **INNER JOIN** – wewnętrzne

Wynikiem tego złączenia są tylko wiersze, które spełniają warunek klauzuli złączenia ON.

```sql
SELECT *
FROM Users
INNER JOIN UserGroups
ON Users.group_id = UserGroups.id
```

W zapytaniu słowo INNER jest opcjonalne, ponieważ jest to domyślny typ. W wyniku tego złączenia pojawią się tylko te wiersze z obu tabel, które spełnią warunki wymienione po klauzuli ON.

- **Self JOIN** – własne

Złączenie typu Self JOIN występuje, jeżeli łączymy ze sobą tę samą tabelę. W takiej sytuacji konieczne jest użycie aliasów dla nazwy tabeli.

```sql
SELECT *
FROM UserGroups g1
JOIN UserGroups g2
ON g1.parent = g2.id
```

- **Equi-JOIN**

To bardzo często występująca kategoria złączeń i pasują do niej również powyższe przykłady. Nazywana bywa również równozłączeniem. Zawierają się w niej wszystkie zapytania, dla których w warunku złączenia klauzuli ON oraz WHERE występuje znak równości =.

- **Theta Join**

Złączenie Theta Join (nierównozłączenie) jest przeciwieństwem dla typu Equi-JOIN. Do tej kategorii należą wszystkie złączenia, w których występują porównania, inne niż zwykłe „równa się”, czyli np. **>, != lub BETWEEN.**

- **Anti Join**

Jest to szczególny przypadek Theta Join (nierównozłączenia), w którym wykorzystano operator !=.

- **NATURAL JOIN** – naturalne

Złączenie typu NATURAL JOIN występuje, jeżeli obie kolumny występujące w warunku złączenia mają taką samą nazwę.

```sql
SELECT *
FROM UserGroups
NATURAL JOIN Users
```
W tym wypadku tabele zostały połączone na podstawie pola id, ponieważ tylko ono jest takie same w obu tabelach.

Nie jest to jednak zalecana praktyka, ponieważ w wyniku swojej niejednoznaczności może prowadzić do pomyłek. Poniżej równoznaczne zapytanie z wykorzystaniem klauzuli ON.

```sql
SELECT *
FROM UserGroups g
JOIN Users u ON (u.id = g.id)
```

- **Semi Join** – częściowe

Złączenie częściowe występuje, jeżeli w klauzuli SELECT są wymienione tylko kolumny z jednej tabeli.

```sql

SELECT u.id, u.age
FROM UserGroups g
JOIN Users u ON (u.group_id = g.id)
```

- **CROSS JOIN** – krzyżowe

Złączenie CROSS JOIN (krzyżowe) wykonuje iloczyn kartezjański z łączonych tabel. W efekcie czego łączy każdy wiersz z pierwszej tabeli z każdym wierszem z drugiej.

```sql
SELECT *
FROM UserGroups g
CROSS JOIN Users u
SELECT * FROM UserGroups, Users
```

Powyższe zapytania zwracają ten sam wynik.

- **LEFT OUTER JOIN**

Złączenia typu OUTER pozwalają uwzględnić w końcowym wyniku wiersze, które nie spełniają wszystkich warunków złączenia. W przypadku LEFT OUTER JOIN wiodąca jest pierwsza tabela, a brakujące dane z drugiej tabeli zostaną uzupełnione pustymi wartościami NULL.

```sql
SELECT u.id, u.age, g.name
FROM Users u
LEFT OUTER JOIN UserGroups g ON (u.group_id = g.id)
```

Można w ten sposób uwzględnić opcjonalność danej relacji. Powyższy przykład zwróci wszystkich użytkowników, nawet jeżeli nie będą mieli przypisanej grupy.

Słowo kluczowe OUTER w zapytaniu jest opcjonalne.

- **RIGHT OUTER JOIN**

Złączenia RIGHT i LEFT OUTER JOIN działają bardzo podobnie, ale w przypadku RIGHT w wyniku uwzględnione są wiersze z drugiej tabeli, które nie spełniły warunków złączenia.

```sql
SELECT u.id, u.age, g.name
FROM UserGroups g
RIGHT OUTER JOIN Users u ON (u.group_id = g.id)
```

- **FULL OUTER JOIN**

Jest to złączenie obustronne, które można rozumieć jako sumę złączeń LEFT i RIGHT. W końcowym wyniku uwzględnione są wiersze z obu tabel, również te, które nie spełniły wszystkich warunków złączenia.

```sql
SELECT u.id, u.age, g.name
FROM UserGroups g
FULL OUTER JOIN Users u ON (u.group_id = g.id)
```

### 6. Co to jest bulk insert?

Bulk insert jest to alternatywne podejście do dodawania danych do tabeli po jednym wierszu, mające na celu przyspieszenie procesu.

Najprostszym sposobem na dodanie kilku wierszy jednocześnie jest wykorzystanie metody COPY lub INSERT INTO.

`COPY UserGroups (id, name) FROM stdin;`

| Id               |   Name    |
|------------------|:---------:|
| 1                |   Admin   |
| 2                |   User    |


`INSERT INTO UserGroups (id, name) VALUES (1, 'Admin'), (2, 'User');`

### 7. Co to jest trigger na bazie danych?
**Trigger**, czyli wyzwalacz to procedura wykonywana automatycznie przez bazę danych jako reakcja na pewne zdarzenie, np. dodanie (INSERT), aktualizację (UPDATE) lub usunięcie (DELETE) danych.

Triggery nie przyjmują żadnych argumentów oraz nie mogą zatwierdzać (COMMIT) i anulować (ROLLBACK) transakcji, ponieważ są wywoływane automatycznie w kontekście danej operacji (instrukcji SQL).

### 8. Co to jest transakcja?
**Transakcja** jest to zbiór operacji wykonywanych na bazie danych, które stanowią jedną spójną całość. Dlatego operacje zawarte w jednej transakcji powinny być wykonane wszystkie lub żadna z nich.

Przykładem operacji wykonywanych w ramach jednej transakcji jest przelew bankowy. Podczas wykonywania jednej transakcji pieniądze są pobierane z jednego konta i przekazywane na drugie. W przypadku niepowodzenia obie operacje muszą zostać wycofane.