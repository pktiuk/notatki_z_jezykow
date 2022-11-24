# Docker

Docker jest jednym z najpopularniejszych obecnie systemów do wirtualizacji systemu operacyjnego.  
Pozwala w prosty sposób stworzyć instancję systemu będącą niemalże zupełnie niezależnym bytem od systemu maszyny na której się znajduje, może mieć ona zainstalowane zupełnie inne oprogramowanie, różnić się konfiguracją sieciową etc.  
Różni się on od zwyczajnej maszyny wirtualnej tym, że taki kontener jest dużo bardziej elastyczny od maszyny wirtualnej, ponieważ nie ma na stałe przydzielonych zasobów takich jak RAM, CPU etc.

Docker często jest wykorzystywany do pracy z różnorodnym oprogramowaniem bez niepotrzebnego zaśmiecania środowiska deweloperskiego. Jest to także jeden ze sposobów uniknięcia piekła zależności.

## Podstawowe Pojęcia

**Obraz/Image** - obrazy dockerowe są już gotowymi, wcześniej przygotowanymi paczkami zawierające systemy w dockerze. Przykładem obrazu jest `ubuntu:latest`.

**Kontener/Container** - jest to uruchomiona instancja naszego dockera bazująca na danym obrazie. Zawiera on konfigurację oraz wszystkie dane unikalne dla danej instancji.

## Obsługa

Mamy kilka grup komend

| Group     | Description                                                                                                                                |
| --------- | ------------------------------------------------------------------------------------------------------------------------------------------ |
| config    | Configuration management                                                                                                                   |
| container | Operations with containers                                                                                                                 |
| context   | Contexts for distributed deployment (k8s, …)                                                                                               |
| image     | Image management                                                                                                                           |
| network   | Network management                                                                                                                         |
| service   | Service (i.e. multiple containers that run the same image) management in distributed deployments (e.g.with docker-compose or docker swarm) |
| system    | Global management                                                                                                                          |
| volume    | Secondary storage management                                                                                                               |

Do zarządzania możemy też używać apek GUI, albo pluginów do IDE.

### Zarządzanie obrazami

Do zarządzania obrazami na naszej maszynie służy polecenie `docker image`.

#### Nowy obraz

