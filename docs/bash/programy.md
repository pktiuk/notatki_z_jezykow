## Screen

Otwarcie nowej sesji
screeen []

Wyjście z sesji
Ctrl+a , potem

lista aktywnych sesji
screen -ls

> There is a screen on:
> 21512.pts-4.komp-pc (07.08.2020 12:54:54) (Attached)
> 1 Socket in /run/screen/S-komp.

Dołącz do jednej z sesji
screen -r [numer_sesji]

Uruchom skrypt w sesji i odłącz się od sesji (dobre do startupu)

```bash
screen -d -m moj_skrypt_albo_komenda
```

Większość komend wewnątrz obsługuje się za pomocą kombinacji Ctrl+a (C-a) i po puszczeniu wciśnięciu danego przycisku.

Podstawowe:

- `C-a + d` -detach, wyjdź z sesji nie zamykając jej (sesja to nie terminal/ekran)
- `C-a + N` - wyświetl numer obecnego ekranu
- `C-a c`/`C-a C-c` - utwórz nowy ekran
- `C-a + [0-9]` - przejdź do ekranu o danym numerze
- `C-a + C-a` - przełącz na poprzedni ekran
- `C-a \` - zakmnij wszystkie okna i zakończ sesję

Inne użyteczne (pełna lista jest w `man screen`):

```
┌──────────────┬────────────────┬─────────────────────────────────────────────────────┐
│C-a '         │ (select)       │ Prompt for a window name or number to switch to.    │
├──────────────┼────────────────┼─────────────────────────────────────────────────────┤
│C-a "         │ (windowlist -b)│ Present a list of all windows for selection.        │
├──────────────┼────────────────┼─────────────────────────────────────────────────────┤
│C-a digit     │ (select 0-9)   │ Switch to window number 0 - 9                       │
├──────────────┼────────────────┼─────────────────────────────────────────────────────┤
│C-a C-a       │ (other)        │ Toggle to the window  displayed  previously.   Note │
│              │                │ that this binding defaults to the command character │
│              │                │ typed twice, unless overridden.  For  instance,  if │
│              │                │ you  use  the  option  "-e]x", this command becomes │
│              │                │ "]]".                                               │
├──────────────┼────────────────┼─────────────────────────────────────────────────────┤
│C-a A         │ (title)        │ Allow the user to enter a name for the current win‐ │
│              │                │ dow.                                                │
├──────────────┼────────────────┼─────────────────────────────────────────────────────┤
│C-a c,        │ (screen)       │ Create a new window with a shell and switch to that │
│C-a C-c       │                │ window.                                             │
├──────────────┼────────────────┼─────────────────────────────────────────────────────┤
│C-a C         │ (clear)        │ Clear the screen.                                   │
├──────────────┼────────────────┼─────────────────────────────────────────────────────┤
│C-a d,        │ (detach)       │ Detach screen from this terminal.                   │
│C-a C-d       │                │                                                     │
├──────────────┼────────────────┼─────────────────────────────────────────────────────┤
│C-a D D       │ (pow_detach)   │ Detach and logout.                                  │
├──────────────┼────────────────┼─────────────────────────────────────────────────────┤
│C-a space,    │ (next)         │ Switch to the next window.                          │
│C-a n,        │                │                                                     │
│C-a C-n       │                │                                                     │
├──────────────┼────────────────┼─────────────────────────────────────────────────────┤
│C-a N         │ (number)       │ Show the number (and title) of the current window.  │
├──────────────┼────────────────┼─────────────────────────────────────────────────────┤
│C-a backspace,│ (prev)         │ Switch to the previous window (opposite of C-a n).  │
│C-a C-h,      │                │                                                     │
│C-a p,        │                │                                                     │
│C-a C-p       │                │                                                     │
├──────────────┼────────────────┼─────────────────────────────────────────────────────┤
│C-a q,        │ (xon)          │ Send a control-q to the current window.             │
│C-a C-q       │                │                                                     │
├──────────────┼────────────────┼─────────────────────────────────────────────────────┤
│C-a Q         │ (only)         │ Delete  all  regions but the current one.  See also │
│              │                │ split, remove, focus.                               │
├──────────────┼────────────────┼─────────────────────────────────────────────────────┤
│C-a r,        │ (wrap)         │ Toggle the current window's line-wrap setting (turn │
│C-a C-r       │                │ the current window's automatic margins on and off). │
├──────────────┼────────────────┼─────────────────────────────────────────────────────┤
│C-a s,        │ (xoff)         │ Send a control-s to the current window.             │
│C-a C-s;      │                │                                                     │
├──────────────┼────────────────┼─────────────────────────────────────────────────────┤
│C-a S         │ (split)        │ Split  the current region horizontally into two new │
│              │                │ ones.  See also only, remove, focus.                │
├──────────────┼────────────────┼─────────────────────────────────────────────────────┤
│C-a t,        │ (time)         │ Show system information.                            │
│C-a C-t       │                │                                                     │
├──────────────┼────────────────┼─────────────────────────────────────────────────────┤
│C-a v         │ (version)      │ Display the version and compilation date.           │
├──────────────┼────────────────┼─────────────────────────────────────────────────────┤
│C-a C-v       │ (digraph)      │ Enter digraph.                                      │
├──────────────┼────────────────┼─────────────────────────────────────────────────────┤
│C-a w,        │ (windows)      │ Show a list of window.                              │
│C-a C-w       │                │                                                     │
├──────────────┼────────────────┼─────────────────────────────────────────────────────┤
│C-a X         │ (remove)       │ Kill the current region.   See  also  split,  only, │
│              │                │ focus.                                              │
├──────────────┼────────────────┼─────────────────────────────────────────────────────┤
│C-a z,        │ (suspend)      │ Suspend screen.  Your system must support BSD-style │
│C-a C-z       │                │ job-control.                                        │
├──────────────┼────────────────┼─────────────────────────────────────────────────────┤
│C-a ?         │ (help)         │ Show key bindings.                                  │
├──────────────┼────────────────┼─────────────────────────────────────────────────────┤
│C-a \         │ (quit)         │ Kill all windows and terminate screen.              │
├──────────────┼────────────────┼─────────────────────────────────────────────────────┤
│C-a {,        │ (history)      │ Copy and paste a previous (command) line.           │
│C-a }         │                │                                                     │
├──────────────┼────────────────┼─────────────────────────────────────────────────────┤
│C-a |         │ (split -v)     │ Split  the  current  region vertically into two new │
│              │                │ ones.                                               │
├──────────────┼────────────────┼─────────────────────────────────────────────────────┤
│C-a *         │ (displays)     │ Show a listing of all currently attached displays.  │
└──────────────┴────────────────┴─────────────────────────────────────────────────────┘
```

## Zdobywanie informacji o systemie

### Ogólne informacje o systemie

uname przydaje się do ogólnych informacji o systemi operacyjnym, architekturze procesora i kernelu.

```bash
uname
```

### Miejsce na dyskach

```bash
df

