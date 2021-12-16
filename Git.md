---
layout: post
title: GIT
author: rafcio
tags: git vcs version control system
---

<p>Baza pytań dotycząca GITa jakie można usłyszeć</p>


### 1. Czy GitHub to Git? Co to jest Bitbucket ?
Git jest rozproszonym systemem kontroli wersji, w którym rozwijany kod źródłowy znajduje się w repozytoriach. GitHub, czy Bitbucket to serwisy internetowe, dzięki którym ich użytkownicy mogą współdzielić między sobą repozytoria. Są też inne serwisy spełniające podobną rolę, np. GitLab. Można główne repozytorium przechowywać na dowolnym serwerze, albo nawet na koncie Dropbox

### 2. Jak utworzyć repozytorium?
Wystarczy $git init w folderze, który ma zostać repozytorium.

### 3. Jak sprawdzić stan repozytorium?
Żeby sprawdzić bieżące zmiany w repozytorium należy wykonać komendę **$git status.**

Żeby sprawdzić poprzednie commits należy wykonać **$git log.**

### 4. Co to jest HEAD, origin, master?
**HEAD** to wskaźnik pokazujący na aktualną gałąź (branch) w repozytorium. Jeżeli aktualna gałąź to master, to HEAD wskazuje na gałąź o nazwie master, jeżeli zmienimy gałąź na development  to HEAD wskazywać będzie na development.

**master** to nazwa gałęzi, która tworzona jest domyślnie po utworzeniu repozytorium. Nie ma szczególnego znaczenia, można ją usunąć i pracować na innej gałęzi.

**origin** to nazwa zdalnego repozytorium. Jeżeli klonujemy repozytorium za pomocą komendy $git clone, domyślnie zdalne repozytorium będzie widoczne pod nazwą origin. Tak jak w przypadku nazwy master, nie ma to szczególnego znaczenia. Można usunąć zdalne repozytorium o nazwie origin i skonfigurować to samo repozytorium pod inną nazwą.

Zatem jeżeli wywołujemy komendę $git push origin master to znaczy, że do zdalnego repozytorium o nazwie origin wysyłamy commits z gałęzi master. Należy jednak pamiętać że master i origin to tylko nazwy. Zwracam na to szczególną uwagę, dlatego, że zrozumienie tego sprawiło mi szczególną trudność.

### 5. Co to jest branch?
Każde repozytorium ma przynajmniej jedną gałąź, domyślnie nazywaną master. Utworzenie nowej gałęzi oznacza, że kod dostępny w gałęzi od której nastąpiło odgałęziene jest teraz dostępny w nowej gałęzi.

### 6. Czym się różni git pull od git fetch?
`$git pull` i `$git fetch` służą do pobrania zmian ze zdalnego repozytorium. $git fetch tylko uaktualnia gałąź wskazującą na zdalne repozytorium (domyślnie origin), natomiast $git pull, dodatkowo wykonuje operację $git merge na skutek czego, aktualna lokalna gałąź synchronizuje się dodatkowo z gałęzią wksazującą na zdalne repozytorium. Oznacza to, że jeśli sklonujemy repozytorium (z serwisu Bitbucket, czy GitHub) i do tego repozytorium zdalnie wprowadzone zostaną zmiany, to żeby gałąź wskazująca na to repozytorium była zsynchronizowana ze zdalnym repozytorium, należy wykonać właśnie komendę $git fetch. Jednak na skutek takiej akcji, pliki w lokalnej gałęzi się nie zmienią. Żeby się zmieniły należy wykonać jeszcze $git merge origin (jeśli gałąź śledząca zdalne zmiany nazywa się origin).