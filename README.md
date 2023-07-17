Created to demonstrate how passing a list of test files to `pytest` changes
the order in which our `conftest.py` hooks are called.

**Example 1**

Running `python -m pytest`, the output is:

```
OUTER
=================================================================== test session starts ====================================================================
platform darwin -- Python 3.9.16, pytest-7.4.0, pluggy-1.2.0
rootdir: /Users/scott/Code/pytest-order-example
collecting ... INNER
collected 2 items                                                                                                                                          

tests/test_outer.py .                                                                                                                                [ 50%]
tests/nested/test_nested.py .                                                                                                                        [100%]

==================================================================== 2 passed in 0.01s ===================================================================== 
```

(we see `OUTER` and then `INNER`)

**Example 2**

Running `python -m pytest tests/test_outer.py tests/nested/test_nested.py`, the output is:

```
INNER
OUTER
=================================================================== test session starts ====================================================================
platform darwin -- Python 3.9.16, pytest-7.4.0, pluggy-1.2.0
rootdir: /Users/scott/Code/pytest-order-example
collected 2 items                                                                                                                                          

tests/test_outer.py .                                                                                                                                [ 50%]
tests/nested/test_nested.py .                                                                                                                        [100%]

==================================================================== 2 passed in 0.00s =====================================================================
```

(we see `INNER` and then `OUTER`)

Note that the file order is the same as how `pytest` discovered them