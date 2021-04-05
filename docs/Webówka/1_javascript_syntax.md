
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

##### `==` vs `===`

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


```js


```