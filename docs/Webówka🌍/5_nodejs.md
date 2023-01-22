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

## Przyjmowanie argumentów programu `argv`

Argumenty znajdują się w zmiennej `process.argv`.

## Poszczególne moduły

### Zarządzanie modułami

Są 2 sposoby na importowanie modułów

- **ESM** - (imo lepszy)

```js
import React from 'react';

import {foo, bar} from './myLib';

...
import * as fs from 'node:fs/promises';
...

export default function() {
  // your Function
};
export const function1() {...};
export const function2() {...};

```

- **CJS** (CommonJS)

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

- Readable:
  - `readable`
  - `data` - część informacji została odczytana (linia)
  - `end` - strumień zamknął obecne połączenie
  - `close` - strumień TCP został zamknięty całkowicie (nie będzie już przyjmował nowych połączeń)
  - `error`.
- Writable: `drain`, `finish`, `pipe`, `unpipe`.

Przykłady:

- Readable: process.stdin, files, HTTP requests (server), HTTP responses (client), ...
- Writable: process.stdout, process.stderr, files, HTTP requests (client), HTTP responses (server),...
- Duplex: TCP sockets, files,...

```js
const st = require('./Circle.js')
const os = require('os')
process.stdout.write("Radius of the circle: ")
process.stdin.resume() // Needed for initiating the reads from stdin.
process.stdin.setEncoding("utf8") // … for reading strings instead of “Buffers”.
// Endless loop. Every time we read a radius its circumference is printed and a new
radius is requested
process.stdin.on("data", function(str) {
  // The string that has been read is “str”. Remove its trailing endline.
  let rd = str.slice(0, str.length - os.EOL.length)
  console.log("Circumference for radius " + rd + " is " + st.circumference(rd))
  console.log(" ")
  process.stdout.write("Radius of the circle: ")
})
// The “end” event is generated when STDIN is closed. [Ctrl]+[D] in UNIX.
process.stdin.on("end", function() {console.log("Terminating...")})
```

### Moduł sieciowy - net

Służy do zarządzania gniazdami TCP. [Dokumentacja](https://nodejs.org/api/net.html)

- net.Server: TCP server.
  - Generated using `net.createServer([options,][connectionlistener])`.
    - “connectionListener”, when used, has a single parameter: a TCP socket already connected.
  - Events that may manage: `listening`, `connection`, `close`, `error`.
- net.Socket: Socket TCP.
  - Generated using `new net.Socket()` or `net.connect(options [,listener])` or `net.connect(port [,host][,listener])`
  - Implements a Duplex Stream.
  - Events that may manage: `connect`, `data`, `end`, `timeout`, `drain`, `error`, `close`.
  - Is child of `EventEmitter`

Przykład (serwer)

```js
const net = require("net");
let server = net.createServer(function (socket) {
  //'connection' listener
  console.log("server connected");
  socket.on("end", function () {
    console.log("server disconnected");
  });
  // Send "Hello" to the client.
  socket.write("Hello\r\n");
  // With pipe() we write to Socket 'c'
  // what is read from 'c'.
  socket.pipe(socket);
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

### Moduł HTTP

Pomaga przy implementacji serwerów webowych (oraz klientów) [Dokumentacja](https://nodejs.org/api/http.html)

Klasy:

- `http.Server` - modeluje web serwer
- `http.ClientRequest` - zapytanie
  - Jest to strumień oraz EventEmitter
  - Wydarzenia: `response`, `socket`, `connect`, `upgrade`, `continue`
- `http.ServerResponse`
- `http.IncomingMessage`

```js
const http = require("http");
const hostname = "127.0.0.1";
const port = 3000;
const server = http.createServer((req, res) => {
  // res is a ServerResponse.
  // Its setHeader() method sets the response header.
  res.statusCode = 200;
  res.setHeader("Content-Type", "text/plain");
  // The end() method is needed to communicate that both the header
  // and body of the response have already been sent. As a result, the response can
  // be considered complete. Its optional argument may be used for including the
  // last part of the body section.
  res.end("Hello World\n");
});
// listen() is used in an http.Server in order to start listening for
// new connections. It sets the port and (optionally) the IP address.
server.listen(port, hostname, () => {
  console.log("Server running at http://" + hostname + ":" + port + "/");
});
```

### Cluster - skalowanie

Jako, że JS jest jednowątkowy to nie możemy w prosty sposób stworzyć nawych wątków do przetwarzania większej ilości zapytań. Musimy uruchamiać kolejne procesy. Do ułatwienia tego zadania mozemy wykorzystać moduł `cluster`. Pozwala na:

- łatwe tworzenie nowych procesów wykonujących ten sam kod
- umożliwia zarządzanie nimi i dzielenie obciążenia (klasa `Worker`)
- procesy mogą dzielić ten sam port przypisany danemu serwisowi
- dostarcza wiele dodatkowych eventów: (`fork`,`online`,`listening`,`disconnect`,`exit`…)

Przykładowy klaster

```js
var cluster = require("cluster");
var numCPUs = require("os").cpus().length;
var server = ...; // the server which runs the workers
var port = ...;// the port where the server binds

if (cluster.isMaster) {// code of the master one
// fork: create workers
  for (var i = 0; i < numCPUs; i++) cluster.fork();
  // listening death of workers
  cluster.on("exit", function (worker, code, signal) {
    console.log("worker", worker.process.pid, "died");
  });
} else {
  // code of any worker
  server.listen(port); // each worker runs the server
}

```

Klaster serwerów HTTP

```js
var cluster = require("cluster");
var http = require("http");
var numCPUs = require("os").cpus().length;
if (cluster.isMaster) {
  // code of the master one
  for (var i = 0; i < numCPUs; i++) cluster.fork();
  cluster.on("exit", function (worker, code, signal) {
    console.log("worker", worker.process.pid, "died");
  });
} else {
  // code of any worker
  http
    .createServer(function (req, res) {
      res.writeHead(200);
      res.end("hello world\n");
    })
    .listen(8000);
}
```
