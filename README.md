# Setting up custom python packages

I know of one or more reported cases where python imports failed.
Because python packages are arranged with reference to the file system structure, running a module that imports a package that is one-level up in the file hierarchy results in an `ImportError`.

This error can be resolved in any of the following ways:

1. Export `$PYTHONPATH` variable in your terminal
    ```bash
    export PYTHONPATH=.
    ```

    Check out this [Enthought article](https://support.enthought.com/hc/en-us/articles/204469160-How-do-I-set-PYTHONPATH-and-other-environment-variables-for-Canopy-) about other alternatives.

2. Programmatically append the module's base path to `sys.path`
    ```python
    import sys

    sys.path.append('./../')
    ```

3. Use Path entry finders ✔️
    While rambling about trying to run a module that imports a name from another module, I came upon a [documentation about Path entry finders in the packages section of python docs](https://docs.python.org/3.5/reference/import.html#package-path-rules)

    Simply set `__path__` to a list or tuple of paths where python can lookup modules.

    For my example package in this repository, I set `__path__ = ['./../']` in the module I that intend to run.

    ```bash
    python3 one/b.py
    two
    ```
