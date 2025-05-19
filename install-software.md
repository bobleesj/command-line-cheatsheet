### Install mamba (macOS)

```
$ rm -rf /Users/<macbook-username>/miniconda3
$ rm -rf /Users/<macbook-username>/miniforge3 
$ curl -L -O "[https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-$(uname)-$](https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-$(uname)-$)(uname -m).sh"
$ bash Miniforge3-$(uname)-$(uname -m).sh
$ mamba shell init
```
