# PythonNotatki

## I

### Shebang

Jest to pierwsza linia skryptu (nie tylko w pythonie), która określa za pomocą czego ma być wykonany skrypt (może być to bash, zsh, python)
Mamy tutaj 2 możliwości:

Ta bardziej uniwersalna (działa z wieloma systemami operacyjnymi)

```python
#!/usr/bin/env python3
```

Ta mniej uniwersalna, ale pozwalająca używać pythona z różnymi parametrami

```python
#!/usr/bin/python3
```

Np z po dodaniu parametru `-i` nadal pozostaniemy w pythonie po wykonaniu skryptu, co pozwoli nam np zajrzeć do zmiennych, które były użyte, lub łatwo użyć klas, albo metod, które zostały zdefiniowane w skrypcie.

### Funkcja main

wykonuje się, gdy skrypt jest uruchamiany jako samodzielny program, a nie jako moduł czegos innego

```python
#!/usr/bin/python3 #warto to dać, aby system widział, że to skrypt w pythonie a nie np. w shellu
def main():
    print("Witaj świecie!")

if __name__ == "__main__":
    main()
```

#### Argumenty programu

```python
# Print total number of arguments
print ('Total number of arguments:', format(len(sys.argv)))

# Print all arguments
print ('Argument List:', str(sys.argv))

# Print arguments one by one
print ('First argument:',  str(sys.argv[0]))
print ('Second argument:',  str(sys.argv[1]))
```

#### Zwracanie wartości

```python
sys.exit(numer)
```

### Funkcje we/wy

```python
pobrany_napis = input()
print("Twój napis to: " + pobrany_napis)
```

 input() jest funkcją, która pobiera napis podany przez użytkownika ze standardowego wejścia (do entera) zwraca zmienną typu str

 Dla strumieni:

```python
import sys

for line in sys.stdin:
    sys.stdout.write(line)
```

## II

### Komentarze

```python
"""
Komentarz na
kilka linii
"""
#komentarz na jedną linię
```

### Zmienne

Deklarujemy je be określania ich typu `a=5` (interpreter automatycznie uzna, że to będzie int)
W odróżnieniu od takich języków jak C++, C# czy Java, w języku Python występuje typowanie dynamiczne. Oznacza to, że konkretny identyfikator, konkretna zmienna, np. a, może raz przechowywać napis ("Ala ma kota") by po chwili przechowywać liczbę całkowitą (3).
Do sprawdzania typu danych służy funkcja `type()`.

```python
logiczna = True
print(type(logiczna))
## <class 'bool'>
```

