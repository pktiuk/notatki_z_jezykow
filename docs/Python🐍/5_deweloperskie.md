# Narzędzia deweloperskie

## VENV - wirtualne środowisko

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

Do tego warto użyć bibliotek booosta.

Przykładowy Github Gist zawierający prosty projekt obrazujący działanie: [TUTAJ](https://gist.github.com/pktiuk/2136eeefaf4271510d82e59f90c904ce)

## Guideline'y

- [PEP 8](https://www.python.org/dev/peps/pep-0008/#module-level-dunder-names)
- [Google](https://google.github.io/styleguide/pyguide.html)
- [docs](https://docs.python-guide.org/writing/structure/)

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

# GDB

[LINK](https://wiki.python.org/moin/DebuggingWithGdb)

/TODO opisać dokładniej

/TODO opisać działanie libki subprocess (czyli jak ogarnąć prawdziwą wielowątkowość w pythonie), oraz uruchamianie procesów.
