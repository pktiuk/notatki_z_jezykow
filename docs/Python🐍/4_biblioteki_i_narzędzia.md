# Różne użyteczne biblioteki i narzędzia

## Różne linki

- [Książka Zanurkuj w Pythonie](https://pl.wikibooks.org/wiki/Zanurkuj_w_Pythonie/Wersja_do_druku) 📖
- [Podstawowy tutorial ze strony learnpython](https://www.learnpython.org/)

## Instalacja pakietów

Do tego służy narzędzie pip, pobieramy pip-a za pomocą zwykłego menadżera pakietów, a potem paczki pythonowskie pobieramy już pip-em.

### Operacje matematyczne

- `**` potęga  
- `2+3j` liczba zespolona

## Manipulacja tekstem

### Stringi wielolinijkowe

```python
slowa=""" linia1
linia2
linia3
"""
```

### Rozbijanie stringów po słowach

```python
slowo="slowo1 slowo2 sl3"
slowo.split()
>>>['slowo1', 'slowo2', 'sl3']
```

### Formatowanie tekstu

Formatowanie tekstu nie tylko w kontekście funkcji `print()`

#### str.format()

```python
def hello(name):
    print("Hello {name}".format(name=name))

```

#### f-stringi (Python 3.6+)

```python
def hello(name):
    print(f"Hello {name}")
```

### Pobieranie ścieżki/folderu obecnego skryptu

```python
import os

os.path.abspath('') # obecny folder

__file__ # zmiennna zawierająca obecnie uruchamiany plik (nie zawsze działa)

```

## Używanie kodu z C++

boost lub ctypes  
Przykład dla boosta: [link](https://gist.github.com/pktiuk/2136eeefaf4271510d82e59f90c904ce)

## Przetwarzanie strumieniowe

## Czas

```python
import time
time.sleep(60)#minuta
```

## Aplikacje webowe

### Proste hostowanie folderu

KIedy chcesz w prosty sposób udostępnić dany folder w sieci.

```bash
python -m http.server #to udostępni pod adresem 8000

#można też samodzielni wybrać port
python -m http.server 8888
```

### Django

jest to dość duża zabawka

### Bottle

Mniejsza i dużo prostsza biblioteka (mieści się w jednym pliku)

```python
from bottle import route,run,template

@route('/hello/<name>') #@route to dekorator
def index(name):
    return template('<b>Hello {{name}} <br/>?',name=name) #otrzymamy prostego html-a

#index = route('//hello/<name>')(index) #ten sam wynik, w sytuacji bez @route


run(host='0.0.0.0',port=8080) #nasza strona będzie dostępna tutaj

```

albo możemy też chcieć wygenerować jsona

```python
def index(name):
    return {"klucz":"wartosc","a_tu":["bedzie","lista"]}
```

## Zapisywanie

### Pickle - zapisywanie zmiennych

Pythonowa biblioteka [Pickle](https://docs.python.org/3/library/pickle.html) pozwala na zapisywanie (i odczytywanie) danych i obiektór w pythonie w formie binarnej.  

//TODO przykłady

### Dill -zapisywanie całej sesji w pythonie

Rozszerzeniem do pickla jest dill, pozwala on na zapisywanie załej sesji w pythonie do pliku, który można potem przywrócić.

//todo przykład

## Debugowanie

### pdb

```python
import pdb
pdb.set_trace() #w tej linii skrypt się zatrzyma i będzie można się rozejrzeć
# (Pdb)
```

zapytania w trybie debuggera :

- w - where (na stosie)
- u -up
- d - down
- c/continue - continue
- args - wyświetla wszystkie argumenty, jakie dana funkcja otrzymała (ta w której obecnie jesteśmy)
Poza tym reszta rzeczy odpowiada zwykłemu pisaniu w pythonie, możemy zmieniać zmienne, printować je, uruchamiać pętle etc.

Warto wtedy używać też:
`locals()` - ładuje do słownika wszystkie obecnie dostępne funkcje

### inspect

```python
import inspect

inspect.getsource(xyz)# wypisuje jak dana funkcja jest napisana

```

### ast

```python
#podobnie jak wyżej
import ast
```

# GDB

[LINK](https://wiki.python.org/moin/DebuggingWithGdb)

/TODO opisać dokładniej



/TODO opisać działanie libki subprocess (czyli jak ogarnąć prawdziwą wielowątkowość w pythonie), oraz uruchamianie procesów.
