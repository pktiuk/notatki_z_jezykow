# Javascript Syntax

## Osadzanie skryptu w HTML-u

W HTML-u skrypty umieszczane są wwenątrz tagów `script`.  
W praktyce skrypty można tak pisać, ale nie jest to wygodne, dlatego używa się osadzania skryptów.

```html
<script src="plik_ze_sryptem.js"></script>

<script>
  ////Tutaj skrypty
</script>
```

## Zmienne

!!! warning
Zmienne nie mogą zaczynać się od liczb, ani nazywać się jak słowa kluczowe w JS (`new` `function` `class` etc)

```js
/* let 3liczba = 43; */
/* let function = 3; */
let $function = 43; // ale za to $ jest dozwolony jako znak
```

### Typy zmiennych

Warto pamiętać, że JS ma dynamiczne typowanie, czyli nie musimy definiować typów zmiennych, ponieważ to jest sprawdzane dynamicznie w trakcie pracy.  
Poza tym możemy nadpisywać zmienne innymi typami.

```js
let mojaZmienna = 43;
mojaZmienna = "teraz slowo";
```

Zalecane formatowanie dla zmiennych to `camelCase`.

#### Podstawowe

```js
//Number - zawsze zmiennoprzecinkowa (także dla całkowitych)
let wiek = 22;

//String - wartpamiętać, że można je definiować na 3 sposoby "", '' i ``
let imie = "Marian";

// Boolean
let isTrue = true;

//Undefined
let jeszczeNieOkreslone;

// Null
let nic = null;

// Symbol (ES2015) - unikatowa wartość, której nie można zmienić
```

Dla sprawdzania typów ożywamy operatora `typeof`

```js
let zmienna = 54;
console.log(typeof zmienna);
//>number
typeof "Slowo";
//>"string"
let nieWiadomo;
console.log(typeof nieWiadomo);
//>undefined
```

Warto zwrócić uwagę na to co daje tutaj `null`. (Jest to wyjątek z którym trzeba się pogodzić)

```js
console.log(typeof null);
//>object
```

#### Tablice (arrays)

Są to kontenery w których trzymamy zmienne i obiekty

```js
const liczby = [22, 33, 45];
const slowa = new Array("slowo1", "slowo2");

console.log(liczby[0]);
// 22

// mamy tu zbliżone odliczanie do pythonowego
console.log(liczby[-1]);
// 45

// co ciekawe mimo inicjalizacji jako const możemy zmieniać wartości w tablicy
liczby[1] = 32;
//Ale nie możemy usunąć samej tablicy
```

Tablice mogą zawierać różne wartości w kolejnych komórkach

```js
let osoba = ["Marian", "Kowalski", 22, ["Burek", "Kulka"]];
```

Operacje na tablicach

```js
let tablica = [];

// rozmiar tablicy
tablica.length;
// 0

tablica.push(10); //teraz tablica zawiera 10
// 1 - zwraca ona nową długośż naszej tablicy

tablica.unshift(0); //tobi to samo co pop, tylko dodaje na początek

tablica.pop(); //a po tej operacji jest znowu pusta
// 10 - zwraca wartość z końca tablicy

const inna = ["pierwszy", "drugi", "trzeci"];
inna.indexOf("pierwszy");
// 0

inna.includes("trzeci");
// true
```

**Iterowanie po tablicach**

```js
const lista = ["a", "b", "c"];
for (const [num, elem] of lista.entries()) {
  console.log(`Indeks: ${num} Zawartosc: ${elem}`);
}
```

**Rozmontowywanie tablic**

```js
// tworzymy trzy zmienne (x, y, z), które bęzą zawierać poszczególne elementy
const [x, y, z] = [1, 2, 3];
const [, dwa, , cztery] = [1, 2, 3, 4, 5]; //nie musimy brać wszystkich elementów z danej tablicy
```

Możemy też w ten sposób definiować zmienne domyślne (jeśli w tablicy nie ma danego elementu do domyślnie jest Undefined)

