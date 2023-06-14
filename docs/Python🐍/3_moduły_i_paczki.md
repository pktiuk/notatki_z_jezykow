# Podział na Moduły i Paczki📦

**Moduł** - plik pythonowy zawierający definicje i wyrażenia, nazwa pliku jest nazwą modułu z dodanym rozszerzeniem `.py` (`nazwa_modułu.py`). Wewnątrz modułu ta nazwa jest dostępna jako zmienna globalna `__name__`.  
Moduł jest jednym ze sposobów organizacji kodu w pythonie, na ogół w jednym module trzyma się blisko powiązane ze sobą definicje funkcji, klas etc.  
Jeśli chodzi tu o grupowanie to warto zadbać tutaj o złoty środek (pliki nie muszą być duże, ani małe, muszą po prostu spójnie tworzyć logiczną całość).

**Paczka** - sposób na ustrukturyzowanie modułów ( pozwala to łatwo ustrukturyzować projekt)

## Zarządzanie paczkami

pip i pip3 #TODO

Do instalacji można używać samodzielnych aplikacji pip (i pip3)

```bash
pip3 install numpy
```

Można też wymusić od danej instancji pythona, aby zainstalował dla siebie daną paczkę (użyteczne gdy mamy wiele wersji).

```bash
python3 -m pip install numpy
```

## Tworzenie i używanie własnych paczek

### Struktura

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
