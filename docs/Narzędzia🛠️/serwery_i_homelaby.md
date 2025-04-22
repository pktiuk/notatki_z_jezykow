# Narzędzia serwerowe☁️

Na dobry początek można zajrzeć [na wiki reddita homelab](https://www.reddit.com/r/homelab/wiki/introduction/), [artykuł o przykładowych usługach](https://hostbor.com/25-must-have-home-server-services/)

Fajne serwisy których hostowanie może posłużyć każdemu:

- [NextCloud](https://nextcloud.com/) - alternatywa dla własnego google clouda. Baza pod dużą ilosć zastosowań, jak file storage, kalendarz, kontakty, zarządzanie zdjęciami, edycja dokumentów, komunikator etc.
- [Jellyfin](https://jellyfin.org/) - własny prywatny serwer multimedialny (taki netflix/legimi/spotify)
- [Pi-Hole](https://pi-hole.net/) - domowy adblock dla wszystkich urządzeń w sieci
- Uptime kuma - prosta apka do monitorowania innych serwerów

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
    Potem w panelu Cloudflate mapujemy nasz adres na `http://localhost:9090`
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

VPN-y

Bazowe protokoły:

- Wireguard - jeden z dwóch popularnych protokołów VPNa.
- OpenVPN - również popularny, lecz troche przestarzały protokół VPNa
- [PiVPN](https://www.pivpn.io/) - prosty i uniwersalny VPN. Ma UI webowe oraz wpiera Wireguarda i OpenVPN-a.

Jednak nieco wygodniejsze wydaje się wykorzystywanie narzędzi takich jak netbird i tailscale.

### Obsługa PiVPN-a i Wireguarda

Zakładam, że PiVPN jest skonfigurowany z Wireguardem.

Aby dodać nowego nowe połączenie do naszego serwera wireguarda nalezy wywołać komendę `pivpn add`, tam określamy nazwę połączenia.

```bash
pawel@amd:~$ pivpn add
Enter a Name for the Client: superserwer
::: Client Keys generated
::: Client config generated
::: Updated server config
::: WireGuard reloaded
======================================================================
::: Done! superserwer.conf successfully created!
::: superserwer.conf was copied to /home/opc/configs for easytransfer.
::: Please use this profile only on one device and create additional
::: profiles for other devices. You can also use pivpn -qr
::: to generate a QR Code you can scan with the mobile app.
======================================================================
```

Konfigi są też zapisywane w `/etc/wireguard/configs`

[Instrukcja podłączenia się](https://docs.pivpn.io/wireguard/) - Aby się podłączyć na maszynie klienckiej umieszczamy ten konfig w folderze `/etc/wireguard/` i wołamy komendę `wg-quick up nazwapliku`🟩 any wystartować i `wg-quick down nazwapliku`🟥 aby zatrzymać.
(przydać się może paczka resolvconf)

## Storage

- [TrueNAS](https://www.truenas.com/) - system operacyjny dedykowany maszynm mającym służyć jako storage
- [Wtyczka do Cockpitu](https://github.com/45Drives/cockpit-file-sharing) pozwalająca na łatwe udostępnianie zawartości, jest też inna [wtyczka do przeglądania plików](https://github.com/45Drives/cockpit-navigator)
- [Duplicati](https://github.com/duplicati/duplicati) - apka do robienia backupów danych (wraz z opcją szyfrowania).

## Dla chcących postawić sobie jakiś serwer

Poszukiwanie VPS-a:

- [mikr.us](https://mikr.us/) - fajne i tanie serwery dla amatorów, jest trochę [dokumentacji](https://www.notion.so/MIKR-US-Don-t-Panic-5c3bdde2e0b545e7866524fc117446c3) i fajna społeczność ( [FB](https://www.facebook.com/groups/mikrusy) i [Discord](https://discord.gg/hFcqJGkppq))
- [Oracle free tier](https://www.oracle.com/pl/cloud/free/) - darmowe serwery VPS or oracle. Omówienie: [link pepper](https://www.pepper.pl/promocje/oracle-cloud-free-tier-darmowe-vpsy-z-ipv4-459055) **SIDENOTE**: jeśli instancje są nieużywane to mogą być automatyucznie wyłączane: [link](https://docs.oracle.com/en-us/iaas/Content/FreeTier/freetier_topic-Always_Free_Resources.htm#compute__idleinstances)
- [serverhunter](https://www.serverhunter.com/) - wyszukiwarka tanich VPSów (gdy mikrus nie starcza)

??? note "Oracle odblokowywanie portów"

    Jako, że maszyny od Oracle mają domyślnie publiczne IP to mają domyślnie nieco bardziej restrykcyjny firewall.
    [link do dokumentacji](https://docs.oracle.com/en-us/iaas/developer-tutorials/tutorials/apache-on-ubuntu/01oci-ubuntu-apache-summary.htm)
    Najpierw trzeba zmienić ustawienia w panelu na stronie oracle, a potem jeszcze dodać zasadę do iptables
    `sudo iptables -I INPUT 6 -m state --state NEW -p tcp --dport 80 -j ACCEPT`
    i jeśli to działa to możemy zapisać naszą zmianę
    `sudo netfilter-persistent save`

Oganianie domen:

- [tld-list](https://tld-list.com/) - porównywarka cen domen
- [seohost](https://seohost.pl/) - moim zdaniem najlepszy dostawca domen w Polsce


## Oszczędzanie energii

Tutaj jest jedna apka `powertop` można w niej podejrzeć jakie power states są obecnie na procesorze (C0, C1, C2...)

Ogólnie warto też zapoznać się z tym wideo.

https://youtu.be/MucGkPUMjNo?si=_4RVAnBg5IsMGqhp

## Szyfrowanie dysków oraz deszyfrowanie z pomocą TPM

Partycje można zabezpieczyć szyfrowaniem z pomocą LUKS-a.    
Tutaj jednak problemem może być automatyczne uruchomienie takiego systemu, aby nie było wymagane wpisywanie hasła ręcznie.

Tutaj z pomocą rzychodzi TPM.

https://fedoramagazine.org/automatically-decrypt-your-disk-using-tpm2/

