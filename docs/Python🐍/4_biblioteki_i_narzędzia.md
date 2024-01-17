# Różne użyteczne biblioteki i narzędzia

## Różne linki

- Stronka agregująca w jedny miejscu najpotrzebniejsze API z bibliotek pythonowych: https://overapi.com/python
- [Książka Zanurkuj w Pythonie](https://pl.wikibooks.org/wiki/Zanurkuj_w_Pythonie/Wersja_do_druku) 📖
- [Podstawowy tutorial ze strony learnpython](https://www.learnpython.org/)

## Parsowanie argumentów

Do parsowania argumentów na ogół korzysta się z biblioteki [argparse](https://docs.python.org/3/howto/argparse.html).

Przykładowy kod

```python
parser = argparse.ArgumentParser(
                    prog='ProgramName',
                    description='What the program does',
                    epilog='Text at the bottom of help')
parser.add_argument('filename')           # positional argument
parser.add_argument('-c', '--count')      # option that takes a value
parser.add_argument('-v', '--verbose',
                    action='store_true')  # on/off flag - czyli przy podaniu -v args.verbose to true
args = parser.parse_args() #parsowanie argumentów,aby uzyskać obiekt z argumentami
```

Najważniejszą metodą klasy ArgumentParser jest `add_argument()`.  
Może przyjmować on [różne argumenty](https://docs.python.org/3/library/argparse.html#quick-links-for-add-argument).  
Najważniejsze wydają się:

- `help` - opis argumentu
- `type` - typ argumentu do jakiego wartość ma być przekonwertowana [link](https://docs.python.org/3/library/argparse.html#argparse-type).
można tutaj podać typ (`int`, `str`), `argparse.FileType` (aby sprawdzić poprawność ścieżki do pliku), bądź funkcja koonwertująca
    ```python
    # kiedy chcemy sprawdzić czy plik istnieje, ale chcemy otrzymać stringa
    def _readable_file_string(path):
        reader = argparse.FileType("r")
        reader(path)  # if not exists, then raises Exception
        return path

    parser.add_argument('input_file', type=argparse.FileType('w', encoding='latin-1'))
    parser.add_argument('file_path', type=_readable_file_string)
    ```
- `default`
- `required`
- `choices`
- `nargs` - ile razy może się pojawić ten argument

## Manipulacja tekstem

### Stringi wielolinijkowe

```python
slowa=""" linia1
linia2
linia3
"""
```

### Rozbijanie stringów po słowach

`string.split(separator, maxsplit)` - domyślny separator to jakikolwiek whitespace, maxsplit- domyślnie -1 (opisuje na ile fragmentów maksymalnie możemy dzielić stringa)

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

Wg [dokumentacji](https://peps.python.org/pep-0498/#format-specifiers) używając tej metody możemy wprowadzać dodatkowe zmiany w tekście

```python
width = 10
precision = 4
value = decimal.Decimal('12.34567')
f'result: {value:{width}.{precision}}'
#12.35
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

### Wykonywanie zapytań w HTMLu - requests

Najprostszą i najwygodniejszą biblioteką jest [requests](https://docs.python-requests.org/en/latest/)
Może ona służyć zarówno do pobierania treści z neta jak i do web scrappingu.

```python
import requests

data = {"name": "Marian"}
response = requests.get("http://127.0.0.1:5000/", json=data)
r.text
# { "id": "3123424", ...
r.json() # zwróci ospowiedź jako słownik
r.status
# 200
```

### Proste hostowanie folderu

KIedy chcesz w prosty sposób udostępnić dany folder w sieci.

```bash
python -m http.server #to udostępni pod adresem 8000

#można też samodzielni wybrać port
python -m http.server 8888
```

### Django

jest to dość duża zabawka [link](../Webówka🌍/9_django)

### Flask

Jeden z mikroframeworków, pozwala dość szybko napisać jakąś aplikację REST-ową.

```python
from flask import Flask, request, response

app = Flask(__name__)

@app.route('/', methods=["GET", "POST"])
def hello_world():
    if request.method == "GET":
        return "Hello"

    if request.method == "POST":
        return "you posted something"

if __name__ == '__main__':
    app.run()
```

### Bottle

Mniejsza i dużo prostsza biblioteka (mieści się w jednym pliku).  
Podobna do flaska.

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

## Aplikacje z GUI

TODO rozpisać się trochę

https://wiki.python.org/moin/GuiProgramming

## Zapisywanie

### Pickle - zapisywanie zmiennych

Pythonowa biblioteka [Pickle](https://docs.python.org/3/library/pickle.html) pozwala na zapisywanie (i odczytywanie) danych i obiektów w pythonie w formie binarnej poprzez serializację.
Serializacja polega na przekształceniu obiektu w postać, która może być zapisana do pliku lub przesłana przez sieć.

```python
import pickle

# tworzenie obiektu do serializacji
data = {'name': 'John Smith', 'age': 30, 'country': 'USA'}

with open('data.pkl', 'wb') as f:
    # serializacja obiektu i zapis do pliku
    pickle.dump(data, f)

# otwieranie pliku z serializowanym obiektem
with open('data.pkl', 'rb') as f:
    # deserializacja obiektu z pliku
    data2 = pickle.load(f)

print(data2)  # {'name': 'John Smith', 'age': 30, 'country': 'USA'}
```

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
