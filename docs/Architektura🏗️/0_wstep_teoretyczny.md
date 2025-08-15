# Wstęp teoretyczny

## Czym jest architektura?

Architektura oprogramowania jest ogólnym opisem organizacji aplikacji (**High level design HLD**).

Obejmuje ona takie aspekty jak:

- Charakterystyki architektoniczne - opisują jakie cechy systemu muszą być brane pod uwagę, takie jak testowalność, rozszerzalność, niezawodność
- Decyzje architektoniczne
- Komponenty logiczne
- Styl architektoniczny - opisuje w jaki sposób dany system powinien być zbudowany/działać. Najczęściej polega na określeniu danego typu takiego jak np: monolit, mikroserwisy, system zdarzeniowy etc.

## Architektura (HLD) a Design (LLD)

W przykładowej aplikacji bankowej architektura wysokopoziomowa obejmuje takie tematy jak to, w jaki sposób klient wymienia się danymi z serwerem, jak bazy danych wymieniają się i zapisują dane etc. Są to aspekty wysokopoziomowe na ogół nie związane nawet z wybranymi językami.  

Nie obejmuje zaś ona takich tematów jak projekt interfejsu, wykorzystywane wzorce projektowe, czy też styl pisania kodu. (te aspekty to **Low Level Design LLD**). [link LLD vs HLD](https://www.geeksforgeeks.org/system-design/difference-between-high-level-design-and-low-level-design/). 

Różnice te można porównać do takich rzeczy jak strategia vs taktyka, czy też struktura budynku vs wygląd, ogół i szczegół.

Przykładowym narzędziem używanym przy LLD są diagramy klas UML, zaś przy HLD są to diagramy architektoniczne (pokazujące jakie serwisy mają gadać ze sobą i które są spięte z jakimi bazami danych).   

Często zagadnienia architektoniczne nie mogą być łatwo przypisane do jednej z tych klas, ponieważ zazębiają się z wieloma poziomami. Mówimy tutaj o takich decyzjach jak:

- wybór framweorka dla interfejsu (wpływa na organizację kodu, ale też może zmieniać sposób komunikacji z innymi elementami)
- rozdzielanie modułów na mniejsze części (może wynikać z nadmiernego rozrostu, co zarówno wpływa na codebase jak i na to jakie są zadania danej części)


## Charakterystyki architektoniczne

Czyli w skrócie co twój system musi umieć i czego od niego wymagamy. Ich określenie jest jednym z pierwszych kroków pracy nad przygotowywaniem systemu. (proces ich zbierania jest opisany [tutaj](./2_prace_koncepcyjne.md))

Charakterystyki te można także określać mianem wymagań niefunkcjonalnych. Do charakterystyk można zaliczyć takie chechy jak testowalność, skalowalność, wydajność, modularność etc. (jest tego [dość dużo](https://iso25000.com/index.php/en/iso-25000-standards/iso-25010)).

Ze względu na mnogość opcji warto podzielić je na kategorie.

### Charakterystyki procesowe

Są to cechy będące często na styku HLD i LLD. WIążą się one często z tym, jak budowane jest dane oprogramowanie.

Mamy tutaj:

- **Modularność/Modułowość** (modularity) - jak bardzo oprogramowanie jest podzielone na mniejsze fragmenty. Wpływa ona na organizację kodu, często tekże na jego reużywalność.
- **Testowalność** (testability) - jak łatwo jest testować system oraz uruchamiać na nim różne rodzaje testów (jednostkowych, integracyjnych, akceptacyjnych etc.).
- **Rozszerzalność** - jak łatwo jest deweloperom dodawać nowe funkcjonalności i rozszerzać system. Obejmuje to bardzo wiele aspektów takich jak standardy pisania, podział na moduły, testowalność, sposób zarządzania kodem etc.
- **Deployowalność/Wdrażalność** - jak łatwo jest wdrożyć dany system

### Charakterystyki strukturalne

TODO