
# Javascript

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
let $function =43 ; // ale za to $ jest dozwolony jako znak
```

### Typy zmiennych

Warto pamiętać, że JS ma dynamiczne typowanie, czyli nie musimy definiować typów zmiennych, ponieważ to jest sprawdzane dynamicznie w trakcie pracy.  
Poza tym możemy nadpisywać zmienne innymi typami.  

```js
let mojaZmienna = 43;
mojaZmienna = "teraz slowo"
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

tablica.unshift(0) //tobi to samo co pop, tylko dodaje na początek

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
const lista = ["a", "b", "c",];
for (const [num, elem] of lista.entries())
{
      console.log(`Indeks: ${num} Zawartosc: ${elem}`);
}

```

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
- trójargumentowy ` ? : `

Kolejność operatorów jest taka jak w matematyce.

##### Operator `==` i `===`

Istnieją dwa operatory równości:

- `===` - ścisły -  zwraca prawdę tylko i wyłącznie wtedy, gdy obie strony są takie same, nie bawi się w żadne konwersje etc.
- `==` - jest nieco luźniejszy, pozwala sobie na konwersje pomiędzy typami jeśli wartości są różnych typów, poza tym ma inne "pomagające" mechanizmy, które w dłuższej prespektywie mogą powodować więcej błędów. (jeśli się da używaj `===`)

```js
19 === "19"
// false

19 == "19"
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
"number"
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

### Printowanie

```js
console.log("Wiadomosc1" , 323);
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
console.log('Wiele\n\
linii w kodzie');

//VS

console.log(`Wiele
linii w kodzie`);
```

## IF-y i warunki

Syntax warunków jest zbliżony do C++

```js
const wiek = prompt("podaj wiek"); //pojawi się okno z pytaniem

if (wiek >= 18)
{
    console.log("Pełnoletni");
}else
{
    console.log("Niepełnoletni");
}

if (true)
      console.log("Nie");
else
      console.log("Tak");

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
      case value3:// dla tych dwóch wartości będzie się dziać to samo
            fun3();
            break;

      default:
            break;
}
```

Jest też operator trójargumentowy ` ? : `

```js
wiek >= 18 ? console.log("Dorosły") : log.console("Nie Dorosły");
// Albo
console.log(wiek >= 18 ? "Dorosły" : "Nie Dorosły");
```

## Pętle

Nic ciekawego mamy 2 zwykłe typy pętli, `for` i `while`.

```js
for(let num=0;num <10;num++)
{
      if(num===5) continue; //ale skipujemy dla 5
     console.log(`Printujemy po raz ${num+1}`) 
}

while(true)
{
      //nigdy nie kończąca się pętla
      break; //no chyba, że użyję break
}
```

Poza tym mamy jeszcze forEach w dwóch wariantach.

```js
const tablica = [0,11,22,33,44];

for (const i of tablica)
{
      console.log(i);
}

// Metoda forEach
tablica.forEach(function(i){console.log(i);});
```

## Funkcje

Definiujemy je używając słowa kluczowego `function`.  
Także są na ogół formatowane jako `camelCase`.

!!! warning
    Niestety JS **nie wspiera** przeciążania funkcji.

Poniżej zwykłe deklaracje funkcji (function declaration).

```js
function printHello()
{
      console.log("Hello");
}

printHello();
// Hello

function isApple(fruit)
{
      if ( fruit == "apple")
            return true;
      else
            return false;
}
```

Co ciekawe nie wysypią się one nawet gdy damy im złą ilość argumentów

```js
printHello(23);
// Hello

isApple("apple",43);
// true

isApple();
// false
```

### Funkcje anonimowe

Tym określeniem określamy funkcje, które są przechowywane w zmiennych. Określane także jako `function expression`.

```js
let myFun = function () {
      lonsole.log("HelloFun");
}

myFun();
// HelloFun
```

### Funkcje strzałkowe

Funkcje strzałkowe (arrow functions) to po prostu inny format funkcji przypominający wyrażenia lambda z innych języków.  
Pozwala na krótszy zapis funkcji.

