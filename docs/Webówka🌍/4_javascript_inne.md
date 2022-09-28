# Javascript - Inne informacje

## Koncepty webowe

W sieci mamy 3 główne technologie:

- html - odpowiada za zawartość strony, ułożenie elementów etc
- CSS - Styl w którym jest nasza strona
- Javascript - język programowania, który odpowaida za wszystkie "ruchome" rzeczy

## Wersje JSa

- ES5 (ECMAScript 5) wersja wydana w 2009
- ES6 (2015) - największa aktualizacja ever - od tego wydania  
- ES6+ - Od tego momentu kolejne wydania wychodzą co roku i określa się je jako ES6+ (ES2019, ES2020)

JS ma podobne założenia jak java jeśli chodzi o zmiany, czyli NIGDY nie usuwamy starych rzeczy z języka, tylko dodajemy nowe.  
Dzięki temu jest świetna kompatybilność wsteczna .Rzeczy napisane w roku 2009 będą działać dobrz na najnowszych przeglądarkach, ale za to nowe mechanizmy mogą nie być obecne na starszych.  
Do tego używa się narzędzia Babel (transpiluje twój kod do ES5).

## Właściwości języka jako takiego

Cechy opisujące JS-a

- wysokopoziomowy
- posiada garbage collectora
- interpretowany lub just in time compiled
- wieloparadygmatowy (Obiektowe, Funkcyjne)
- Wszystko jest klasą (za wyjątkiem prymitywów)
- Jednowątkowy

### Kolejka Wydarzeń



## Zalecane formatowanie

TODO

## Strict mode

Jest to specjalny tryb pomagający przy developmencie.  
Zapobiega głównie robieniu niektórych operacji oraz wyrzuca więcej errorów.

Aby go aktywować wystarczy dodać linię `'use strict';` na samym początku skryptu.

Przykładowe mechanizmy:

- Łapanie użycia nieistniejących zmiennych. (częste przy literówkach)
- Pilnowanie próby użycia zastrzeżonych słów w złych miejscach (np jako nazwy zmiennych)


Więcej przykładów [tutaj](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode)



## Wczytywanie i wykonywanie skryptu

TODO async, defer 
https://www.udemy.com/course/the-complete-javascript-course/learn/lecture/22649011#overview

## Pomniejsze libki i obiekty wbudowane

### Math

```js
Math.random(); //zwraza liczbę z zakresu 0-1
Math.trunc(num);//przycina liczbę co całkowitej
```

### Czas
//TODO

