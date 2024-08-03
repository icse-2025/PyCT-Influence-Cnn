# PyCT

The main objective of PyCT is to produce as a minimum number of different input arguments to achieve as much coverage of the target function as possible by feeding the produced arguments one in an iteration. The currently supported input arguments can only be integers or strings. Other types of arguments may be supported in the future.

---

## Abstract

Concolic testing is a software testing technique for generating concrete inputs of programs to increase code coverage and has been developed for years. For programming languages such as C, JAVA, x86 binary code, and JavaScript, there are already plenty of available concolic testers. However, the concolic testers for Python are relatively less. Since Python is a popular programming language, we believe there is a strong need to develop a good one.

Among the existing testers for Python, PyExZ3 is the most well-known and advanced. However, we found some issues of PyExZ3: (1) it implements only a limited number of base types’ (e.g., integer, string) member functions and(2) it automatically downcasts concolic objects and discards related symbolic information as it encounters built-in types’ constructors.

Based on the concept of PyExZ3, we develop a new tool called PyCT to alleviate these two issues. PyCT supports a more complete set of member functions of data types including integer, string, and range. We also proposes a new method to upcast constants to concolic ones to prevent unnecessary downcasting. Our evaluation shows that with more member functions being supported, the coverage rate is raised to (80.20%) from (71.55%). It continues to go up to (85.68%) as constant upcasting is also implemented.

---

## Prerequisites

- [Python](https://www.python.org/downloads/) version == 3.8.5<br>
  Basically, it should also work for other versions not lower than 3.8. Simply follow the usual installation instructions for Python.<br>

- [CVC4](https://github.com/CVC4/CVC4) commit version == [d1f3225e26b9d64f065048885053392b10994e715](https://github.com/cvc5/cvc5/blob/d1f3225e26b9d64f065048885053392b10994e71/INSTALL.md)<br>
  Since our CVC4 version has to cope with that of the base project PyExZ3 when we compare the performance of the two, our designated version above cannot be the latest. Otherwise, the CVC4 Python API bindings used in PyExZ3 cannot work.<br>The installation instructions for CVC4 is almost the same as that in the provided link, except that the configuration command should be modified to `./configure.sh --language-bindings=python --python3` for the use of CVC4 Python API bindings. A user must ensure by himself/herself that the command `cvc4` can be found by an operating system shell. Otherwise the tool may not work.<br>

- [pipenv](https://pypi.org/project/pipenv/)<br>
  This is required for the use of the virtual environment mechanism in our project. Install it as a usual Python package.<br>

- additional settings<br>
  1. For CVC4 to be findable by the Python API, `export PYTHONPATH={path-to-CVC4-build-folder}/src/bindings/python` should be put in `~/.bashrc`.
  2. For pipenv to create a virtual environment in each project folder, `export PIPENV_VENV_IN_PROJECT=1` should be put in `~/.bashrc`, too.

