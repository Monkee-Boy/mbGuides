# Git Resources

## Installing Git

* <a href="http://code.google.com/p/git-osx-installer/downloads/list?can=3" title="Download git for OSX">Download git for OSX</a>
* <a href="http://code.google.com/p/msysgit/downloads/list?can=3" title="Download git for Windows">Download git for Windows</a>
* <a href="http://book.git-scm.com/2_installing_git.html" title="Download git for Linux">Download git for Linux</a>

## Dot Files

The follow .files are from [github.com/fleeting/dotfiles](https://github.com/jamesfleeting/dotfiles) and the most up to date versions can be found there.

### .gitconfig

```
[color]
   ui = auto
[color "branch"]
  current = yellow reverse
  local = yellow
  remote = green
[color "diff"]
  meta = yellow bold
  frag = magenta bold
  old = red bold
  new = green bold
[color "status"]
  added = yellow
  changed = green
  untracked = cyan

[alias]
  st = status
  cl = clone
  ci = commit
  cm = commit -m
  br = branch -v
  co = checkout
  pu = pull
  pr = pull --rebase
  go = checkout -B
  unstage = reset HEAD --
  cim = commit -a -m
  pom = !sh -c 'git h && echo Clear to push? Hit enter. && read && git push origin master' -
  df = diff
  tags = tag -l
  undopush = push -f origin HEAD^:master
  h = !git --no-pager log origin/master..HEAD --abbrev-commit --pretty=oneline
  lg = log -p
  lol = log --graph --decorate --pretty=oneline --abbrev-commit
  lola = log --graph --decorate --pretty=oneline --abbrev-commit --all
  ls = ls-files
	branches =› !legit branches
  remotes = remote -v
  sclone = svn clone -s
  spush = svn dcommit
  spull = svn rebase

[core]
  quotepath = false
  excludesfile = ~/.gitignore_global

[merge]
  log = true

[branch "master"]
  remote = origin
  merge = refs/heads/master

[user]
  name = YOUR NAME
	email = YOUR EMAIL

[init]
	templatedir = ~/.git_template
```

Most of the above aliases should be understandable. One to make note of is `pom`. This is basicaly `git push origin master` however before it pushes it will list out each commit you are about to push and ask you to confirm before pushing. This is very helpful when pushing multiple commits over a day or multiple days. This is also where being descriptive in commit messages helps a lot.

### .gitignore_global

```
# Compiled source #
###################
*.com
*.class
*.dll
*.exe
*.o
*.so

# Packages #
############
# it's better to unpack these files and commit the raw source
# git has its own built in compression methods
*.7z
*.dmg
*.gz
*.iso
*.jar
*.rar
*.tar
*.zip

# Logs and databases #
######################
*.log
*.sql
*.sqlite

# OS generated files #
######################
.DS_Store
.DS_Store?
._*
.Spotlight-V100
.Trashes
Icon
ehthumbs.db
Thumbs.db
.AppleDouble
.LSOverride

# Espresso #
############
*.esproj

# SublimeText #
###############
*.sublime-project
*.sublime-workspace

# TextMate #
############
*.tmproj
*.tmproject
tmtags

# vim #
#######
.*.sw[a-z]
*.un~
Session.vim

# SASS #
########
*.sass-cache

# SVN #
#######
.svn/

# NODE #
########
npm-debug.log
node_modules
```
