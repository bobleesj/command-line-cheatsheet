# How to increase productivity as a group member

Nov 13, 2024 for Mac only

## 1. Configure command-line shortcuts

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

## Utilize GH Command-line tool for visualization

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







