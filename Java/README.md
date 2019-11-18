# Java Notatki

## Narzędzia:
 - `jshell` – interpretator interaktywny **?jak importować w nim własne pakiety?**
 - `jlink` – generacja modułu aplikacji



### HelloWorld w javie
```java
public class HelloWorldApp {
    public static void main(String[] args) {
        System.out.println("Hello world from Java!");
    }
}
```
Wszystko jest tu klasą, nasza apka też. Jeżeli chcemy, aby jakaś klasa zaczęła coś robić przy jej samodzielnym uruchomieniu to dodajemy funkcję: `public static void main(String[] args)` 

## Pakiety
Każda klasa należy do jakiegoś pakietu. Jeśli w pliku z kodem źródłowym klasy nie występuje na początku deklaracja przynależności tej klasy do konkretnego pakietu, wówczas klasa ta będzie należeć do domyślnego pakietu.
Klasy należące do tego samego pakietu mogą odwoływać się do siebie bez konieczności stosowania nazw kwalifikowanych (bez przedrostka)
```java
import java.applet.Applet;
public class App extends Applet {////kod
}
//LUB
public class App extends java.applet.Applet {////kod
}
```
Klasa System jest zawarta w java.lang, importowanym automatycznie

## Typy danych
**Wbudowane** – określone przez twórców języka
– typy proste (albo: typy dla wartości, value-type): zmienne tych typów zawierają wartości tychże typów
– typy referencyjne: zmienne tych typów zawierają odniesienie do tablicy lub obiektu, który reprezentują
**Definiowane** przez programistę
– klasy
– typy wyliczeniowe (enumeration)

Java ma **statyczne typowanie** tzn, że raz zdefiniowana zmienna nie zmienia swojego typu (jak np. w pythonie)

Wbudowane typy proste
 - całkowitoliczbowe, kodowane U2
    - `byte`   jednobajtowy
    - `short`  dwubajtowy
    - `int` czterobajtowy
    - `long` ośmiobajtowy
 - zmiennoprzecinkowe, kodowane IEEE 754
    - `float` czterobajtowy
    - `double` ośmiobajtowy
 - inne
    - `char` dwubajtowy, kodowany Unicode (utf-16)
    - `boolean` wartość logiczna true lub false

do javy 11 można stosować identyfikator typu wywnioskowanego:
`var s = "test";`

#### Stałe
**Literały** – stałe bez nazwy, o typie wynikającym ze sposobu zapisu literału, np.

|78,| 8864L,| 37.266,| 37.266D, |37.266F, |’c’,| true, null|
|--|--|--|--|--|--|--|
|int| long| double| double| float| char| boolean|

oraz łańcuchy znaków, typu String: "ala ma kota"
**Stałe symboliczne** – stałe opatrzone nazwą i jawną deklaracją typu
```java
final typ NAZWA_STAŁEJ = wartość;
//np.
final float PI= 3.14;
```
Lokalną stałą symboliczną można zainicjować później – najpierw wystąpi sama
deklaracja, a później przypisanie pierwszej (i ostatecznej) wartości.
```java
final int STAŁA_CZYSTA; // Definicja stałej
/**/
STAŁA_CZYSTA = 0; // Inicjalizacja stałej
```
### Typ wyliczeniowy
```java
enum Season { WINTER, SPRING, SUMMER, FALL }
```
– kompilator sprawdza zgodność typu
– może być użyty w instrukcji switch
```java
Season anything=Season.WINTER;
switch(anything){
case SUMMER: System.out.println("Lato");
//…
}
```
### Referencja
**Referencja** to zmienna, której wartością jest adres.
Typy referencyjne:
 - tablice,
 - klasy,
 - interfejsy.
Zmienna referencyjna odnosi się do miejsca pamięci, w którym pomieszczono daną lub
wektor danych reprezentowanych tą zmienną.
Java nie zna typu wskaźnikowego, tzn. jawnego korzystania z adresów.

### Konwencje nazewnicze dla nazw zmiennych i klas:
 - nazwa zmiennej rozpoczyna się małą literą,
 - nazwa klasy rozpoczyna się wielką literą,
 - kolejne słowa w nazwie rozpoczyna się wielką literą, np. isVisible,
 - znak podkreślenia (_) jest wprawdzie poprawny w nazwie, ale powinien być używany jedynie w nazwach stałych.