```js
const arrowFun = value => value+12;

arrowFun(10);
// 22

const arrowFunMultiline = imie => {
      console.log(`imie to ${imie}`);
      return imie;
}

arrowFunMultiline("Jan");
// imie to Jan
// "Jan"

const linkNames = (imie, nazwisko) => imie + " " + nazwisko;
```

Mają one dość elastyczny zapis, w wypadku jednego argumentu nie musimy używać nawiasów początkowych, podobnie wygląda sytuacja z klamerkami w któ©ych zawieramy nasze funkcje.

## Obiekty

Obiekty tutaj wydają się nieco zbliżone do typowych słowników.

```js
const osoba = {
      imie: "Marian",
      nazwisko: "Nowak",
      ur: 1999,

      getAge: function () {
            return 2021 - this.ur;
      },
}
```

Poszczególne elementy powinny być oddzielone przecinkami.  
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

osoba
// Object { imie: "Marian", nazwisko: "Nowak", wiek: 25, drugie_imie: "Zbigniew" }

osoba.getAge();
// 22
```

## DOM - interakcja z elementami strony

DOM (Document Object Model) -ustrukturyzowana reprezentacja dokumentów HTML.  
Pozwala Javascriptowi na dostęp do jego elementów i manipulowanie nimi (zmiana stylu, tekstu, czy też stylu CSS).  

Jest to drzewiasta struktura łącząca elementy rodziców z ich dziećmi.  

![Drzewo DOM](https://www.guru99.com/images/JavaScript/javascript8_1.png)

Korzeniem tej struktury jest `document`. Jest to klasa dostępna w JS-ie do której się odwołujemy, gdy chcemy wejść w interakcję z naszym dokumentem.

Do manipulacji elementami zawartymi w dokumencie HTML wystarczy użyć metody `document.querySelector`, która zwróci nam obiekt reprezentujący dany element.

### Manipulacja elementami strony

W praktyce 

```js
document.querySelector('.message'); 
//W nawiasie podajemy jego identyfikator, analogicznie jak w CSS-ie .klasa lub #id 

document.querySelector('.message').textContent;
//"Wiadomość"
document.querySelector('.message').textContent="Nowa wiadomość"; // w tym momencie zmieni się tekst zawarty w tym elemencie
```

#### Znajdowanie elementów

```js
document.querySelector('.message');  //szuka po nazwie i zwraca pierwszy pasujący
document.querySelectorAll('.message'); //jak wyżej, tylko zwraca listę wszystkich elementów

document.documentElement; //zwraca nam całe drzewo dokumentu
document.body; //analogicznie
document.head;

document.getElementById('element1'); // zwraca nam element po ID (bez potrzeby używania krokek, czy haszów przy nazwach)
document.getElementsByTagName("button"); //Elements - czyli zwróci nam listę elementów typu button
document.getElementsByClassName("moja_klasa");
```

#### Dodawanie i tworzenie elementów

Do dodawanie elementów w HTML-u używa się metody [Element.insertAdjacentHTML()](https://developer.mozilla.org/pl/docs/Web/API/Element/insertAdjacentHTML).  
Pozwala ona nam wstawić dowolny tekst (element) względem wybranego elementu.

```js
element.insertAdjacentHTML(position, text);
```

`position` może przyjmować wartości:

- 'beforebegin': przed element -em.
- 'afterbegin': W środku element-u przed jego pierwszym dzieckiem.
- 'beforeend': W środku elementu po jego ostatnim dziecku.
- 'afterend': Po element-cie 

Odpowiadają one takim wstawienion:

```html
<!-- beforebegin -->
<p>
  <!-- afterbegin -->
  foo
  <!-- beforeend -->
</p>
<!-- afterend -->
```

Stworzenie elementu (którego jeszcze nie dodajemy do naszego DOM-a)

```js
const my_element = document.createElement('div'); //to co dostaliśmy zachowuje się jak każdy element zdobyty za pomocą np query selectora
my_element.classList.add('my-created-class');
my_element.textContent ="Trochę tekstu";
my_element.innerHTML ="<h1>Trochę tekstu tylko inaczej</h1>";

document.body.prepend(my_element); //po wstawieniu naszego elementu do dokumentu nasz obiekt może być nadal używany 
//możemy np zmienić położenie naszego elementu
document.body.append(my_element); // przeniesie to nasz element bo może istnieć tylko jedna instancja obiektu w DOM-ie
// jesli chcemy kopiować to trzeba użyć .cloneNode(true)


