# Terminal - podstawowe komendy i koncepty

## Szukanie pomocy

Sprawdzanie co jest czym oraz do czego służy

- man - manual
- apropos - wyszukujemy nim słów kluczowych (np w opisach programów etc)
- whatis -
- file - opisuje typ pliku

## Wyrażenia regularne

[link do regexów](./regex.md)

## Pliki

### Uprawnienia plików

Każdy plik w linuxie  ma swoje uprawnienia, które są podzielone na trzy grupy:

- właściciel `u`
- grupa `g`
- inni `o`

Każda z tych grup ma swoje uprawnienia do pliku, które są podzielone na:

- odczyt `r`
- zapis `w`
- wykonanie `x`

Poza tym są też specjalne uprawnienia:

- `s` - setuid (gdy dla właściciela), setgid (gdy dla grupy), sticky bit - jest to flaga, która może mieć różne efekty w zależności od tego, czy jest ustawiona na piku, czy nafolderze. [przykład](https://askubuntu.com/questions/313089/how-can-i-share-a-directory-with-an-another-user)
  - na pliku wykonywalnym - jeśli jest ustawiona to plik będzie wykonywany z uprawnieniami właściciela pliku, a nie osoby, która go uruchomiła. Tzn może być używana do uruchamiania aplikacji z uprawnieniami roota, nawet jeśli się nim nie jest.
  - na folderze - jeśli setgid jest ustawiony na folderze, to każdy plik stworzony w tym folderze będzie miał grupę ustawioną na grupę folderu, a nie grupę użytkownika, który go stworzył.

??? Przykładowe korzystanie ze sticky bitów

    Wartość `0770` wszyscy w grupie mogą dodawać, usuwać i czytać sobie nawzajem pliki w folderze, ale nie mogą sobie nawzajemi pisać.

    ```bash
    sudo chmod 0770 folder
    ``` 

    Wartość `1770` daje takie uprawnienia jak wyżej z tą różnicą, że tylko właściciel pliku może go usunąć.

    ```bash
    sudo chmod 1770 folder
    ```

    Wartość `2770` oznacza, że wszyscy użytkownicy grupy mogą dodawać, czytać, zadpisywać i usuwać sobie nawzajem pliki w folderze.

    Wartość `3770` oznacza to samo co wyżej z tą różnicą, że tylko właściciel może usuwać pliki.

    pierwsza cyfra jest wynikiem sumowania `sticky bit + 2 * setgid`

```bash
ls -l
#-rw-r--r-- 1 user privileged_users 0 Oct  9 12:00 plik.txt
```

Pierwszy znak to typ pliku, a kolejne trzy grupy to uprawnienia dla właściciela, grupy i innych.
Czyli przykładowy ciąg `-rw-r--r--` można rozpisać na

- pierwszy bit jako `-` (plik zwykły) (może być też `d` dla folderów) 
- właściciela jako `rw-` 
- grupę jako `r--` 
- i innych jako `r--`.

Można to także przedstawić w formacie zapisu liczbowego, gdzie każda grupa ma swoją wartość: `r=4`, `w=2`, `x=1`.

```bash
#-rw-r--r--
# 110 100 100
# 6   4   4
```

Ten zapis może być wykorzystywany chociażby przez komendę `chmod`, która przyjmuje różne waroanty argumentów [link](https://docs.nersc.gov/filesystems/unix-file-permissions/).

```bash
chmod 777 plik.txt #nadanie pełnych uprawnień wszystkim
chmod 755 plik.txt #nadanie pełnych uprawnień właścicielowi, a grupie i innym tylko odczytu i wykonania

# zapis zmieniający uprawnienia
chmod u+x plik.txt #dodanie uprawnień do wykonania dla właściciela
chmod u-x plik.txt #usunięcie uprawnień do wykonania dla właściciela
chmod g+rw plik.txt #dodanie uprawnień do odczytu i zapisu dla grupy
```



### Szukanie plików

```bash
find -name a*n.java
```

### Rozmiary folderów

domyślne `ls` ni pokauje rozmiarów folderów. Do tego należy użyć komandy `du`

```bash
du -s /home/ja
```

Przydatne flagi:

- `-s` -pokaż tylko wybrany folder bez podfolderóœ
- `-h` - human readable, zaokrągla do GB, MB etc.
- `--max-depth=2` - maksymalna głębokość przy pokazywaniu podfolderów

Alternatywnie do badania struktury katalogów można użyć `tree`

```bash
tree --du -h -d
```

Flagi:

- `-d` - wyświetl tylko foldery
- `--du` - podlicz rozmiary folderów
- `-h` podawaj rozmiary w czytelnym formacie

### Pisanie do plików

Każda aplikacja ma wejście (`stdin`) oraz dwa wyjścia (`stdout`-zwykłe i `stderr`-dla błędów)

Z pomocą poniższych komend możemy przekierowywać wyjścia programów do urządzeń lub plików

| Komenda     | Działanie                                                    |
| ----------- | ------------------------------------------------------------ |
| `<`         | deviceredirects stdin to the device                          |
| `>>`        | deviceredirects stdout to the device (appends to the end)    |
| `>` device  | redirects stdout to the device (overwrites previous content) |
| `2>` device | redirects stderr to the device (overwrites previous content) |
| `2>&1`      | redirects stderr to the device associated to stdout          |

```bash
cat logi.log | grep "10-10-2022" > logs_from_10-10-2022.log
```

## Obróbka tekstu

#### Wyszukiwanie wzorca

```bash
cat PLIKI | grep wyszukiwane_slowo
```

```bash
grep -r . #przeszukanie wszystkich plików (nawet binarnych) w danym folderze
```

strings służy do wypisywania stringów z plików binarnych (dobrze współdziała z grep)

```bash
strings PLIK
```

Inne przydatne flagi grepa

|                              |                                                    |
| ---------------------------- | -------------------------------------------------- |
| `-v` `--invert-match`        | odwrócony grep, przekazuje tylko to, co nie pasuje |
| `-B`, `--before-context=ILE` | Wypisz ILE linii po przed znaleziskiem wyświetlić  |
| `-A`, `--after-context=ILE`  | Wypisz ILE linii po znalezisku wyświetlić          |

### Dzielenie dłuższych łańcuchów znaków

`cut` - proste wycinanie fragmentów tekstu

- `-b` byte - wydziela poszczególne bajty

```bash
echo "abcdefgh" | cut -b 1,3,5-6
# acef
```

```bash
echo "qwer tyui xxx" | cut -d " " -f 2 #-d delimiter (separator) -f pole
#tyui
```

`-f` przyjmuje liczby w następujących formatach: `N`, `N-M`, `-M`, `N-`, `X,Y,Z`

`head` - służy do pokazywania tylko wybranych linii.

```bash
cat ./dlugi_plik.log | head -n 100 #drukuje tylko 100 pierwszych linii
```

W wypadku, gdy chcemy wydzielić samą nazwę pliku ze ścieżki warto użyć komendy `basename`

```bash
basename /sciezka/do/pliku/plik.txt
# plik.txt
```

### Manipulacja tekstem

`sed` służy do nieco bardziej zaawansowanych manipulacji

```bash
echo "abcdefbc" | sed "s/bc/BC/" # zamień pierwszy pasujący ciąg (bc) na BC
#aBCdefbc
```

```bash
TODO

```

## Zmienne

Zmienną tworzymy za pomocą znaku `=`, który przypisuje wartość do dane identyfikatora. `identyfikator=wartość`.  
Aby uzyskać dostęp do zawartości używamy `$` przed nazwą zmiennej.

```bash
$ msg=”Hello World”
$ echo $msg
Hello World
```

### Wstawianie zmiennych w tekst

Jest kilka sposobów, aby mieć w sktyptach tekst, który jest zależny od sytuacji. Możemy do tego wykorzystywać:

- Zmienne `/my/path/to/${EDITED_FILE}`
- Wyniki funkcji ` dsd
-

## Argumenty

Każda funkcja, czy też skrypt bashowy może mieć przekazywane poprzez proste podanie ich po wywołaniu.

Dla skryptu:

```bash
#!/bin/bash

wyprintuj_argument()
{
    #tutaj odwołujemy się do pierwszego argumentu przekazanego do funkcji
    #a nie do skryptu
    echo "argument $1"
}

wyprintuj_argument $1
wyprintuj_argument $2
```

przy wywołaniu `./skr.sh Hello 222`
Otrzymamy

```bash
argument Hello
argument 222
```

Zwroty przydatne przy obsłudze argumentów

|          |                                                  |
| -------- | ------------------------------------------------ |
| $0       | Nazwa wołanej komendy/skryptu                    |
| $1 $2 $3 | poszczególne argumenty (pierwszy, drugi, trzeci) |
| $#       | Liczba argumentów                                |
| $\*      | Wszystkie argumenty jako jeden string            |
| $@       | Wszystkie argumenty jako lista                   |

### xargs

Jeśli chcemy wykorzystywać wyjścia mechanizm strumieni do przekazywania argumentów to możemy użyć także komendy [xargs](https://man7.org/linux/man-pages/man1/xargs.1.html)

```bash
#Wywołanie komendy rm dla każdego znalezionego pliku
find /path -type f -print | xargs rm
```

Flagi:

- `-n` - maksymalna liczba argumentów
- `-d`, `--delimiter` - podział na części (komenda zostanie wywołana wielokrotnie)

```bash
echo -n 123-456-7890 | xargs echo
#> 123-456-7890
echo -n "123-456-789" | xargs -n 1 -d - echo
#> 123
#> 456
#> 789
```

- `-I`, `-i`, `--replace=` pozwala na elastyczne wstawianie otrzymanego argumentu

```bash
#Stworzy pliki 123.txt 456.txt 789.txt
echo -n "123-456-789" | xargs -d - -n 1 -I{} echo {}.txt
```

## Procesy

Łączniki:

- `&&` -wykonaj kolejny proces, jeśli poprzedni się powiedzie (retcode 0)
- `||` - wykonaj następny, gdy poprzedni to porażka
- `&` - proces jest utuchamiany w tle (jego pid można zdobyć za pomocą `$!`)

TODO więcej

## Warunki

Warunki sprawdza się za pomocą komendy `test` z odpowiednimi flagami.
Można to także robić za pomocą wmieszczając warunek w nawiasach `[]`.
Możliwy jest też wariant z dwoma nawiasami `[[ cośtam ]]` jest on wspierany przez wszystkie nowsze systemy używające Basha, ale mimo wszystko może byc on niekompatybilny ze starszymi.

Warto pamiętać, że bardzo ważne tu są spacje i aby o nich nie zapomnieć.

Samo `test` jako komenda nie robi nic po prostu sprawdza warunek i zależnie od niego zwraca jakiś kod.

```bash
[ 1 -gt 100 ]
echo "Ret: $?" #zwraca kod ostatnio działającej aplikacji
# Ret: 1

[ 100 -gt 1 ]
echo "Ret: $?"
# Ret: 0
```

| Operator              | Description                                                           |
| --------------------- | --------------------------------------------------------------------- |
| ! EXPRESSION          | The EXPRESSION is false.                                              |
| -n STRING             | The length of STRING is greater than zero.                            |
| -z STRING             | The lengh of STRING is zero (ie it is empty).                         |
| STRING1 = STRING2     | STRING1 is equal to STRING2                                           |
| STRING1 != STRING2    | STRING1 is not equal to STRING2                                       |
| INTEGER1 -eq INTEGER2 | INTEGER1 is numerically equal to INTEGER2                             |
| INTEGER1 -gt INTEGER2 | INTEGER1 is numerically greater than INTEGER2                         |
| INTEGER1 -lt INTEGER2 | INTEGER1 is numerically less than INTEGER2                            |
| -d FILE               | FILE exists and is a directory.                                       |
| -e FILE               | FILE exists.                                                          |
| -r FILE               | FILE exists and the read permission is granted.                       |
| -s FILE               | FILE exists and it's size is greater than zero (ie. it is not empty). |
| -w FILE               | FILE exists and the write permission is granted.                      |
| -x FILE               | FILE exists and the execute permission is granted.                    |

Dopiero po połączeniu z wyrażeniami warunkowymi się przydaje.

**Uwagi**

- `=` oraz `-eq` działają inaczej np `01 = 1` da fałsz, ale `01 -eq 1` da prawdę

### Warunki if

```bash
 #nie musi tu być koniecznie test, może to być dowolna. Jeśli zwraca ona 0 to mamy sukces i wchodzimy do środka
if apka_zwracająca_jakiś_kod
then
    komendy
fi

#wariant z else
if apka_zwracająca_jakiś_kod
then
    komendy
else
    inne komendy
fi
```

### Pętle

**for** - iteruje po liście

```bash
for variable in valuelist
do
    something
done
```

Listą mogą być argumenty programu

```bash
#!/bin/bash
echo The number of arguments is: $#
echo The entered command line is: $0 $@
echo The command arguments are:
for i in "$@"
do
    echo $i
done
```

... albo pliki w folderze

```bash
for k in *
do
    cp $k $k.bak
    echo $k copy created
done
```

lub wynik komendy (używamy do tego `$()`)

```bash
for i in $(ls)
do
    echo $i
done
```

//TODO opis skrótów klawiszowych Ctrl-C Ctrl-D etc
// https://www.howtogeek.com/howto/ubuntu/keyboard-shortcuts-for-bash-command-shell-for-ubuntu-debian-suse-redhat-linux-etc/
