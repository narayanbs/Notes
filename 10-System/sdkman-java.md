
#### sdkman 
* Open a terminal and enter  
~~~bash
  $ curl -s "https://get.sdkman.io" | bash
~~~
* Relaunch the terminal or enter the following 
~~~bash
  $ source "$HOME/.sdkman/bin/sdkman-init.sh"
~~~
* Check the installation with 
~~~bash
  $ sdk version 
~~~
* To upgrade sdkman version, use 
~~~bash
  $ sdk selfupdate 
    or
  $ sdk selfupdate force # in case the previous command fails
~~~

#### Java 
* Installing JDK using sdkman is pretty easy, List the available JDKs using 
~~~bash
  $ sdk list java
~~~
* choose the right jdk and install it
~~~bash
  $ sdk install java 8.0.265-open
~~~
* you can install multiple versions of JDK and you can verify the installation 
~~~bash
  $ sdk list java
~~~
* you can switch between versions 
~~~bash
  $ sdk use java 8.0.265-open
~~~
* or permanently
~~~bash
  $ sdk default java 8.0.265-open
~~~
* JAVA_HOME will be set to the following folder `~/.sdkman/candidates/java/current`

* Remove a version using `sdk uninstall java 8.0.265-open`

#### Uninstall sdkman
* To uninstall sdkman
~~~bash
  $ tar zcvf ~/sdkman-backup_$(date +%F-%kh%M).tar.gz -C ~/ .sdkman
  $ rm -rf ~/.sdkman
~~~
