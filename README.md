MVP showcasing an import issue with poetry importing a Rust package with namespace clashes

1. Download the wheel in https://github.com/migueltorrescosta/my_rust , under the dist folder.
2. Update the `PATH_TO_THE_WHEEL_IN_YOUR_SYSTEM` in `pyproject.toml` to use the downloaded wheel.

## Without my-rust as a dependency, we get

```shell
❯ poetry lock
Creating virtualenv my-python in /Users/mcosta/Pit/my_python/.venv
Updating dependencies
Resolving dependencies... (0.1s)
❯ poetry install
Installing dependencies from lock file
❯ poetry run python
Python 3.10.11 (v3.10.11:7d4cc5aa85, Apr  4 2023, 19:05:19) [Clang 13.0.0 (clang-1300.0.29.30)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> from my import python
>>> from my import rust
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ImportError: cannot import name 'rust' from 'my' (unknown location)
>>> 
```


## With my-rust as a dependency, we get

```shell
❯ poetry lock
Updating dependencies
Resolving dependencies... (0.1s)

Writing lock file
❯ poetry install
Installing dependencies from lock file

Package operations: 1 install, 0 updates, 0 removals

  • Installing my-rust (0.1.0 /Users/mcosta/Pit/test/my_rust-0.1.0-cp310-cp310-macosx_13_0_arm64.whl)
❯ poetry run python
Python 3.10.11 (v3.10.11:7d4cc5aa85, Apr  4 2023, 19:05:19) [Clang 13.0.0 (clang-1300.0.29.30)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> from my import rust
>>> from my import python
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ImportError: cannot import name 'python' from 'my' (/Users/mcosta/Pit/my_python/.venv/lib/python3.10/site-packages/my/__init__.py)
```

# Questions

1. Why does installing `my-rust` break `my-python` ?
2. What changes are needed to be able to install both `my-rust` and `my-python`?