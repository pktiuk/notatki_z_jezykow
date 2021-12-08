# Przydatne komendy git

## Włączanie i wyłączanie ignorowania zmian dla danego pliku

```bash
git update-index --skip-worktree default_values.txt

git update-index --no-skip-worktree default_values.txt

#list of files marked as skipped
git ls-files -v . | grep ^S
```

Albo:

```bash
git update-index --assume-unchanged <file>

#i aby cofnąć
git update-index --no-assume-unchanged <file>

```

## Sprzątanie

```bash
git reset #unstage all of files
git checkout . #revert all local uncommitted changes
git clean -fdx #remove all local untracked files
```

Usuwa wszystkie niezacommitowane zmiany.

## Sprzątanie w commitach (interactive rebase)

Inspirowane [artykułem](https://bulldogjob.pl/news/1503-jak-git-rebase-pomoze-ci-posprzatac-w-commitach).

```bash
git rebase -i JAK_DALEKO
#np
git rebase -i HEAD~3 #3 commity do tyłu
#lub
git rebase -i master
```

To jak głęboki ma być nasz rebase możemy określić jako ilość commitów (`HEAD~9` - czyli 9 commitów do tyłu), czy też względem innego brancha (np. mając feature branch wychodzęcy z mastera możemy zrobić rebase względem mastera).

Po zatwierdzeniu otrzymujemy listę commitów z którymi decydujemy co zrobić.

```bash
pick 56dc78c Poprawki do manipulacji tekstem
pick 57d9877 Podstawy templatek
pick b0675c9 Wykluczanie słów w regexach
pick 1c30565 Cockpit dodany do narzędzi

# Przestawianie 578f646..1c30565 na 1c30565 (4 polecenia)
#
# Polecenia:
# p, pick <zapis> = dobierz zapis
# r, reword <zapis> = użyj zapisu, ale przeredaguj jego komunikat
# e, edit <zapis> = użyj zapisu, ale zatrzymaj się, żeby go poprawić
# s, squash <zapis> = użyj zapisu, ale połącz go z poprzednim (spłaszcz)
# f, fixup <zapis> = jak „squash”, ale odrzuć komunikat tego zapisu
# x, exec <polecenie> = wykonaj polecenie (resztę wiersza) w powłoce
# b, break = zatrzymaj się tu (kontynuuj przestawianie przez „git rebase --continue”)
# d, drop <zapis> = usuń zapis
# l, label <etykietka> = nazwij bieżące HEAD
# t, reset <etykietka> = zresetuj HEAD do etykietki
# m, merge [-C <zapis> | -c <zapis>] <etykietka> [# <wiersz>]
# .       utwórz zapis scalenia używając pierwotnego komunikatu scalenia
# .       (albo <wiersza>, jeśli nie podano pierwotnego zapisu scalenia.
# .       Użyj -c <zapis>, aby przeredagować komunikat zapisu.
# Kolejność wierszy może być zmieniona; są wykonywane z góry na dół.
#
# Jeśli usuniesz tutaj wiersz, TEN ZAPIS BĘDZIE STRACONY.
#
# Jeśli jednak usuniesz wszystko, przestawianie zostanie przerwane.
#
# Zważ, że puste zapisy są wykomentowane
```

Następnie po wybraniu operacji zatwierdzamy i rozpoczynamy zmiany.
