
# Simple daily git workflow


|   |   |
|---|---|
| git pull  | pull all the changes from the remote repository  |
| git checkout -b branch-name-here  | create a new branch for your bug/feature/issue  |
| DO YOUR WORK HERE. keep it in small chunks, the smaller your commits the better, in case things go wrong |   |
| git add . | add any new les you ve created  |
| git status and/or git diff  | see the changes you re going to commit  |
| git commit -m “Detailed message here”  | make the commit with a nice detailed message  |
| git checkout master  | switch back to the master branch when the feature is done, your tests pass right?  |
| git merge branch-name-here | update the master branch to update the master with all your changes  |
| git push  | send your changes up to the remote repository  |

# Git notes

`git push` is like `git push origin master`

```
git push [remote-name] [branch-name]
```

git log --oneline --all

http://stackoverflow.com/questions/5361019/viewing-full-version-tree-in-git

# Git remotes

http://git-scm.com/docs/git-push
http://git-scm.com/book/en/v2/Git-Internals-The-Refspec

```
$ more .git/config 
[core]
	repositoryformatversion = 0
	filemode = true
	bare = false
	logallrefupdates = true
[remote "origin"]
	url = https://github.com/fgeorgy/webrename.git
	fetch = +refs/heads/*:refs/remotes/origin/*
[branch "master"]
	remote = origin
	merge = refs/heads/master
```

In the default case that is automatically written by a git remote add command, Git fetches all the references under refs/heads/ on the server and writes them to refs/remotes/origin/ locally. So, if there is a master branch on the server, you can access the log of that branch locally via

```
$ git log origin/master
$ git log remotes/origin/master
$ git log refs/remotes/origin/master
```

They’re all equivalent, because Git expands each of them to refs/remotes/origin/master.

```
$ git remote show origin
* remote origin
  Fetch URL: https://github.com/user/repo.git
  Push  URL: https://github.com/user/repo.git
  HEAD branch: master
  Remote branch:
    master tracked
  Local branch configured for 'git pull':
    master merges with remote master
  Local ref configured for 'git push':
    master pushes to master (up to date)
```

# Git info

