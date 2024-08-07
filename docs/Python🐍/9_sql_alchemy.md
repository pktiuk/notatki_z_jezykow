# SqlAlchemy

Jedną z najpopularniejszych bibliotek ORM (Object-Relational Mapping) w Pythonie jest SqlAlchemy. Pozwala ona na tworzenie modeli bazodanowych w Pythonie, które są mapowane na tabele w bazie danych. SqlAlchemy pozwala na tworzenie zapytań SQL w Pythonie, bez konieczności pisania czystego SQL-a.
Działa to trochę jak [Django ORM](../Webówka🌍/9_django.md).


## Minimalny przykład

Omówienie minimalnego przykładu (bazującego na [dokumentacji FastAPI](https://fastapi.tiangolo.com/tutorial/sql-databases/))

Layout projektu:

```
.
└── sql_app
    ├── __init__.py
    ├── database.py - konfiguracja bazy danych
    ├── models.py - opisy modeli
    ├── crud.py - Create, Read, Update, and Delete. Funkcje do obsługi bazy danych
    ├── main.py
```

Plik `database.py`:

```py
from sqlalchemy import create_engine
from sqlalchemy.orm import sessionmaker

#określenie bazy z którą będziemy się łączyć
SQLALCHEMY_DATABASE_URL = "sqlite:///./sql_app.db"

#I utworzenie silnika bazy danych
engine = create_engine(
    SQLALCHEMY_DATABASE_URL, connect_args={"check_same_thread": False}
)
#II utworzenie lokalnej sesji
SessionLocal = sessionmaker(autocommit=False, autoflush=False, bind=engine)
```

- **I** - silnik jest obiektem służącym min. do tworzenia połączeń z bazą. Często jest on po prostu globalnym obiektem tworzonym raz dla danego serwera bazodanowego. ([omówienie silnika](https://docs.sqlalchemy.org/en/20/tutorial/engine.html#tutorial-engine))
- **II** - TODO nie wiem, czem nie zwykła sesja [innty tutorial](https://docs.sqlalchemy.org/en/20/tutorial/dbapi_transactions.html#executing-with-an-orm-session)

PLik ``models.py``:

```py
from sqlalchemy import Boolean, Column, ForeignKey, Integer, String
from sqlalchemy.orm import DeclarativeBase, relationship

# Deklaratywna klasa bazowa
class Base(DeclarativeBase):
    pass

# konkretne opisy klas
class User(Base):
    __tablename__ = "users"

    id = Column(Integer, primary_key=True)
    email = Column(String, unique=True, index=True)
    hashed_password = Column(String)
    is_active = Column(Boolean, default=True)

    items = relationship("Item", back_populates="owner")


class Item(Base):
    __tablename__ = "items"

    id = Column(Integer, primary_key=True)
    title = Column(String, index=True)
    description = Column(String, index=True)
    owner_id = Column(Integer, ForeignKey("users.id"))

    owner = relationship("User", back_populates="items")
```

**Deklaratywna klasa bazowa**, wykorzystywana do deklaratywnego definiowania obiektów (możliwe też imperatywne). ([Deklaratywne mapowanie w SQLAlchemy](https://docs.sqlalchemy.org/en/20/orm/mapping_styles.html#orm-declarative-mapping)). Kiedy tworzona jest klasa dziedzicząca po niej to baza zapamiętuje informacje o swoich dzieciach.   
Wcześniej do tego samego celu zamiast [DeclarativeBase](https://docs.sqlalchemy.org/en/20/orm/mapping_api.html#sqlalchemy.orm.DeclarativeBase) używano funkcji [declarative_base()](https://docs.sqlalchemy.org/en/20/orm/mapping_api.html#sqlalchemy.orm.declarative_base)

Plik `crud.py`:

```py
from sqlalchemy.orm import Session

from . import models


def get_user(db: Session, user_id: int):
    return db.query(models.User).filter(models.User.id == user_id).first()


def get_user_by_email(db: Session, email: str):
    return db.query(models.User).filter(models.User.email == email).first()


def get_users(db: Session, skip: int = 0, limit: int = 100):
    return db.query(models.User).offset(skip).limit(limit).all()


def create_user(db: Session, email, password):
    fake_hashed_password = password + "notreallyhashed"
    db_user = models.User(email=email, hashed_password=fake_hashed_password)
    db.add(db_user)
    db.commit()
    db.refresh(db_user)
    return db_user


def get_items(db: Session, skip: int = 0, limit: int = 100):
    return db.query(models.Item).offset(skip).limit(limit).all()

```

Plik `main.py`:

```py
from . import models
from . import crud
from .database import SessionLocal, engine

models.Base.metadata.create_all(bind=engine)

db = SessionLocal()

crud.create_user(db, "j@gmail.com","xxx")
crud.create_user(db, "anna@gmail.com","xxx")

print(crud.get_users(db))
```

Do wygodnego otwarcia bazy danych można użyć narzędzia [DB Browser for SQLite](https://sqlitebrowser.org/)   
Zaś do weryfikacji wprowadzanych danych może się przydać [pydantic](https://docs.pydantic.dev/latest/) (użyty w [oryginalnym przykładzie FastAPI](https://fastapi.tiangolo.com/tutorial/sql-databases/))



## Mapowanie klas

[link](https://docs.sqlalchemy.org/en/20/orm/mapping_styles.html)

SQLAlchemy pozwala na mapowanie klas na 2 sposoby:

- **Deklaratywne** - opisuje się klasę, a SQLAlchemy tworzy mapowanie do tabeli
- **Imperatywne** - tworzy się mapowanie wprost

### Mapowanie deklaratywne


```py
from sqlalchemy import Integer, String, ForeignKey
from sqlalchemy.orm import DeclarativeBase
from sqlalchemy.orm import Mapped
from sqlalchemy.orm import mapped_column


# declarative base class
class Base(DeclarativeBase):
    pass


# an example mapping using the base
class User(Base):
    __tablename__ = "user"

    id: Mapped[int] = mapped_column(primary_key=True)
    name: Mapped[str]
    fullname: Mapped[str] = mapped_column(String(30))
    nickname: Mapped[Optional[str]]
```

Wykorzystujemy tutaj bazową klasę jako podstawę dla klas mapowanych w bazie danych.   

Pola dla klasy możemy zdefiniować bezpośrednio ([ORM declarative table](https://docs.sqlalchemy.org/en/20/orm/declarative_tables.html#orm-declarative-table)) używając metody [`Mapped_column()`](https://docs.sqlalchemy.org/en/20/orm/mapping_api.html#sqlalchemy.orm.mapped_column):

```py
class User(Base):
  __tablename__ = "user"

  id = mapped_column(Integer, primary_key=True)
  name = mapped_column(String(50), nullable=False)
  fullname = mapped_column(String)
  nickname = mapped_column(String(30))
```

Lub używając annotacji typu pomocniczego [`Mapped`](https://docs.sqlalchemy.org/en/20/orm/internals.html#sqlalchemy.orm.Mapped):

```py
class User(Base):
    __tablename__ = "user"

    id: Mapped[int] = mapped_column(primary_key=True)
    name: Mapped[str] = mapped_column(String(50))
    fullname: Mapped[Optional[str]]
    nickname: Mapped[Optional[str]] = mapped_column(String(30))
```

W wypadku relacji można używać [`relationship()`](https://docs.sqlalchemy.org/en/20/orm/relationship_api.html#sqlalchemy.orm.relationship) lub [`mapped_column()`](https://docs.sqlalchemy.org/en/20/orm/mapping_api.html#sqlalchemy.orm.mapped_column) z parametrem `ForeignKey`. ([Link do relacji](https://docs.sqlalchemy.org/en/20/orm/basic_relationships.html#one-to-many))

```py
class Parent(Base):
    __tablename__ = "parent_table"

    id: Mapped[int] = mapped_column(primary_key=True)
    children: Mapped[List["Child"]] = relationship(back_populates="parent")


class Child(Base):
    __tablename__ = "child_table"

    id: Mapped[int] = mapped_column(primary_key=True)
    parent_id: Mapped[int] = mapped_column(ForeignKey("parent_table.id"))
    parent: Mapped["Parent"] = relationship(back_populates="children")
```

### Sprawdzanie wartości i walidacja

[Defining Constraints](https://docs.sqlalchemy.org/en/20/core/constraints.html#constraints-api), [Simple validation](https://docs.sqlalchemy.org/en/20/orm/mapped_attributes.html#simple-validators)

Istnieje kilka sposobów na walidację danych. Najprostszym jest prosty dekorator fla funkcji walidującej

```py
from sqlalchemy.orm import validates


class EmailAddress(Base):
    __tablename__ = "address"

    id = mapped_column(Integer, primary_key=True)
    email = mapped_column(String)

    @validates("email")
    def validate_email(self, key, address):
        if "@" not in address:
            raise ValueError("failed simple email validation")
        return address
```

