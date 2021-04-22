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