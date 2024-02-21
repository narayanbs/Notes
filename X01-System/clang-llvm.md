
#### Prerequisites
~~~bash
  $ sudo apt-get update
  $ sudo apt-get upgrade
  $ sudo apt-get install build-essential curl xz-utils
~~~

#### Installation
* Download the binary and extract them
~~~bash
  $ curl -SL https://github.com/llvm/llvm-project/releases/download/llvmorg-17.0.2/clang-llvm-17.0.2-x86_64-linux-gnu-ubuntu-22.04.tar.xz | tar -xJ -C .
~~~
* rename and move to the appropriate location
~~~bash
  $ mv clang-llvm-17.0.2-x86_64-linux-gnu-ubuntu-/ clang_17.0.2
  $ sudo mv clang-llvm-17.0.2 /usr/local
~~~
* Update entries in .bashrc
~~~bash
  export PATH=/usr/local/clang_17.0.2/bin:$PATH
  export LD_LIBRARY_PATH=/usr/local/clang_17.0.2/lib:$LD_LIBRARY_PATH
~~~

You may need to install libncurses5 if you get libtinfo.so.5 error `sudo apt install libncurses5`
