# Nginx

Służy do routowania i zarządzania połączeniami przychodzącymi na dany serwer.

Jeśli nie chcesz robić niczego skomplikowanego to polecam po prostu użyć apki [Nginx proxy manager](https://nginxproxymanager.com/). Zrobisz większość rzeczy z pomocą prostego GUI.

## Instalacja i odpalenie

```bash
sudo apt install nginx
```

Po instalacji jest duża szansa, że nginx wystartuje jako serwis z domyślną konfiguracją w `/etc/nginx/nginx.conf`.

Do zarządzania przydaje się komenda `service`. Przydatna zwłąszcza, gdy chcemy zrestartować serwis, aby wczytał zaktualizowaną konfigurację.

```bash
sudo service nginx reload #restartuje go
sudo service nginx start
sudo service nginx stop
```

Jeśli chcesz na szybko coś pozmieniać to wystarczy, że wyedytujesz plik `nginx.conf` i zrestartujesz usługę.  
Jednak przed restartem warto sprawdzić, czy ta konfiguracja ma sens `nginx -t`.

## Konfiguracja

```nginx
http{ # Tutaj opisujemy zasady dla protokołu http

}

```

/// TODO sprawdzić prostsze alternatywi jak CADDY https://caddyserver.com/
