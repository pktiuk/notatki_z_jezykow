# Praca z GDB

## Kompilacja z flagami debugowymi

W wypadku najprostszych aplikacji kompilowanych za pomocą gcc g++ wystarczy dodanie flagi `-g`

```bash
gcc -g hello.c
```

## Uruchomienie aplikacji za pomocą GDB

Aby uruchomić aplikację z pomocą debugera wystarczy wpisać:

```bash
gdb a.out
```

Wtedy uruchamiamy nasz program w trybie terminalowym.

## Praca ze zrzuconą pamięcią (coredump)

### Przygotowania

Do stworzenia zrzutu często należy zwiększyć ilość dozwolonej ilości pamięci:  
 `ulimit -c unlimited`

Kompilujemy nasz program z flagami debugowymi: - **Cmake** - `cmake .. -DCMAKE_BUILD_TYPE=Debug && cmake --build .` - **make** - TODO

### Zbieranie stosu

Na ogół zrzuty ze stosu są pzechowywane w folderze `/var/crash` są to pliki z rozszerzeniem .crash  
Np `_usr_share_teams_teams.1000.crash` = "http://127.0.0.1:5000/";
// let url2 = "https://httpbin.org/post";

// xhr.open("POST", url, true);
// xhr.setRequestHeader("Content-Type", "application/json");
// xhr.onreadystatechange = function () {
// console.log("Jest git");
// console.log(this.responseText);
// };
// var data = JSON.stringify({ name: "xxx", code: "xx=12" });
// xhr.send(data);

### Analiza (w terminalu)

Uruchomienie `gdb ./plik/wykonywalny ./plik/zrzutu/core`

`backtrace` / `bt full` - pokazywanie stanu stosu
