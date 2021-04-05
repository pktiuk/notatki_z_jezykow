
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

Do tworzenie zmiennych w JS używamy słowa kluczowego `let`.  
JS nie wymusza niezmienności typów. (zalecanym stylem jest camelCase dla zmiennych)

```js
let mojaZmienna = 43;
mojaZmienna = "teraz slowo"
```

Zmienne nie mogą zaczynać się od liczb, ani nazywać się jak słowa kluczowe w JS (`new` `function` `class` etc)

```js
/* let 3liczba = 43; */
/* let function = 3; */
let $function =43 ; // ale za to $ jest dozwolony jako znak
```

### Typy zmiennych

Warto pamiętać, że JS ma dynamiczne typowanie, czyli nie musimy definiować typów zmiennych, ponieważ to jest sprawdzane dynamicznie w trakcie pracy.  
Poza tym możemy nadpisywać zmienne innymi typami.  

Zalecane formatowanie dla zmiennych to `camelCase`.

#### Podstawowe

```js
//Number - zawsze zmiennoprzecinkowa (także dla całkowitych)
let wiek = 22;

//String
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
// number
typeof "Slowo";
// "string"
let nieWiadomo;
console.log(typeof nieWiadomo);
// undefined
```

Warto zwrócić uwagę na to co daje tutaj `null`. (Jest to wyjątek z któreym trzeba się pogodzić)

```js
console.log(typeof null);
// object
```


```js


```