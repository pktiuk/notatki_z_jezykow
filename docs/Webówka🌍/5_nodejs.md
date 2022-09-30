# NodeJS

Jest to narzędzie wykorzystywane do rozwijania komponentów systemów rozproszonych.  
Dostarcza serię modułów, które pomagają w rozwijaniu takich apek.  
Jest zaprojektowany do zwinnego rozwijania skalowalnych aplikacji.

Definiuje:

- Interfejsy
- Interpreter - operty na silniku V8 (z google chrome'a)
- zarządzanie modułami
- ...

Inne cechy:

- I/O model oparty o zdarzenia
  - pętla zdarzeń działa w jednym wątku
  - aktywność nigdy nie jest bolkowana
- równoległość oparta o callbacki oraz wydarzenia

Zastosowania:

- Komponenty serwerowe
- Niekrytyczne aplikacje
- Aplikacje z lekkimi interfejsami REST/JSON
- Aproste aplikacje (takie, które korzystają z AJAX-a, do interakcji z serwerami)

## Zarządzanie modułami

Korzystając z funkcji `require()` możemy włączać inne moduły do naszego programu

```js
const HTTP = require(‘http’);

const st = require(‘./Circle.js’);
console.log( “Area of a circle with radius 5: “ + st.area(5) );
```

Aby coś dało się zaimportować musimy użyć `exports`

```js
// Module Circle.js
exports.area = function (r) {
  return Math.PI * r * r;
};
```

### Moduł Events

[Dokumentacja](https://nodejs.org/api/events.html)  
Jest on wykorzystywany do implementacji generatorów wydarzeń.

Generatory są instancjami `EventEmitter`

Proste użycie

```js
const emitter = new ev.EventEmitter();
emitter.on(eventName, functionHandler); //Rejestrowanie callbacka
emitter.emit(eventName, arg1, arg2, ....); //Wywołanie zdarzenia z argumentami
```

`emit()` powoduje wywołanie natychmiastowe wywołanie callbacku.  
Jeśli chcemy, aby wydarzyło się to potem możemy skorzystać z asynchrnoiczności.  
`setTimeout(function() {emit(event,...);},0)`

MOże być wiele callbacków dla danego wydarzenia.

Większy przykład

```js
const ev = require("events");
const emitter = new ev.EventEmitter(); // DON’T FORGET NEW OPERATOR!!
const e1 = "print",
  e2 = "read"; // Names of the events.

function createListener(eventName) {
  let num = 0;
  return function () {
    console.log(
      "Event " + eventName + " has " + "happened " + ++num + " times."
    );
  };
}
// Listener functions are registered in the event emitter.
emitter.on(e1, createListener(e1));
emitter.on(e2, createListener(e2));
// There might be more than one listener for the same event.
emitter.on(e1, function () {
  console.log("Something has been printed!!");
});
// Generate the events periodically...
setInterval(function () {
  emitter.emit(e1);
}, 2000); // First event emitted every 2s
setInterval(function () {
  emitter.emit(e2);
}, 3000); // Second event emitted every 3s
```

### Stream module

Uzywane do pracy ze strumieniemi danych. [Dokumentacja](http://nodejs.org/api/stream.html)

Istnieją 4 warianty:

- Readable: odczyt
- Writable
- Duplex: odczyt i zapis dostępny
- Transform: podobne do duplexu, ale wpisy na ogół zależą od odczytów

Wszystkie z nich są klasami typu `EventEmitter`, posiadają one zdarzenia:

- Readable: `readable`, `data`, `end`, `close`, `error`.
- Writable: `drain`, `finish`, `pipe`, `unpipe`.

Przykłady:

- Readable: process.stdin, files, HTTP requests (server), HTTP responses (client), ...
- Writable: process.stdout, process.stderr, files, HTTP requests (client), HTTP responses (server),...
- Duplex: TCP sockets, files,...

### Moduł sieciowy - net

Służy do zarządzania gniazdami TCP

- net.Server: TCP server.
  - Generated using `net.createServer([options,][connectionlistener])`.
    - “connectionListener”, when used, has a single parameter: a TCP socket already connected.
  - Events that may manage: `listening`, `connection`, `close`, `error`.
- net.Socket: Socket TCP.
  - Generated using `new net.Socket()` or `net.connect(options [,listener])` or `net.connect(port [,host][,listener])`
  - Implements a Duplex Stream.
  - Events that may manage: `connect`, `data`, `end`, `timeout`, `drain`, `error`, `close`.

Przykład (serwer)

```js
const net = require("net");
let server = net.createServer(function (c) {
  //'connection' listener
  console.log("server connected");
  c.on("end", function () {
    console.log("server disconnected");
  });
  // Send "Hello" to the client.
  c.write("Hello\r\n");
  // With pipe() we write to Socket 'c'
  // what is read from 'c'.
  c.pipe(c);
}); // End of net.createServer()
server.listen(9000, function () {
  //'listening' listener
  console.log("server bound");
});
```

Klient

```js
const net = require("net");
// The server is in our same machine.
let client = net.connect({ port: 9000 }, function () {
  //'connect' listener
  console.log("client connected");
  // This will be echoed by the server.
  client.write("world!\r\n");
});
client.on("data", function (data) {
  // Write the received data to stdout.
  console.log(data.toString());
  // This says that no more data will be
  // written to the Socket.
  client.end();
});
client.on("end", function () {
  console.log("client disconnected");
});
```
