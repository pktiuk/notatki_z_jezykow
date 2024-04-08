# Zbiór informacji o C++

Oficjalna dokumentacja i zalecenia: [ISO CPP GUIDELINES](https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines)

## Dane i struktury

### Proste typy danych

Proste typy zmiennych:

- `int` - liczba całkowita
- `float` - liczba zmiennoprzecinkowa
- `double` - liczba zmiennoprzecinkowa podwójnej precyzji
- `char` - pojedynczy znak
- `bool` - wartość logiczna
- `void` - brak wartości

### Kontenery📦

W bibliotekach standardowych C++ mamy następujące typy kontenerów:

- Sekwencyjne
  - `vector` - jednowymiarowa tablica
  - `string` - jednowymiarowa tablica
  - `list` - lista dwukierunkowa
  - `deque` - kolejka o dwóch końcach
- Asocjacyjne
  - `set` - usuwa elementy równoważne
  - `map` - tablica asocjacyjna (słownik)
  - `multiset` - nie usuwa el. równoważnych
  - `multimap` - klucz może występować wielokrotnie
- Haszujące (unordered\_)
  - `unordered_set`
  - `unordered_map`
  - `unordered_multiset`
  - `unordered_multimap`

Można też je podzielić względem tego na czym bazują:

- Tablice: vector, string, array
- Węzły: list, set, map, multiset, multimap, unordered_set, unordered_map, unordered_multiset, unordered_multimap

Kontenery biblioteki standardowej operują na kopiach elementów. W przypadku, gdy chcemy operować na oryginalnych elementach, należy użyć wskaźników lub referencji.

#### Vector

Podstawowym kontenerem w C++ jest `std::vector`, który jest odpowiednikiem tablicy dynamicznej w C.

```cpp
#include <vector>
std::vector <int> zero_vector(5); //wektor zainicjalizowany 5 zerami

//wektor zainicjalizowany podanymi wartościami
std::vector<int> numbers = {1, 2, 3, 4, 5};

numbers[0] = 10; //zmiana wartości pierwszego elementu
```

Metody dostępu (mogą być używane także do zmieniania wartości):

