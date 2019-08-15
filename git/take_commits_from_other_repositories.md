## Take commits from other repos
```
Clone projectB

git clone git clone <projectB repo URL>
Create an empty orphan branch

git checkout --orphan temp_branch
git rm -rf .
Add remote of projectA

git remote add -f projectA  <projectA repo URL>
Merge temp_branch with branchA from projectA

git merge projectA/branchA --allow-unrelated-histories
At this point you could move the contents as they are or also rewrite the history to make it seem that these files had always been in a sub folder.

NOTE: You have to chose one or the other either option 1 or option 2. Then you can continue the rest of the steps normally.

Move contents of temp_branch to sub folder and commit(without rewrite - option 1)

mkdir projectA
git mv -k * projectA/ 
git add .
git commit -m "Move projectA/branchA to sub folder" 
Move contents of temp_branch to sub folder and commit(with rewrite - option 2)

git filter-branch --tree-filter "mkdir projectA;git mv -k * projectA" HEAD
Merge with projectB/branchB

git checkout branchB
git merge temp_branch --allow-unrelated-histories
Delete temp_branch and projectA remote

git branch -D temp_branch 
git remote remove projectA
Push to projectB remote (make sure you are on branchB)

git checkout branchB
git push origin branchB
You should have merged the two while retaining the git history of both branches. Since the histories are unrelated I recommend using option 2 because it rewrites the history in such a way that it seems projectA always existed in its sub folder. Just my opinion though.

Final NOTE: that when moving the files to a sub folder, make sure you move any hidden files accordingly(one by one or all at once), I just used the * to give a simple example but you may have some .(dot) files that need to be moved too. Just make sure not to move the .git folder. I also used git mv instead of mv to ensure compatibility with windows if you are using a windows PC
```

https://stackoverflow.com/a/46629547