my_element.remove(); // usuwa ten element
```


#### CSS

Aby dostać się do stylu w CSS należy dostać się do parametru `style`.

```css
body {
  font-family: sans-serif;
  color: #eee;
  background-color: rgb(36, 33, 33);
}
```

Trzeba tylko pamiętać, że wszystkie zmienne wewnątrz stylów (także liczby) muszą być podawane jako stringi.

```js
document.querySelector('body').style.backgroundColor = '#60b347';
```

### Odbieranie zdarzeń

Aby odbierać zdarzenia z elementów wystarczy dodać funkcję będącą callbackiem dla danego wydarzenia powiązanego z tym elementem.

```js
document.querySelector('.myButton').addEventListener('click', function () {
    console.log("pressed button");
});
```

Warto pamiętać, że możemy odbierać zdarzenia nie tylko z elementów, lecz także z dokumentu jako całości. Np poprzez odbieranie wciśnięć.

```js
document.addEventListener('keydown', function (e) {
  console.log(e);
});
//keydown { target: body, key: "Escape", charCode: 0, keyCode: 27 }
```

## Komunikacja zewnętrzna i funkcje asynchroniczne

Aby zapobiec marnowaniu czasu niektóre funkcje w JS-ie zostały zaimplementowane asynchronicznie.

```js
const img =document.querySelector('.dog');
img.src = "dog.jpg"; // I właśnie to wczytywanie będzie asynchroniczne

//Jak już się wczyta to odpalony zostanie ten event
img.addEventListener('load', function() {console.log("Wczytano");});

```

### AJAX

**AJAX** - Async JavaScript And XML. Pozwala asynchronicznie komunikować się z zewnętrznymi serwerami (wysyłać żądania etc). Kiedyś opierało się to na użyciu XML-a, ale od iluś lat używa się jednak JSONa.

Na potrzeby przykładów korzystamy z darmowych API [stąd](https://github.com/public-apis/).

Wcześniej używało się do tego XMLHttpRequest.

```js
const request = new XMLHttpRequest();
request.open('GET','https://restcountries.eu/rest/v2/name/poland');
wynik = request.send();



var polska;
request.addEventListener('load',() =>{
      console.log(this.responseText);
//po otrzymaniu wyświetli nam się cały surowy tekst JSONa,
//który trzeba przekształcić w jakiś sensowny obiekt
      [polska] = JSON.parse(this.responseText);
      //json parse zwraca listę obiektów, więc bierzemy tylko pierwszy
      })

```

Jednak obecnie ta metoda jest przestarzała i zamiast tego używa się fetch, które zwraca nam Obietnicę (promise). Jest to tymczasowy obiekt w którym znajdziemy wynik operacji asynchronicznej jak już się wykona.  
Dzięki takiemu podejściu nie musimy polegać na callbackach, które mogą być problematyczne.

```js
const promise = fetch('https://restcountries.eu/rest/v2/name/poland');

```

Taka obietnica po zakończeniu zadania może zmienić swój stan na spełnioną, lub odrzuconą.  
Jak już została wykonana to możemy ją skonsumować.  
Do tego warto używać metody `then` do której przekazujemy co ma zostać zrobione z otrzymanymi danymi.

```js

fetch('https://restcountries.eu/rest/v2/name/poland').then(function(response){
      console.log(response);//wypisze nam całą klasę odpowiedzi z kodem statusu etc
      const new_promise = response.json(); //zwraca sparsowany obiekt, ale jest też kolejną obietnicą
})
```

Używając tych mechanizmów można łatwo łączyć wiele żądań w ciągi.

```js
const getCountryData = function (country) {
  fetch(`https://restcountries.eu/rest/v2/name/${country}`)
    .then(response => {response.json();}) //po otrzymaniu odpowiedzi parsujemy ją asynchronicznie
    .then(data => { console.log(data); }); //po sparsowaniu w końcu możemy ją wyświetlić
};
```

Mamy tu jedno żądanie, które po wykonaniu ma zwrócić kolejną obietnicę, która po spełnieniu ma nam wyświetlić sparsowany wynik.