```js
const [x = 1, , z = 3] = [0, 1];
```

Ten mechanizm pozwala na łatwe zwracanie wielu elementów z funkcji, podobnie do krotek z pythona.

#### Sposoby definiowania

Jest kilka sposobów na definiowanie zmiennych. Służą do tego słowa kluczowe `let`, `var` i `const`.

**let** - definiowanie zwykłej zmienej wartości, za jego pomocą można też definiować puste zmienne.

```js
let num = 30;
num = 32;

let undef;
```

**var** - podobne do let lecz jest już przestarzałe i nie zaleca się jego używania.

**const** - po prostu stałe zmienne

```js
const PI = 3.14;
// PI = 1; - spowoduje TypeError

// const unknown; - to też nie zadziała (SyntaxError)
```

Teoretycznie można pracować nawet bez definiowania zmiennych wg wymienionych wyżej sposobów.

```js
imie = "Jan";
console.log(imie);
// Jan
```

Tylko, że ta zmienna będzie wtedy odpowiednikiem zmiennej globalnej.

#### Operatory

Typy operatorów:

- Matematyczne: `+` `-` `*` `/` `**` (potęgowanie)
- Przypisywania: `=` `+=` `*=` `-=` `++` `--` etc
- Boolowskie
  - porównania: `>` `>=` `<` `<=` `==` `!=` `===`
  - logiczne `&&` `||` `!`
- trójargumentowy `? :`

Kolejność operatorów jest taka jak w matematyce.

##### Operator `==` i `===`

Istnieją dwa operatory równości:

- `===` - ścisły - zwraca prawdę tylko i wyłącznie wtedy, gdy obie strony są takie same, nie bawi się w żadne konwersje etc.
- `==` - jest nieco luźniejszy, pozwala sobie na konwersje pomiędzy typami jeśli wartości są różnych typów, poza tym ma inne "pomagające" mechanizmy, które w dłuższej prespektywie mogą powodować więcej błędów. (jeśli się da używaj `===`)

```js
19 === "19";
// false

19 == "19";
// true
```

Podobnie do `===` działa `!==`

#### Konwersja

Aby dokonać konwersji trzeba po prostu użyć konstruktora danego typu.

```js
const rokStr = "2001";
Number(rokStr);
//>2001

String(55);
//>"55"
```

Tutaj w wypadku podania niewłaściwej wartości zamiast wyjątku dla liczby możemy dostać `NaN` (Not a Number)

```js
let a = Number("ff2");
a;
//>NaN

typeof a; // Co ciekawe ten typ jest wciąż numerem
("number");
```

Poza tym warto uważać na sprytną konwersję typów np przy printowaniu.  
Na ogół działa to fajnie, ale operator `+` może trochę napsuć i być źródłem wielu błędów.

```js
"22" + 10;
// 2210

"22" - 10;
// 12

"22" - "10";
// 12

"22" - "10" + 55;
// 67

"22" - "10" + "55";
// 1255
```

**Konwersja na Boola** - wartości, które przy konewrsji na boola dają `false`:

- 0 - wartość liczbowa równa zero
- ""
- `undefined`
- `null`
- `NaN`

Pozostałe konwertują się na wartość `true`

#### Praca ze stringami

Mamy tutaj standardowe metody do pracy z ciągami znaków, podobne nieco do tych pythonowych.

Mamy:

- `split(separator=" ")`
- `replace(co,na_co)`, `replaceAll(co,na_co)`

```js
let slowo = "";
```

### Printowanie

```js
console.log("Wiadomosc1", 323);
//> Wiadomosc1 323

// aby wypisać wiadomośc można klasycznie połączyć stringi
const wiek = 10;
const wiadomosc = "Hej, mam " + wiek + "lat";
console.log(wiadomosc);

// Ale można to zrobić wygodniej warto pamiętać, że robimy to w ``, a nie w ''
const wiadomosc2 = `Hej, mam ${wiek} lat`;
console.log(wiadomosc2);
```

