# Dokumentowanie kodu - Doxygen

Z pomocą doxygena można łatwo udokumentować kod z jego poziomu w sposób zarówno łatwy do odczytania w surowym kodzie, jak i umożliwiający automatyczne generowanie dokumentacji i podpowiadanie opisów funkcji w różnych IDE.

Jest on poza tym dość uniwersalny, wspiera języki takie jak:

- C++
- Java
- C#
- Python
etc.

## Syntax

O ile sam wygląd bloków doxygenowych w różnych językach może nieco się różnić to komendy (znaczniki) pozostają takie same.

[Oficjalna dokumentacja](https://www.doxygen.nl/manual/docblocks.html)  
[Pełna lista komend](https://www.doxygen.nl/manual/commands.html)  
[instrukcja2](https://www.star.bnl.gov/public/comp/sofi/doxygen/commands.html)

**Język C++**

```cpp
/**
 * @brief krótki opis funkcji
 *
 * Dłuższy opis
 *
 * @param argument1 - opis argumentu, do czego służy
 * @exception opis rzucanego wyjątku 
 * @return opis tego co jest zwracane
 */
int fun(const int &argument1);

/**
 * @brief Klasa będąca przykładem
 * 
 */
class A
{
private:
    int var1; //!< Krótki opis
    int var2; ///< Dłuższy
              ///< opis

public:
    A(/* args */);
    
};

```

**Python**

```python
## @package pyexample
#  Documentation for this module.
#
#  More details.
 
## Documentation for a function.
#
#  More details.
def func():
    pass
 
## Documentation for a class.
#
#  More details.
class PyClass:
   
    ## The constructor.
    def __init__(self):
        self._memVar = 0;
   
    ## Documentation for a method.
    #  @param self The object pointer.
    def PyMethod(self):
        pass
     
    ## A class variable.
    classVar = 0;
 
    ## @var _memVar
    #  a member variable

```

## Generowanie dokumentacji

TODO

### Gnerowanie diagramów klas

TODO