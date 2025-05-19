```
# My custom aliases, appliy via source ~/.zshrc

# Navigate
alias dev='cd /Users/imac/downloads/dev'
alias skpkg='cd /Users/imac/downloads/dev/infra/skpkg && mamba activate skpkg-env'
alias bob='cd /Users/imac/downloads/dev/bobleesj/bobleesj.github.io'
alias bob-utils='cd /Users/imac/downloads/dev/bobleesj/bobleesj.utils'
alias caf='cd //Users/imac/downloads/dev/oliynyk/CAF && mamba activate cifkit-env'
alias saf='cd /Users/imac/downloads/dev/oliynyk/SAF && mamba activate cifkit-env'
alias cifkit='cd /Users/imac/downloads/dev/oliynyk/cifkit && mamba activate cifkit-env'

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
alias grao='git remote add origin'
alias gpso='git push --set-upstream origin'
alias gfa='git fetch --all'
alias grv='git remote -v'
alias gcm='git commit -m'
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

# check out a new branch synced with main
alias gcmpb='gc main && git pull && gpum && gcb'

# github CLI
alias gpcr='gh pr create'
alias gpl='gh pr list'
alias gpch='gh pr checkout'
alias gil='gh issue list'
alias ghb='gh browse'
alias gpvw='gh pr view --web'
alias gpv='gh pr view'

# Combined -
alias gpsuop='gpsuo && gpcr'

# install
alias pi='pip install'
alias pir='pip install -r'
alias pie='pip install -e . && pip install -r requirements/test.txt'
alias mi='mamba install \
    --file requirements/test.txt \
    --file requirements/conda.txt'

# conda
alias ma='mamba activate'
alias mcn='mamba create -n'
alias mcnt='mamba create -n test_env python=3.13 \
    --file requirements/test.txt \
    --file requirements/conda.txt \
    --file requirements/docs.txt'

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

# bash
alias rmf='rm -rf'
alias rmd='rm -rf doc/_build'

# cookiecutter
alias cc='cookiecutter .'

# Copy news/TEMPLATE.rst and readme based on current branch
alias cpnews='f() { cp news/TEMPLATE.rst news/$(git rev-parse --abbrev-ref HEAD).rst && vim news/$(git rev-parse --abbrev-ref HEAD).rst; }; f'
alias cpnews-no-vim='cp news/TEMPLATE.rst news/$(git rev-parse --abbrev-ref HEAD).rst'
alias cpnews-no='cp ~/Downloads/dev/bob-dev-utils/skpkg/no-news-file.rst news/$(git rev-parse --abbrev-ref HEAD).rst'

api() {
    IMPORT_NAME=$(basename "$(pwd)")  # e.g., "diffpy.utils"
    IMPORT_PATH=$(echo "$IMPORT_NAME" | tr '.' '/')  # e.g., "diffpy/utils"
    MODULE_PATH="src/$IMPORT_PATH"  # e.g., "src/diffpy/utils"
    DOC_PATH="doc/source/api"

    python "../release-scripts/auto_api.py" "$IMPORT_NAME" "$MODULE_PATH" "$DOC_PATH"
}
```
