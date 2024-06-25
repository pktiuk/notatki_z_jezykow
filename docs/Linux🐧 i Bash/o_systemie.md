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

TODO opisz same  pliki konfiguracyjne i ich syntax

## Domślne foldery systemowe

![Schemat](assets/linux_directories.jpeg)

TODO opisz te najważniejsze dla mnie

- `/home/`
- `/mnt`
- `/tmp`
- `/`

## Firewalle i sieć

TODO