- `at(index)` - zwraca element na danym indeksie (w razie problemów rzuca wyjątek [`std::out_of_range`](https://cplusplus.com/reference/stdexcept/out_of_range/))
- operator `[]` - zwraca element na danym indeksie (nie sprawdza czy indeks jest poprawny)
- `front()` - zwraca pierwszy element
- `back()` - zwraca ostatni element

Metody modyfikujące:

- `push_back(elem)` - dodaje element na koniec
- `pop_back()` - usuwa element (nie zwraca go).
- `size()` - zwraca ilość elementów
- `clear()` - usuwa wszystkie elementy

#### List

`std::list` jest to lista dwukierunkowa, która pozwala na szybkie dodawanie i usuwanie elementów z początku i końca listy. Nie posiada operatora `[]`, więc dostęp do elementów odbywa się za pomocą iteratorów.

```cpp
#include <list>

std::list<int> numbers = {1, 2, 3, 4, 5};
```

Metody dostępu:

- `front()`
- `back()`

Metody modyfikujące:

- `push_front(elem)`, `push_back(elem)`
- `pop_front()`, `pop_back()`
- `insert(iterator, elem)`
- `erase(iterator)`

#### std::set

Jest to kontener zawierający kolekcję niepowtarzalnych elementów.

Eliminuje on elementy równoważne
`a jest równoważne b, jeżeli !(a < b) && !(b < a)`

```cpp
#include <set>

std::set<int> numbers = {1, 2, 3, 4, 5};

set<int> s; //zbiór liczb całkowitych
s.insert(1); //dodaje elementy do kolekcji
s.insert(1); //ta operacja jest pusta (usuwa elementy równoważne)
s.insert(2);
assert( s.size() == 2); //bada liczbę elementów
assert( s.count(1) == 1 ); //zlicza liczbę wystąpień elementu
```

set jest zaimplementowany jako drzewo czerwono-czarne, co pozwala na szybkie dodawanie i usuwanie elementów. Z tego powodu potrzebuje on operatorów `<` i `==` dla swoich elementów.

```cpp
#include <set>

typedef std::pair<int,int> para;
//Aby zdefiniować set z parami, musimy zdefiniować operator < dla pary
bool operator<(const para& a, const para& b) {
    return a.first < b.first || (a.first == b.first && a.second < b.second);
}

std::set<para> pary = {para(1, 2), para(2, 3)};
```

#### Ciągi znaków `std::string`

`std::string` jest to kontener przechowujący ciągi znaków.

```cpp
#include <string>

std::string s = "Hello, World!";
```

Stringi nie są typowymi kontenerami. Mają one wiele metod do mnipulaji nimi.

Metody do konwersji:

- `std::string::c_str()` - zwraca wskaźnik do tablicy znaków (kiedy potrzebujemy kompatybilności z C)
- `atoi(str)`, `atof(str)`, `atol(str)` - konwertują string na liczbę (nie są to metody klasy string, ale funkcje globalne)
- `std::to_string(num)` - konwertuje liczbę na string

Metody do edycji:

- `std::string::erase(start, length)` - usuwa podciąg
- `std::string::replace(start, length, str)` - zamienia podciąg na inny
- `std::string::append(str)` - dodaje string na koniec (analogiczny do operatora `+`)

Inne:

- `std::string::compare(str)` - porównuje dwa stringi (zwraca 0, jeżeli są równe lub liczbę ujemną/dodatnią, jeżeli pierwszy jest mniejszy/większy od drugiego)

  ```cpp
  std::string s1 = "abc";
  std::string s2 = "def";
  assert(s1.compare(s2) < 0);
  ```

  Do porównań można też użyć operatorów `==`, `!=`, `<`, `>`, `<=`, `>=`

- `std::string::substr(start, length)` - zwraca podciąg stringa
- `std::string::find(str)` - zwraca pozycję, na której zaczyna się podciąg (lub `std::string::npos`, jeżeli nie znaleziono)

  ```cpp
  std::string s = "Hello, World!";
  assert(s.find("World") == 7);
  ```

## Mechanizmy języka

### Zarządzanie pamięcią

#### `new` i `delete`

Zarządzanie pamięcią w C++ jest podobne do [zarządzania w C](0_C.md#tablice-i-alokowanie-pamięci). Jednak jest oparta o słowa kluczowe `new` i `delete`. (NIGDY nie mieszajmy tych dwóch sposobów)

[artykuł](https://pl.wikibooks.org/wiki/C%2B%2B/Zarz%C4%85dzanie_pami%C4%99ci%C4%85)

`new` służy do tworzenia nowych obiektów i alokowania pamięci dla nich, natomiast `delete` służy do zwalniania zarezerwowanej wcześniej pamięci.

Przykład użycia słowa kluczowego new:

```cpp
int *p = new int; // alokuje pamięć dla zmiennej typu int
*p = 5; // przypisuje wartość 5 do zmiennej
delete p; // zwalnia pamięć zarezerwowaną dla zmiennej p
```

Możliwe jest także użycie słowa kluczowego new do tworzenia tablic dynamicznych:

```cpp
int *tab = new int[10]; // alokuje pamięć dla tablicy 10-elementowej
tab[0] = 5; // przypisuje wartość 5 do pierwszego elementu tablicy
delete[] tab; // zwalnia pamięć zarezerwowaną dla tablicy tab
```

#### Sprytne wskaźniki - Smart Pointers

W związku z wieloma problemami występującymi przy zarządzaniu pamięcią w C++, takimi jak wycieki pamięci, powstały tzw. smart pointery. Są to obiekty, które pomagają zautomatyzować zarządzanie pamięcią.

- `std::unique_ptr` - jest to smart pointer, który przechowuje wskaźnik do obiektu i zwalnia pamięć po wyjściu poza zakres. Nie można go kopiować, ale można przenieść.

  ```cpp
  std::unique_ptr<int> p(new int);
  *p = 5;
  ```

  - obiekty unique_ptr mają wielkość zwykłego wskaźnika
  - zastąpił on `auto_ptr` z C++98
  - automatycznie usuwają wskazywany obiekt w destruktorze
  - mogą być przechowywane w kontenerach standardowych
  - nie można kopiować, ale można przenieść

  ```cpp
    std::unique_ptr<Foo> f() {
      return std::unique_ptr<Foo>(new Foo(42));
    }
    std::unique_ptr<Foo> q = f(); //konstruktor kopiujący z r-value
    // v.push_back(p); //błąd kompilacji - nie ma konstruktora kopiującego
    v.push_back( std::move(p) ); //v staje się wł. wskazywanego obiektu
    //teraz p wskazuje na null
  ```

- `std::shared_ptr` - jest to smart pointer, który przechowuje wskaźnik do obiektu i zwalnia pamięć po wyjściu poza zakres, jeżeli nie ma innych shared_ptr wskazujących na ten obiekt. Można go kopiować.

  - obiekty shared_ptr mają dodatkowo licznik referencji
  - konstruktor ustwia licznik na 1
  - konstruktor kopiujący zwiększa licznik referencji
  - destruktor zmniejsza licznik

  ```cpp
  #include <memory>
  class Foo { /* ... */ };
  {
    std::shared_ptr<Foo> p1(new Foo(1) );
    {
      std::shared_ptr<Foo> p2(p1);
      //licznik odniesien == 2
      /* ... */
    } //destruktor p2, licznik = 1
  } //destruktor p1 usuwa obiekt
  ```

- `std::weak_ptr` - jest to smart pointer, który przechowuje wskaźnik do obiektu, ale nie zwiększa licznika referencji. Można go kopiować.

  - używany do uniknięcia cyklicznych referencji
  - nie zwiększa licznika referencji
  - nie ma operatora `->` ani `*`
  - można go zamienić na shared_ptr za pomocą `lock()`

  ```cpp
  std::shared_ptr<int> p(new int(42));
  std::weak_ptr<int> q(p);
  if (std::shared_ptr<int> r = q.lock()) {
    // r jest teraz shared_ptr
  }
  ```

Przy okazji korzystania ze sprytnych wskańników warto wspomnić o istnieniu funkcji `std::make_shared` i [`std::make_unique`](https://en.cppreference.com/w/cpp/memory/unique_ptr/make_unique), które pozwalają na tworzenie obiektów bezpośrednio w smart pointerach, bez używaniu operatora `new`.

```cpp
#include <boost/make_shared.hpp>
std::shared_ptr<Foo> pf = make_shared<Foo>(); //konstruktor domyślny
std::shared_ptr<Foo> pf2 = make_shared<Foo>(arg1,...,argN);
```

### Pętle

Typy pętli:

- Podstawowa pętla `for`

  ```cpp
  for (int i = 0; i < 5; ++i)
  ```

- pętla `while`

  ```cpp
  int j = 0;
  while (j < 10) {
      // rób coś
      ++j;
  }
  ```

- pętla `do-while`

  ```cpp
  int k = 0;
  do {
      // Wykonuj przynajmniej raz, potem sprawdzaj warunek
      ++k;
  } while (k < 3);
  ```

- range-based `for` - jest to zalecana metoda dla zbiorów iterowalnych

  ```cpp
  std::vector<int> numbers = {1, 2, 3, 4, 5};
  for (int num : numbers) {
      // Iteracja po elementach kontenera
  }
  ```

  W wypadku bardziej złożonych obiektów można użyć też referencji

  ```cpp
  for(auto&& element: lista)
  ```

  może być też używany do rozpakowywania [link](https://en.cppreference.com/w/cpp/language/range-for)

  ```cpp
  for (auto&& [first, second] : mymap)
  ```

### Funkcje

#### Lambdy

Składnia lambdy:

- `[]` - Tu podajemy listę przechwytywania
  - `[x]` - przechwytuje obiekt x (tylko odczyt)
  - `[&x]` - przechwytuje obiekt x (odczyt i zapis)
  - `[=]` - dowolny obiekt ze scope'a do odczytu
  - `[&]` - dowolny obiekt ze scope'a do odczytu i zapisu
- `()` - argumenty, jakie ma przyjmować wyrażenie lambda. (Opcjonalne)
- atrybuty wyrażenia lambda, z możliwych atrybutów w tym momencie najistotniejszy jest mutable, który sprawia że zmienne przechwycone przez wartość mogą być modyfikowane wewnątrz ciała wyrażenia. (Opcjonalne)
- `-> T` - typ zwracany (Opcjonalne)
- `{}` - ciało wyrażenia

```cpp
//Najprostsza możliwa lambda
[] { }();

[]( int a )->float
{
    if( a < 0 )
         return 0;

    return a * 0.5f;
}
```

#### Przekazywanie argumentów do funkcji

W C++ istnieją różne sposoby na przekazywanie argumentów do funkcji.

- poprzez **kopię** - w domyślnym wypadku do naszej funkcji przekazywana jest kopia naszego obiektu.
  O ile to nie jest problem przy liczbach to przy większych obiektach to to może być już problem.
- poprzez **wskaźnik** - jest to opcja zalecana bardziej przy kodzie napisanym w czystym C, czy też w wypadku, gdy chcemy sobie zastrzec możliwość przekazania pustego wskaźnika.
- poprzez **referencję** - jest to sposób zbliżony do wskaźnika, do funkcji przekazujemy referencję do naszego obiektu.

```cpp
class Klasa
{
private:
    /* data */
public:
    Klasa(/* args */)
    {
        std::cout << "Wołanie konstruktora\n";
    }

    Klasa(const Klasa& other)
    {
        std::cout << "Wołanie konstruktora kopiującego\n";
    }
};

void funkcja_zwykla(Klasa k) {}
void funkcja_pointer(Klasa *k) {}
void funkcja_referencja(Klasa &k) {}

int main()
{
    Klasa k = Klasa();
    std::cout << "funkcja_zwykla:\n";
    funkcja_zwykla(k);
    std::cout << "funkcja_pointer:\n";
    funkcja_pointer(&k);
    std::cout << "funkcja_referencja:\n";
    funkcja_referencja(k);
}
```

program wypisze:

```log
Wołanie konstruktora
funkcja_zwykla:
Wołanie konstruktora kopiującego
funkcja_pointer:
funkcja_referencja:
```

W wypadku przekazywania poprzez referencję lub wskaźnik należy pamiętać o tym, że zmiany obiektu, które miały miejsce wewnątrz funkcji będą nadal widoczne z zewnątrz, ponieważ operujemy tam na tej samej instancji obiektu.
Aby uniknąć takich problemów warto przekazywać te argumenty jako `const`, albo zastanowić się, czy jednak kopia nie będzie lepsza.

#### L-Value i R-Value

Przy okazji przekazywania wartości warto pamiętać też o pojęciu `r-value` i `l-value`. (lvalue rvalue)

TODO

### Wyjątki

Wyjątki służą do niesekwencyjnego przekazania sterowania, kiedy pojawi się jakiś nieoczywisty problem. W C++ wyjątki są rzucane za pomocą słowa kluczowego `throw`, a łapane za pomocą bloku `try-catch`.

Są rzucane w rzadkich sytuacjach, kiedy nie da się kontynuować programu. Należy unikać rzucania wyjątków w miejscach, gdzie można to zastąpić zwracaniem wartości. (ich koszt obliczeniowy jest dużo większy)

```cpp
try {
    throw std::runtime_error("Error");
} catch (std::runtime_error& e) {
    std::cout << e.what() << std::endl;
}
```

Zasady używania:

- Wyjątki powinny dziedziczyć po klasie [`std::exception`](https://cplusplus.com/reference/exception/exception/).
- Nie należy rzucać wyjątków w destruktorach. Bo podczas wyjątku niszczymy stare klasy i wtedy po raz drugi wywołałby się nasz destruktor i poraz drugi pojawiłby się wyjątek.
- Wyjątek rzucać przez wartość.

  ```cpp
  throw Exception //zgłasza wyjątek przez wartość
  throw new Exception;//zajmuje pamięć na stercie
  ```

- Wyjątek przechwytywać przez referencję

  ```cpp
  catch (const Exception& e) //przechwytuje przez referencję
  //catch(Exception e) //tworzy lokalną kopię
  ```

### Klasy

#### Funkcje wirtualne

są oznaczane za pomocą słowa kluczowego `virtual`.

```cpp
class Base {
   public:
    virtual void print() {
        cout << "Base Function" << endl;
    }
};

class Derived : public Base {
   public:
    void print() {
        cout << "Derived Function" << endl;
    }
};

int main() {
    Derived derived1;

    // pointer of Base type that points to derived1
    Base* base1 = &derived1;

    // calls member function of Derived class
    base1->print();

    return 0;
}
```

Podczas pracy z funkcjami wirtualnymi [dobrą praktyką](https://stackoverflow.com/questions/39932391/should-i-use-virtual-override-or-both-keywords) jest korzystanie ze specyfikatora [override](https://en.cppreference.com/w/cpp/language/override).  
Dzięki jego użyciu w klasie potomnej będziemy mieć pewność, że ta funkcja w klasie bazowej jest wirtualna.

```cpp
struct A
{
    virtual void foo();
    void bar();
    virtual ~A();
};

// member functions definitions of struct A:
void A::foo() { std::cout << "A::foo();\n"; }
A::~A() { std::cout << "A::~A();\n"; }

struct B : A
{
//  void foo() const override; // Error: B::foo does not override A::foo
                               // (signature mismatch)
    void foo() override; // OK: B::foo overrides A::foo
//  void bar() override; // Error: A::bar is not virtual
    ~B() override; // OK: `override` can also be applied to virtual
                   // special member functions, e.g. destructors
};
```

### Templatki

Pozwalają kompilatorowi na łatwą autogenerację kodu.

Templatka metody

```cpp
template <class myType>
myType GetMax (myType a, myType b) {
 return (a>b?a:b);
}
```

Templatka klasy

```cpp
template <class T>
class mypair {
    T values [2];
  public:
    mypair (T first, T second)
    {
      values[0]=first; values[1]=second;
    }
};
```

Specjalizacje templatek - pozwalają na łatwe doprecyzowanie implementacji dla pewnych ścićle określonych typów.

```cpp
template <class T> class mycontainer { ... };
template <> class mycontainer <char> { ... };
```

## Typy castów (operatorów rzutowania)

Używając tych operatorów na ogół powinno się operować na wskaźnikach (albo referencjach)

- `static_cast<naCoChcemyZrzutowac>(wyrazenie)` - wykorzystywany do konwersji danych w zmiennych różnych typów (np pomiędzy typami reprezentującymi liczby), jest on wykonywany w trakcie kompilacji.
- `dynamic_cast<naCoChcemyZrzutowac>(wyrazenie)` - służy do przekształcania typów klas pomiędzy klasami które po sobie dziedziczą. W wypadku niepowodzenia zwraca `null` Wyróżniamy:
  - Downcasting - kastujemy klasę bazową na potomną
  - Upcasting - gdy chcemy uzyskać instancję klasy bazowej
- `reinterpret_cast<naCoChcemyZrzutowac>(wyrazenie)` - działa podobnie do dynamic casta, ale nie zwraca nulla, zaleca się używanie tylko kiedy dobrze wiesz co robisz.
- `const_cast<naCoChcemyZrzutowac>(wyrazenie)` - pozwala zmienić stałą na zmienną i na odwrót na ogół jego używanie nie jest zalecane

```cpp
     const double liczbaPI = 3.14;
     const double *wskDoStalej = &liczbaPI;

     double *wskaznik = const_cast<double *>(wskDoStalej); //przypisujemy dane ze stałej do zwykłego wskaźnika

     cout << *wskaznik << endl; //wypisze 3.14
     *wskaznik = 43;
     // *wskDoStalej = 43; ERROR
     cout << *wskaznik << endl; //wypisze 3.14
```

## Wydajność

### Wątki

Jest wiele sposobów na wątki, ale najprostszym do użycia jest [`std::thread`](https://en.cppreference.com/w/cpp/thread/thread/thread)

```cpp
#include <thread>

void foo() {
    // funkcja, którą chcemy uruchomić w nowym wątku
}

int main() {
    std::thread t(foo); // tworzymy nowy wątek, który uruchomi funkcję foo
    //robimy coś w głównym wątku
    t.join(); // czekamy na zakończenie wątku
}
```

W wypadku klas wygląda to następująco:

```cpp
#include <thread>

class Klasa
{
public:
    void foo()
    {
        // funkcja, którą chcemy uruchomić w nowym wątku
    }
};

int main()
{
    Klasa k;
    //std::thread t(&Klasa::moja_metoda,&instancja_klasy, argument1, argument2, argument3);
    std::thread t(&Klasa::foo, &k); // tworzymy nowy wątek, który uruchomi funkcję foo
    //robimy coś w głównym wątku
    t.join(); // czekamy na zakończenie wątku
}
```

## Inne Słowa kluczowe

explicit TODO

## Nowe standardy

### C++17

[Artykuł](https://dsp.krzaq.cc/post/1417/artykul-cpp17-nowy-milosciwie-panujacy-nam-standard-c-z-programisty-66/)

### C++20

[Pełna lista z omówieniem](https://oleksandrkvl.github.io/2021/04/02/cpp-20-overview.html)

## Do zrobienia

TODO: std::move, lvalue i rvalue, &&, ogólnie o klasach i dziedziczeniu, explicit C- czyli co musi być kompilowane jako czyste C, typy smart pointerów.

//TODO VOLATILE https://en.cppreference.com/w/cpp/language/cv

//TODO C++ contracts https://www.modernescpp.com/index.php/c-core-guidelines-a-detour-to-contracts (similar to java JML, or Dafny for C#)
