# Nginx

Służy do routowania i zarządzania połączeniami przychodzącymi na dany serwer.

Jeśli nie chcesz robić niczego skomplikowanego to polecam po prostu użyć apki [Nginx proxy manager](https://nginxproxymanager.com/). Zrobisz większość rzeczy z pomocą prostego GUI.   
Jest też [prosty konfigurator od Mozilli](https://ssl-config.mozilla.org/)

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

Przykładowa konfiguracja dla prostego serwera HTTP

```nginx
# Tworzymy serwer
server {
    #słuchający na porcie 80 (dla różnych interfejsów)
    listen 80;
    listen [::]:80;

    #umieszcza on logi w tych lokalizacjach
    access_log /var/log/nginx/reverse-access.log;
    error_log /var/log/nginx/reverse-error.log;
    
    # i dla endpointów zaczynających się na / (czyli dla wszystkich)
    location / {
        #przekierowuje ruch na adres http://127.0.0.1:8000
        proxy_pass http://127.0.0.1:8000;
        #nadpisujemy wartość nagłówka Host (aby zapobiec problemom z CSRF)
        proxy_set_header Host $http_host;
  }
}
```

Bardziej złożona konfiguracja

```nginx
#proste przekierowanie zapytań HTTP na HTTPS
server {
    listen 80;
    return 301 https://$host$request_uri;
}

server {
    listen 443;
    # podajemy nazwę dla tego serwera
    server_name example.com;
    client_max_body_size 0; #potrzebne do przesyłania dużych zapytań

    ssl_certificate           /etc/ssl/certs/example_local.crt;
    ssl_certificate_key       /etc/ssl/private/example_local.key;

    ssl_session_cache  builtin:1000  shared:SSL:10m;
    ssl_protocols  TLSv1 TLSv1.1 TLSv1.2;
    ssl_ciphers HIGH:!aNULL:!eNULL:!EXPORT:!CAMELLIA:!DES:!MD5:!PSK:!RC4;
    ssl_prefer_server_ciphers on;

    access_log            /var/log/nginx/example.access.log;

    location / {

      proxy_set_header        Host $host;
      proxy_set_header        X-Real-IP $remote_addr;
      proxy_set_header        X-Forwarded-For $proxy_add_x_forwarded_for;
      proxy_set_header        X-Forwarded-Proto $scheme;

      # Fix the It appears that your reverse proxy set up is broken" error.
      proxy_pass          http://localhost:8080;
      proxy_read_timeout  90;

      proxy_redirect      http://localhost:8080 https://example.com;
    }
  }
```

[link do dokumentacji modułu HTTP](https://nginx.org/en/docs/http/ngx_http_proxy_module.html)

Różne użyteczne parametry:

- `proxy_set_header HEADERNAME VALUE;` - pozwala na łatwe ustawianie/zmienianie nagłówków zapytań wysyłanych dalej
- `client_max_body_size 100G;` - jak duży zapytania mogą być wysyłane przez klientóœ

Do debugowania nginx-a i certyfikatów warto używać komend:

```bash
wget --header="Host: example.com" http://192.168.1.10/
curl -H "Host: example.com" -O http://192.168.1.10/myfile.txt
```

Przy deploymentach złożonych systemów warto użyć [nginx-a w dockerze](https://hub.docker.com/_/nginx) i zmapować folder z konfigiem na folder `/etc/nginx/conf.d/`

Przykład dla compose'a

```yml
  nginx:
    image: nginx:alpine
    ports:
      - "80:80"
      - "443:443"
    volumes:
      - ./conf.d:/etc/nginx/conf.d
      - ./ssl:/etc/nginx/ssl
    depends_on:
      - my_webapp

```


/// TODO sprawdzić prostsze alternatywy jak CADDY https://caddyserver.com/
