# Narzędzia serwerowe☁️

Na dobry początek można zajrzeć [na wiki reddita homelab](https://www.reddit.com/r/homelab/wiki/introduction/)

## Monitoring i zarządzanie infrastrukturą

Przydatne narzędzia dla każdej osoby, która zamierza rozpocząć swoją przygodę z serwerami/homelabem.

- [cockpit](https://cockpit-project.org/) - pozwala w prosty sposób monitorować serwer (poprzez apkę webową możemy się zalogować, uruchomić terminal, sprawdzać obciążenie, logi etc) ( [link to konfiguracji](https://cockpit-project.org/guide/latest/cockpit.conf.5))

  - Jeśli chcemy w cockpicie wygodnie zarządzać także portami warto doinstalować

- [linux-dash](https://afaqurk.github.io/linux-dash/#/system-status) - nieco prostsza alternatywa od cockpita

Narzędzia do monitorowania - długa lista <https://www.ubuntupit.com/most-comprehensive-list-of-linux-monitoring-tools-for-sysadmin/>

??? note "Cockpit + cloudflare tunnel"

    Wymagana edycja pliku
    ```
    cat /etc/cockpit/cockpit.conf
    ```

    ```
    [WebService]
    Origins = https://dashboard.xxxxx.ca wss://dashboard.xxxxx.ca
    ProtocolHeader = X-Forwarded-Proto
    AllowUnencrypted = true
    ```
    [źródło](https://github.com/cockpit-project/cockpit/issues/16396)
    Inną ważną rzeczą jest ograniczenie poziomu domeny. Nie powinno się używać pod-poddomen. może być `cockpit-serwer.domena.pl`, ale nie `cockpit.serwer.domena.pl` [żródło](https://mindlesstux.com/2022/01/16/cloudflare-tunnels-and-cockpit/)

Monitorowanie dockerów 🐋

- [portainer](https://www.portainer.io/) aplikacja służąca do wygodnej pracy oraz monitorowania dockerów w systemie
- [Yacht](https://yacht.sh/) - alternatywa dla portainera (trochę młodszy i prostszy projekt)

## Sieć, łączenie się i udostępnianie

- [ngrok](https://ngrok.com/) - pozwala łatwo udostępniać serwisy z urządzeń w sieci lokalnej. Dobre do prototypowania oraz prostych stron
- [cloudflare](https://dash.cloudflare.com/) - must-have gdy masz jakąś domenę i nią zarządzasz
  - Cloudflare Proxy - zwiększa wydajność twoich stron oraz pozwala tunelować ruch IPv4 na adresy PIv6
  - [Tunelowanie](https://developers.cloudflare.com/cloudflare-one/connections/connect-apps/install-and-setup/tunnel-guide/) - pozwala wystawiać do sieci serwery z sieci lokalnych pozbawione publicznych adresów. Można użyć tego chociażby do udostępnienia cockpita, czy też [SSH (instrukcje)](https://developers.cloudflare.com/cloudflare-one/connections/connect-apps/use-cases/ssh/#connect-to-ssh-server-with-cloudflared-access)

## Storage

- [TrueNAS](https://www.truenas.com/) - system operacyjny dedykowany maszynm mającym służyć jako storage
- [Wtyczka do Cockpitu](https://github.com/45Drives/cockpit-file-sharing) pozwalająca na łatwe udostępnianie zawartości, jest też inna [wtyczka do przeglądania plików](https://github.com/45Drives/cockpit-navigator)

## Dla chcących postawić sobie jakiś serwer

Poszukiwanie VPS-a:

- [mikr.us](https://mikr.us/) - fajne i tanie serwery dla amatorów, jest trochę [dokumentacji](https://www.notion.so/MIKR-US-Don-t-Panic-5c3bdde2e0b545e7866524fc117446c3) i fajna społeczność ( [FB](https://www.facebook.com/groups/mikrusy) i [Discord](https://discord.gg/hFcqJGkppq))
- [Oracle free tier](https://www.oracle.com/pl/cloud/free/) - darmowe serwery VPS or oracle. Omówienie: [link pepper](https://www.pepper.pl/promocje/oracle-cloud-free-tier-darmowe-vpsy-z-ipv4-459055)
- [serverhunter](https://www.serverhunter.com/) - wyszukiwarka tanich VPSów (gdy mikrus nie starcza)

Oganianie domen:

- [tld-list](https://tld-list.com/) - porównywarka cen domen
- [seohost](https://seohost.pl/) - moim zdaniem najlepszy dostawca domen w Polsce
