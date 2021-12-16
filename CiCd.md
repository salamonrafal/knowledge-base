---
layout: post
title: CI/CD
author: rafcio
tags: continuous integration delivery
---

<p>Baza pytań dotycząca CI/CD jakie można usłyszeć</p>

### 1. Co to jest CI (Continuous Integration)?
raktyka stosowana w trakcie rozwoju oprogramowania, polegająca na częstym, regularnym włączaniu (integracji) bieżących zmian w kodzie do głównego repozytorium i każdorazowej weryfikacji zmian, poprzez zbudowanie projektu (jeśli jest taka potrzeba) oraz wykonanie testów jednostkowych. W praktyce, zaleca się, by każdy członek zespołu programistycznego przynajmniej raz dziennie umieścił wykonaną przez siebie pracę w repozytorium.

Prawidłowo przeprowadzana ciągła integracja powinna prowadzić do:
- zmniejszenia kosztów i ilości pracy niezbędnej do łączenia prac wykonanych przez różne osoby,
- uniknięcia powtórzeń,
- wcześniejszego wykrywania błędów.

Rozpoczynając zmianę, programista pobiera kopię aktualnej bazy kodu, na której ma pracować. Ponieważ inni programiści przesyłają zmieniony kod do repozytorium kodu źródłowego, ta kopia stopniowo przestaje odzwierciedlać kod repozytorium. Można nie tylko zmienić istniejącą bazę kodu, ale można dodać nowy kod, a także nowe biblioteki i inne zasoby, które tworzą zależności i potencjalne konflikty.

### 4.  Co to jest CD (Continuous Delivery)?
Continous Delivery to nic innego jak dostarczanie oprogramowanie w bardzo krótkich cyklach. Nie musi być ono nawet tworzone przez zespoły scrumowe, bo do wykorzystania idei Continuous Delivery wystarczy po prostu iteracyjne wytwarzanie oprogramowania.

Czym są owe iteracje? To powtarzalne czynności, mające na celu zapewnienie odpowiedniej jakości wytwarzanego oprogramowania. Każda jego część musi przejść przez zdefiniowane etapy, podczas których następuje weryfikacja różnymi dostępnymi metodami. W tym także, jeśli zachodzi taka potrzeba, przy pomocy testów manualnych.

Mówiąc o CD nie można nie wspomnieć, że ważnym elementem tego podejścia jest zapewnienie wiarygodności, pełnej transparentności oraz potencjalnej wdrażalności dostarczanego fragmentu oprogramowania.

Tylko regularne tworzenie kompletnych i poprawnych przyrostów może pokazać, że idea Continuous Delivery jest faktycznie obecna w naszej organizacji. Bez spełnienia powyższych warunków nie będziemy w stanie wziąć odpowiedzialności za jakość dostarczanego w cyklach oprogramowania.