Ogólnie to obecnie ten drugi sposób definiowania jest wygodniejszy

```js
console.log(
  "Wiele\n\
linii w kodzie"
);

//VS

console.log(`Wiele
linii w kodzie`);
```

## IF-y i warunki

Syntax warunków jest zbliżony do C++

```js
const wiek = prompt("podaj wiek"); //pojawi się okno z pytaniem

if (wiek >= 18) {
  console.log("Pełnoletni");
} else {
  console.log("Niepełnoletni");
}

if (true) console.log("Nie");
else console.log("Tak");

if (true) console.log("True to prawda");
```

Mamy też tu switcha

```js
switch (key) {
  case value:
    fun1();
    fun2();
    break;

  case value2:
  case value3: // dla tych dwóch wartości będzie się dziać to samo
    fun3();
    break;

  default:
    break;
}
```

Jest też operator trójargumentowy `? :`

```js
wiek >= 18 ? console.log("Dorosły") : log.console("Nie Dorosły");
// Albo
console.log(wiek >= 18 ? "Dorosły" : "Nie Dorosły");
```

## Pętle

Nic ciekawego mamy 2 zwykłe typy pętli, `for` i `while`.

```js
for (let num = 0; num < 10; num++) {
  if (num === 5) continue; //ale skipujemy dla 5
  console.log(`Printujemy po raz ${num + 1}`);
}

while (true) {
  //nigdy nie kończąca się pętla
  break; //no chyba, że użyję break
}
```

Poza tym mamy jeszcze forEach w dwóch wariantach.

```js
const tablica = [0, 11, 22, 33, 44];

for (const i of tablica) {
  console.log(i);
}

// Metoda forEach
tablica.forEach(function (i) {
  console.log(i);
});
```

## Funkcje

Definiujemy je używając słowa kluczowego `function`.  
Także są na ogół formatowane jako `camelCase`.

!!! warning
Niestety JS **nie wspiera** przeciążania funkcji.

Poniżej zwykłe deklaracje funkcji (function declaration).

```js
function printHello() {
  console.log("Hello");
}

printHello();
// Hello

function isApple(fruit) {
  if (fruit == "apple") return true;
  else return false;
}
```

### Argumenty funkcji

Funckcję mającą `n` argumentów możemy wywołać używając:

- `n` argumentów

```js
printHello(23);
// Hello
```

- więcej niż `n` argumentów - nieoczekiwane argumenty są ignorowane

```js
isApple("apple", 43); //drugi argument jest ignorowany
// true
```

- mniej niż `n` argumentów - brakujące mają wartość `undefined`

```js
isApple(); //pierwszy argument ma wartość "undefined"
// false
```

Do argumentów możemy odwołać się poprzez:

- nazwę
- pseudo-listę `arguments`

```js
function greetings() {
  for (let i = 0; i < arguments.length; i++) {
    console.log("Hi, " + arguments[i]);
  }

  //Hi, Tom
}
```

W razie potrzeby możemy wymusić liczbę argumentów

```js
function f(x,y) {if (arguments.length != 2)...
```

Właśnie przez ten śmietnik nie mamy przeciążania funkcji.

### Funkcje anonimowe

Tym określeniem określamy funkcje, które są przechowywane w zmiennych. Określane także jako `function expression`.

```js
let myFun = function () {
  lonsole.log("HelloFun");
};

myFun();
// HelloFun
```

### Funkcje strzałkowe

Funkcje strzałkowe (arrow functions) to po prostu inny format funkcji przypominający wyrażenia lambda z innych języków.  
Pozwala na krótszy zapis funkcji.

```js
const arrowFun = (value) => value + 12;

arrowFun(10);
// 22

const arrowFunMultiline = (imie) => {
  console.log(`imie to ${imie}`);
  return imie;
};

arrowFunMultiline("Jan");
// imie to Jan
// "Jan"

const linkNames = (imie, nazwisko) => imie + " " + nazwisko;
```

