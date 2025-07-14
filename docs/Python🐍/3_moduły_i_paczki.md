# Podział na Moduły i Paczki📦

**Moduł** - plik pythonowy zawierający definicje i wyrażenia, nazwa pliku jest nazwą modułu z dodanym rozszerzeniem `.py` (`nazwa_modułu.py`). Wewnątrz modułu ta nazwa jest dostępna jako zmienna globalna `__name__`.  
Moduł jest jednym ze sposobów organizacji kodu w pythonie, na ogół w jednym module trzyma się blisko powiązane ze sobą definicje funkcji, klas etc.  
Jeśli chodzi tu o grupowanie to warto zadbać tutaj o złoty środek (pliki nie muszą być duże, ani małe, muszą po prostu spójnie tworzyć logiczną całość).

**Paczka** - sposób na ustrukturyzowanie modułów ( pozwala to łatwo ustrukturyzować projekt)

## Zarządzanie paczkami

Do instalacji można używać samodzielnych aplikacji pip (i pip3). (Ale w sytuacjach bardziej złożonych projektów warto rozważyć użycie innych menadżerów pakietów jak np [UV](https://docs.astral.sh/uv/))

```bash
pip3 install numpy
```

Można też wymusić od danej instancji pythona, aby zainstalował dla siebie daną paczkę (użyteczne gdy mamy wiele wersji).

```bash
python3 -m pip install numpy
```

PIP może też używać plików zawierających opisy paczek potrzebnych do zainstalowania [`requirements.txt`](https://pip.pypa.io/en/stable/reference/requirements-file-format/)

```bash
python3 -m pip install -r requirements.txt
```

gdzie plik moze wyglądać tak

```txt
# zsykłe paczki
pytest
pytest-cov

# Podawanie konkretnych paczek po sieci
http://my.package.repo/simple
git+ssh://git@git.example.com/MyProject
```

## Tworzenie i używanie własnych paczek

### Struktura projektu pythonowego

```
.
├── pyproject.toml
├── README.md
├── requirements-dev.txt
├── requirements.txt
├── src
│   └── package
│       ├── __init__.py
│       └── main.py
└── tests
    └── test_classes.py
```

Opisy poszczególnych plików:

- `requirements.txt` - plik zawierający listę zależności projektu (instalowanych np. pip-em)
- `pyproject.toml` - [oficjalnie zalecany](https://packaging.python.org/en/latest/guides/writing-pyproject-toml/) plik konfiguracyjny projektu pythonowego. Zawiera on informacje o projekcie, konfiguracje dla narzędzi potrzebnych do jego budowy, testowania, formatowania kodu etc.

Przykładowy toml
```toml
[project]
name = "myproj_pythonowy"
version = "0.1.0"
authors = [{name = "Jan Kowalski", email = "jkowalski@email.pl"}]
readme = "README.md"
requires-python = ">=3.10"
description = "Mega fajny projekt"

[project.urls]
"Source" = https://strona.com

[project.scripts]
myproj = "myproj_pythonowy.__main__:main"
```

### Struktura biblioteki

Przykładowa struktura paczki

```
sound/                          Top-level package
      __init__.py               Initialize the sound package
      formats/                  Subpackage for file format conversions
              __init__.py
              wavread.py
              wavwrite.py
              aiffread.py
              aiffwrite.py
              auread.py
              auwrite.py
              ...
      effects/                  Subpackage for sound effects
              __init__.py
              echo.py
              surround.py
              reverse.py
              ...
      filters/                  Subpackage for filters
              __init__.py
              equalizer.py
              vocoder.py
              karaoke.py
              ...
```

Aby wykorzystać zawartość pliku `karaoke.py` należy zaimportować:

```python
import sound.filters.karaoke
```

### Wewnętrzne linkowanie

Przy linkowaniu pomiędzy poszczególnymi elementami paczki zaleca się używanie poniższej konwencji:

```python
#zakładamy, że jesteśmy w pliku filters/karaoke.py
from . import echo
from .. import formats
from ..filters import equalizer
```

## Wczytywanie paczki z danego folderu

Kiedy nasza paczka jest w niestandardowym folderze można ją wczytać tak

```python
#tu zakładam, że paczka jest umieszczona w jakimś folderze umieszczonym gdzieś względem pliku ze skryptem, ale module_path może być dowolne
module_path = os.path.dirname(os.path.realpath(__file__)) + "/.."
sys.path.append(module_path)
```
