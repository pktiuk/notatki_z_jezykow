# HTML i CSS

Źródło tej notatki <https://developer.mozilla.org/pl/docs/Learn/Getting_started_with_the_web/HTML_basics>

HTML jest językiem znaczników (ang. markup language).  
Składa się z serii znaczników (**tagów**), których używa się do zamknięcia, opakowania różnych części treści, tak aby wyglądały i/lub działały w określony sposób. Z pomocą tagów możesz ze słów czy obrazów zrobić linki do innych stron, etc.

## Podstawowa struktra

### Element

Podstawową strukturą jest element.

![](./assets/budowa_paragrafu.png)
Mamy tutaj:  

- Tag otwierający
- Tag zamykający
- Zawartość  
Razem tworzą one nasz element

Elementy mogą zawierać także atrybuty

![](./assets/atrybut.png)

Atrybut zawsze powinien mieć:

- Spację między nazwą tagu a nazwą atrybutu (lub innego atrybutu, jeśli dany element ma więcej atrybutów).
- Nazwę atrybutu oraz znak równości.
- Wartość podaną w "cudzysłowie"

Atrybuty `class` i `id` są uniwersalnymi atrybutami dla wszystkich tagów. Pozwalają one na łatwe zarządzanie elementami strony poprzez przypisywane im identyfikatorów i określanie ich przynależności do różnych klas. (ID musi być unikalne, klasa już nie)
Potem można używać tego do zmiany stylów w CSS, czy też w skryptacj w JS.

Warto pamiętać, że elementy mogą mieć wiele klas jednocześnie

```html
<button class="btn again">Again!</button>
```

Elementy mogą się w sobie zagnieżdżać

```html
<p>My cat is <strong>very</strong> grumpy.</p>
```

Elementy mogą być też **puste** - gdy nie zawierają żadnej treści.  
Nie muszą wtedy mieć tagu zamykającego.

```html
<img src="images/firefox-icon.png" alt="My test image">
```

### Struktura plików

Całość zawsze jest zawarta w tagach HTML.

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>My test page</title>
  </head>
  <body>
    <img src="images/firefox-icon.png" alt="My test image">
  </body>
</html>
```

Opisy elementów:

- `<!DOCTYPE html>` - typ dokumentu (opcjonalny)
- `<html>` - element [html](https://developer.mozilla.org/pl/docs/Web/HTML/Element/html) zawiera całą treść strony i czasem nazwany jest elementem bazowym (ang. root element). Wskazuje, gdzie zaczyna i kończy się kod HTML.
- `<head>` -element [head](https://developer.mozilla.org/pl/docs/Web/HTML/Element/head) to tzw. nagłówek strony. Ten element działa jak kontener dla wszystkich elementów, które chcesz umieścić na stronie HTML, ale nie w treści, które wyświetlasz przeglądającym twoją stronę. Ma on w sobie na ogół konfigurację.
- `<body>` - element [body](https://developer.mozilla.org/pl/docs/Web/HTML/Element/body). Zawiera onczęść właściwą strony, czyli jej zawartość.
- `<meta charset="utf-8">` - reprezentuje metadane, które nie mogą być reprezentowane przez inne elementy związane z metadanymi w HTML. Tutaj ustawia zestaw znaków.
- `<title>` - Ustawia tytuł strony, który jest tytułem wyświetlanym na karcie przeglądarki

### Tekst

#### Nagłówek

Nagłówki opisujemy jako h1 (najgłówniejszy), h2,h3...

```html
<h1>My main title</h1>
<h2>My top level heading</h2>
<h3>My subheading</h3>
<h4>My sub-subheading</h4>
```

#### Paragraf

Służą one do dzielenia tekstu na paragrafy

```html
<p>This is a single paragraph</p>
```

#### Lista

```html
<ul>
  <li>technologists</li>
  <li>thinkers</li>
  <li>builders</li>
