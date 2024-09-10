# tldr: pipx is not ready for prime time, stick with venv for colrev dev and stable

- Different versions of pipx from different sources
- [TODO add link from official documentary]
- from apt: 1.10
- from pip: 1.7.1
  - not recommended, requires the usage of venv or --break system-packages
  - with venv prepared and active: $ python3 -m pip install --user pipx
  - install it globally: $ pip install pipx --break-system-packages

## Test scenarios

## Use pipx for colrev pip package
- $ sudo apt install pipx
- $ pipx install colrev --verbose
- $ colrev init # fails!
- Links not updated yet (new: colrev-environment), e.g. in colrev shell

## Use pipx for colrev development installation
- $ sudo apt install pipx
- Clone the colrev repository
- $ cd ~/Desktop/colrev # cd into repository
- $ pipx install -e .[dev,docs] --verbose
- $ colrev init # fails!
- $ pre-commit # missing!

## Use venv for colrev pip package
- $ python -m venv cvenv-stable
- $ source cvenv-stable/bin/activate
- $ pip install colrev
- $ colrev init # runs without issues!
- Links not updated yet (new: colrev-environment), e.g. in colrev shell
- Note: not supposed to enter colrev repo and run commands from there
  - no pylint
  - no pytest
  - no pre-commit 

## Use venv for colrev development installation
- $ python -m venv cvenv-dev
- $ source cvenv-dev/bin/activate
- cd into colrev repo
- pip install -e .[dev,docs]
- Create a test directory
- $ colrev init # runs without issues!

## Background

error: externally-managed-environment

× This environment is externally managed
╰─> To install Python packages system-wide, try apt install
    python3-xyz, where xyz is the package you are trying to
    install.  
    
    If you wish to install a non-Debian-packaged Python package,
    create a virtual environment using python3 -m venv path/to/venv.
    Then use path/to/venv/bin/python and path/to/venv/bin/pip. Make
    sure you have python3-full installed.
    
    If you wish to install a non-Debian packaged Python application,
    it may be easiest to use pipx install xyz, which will manage a
    virtual environment for you. Make sure you have pipx installed.
    
    See /usr/share/doc/python3.11/README.venv for more information.

note: If you believe this is a mistake, please contact your Python installation or OS distribution provider. You can override this, at the risk of breaking your Python installation or OS, by passing --break-system-packages.
hint: See PEP 668 for the detailed specification.

