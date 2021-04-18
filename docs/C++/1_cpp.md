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