Mają one dość elastyczny zapis, w wypadku jednego argumentu nie musimy używać nawiasów początkowych, podobnie wygląda sytuacja z klamerkami w któ©ych zawieramy nasze funkcje.

Różnią się też nieco implementacją, nie jest dla nich tworzony `this`, ani obiekt `arguments`.

```js
const fun1 = function () {
  console.log(this); // undefined
};

const fun2 = () => {
  console.log(this); // zwróci globalny obiekt window
};
```

### Kolejność (hoisting)

Przy deklarowaniu funkcji nie musimy się martwić kolejnością ich deklaracji, ponieważ ich deklaracje są doczytywane wcześniej (ale na ich użycie musimy poczekać).

```js
const fun1 = function () {
  fun2();
};

const fun2 = function () {
  console.log("ok");
};

fun1(); //ale ta już musi być po deklaracji
```

### Dostęp do zmiennych w funkcji zagnieżdżonej

Funkcjie zdefiniowane we wnętrzu innuch funkcji mają dostęp do wszystkich zmiennych które są dostępne w wybranym zakresie.

```js
var global = "this is global";
function scopeFunction() {
  alsoGlobal = "This is also global!";
  var notGlobal = "This is private to scopeFunction!";
  function subFunction() {
    alert(notGlobal); // We can still access notGlobal in this child function.
    stillGlobal = "No var keyword so this is global!";
    var isPrivate = "This is private to subFunction!";
  }
  alert(stillGlobal); // This is an error since we haven't executed subfunction
  subFunction(); // execute subfunction
  alert(stillGlobal); // This will output 'No var keyword so this is global!'
  alert(isPrivate); // This generate an error since isPrivate is private to
  // subfunction().
  alert(global); // outputs: 'this is global'
}

alert(global); // outputs: 'this is global'
alert(alsoGlobal); // generates an error since we haven't run scopeFunction yet.
scopeFunction();
alert(alsoGlobal); // outputs: 'This is also global!';
alert(notGlobal); // generates an error.
```

### Zmienne proste vs złożone (kopia vs referencja)

Przy pracy ze zmiennymi warto pamiętać o tym, że jedynie proste typy zmiennych są kopiowane przy przekazywaniu dalej (Number, String, Boolean, Undefined, Null, Symbol, BigInt), w pozostałych przypadkach przekazywana jest referencja.

```js
let x = 1;
let y = x;
y = 2;
console.log(x);
// 1
console.log(y);
// 2

let d1 = { x: 1 };
let d2 = d1;

d2.x = 2; //niechcący nadpisaliśmy wartość x obiektu d1
console.log(d1);
//{ x: 2 }
console.log(d2);
//{ x: 2 }
```

Aby temu zapobiec można użyć operatora `Object.assign()` - łączy on ze sobą 2 obiekty, wystarczy połączyć nasz z jakimś pustym.  
Tworzy on jednak tylko płytką kopię.

```js
let kopia = Object.assign({}, d1);
```

## Obiekty

Obiekty mogą być tworzone na dwa sposoby.

### Tworzenie

**Jako wyrażenie** (expression) - sposób nieco zbliżony do opisu słownika. Otrzymujemy od razu gotową instancję naszej klasy.

```js
const osoba = {
  imie: "Marian",
  nazwisko: "Nowak",
  ur: 1999,

  getAge: function () {
    return 2021 - this.ur;
  },
};
```

Poszczególne elementy powinny być oddzielone przecinkami.

**Deklaracja** - tworzymy deklarację klasy i potem możemy (używając operatora `new` tworzyć jej instancje)

```js
class Rectangle {
  constructor(height, width) {
    this.height = height;
    this.width = width;
  }
}

let instancja = new Rectangle(0, 0);
```

Dostęp do elementów danej klasy uzyskujemy za pomocą słowa `this`.

