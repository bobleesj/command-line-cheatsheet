# command-line-cheatsheet

This document contains commonly used commands for 
- GitHub
- Conda`
- conda-forge
- pip
- pre-commit
- Test PyPI
- Bash scripting

Feel free to fork and add more useful commands and flags as needed.

## Vim

Cursor nav
- H - move to top of screen
- M - move to middle of screen
- L - move to bottom of screen
- 0 / $ - move cursor to beginning / end
- b / B - move word left, b but skip special chracters

Edit
- D - delete everything on the right
- S - delete line and substitute text (same as cc)
- r - replace a single character.
- i - insert before the cursor
- I - insert at the beginning of the line
- A - insert (append) at the end of the line
- o - append (open) a new line below the current line
- O - append (open) a new line above the current line
- $d - From the current line to the end of the file
- 1d - From the current line to the beginning of the file
- dd - delete (cut) a line
- yy - yank (copy) a line

- u - undo
- U - restore (undo) last changed line
- . - repeat last command
- 5gg or 5G - go to line 5
- gg - go to the first line of the document
- zz - center cursor on screen
- zt - position cursor on top of the screen
- zb - position cursor on bottom of the screen

From: https://vim.rtorr.com/

## Tool

Get the tree structure

`brew install tree` and run `tree`

## GitHub

### Git revert - for shared repositories undo or go back to the previous commit pushed to public and shared remote

Assume you have 2 commits, and the last commit is a mistake. The last commit is called "bad mistake". Use `git revert HEAD` to undo the last commit, but this generates a third commit called `Revert "bad mistake"`. You can provide a specific commit ID for `revert`. An example from StackOverflow: assume you have four commit IDs `1, 2, 3, 4`. If you run `git revert 2`, it returns the state at `3`. This is the safe way since the commit history is preserved

### Git reset - undo changes that have not been shared

“You should never use `git reset` when any snapshots after have been pushed to a public repository. After publishing a commit, you have to assume that other developers are reliant upon it.” - https://www.atlassian.com/git/tutorials/undoing-changes/git-reset

- Reset does not make commits.
- It changes the pointer to a commit

`git reset` resets Staging to the last commit. Use `--hard` to also reset files in your Working directory to the last commit.

`HEAD~` is short for `HEAD~1`

`soft` does not change index (staging area) nor the files - but only the head

mixed/deafult changes the index but not the files

hard reset - resets index and working directory

```
# Delete remote branch
git push origin --delete cookierelease

# Delete local branch
git branch -D cookierelease

# Delete all branh
git branch | grep -v "main" | xargs git branch -D

# Delete all local tags
git tag -d $(git tag -l)

# Delete all remote tags
# git push origin --delete $(git tag -l)
```

Rest GitHub commit history (Know what you are done)

```
git checkout --orphan new-main HEAD~10
git add -A
git commit -m "Cleaned history: kept last 10 commits"
git branch -D main
git branch -m main
git push -f origin main
```

Git stash

```
# List all the stashes
$ git stash list
stash@{0}: WIP on admin_ui: 0c1a80a Removed annotation from JdbcAdminService, it is now explicity initialized in the applicationContext.
stash@{1}: WIP on admin_ui: 14e12e6 Added foreign keys for UserRole
stash@{2}: WIP on master: d188ecd Merge branch 'master' of semc-git:customercare
stash@{3}: WIP on master: 3763795 More work on user_details.
...

# Apply the latest stash, and remove it from the stack
$ git stash pop

# Apply a named patch, but leave it on the stack
$ git stash apply stash@{2} 

# Drop a stash
$ git stash drop stash@{3} 

# Clear the entire stash stack (almost never needed)
$ git stash clear

# A better way to purge the stash
$ git reflog expire --expire=30.days refs/stash

the `/refs/stash` file.

`git stash` does not commit but takes a snapshot of the local changes.

`git reset` creates a new commit point. It can jump back to any prior commit and also undo previous local changes.

`git stash save message` to add a custom message

`git stash push` also stash untracked files

`git stash pop` takes the files in the stash place and delete it from the histroy

`git stash show` inspect a summary

`git stash show diff` diff b/w a stashed change and the current state

`git stash apply` same as `git stash pop` but does not delete the history

`git stash list` displays history

`git stash drop` removes the latest stash

`git stash clear` removes all stashes
```

## GitHub

You want to force sync with your forked remote branch

```
git fetch origin
git reset --hard origin/main
```

## GitHub CLI

### Show readme
```bash
# Show readme
gh repo view

