# Create patch
## From commits
**Ref:** https://gist.github.com/stokito/434a129e4758489577502597c0a8c42b#file-create_patch-sh

Sample: Last three commits 
```bash
git format-patch -3 --stdout > multi_commit.patch
```
Sample: All commits that are in your branch and not in master into a single patch file multi_commit.patch
```bash
git format-patch --signoff master --stdout > multi_commit.patch
```
Sample: Create patches in the folder ~/output/directory/ for all commits that are in your branch and not in master
```bash
git format-patch -o ~/output/directory/ --signoff master
```
## From stash
Sample: From latest stash
```bash
git stash show -p stash@{0} > Stash0.patch
```
## Get branch of a specific commit
```bash
commit=fe116a929fd992f96c2860b38b6c641d9df7f60b
git branch --contains $commit
```
