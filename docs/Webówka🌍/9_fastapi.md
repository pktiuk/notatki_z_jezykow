# FastAPI

Jest to jeden z mikroframeworków pythonowych wykorzystywanych przy apkach webowych.  
Jego zaletą na tle podobnych bibliotek typu flask jest automatyczne generowanie dokumentacji oraz automatyczne sprawdzanie i walidacja danych.

[link](https://fastapi.tiangolo.com/)

## Podstawy

```python
from typing import Optional

from fastapi import FastAPI

app = FastAPI()


@app.get("/")
def read_root():
    return {"Hello": "World"}


@app.get("/items/{item_id}")
def read_item(item_id: int, slowo: Optional[str] = None):
    """
    przyjmujemy zapytanie i zwracamy je jako json
    np /items/8?q=zbyszek
    """
    return {"item_id": item_id, "slowo": slowo}

```

Aby uruchomić powuższy kod (plik `main.py`) należy użyć komendy:

```bash
uvicorn main:app --reload
# main - nazwa pliku
# app - obiekt typu FastAPI
# --reload - restartuje serwer po zmianach w kodzie
```

Dodatkowo pod ścieżką `/docs` dostępna jest dokumentacja użytych API.

## Definiowanie modeli

Modele można definiować z wykorzystaniem biblioteki [pytandic](https://pydantic-docs.helpmanual.io/) ([tutorial od bulldogjobs](https://bulldogjob.pl/news/1747-przewodnik-dla-poczatkujacych-po-pydantic-pythona)).

```python

from typing import Optional

from fastapi import FastAPI
from pydantic import BaseModel

app = FastAPI()


class Item(BaseModel):
    name: str
    price: float
    is_offer: Optional[bool] = None


@app.put("/items/{item_id}")
def update_item(item_id: int, item: Item):
    return {"item_name": item.name, "item_id": item_id}
```

## Serwowanie plików HTML

FastAPI może być łączone z każdym silnikiem do generowania plików HTML ze schematów. Najpopularniejszym wyborem jest tutaj Jinja2 ([przykład użycia](https://fastapi.tiangolo.com/advanced/templates/)).

Jeśli nie potrzebujemy niczego tak skomplikowanego i wystarczą nam proste, ręcznie napisane pliki HTML to wystarczy wystawić je jako pliki statyczne lub jako pojedyncze pliki.

```python
from fastapi import FastAPI
from fastapi.staticfiles import StaticFiles

app = FastAPI()

app.mount("/static", StaticFiles(directory="static"), name="static")

#lub
@app.get("/")
async def read_index():
    return FileResponse('index.html')
```

## Bazy danych

FastAPI nie jest związane z żadną biblioteką do baz danych.  
Mamy tutaj dużą dowolność. Dla przykładu w [oficjalnej dokumentacji](https://fastapi.tiangolo.com/tutorial/sql-databases/) pokazano przykład użycia sla [SQLAlchemy](https://www.sqlalchemy.org/). Można też użyć [Peewee](http://docs.peewee-orm.com/en/latest/).

[LINK DO MOJEGO TUTORIALA SQLALCHEMY](../Python🐍/9_sql_alchemy.md)
