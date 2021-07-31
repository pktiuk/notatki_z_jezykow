<script src="https://pktiuk.github.io/notatki_z_jezykow/Architektura%F0%9F%8F%97%EF%B8%8F/mermaid.min.js"></script> <script>mermaid.initialize({startOnLoad:true});</script>

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

<div class="mermaid">
classDiagram
    class Singleton{
        -instance
        -Singleton()
        +getInstance()
    }
</div>

```python
# jest wiele sposobów implementacji
class Singleton
    _instance = None

    def __new__(cls, *args, **kwargs):
        if cls._instance is None:
            cls._instance = super().__new__(cls, *args, **kwargs)

        return cls._instance
```

### Strukturalne

#### Adapter

#### Proxy

#### Fasada

### Behawioralne

### nieposortowane TODO

#### Wstrzykiwanie zależności

Zamiast tworzyć obiekty w klasie przekazujemy jej zależne klasy.

- inicjalizacja nie następuje w naszych klasach z logiką biznesową (PKI wykład 8 30 min to było omwione)

#### Obserwator

#### MVC - porządnie omówione
