### Normal
```bash
ssh s240
cd /opt/github/KantarProfiles

# verify you are ox0
ssh -T git@github.com
"Hi ox0! You've successfully authenticated, but GitHub does not provide shell access."

export REPO='busi-infrastructure'
git clone git@github.com:KantarProfiles/$REPO.git
cd $REPO

git status
git pull

export BRANCH='XXX/xxx-xxx'
git checkout -B $BRANCH

/opt/github/git.config.sh

# do modification here

git diff
git status

git add -A && git commit -a -m $BRANCH
git push --set-upstream origin $BRANCH

# clean up
cd /opt/github/Kantar_Profiles
\rm -rf $REPO
```
### Main changed
```bash
# merge the branch to new main
git fetch origin
git checkout $BRANCH
/opt/github/git.config.sh
git merge origin/main

# edit the conflicted files, then
git add <file(s)-you-fixed>
git commit   # completes the merge commit

git push origin $BRANCH

```

