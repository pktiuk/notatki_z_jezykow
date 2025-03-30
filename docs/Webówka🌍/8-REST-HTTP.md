# REST i HTTP

## HTTP i HTTPS

HTTP (Hypertext Transfer Protocol) to protokół sieciowy stosowany do przesyłania danych w sieci.  
Protokół HTTP pozwala na wymianę danych za pomocą zapytań (ang. `requests`) i odpowiedzi (ang. `responses`). Zapytania są wysyłane przez przeglądarkę internetową do serwera, a odpowiedzi są wysyłane przez serwer z powrotem do przeglądarki. Zapytania i odpowiedzi są wysyłane w postaci ciągów tekstowych, które są następnie parsowane i interpretowane przez klienta i serwer.

??? note "Kiedy wysyłanie zapytań do serwera to za mało."

    Tutaj warto pamiętać, że w niektórych wypadkach, kiedy ciągłe odpytywanie serwera jest nieefektywne możliwe jest wysłanie informacji do klienta. Można do tego celu użyć [WebSocektów](https://developer.mozilla.org/en-US/docs/Web/API/WebSocket), bądź SSE (Server Sent Events) [link](https://developer.mozilla.org/en-US/docs/Web/API/Server-sent_events/Using_server-sent_events)

Protokół HTTP składa się z kilku elementów, takich jak:

- Metoda zapytania: określa, co ma zostać zrobione z danymi. Najczęściej używane metody to `GET`, `POST`, `PUT` i `DELETE`.
- Adres URL: określa lokalizację danych, do których zostanie wysłane zapytanie.
- Nagłówki: są to informacje dodatkowe, które są wysyłane razem z zapytaniem lub odpowiedzią. Nagłówki mogą zawierać informacje o typie zawartości, autoryzacji lub innych szczegółach zapytania lub odpowiedzi.
- Treść zapytania lub odpowiedzi: zawiera dane, które są przesyłane pomiędzy klientem a serwerem.

### Metody HTTP wykorzystywane przy transferze

| Nazwa  | Opis                              |
| ------ | --------------------------------- |
| GET    | Pobierz dane                      |
| PUT    |                                   |
| POST   | Utwórz lub zaktualizuj jakąś daną |
| DELETE | Usuń jakąś daną                   |

### Kody odpowiedzi

Po wykonaniu każdego zapytania otrzymujemy kod odpowiedzi opisujący wynik naszej operacji.

Pierwsza cyfra kodu opisuje typ błędu

- 1xx - kody informacyjne
- 2xx - sukces
- 3xx - przekierowanie
- 4xx - błąd klienta
- 5xx - błąd serwera

#### Popularne kody

- `200` OK: Żądanie zostało pomyślnie zrealizowane i serwer zwrócił odpowiednią treść.
- `301` Moved Permanently: Zasób, który został zażądany, został przeniesiony na stałe na nowy adres URL. Przeglądarka powinna automatycznie przekierować użytkownika na nowy adres.
- `401` Unauthorized: Serwer wymaga uwierzytelnienia użytkownika, aby zaakceptować żądanie.
- `404` Not Found: Zasób, który został zażądany, nie został znaleziony na serwerze.
- `500` Internal Server Error: Serwer napotkał błąd wewnętrzny podczas próby zrealizowania żądania.

### URL

**URL** (Uniform Resource Locator) to ciąg tekstowy, który służy do identyfikowania i lokalizowania zasobów w sieci. Zasoby te mogą być plikami, obrazami, stronami internetowymi lub innymi danymi.

Składnia URL składa się z kilku elementów, które są oddzielone znakiem "/":

- `Protokół` określa, jaki protokół sieciowy jest używany do połączenia z zasobem. Najczęściej używanymi protokołami są `HTTP` i `HTTPS`.
- `Nazwa hosta` określa, na którym serwerze znajduje się zasób. Nazwa hosta może być nazwą domeny, np. "example.com", lub adresem IP serwera.
- `Ścieżka` określa lokalizację zasobu na serwerze. Ścieżka składa się z katalogów i nazw plików, które są oddzielone znakami "/".
- `Parametry`zapytania: są to dodatkowe informacje przekazywane do serwera podczas żądania zasobu. Parametry zapytania są zazwyczaj w postaci pól klucz-wartość, które są oddzielone znakiem `&` i są dodawane do URL po znaku `?`.

```url
https://example.com/path/to/file.html?key1=value1&key2=value2
```

## REST

**Representational state transfer** - sposób komunikacji aplikacji siecowymi oparty na zapytaniach HTTP i przesyłaniu JSONów (lub innych zbliżonych plików) z odpowiedziami.

W takim systemie każdemu API odpowiada unikalny url.

### JSON

**JSON** (JavaScript Object Notation) to lekki format wymiany danych, który jest często stosowany do przesyłania danych między aplikacjami i systemami w sieci. Jest to format tekstowy, który jest łatwy do odczytu i zapisu dla ludzi, a także łatwy do analizowania i generowania przez komputery.

Format JSON opiera się na składni języka JavaScript i składa się z par klucz-wartość. Klucze są ciągami tekstowymi zawierającymi nazwy pól, a wartości mogą być różnymi typami danych, takimi jak liczby, ciągi znaków, tablica lub obiekt.

```json
{
  "name": "John Smith",
  "age": 30,
  "city": "New York",
  "skills": ["JavaScript", "HTML", "CSS"]
}
```

Opiera się ona na słownikach `{"nazwa":wartość}` oraz na listach `[]`.

### Przesyłanie danych nie tekstowych

Jako, że JSON wspiera przede wszystkim dane tekstowe to aby zapakować inne dane do zapytania/odpowiedzi należy skorzystać z algorytmu takiego jak `base64`

**Base64** to sposób kodowania danych binarnych w postaci ciągu znaków ASCII. Dzięki kodowaniu base64 dane binarne są konwertowane na ciąg znaków, które mogą być przesłane przez sieć jako zwykły tekst.  
Algorytm base64 używa 64 znaków do kodowania danych. Są to litery alfabetu łacińskiego (wielkimi i małymi literami), cyfry oraz kilka znaków specjalnych. Każde 3 bajty danych są kodowane jako 4 znaki base64. Jeśli liczba bajtów danych nie jest podzielna przez 3, to są one uzupełniane dodatkowymi znakami "=", aby zapewnić pełne grupy po 3 bajty.