### Cykl życia obiektu
1. Utworzenie zmiennej typu referencji do obiektu (`typ nazwa;`) Dla typu klasy lub interfejsu zmienna przechowuje adres do obiektu klasy – nie jest on dostępny bezpośrednio, lecz stanowi referencję. Do momentu przypisania jej adresu ma ona wartość zerową (null).
2. Utworzenie obiektu (`new` alokuje obszar pamięci) `nazwa=new typ(argumenty)` Operator new zwraca referencję do nowo utworzonego obiektu.
3. Inicjalizacja -wywołanie konstruktora
4. Używanie
5. Usuwanie obiektu - "Garbage Collector" środowisko samodzielnie usuwa obiekt, jeżeli wykryje, że już więcej nie będzie używane w programie, wywołuje się on samoczynnie co jakiś czas, ale można to zrobić ręcznie `System.gc()`
6. Ewentualne wykonanie metody `finalize()` dziedziczona po klasie Obiect- pozwala wykonać dodatkowe czynności związane z usuwaniem obiektu 

## Operatory
Operator – funkcja podana w notacji operatorowej - z 1, 2 lub 3 argumentami
(operandami).
 - 1-argumentowe operatory mogą być przedrostkowe i przyrostkowe:
operator operand // notacja przedrostkowa
operand operator // notacja przyrostkowa
    - przedrostkowe i przyrostkowe `++` i `--`
 - 2-argumentowe operatory występują pomiędzy swoimi operandami:
operand1 operator operand2
    - Działania matematyczne`+`,`-`,`*`,`/`,`%`
    - Porównania `>`,`>=`,`==`,`<=`,`<`,`!=`
    - Tylko dla wartości logicznych: 
        - `&&` , `&` "and"
        - `||`, `|` "or"
        - `!` negacja
        - `^` op1 ^ op2 true, gdy op1 i op2 mają różne wartości
    - Przesunięcia
        - `>>` np op1>>op2 przesuń op1 w prawo o op2 bitów
        - `<<` np op1<<op2 przesuń op1 w lewo o op2 bitów
        - `>>>` op1>>>op2 przesuń op1 w prawo o op2 bitów, zastępując bit znaku zerem
    - Bitowe logiczne
        - `&` op1 & op2 iloczyn bitowy op1 i op2
        - `|` op1 | op2 suma bitowa op1 i op2
        - `^` op1 ^ op2 bitowa różnica symetryczna op1 i op2
        - `~` ~op bitowa negacja op
    - Przypisania
        - op1=op2
        - `*=`,`+=`,`-=`,`|=`,`%=`itp...
 - 3-argumentowy operator (jedyny w Javie):
operand1 ? operand2 : operand3
    - `op1?op2:op3` gdy op1 jest „true”, zwraca op2, w przeciwnym razie zwraca op3
 - Inne
     - `typ[]`/`typ[liczba]` deklaracja tablicy
     - `op[liczba]` pobranie elementu z tablicy
     - `(typ)op` konwersja wyrażenia op do typu typ
     - `net op1` utowrzenie obiektu lub tablicy
     - `op1 instanceof op2` zwraca „true”, gdy obiekt op1 jest instancją klasy op2

Za wyjątkiem operatora + używanego też do łączenia napisów, operatory arytmetyczne są przeznaczone tylko dla operandów liczbowych.


## Instrukcje sterujące (pętle i warunki)
```java
while (wyrażenie) {
    instrukcje
} // Wykonuj pętlę gdy wyrażenie jest prawdziwe

do {
    instrukcje
} while (wyrażenie);
// Sprawdzenie warunku następuje po zakończeniu pętli

for (inicjalizacja; warunek; inkrementacja) {
instrukcje
} // Wszystkie trzy wyrażenia są opcjonalne; może być: for(;;)

for (typ zm_lokalna:ref_obiekt_iterowany_lub_tablica) {
instrukcje
}

if( wyrażenie ) {
    instrukcje
} else {
    instrukcje
}

switch( zmienna ) {
    case wartość1: instrukcje; break;
    case wartość2: instrukcje; break;
    …
    default: instrukcje; break;
}
```
Słowa kluczowe:
 - `break` bez etykiety – kończy wykonywanie aktualnej wewnętrznej instrukcji sterującej switch, for, while, do-while
 - instrukcja break z etykietą – kończy wykonywanie zewnętrznego switch, for, while, do-while o danej etykiecie:
`break etykieta_instrukcji; `
 - `continue` kończy bieżącą iterację wewnętrznej pętli
 - `continue` z etykietą -analogicznie
 -  `return` – powrót z wykonywanej metody

## Klasa
Definicja klasys kłada się z
 - nagłówka definicji klasy
    - class nazwa_klasy (obligatoryjnie)
    - specyfikacje: dostępu i dziedziczenia (opcjonalnie)
 - bloku definicji klasy

Specyfikacje domyślne klasy:
 - niepubliczna (istnieją restrykcje dostępu)
 - nieabstrakcyjna (można tworzyć obiekty tej klasy)
 - niefinalna (może mieć klasy pochodne)
 - dziedziczy niejawnie po klasie Object
 - nie implementuje niejawnie żadnych 