</ul>
```

#### Linki

Aby utworzyć odnośnik musimy użyć prostego elementu — [a](https://developer.mozilla.org/pl/docs/Web/HTML/Element/a) — "a" jest skrótem od angielskiego "anchor".

```html
<a href="https://www.mozilla.org/en-US/about/manifesto/">Mozilla Manifesto</a>
```

- href (hypertext reference) - link

### Obraz

Używamy do tego tagu [img](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/img)

```html
 <img src="images/firefox-icon.png" alt="My test image">
```

- `src` - źródło obrazu
- `alt` - tekst alternatywny - pokazuje się w razie problemów z wyświetleniem.

### DIV

[div](https://developer.mozilla.org/pl/docs/Web/HTML/Element/div) - jest to element który nie robi nic. Służy on jako kontener, dzięki któremu można łatwo podzielić i pogrupować elementy.

### Wejścia

pole tekstowe i przycisk (bez JS-a bezuzyteczne)

```html
<input type="text" placeholder="Domyślny tekst" />
<button>GIT!</button>
```

<input type="text" placeholder="Domyślny tekst" />
<button>GIT!</button>

## CSS

CSS służy do ustalania stylu naszej strony. Analogicznie do JS-a może być umieszczonyw pliku html, lub w oddzielnym pliku.

```html
<html>
<head>
 <title>Learning CSS</title>
<style>
    body {
        background-color: green;
    }
</style>
</head>

<body></body>
</html>
```

Osadzamy to za pomocą linku (ale nie tagoem a - anchor, tylko link)

```html
 <title>Learning CSS</title>
<link href="style.css" rel="stylesheet">
</head>
```

### Składnia CSS

Poniżej widać, że przypisujemy dane parametry dla wszystkich elementów należących do tagu `body` tzn do wszystkich elementóœ dziedziczących po nim.

```css
body {
  background-color: yellow;
  font-family: sans-serif;
}
```

Pliki CSS zawierają listy elementów, które mają mieć zmienione wartości, mogą one opisywać zarówno to jak ammy zmienić niektóre tagi, jak i plasy, czy też edytować poszczególne ID.

**Klasa** - do zmian właściwości klasy używamy nazwy klasy poprzedzonej kropką

```html
    <p class="mojaklasa">
      Przykładowa klasa
    </p>
```

```css
.mojaklasa {
  color: red;
}
```

**ID** - tutaj zamiast kropki używamy `#`

```html
    <p id="moj_paragraf">
      Przykładowa klasa
    </p>
```

```css
#moj_paragraf {
  color: green;
  border: 5px solid black
}
```

Co ciekawe widać tutaj właściwość `border` - może ona mieć więcej niż jedną właściwość - tutaj są to grubość, styl i kolor.

**Kilka elementów** wystarczy je wymienić po przecinku

```css
input,
button {
  padding: 10px;
  font-size: 16px;
}
```

**Elementy umieszczone względem innych** - jeśli chcemy oznaczyć wszystkie elementy znajdujące się wewnątrz innych to wypisujemy obok siebie, tylko bez przecinków

```css
#moj-element h2 {
  color: black;
} /* będzie dotyczyć tylko nagłówków h2 wewnątrz elementu z id moj-element */
```

**Wszystko**

Za pomocą `*` można łatwo "złapać" wszystkie elementy.  
Można to użyć, aby łątwo dostosować np. marginesy wszystkich elementów.

```css
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box; /* ta właściwość zmiania liczenie rozmiaru, od teraz ustalony rozmiar dotyczy zawartości wraz z paddingiem, a nie tylko zawartości */
}
```

Warto pamiętać, że nie wszystkie właściwości są dziedziczone, np `padding` dotyczy tylko wskazanego elementu, elementy wewnątrz nie będą zmieniane.

### Box Model

Jest to koncepcja mówiąca, że każdy element strony powinniśmy postrzegać jako prostokąt z zawartością charakteryzujący się takimi właściwościami jak szerokość wysokość etc.

![](./assets/css-box-model.jpg)

Dodatkowo jest jeszcze **fill area** czyli cała przestrzeń znajdująca się w obrębie granicy (border).

I właśnie te parametry możemy złatwością dostosowywać za pomocą CSS-ów.
