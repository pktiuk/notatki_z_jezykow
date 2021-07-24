# Javascript DOM - Interakcje i właściwości

DOM (Document Object Model) -ustrukturyzowana reprezentacja dokumentów HTML.  
Pozwala Javascriptowi na dostęp do jego elementów i manipulowanie nimi (zmiana stylu, tekstu, czy też stylu CSS).

Jest to drzewiasta struktura łącząca elementy rodziców z ich dziećmi.

![Drzewo DOM](https://www.guru99.com/images/JavaScript/javascript8_1.png)

Korzeniem tej struktury jest `document`. Jest to klasa dostępna w JS-ie do której się odwołujemy, gdy chcemy wejść w interakcję z naszym dokumentem.

Do manipulacji elementami zawartymi w dokumencie HTML wystarczy użyć metody `document.querySelector`, która zwróci nam obiekt reprezentujący dany element.

## Manipulacja elementami strony

W praktyce

```js
document.querySelector(".message");
//W nawiasie podajemy jego identyfikator, analogicznie jak w CSS-ie .klasa lub #id

document.querySelector(".message").textContent;
//"Wiadomość"
document.querySelector(".message").textContent = "Nowa wiadomość"; // w tym momencie zmieni się tekst zawarty w tym elemencie
```

### Znajdowanie elementów

```js
document.querySelector(".message"); //szuka po nazwie i zwraca pierwszy pasujący
document.querySelectorAll(".message"); //jak wyżej, tylko zwraca listę wszystkich elementów

document.documentElement; //zwraca nam całe drzewo dokumentu
document.body; //analogicznie
document.head;

document.getElementById("element1"); // zwraca nam element po ID (bez potrzeby używania krokek, czy haszów przy nazwach)
document.getElementsByTagName("button"); //Elements - czyli zwróci nam listę elementów typu button
document.getElementsByClassName("moja_klasa");
```

### Dodawanie i tworzenie elementów

Do dodawanie elementów w HTML-u używa się metody [Element.insertAdjacentHTML()](https://developer.mozilla.org/pl/docs/Web/API/Element/insertAdjacentHTML) albo [insertAdjacentElement()](https://developer.mozilla.org/en-US/docs/Web/API/Element/insertAdjacentElement).  
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
const my_element = document.createElement("div"); //to co dostaliśmy zachowuje się jak każdy element zdobyty za pomocą np query selectora

document.body.prepend(my_element); //po wstawieniu naszego elementu do dokumentu nasz obiekt może być nadal używany
//możemy np zmienić położenie naszego elementu
document.body.append(my_element); // przeniesie to nasz element bo może istnieć tylko jedna instancja obiektu w DOM-ie
// jesli chcemy kopiować to trzeba użyć .cloneNode(true)

my_element.remove(); // usuwa ten element
```

W niektórych przypadkach zamiast `createElement()` trzeba użyć [createElementNS()](https://developer.mozilla.org/en-US/docs/Web/API/Document/createElementNS) (np w wypadku elementów wewnątrz svg).

### Edycja elementu oraz atrybutów

```js
my_element.classList.add("my-created-class");
my_element.textContent = "Trochę tekstu";

// Ten jest chyba najbardziej uniwersalny przy prostych zastosowaniach
my_element.innerHTML = "<h1>Trochę tekstu tylko inaczej</h1>";

// zmiana atrybutów elementów
my_element.color = "green"; // dla standardowych możemy się do nich dostać przez pole w klasie
my_element.setAttribute("creator", "Marian"); //to się za to sprawdzi dla niestandardowych

// jedynym wyjątkiem dla niestandardowych atrybutów są atrybuty data-.....
// <button data-version-number=0/>
mybtn.dataset.versionNum = 32;
```

### CSS

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
document.querySelector("body").style.backgroundColor = "#60b347";
```

Należy pamiętać o tym, że pobierając style w sposób pokazany powyżej pobieramy tylko style określonych elementów.

```js
const bt = document.querySelector("#my-btn");
bt.style.width; //to zwróci nam wartość tylko i wyłącznie wtedy, gdy dany przycisk miał to zapisane bezpośrednio
// (nie np gdy ta wartość jest dziedziczona po klasie, typie, albo jest zapisana w pliku CSS)

getComputedStyle(bt).color; // to nam zawsze zwróci jakąś wartość
```

Podobnie możemy manipulować zmiennymi CSSowymi

```js
document.documentElement.style.setProperty("--background-color", "red");
```

## Odbieranie zdarzeń

Aby odbierać zdarzenia z elementów wystarczy dodać funkcję będącą callbackiem dla danego wydarzenia powiązanego z tym elementem.

```js
document.querySelector(".myButton").addEventListener("click", function () {
  console.log("pressed button");
});
```

Warto pamiętać, że możemy odbierać zdarzenia nie tylko z elementów, lecz także z dokumentu jako całości. Np poprzez odbieranie wciśnięć.

```js
document.addEventListener("keydown", function (e) {
  console.log(e);
});
//keydown { target: body, key: "Escape", charCode: 0, keyCode: 27 }
```

Warto wiedzieć, żę w wypadku funkcji wołanych przez zdarzenia mamy w nich dostęp do słowa kluczowego `this` - reprezentuje ono wskaźnik na obiekt, który uruchomił dane wydarzenie.

//TODO przykład

## Co można znaleźć w DOM-ie

### Właściwości globalne

[Window](https://developer.mozilla.org/en-US/docs/Web/API/Window/window) jest globalnym obiektem [Window](https://developer.mozilla.org/en-US/docs/Web/API/Window).  
W pewnym sensie to z jego wnętrza operujemy, bo `window.window.pageYOffset` zwraca to samo co `pageYOffset`.
Z jego pomocą można łatwo ustalić jego wymiary, obecne położenie na stronie i tym podobne.

Przykładowe właściwości i metody obiektu window:

- `pageYOffset` `pageXOffset` - obecne położenie (tylko odczyt), czyli o ile pikseli przewinęliśmy

Warto także pamiętać o takich obiektach jak `document` oraz `screen` (zawiera informacje na temat wymiarów ekranu itp).

### Metody dla elementów

Przydatne metody dla klasy bazowej [Element](https://developer.mozilla.org/en-US/docs/Web/API/Element)

- [scrollTo(x,y)](https://developer.mozilla.org/en-US/docs/Web/API/Element/scrollTo), [scrollIntoView()](https://developer.mozilla.org/en-US/docs/Web/API/Element/scrollIntoView) - ten drugi nieco nowszy

### Przydatne właściwości elementów

**Wymiary i położenie**

```js
element.getBoundingClientRect();
```

zwróci

```json
DOMRect { x: 30, y: -1054.9000244140625, width: 115.69999694824219, height: 28.79998779296875, top: -1054.9000244140625, right: 145.6999969482422, bottom: -1026.1000366210938, left: 30 }
```

wartości `x` oraz `y` pokazują położenie względem lewej i góry okna (viewport-u, nie strony), to znaczy, że mogą się zmieniać wraz z przewijaniem.
