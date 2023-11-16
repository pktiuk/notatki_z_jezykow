# Zbiór informacji o C++

Oficjalna dokumentacja i zalecenia: [ISO CPP GUIDELINES](https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines)

## Elementy języka i jego mechanizmy

### Zarządzanie pamięcią `new` i `delete`

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

### Przekazywanie argumentów do funkcji

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

```
Wołanie konstruktora
funkcja_zwykla:
Wołanie konstruktora kopiującego
funkcja_pointer:
funkcja_referencja:
```

W wypadku przekazywania poprzez referencję lub wskaźnik należy pamiętać o tym, że zmiany obiektu, które miały miejsce wewnątrz funkcji będą nadal widoczne z zewnątrz, ponieważ operujemy tam na tej samej instancji obiektu.
Aby uniknąć takich problemów warto przekazywać te argumenty jako `const`, albo zastanowić się, czy jednak kopia nie będzie lepsza.

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

## Biblioteki

### Wątki

Jest wiele sposobów na wątki, ale najprostszym do użycia jest `std::thread`

```cpp
#include <thread>

// Start thread t1
    std::thread t1(callable);

    // Wait for t1 to finish
    t1.join();

    // t1 has finished do other stuff

    //Wywołanie dla metody w klasie
    std::thread t2(&Klasa::moja_metoda,&instancja_klasy, argument1, argument2, argument3);
    t2.join();
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
