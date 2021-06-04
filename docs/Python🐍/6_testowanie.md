# Testowanie

Do testów wykorzystujemy słowo kluczowe assert

```python
x = "hello"

#if condition returns False, AssertionError is raised:
assert x == "goodbye", "x should be 'hello'"
```

jeśli to co znajdzie się w assercie zwraca true to nic się nie dzieje, zaś jeśli jest to fałsz to rzuca wyjątek `AssertionError`. Wiadommość zawartą w tym wyjątku możemy podać po przecinku.

W pythonie jest kilka frameworków do testów: [pytest](https://docs.pytest.org/en/latest/getting-started.html), doctest i [unittest](https://docs.python.org/3/library/unittest.html#module-unittest)

Jeśli chodzi o strukturę testów to warto zwrócić uwagę na to, jak są one znajdowane. [Conventions for Python test discovery (pytest)](https://docs.pytest.org/en/latest/explanation/goodpractices.html#test-discovery)

## Unittest

Jest to domyślny sposób testowania wbudowany w język, jest też najmniej rozbudowany.

## Testy z doctest

Jest to sposób na pisanie testów funkcji w jej definicji, testy stanowią cześc opisu naszej funkcji

Składnia:

- znajduje się pomiędzy `"""` i `"""`
- linie kodu są umieszczane po `>>>`
- oczekiwane wyniki wpisujemy w miejscach w których powinny się wyświetlić po wykonaniu

Np:

```python
"""
This is the "example" module.

The example module supplies one function, factorial().  For example,

>>> factorial(5)
120
"""

def factorial(n):
    """Return the factorial of n, an exact integer >= 0.

    >>> [factorial(n) for n in range(6)]
    [1, 1, 2, 6, 24, 120]
    >>> factorial(30)
    265252859812191058636308480000000
    >>> factorial(-1)
    Traceback (most recent call last):
        ...
    ValueError: n must be >= 0

    Factorials of floats are OK, but the float must be an exact integer:
    >>> factorial(30.1)
    Traceback (most recent call last):
        ...
    ValueError: n must be exact integer
    >>> factorial(30.0)
    265252859812191058636308480000000

    It must also not be ridiculously large:
    >>> factorial(1e100)
    Traceback (most recent call last):
        ...
    OverflowError: n too large
    """

    import math
    if not n >= 0:
        raise ValueError("n must be >= 0")
    if math.floor(n) != n:
        raise ValueError("n must be exact integer")
    if n+1 == n:  # catch a value like 1e300
        raise OverflowError("n too large")
    result = 1
    factor = 2
    while factor <= n:
        result *= factor
        factor += 1
    return result


if __name__ == "__main__":
    import doctest
    doctest.testmod()
```

flaga "-v" przy uruchamianiu takiego skryptu sprawia, że wyświetlają się także raporty z poprawnych testów.

## Pytest

Jeden z najpopularniejszych sposobów testowania [link](https://docs.pytest.org/en/latest/getting-started.html).
Pytest odpala wszystkie pliki `test_*.py` i `*_test.py` z naszego folderu. I uruchamia wszystkie funkcje zwawierające `test_` w nazwie (także metody zdefiniowanych klas).

Pozwala na łtew testowanie klas, wyjątków etc

```python
import pytest

def f():
    raise SystemExit(1)

# sprawdzanie wyjątku
def test_mytest():
    with pytest.raises(SystemExit):
        f()

class TestClass:
    def test_one(self):
        x = "this"
        assert "h" in x

    def test_two(self):
        x = "hello"
        assert hasattr(x, "check")
```

### Pokrycie testami

Przy testach można sobie wygenerować raport pokrycia kodu

```bash
pytest --cov=./nazwa_paczki/ 
coverage xml #konwertuje plik .coverage do raportu w xml-u
```
