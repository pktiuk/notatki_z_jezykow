# 3 Różne użyteczne biblioteki i narzędzia dla ogólniejszych zagadnień

## Instalacja pakietów
Do tego służy narzędzie pip, pobieramy pip-a za pomocą zwykłego menadżera pakietów, a potem paczki pythonowskie pobieramy już pip-em.

### Operacje matematyczne
** potęga
2+3j liczba zespolona

## Wielowątkowość
moduł threading

multiprocessing - podobny, ale niekompatybilny

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

## Używanie kodu z C++
boost lub ctypes


## Przetwarzanie strumieniowe

## Czas
```python
import time
time.sleep(60)#minuta
```

## Aplikacje webowe

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
/TODO opisać dokładniej
