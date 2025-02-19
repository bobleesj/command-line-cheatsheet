# How to Reuse and Share Code

Here you will learn 4 different levels of sharing.

## Level 1. Reuse functions inside a module

Assume you have a Python file called `calculator.py` and copy and paste the following block of code into the blank file.

```python
def multiply(*nums):
    result = 1  # Start with 1 because multiplying by 1 has no effect on the outcome
    for num in nums:
        result *= num  # Multiply each number with the result
    print(f'Multiplication result of {nums} = {result}')
```

Below the code block of `multiply`, copy the following to reuse `multiply`.

```python
print("Math problem 1")
multiply(1, 3)

print("Math problem 2")
multiply(2, 5, 4)
```

Run `python calculator.py`.

## Level 2. Share functions across modules

Imagine you have `hw1.py` that you want to use the `multiply` function. Here is the folder structure:

```text
my_project/
├── calculator.py
└── hw1.py
```

`calculator.py` is considered a single module because you are able to import the file into another Python file.

In `hw1.py`, copy and paste the following block to import the `calculator.py` module to use the `multiply` function:

```python
import calculator

print("Math problem 1")
calculator.multiply(1, 3)

print("Math problem 2")
calculator.multiply(2, 5, 4)
```

`calculator.multiply` can be a bit long. You may rename it by running the `import ... as ...` syntax:

```python
import calculator as calc

print("Math problem 1")
calc.multiply(1, 3)
```

Or, you may import the `multiply` funciton only from the `calculator.py` module.

```python
from calculator import multiply

multiply(1, 2, 3)
multiply(3, 5)
multiply(5.5, 5.5, 6.5)
```

## Level 3. Share functions across different directories within the same project

In Level 2, we had `calculator.py` and `hw1.py` within the same directory path:

```text
my_project/
├── calculator.py
└── hw1.py
```

Now, what if `calculator.py` is located under `utils` and  `hw1.py` under `solutions`? See the new folder structure below:

```text
my_project/
├── solutions/
│   └── hw1.py
└── utils/
    └── calculator.py
```

Now, we need to somehow import `utils/calculator.py` from another directory of `solutions/hw1.py`.

To do so, we need to manually let Python know that each `my_project`, `solutions`, `utils` are directories that are importable by having an **empty** `__init__.py` file. See below:

```text
my_project/
├── solutions/
│   ├── __init__.py
│   └── hw1.py
├── utils/
│   ├── __init__.py
│   └── calculator.py
└── __init
```

Then, you need to set the absolute path as the root path of your Python project.

For example, if your `my_projet` is located under `Users/imac/Downloads/dev/spring_2025`, run

```bash
export PYTHONPATH="${PYTHONPATH}:/Users/imac/Downloads/dev/spring_2025"
```

> If you want to know the current path within your Terminal, run `pwd`.

In `my_project/solutions/hw1.py`, copy and paste the following:

```python
from my_project.utils import calculator

calculator.multiply(2, 3)
```

Execute the code by running

```bash
python my_project/solutions/hw1.py
```

As you may see, the downside of this approach is that you have to manually run `export PYTHONPATH=...` above. In the next level of code sharing, this is no longer required.

## Level 4. Share code as an installable package

Here, the goal is to achieve what we did in Level 3, but as an installabe package.

Please following the new folder structure. Notice that `my_project` has been re-named to `team_project`.

```text
team_project/
├── src/
│   ├── team_project/
│   │   ├── solutions/
│   │   │   ├── __init__.py
│   │   │   └── hw1.py
│   │   ├── utils/
│   │   │   ├── __init__.py
│   │   │   └── calculator.py
│   └── __init__.py
└── pyproject.toml
```

There is a new file called `pyproject.toml`. Here we will define metadata. Copy and paste the following to `pyproject.tomml`.

```text
[build-system]
requires = ["setuptools>=62.0", "setuptools-git-versioning>=2.0"]
build-backend = "setuptools.build_meta"

[project]
name = "team-project"
dynamic=['version', 'dependencies']

[tool.setuptools.packages.find]
where = ["src"]  # list of folders that contain the packages (["."] by default)
```

In `src/team_project/solutions/hw1.py`, copy and paste the following.

```python
from team_project.utils import calculator

calculator.multiply(2, 3)
```

> Notice that the only difference is from `my_project` to `team_project`!

Then, install your `tema-project` package by running

```bash
pip install -e .
```

> `-e` means development mode. Each time you modify any part of the package under `src`, you do not have to re-install it.

Check that you have `team-project` installed by running

```bash
pip list
```

Execute your code by running

```bash
python python src/team_project/solutions/hw1.py  # Multiplication result of (2, 3) = 6
```

Congratulations! You have learned how to share code between two separate directories by creating a complete package!
