```
git branch -r | awk -F/ '/\/feature-/{print $2}' | xargs -I {} git push origin :{}
```

```
git branch -r | grep -Eo 'issue/.*' | xargs git push --delete downstream
```

### pipe v. xargs
https://superuser.com/a/600273

### Reference
https://coderwall.com/p/eis0ba/remove-a-thousand-stale-remote-branches-on-git
https://stackoverflow.com/a/30619317
