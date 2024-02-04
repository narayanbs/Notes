
#### Prerequisites

* Install NVM
* Node Version Manager (NVM) is a shell script that enables installation and management of multiple NodeJS versions. It is similar to pyenv. You can install/uninstall and set a specific version as default.

* To download the NVM script enter
~~~bash
  $ curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash
~~~
* Verify the installation
~~~bash
  $ source ~/.bashrc
  $ nvm --version
~~~

#### Node 

* Retrieve the set of NodeJS versions that can be installed
~~~bash
  $ nvm list-remote
~~~
* To install the latest LTS version
~~~bash
  $ nvm install --lts
~~~
* Verify the installation
~~~bash
  $ node --version
  $ npm --version
~~~

* To install a specific version
~~~bash
  $ nvm install 17.7.2
~~~

* Verify the installation as before
* To list all the versions of NodeJS installed on the system
~~~bash
  $ nvm ls
~~~
* To use another version of NodeJS
~~~ bash
  $ nvm use 17.7.2
~~~

* To set the default version of NodeJS, run
~~~bash
  $ nvm alias 17.7.2
~~~
* To uninstall a version use
~~~bash
  $ npm deactivate

  # for lts
  $ nvm uninstall --lts

  # for specific version
  $ nvm uninstall v17.7.2
~~~

#### yarn
~~~bash
  $ npm install --global yarn
~~~

#### Uninstall nvm
* To remove nvm manually 
~~~bash
  $ rm -rf "$NVM_DIR"
~~~

* Edit ~/.bashrc and remove the lines below
~~~bash
  export NVM_DIR="$HOME/.nvm"
  [ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm
  [[ -r $NVM_DIR/bash_completion ]] && \. $NVM_DIR/bash_completion
~~~
