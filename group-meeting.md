# How to increase productivity as a group member

Nov 13, 2024 for Mac only

1. We want to produce high quality work, constrained by time and stamina.
2. We must **choose the correct tools**.
3. We must **refine our habits** with those tools.

## 1. Configure command-line shortcuts

Set alias for longer commands in the Zsh and Bash shells:

> A shell is a CLI that briges between the OS and the human.

```
code  ~/.zshrc  # or ~/.bashrc
```

Add the following:

```
# My custom aliases, appliy via source ~/.zshrc
alias ga='git add'
alias gc='git checkout'
alias gpum='git pull upstream main'
alias grau='git remote add upstream'
alias gfa='git fetch --all'

# test
alias pt='pytest'
alias pc='pre-commit run --all-files'
```

Activate the alias

```
source ~/.zshrc  # or source ~/.bashrc
```

- Practice with pt and pc
- Add a new alias for ptc 

## 2. Utilize GH Command-line tool to save time

Install:
```
brew install gh
```

> Ref: https://github.com/cli/cli

Basic commands:

```
# Browse
gh browse

# View all PR
gh issue list
gh issue view 144
gh issue view 143 --web 
```

Important commands:

```
# List all opening PRs
gh pr list

# Check the differences
gh pr diff 154

# Checkout that PR
gh pr chckout 1

# View via web
gh pr view --web
```

> Ref: https://cli.github.com/manual/gh_pr_view

Useful command for release:

```
gh release list
```

## Conclusion

More future hands-on workshop available:

1. keyboard shortcuts (code editor)
2. Python best practices (PEP)
3. GitHub communicaiton rules
4. Writing 101 for programming (error message, docstrings, comments)

Lessons learned in Billinge Group
https://gitlab.thebillingegroup.com/resources/group-wiki/-/wikis/Lessons-learned-in-Billinge-Group