Specyfikacje dodatkowe (niedomyślne) klasy:
 - public – klasa jest dostępna dla wszystkich klas (domyślnie: tylko dla klas z tego samego pakietu)
 - abstract – nie można tworzyć obiektów tej klasy
 - final – nie można dziedziczyć z tej klasy
 - extends klasa_bazowa – deklaruje dziedziczenie po klasie bazowej
 - implements interfejs1, interfejs2 – deklaruje implementowanie jednego lub więcej interfejsów

Blok definicji klasy – ograniczony parą nawiasów klamrowych, zawiera
 - deklaracje wszystkich zmiennych składowych - pól (w tym obiektów i pól statycznych)
 - deklaracje i definicje wszystkich funkcji składowych - metod (w tym metod wywoływanych na rzecz obiektu lub metod statycznych)
 - ewentualnie, definicje jednego lub więcej konstruktorów

**Konstruktory**
Nazwy konstruktorów są takie same jak nazwa konstruowanej klasy.
Wywołania konstruktorów:
`new Stack();`
`new Stack(123);`
Odpowiednikiem **destrukotrów** jest metoda `finalize()`
Jeśli w klasie nie zdefiniowano żadnego konstruktora, tworzony jest automatycznie  domyślny konstruktor (pusty)
Klasy dziedziczące korzystają z konstruktora pustego, jeżeli go nie ma to należy samodzielnie wywołać inny
Konstruktory – specyfikacja dostępu
 - `private` - żadna inna klasa nie może bezpośrednio użyć takiego konstruktora do tworzenia obiektów danej klasy
 - `protected` – obiekty mogą być tworzone przez klasy pochodne danej klasy i klasy należące do tego samego pakietu
 - `public` - każda klasa może tworzyć obiekty danej klasy
 - brak specyfikatora dostępu - każda klasa z tego samego pakietu może tworzyć obiekty danej klasy

Pola klasy – specyfikatory
 - `private`, `public`, `protected`, (package) – specyfikacja dostępu
 - `static` – deklaracja pola statycznego (przynależnego do klasy, a nie – jej obiektów)
 - `final` – deklaracja pola stałego
 - `transient` – specyfikacja pola, które nie powinno podlegać serializacji
 - `volatile` – specyfikacja pola ulotnego, niepodlegającego optymalizacji: przypisanie zmiennej wartości odbywa się zawsze w pamięci (współdzielonej przez wątki), a nie w rejestrze procesora, więc jest od razu widoczne dla współbieżnych wątków

Pole i metoda jednej klasy mogą nosić taką samą nazwę:
```java
public class CircularBuffer{
private float[] buffer; // pole buffer
private float[] buffer(); // metoda buffer
}
```
## Metody
Deklaracja metody – specyfikacja
 - poziomu dostępu
 - typu wyniku
 - nazwy
 - listy argumentów formalnych
`public Object push(Object item)`

Wszystkie możliwe elementy nagłówka definicji metody (w ich kolejności)
 - poziom dostępu - `public`, `protected`, `package`, `private`
 - `static` - deklaruje metodę jako statyczną
 - `abstract` – metoda nie posiada definicji, jej klasa musi być abstrakcyjna
 - `final` - nie może być nadpisana przez metody klas pochodnych
 - `native` - metoda rodzima, napisana w innym języku programowania
 - `synchronized` – może być jednocześnie wykonywana (na rzecz konkretnego obiektu) tylko przez jeden wątek
 - typ wyniku OBOWIĄZKOWE
 - nazwa metody OBOWIĄZKOWE
 - lista parametrów (w nawiasach) OBOWIĄZKOWE
 - throws wyjątki - lista wyjątków zgłaszanych przez metodę

**Wynik metody**
Można zwrócić
 - nic -`void` `return;`
 - zmienną np int `return 10;`
 - obiekt (referencja) np. `return new String();`

 - Metody przeciążone różnią się liczbą lub typem parametrów
 - Metoda nadpisana (polimorficzna) ma tę samą sygnaturę, co metoda w klasie
bazowej. Nie może rozszerzać zbioru zgłaszanych wyjątków.

**Odwołania w metodach**
 - `this`-odwołanie do obiektu, na rzecz którego wykonywana jest metoda
 - `super` - odwołanie do "nadobiektu", określonego przez klasę bazową

## Wyjątki
Wyrzucenie wyjątku:
`throw obiekt`
Obsługa:
```java 
try {
    instrukcje // tu może wystąpić throw
} catch (typ_wyjątku nazwa) { // obsługa wyjątku danego typu
    instrukcje
} finally { // wykonywana zawsze niezależnie od zaistnienia wyjątku
    instrukcje
}
```
# Skończone na slajdzie 17 Wykadu 2
