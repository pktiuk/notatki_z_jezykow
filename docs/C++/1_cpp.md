# Zbiór informacji o C++


## Templatki

//TODO

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
