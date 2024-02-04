
#### Packaging
* Wheel is currently considered the standard for built and binary packaging for Python, Previously it was egg
- **Building a package or packaging** refers to the general activity of creating and distributing Python packages, which are bundles of Python code (usually as a compressed file archive) in a wheel format that can be distributed to other people and installed by a tool like **pip**
- Currently the standardised way to specify package metadata (things like package name, author, dependencies)  and the way to build packages from source code using that metadata, is specified in a **pyproject.toml** file. 
- **pyproject.toml** allows us to specify the build tool needed to build our packages. 
- Previously the build tool was assumed to be **setuptools** and much before that the **distutils**
- Previously **setup.py** or a **setup.cfg** was used, in place of pyproject.toml.
- Popular build tools nowadays include : [flit-core](https://github.com/pypa/flit/tree/main/flit_core), [hatchling](https://pypi.org/project/hatchling/), [pdm-backend](https://pdm-backend.fming.dev/), and [setuptools (>=61)](https://setuptools.pypa.io/en/latest/userguide/pyproject_config.html).
- Libraries and other dependencies that the project relied upon can be specified in **requirements.txt** or can be directly specified inline (inside setup.py or setup.cfg or pyproject.toml)