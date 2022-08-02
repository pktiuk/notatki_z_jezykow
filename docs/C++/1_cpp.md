# Zbiór informacji o C++

Oficjalna dokumentacja i zalecenia: [ISO CPP GUIDELINES](https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines)

## Przekazywanie argumentów do funkcji

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

W wypadku przekazywania poprzez referencję lub wskaźnik należy pamiętać o tym, że zmiany obiektu, które miały miejsce wewnątrz funkcji będą nadal widoczne z zewnątrz, ponieważ operujemy tam na tej samej instancji obiektu.
Aby uniknąć takich problemów warto przekazywać te argumenty jako `const`, albo zastanowić się, czy jednak kopia nie będzie lepsza.

## Templatki

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

- `static_cast<naCoChcemyZrzutowac>(wyrazenie)` - wykorzystywany do konwersji danych w zmiennych różnych typów (np pomiędzy typami reprezentującymi liczby)
- `dynamic_cast<naCoChcemyZrzutowac>(wyrazenie)` -
- `reinterpret_cast<naCoChcemyZrzutowac>(wyrazenie)` -
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

## Wątki

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

## Funkcje

### Lambdy

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

## Słowa kluczowe

explicit TODO

## Nowości z C++20

[Pełna lista z omówieniem](https://oleksandrkvl.github.io/2021/04/02/cpp-20-overview.html)

## Do zrobienia

TODO: std::move, lvalue i rvalue, &&, ogólnie o klasach i dziedziczeniu, explicit C- czyli co musi być kompilowane jako czyste C, typy smart pointerów.
