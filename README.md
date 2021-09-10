# Magic Git Config

## Things to be changed

| Variable            | Quantity | Value                          |
| ------------------- | :------: | ------------------------------ |
| `[YOUR_NAME_HERE]`  |    2     | Your name (Ex: Henrique Leite) |
| `[YOUR_EMAIL_HERE]` |    2     | Your email address             |

## Contributing

Fork this project and add more commands, help the community!

## File Content

```sh
[user]
	name = [YOUR_NAME_HERE]
	email = [YOUR_EMAIL_HERE]

[pull]
	default = current

[push]
	default = current

[core]
	eol = lf # Defines eol using Linux format
	autocrlf = input

[alias]
	# Clean
	gone = "!f() { git fetch -p && git branch -vv | grep 'origin/.*: gone]' | awk '{print $1}' | xargs git branch -D; } ; f" # https://medium.com/darek1024/how-to-clean-local-git-branches-that-were-removed-on-the-remote-4d76f7de93ac
	cln = prune -v --progress # Remove Branches That No Longer Exists In Repository
	ignore = "!f() { git rm --cached `git ls-files -i --exclude-from=.gitignore`; } ; f" # Removes Files That Are In .gitignore From The Repository
	# Clone
	cn = clone # Clone Project
	cnsb = "!f() { git clone -b $* $*; } ; f" # Clone specific branch from project
	# Fork
	updfork = git fetch upstream # Update your fork
	# Remote
	rls = remote -v # Return a List of All Branches In Repository
	rrem = "!f() { git remote remove origin; } ; f" # Remove Origin Repository
	radd = "!f() { git remote add origin $*; } ; f" # Add A Repository as Origin
	ups = "!f() { git branch --set-upstream-to=origin/$1 $1; } ; f" # Set Branches Upstream
	# Master Branch
	pum = pull origin master # Pull From Master
	pom = push origin master -u # Push to Master
	# Add
	a = add . # Stage All Changes
	# Pull
	pl = pull # Get Project From Repository
	# Push
	ps = "!f() { git push -f; } ; f" # Push Changes to Repository
	psu = "!f() { git push --set-upstream; } ; f" # Create a Link Between Local Branch And Repository Branch
	acips = "!f() { git a && git ci $* && git ps; } ; f" # Stage Changes, Create Commit And Push To Repository
	acaps = "!f() { git a && git ca $* && git ps; } ; f" # Stage Changes, Amend Commit And Push To Repository
	acipsn = "!f() { git a && git commit -m \"$*\" --no-verify && git push --no-verify; } ; f" # git acips With --no-verify
	# Commit
	ci = "!f() { git commit -m \"$*\"; } ; f" # Stage Changes and Create Commit
	ca = "!f() { git commit --amend -m \"$*\"; } ; f" # Stage Changes and Amend Commit
	author = "!f() { git commit --amend --author=\"[YOUR_NAME_HERE] <[YOUR_EMAIL_HERE]>\"; } ; f" # Change Commit Author
	# Branch
	b = branch # List All Local Branches
	bd = "!f() { git branch -D $*; } ; f" # Delete Local Branch
	bn = "!f() { git branch -m $*; } ; f" # Change Branch Name
	# Checkout
	ckm = "!f() { git checkout master && git pull origin master; } ; f" # Change To master Branch And Git Pull
	ckd = "!f() { git checkout dev && git pull origin dev; } ; f" # Change To dev Branch And Git Pull
	ckp = "!f() { git checkout $* && git pull; } ; f" # Change Branch And Git Pull
	ck = "!f() { git checkout $*; } ; f" # Change Branch
	cb = "!f() { git checkout -b $*; } ; f" # Create New Branch
	# Rebase
	rbd = "rebase dev" # Rebase Actual Branch With dev Branch
	rbm = "rebase master" # Rebase Actual Branch With master Branch
	rbh = "!f() { git rebase -i HEAD~$*; } ; f" # Rebase commits (Merge multiple commits in one)
	rbc = "!f() { git a && git rebase --continue; } ; f" # Incase of conflict, you will have to fix it, and then, use this command to continue
	rmm = "!f() { git rebase -i origin/master~$* master; } ; f" # Merge all the commits of master branch
	# Stash
	sts = stash
	sta = stash apply
	std = stash drop
	stl = stash list
	stc = stash clear
	# Merge
	mg = merge --no-ff
	cat = checkout --theirs .
	cao = checkout --ours .
	# Log
	st = status # List Changes
	su = "!f() { git status --short | grep --color -E '^(AA|UU)'; } ; f"
	ss = "!f() { git status --short | grep --color -E '^(M |A |C )'; } ; f"
	sf = show --name-only
	lg = log --pretty=format:'%Cred%h%Creset %C(bold)%cr%Creset %Cgreen<%an>%Creset %s' --max-count=7 # Show the 7 latest commits minified
	incoming = !(git fetch --quiet && git log --pretty=format:'%C(yellow)%h %C(white)- %C(red)%an %C(white)- %C(cyan)%d%Creset %s %C(white)- %ar%Creset' ..@{u})
	outgoing = !(git fetch --quiet && git log --pretty=format:'%C(yellow)%h %C(white)- %C(red)%an %C(white)- %C(cyan)%d%Creset %s %C(white)- %ar%Creset' @{u}..)
	# Undo
	unstage = reset HEAD --
	undo = checkout . # Undo Changes
	rollback = reset --soft HEAD~1 # Undo last commit
	# Transfer
	tsf = "!f() { git show $1:$2 > $2 } ; f" # Move changes from a file to another
```

## Warnings

- The `git ignore` doesn't works on Windows
