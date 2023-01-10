# Zbiór różnych użytecznych narzędzi, frameworków , stron i bibliotek z któymi się spotkałem

## Praca z maszynami poprzez sieć

- [cockpit](https://cockpit-project.org/) - pozwala w prosty sposób monitorować serwer (poprzez apkę webową możemy się zalogować, uruchomić terminal, sprawdzać obciążenie, logi etc) ( [link to konfiguracji](https://cockpit-project.org/guide/latest/cockpit.conf.5))

  - Jeśli chcemy w cockpicie wygodnie zarządzać także portami warto doinstalować

- [linux-dash](https://afaqurk.github.io/linux-dash/#/system-status) - nieco prostsza alternatywa od cockpita

Narzędzia do monitorowania - długa lista <https://www.ubuntupit.com/most-comprehensive-list-of-linux-monitoring-tools-for-sysadmin/>

<details>
  <summary>COckpit + cloudflare tunnel</summary>
  <code>cat /etc/cockpit/cockpit.conf
[WebService]
Origins = <https://dashboard.xxxxx.ca> wss://dashboard.xxxxx.ca
ProtocolHeader = X-Forwarded-Proto
AllowUnencrypted = true</code>

[github source](https://github.com/cockpit-project/cockpit/issues/16396)

</details>

## Dokumentacja

- doxygen
- <https://readthedocs.org/>
- mkdocs
- <https://jekyllrb.com/>
- [Daux.io](https://daux.io/)

## Statystyki githuba i repozytoriów

- statystyki pobrań projektów - [github-release-stats](https://somsubhra.com/github-release-stats/) i [GithubStats](https://githubstats0.firebaseapp.com/)
- najaktywniejsze forki danego repo - [legacy](https://techgaun.github.io/active-forks/index.html), [nowa wersja](https://github.com/lukaszmn/active-forks)
- ststystyki użytkownika - [Coderstats](https://coderstats.net/)
- Graf gwiazdek - [star-history](https://star-history.t9t.io/?ref=producthunt)
- Liczenie linii kodu `cloc` (lokalnie) lub https://codetabs.com/count-loc/count-loc-online.html

## Dla chcących postawić sobie jakiś serwer

Poszukiwanie VPS-a:

- [mikr.us](https://mikr.us/) - fajne i tanie serwery dla amatorów, jest trochę [dokumentacji](https://www.notion.so/MIKR-US-Don-t-Panic-5c3bdde2e0b545e7866524fc117446c3) i fajna społeczność ( [FB](https://www.facebook.com/groups/mikrusy) i [Discord](https://discord.gg/hFcqJGkppq))
- [Oracle free tier](https://www.oracle.com/pl/cloud/free/) - darmowe serwery VPS or oracle. Omówienie: [link pepper](https://www.pepper.pl/promocje/oracle-cloud-free-tier-darmowe-vpsy-z-ipv4-459055)
- [serverhunter](https://www.serverhunter.com/) - wyszukiwarka tanich VPSów (gdy mikrus nie starcza)

Oganianie domen:

- [cloudflare](https://dash.cloudflare.com/) - must-have gdy masz jakąś domenę i nią zarządzasz
  - Cloudflare Proxy - zwiększa wydajność twoich stron oraz pozwala tunelować ruch IPv4 na adresy PIv6
  - [Tunelowanie](https://developers.cloudflare.com/cloudflare-one/connections/connect-apps/install-and-setup/tunnel-guide/) - pozwala wystawiać do sieci serwery z sieci lokalnych pozbawione publicznych adresów
- [tld-list](https://tld-list.com/) - porównywarka cen domen

Inne

- [ngrok](https://ngrok.com/) - pozwala łatwo udostępniać serwisy z urządzeń w sieci lokalnej. Dobre do prototypowania oraz prostych stron

## Inne

- [SearchCode](https://searchcode.com/) - przeszukiwanie baz z kodem źródłowym. Przydatne, gdy chcesz znaleźć przykłady wywoływania danej funkcji.
- [zerotier](https://www.zerotier.com/) - chyba najprostszy VPN

  - Gdy chcemy w sieci zerotiera postawić serwer DNS <https://github.com/zerotier/zeronsd>

- [Xonsh](https://xon.sh/) - odmiana shella (zamiennik dla klasycznego basha) bazujący na pythonie

```python
len($(curl -L https://xon.sh))

for filename in `.*`:
    print(filename)
    du -sh @(filename)
```
