# Różne użyteczne biblioteki i narzędzia dla ogólniejszych zagadnień

## Manipulacja tekstem

## Przetwarzanie strumieniowe

## Czas
```python
import time
time.sleep(60)#minuta
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