W większości wypadków warto wykorzystywać obrazy znajdujące się na stronie [hub.docker.com](https://hub.docker.com/) - zawiera ona zarówno obrazy większości dystrybucji Linuxa, jak i obrazy z systemami zawierające już przygotowane narzędzia deweloperskie (np obrazy zawierające) zainstalowane i skonfigurowane bazy danych.

Aby pobrać taki obraz na naszą maszynę należy użyć komendy:

```bash
docker image pull [OPTIONS] NAME[:TAG|@DIGEST]
```

Na przykład:

```bash
docker image pull alpine:latest # pobiera najnowszy obraz systemu alpine
```

Jeśli potrzebujemy stworzyć własny obraz to możemy go samodzielnie zbudować za pomocą komendy:

```bash
docker image build
```

Pozwala ona zbudować nam własny obraz dockerowy na bazie pliku `dockerfile`. ([Opis składni](#składnia-pliku-dockerfile))

#### Zarządzanie posiadanymi obrazami

Za pomocy komendy [`docker image ls`](https://docs.docker.com/engine/reference/commandline/image_ls/) możemy łatwo wypisać lokalnie pobrane obrazy.

```bash
docker image ls
REPOSITORY                                                TAG             IMAGE ID       CREATED         SIZE
<none>                                                    <none>          93c4e800ab68   2 weeks ago     677MB
postgres                                                  11-alpine       ec1e25ef56d1   5 weeks ago     156MB
alpine                                                    latest          6dbb9cc54074   5 weeks ago     5.61MB
nginx                                                     1.19.0-alpine   7d0cdcc60a96   11 months ago   21.3MB
```

[`docker image rm`](https://docs.docker.com/engine/reference/commandline/image_rm/) usuwa dany obraz.

```bash
docker image rm [OPTIONS] IMAGE [IMAGE...]
```

Ale do czyszczenia jednak lepsze jest [`docker image prune`](https://docs.docker.com/engine/reference/commandline/image_prune/), które usuwa wszystkie "wiszące" (dangling) obrazy, czyli np stare kopie obrazów, które zostały już przebudowane (na liście obrazów podpisane są jako `<none>`).  
Dodanie flagi `-a` usuwa także wszystkie obrazy, które są nie są używane przez żadne kontenery.

```bash
$ docker image prune -a
WARNING! This will remove all images without at least one container associated to them.
Are you sure you want to continue? [y/N] y
Deleted Images:
untagged: alpine:latest
```

### Zarządzanie kontenerami

[`docker container ls`](https://docs.docker.com/engine/reference/commandline/container_ls/) - wypisuje kontenery obecnie uruchomione w systemie, dodanie flagi `-a` sprawia, że pokazuje także te wyłączone.

```bash
$ docker container ls -a
CONTAINER ID   IMAGE                                              COMMAND                CREATED       STATUS                 PORTS  NAMES
bd1415cdc985   server_nginx                                       "/docker-entrypoint.…" 25 hours ago  Exited (0) 24 hours ago       server_nginx_1
2474e0650b34   registry.gitlab.com/subjects-toolkit/server:latest "sh -c 'python manag…" 25 hours ago  Exited (0) 25 hours ago       server_web_1
ce6a641e20c1   postgres:11-alpine                                 "docker-entrypoint.s…" 2 weeks ago   Exited (0) 21 hours ago       server_db_1
```

### Uruchamianie

[`docker container create [OPTIONS] IMAGE [COMMAND] [ARG...]`](https://docs.docker.com/engine/reference/commandline/container_create/) - tworzy nam nowy kontener bazujący na danym obrazie, możemy także wybrać jaka komenda ma zostać w nim uruchomiona. (ale go nie uruchamia)  
Możemy go potem uruchomić komendą `docker container start ID`.

Do stworzenia nowego kontenera i natychmiastowego uruchomienia służy [`docker container run`](https://docs.docker.com/engine/reference/commandline/container_run/).

Przydatne flagi:

- `-rm` usuwa kontener po zakończeniu pracy
- `-i`, `--interactive` po odpaleniu nadal mamy podłączone STDIN
- `-t`, `--tty` Podłączamy się terminalem do kontenera (warto użyć razem z `-i`)

```bash
docker container run ubuntu -i -t bash
```

Do pracy z kontenerem możemy używać komend:

- `docker container run` albo też `docker run`
- `docker container pause`
- `docker container start`
- `docker container stop`
- `docker container restart`
- `docker commit containerName ImageName` -zapisujemy zmiany wprowadzone w danym kontenerze jako nowy obraz

Do usuwania kontenerów służą `docker container prune` i `docker container rm`.

### Składnia pliku dockerfile

Plik [dockerfile](https://docs.docker.com/engine/reference/builder/#format) opisuje kolejne operacje pokazujące, jak powinien być zbudowany nasz obraz.

Przykładowy plik dockerfile:

```docker
# wybierz obraz bazowy od którego zaczynasz konstruowanie
FROM ubuntu:latest

# Ustaw zmienne środowiskowe
ENV APP_USER=user

# Wykonaj daną komendę, np zainstaluj potrzebne pakiety etc.
RUN apt install -y firefox

# określ położenie folderu roboczego w którym odpalane są komendy
WORKDIR /home/user

# Kopiuj pliki z hosta do systemu plików wewnątrz kontenera
COPY ./plik /home/user/
```

Każda nowa linia/polecenie zaczyna się od komendy DUŻYMI_LITERAMI (taka konwencja).

Komendy:

- Pierwsza instrukcja to zawsze `FROM imageBase`
- `RUN command` wykonuje komendy w powłoce kontenera przy budowaniu
- `ENV variable value` ustawia wartości w środowisku (mogą być używane przez wszystko co będzie od teraz chodzić w kontenerze)
- `COPY source destination` kopiuje pliki ze źródła (URL, plik, folder) do miejsca w kontenerze
- `ADD source destination` to samo co `ADD` z różnicą, że gdy potrafi zorpakować archiwum, gdy jest ono podane jako plik
- `EXPOSE port` określa który port z kontenera wystawiamy na zewnątrz (na których portach kontener może słuchać)
- `WORKDIR path` określa folder roboczy w którym mają się wykonywać pozostałe komendy jak `RUN`, `CMD`, `ENTRYPOINT`
- `CMD command arg1 arg2 ...` dostarcza domyślnych komand i wartości argumentów, które zostaną uruchomione w kontenerze
- `ENTRYPOINT command arg1 arg2 ...` uruchamia tą komendę, kiedy kontener jest uruchamiany (kontener jest zamykany kiedy ta komenda się kończy)

**Uwaga** - w pliku dockerowym może być tylko jeden `CMD` albo `ENTRYPOINT`, jak nie to tylko `ENTRYPOINT` jest używany (na ogół).

#### ENTRYPOINT i CMD

ENTRYPOINT ma 2 warianty

- bazujący na samej komendzie

```docker
 ENTRYPOINT node app.js 9000 9001
```

- używany razem z CMD

```docker
ENTRYPOINT ["/bin/node","app.js"]
CMD ["9000","9001"]
```

I możemy to potem odpalić tak

```bash
docker build -t app
docker run app
docker run app 5555 5556 # gdy chcemy użyć własnych argumentów
```
