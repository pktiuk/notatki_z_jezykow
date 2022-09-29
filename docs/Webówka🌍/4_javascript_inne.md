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
- wieloparadygmatowy (Obiektowy, Funkcyjny)
- Wszystko jest klasą (za wyjątkiem prymitywów)
- Jednowątkowy

### Asynchroniczność, Wydarzenia(eventy) etc

Ze względu na naturę języka (obsługa GUI oparta na zdarzeniach) oraz braku wsparcia dla wielowątkowości bardzo ważną rolę odgrywa tutaj asynchroniczność.

![Kolejka JS](assets/js_queue.gif)

W [pewnym uproszenieniu](https://stackoverflow.com/questions/67554089/what-is-the-difference-between-callback-queue-and-event-queue) można powiedzieć, że w JS-ie mamy stos na którym wykonywane są funkcje z głównego pliku oraz kolejkę na której znajdują się wydarzenia do obsłużenia.  
W momencie, gdy wszystko co znajdowało się na stosie zostanie wykonane to wtedy na stos "wrzucona" zostanie funkcja z kolejki do wykonania. Z tego powodu czasami może dojść do przyblokowania, eventów, co może mieć nieoczekiwane konsekwencje (np. funkcja z `setTimeout` może się wykonað później niż planowaliśmy)

<details>
  <summary>Przykład</summary>

```js
function fibo(n) {
  return n < 2 ? 1 : fibo(n - 2) + fibo(n - 1);
}

function showMessage(m, u) {
  console.log(m + ": The result is: " + u);
}

console.log("Starting the process...");
// Wait for 10 ms in order to show the message...
setTimeout(function () {
  console.log("M1: My first message...");
}, 10);
// Several seconds are needed in order to
// complete this call: fibo(40)
let j = fibo(40);
// M2 is written before M1 is shown. Why?
showMessage("M2", j);
// M3 is written after M1. Why?
setTimeout(function () {
  showMessage("M3", j);
}, 1);
```

Powyższy kod drukuje:

```
C:\> node turnQueue.js
Starting the process...
M2: The result is: 165580141
M1: My first message...
M3: The result is: 165580141
```


</details>

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
Math.trunc(num); //przycina liczbę co całkowitej
```

### Czas

//TODO
