```
# My custom aliases, appliy via source ~/.zshrc

# Navigate
alias dev='cd /Users/imac/downloads/dev'
alias skpkg='cd /Users/imac/downloads/dev/bob/skpkg && mamba activate skpkg-env'
alias bobu='cd /Users/imac/downloads/dev/bob/my-package/bobleesj.utils && mamba activate bob-env'
alias caf='cd //Users/imac/downloads/dev/bob/my-package/CAF && mamba activate cifkit-env'
alias saf='cd /Users/imac/downloads/dev/bob/my-package/SAF && mamba activate cifkit-env'
alias cif='cd /Users/imac/downloads/dev/bob/my-package/cifkit && mamba activate cifkit-env'
# bob commands
alias bdlb='bob delete local-branches'
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
alias gpsh='git push'
alias gp='git pull'
alias grau='git remote add upstream'
alias grao='git remote add origin'
alias gpso='git push --set-upstream origin'
alias gfa='git fetch --all'
alias grv='git remote -v'
alias gcm='git commit -m'
alias gcam='git commit -a -m'
alias gce='git commit --allow-empty -m "ci: re-run CI with empty commit"'
alias gcb='git checkout -b'
alias gpum='git pull upstream main'
alias gpo='git push origin'
alias gl='git log'
alias gs='git status'
alias gd='git diff'
alias gb='git branch'
alias gr='git restore'

# for a new branch, set upstream to origin and push
alias gpsuo='git push --set-upstream origin $(git rev-parse --abbrev-ref HEAD)'
# Sync with main and create a new branch
alias gsub='gc main && git pull upstream main && gcb'
alias gsob='gc main && git pull && gcb'
# github CLI
alias gpcr='gh pr create'
alias gpl='gh pr list'
alias gpch='gh pr checkout'
alias gpvw='gh pr view --web'
alias gil='gh issue list'
alias ghb='gh browse'
alias ghbi='gh issue list --web'
alias gpv='gh pr view'
alias gbd='gh workflow run publish-docs-on-release.yml'
alias gbds='gh run list --workflow=publish-docs-on-release.yml'
# Combined
alias gpsuop='gpsuo && gpcr'
# Create news file, add, commit, push, and create PR with the same news title.
_make_pr() {
  TOOL="$1"        # e.g. "na" (which is aliased to a full package command)
  TITLE="$2"       # PR title
  FILL_FLAG="$3"   # "fill" or empty
  eval "$TOOL \"$TITLE\"" || return 1
  git add news/ || return 1
  git commit -m "news: $TITLE" || return 1
  BRANCH=$(git rev-parse --abbrev-ref HEAD)
  git push --set-upstream origin "$BRANCH" || return 1
  if [ "$FILL_FLAG" = "fill" ]; then
    gh pr create --title "$TITLE" --fill
  else
    gh pr create --title "$TITLE"
  fi
}
# scikit-package
alias na='package add news -a -m'
alias nf='package add news -f -m'
alias nc='package add news -c -m'
alias nr='package add news -r -m'
alias nd='package add news -d -m'
napr()  { _make_pr "na" "$1" ""; }
naprf() { _make_pr "na" "$1" "fill"; }
nrpr()  { _make_pr "nr" "$1" ""; }
nrprf() { _make_pr "nr" "$1" "fill"; }
nspr()  { _make_pr "ns" "$1" ""; }
nsprf() { _make_pr "ns" "$1" "fill"; }
ncpr()  { _make_pr "na" "$1" ""; }
ncprf() { _make_pr "na" "$1" "fill"; }
ndpr()  { _make_pr "nd" "$1" ""; }
ndprf() { _make_pr "nd" "$1" "fill"; }
gict() {
  gh issue create -t "$1" -b ""
}
# install
alias pi='pip install'
alias pir='pip install -r'
alias pie='pip install -e . && pip install -r requirements/test.txt'
alias mi='mamba install \
    --file requirements/test.txt \
    --file requirements/conda.txt'\
# conda/mamba
alias ma='mamba activate'
alias mao='mamba activate ophus-env'
alias mab='mamba activate bob-env'
alias mcn='mamba create -n'
mce() {
    folder_name=$(basename "$PWD")
    env_name="${folder_name}-env"
    mamba create -y -n "$env_name" python=3.13 \
        --file requirements/test.txt \
        --file requirements/conda.txt \
        --file requirements/docs.txt && \
        mamba activate "$env_name" && \
        pip install -e .
}
# test
alias pt='pytest'
alias pc='pre-commit run --all-files'
alias ptc='pytest && pre-commit run --all-files'
alias pb='python -m build'
alias doc='sphinx-reload doc'
alias testpypi='twine upload --repository testpypi dist/*'
# VS code
alias c='code .'
# bash
alias rmf='rm -rf'
alias rmd='rm -rf doc/_build'
# cookiecutter
alias cc='cookiecutter .'
