# Moduły i Paczki


**Moduł** - plik pythonowy zawietający definicje i wyrażenia, nazwa pliku jest nazwą modułu z dodanym rozszerzeniem `.py` (`nazwa_modułu.py`). Wewnątrz modułu ta nazwa jest dostępna jako zmienna globalna `__name__`.

**Paczka** - sposub na ustrukturyzowanie modułów ( pozwala to łatwo ustrukturyzować projekt)

## Zarządzanie paczkami
pip i pip3 #TODO

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