# Open URL
gh browse
```

### Pull request

```bash
# List
gh pr list
gh pr list --state open
gh pr list --state closed

# Status
gh pr checks 132

# Diff
gh pr diff 132

# Checkout
gh pr checkout 132

# Create
gh pr create
gh pr create --web
gh pr create --title "Fix codecov badge" --body "Closes #<issue number>"

# Review
gh pr review 132 --approve
```

### Issue

```bash
# List
gh issue list
gh issue list --label bug

# Delete
gh issue delete 132
gh issue delete 132 --yes

# Create
gh issue create --web
gh issue create --title "Fix codecov badet unknown problem" --label "documentation" --body "Double check the secret value"
```

### Workfow

```bash
# List available workflow(s)
gh workflow list

# View individual workflow
gh workflow view
gh workflow view check-news-item.yml --yaml
```

## Git

Not covering basic ones suhc as checkout, pull, etc.

```bash
# Fetch all tags, branches, etc. without merging to your local branches
git fetch --all

# Add tag locally
git tag -a 0.1.3 -m "Test PyPI pre-release"

# Push tag to remote origin
git push origin 0.1.3
```

## pip

```bash
# Install a list of packages in a file(s)
pip install -r requirements.txt
pip install -r pip.txt -r test.txt

# Install a specific version of a package
pip install bob==3.2

# Build and install your package to your environment
pip install .

# Build and install locally without using cache
pip install . --no-cache-dir

# Build and install locally without installing dependencies from metadata
pip install . --no-cache-dir --no-deps

# Build and install in development mode
# compiled binaries/extensions are located in the project folder, not the environment
pip install -e .

# Install a package from a .whl file
pip install bob-1.0.0-py3-none-any.whl

# Install a package from a source distribution (sdist) file
pip install https://example.com/package.tar.gz
```

## Conda

Create an environment with Python 3.12:
```bash
conda create -n bob_env python=3.12
conda activate bob_env
```

Create an environment with specific Python, dependencies:
```bash
conda create -n diffpy_utils_env python=3.13 \
    --file requirements/test.txt \
    --file requirements/conda.txt \
    --file requirements/build.txt
```

For Apple Silicon (M1/M2, arm64), set the environmet as if running on an Intel-based macOS (osx-64):

```bash
CONDA_SUBDIR=osx-64 conda create -n diffpy_utils_env python=3.13 \
    --file requirements/test.txt \
    --file requirements/conda.txt \
    --file requirements/build.txt
```

Confirm your environment:
```bash
conda config --show subdir  #  osx-arm64
```

Install the latest pre-release package in the `rc` channel:
```bash
conda install -c conda-forge/label/bob_rc -c conda-forge bob
```

Install specific version of the conda package:
```bash
conda install bob-1.4.4rc3-py312h9fbc349_2
```

Add/remove a new channel:
```bash
# Add channel
conda config --add channels conda-forge/label/bob_rc

# Remove channel
conda config --remove channels conda-forge/label/bob_rc
```

Once install, do a quick import test:
```bash
python -c "import bob; print(bob.__version__)"
```

### info

```
# List all available environments
conda env list

# Get info on current environment
conda info

# List packages installed
conda list
conda list -n bob
```


## conda-forge

Only relevent for conda-forge users:

```bash
# Install
conda install -n root -c conda-forge conda-smithy

# Rerender
conda smithy rerender

# Lint the meta.yaml file
conda smithy recipe-lint
```

## command-line shortcuts

Open up the shell configuration file using Visual Studio:

```bash
code  ~/.zshrc  # or ~/.bashrc
```

Copy the following to the file:

```bash
# My custom aliases, appliy via source ~/.zshrc

# Navigate
alias cdev='cd /Users/imac/downloads/dev'
alias cdutils='cd /Users/imac/downloads/dev/bg/diffpy.utils'
alias cdc='cd /Users/imac/downloads/dev/infra/cookiecutter'

# Visual studio
alias c='code .'

# Shortcuts
alias sc='code . ~/.zshrc'
alias ss='source ~/.zshrc'

# CV
alias cv='nodemon --exec python cv.py --watch . --ext py,json'

