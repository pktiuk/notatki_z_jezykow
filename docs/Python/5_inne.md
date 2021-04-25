# Inne

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

## Implementacje Pythonowa

Warto wiedzieć, że jest wiele implementacji pythona. Najbardziej znaną jest CPython napisany w C.  
Ze względu na wydajność warto się zapoznać z:

- PyPy - kompilator typu JIT
- Nuitka [link](https://nuitka.net/pages/overview.html) - o ile dobrze rozumiem to taki jakby kompilator pythona

Ze względu na kompatybilność:  

- Jython (java)
- IronPython (C#)

Pełna lista implementacji [link](https://wiki.python.org/moin/PythonImplementations)