```js
// Dane można pozyskiwać na 2 sposoby
osoba.imie;
//Marian

//Ten sposób jest nieco bardziej elastyczny i pozwala na nieco łatwiejsze zarządzanie polami
osoba["imie"];
//Marian

// Możemy tutaj też łątwo edytować pola w klasie
osoba.drugie_imie = "Zbigniew";

osoba;
// Object { imie: "Marian", nazwisko: "Nowak", wiek: 25, drugie_imie: "Zbigniew" }

osoba.getAge();
// 22
```

### Prototypy

Prototyp jest deklaracją zawierającą definicje, które są współdzielone między instancjami. Każda instancja ma dostęp do pól i metod prototypu.

Jest to przydatne, gdy chcemy coś zmienić we wszystkich instancjach danego obiektu bez ingerowania w niego.

```js
class Rectangle {
  constructor(height, width) {
    this.height = height;
    this.width = width;
  }
}

let rect = new Rectangle(10, 10);

// dla obiektu prototype dla instancji __proto__
Rectangle.prototype.field = function () {
  return this.height * this.width;
};

rect.field(); // to nam zwróci 100

Rectangle.__proto__; //zwróci nam prototyp bazowego obiektu
```

### Gettery i settery

Pozwalają na używanie niektórych metod tak, jakby były polami.  
Settery są bardzo przydatne podczas walidacji danych.

```js
const account = {
  owner: "Jonas",
  movements: [200, 530, 120, 300],

  get latest() {
    return this.movements.slice(-1).pop();
  },

  set latest(mov) {
    this.movements.push(mov);
  },
};

account.latest = 23;
account.latest;
```

## Komunikacja zewnętrzna i funkcje asynchroniczne

Aby zapobiec marnowaniu czasu niektóre funkcje w JS-ie zostały zaimplementowane asynchronicznie.

```js
const img = document.querySelector(".dog");
img.src = "dog.jpg"; // I właśnie to wczytywanie będzie asynchroniczne

//Jak już się wczyta to odpalony zostanie ten event
img.addEventListener("load", function () {
  console.log("Wczytano");
});
```

//TODO add obrazek https://www.google.com/search?q=javascript+main+thread+event+queue&sxsrf=ALiCzsa8Pc3xNZVsnB7g2sBxgdnyPUljVw:1664364932726&source=lnms&tbm=isch&sa=X&ved=2ahUKEwiFv93Esrf6AhXOh_0HHWrZD2YQ_AUoAXoECAIQAw&biw=1753&bih=850&dpr=1.09#imgrc=BQyez2KT8p8KzM
//Oisujący jak działa pętla zdarzeń

Warto pamiętać, że eventy z pętli zdarzeń mają miejsce **tylko** wtedy, gdy w głównym wątku nic nie jest przetwarzane.  
Po dokładniejsze wyjaśnienia zajrzyj do [Javascript - Inne informacje](./4_javascript_inne.html)

### AJAX

**AJAX** - Async JavaScript And XML. Pozwala asynchronicznie komunikować się z zewnętrznymi serwerami (wysyłać żądania etc). Kiedyś opierało się to na użyciu XML-a, ale od iluś lat używa się jednak JSONa.

