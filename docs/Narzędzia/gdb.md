# Używanie GDB


## Analiza zrzutów pamięci

### Przygotowania
Do stworzenia zrzutu często należy zwiększyć ilość dozwolonej ilości pamięci:  
 `ulimit -c unlimited`


Kompilujemy nasz program z flagami debugowymi:
    - **Cmake** - `cmake .. -DCMAKE_BUILD_TYPE=Debug &&  cmake --build .`
    - **make** - TODO


### Analiza (w terminalu)
Uruchomienie `gdb ./plik/wykonywalny ./plik/zrzutu/core`

`backtrace` / `bt full` - pokazywanie stanu stosu