# Wyrażenia regularne (Regexy)

Świetna strona do ekspreymentowania z wyrażeniami regularnymi [Regex101](https://regex101.com/)
Ściągawka z BulldogJobs https://bulldogjob.pl/readme/samouczek-regex-sciagawka-z-przykladami

## Znaki

| symbol | Opis                                         |
| ------ | -------------------------------------------- |
| \s     | whitespace                                   |
| \S     | nie whitespace                               |
| \d     | cyfra                                        |
| \D     | nie cyfra                                    |
| \w     | słowo                                        |
| \W     | nie słowo                                    |
| \n     | nowa linia                                   |
| \t     | tabulacja                                    |
| \A     | Początek wyrażenia                           |
| $      | koniec wyrażenia lub/EOL/EOF                 |
| \Z     | koniec wyrażenia                             |
| .      | Jakikolwiek znak (nie licząc nowej linii \n) |
| `\.`   | Kropka `.` (w grepie jednak trzeba dać `\\.` |

Znaki specjalne: `^ [ . $ { * ( \+ ) | ? < >`  
Do ich escape'owania na ogół wystarcza `\`.

## Grupy i zakresy

|             |                                                                                    |
| ----------- | ---------------------------------------------------------------------------------- |
| [a-c]       | znaki z zakresu a-c. Mogą być łączone w większe grupy (np. [a-deA-D1-4])           |
| [^a-c]      | Zaprzeczenie znakom z danego zakresu (nie a nie b i nie c)                         |
| `(aIbIc)`   | Alternatywa a lub lub c (zamiast I powinny tam być linie pionowe)                  |
| `*`         | Znak/wyrażenie znajdujący się przed gwiazdką może pojawić się dowolną ilość razy   |
| `+`         | Znak/wyrażenie sprzed plusa pojawi się dowolnie wiele razy (ale co najmniej 1 raz) |
| `?`         | Znak/wyrażenie pojawia się 0 lub 1 raz                                             |
| `(?!slowo)` | zaprzeczenie - wyklucz wyniki zawierające `slowo` (negative lookahead)             |
| I           | alternatywa(nie litera i, lecz beleczka) - rzecz polewej albo po prawej            |

## Podmienianie znaków

Używając regexów można w łatwy sposób podmieniać części naszych wyrażeń na inne.

Wystarczy tutaj opakować część wyrażenia, którą chcemy wymienić w nawiasy `()` i potem w wyrażeniu docelowym możemy się odwoływać do zawartości poszczególnych nawiasów.

Najbardziej przydatne odwołania:

|            |                        |
| ---------- | ---------------------- |
| `$1`, `$2` | Pierwszy, drugi nawias |
| `$&`       | Całe wyrażenie         |

```txt
Find        Carrots(With)Dip(Are)Yummy
Replace     Bananas$1Mustard$2Gross
Result      BananasWithMustardAreGross
```
