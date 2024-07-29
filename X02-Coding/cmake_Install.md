
### Installation 
#### From binary

- Download the binary from `https://cmake.org/download/`
- Extract the binary `tar -xvf cmake-3.25.3-linux-x86_64.tar.gz`
- `mv [cmake-3.25.3-linux-x86_64 cmake-3.25.3`
- `sudo mv cmake-3.25.3 /usr/local`
- Update PATH in ~/.bashrc  - `export PATH=$PATH:/usr/local/cmake-3.25.3/bin`
- To uninstall `sudo rm -rf /usr/local/cmake-3.25.3` and remove the entry from 
PATH in .bashrc

#### From source

- Download the source from `https://cmake.org/download/`
- Choose the `Unix/Linux Source (has \n line feeds)`
	for ex:  cmake-3.25.3.tar.gz
- It is located at 
https://github.com/Kitware/CMake/releases/download/v3.25.3/cmake-3.25.3.tar.gz
- Extract it  `tar -xvf cmake-3.25.3.tar.gz`
- cd cmake-3.25.3
-  ./configure
-  make
-  sudo make install
-  To uninstall `sudo make uninstall`