Najważniejsze typy zmiennych:
`bool`, wartość logiczna, tak lub nie, prawda (True) albo fałsz (False)
`int`, liczba całkowita, np. -7, 0 czy 3:
`float`, czyli wartość zmiennopozycyjna, można ją utożsamiać z wartościami rzeczywistymi, np. -0.67, 1.0, 3.14
`complex`, czyli liczba zespolona, np. -7+8.5j. Warto pamiętać, że w Pythonie jednostką urojoną jest j, a nie i
`str`, powszechnie znany w innych językach jako string, czyli napis. Napis poznajemy głównie po tym, że jest zapisany w cudzysłowie (i to odróżnia go choćby od nazwy zmiennej czy liczby, które nie są w cudzysłowach). Dodamy, że w języku Python nie ma znaczenia, czy posługujemy się pojedynczymi (') czy podwójnymi (") cudzysłowami

Konwersja typów analogiczna dla przykładu poniżej

```python
print(int(5.3))
## 5
```

Operatory:

- dodawanie (`+`)
- odejmowanie (`-`)
- mnożenie (`*`)
- dzielenie (`/`)
- reszta z dzielenia, modulo (`%`)
Analogiczne co C operatory `-=`, `*=`, `/=`, `%=`...
UWAGA! Brak operatorów `++` i `--`

Operatory Logiczne zwracają wartość logiczną (True/False)

- `<` - mniejsze
- `<=` - mniejsze równe, zwróćmy uwagę, że zapisujemy tak jak czytamy, nie ma operatora =< (równe mniejsze)
- `>` - większe
- `>=` - większe równe
- `==` - równa się. Tutaj bardzo ważne jest, aby odróżniać operator przypisania (=) od operatora porównania równa się (==). To bardzo częsty błąd wśród początkujących programistów. Operator = nie jest symetryczny, ma na celu przekopiowanie wartości z prawej do lewej. W niektórych językach zapisuje się go jako <- (ale nie w Pythonie). Operator = nie ma nic wspólnego z wartościami logicznymi. Za to operator == jest operatorem zwracającym wartość logiczną, a co więcej, jest on operatorem symetryczym (nie ma znaczenia zamienienie kolejnością argumentów).
- `!=` - nie równa się
Operator koniunkcji, `and`, utożsamiany z polskim i. Zwraca wartość True wtedy i tylko wtedy, gdy oba argumenty są równe True
Operator alternatywy, `or`, utożsamiany z polskim lub. Zwraca wartość True wtedy i tylko wtedy, gdy przynajmniej jeden argument jest równy True
Operator zaprzeczenia, `not`, utożsamiany z polskim nie. Zwraca wartość przeciwną, niż argument

Można łączyć kilka operatorów np:
`czy_wiek_produkcyjny = 18 <= wiek <= 65` - w pythonie porównania rozwijane są tak jak w matematyce, czyli np możemy też napisać `2 <= 4 < 8`, co zwróci nam `True`

Inne operatory:

- `is` - czy dwie zmienne są różnymi instancjami tego samego obiektu

```python
s1={}
s2={}

s1==s2
#True

s1 is s2
#False ##ponieważ to nie jest ten sam słownik
```

- `in` używany do sprawdzenia, czy dana wartość/obiekt zawiera się w liście/słowniku/secie...

```python
zbior = {1, 3, 5}
zbior_pusty = {}

print(1 in zbiorPusty)
## False
print(1 in zbior)
## True
```

Instrukcja warunkowa if

```python
if warunek:
    instrukcja1
    instrukcja2
elif warunek2: # gdy warunek nieprawdziwy, sprawdz warunek2
    instrukcja3
    instrukcja4
elif warunek3: #gdy warunek2 nieprawdziwy, sprawdz warunek3
    instrukcja5
    instrukcja6
else: #gdy zaden z warunkow nie byl prawdziwy
    instrukcja7
    instrukcja8
```

#### Pusta zmienna

Czasem `_` jest używane jako pusta zmienna jest to swego rodzaju odpowiednik `/dev/null`

TODO dopisać i omówić przykłady:
<https://stackoverflow.com/questions/5893163/what-is-the-purpose-of-the-single-underscore-variable-in-python>

### Pętle

Po `for` (`foreach`) może się znajdować lista (obrót dla każdego elementu)
Po while warunek logiczny (obroty dopóki prawda)

```python
for i in range(0, 4):
print(i)

## 0
## 1
## 2
## 3

#lub
i = 0
while i < 4:
print(i)
i+=1

liczby = [2, 3, 5]
for liczba in iczby:
print(liczba)
## 2
## 3
## 5
```

Słowo kluczowe `continue` przerywa dany obrót pętli
Słowo kluczowe `break` przerywa całą pętlę

Jeśli iterujemy po liście krotek możemy sobie je rozbić

```python
for i, line in enumerate(strings_list): #enumerate zwraca dla danej listy krotkę zawierającą numer i element z listy
    ###jakiś kod
```

**Pętle jednolinijkowe (List Comprehensions)**
Jednolinijkowe pętle zwracające np listę dobre dla prostych operacji

```python
newlist = [expression for item in iterable if condition == True]
#albo bez if-a
newlist = [x for x in range(10)]

fruits = ["apple", "banana", "cherry", "kiwi", "mango"]
newlist = []

for x in fruits:
  if "a" in x:
    newlist.append(x)

#daje to samo co:

newlist = [x for x in fruits if "a" in x]
```

## III

### Krotka (tuple)

Pewną specyficzną dla języka Python strukturą jest krotka. Polega ona na grupowaniu paru wartości w jeden byt. Warto zaznaczyć, że krotka, która raz została stworzona, nie może być modyfikowana: nie możemy podmienić jednej ze składowych krotki

```python
krotka = (2,3)
print(krotka)
## (2, 3)
```

Gdybyśmy chcieli uzyskać poszczególne składowe krotki, możemy to zrobić przy użyciu operatora kwadratowych nawiasów. W Pythonie, tak jak w wielu językach programowania, numerujemy składowe od 0:

```python
pierwsza = krotka[0]
druga = krotka[1]
print(pierwsza)
## 2
print(druga)
## 3
W krotce możemy mieszać typy danych:
krotka = (2, "Napis")
print(krotka)
## (2, 'Napis')
len(krotka) #dlugosc krotki
## 2
```

Kiedy krotka może być przydatna? Np. gdy chcemy zwrócić więcej niż jedną wartość w funkcji.

```python
def f(x):
    y0 = x + 1
    y1 = x * 3
    y2 = y0 ** y3
    return (y0, y1, y2)
```

Jeśli chcemy możemy rozbić krotkę na poszczególne zmienne

```python
a,b,c = (1,2,3)
```

#### named tuple

Specjalne obiekty działające jak krotki i kompatybilne z nimi.

```python
from collections import namedtuple
Point = namedtuple('Point', 'x y')
pt1 = Point(1.0, 5.0)
pt2 = Point(2.5, 1.5)

from math import sqrt
# wskazanie poprzez indeks
line_length = sqrt((pt1[0]-pt2[0])**2 + (pt1[1]-pt2[1])**2)
 # rozpakowanie krotki
x1, y1 = pt1
```

#### Funkcja zip

Do operowania na krotkach przydatna jest funkcja wbudowana `zip` zwracająca iterator (nie listę) pozwalacjący iterować po protkach tworzonych z obiektów danych w funkcji.

```python
a = ("John", "Charles", "Mike")
b = ("Jenny", "Christy", "Monica", "Vicky") # wartości nadmiarowe są pomijane

for kr in zip(a, b):
    print(kr)

#('John', 'Jenny')
#('Charles', 'Christy')
#('Mike', 'Monica')
```

### Lista

Podobną, przynajmniej na pozór, strukturą danych do krotki jest lista. Tutaj także możemy grupować dane oraz nie muszą one być tego samego typu. Jednak główną różnicą jest to, że listę możemy modyfikować. Możemy dodawać nowe elementy czy zastępować dotychczasowe.

```python
lista = [1, False, "Napis"]
print(lista)
## [1, False, 'Napis']
print(len(lista))
## 3
lista.append(2.5+3.7j)
print(lista)
## [1, False, 'Napis', (2.5+3.7j)]
lista.extend([97,98,99]) # metoda podobna po append, która przyjmuje jako argument całą listę i dodaje z niej kolejne elementy
print(lista)
## [1, False, 'Napis', (2.5+3.7j), 97, 98, 99]
```

Operatory `+` i `*` mają zdefiniowane działanie w kontekście list.
`+`, tak jak w przypadku napisu, to konkatenacja, czyli połączenie dwóch list w jedną
`*` zaś pozwala nam powielić daną listę:

```python
print(lista + [7,8,9])
## [1, False, 'Napis', (2.5+3.7j), 97, 98, 99, 7, 8, 9]
print([7,8,9] * 3)
## [7, 8, 9, 7, 8, 9, 7, 8, 9]
```

Odwołanie się do konkretnego elementu następuje tak jak w krotce:

```python
print(lista[2])
## Napis
! ujemne indeksy oznaczają pozycje liczone od tyłu
print(lista[-1])
## 99
Odwoływanie się do wycinka listy
print(lista[2:5])
## ['Nowy', (2.5+3.7j), 97]
Elementy o numerach 2, 3, 4 (bez 5)
```

Podmiana

```python
lista[0:3] = [98,99,101,102]
print(lista)
## [98, 99, 101, 102, (2.5+3.7j), 97, 98, 99]
```

Usuwa 3 pierwsze elementy i na ich miejsce wstawia te podane

Wstawienie elementu w innym miejscufor klucz in bazaDanychPolakow.keys():

```python
print(klucz)

for wartosc in bazaDanychPolakow.values():
print(wartosc)

for klucz, wartosc in bazaDanychPolakow.items(): ##Tutaj items() zwraca krotkę
print(klucz)
print(wartosc)
print("-----")


lista.insert(1, "Nowy2")
print(lista)
## [98, 'Nowy2', 99, 101, 102, (2.5+3.7j), 97, 98, 99]
Usunięcie elementu
del lista[1]
print(lista)
## [98, 99, 101, 102, (2.5+3.7j), 97, 98, 99]
Napisy
Zmienna w napisie
zmienna = 7
napis = f"wartość zmiennej to {zmienna}"
print(napis)
## wartość zmiennej to 7
wieleWierszy = """Tutaj pierwszy
a tu drugi
tutaj trzeci"""
print(wieleWierszy)
## Tutaj pierwszy
## a tu drugi
## tutaj trzeci
```

Kolejność alfabetyczna

```python
print("a" < "b")
## True
```

Więcej na:
<https://www.kodolamacz.pl/blog/wyzwanie-python-3-algorytmy-i-struktury-danych/>

### Zbiór (set)

to tablica (tyle, że bez indeksowania), w których nie ma dwóch lub więcej identycznych elementów. (jest szybszy od listy)

```python
zbiorPusty = set()
zbior = {1, 3, 5}
print(zbiorPusty)
## set()
print(zbior)
## {1, 3, 5}
zbior.add(2) ##Dodawanie elementu
zbior.discard(2) ##Usuwanie elementu
Można w nim łatwo sprawdzać, czy dany element należy do zbioru
print(1 in zbiorPusty)
## False
print(1 in zbior)
## True
print(1 not in zbiorPusty)
## True
```

Możemy na nich wykonać typowe operacje teoriomnogościowe, jak suma, różnica czy przecięcie dwóch zbiorów

```python
print({1,5,8} | {1,5,9}) # suma
## {1, 5, 8, 9}
print({1, 5, 8} - {1, 5, 9}) # różnica

## {8}
print({1, 5, 8} & {1, 5, 9}) # przecięcie
## {1, 5}
Można zapytać, czy jeden zbiór jest podzbiorem drugiego
print({1, 5}.issubset({1, 5, 9}))
## True
```

### Słownik

Jest to rozszerzenie idei zbioru.
Słownik zawiera pary klucz-wartość. Wyszukiwanie po kluczu jest szybkie, tak jak w zbiorze, jednak gdy już odnajdziemy klucz, możemy odzyskać także stowarzyszoną z nim wartość. Gdy usuniemy ze słownika wartości, a zostawimy same klucze, otrzymamy zbiór. Tak jak w zbiorze, w słowniku klucze nie mogą się powtarzać.

```python
bazaDanychPolakow = {"89082911111" : ["Jan", "Kowalski", 29],
"95092200000" : ["Ania", "Nowak", 23],
"98122422222" : ["Adam", "Mickiewicz", 220]
}
bazaDanychPolakow["88081244444"] = ["Magda", "K", 30] #Dodanie nowej pary klucz-wartość
del bazaDanychPolakow["88081244444"] #Usunięcie danej pary
```

Tak jak w zbiorze możemy sprawdzać, czy klucz znajduje się w słowniku.

Uzyskanie wartości stowarzyszonej z kluczem

```python
print(bazaDanychPolakow["98122422222"])
## ['Adam', 'Mickiewicz', 220]
Gdy chcemy zabezpieczyć się przed odwołaniem do nieistniejącego elementu (i w tym wypadku zwrócić wartość domyślną), użyjemy metody get():
print(bazaDanychPolakow.get("89082911111", "wartość domyślna"))
## ['Jan', 'Kowalski', 29]
print(bazaDanychPolakow.get("95092200022", "wartość domyślna"))
## wartość domyślna
```

Przejście w pętli

```python
for klucz in bazaDanychPolakow.keys():
print(klucz)

for wartosc in bazaDanychPolakow.values():
print(wartosc)

for klucz, wartosc in bazaDanychPolakow.items(): ##Tutaj items() zwraca krotkę
print(klucz)
print(wartosc)
print("-----")
```

Przy printowaniu słowników (zwłaszcza tych skomplikowanych) warto użyć `pprint`

```python
import pprint
pprint.pprint(duzy_slownik)
```

## IV

### Funkcje

Funkcje

```python
def nazwaFunkcji(parametry, oddzielone, przecinkami):
return wynik
Wartości domyślne parametrów
def potega(podstawa, wykladnik=1):
#ciało funkcji
Argumenty nazwane Możemy podawać argumenty w dowolnej kolejności, gdy podamy ich nazwy
print(potega(wykladnik = 4, podstawa = 3))
## 81
```

```python
def printinfo( name, age = 35 ):
   "Prosta funkcja z domyślnymi wartościami"
   print("Name: ", name)
   print("Age ", age)
   return;
```

Funkcja może także przyjmować wiele argumentów

```python
#** - zmienne będą interpretowane jako krotka
def printinfo( arg1, *krotka ):
   print("Output is: ")
   print(arg1)
   for var in krotka:
      print(var)
   return
#** - zmienne będą interpretowane jako słownik
def printinfo2( arg1, **slownik ):
   print( "Output is: ")
   print(arg1)
   for key in slownik.keys():
      print(key)
   return

printinfo( 10 )
printinfo( 70, 60, 50 )
printinfo2("argum1",klucz1=wart1,klucz2=wart2,klucz3=523,pusty=None) #ważne, aby słownik był definiowany jako słownik, czyli klucz=wartosc
```

W pythonie jedna funkcja może zwracać różne rzeczy, obiekty, zmienne, nic.

```python
def returnOrNot(return_bool=True):
    if return_bool:
        return True
    return

```

#### Adnotacje

W wypadku funkcji możemy też dodać adnotacje (typowanie zmiennych) do ich argumentów oraz wartości zwracanych (nie są one wykorzystywane przez interpreter, ale ułatwiają dokumentowanie)

```python
def funkcja( liczba1:99=12 , slowo1:str="sl", slowo2:"inne slowo"="inne") -> str:
    #some code
    return "slowo"

```

Można potem je sprawdzić poprzez sięgnięcie do aotrybutu `__annotations__`

```python
>>>funkcja.__annotations__
{'liczba1': 99, 'slowo1': <class 'str'>, 'slowo2': 'inne slowo', 'return': <class 'str'>}
```

#### Wyrażenia lambda

Lambdy to są funkcje, które można w dość podręczny sposób zdefiniować

```python
#Ogólna definicja
lambda arg1, arg2, arg3: nasze_wyrazenie #ta lambda zwróci wartość naszego wyrażenia

nasza_lambda = lambda x: x*2
nasza_lambda(2)
#>4

```

Argumenty w lambdach można zapisywać tak samo jak w zwykłych funkcjach, mogą tam być wartości domyślne,

#### Zasięg i zmienne globalne

W pythonie na ogół funkcje nie mogą edytować (mogą mieć dostęp, ale nie edytować) zmienne poza swoim zakresem.

```python
c = 1 # global variable

def add():
    print(c)
    c = c + 2 # increment c by 2
    print(c)

add()
#>2
#>UnboundLocalError: local variable 'c' referenced before assignment
```

Aby móc je jednak zmieniać jest używane słowo kluczowe `global`.

```python
c = 0 # global variable

def add():
    global c
    c = c + 2 # increment by 2
    print("Inside add():", c)

add()
print("In main:", c)
#>Inside add(): 2
#>In main: 2
```

#### Przekazywanie dowolnych argumentów (**kwargs i *args)

Pozwalają one na umieszczeanie argumentów o dowolnej liczbie i nazwie w naszej funkcji. **args** przyjmuje je jako listę kolejnych elementów, zaś **kwargs** przyjmuje je jak słownik.

```python
def parametr_args(*args):
    print("zawartość args: {}".format(args))

parametr_args('python', 'spam', 'eggs', 'test')
###zawartość args: ('spam', 'eggs', 'test')

def parametr_kwargs(argument, **kwargs):
    print("argument: {}".format(argument))
    print("zawartość kwargs: {}".format(kwargs))

parametr_kwargs(dodatkowy=48, nastepny=111, argument=12)

# argument: 12
# zawartość kwargs: {'dodatkowy': 48, 'nastepny': 111}
```

//TODO https://printpython.pl/poczatki/zadanie-z-gwiazdka/

### Obiekt

```python
class Osoba: #Definicja klasy o nazwie Osoba
    ile = 0 # pole statyczne
    def __init__(self, imie, nazwisko, wiek): #Definicja konstruktora
        self.imie = imie
        self.nazwisko = nazwisko
        self.wiek = wiek
    def przedstaw_sie(self):
        print(f"Jestem {self.imie} {self.nazwisko}. Mam {self.wiek} lat.")
    def urodziny(self):
        wiek_przed = self.wiek
        self.wiek += 1
    return wiek_przed
    def __del__(self): # destruktor, czyli kod, który wykonuje się podczas niszczenia obiektu
    @staticmethod
    def policz():
        return Osoba.ile
```

#### Metody

Metodę możemy poznać min. także po pierwszym argumencie: `self`.
W języku Python metody przyjmują jako pierwszy parametr obiekt, na rzecz którego są wywoływane. W samym wywołaniu nie musimy go sami podawać. Wystarczy, że metoda jest napisana po kropce. Następnie następują trzy zwykłe parametry: imie, nazwisko oraz wiek.

#### Konstruktor i destruktor

Jest to taka metoda, która jest wywoływana, gdy obiekt jest tworzony. Jej celem jest zainicjowanie pól w instancji. Tu są definiowane parametry klasy.
Konstruktor poznajemy po jego specjalnej nazwie: `__init__`.
Analogicznie działa destruktor (nazwa: `__del__`)
Przy wywołaniu pomijamy argument self.

```python
Jan = Osoba("Jan", "Nowak", 48)
Jan = None #Wymuszenie destrukcji obiektu
```

#### Widoczność elementów

W języku Python nie ma pól prywatnych w klasie: nie jesteśmy w stanie w praktyce czegokolwiek “ukryć”. Jednak są pewne zasady nazewnictwa, które działają raczej na zasadzie porozumienia, niż będące prawdziwą barierą. I tak, gdy poprzedzimy nazwę jednym znakiem podkreślenia `_`, oznajmiamy, że dany element nie jest uwzględniony w dokumentacji, może się zmienić, raczej nie należy z niego korzystać, a środowisko programistyczne nie będzie nam go podpowiadać. Przykładowo pole `_imie`, np. `self._imie`, czy `self._metoda()`.

Gdy użyjemy dwóch znaków podkreślenia `__`, zachowanie jest trochę inne: dane pole czy metoda nie będzie widoczna pod tą nazwą wcale, ale za to będzie można się do niego odwołać (dla nazwy `__element`) poprzez `_nazwaklasy.__element`.

#### Statyczne

Dla odmiany są one tworzone poza konstruktorem. Do pola tego odwołujemy się poprzez nazwę klasy. Np `Osoba.ile`
Sama metoda statyczna ma nad sobą napis `@staticmethod`. To tzw. dekorator. Dekoratory (zaczynające się od `@`) służą do modyfikacji definiowanej funkcji lub metody w określony sposób. W ten właśnie sposób oznaczamy metodę statyczną.
Metoda statyczna nie może odwoływać się do instancyjnych pól (czyli tych zwykłych, jak imie z poprzedniego przykładu), a jedynie do statycznych. Wynika to z faktu, że metoda statyczna nie jest wywoływana na rzecz konkretnego obiektu, który by takie właśnie pola miał.

#### Dekoratory

```python
#foo jest dekoratorem, który wzbogaci naszą funkcję
def foo(to_be_wrapped):
    def new_func(*args,**kwargs):
        print("uwaga, będzie sześcian")
    return to_be_wrapped

@foo #jeśli dodamy ten dekorator to użycie tej funkcji zostanie zmienione, tzn zamiast oryginalnej funkcji cube() otrzymamy "wzbogacone" cube drukujące komunikat przed drukowaniem
def cube(d):
    return d ** 3 #podniesienie do potęgi 3
```

### Dziedziczenie

```python
class Zwierze:
    def __init__(self, nazwa, wiek, waga):
        self.nazwa = nazwa
        self.wiek = wiek
        self.waga = waga
    def przedstaw_sie(self):
        print(f"Jestem zwierzęciem {self.nazwa}, mam {self.wiek} lat oraz wazę {self.waga} kg.")
    def urodziny(self):
        self.wiek += 1

class Mrowka(Zwierze):
    pass #Oznacza, że ciało jest puste

class Slon(Zwierze):
    def przedstaw_sie(self):
        print(f"Jestem słoniem {self.nazwa}, mam {self.wiek} lat oraz wazę {self.waga} kg.")

class Lew(Zwierze):
    def przedstaw_sie(self):
        super().przedstaw_sie()
        print("A tak w ogóle to jestem lwem")

class Papuga(Zwierze):
    def __init__(self, nazwa, wiek, waga, kolor):
        super().__init__(nazwa, wiek, waga)
        self.kolor = kolor
    def przedstaw_sie(self):
        super().przedstaw_sie()
        print(f"Jako papuga mój kolor to {self.kolor}")
```

`super()` zwraca nam instancję klasy bazowej: są to wszystkie pola i metody naszego obiektu, jakie otrzymaliśmy dzięki klasie bazowej.

#### Polimorfizm

Pozwala na używanie klasy dziedziczącej wszędzie tam, gdzie może być użyta klasa bazowa.
Oznacza to, że instancja klasy dziedziczącej jest uznawana za instancję klasy bazowej. W języku Python sprawdzenie przynależności danego obiektu do klasy wykonuje się metodą isinstance():

```python
def main():
    Dumboo = Slon("Dumboo", 77, 6000)
    Simba = Lew("Simba", 24, 100)
    Jago = Papuga("Jago", 32, 3, "czerwony")
    jakis_zwierz = Zwierze("Katarzyna", 31, 80)
    print(f"isinstance(Dumboo, Slon): {isinstance(Dumboo, Slon)}")
    print(f"isinstance(Dumboo, Lew): {isinstance(Dumboo, Lew)}")
    print(f"isinstance(Jago, Papuga): {isinstance(Jago, Papuga)}")
    print(f"isinstance(Jago, Zwierze): {isinstance(Jago, Zwierze)}")
    print(f"isinstance(jakis_zwierz, Zwierze): {isinstance(jakis_zwierz, Zwierze)}")
    print(f"isinstance(jakis_zwierz, Papuga): {isinstance(jakis_zwierz, Papuga)}")

if __name__ == "__main__":
    main()

## isinstance(Dumboo, Slon): True
## isinstance(Dumboo, Lew): False
## isinstance(Jago, Papuga): True
## isinstance(Jago, Zwierze): True
## isinstance(jakis_zwierz, Zwierze): True
## isinstance(jakis_zwierz, Papuga): False
```

### Abstrakcja

Uniemożliwia tworzenie instancji danej klasy. Przydatne przy klasach bazowych

```python
class Zwierze(ABC):
    def __init__(self,nazwa, wiek, waga):
        self.nazwa=nazwa
        self.wiek=wiek
        self.waga=waga
        @abstractmethod #tutaj wymuszamy implementację tej metody w klasach pochodnych
    def nazwa_gatunku(self):
        pass
    def przedstaw_sie(self):
        print(f"Jestem {self.nazwa_gatunku()}. Mam na imię {self.nazwa}, mam {self.wiek} lat oraz wazę {self.waga} kg.")
    def urodziny(self):
        self.wiek += 1

class Slon(Zwierze):
    def nazwa_gatunku(self):
        return "Słoń"

class Lew(Zwierze):
    def nazwa_gatunku(self):
        return "Lew"
```

Niestety, mechanizm klas i metod abstrakcyjnych (klasa jest abstrakcyjna gdy ma co najmniej jedną metodę abstrakcyjną) w języku Python jest wprowadzony trochę sztucznie. Klasa bazowa (abstrakcyjna) musi dziedziczyć po sztucznej klasie ABC, a metoda abstrakcyjna jest opatrzona dekoratorem @abstractmethod. Zwróćmy uwagę, że jedno i drugie zostało zaimportowane. Jednak po tych czynnościach rzeczywiście nie jesteśmy w stanie stworzyć instancji klasy bazowej.

Zwróćmy uwagę na ten zaawansowany mechanizm: w klasie Zwierze tworzymy metodę, zakładamy, co ta metoda będzie zwracać, a następnie korzystamy z niej w innej metodzie, pomimo, że prawdziwa jej implementacja nastąpi dopiero w klasie pochodnej. Dzięki temu musimy napisać mniej kodu w klasach pochodnych: musimy jedynie zaimplementować metodę nazwa_gatunku(), jednak nie musimy już od zera pisać kodu na przedstawienie zwierzęta. Jedynie w klasie Papuga, gdzie wprowadziliśmy nowe pole, dopisujemy kod odpowiedzialny za wypisanie jego wartości.

### Hermetyzacja

Polega na odcinanie użytkownikowi dostępu do pól, aby operował tylko metodami klasy.
Jednak oczywiście używanie metod, zwłaszcza z przedrostkiem get_czy set_, jest mniej wygodne. Dlatego nowoczesne języki programowania umożliwiają tworzenie tzw. właściwości (ang. property). Z punktu widzenia możliwości, są to po prostu metody, jednak z punktu widzenia zapisu i wygody, przypominają one pola.

```python
class Zwierze:
    def __init__(self, wiek):
        self.wiek = wiek

    @property
    def wiek(self):
        return self.__wiek
    @wiek.setter
    def wiek(self, wiek):
        if wiek < 0:
            self.__wiek = 0
        elif wiek > 200:
            self.__wiek = 200
        else:
            self.__wiek = wiek
def main():
    jakis_zwierz = Zwierze(202)
    print(jakis_zwierz.wiek)
    jakis_zwierz.wiek = -10
    print(jakis_zwierz.wiek)
    jakis_zwierz.wiek = 30
    print(jakis_zwierz.wiek)

if __name__ == "__main__":
    main()
## 200
## 0
## 30
```

## V

### Wyjątki

```python
def silnia(n):
    if n < 0:
    raise ValueError("silnia niezdefiniowana dla liczb ujemnych")
    wynik = 1
    for i in range(1, n+1):
        wynik *= i
    return wynik

try:
    print("Pozyskuję zasób")
    print(f"Silnia z -5 to {silnia(-5)}")
except ValueError as e:
    print("Och nie, coś poszło nie tak! Szczegóły poniżej:")
    print(e)
finally:
    print("Zwalniam zasób")
```

Gdy spodziewamy się, że dany fragment kodu może rzucać wyjątkami, opakowujemy go w konstrukcję try-except. Kod, który chcemy wykonać, a który może rzucić wyjątek, zapisujemy po try:. Następnie, na dole tego kodu, piszemy except, po czym piszemy nazwę klasy wyjątku, a także as, po którym mówimy, jakim identyfikatorem (w jakiej zmiennej) chcemy się odnosić do instancji tego wyjątku. Najważniejsza jest nazwa klasy, aby ustalić, jaki typ błędów łapiemy. Konkretna instancja, w przykładzie e, przydaje się, gdy np. chcemy wyświetlić komunikat błędu na ekran. Teoretycznie instanacja ma swoje pola, do których możemy się odnieść, jednak rzadko się z nich korzysta.

Listę wbudowanych klas wyjątków znajdziemy pod docs.python.org/3/library/exceptions.html. Szczególnej uwadze polecamy IndexError, gdy odwołujemy się do nieistniejącego elementu listy, FileNotFoundError, gdy plik nie istnieje, ZeroDivisionError dla dzielenia przez zero i wymieniony w przykładzie ValueError, gdy argumenty funkcji są błędne

#### With

Słowo kluczowe `with` pozwala na alternatywną (czystszą i czytelniejszą obsługę wyjątków)

```python
# file handling

# 1) without using with statement
file = open('file', 'w')
file.write('hello world !')
file.close()

# 2) without using with statement
file = open('file', 'w')
try:
 file.write('hello world')
finally:
 file.close()

# using with statement
with open('file', 'w') as file:
 file.write('hello world !')
```

Słowo `with` pozwala na automatyczne zwalnianie zasobów (na przykładzie powyżej widać, że nie trzeba wołać `close()`) przy wyjątku.
Mechanizm ten korzysta z metod `__enter__()` i `__exit__()` dla używanego obiektu.

Możemy wykorzystać ten mechanizm we własnych klasach

```python
# a simple file writer object

class Manager(object):
 def __init__(self, file_name):
  self.file_name = file_name

 def __enter__(self):
  self.file = open(self.file_name, 'w')
  return self.file

 def __exit__(self):
  self.file.close()

with Manager('file.txt') as xfile:
 xfile.write('hello world')
```

### Pliki

```python
sciezka_do_pliku = r"C:\przykladowy.txt"
#r sprawia, że / nie jest znakiem specjalnym
f = open(sciezka_do_pliku)
print(f.read())
f.close()
```

Tutaj mamy wszystko: `open()` służy otworzeniu połączenia do pliku. Jest to wspomniane wcześniej pozyskanie zasobu. Następnie następuje użycie metody read(). Odczytuje ona całą treść pliku za jednym zamachu. Po pojedynczym odczytaniu, drugie wywołanie zwróci nam napis pusty. Na końcu jest `close()`, zamknięcie połączenia do pliku. Jest to zwolnienie zasobu.

Jednak istnieje jeszcze drugi zapis. Używamy słowa kluczowego `with`. Wtedy definiujemy zasób, mówimy co chcemy zrobić, (open/write) gdy go pozyskamy, a na końcu, po wykonaniu całej klauzuli, zasób jest zwolniony, niezależnie od tego, czy wydarzyła się sytuacja wyjątkowa czy też nie

```python
try:
    with open(sciezka_do_pliku) as f:
    print(f.read())
    print(2/0)
except ZeroDivisionError as e:
    print(e)
```

```python
with open(sciezka_do_pliku, 'w') as f:
f.write("Trzeci wiersz")
f.write("Czwarty wiersz")#jeżeli nie damy \n to oba wiersze są zapisane w tej samej linijce
```

```python
#Pozostałe przydatne metody
f.readline()
f.read()
f.closed #informuje czy już zamknięte
```

With open flagi:
-`r` -read
-`w` -write otiwera plik (i nadpisuje, jeżeli tam już coś jest)
-`a` -append (otiwera do zapisu i zaczyna na końcu tzn dopisuje)

#### Dane o plikach

```python
import os
print(os.path.exists(sciezka_do_pliku))
## True
print(os.listdir("C:\folder\"))
## ['Wyzwanie6', 'pomysly.txt', inne pliki...]
print(os.path.join("folder1", "folder2", "plik.txt"))
## folder1/folder2/plik.txt #funkcja ta wstawia \ / zależnie od systemu
os.remove(sciezka_do_pliku) #usuwamy plik
```

```python
import datetime
(mode, ino, dev, nlink, uid, gid, size, atime, mtime, ctime) = os.stat(sciezka_do_pliku)
data_modyfikacji = datetime.datetime.fromtimestamp(mtime)
print(data_modyfikacji)
## 2018-12-21 10:46:54
```

## Wielowątkowość

```python
import threading

def foo():
  print("Hello threading!")

my_thread = threading.Thread(target=foo)

my_thread.start()
#>> Hello threading
# kolejne uruhomienie za pomocą start rzuci nam RuntimeError
```

Przy dłuższym czasie wykonywania możemy poczejać na wątki za pomocą

```python
my_thread.join()
```

### Testy z doctest

Jest to sposób na pisanie testów funkcji w jej definicji

Składnia:

- znajduje się pomiędzy `"""` i `"""`
- linie kodu są umieszczane po `>>>`
- oczekiwane wyniki wpisujemy w miejscach w których powinny się wyświetlić po wykonaniu

Np:

```python
"""
This is the "example" module.

The example module supplies one function, factorial().  For example,

>>> factorial(5)
120
"""

def factorial(n):
    """Return the factorial of n, an exact integer >= 0.

    >>> [factorial(n) for n in range(6)]
    [1, 1, 2, 6, 24, 120]
    >>> factorial(30)
    265252859812191058636308480000000
    >>> factorial(-1)
    Traceback (most recent call last):
        ...
    ValueError: n must be >= 0

    Factorials of floats are OK, but the float must be an exact integer:
    >>> factorial(30.1)
    Traceback (most recent call last):
        ...
    ValueError: n must be exact integer
    >>> factorial(30.0)
    265252859812191058636308480000000

    It must also not be ridiculously large:
    >>> factorial(1e100)
    Traceback (most recent call last):
        ...
    OverflowError: n too large
    """

    import math
    if not n >= 0:
        raise ValueError("n must be >= 0")
    if math.floor(n) != n:
        raise ValueError("n must be exact integer")
    if n+1 == n:  # catch a value like 1e300
        raise OverflowError("n too large")
    result = 1
    factor = 2
    while factor <= n:
        result *= factor
        factor += 1
    return result


if __name__ == "__main__":
    import doctest
    doctest.testmod()
```

flaga "-v" przy uruchamianiu takiego skryptu sprawia, że wyświetlają się także raporty z poprawnych testów.

//TODO lista: mixin, importowanie, biblioteka sys, instance methods
