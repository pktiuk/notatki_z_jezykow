# Prace koncepcyjne - opis systemu

Przed rozpoczęciem prac nad systemem, a nawed przed rozpoczęciem projektowania systemu warto dokładnie zdefiniować jaki system zamierzamy zbudować.

Prace takie zaczyna się od rozmów z klientami/użytkownikami i rozpisania kilku dokumentów takich jak SRS (Software Requirement Specification) lub URS (User Requirement Specification)

## Podstawowe pojęcia

### User stories

Jest to jedna z najbardziej łopatologicznych i intuicyjnych metod opisujących wymagania.  
Polega ona na zebraniu wymagań w postaci **krótkich** historyjek opisujących sytuacje z perspektywy użytkownika.

Najczęściej prezentują się w następujący sposób:

**JAKO** ktoś **CHCIAŁBYM** cośtam zrobić **ABY** opis powodu.

Czyli np:  

- Jako marketingowiec chciałbym, żeby użytkownicy rejestrowali się w serwisie, po to, abym mógł potem ich śledzić i podnosić skuteczność sprzedaży
- Jako użytkownik Wikipedii chcę edytować artykuł, żeby dopisać lepszy przykład ilustrujący artykuł.
- Jako klient banku chcę zobaczyć listę ostatnich transakcji, żeby kontrolować swoje wydatki.
- Jako właściciel salonu fryzjerskiego chcę opublikować reklamę w internecie, żeby przyciągnąć więcej klientów.

W historyjkach opisujemy problemy, a niekoniecznie same rozwiązania. Unikamy jakichkolwiek szczegółów technicznych.

Przykłady niewłaściwych historyjek:

- `Jako użytkownik chcę się zarejestrować, aby móc korzystać z portalu` - użytkownik nie chce rejestrować się w portalu, bo to samo w sobie nie przynosi mu wartości. On chce korzystać
- `Jako klient banku potrzebuję listy transakcji, żeby kontrolować swoje wydatki` - tutaj niepotrzebnie zdefiniowane jest rozwiązanie problemu. Często istnieje wiele sposobów na rozwiązanie wybranych problemów, z tego powodu warto opisać sam problem, aby deweloperzy mogli samodzielnie pomyśleć nad najlepszym rozwiązaniem. (Może zamiast listy transakcji lepsze byłoby podsumowanie transakcji, bądź pogrupowanie ich typami.)
- `Jako product Owner chcę aby zmieniono interfejs na bardziej intuicyjny` - opisujemy co ma być zmienione, a nie jaka jst potrzeba/jaki jest problem


### Wymagania funkcjonalne



### Wymagania niefunkcjonalne

