#### Prerequisites

* Install Pyenv 
~~~bash
  $ git clone https://github.com/pyenv/pyenv.git ~/.pyenv
  $ cd ~/.pyenv && src/configure && make -C src
~~~

* Configure the shell environment for pyenv
~~~bash
  # the sed invocation inserts the lines at the start of the file
  # after any initial comment lines
  sed -Ei -e '/^([^#]|$)/ {a \
  export PYENV_ROOT="$HOME/.pyenv"
  a \
  export PATH="$PYENV_ROOT/bin:$PATH"
  a \
  ' -e ':a' -e '$!{n;ba};}' ~/.profile
  echo 'eval "$(pyenv init --path)"' >>~/.profile

  echo 'eval "$(pyenv init -)"' >> ~/.bashrc
~~~
* Restart your login session for the changes to take effect.

#### Python

* Install python dependencies before installing a python version
~~~bash
  $ sudo apt update
  $ sudo apt install make build-essential libssl-dev zlib1g-dev libbz2-dev \
  libreadline-dev libsqlite3-dev wget curl llvm libncursesw5-dev xz-utils \
  tk-dev libxml2-dev libxmlsec1-dev libffi-dev liblzma-dev
~~~
* Now list the versions and Choose the appropriate version to install
~~~bash
  $ pyenv install -l
  $ pyenv install 3.12.0
~~~

* check the installed versions
~~~bash
  $ pyenv versions 

  * system (set by /home/phoenix/.pyenv/version)
    3.12.0

  $ python3 -V
    Python 3.11.0

  $ pyenv rehash

  $ which python
    /home/phoenix/.pyenv/shims/python
~~~

* make the newly installed python as the global
~~~bash
  $ pyenv global 3.12.0
~~~
* Location where pyenv installs python
~~~bash
  $ ls ~/.pyenv/versions/
~~~

* To uninstall a version 
~~~bash
  $ pyenv uninstall <version_name> 
      or
  $ rm -rf ~/.pyenv/versions/<version_name>
~~~

* To use the new python 
~~~bash
  $ pyenv global 3.12.0 
    	or
  $ pyenv local 3.12.0
      or
  $ pyenv global system  (to return to the system installation)
~~~

#### Poetry 

* Installation and Configuration
~~~bash
  # Install poetry via curl
  $ curl -sSL https://install.python-poetry.org | python3 -
~~~
* The installer installs the poetry tool to **$HOME/.local/bin**
* Add poetry to the PATH your bashrc `export PATH=$PATH:$HOME/.local/bin`
* After installation logout and login. Finally verify your installation
~~~bash
  $ poetry --version
~~~
* Configure poetry to create virtual environments inside the project's root directory
~~~bash
  $ poetry config virtualenvs.in-project true
~~~

* Uninstall poetry
~~~bash
  $ curl -sSL https://install.python-poetry.org | python3 - --uninstall
~~~

#### Barebones -  Without Pyenv 

* check the existing version of python, On ubuntu
~~~bash
  $ which python3
    /usr/bin/python3

  $ python3 -V
    Python 3.8.10
~~~

* create an alias in .bashrc `alias python='/usr/bin/python3'`
* Install pip
~~~bash
  $ sudo apt install python3-pip 
~~~
