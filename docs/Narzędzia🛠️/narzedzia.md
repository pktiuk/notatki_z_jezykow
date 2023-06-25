# Zbiór różnych użytecznych narzędzi, frameworków , stron i bibliotek z któymi się spotkałem

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