# git
alias ga='git add'
alias gc='git checkout'
alias gp='git push'
alias grau='git remote add upstream'
alias gpso='git push --set-upstream origin'
alias gfa='git fetch --all'
alias grv='git remote -v'
alias gcm='git commit -m'
alias gcb='git checkout -b'
alias gpum='git pull upstream main'
alias gpo='git push origin'
alias gl='git log'
alias gs='git status'
alias gd='git diff'
alias gb='git branch'
alias gr='git restore'

# git - check out a new branch synced with main
alias gcnb='gc main && gpum && gcb'

# github CLI
alias gpcr='gh pr create'
alias gpl='gh pr list'
alias gpch='gh pr checkout'
alias gil='gh issue list'
alias ghb='gh browse'
alias gpvw='gh pr view --web'
alias gpv='gh pr view'

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

# doc
alias doc='sphinx-reload doc'

# dist
alias testpypi='twine upload --repository testpypi dist/*'

# VS Code
alias c='code .'

# sphinx
alias doc-s='cd doc && make html && open build/html/index.html && cd ..'

# skpkg
alias cpnews='cp news/TEMPLATE.rst news/$(git rev-parse --abbrev-ref HEAD).rst'
```

Activate the alias:
```
source ~/.zshrc  # or source ~/.bashrc
```

## Sphinx preview

Use https://github.com/prkumar/sphinx-reload

```bash
pip install sphinx-reload
sphinx-reload docs
```

## Test PyPI

```bash
# Build pakcage and upload to Test PyPI
python -m build && twine upload --repository testpypi dist/*
```

## pre-commit

Run pre-commit

```bash
pre-commit run --all-files
```

## Bash scripting

### Bascis

The shebang line tells the system which interpreter to use to execute the script:

```bash
#!/bin/bash
```

Variable:

```bash
name="Bob"
echo "Hello world, $Bob!"
```

User inpput:

```bash
echo "What is your name?"
read name
echo "Hello, $name!"
```

For loop:

```
for i in {1..5}; do
    echo "Number $i"
done
```

Conditional statement:

```bash
echo "Enter a number:"
read num
if [ $num -lt 10 ]; then
    echo "The number is less than 10."
else
    echo "The number is 10 or greater."
fi
```

- `gt` for "greater than"
- `eq` for "equals"
- `ne` for "not equal"
- `le` for "less than or equal to"
- `ge` for "greater than or equal to"

While loop:

```bash
counter=1
while [ $counter -le 5 ]; do
    echo "Counter is $counter"
    ((counter++))
done
```

Function:

```bash
intro() {
    echo "Hi $1! You are $2 years old."
}
intro "Bob" 3
```

### Folder/file management

```bash
# $# is a special variable giving the # of arguments
if [ "$#" -ne 1 ]; then
    exit 1
fi

# Use the first argument as the root directory
root_dir="$1/*"

# Loop through each item in the root directory
for dir in $root_dir; do
    if [ -d "$dir" ]; then  # Check if it's a directory
        echo "Visiting directory: $dir"
        # Perform operations in "$dir"
    fi
done
```

To use, run `./script.sh /path/to/directory`.

Check a file exists:

```bash
# Check if a file exists
if [ ! -f "my_file.txt" ]; then
    echo "Error: File does not exist."
    exit 1
fi
```

`exit 1` (or any non-zero value) indicates that the script is terminated with an error.

## skpkg - Deploy sphinx doc via dispatch

```yml
name: Deploy Documentation

on:
  workflow_dispatch:

jobs:
  build-deploy:
      defaults:
        run:
          shell: bash -l {0}

      runs-on: ubuntu-latest
      steps:
        - name: Check out project
          uses: actions/checkout@v4
          with:
            ref: ${{ github.ref }}

        - name: Initialize miniconda
          uses: conda-incubator/setup-miniconda@v3
          with:
            activate-environment: build
            auto-update-conda: true
            environment-file: environment.yml
            auto-activate-base: false
            python-version: 3.13

        - name: Conda config
          run: >-
            conda config --set always_yes yes
            --set changeps1 no

        - name: Install  and docs requirements
          run: |
            conda install --file requirements/conda.txt
            conda install --file requirements/docs.txt
            python -m pip install -e . --no-deps

        - name: build documents
          run: make -C doc html

        - name: Deploy
          uses: peaceiris/actions-gh-pages@v4
          with:
            github_token: ${{ secrets.GITHUB_TOKEN }}
            publish_dir: ./doc/build/html
```

To see the rendered page, 

https://htmlpreview.github.io/?https://github.com/bobleesj/scikit-package/gh-pages/index.html

## References

- GitHub CLI https://cli.github.com/manual/
