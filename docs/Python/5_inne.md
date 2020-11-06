# Uruchamianie skryptu w trybie interaktywnym
Z poziomu basha:
```bash
python -i ./skrypt.py
```
Z poziomu pythona:
```python
exec(open("./first.py").read())
```

Dzięki temu po zakończeniu wykonywania nie wyjdziemy ze skryptu i będziemy mogli kontynuować jego pracę używając już zaimportowanych przez niego bibliotek oraz zmiennych, które utworzył.