# Create patch
**Ref:** https://gist.github.com/stokito/434a129e4758489577502597c0a8c42b#file-create_patch-sh
## last three commits 
git format-patch -3 --stdout > multi_commit.patch
## all commits that are in your branch and not in master into a single patch file multi_commit.patch
git format-patch --signoff master --stdout > multi_commit.patch
## create patches in the folder ~/output/directory/ for all commits that are in your branch and not in master
git format-patch -o ~/output/directory/ --signoff master

