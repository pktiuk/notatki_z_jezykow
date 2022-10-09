# UML - Unified Modelling Language

Jest to uniwersalny język do modelowania systemów i nie tylko.

Istnieje wiele typów diagramów UML. Takie jak:

- Diagram klas - pozwala na łatwe opisanie systemów obiektowych
- Diagram komponentów - pokazuje fizyczne elementy systemu oraz interakcje między nimi
- Diagram stanów - opisuje stany obiektu i przejścia między nimi
- Diagram aktywności (czynności) - podobny do diagramu stanów, z tą różnicą, że opisuje wiele obiektów
- Diagram przypadków użycia (use case) - pokazuje aktorów oraz przypadki użycia systemu
- ...

## Diagram klas

Przedstawienie klas oraz zależności i relacji między nimi. [Wikipedia](https://pl.wikipedia.org/wiki/Diagram_klas)

![Przykład](assets/uml_class_diagram_example.png)

Poszczególne klasy mają wyróżnioną nazwę oraz atrybuty takie jak:

- metody (funkcje)
- właściwości
- pola (zmienne)

Możemy je pokazwać jako sama nazwa, opcjonalnie wzbogacona o typ, argumenty i inne cechy. Dozwolone są tylko typy bazowe (`integer`, `real`, `char`, `string`, etc.) bez klas.

![bank](assets/uml-BankAccount1.svg.png)

Możemy także określać widoczność atrybutów

- `+` dla public – publiczny, dostęp globalny
- `#` dla protected – chroniony, dostęp dla pochodnych klasy (wynikających z generalizacji)
- `−` dla private – prywatny, dostępny tylko w obrębie klasy (przy atrybucie statycznym) lub obiektu (przy atrybucie zwykłym)
- `~` dla package – pakiet, dostępny w obrębie danego pakietu, projektu.

Zależności pomiędzy poszczególnymi klasami opisujemy za pomocą związków (powiązań)

![strzałki](assets/Uml_classes_relations.svg)

- **Zależność** (ang. dependency) – najsłabszy związek znaczeniowy między klasami, gdy jedna z klas używa innej. Na diagramie klas oznaczana `------->` przerywaną linią zakończoną strzałką wskazującą kierunek zależności
- **Asocjacja** (ang. association) wskazuje na silniejsze powiązanie pomiędzy obiektami danych klas (np. firma zatrudnia pracowników). Na diagramie asocjację oznacza się za pomocą linii `_______`. Nazwy cech (np. zatrudniony, zatrudniający) wraz z krotnością umieszcza się w punkcie docelowym asocjacji. Nazwę asocjacji podaje się pośrodku (np. zatrudnia).  
![Asocjacja](assets/UML_association_role_example.gif)
- **Generalizacja** lub **dziedziczenie** - wypełniona strzałka wskazuje na klasę bazową względem pochodnej
- **Agregacja** (ang. aggregation) reprezentuje związek typu całość-część, czyli jakaś większa całość jest rozbita na elementy. Oznacza to, że elementy częściowe mogą należeć do większej całości, jednak również mogą istnieć bez niej (np. koła i samochód).
- **Kompozycja** (ang. composition), jest silniejszą formą agregacji. W związku kompozycji, części należą tylko do jednej całości, a ich okres życia jest wspólny — razem z całością niszczone są również części. W dużej mierze jest to kwestia umowna, zależna od danego systemu.  
![Aggregation Composition](assets/uml-AggregationAndComposition.svg.png)


## Diagram aktywności

//TODO

## Diagram stanów

//TODO