#df --block-size=1M poda ci rozmiar w gigabajtach
```

Może być przydatne w bombinacji z `du`, które może pokazywać ile miejsca zajmują dane foldery i pliki.
(terminalowa alternatywa dla apki `baobab` [link](https://wiki.gnome.org/Apps/DiskUsageAnalyzer))

```bash
du -d 1
# 1760    ./docs
# 9876    ./.git
# 12      ./.github
# 8       ./.vscode
# 11672   .
```

### Hardware

`lsusb` - przydatne do sprawdzania tego, jakie urządzenia usb mamy podłączone

```bash
lsusb
```

## Networking

`ip` - kombajn do sieciówki w Linuxie

`ifconfig` (już przestarzałe) - zwraca informacje o wszystkich odstępnych interfejsach sieciowych, IP, adresy MAC etc. Zamiast niego zaleca się `ip addr`

### Listowanie urządzeń w sieci lokalnej

```
sudo nmap -sn 192.168.1.0/24
```

### Wypisywanie portów na których maszyna nasłuchuje

`ss` apka do badania gniazd

```bash
ss -plnt #p - procesy l-listening n-numeric t-tcp
```

## Montowanie

mount
TODO

## SSH

SSH służy do zdalnego podłącznia się do powłoki systemów.

Łączymy się komendą `ssh login@adres`

Na przykład

```bash
marian@192.168.0.32

root@serwer.moj.pl

# Tutaj loginem jest pracownik@firma.com a adresem serwer.com
pracownik@firma.com@serwer.com
```

### Bash klucze

Po zalogowaniu na ogół musimy ręcznie wpisywać hasło.  
Aby tego nie robić możemy dodać klucz publiczny do naszej maszyny.

Dodatanie klucza do maszyny

```bash
ssh-copy-id login@adres
```

Aby uprościć wpisywanie adresów maszyn (oraz konfigurację) w terminalu możemy dopisać je do pliku `~/.ssh/config`

```txt
Host fajnyserwer
  HostName 198.43.32.33
  User pawel
  Port 9999
```

### Bash tunelowanie

Inną przydatną rzeczą jest tunelowanie portów za pomocą ssh. Pozwala to na dostęp do zdalnych usług na danych portach tak, jakby były u nas lokalnie. [link do artykułu](https://goteleport.com/blog/ssh-tunneling-explained/)


Na przykład komenda: 

```bash
ssh -L 9999:localhost:9090 marian@moj_serwer
```

Sprawi, że na naszej lokalnej maszynie pod portem `9999` będzie dostępna usługa, która jest dostępna pod portem `9090` naszego serwera.


### Bash aplikacje okienkowe

W niektórych wypadkach możemy potrzebobować jakiejś aplikacji okienkowej, wtedy używamy flagi `-X` (forwardowanie dla X11)

```bash
ssh -X jkowalski@adres
```

Wtedy po uruchomieniu w tym terminalu aplikacji z GUI jak np gedit to będziemy mogli zobaczyć jej okienko na naszej maszynie.

