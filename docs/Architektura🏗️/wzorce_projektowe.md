## Wzorce projektowe

Podstawowe źródła: [Wikipedia](<https://pl.wikipedia.org/wiki/Wzorzec_projektowy_(informatyka)>) oraz [Refactoring Guru](https://refactoring.guru/pl)

Wzorce projektowe dzielimy na 3 kategorie:

- **kreacyjne** - wzorce używane do generowania obiektów z określonymi zachowaniami
- **strukturalne** - opisują struktury z powiązanych ze sobą obiektów
- **behawioralne** - opisują zachowania oraz zadania poszczególnych obiektów

### Wzorce kreacyjne

#### Singleton

Używany, kiedy chcemy mieć tylko jedną instancję danej klasy w całym programie.

Zdaniem wielu jest to dość kontrowersyjny wzorzec ([wiki](<https://pl.wikipedia.org/wiki/Singleton_(wzorzec_projektowy)#Konsekwencje_stosowania>)), często traktowany jako antywzorzec.  
Ma on takie wady jak:

- Łamie [zasadę jednej odpowiedzialności](./architektura_i_paradygmaty.md#Programowanie_obiektowe)
- Łamie [zasadę otwarte-zamknięte](./architektura_i_paradygmaty.md#Programowanie_obiektowe)
- pogarsza elastyczność
- utrudnia testowanie

<!-- <div class="mermaid"> -->
```mermaid
classDiagram
    class Singleton{
        -instance
        -Singleton()
        +getInstance()
    }
```
<!-- </div> -->

```python
# jest wiele sposobów implementacji
class Singleton
    _instance = None

    def __new__(cls, *args, **kwargs):
        if cls._instance is None:
            cls._instance = super().__new__(cls, *args, **kwargs)

        return cls._instance
```

#### Prototyp

Jest on wykorzystywany wtedy, kiedy chcemy uprościć sobie tworzenie nowych instancji danej klasy bazując na już istniejącym obiekcie. Np kiedy mamy jakiś plik konfiguracyjny, który musimy tylko lekko zmodyfikować na nasze potrzeby.

W wielu wypadkach klonowanie obiektu z zewnątrz nie jest możliwe (np z powodu prywatnych parametrów). W takiej sytuacji warto wykorzystać interfejs dostarczający metodę `clone()`.

Takie podejście jest użyteczne kiedy chcemy, aby nasz kod był niezależny ok konkretnych klas obiektów, z które chcemy skopiować.

### Strukturalne

#### Adapter

#### Proxy

#### Fasada

Jest to wzorzec mający na celu uproszczenie korzystania ze skomplikowanego systemu poprzez dostaczenie uproszczonego interfejsu dostarczającego tylko te funkcjonalności, które są nam naprawdę potrzebne.

### Behawioralne

### nieposortowane TODO

#### Wstrzykiwanie zależności

Zamiast tworzyć obiekty w klasie przekazujemy jej zależne klasy.

- inicjalizacja nie następuje w naszych klasach z logiką biznesową (PKI wykład 8 30 min to było omwione)

#### Obserwator

#### MVC - porządnie omówione
