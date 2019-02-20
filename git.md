# Git

## Remove commit

- local: `git reset --soft HEAD^`
- remote: `git push -f origin HEAD^:master`


## Stats

- commit stats per user:  `git shortlog -s -n --all`
- commit count: `git log --oneline --all | wc -l`
