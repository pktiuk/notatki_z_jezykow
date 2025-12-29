# Protobuf

[protobuf.dev](https://protobuf.dev/)
[Repo protobufa](https://github.com/protocolbuffers/protobuf)

Protocol Buffers (w skrócie Protobuf) to opracowany przez Google mechanizm służący do serializacji danych strukturalnych. Można go porównać do formatów takich jak XML czy JSON, ale z jedną kluczową różnicą: Protobuf jest mniejszy, szybszy i prostszy.

Zamiast przesyłać dane w formie tekstowej (którą człowiek może łatwo odczytać), Protobuf zamienia je na format binarny.

## Działanie

Pracując z protobufem najpierw definiujesz plik `.proto`, w którym opisujesz, jak wyglądają Twoje dane.   

```proto
syntax = "proto3";

message Person {
  string name = 1;
  int32 id = 2;
  string email = 3;
}
```

Następnie kompilujesz go za pomocą kompilatora takiego jak `protoc`.   

```bash
protoc --proto_path=IMPORT_PATH --cpp_out=DST_DIR --java_out=DST_DIR --python_out=DST_DIR --go_out=DST_DIR --ruby_out=DST_DIR --objc_out=DST_DIR --csharp_out=DST_DIR path/to/file.proto
```

Potem korzystasz już z klas wygenerowanych dla twojego języka (`C++`, `Python`, `Java` etc.).

```java
// Java code
Person john = Person.newBuilder()
    .setId(1234)
    .setName("John Doe")
    .setEmail("jdoe@example.com")
    .build();
output = new FileOutputStream(args[0]);
john.writeTo(output);
```

## Proto Syntax

Ogólny przykład.

```proto
edition = "2023"; //opis wersji protobuffa

enum SearchType {
    REGULAR = 0;
    FULLTEXT = 1;
}

message SearchRequest {
  reserved 4, 6 to 8;

  string query = 1;
  int32 page_number = 2 [default = 1];
  int32 results_per_page = 3;
  User user = 5;
  SearchType type = 6 [default = REGULAR];
}
```

- `edition` (lub `syntax`)- opisuje wersję definicji proto
- `message` oznacza strukturę, każda struktura może zawierać wiele pól takich jak:
  - [scalar](https://protobuf.dev/programming-guides/editions/#scalar), czyli podstawowe wartości jak string, int bool etc
  - inne struktury proto(patrz `user`, `type`) - czyli inne już zdefiniowane elementy
  - `repeated` - listy
  - [`map`](https://protobuf.dev/programming-guides/editions/#maps) - czyli słowniki
- `reserved` wskazuje jakie numery pól są zajęte i nie powinny być używane 

Przy tworzeniu wiadomości niezwykle waśne są numery pól, które muszą być unikalne i nie mogą być reużywane po skasowaniu pola.

### Inne pola w strukturach

```proto
/* możliwe jest zaimportowanie elementów z innych plików proto*/
import "google/protobuf/any.proto";

message SimpleMes{
    // może być tutaj przechowywana zmienna dowolnego typu
    google.protobuf.Any payload = 1;
      oneof test_oneof {
    string name = 4;
    SubMessage sub_message = 9;
  }
}

message Division{
    map<string, Project> projects = 3;
    repeated User employees = 4;
}
```

- [oneof](https://protobuf.dev/programming-guides/editions/#oneof)
- repeated
- map

### Inne specyfikatory

[**Packages**](https://protobuf.dev/programming-guides/editions/#packages) - pozwalają określać przestrzenie nazw, aby unikać konfliktów

```proto
package foo.bar;

// Uzywając odwołujemy się do foo.bar.Open
message Open { ... }
```

[**Options**](https://protobuf.dev/programming-guides/editions/#options) - poszczególne adnotacje w proto mogą być także adnotowane z pomocą słowa `option`. Najczęściej wpływają one na zachowanie kompiatora.  
Niektóre opcje umieszcza się w nagłówku pliku, ponieważ wpływają na wszystkie definicje. Jak np:
- `option java_package = "com.example.foo"` - nazwa paczki java która ma zawierać definicje z tego pliku
- `option optimize_for = CODE_SIZE;`

Inne zaś umieszcza się przy popszczególnych polach jak np:
- `default` dla domyślnych wartości (`int x = 1 [default = 5];`)
- `deprecated` (`int32 old_field = 6 [deprecated = true];`)

Możliwe jest też adnotowanie wartości enumów

```proto
import "google/protobuf/descriptor.proto";

extend google.protobuf.EnumValueOptions {
  string string_name = 123456789;
}

enum Data {
  DATA_UNSPECIFIED = 0;
  DATA_SEARCH = 1 [deprecated = true];
  DATA_DISPLAY = 2 [
    (string_name) = "display_value"
  ];
}
```

## Definiowanie API i seriwisów

Poza samymi strukturami danych proto może być także używane do definiowania serwisów RPC. [link](https://protobuf.dev/programming-guides/editions/#services) 

```proto
service SearchService {
  rpc Search(SearchRequest) returns (SearchResponse);
}
```

Najlepiej wspierany jest tutaj gRPC od Googla.

TODO options, adnotacje, importy, extensions, package, 