```bash
francois@t917840 ~/dev/cyber/portail $ git remote show origin
* remote origin
  Fetch URL: git@git.etat-de-vaud.ch:/cyber/portail
  Push  URL: git@git.etat-de-vaud.ch:/cyber/portail
  HEAD branch: master
  Remote branches:
    16P3.C           tracked
    16P4.B           tracked
    agent-openam     tracked
    legacy           tracked
    master           tracked
    poc-openam-agent tracked
  Local branches configured for 'git pull':
    agent-openam merges with remote agent-openam
    master       merges with remote master
  Local refs configured for 'git push':
    agent-openam pushes to agent-openam (up to date)
    master       pushes to master       (local out of date)
francois@t917840 ~/dev/cyber/portail $ git config --get remote.origin.url
git@git.etat-de-vaud.ch:/cyber/portail
francois@t917840 ~/dev/cyber/portail $ cd ..
francois@t917840 ~/dev/cyber $ cd portail-master/
francois@t917840 ~/dev/cyber/portail-master $ git config --get remote.origin.url
git@git.etat-de-vaud.ch:/cyber/portail
francois@t917840 ~/dev/cyber/portail-master $ git remote show origin
* remote origin
  Fetch URL: git@git.etat-de-vaud.ch:/cyber/portail
  Push  URL: git@git.etat-de-vaud.ch:/cyber/portail
  HEAD branch: master
  Remote branches:
    16P3.C           tracked
    16P4.B           tracked
    agent-openam     tracked
    legacy           tracked
    master           tracked
    poc-openam-agent tracked
  Local branch configured for 'git pull':
    master merges with remote master
  Local ref configured for 'git push':
    master pushes to master (up to date)
francois@t917840 ~/dev/cyber/portail-master $ git remote -v
origin	git@git.etat-de-vaud.ch:/cyber/portail (fetch)
origin	git@git.etat-de-vaud.ch:/cyber/portail (push)
francois@t917840 ~/dev/cyber/portail-master $ git ls-remote
From git@git.etat-de-vaud.ch:/cyber/portail
a4bfed63037f72f231db038217f47768998824c6	HEAD
75cfc5aa0cc17cd198ee198d9dd9448ddb149069	refs/heads/16P3.C
61b4f61d602e8dfe9a5a36f8f2f82ff8cd965b42	refs/heads/16P4.B
effb116cec84ca33d2d1c0232ac51a889cbcdd60	refs/heads/agent-openam
e8b71883a38df1163c6b47a59d1b811c532a1af2	refs/heads/legacy
a4bfed63037f72f231db038217f47768998824c6	refs/heads/master
3296f49e3ec8dbb2fddfe6995d920354f3d23e34	refs/heads/poc-openam-agent
acfd1dcb1f8f541fc1264cca1e545b9aa9af358f	refs/tags/16P3.C.0
e7ccde3035aae34d128870d98cb64a8a77b6b5ee	refs/tags/16P3.C.0^{}
31fc069fb50bd2e0526b24fb7ebe31d9827a1495	refs/tags/16P3.C.1
1dca7d7b25bb70c366d84da0d49c0504b9503d2a	refs/tags/16P3.C.1^{}
aa1702703581ced8323c43915c62f11cebf3c404	refs/tags/16P4.B.0
61b4f61d602e8dfe9a5a36f8f2f82ff8cd965b42	refs/tags/16P4.B.0^{}
616c61c9109078e34032708b0d1b497d9302abc6	refs/tags/16P4.C.0
280be82aa5f6c995378713ac752f8066d9d43285	refs/tags/16P4.C.0^{}
francois@t917840 ~/dev/cyber/portail-master $ git remote show -n origin
* remote origin
  Fetch URL: git@git.etat-de-vaud.ch:/cyber/portail
  Push  URL: git@git.etat-de-vaud.ch:/cyber/portail
  HEAD branch: (not queried)
  Remote branches: (status not queried)
    16P3.C
    16P4.B
    agent-openam
    legacy
    master
    poc-openam-agent
  Local branch configured for 'git pull':
    master merges with remote master
  Local ref configured for 'git push' (status not queried):
    (matching) pushes to (matching)
francois@t917840 ~/dev/cyber/portail-master $ git branch -vv
* master a4bfed6 [origin/master] Déploiement des briques de base du portail en IN
francois@t917840 ~/dev/cyber/portail-master $ cd ..
francois@t917840 ~/dev/cyber $ cd portail
francois@t917840 ~/dev/cyber/portail $ git branch -vv
* agent-openam effb116 [origin/agent-openam] Changement du nom de l'agent
  master       047b2d9 [origin/master: behind 20] Passage au cyber-parent 2.4.0-SNAPSHOT pour avoir les nouvelles propriétés du configserver de dev -> slv1443v:47620
```

# Fetch unmergeg upstream pull-requests from other fork

http://stackoverflow.com/questions/6022302/how-to-apply-unmerged-upstream-pull-requests-from-other-forks-into-my-fork

Add:

```
[remote "source"]
    url = https://github.com/aterrien/jQuery-Knob.git
    fetch = +refs/heads/*:refs/remotes/source/*
    fetch = +refs/pull/*/head:refs/remotes/origin/pr/*
````

Do:

```
git fetch source
```

After the, merge any PR.

```
git merge master origin/pr/123
```

# Git resources

* http://marklodato.github.io/visual-git-guide/index-en.html
* http://marklodato.github.io/visual-git-guide/index-fr.html
* http://ndpsoftware.com/git-cheatsheet.html
* https://training.github.com/kit/downloads/github-git-cheat-sheet.pdf
* https://www.sonassi.com/wp-content/uploads/2012/07/simple_git_daily_workflow.pdf
* http://gitready.com/
* http://gitready.com/intermediate/2009/01/31/intro-to-rebase.html












