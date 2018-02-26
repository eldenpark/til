```
git branch -r | awk -F/ '/\/feature-/{print $2}' | xargs -I {} git push origin :{}
```

### pipe v. xargs
https://superuser.com/a/600273

### Reference
https://coderwall.com/p/eis0ba/remove-a-thousand-stale-remote-branches-on-git