# Bash - podstawowe komendy ściągawka


## Szukanie pomocy
Sprawdzanie co jest czym oraz do czego służy
- man - manual
- apropos - wyszukujemy nim słów kluczowych (np w opisach programów etc)
- whatis -
- file - opisuje typ pliku


## Wyrażenia regularne

- `*` - zastępuje dowolny ciąg znaków
- `?` - 
- 

## Pliki
### Szukanie plików
```bash
find -name a*n.java
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


#### Dzielenie dłuższych łańcuchów znaków
```bash
cut 

```
```bash


```
```bash
TODO

```






## Argumenty

TODO


## Procesy

Łączniki:

 - `&&` -wykonaj kolejny proces, jeśli poprzedni się powiedzie (retcode 0)
 - `||` - wykonaj następny, gdy poprzedni to porażka
 - `&` - proces jest utuchamiany w tle (jego pid można zdobyć za pomocą `$!`)

TODO więcej



## Warunki

Warunki sprawdza się za pomocą komenty `test` z odpowiednimi flagami.  
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

| Operator                |Description       |
|-------------------------|------------------|
| ! EXPRESSION            |The EXPRESSION is false.|
| -n STRING               |The length of STRING is greater than zero.|
| -z STRING               |The lengh of STRING is zero (ie it is empty).|
| STRING1 = STRING2       |STRING1 is equal to STRING2|
| STRING1 != STRING2      |STRING1 is not equal to STRING2|
| INTEGER1 -eq INTEGER2   |INTEGER1 is numerically equal to INTEGER2|
| INTEGER1 -gt INTEGER2   |INTEGER1 is numerically greater than INTEGER2|
| INTEGER1 -lt INTEGER2   |INTEGER1 is numerically less than INTEGER2|
| -d FILE                 |FILE exists and is a directory.|
| -e FILE                 |FILE exists.|
| -r FILE                 |FILE exists and the read permission is granted.|
| -s FILE                 |FILE exists and it's size is greater than zero (ie. it is not empty).|
| -w FILE                 |FILE exists and the write permission is granted.|
| -x FILE                 |FILE exists and the execute permission is granted.|

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





```bash
TODO

```


