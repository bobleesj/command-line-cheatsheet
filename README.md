# command-line-cheatsheet

This document contains commonly used commands for 
- GitHub
- Conda`
- conda-forge
- Documentation (Sphinx)

Feel free to fork and add more useful commands and flags as needed.

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

# Build and install your package locally
pip install .

# Build and install locally without using cache
pip install . --no-cache-dir

# Build and install locally without installing dependencies from metadata
pip install . --no-cache-dir --no-deps

# Build and install in development mode
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
conda create -n bob_env \                                            
    python=3.12 \
    --file requirements/test.txt \
    --file requirements/run.txt \
    --file requirements/build.tx
```

For Apple Silicon (M1/M2, arm64), set the environmet as if running on an Intel-based macOS (osx-64):

```bash
CONDA_SUBDIR=osx-64 conda create -n bob_env \                                            
    python=3.12 \
    --file requirements/test.txt \
    --file requirements/run.txt \
    --file requirements/build.tx
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

## References

- GitHub CLI https://cli.github.com/manual/
