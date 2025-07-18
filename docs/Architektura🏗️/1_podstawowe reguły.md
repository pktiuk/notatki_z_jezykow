# Reguły wytwarzania oprogramowania i inne skrótowce

## Najważniejsze zasady, którymi warto się kierować

![Piramidka zasad https://medium.com/@bartoszkrajka/principle-of-software-development-principles-f0143d6f405](assets/piramida.png)

Bardzo dobry artykuł o tym [link](https://medium.com/@bartoszkrajka/principle-of-software-development-principles-f0143d6f405)


### Więcej mądrych skrótowców

**DRY** - Don't Repeat Yourself. Nie powtarzaj się. Jeśli coś jest powtarzane to warto to wydzielić do osobnej funkcji.

**KISS** - Keep It Simple, Stupid. Trzymaj to proste. Im prostszy kod tym lepiej.

**YAGNI** - You Aren't Gonna Need It. Nie rób rzeczy, które nie są potrzebne. Nie dodawaj funkcjonalności, które nie będą przez ciebie wykorzystywane.

**SOLID** - pięć zasad programowania obiektowego:

- **S** - Single Responsibility Principle. Każda klasa powinna mieć jedną odpowiedzialność.
- **O** - Open/Closed Principle. Kod powinien być otwarty na rozszerzenia, ale zamknięty na modyfikacje.
- **L** - Liskov Substitution Principle. Obiekty klas dziedziczących powinny być zastępowalne przez obiekty klas bazowych.
- **I** - Interface Segregation Principle. Klienty nie powinny być zmuszane do implementacji interfejsów, których nie używają.
- **D** - Dependency Inversion Principle. Moduły wysokiego poziomu nie powinny zależeć od modułów niskiego poziomu. Oba powinny zależeć od abstrakcji. Detale nie powinny zależeć od abstrakcji. Abstrakcje powinny zależeć od detali.

## Narzędzia dla architektury

Warto najpierw przechytać te artykuły:

[Software architecture diagrams - which tool should we use? ](https://dev.to/simonbrown/software-architecture-diagrams-which-tool-should-we-use-29e)  
[Visio, draw.io, LucidChart, Gliffy, etc - not recommended for software architecture diagrams](https://dev.to/simonbrown/visio-draw-io-lucidchart-gliffy-etc-not-recommended-for-software-architecture-diagrams-4bmm)

Do modelowania architektury można używać różnych typów narzędzi.

Tekstowych, które opisują diagramy, które możemy potem wygenerować:

- [mermaid](https://mermaid.js.org/)
- PlantUML
- Structurizr DSL - opisujemy strukturę raz a potem możemy wygenerować wiele typów diagramów dla niej [przykład](https://c4model.com/#ContainerDiagram)

Graficznych, gdzie ręcznie ustawiamy bloczki

- draw.io/ diagrams.net
- visio
- Gliffy
- [ExcaliDraw](https://excalidraw.com/)