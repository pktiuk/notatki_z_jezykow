# Zarządzanie systemem

## Serwisy i demony

`/etc/systemd/system/`

`systemctl`

W większości dystrybucji Linuxa, zarządzanie serwisami i demonami odbywa się za pomocą [`systemd`](https://systemd.io). Wszystkie pliki konfiguracyjne znajdują się w katalogu `/etc/systemd/system/`.

Do zarządzania serwisami i demonami korzysta się z aplikacji `systemctl`. Poniżej znajdują się najważniejsze komendy:

- `systemctl start nazwa_serwisu` - uruchamia serwis
- `systemctl stop nazwa_serwisu` - zatrzymuje serwis
- `systemctl restart nazwa_serwisu` - restartuje serwis
- `systemctl status nazwa_serwisu` - sprawdza status serwisu. Pokazuje nie tylko status, ale także wyświetla logi.
- `systemctl enable nazwa_serwisu` - ustawia serwis do uruchamiania przy starcie systemu
- `systemctl disable nazwa_serwisu` - usuwa serwis z uruchamiania przy starcie systemu

Składnia plików opisujących serwisy jest dosć prosta.  
Przykładowy plik konfiguracyjny (`/etc/systemd/system/http-map-socat.service`):

```toml
[Unit]
Description=Map HTTP port (80) to port 80 of another machine using socat
#po jakich pozostałych serwisach powinien się uruchomić (lista podzielona spacjami)
After=network.target netbird.service

[Service]
ExecStart=socat TCP-LISTEN:80,fork TCP:100.81.47.39:80
RestartSec=15
Restart=always
StandardOutput=syslog
StandardError=syslog

[Install]
WantedBy=multi-user.target
```

## Logi systemowe

Do prostego wyświetlania logów kernela może być uzyta komenda dmesg

```bash
sudo dmesg
```

Przydatne flagi to:

- `-w` `--follow` - podążanie za kolejnymi logami
- `-T` - czas w formacie godziny (a nie liczony od startu)

Do bardziej zaawansowanych zastosowań można używać komendy journalctl.

Przykładowa komendy

```bash
journalctl --list-boots # wypisz ostatnie uruchomienia oraz ich czasy trwania
journalctl -b-1 # wyświetl logi tylko z ostatniego uruchomienia (oznaczonego jako -1)
```

## Domślne foldery systemowe

![Schemat](assets/linux_directories.jpeg)

TODO opisz te najważniejsze dla mnie

- `/home/`
- `/mnt`
- `/tmp`
- `/`

## Bootowanie i GRUB

Podczas bootowania GRUB wybiera wpis opisujący obecną konfigurację (czyli np jaki kernel użyć z jakimi flagami etc.). Jego konfigurację można znaleźć w pliku `/boot/grub2/grub.cfg` jednak jego edycja jest niezalecana.



## Firewalle i sieć

TODO
