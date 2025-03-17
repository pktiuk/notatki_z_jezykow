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

## Logowanie (logging)


Wbudowane biblioteka [logging](https://docs.python.org/3/library/logging.html) w Pythonie dostarcza gotowych mechanizmów do generowania, formatowania oraz zarządzania logami systemowymi. [Oficjalny tutorial](https://docs.python.org/3/howto/logging.html#custom-levels)

Minimalny przykład:

```python
import logging

logging.debug("This is a debug")
logging.info("This is an info")
logging.warning("This is a warning")
logging.error("This is an error")
logging.critical("This is a critical message")
#> WARNING:root:This is a warning
#> ERROR:root:This is an error
#> CRITICAL:root:This is a critical message
```

Dla takiego sktyptu otrzymany tylko ostatnie 3 linijki, ponieważ domyślny poziom logów jest za niski.

Do odpowiedniego ustawienia tego parametru można użyć funkcji [logging.basicConfig](https://docs.python.org/3/library/logging.html#logging.basicConfig)

```python
logging.basicConfig(level=logging.DEBUG)
logging.debug('To już się wyświetli')
```

Za pomocą tej funkcji możemy określić inne podstawowe parametry jak format, kodowanie, styl, format daty, plik z logami etc.


### Formatowanie logów

Format logów można zdefiniować za pomocą jednego stringa odpowiadającego określonej składni.

```py
import logging
logging.basicConfig(format='%(asctime)s %(message)s')
logging.warning('is when this event was logged.')
# 2019-12-12 11:51:42,692 is when this event was logged.
```

W definicjach logów odwołujemy się do atrybutów klasy [LogRecord](https://docs.python.org/3/library/logging.html#logrecord-attributes).

Z pomocą `basicConfig` możemy też łatwo określić używany format czasu ([ściągawka](https://www.w3schools.com/python/python_datetime.asp)) (milisekundy lepiej określać w ramach formatu z LogRecord-a)

```py
import logging
logging.basicConfig(format='%(asctime)s%(msecs)d %(message)s', datefmt='%m/%d/%Y %I:%M:%S.')
logging.warning('is when this event was logged.')
#> 12/12/2010 11:46:36.423 is when this event was logged.
```

### Poziomy logowania

Każdy poziom logowania ma własną przyporządkowaną wartość liczbową [link](https://docs.python.org/3/library/logging.html#levels).

Im wyższa tym ważniejszy log (Debug to 10, CRITICAL to 50). Dzięki temu możliwe jest dodawanie własnych poziomów logowania. Możliwe jest tutaj wykorzystanie funkcji [addLevelName](https://docs.python.org/3/library/logging.html#logging.addLevelName).

```py
    #tutaj nadpisuję aby mieć fajniejszą nazwę
    logging.addLevelName(logging.DEBUG, "🐞DEBUG")
    # a tutaj dodaję nowy poziom
    logging.addLevelName(15, "VERBOSE")
```


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

now = time.time() #godzina jako epoch w sekundach
# 1715610262.8038244 
```

Do wygodniejszej obsługi czasu i jego ptintowania można użyć biblioteki `datetime`.  
Możemy tutaj zdefiniować także własny format printowania daty. [link](https://docs.python.org/3/library/datetime.html#datetime.date.strftime)

```py
import datetime
datetime.datetime.now()
# datetime.datetime(2024, 5, 14, 19, 14, 0, 297824)

datetime.datetime.fromtimestamp(1715610262.8038244)
# datetime.datetime(2024, 5, 13, 16, 24, 22, 803824)

x = datetime.datetime(2018, 6, 1)

print(x.strftime("%B")) 
# June
```

## Uruchamianie innych aplikacji

Do wygodnego uruchamiania innych aplikacji w terminalu można użyć biblioteki subprocess z metodą [check_output](https://docs.python.org/3/library/subprocess.html#subprocess.check_output).

Przykładowy snippet:

```py
result = subprocess.check_output(
        f"pwd", shell=True
    ).decode()
print(result)
#>/home/admin/examples
```

Innym, ogólniejszym wariantem jest uruchomienie [`subprocess.run()](https://docs.python.org/3/library/subprocess.html#subprocess.run), który zwraca obiekt [CompletedProcess](https://docs.python.org/3/library/subprocess.html#subprocess.CompletedProcess)

```py
subprocess.run(["ls", "-l"])  #printuje komendę na stdout
#>total 12
#>-rw-rw-rw-   1 codespace root  199 Mar  5 13:11 README.md
#>drwxrwxrwx+ 10 codespace root 4096 Mar 15 14:44 docs
#>-rw-rw-rw-   1 codespace root 1085 Apr  2 12:30 mkdocs.yml
#>CompletedProcess(args=['ls', '-l'], returncode=0)
result=subprocess.run(["ls"],capture_output=True)
print(result.stdout.decode())
```

Przydatne argumenty:

- `shell: bool = False` - dzięki temu możemy podawać komendy jako jeden dłuższy string, a nie listę (`ls --all`)
- `check: bool = False` - kiedy komenda zwróci status inny niż 0, metoda rzuca wyjątek: `CalledProcessError`
- `capture_output: bool = False` - STDOUT jest przechwytywany i umieszczany w zmiennej `CompletedProcess`

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