Na potrzeby przykładów korzystamy z darmowych API [stąd](https://github.com/public-apis/).

Wcześniej używało się do tego XMLHttpRequest.

```js
const request = new XMLHttpRequest();
request.open("GET", "https://restcountries.eu/rest/v2/name/poland");
wynik = request.send();

var polska;
request.addEventListener("load", () => {
  console.log(this.responseText);
  //po otrzymaniu wyświetli nam się cały surowy tekst JSONa,
  //który trzeba przekształcić w jakiś sensowny obiekt
  [polska] = JSON.parse(this.responseText);
  //json parse zwraca listę obiektów, więc bierzemy tylko pierwszy
});
```

Jednak obecnie ta metoda jest przestarzała i zamiast tego używa się fetch, które zwraca nam Obietnicę (promise). Jest to tymczasowy obiekt w którym znajdziemy wynik operacji asynchronicznej jak już się wykona.  
Dzięki takiemu podejściu nie musimy polegać na callbackach, które mogą być problematyczne.

```js
const promise = fetch("https://restcountries.eu/rest/v2/name/poland");
```

Taka obietnica po zakończeniu zadania może zmienić swój stan na spełnioną, lub odrzuconą.  
Jak już została wykonana to możemy ją skonsumować.  
Do tego warto używać metody `then` do której przekazujemy co ma zostać zrobione z otrzymanymi danymi.

```js
then(onFulfilled);
then(onFulfilled, onRejected);

then(
  (value) => {
    /* fulfillment handler */
  },
  (reason) => {
    /* rejection handler */
  }
);
```

W wypadku błędu, lud odrzucenia rządania możemy też wykorzystać `catch()` na końcu łańcuszka.

```js
fetch("https://restcountries.eu/rest/v2/name/poland").then(function (response) {
  console.log(response); //wypisze nam całą klasę odpowiedzi z kodem statusu etc
  const new_promise = response.json(); //zwraca sparsowany obiekt, ale jest też kolejną obietnicą
});
```

Używając tych mechanizmów można łatwo łączyć wiele żądań w ciągi.

```js
const getCountryData = function (country) {
  fetch(`https://restcountries.eu/rest/v2/name/${country}`)
    .then((response) => {
      response.json();
    }) //po otrzymaniu odpowiedzi parsujemy ją asynchronicznie
    .then((data) => {
      console.log(data);
    }); //po sparsowaniu w końcu możemy ją wyświetlić
};
```

Mamy tu jedno żądanie, które po wykonaniu ma zwrócić kolejną obietnicę, która po spełnieniu ma nam wyświetlić sparsowany wynik.

#### Wysyłanie żądań z zawartością

Wysyłanie żądania zawierającego JSONa

Stary sposób:

```js
let xhr = new XMLHttpRequest();
let url = "https://httpbin.org/post";

xhr.open("POST", url, true); //true mówi, że ma być asynchronicznie
xhr.setRequestHeader("Content-Type", "application/json"); //kiedy jsona trzeba określić jaki to typ zawartości
xhr.onreadystatechange = function () {
  console.log("Jest git");
  console.log(this.responseText);
};
var data = JSON.stringify({ imie: "Jan", wiek: 12 });
xhr.send(data);
```

Nowy sposób:

```js
fetch("https://httpbin.org/post", {
  method: "post",
  headers: {
    Accept: "application/json, text/plain",
    "Content-Type": "application/json",
  },
  body: JSON.stringify({ imie: "Jan", wiek: 12 }),
})
  .then((res) => res.json())
  .then((res) => console.log(res));
```

Tutaj drugim argumentam fetcha jest odpowiednik obiektu [Request](https://developer.mozilla.org/en-US/docs/Web/API/Request/Request).

Warto zwrócić tu uwagę na pola:

- `method` - określa typ żądania
- `headers` - mamy tutaj typowe nagłówki http [lista](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers), za ich pomocą ustalamy np jaki typ danych wysyłamy (`Content-Type`), czy też jakie dane jesteśmy w stanie przyjąć (`Accept`).
- `body` - już samo ciało żądania, tutaj warto pamiętać, że najczęściej wysyłamy je w postaci stringa

### Runkcje asynchroniczne

Do zdefiniowania funkcji asynchronicznej (zwracającej obietnicę) wykorzystujemy słowo kluczowe `async`.

```js
// Variation of program in slide 38...
const fs = require("fs");
function readFilePromise(filename) {
  return new Promise((resolve, reject) => {
    fs.readFile(filename, (err, data) => {
      if (err) reject(err + "");
      else resolve(data + "");
    });
  });
}
async function readTwoFiles() {
  try {
    console.log(await readFilePromise("readfile.js"));
    console.log(await readFilePromise("doesntExist.js"));
  } catch (err) {
    console.error(err + "");
  }
}
readTwoFiles();
```

## Włączanie zewnętrznych bibliotek

TODO
