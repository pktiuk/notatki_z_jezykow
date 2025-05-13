# Narzędzia deweloperskie

## Utrzymanie jakości kodu

### Guideline'y

Istnieje kilka znanych i powszechnie stosowanych guideline'ów, które warto znać i stosować w pythonie:

- [PEP 8](https://www.python.org/dev/peps/pep-0008/#module-level-dunder-names)
- [Google](https://google.github.io/styleguide/pyguide.html)
- [docs](https://docs.python-guide.org/writing/structure/)


### Autoformatowanie kodu

Do tego celu można użyć narzędzi takich jak:

- black
- autopep8
- yapf
- [ruff](https://github.com/astral-sh/ruff) format

### Lintowanie kodu

Lintowanie kodu to sprawdzanie go pod kątem problemów z samym kodem oraz jego zgodności z wybranymi guideline'ami. Może to obejmować takie problemy jak np. nieużywane zmienne, niezgodność z PEP8, błędy składniowe, itp.

Do tego celu można użyć narzędzi takich jak:

- pylint
- flake8
- [ruff](https://github.com/astral-sh/ruff)

W kontekście typowania warto także zwrócić uwagę na zagadnienia związane z typowaniem i adnotacjami typów ([link do adnotacji](./1_ogolne_notatki.md#adnotacje)). O ile sam python traktuje adnotacje jedynie jako sugestie i komentarze to możliwe jest sprawdzenie ich poprawnosci z pomocą type checkerów takich jak:

- [mypy](https://mypy-lang.org/)
- [pyright](https://github.com/microsoft/pyright)
- [pyre](https://pyre-check.org/)

## VENV

Venv, czyli wirtualne środowisko pythona, to narzędzie, które pozwala na stworzenie odizolowanego środowiska pythonowego z własnymi pakietami, aby nie zaśmiecać hosta.

Jest to bardzo potrzebne gdy nie chcemy przypadkiem namieszać w naszych już zainstalowanych paczkach pythonowych, a chcemy odpalić jakiś projekt wymagający konkretnych wersji danych pakietów. [Dokumentacja](https://docs.python.org/3/library/venv.html)

Instalacja dla debianów: `sudo apt install python3-venv`.

Tworzenie nowego venva

```bash
python3 -m venv /path/to/new/virtual/environment
```

Aby aktywować venva (czyli odpalić w pythona korzystającego z pakietów w tym venvie) trzeba użyć komendy

| Shell               | Command to activate virtual environment                                       |
| ------------------- | ----------------------------------------------------------------------------- |
| bash/zsh            | `$ source <venv>/bin/activate`                                                |
| fish                | `$ source <venv>/bin/activate.fish csh/tcsh $ source <venv>/bin/activate.csh` |
| PowerShell          | `$ <venv>/bin/Activate.ps1 `                                                  |
| (Windows)cmd.exe    | `C:\> <venv>\Scripts\activate.bat `                                           |
| (Windows)PowerShell | `PS C:\> <venv>\Scripts\Activate.ps1`                                         |

## Uruchamianie skryptu w trybie interaktywnym

Z poziomu basha:

```bash
python -i ./skrypt.py
```

Z poziomu pythona:

```python
exec(open("./first.py").read())
```

Dzięki temu po zakończeniu wykonywania nie wyjdziemy ze skryptu i będziemy mogli kontynuować jego pracę używając już zaimportowanych przez niego bibliotek oraz zmiennych, które utworzył.

## Użycie modułów z C/C++

Do tego warto użyć bibliotek boosta, popularny jest też [pybind11](https://github.com/pybind/pybind11) .

Przykładowy Github Gist zawierający prosty projekt obrazujący działanie: [TUTAJ](https://gist.github.com/pktiuk/2136eeefaf4271510d82e59f90c904ce)

Przy pracy z bibliotekami tego typu mogą pojawić sie problemy min z autopodpowiadaniem kodu.   
W takiej sytuacji można np wygenerować sobie stubsy [link stack](https://stackoverflow.com/questions/73879484/vscode-not-autocompleting-python-from-module-made-with-pybind11) (czasami może to działać bez takich obejść)

## Implementacje Pythonowe

Warto wiedzieć, że jest wiele implementacji pythona. Najbardziej znaną jest CPython napisany w C.  
Ze względu na wydajność warto się zapoznać z:

- PyPy - kompilator typu JIT
- Nuitka [link](https://nuitka.net/pages/overview.html) - o ile dobrze rozumiem to taki jakby kompilator pythona

Ze względu na kompatybilność:

- Jython (java)
- IronPython (C#)

Pełna lista implementacji [link](https://wiki.python.org/moin/PythonImplementations)

## Dokumentowanie

### Diagramy klas

Do tego można użyć:

- pyreverse - chyba najprostsze (do pobrania z pipa)

```bash
pyreverse -o png moje_klasy.py
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

### GDB

[LINK](https://wiki.python.org/moin/DebuggingWithGdb)

/TODO opisać dokładniej

## Profilowanie kodu

Profilowanie kodu to sprawdzanie, które fragmenty kodu zajmują najwięcej czasu. Ważny jest tutaj dobór narzędzi do wizualizacji.

### VizTracer

[VizTracer](https://github.com/gaogaotiantian/viztracer) jest bardzo prostym w użyciu narzędziem.

[![example_img](https://github.com/gaogaotiantian/viztracer/blob/master/img/example.png)](https://github.com/gaogaotiantian/viztracer/blob/master/img/example.png)

Generowanie raportu (result.json):

```
# Instead of "python3 my_script.py arg1 arg2"
viztracer my_script.py arg1 arg2
```

Podgląd:

```
vizviewer result.json
```

### Scalene

[Scalene](https://github.com/plasma-umass/scalene) jest nieco bardziej szczegółowym narzędziem. pokazuje także użycie pamięci i GPU.



-------------------------

/TODO opisać działanie libki subprocess (czyli jak ogarnąć prawdziwą wielowątkowość w pythonie), oraz uruchamianie procesów.
