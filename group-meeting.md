# How to increase productivity as a group member

Nov 13, 2024 for Mac only

1. We want to produce high quality work, constrained by time and stamina.
2. We must **choose the correct tools**.
3. We must **refine our habits** with those tools.

## 1. Configure command-line shortcuts

Set alias for longer commands in the Zsh and Bash shells:

> A shell is a CLI that bridges between the OS and the human.


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
alias grv='git remote -v'
alias gcm='git commit -m'
alias gcb='git checkout -b'
alias gp='git pull'
alias gpo='git push origin'
alias gl='git log'
alias gs='git status'
alias gd='git diff'
alias gb='git branch'
alias gr='git restore'

# github CLI
alias ghpr='gh pr create'
alias ghprl='gh pr list'
alias ghprc='gh pr checkout'
alias ghil='gh issue list'
alias ghb='gh browse'

# install
alias pi='pip install'
alias pir='pip install -r'
alias pie='pip install -e . && pip install -r requirements/test.txt'
alias ci='conda install'

# conda
alias ca='conda activate'
alias ccn='conda create -n'
alias ccnt='conda create -n test_env python=3.13 \
    --file requirements/test.txt \
    --file requirements/conda.txt \
    --file requirements/build.txt'

# test
alias pt='pytest'

# format
alias pc='pre-commit run --all-files'

# test/format
alias ptc='pytest && pre-commit run --all-files'

# build
alias pb='python -m build'

# dist
alias testpypi='twine upload --repository testpypi dist/*'

# VS Code
alias c='code .'

# sphinx
alias doc='cd doc && make html && open build/html/index.html && cd ..'
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
gh pr checkout 1

# Create PR
gh pr create

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





