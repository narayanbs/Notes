##### New Project using Poetry (name: pydb)
```bash
$ poetry new pydb
$ cd pydb
	
	or

$ mkdir -p pydb/{pydb,tests} && cd pydb
$ touch pydb/__init__.py tests/__init__.py README.md
$ poetry init -n

# Inside pydb folder

	├── pydb
	│   └── __init__.py
	├── pyproject.toml
	├── README.md
	└── tests
	    └── __init__.py

# Specify a python version using pyenv
$ pyenv local 3.11.0

# update pyproject.toml, so that tool.poetry.dependencies reflect the chosen python version
$ vim pyproject.toml

[tool.poetry.dependencies]
python = "^3.11"

# Activate virtual environment
$ poetry shell 

# Add dependencies
$ poetry add pymysql[rsa]

# Dependencies will be reflected in pyproject.toml
	[tool.poetry.dependencies]
	python = "^3.11"
	pymysql = {extras = ["rsa"], version = "^1.1.0"}

# Add development dependenices 
$ poetry add --group=dev black flake8-bugbear isort mypy

# Development dependencies will be reflected in pyproject.toml
	[tool.poetry.group.dev.dependencies]
	black = "^24.2.0"
	flake8-bugbear = "^24.2.6"
	isort = "^5.13.2"
	mypy = "^1.8.0"

# create source files inside pydb/ and test files inside tests/

```
##### New Project using pip (name: pydjango)
```bash
$ mkdir -p pydjango/{pydjango,tests} && cd pydjango
$ touch pydjango/__init__.py tests/__init__.py pyproject.toml README.md

	├── pydjango
	│   └── __init__.py
	├── pyproject.toml
	├── README.md
	└── tests
	    └── __init__.py

# Specify a python version using pyenv
$ pyenv local 3.11.0

# create virtual environment and activate
$ python -m venv myenv
$ source myenv/bin/activate

# Install dependencies
$ pip install django~=4.0 black flake8-bugbear isort mypy
```

##### Python with MySQL - Prerequisite- Look at [[Docker#Docker Workflow Example|MySQL with docker]]
```bash
# start the mysql container 
$ docker start mysql-local

# go to the mysql prompt
$ docker exec -it mysql-local bash
bash#> mysql -uroot -p
Enter passsord: 

# Create a user
mysql> CREATE USER 'rev_user'@'%' IDENTIFIED BY 'slayer';

# create database and grant permission to rev_user
mysql> CREATE DATABASE revision;
mysql> GRANT ALL PRIVILEGES ON revision.* to 'rev_user'@'%';
mysql> use revision

# create a user table and insert some data
CREATE TABLE user (
  id INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
  email VARCHAR(255) NOT NULL UNIQUE,
  password VARCHAR(255) NOT NULL
);

INSERT INTO user (email, password) VALUES ('narayan@email.com', 'Admin123');

```
* Create a python project as shown above namely pydb
* It also indicates the driver required for connecting python to MySQL 
```bash
pip install PyMySQL[rsa]
or
poetry add PyMySQL[rsa]
```

**Python source**
```bash
# Create a python source file pydb/dbex.py in the pydb project mentioned above
# Add the following content

import pymysql.cursors
from pymysql import Error

try:
    connection = pymysql.connect(host='localhost',
                                user='rev_user',
                                password='slayer',
                                database='revision',
                                cursorclass=pymysql.cursors.DictCursor)


    with connection:
        db_info = connection.get_server_info()
        print(f"Connected to mysql server version {db_info}")
        with connection.cursor() as cursor:
            cursor.execute("select database();")
            result = cursor.fetchone()
            print(result)
except Error as e:
    print(f"Error while connection to MySQL {e}")
```
Run the above and check if the connection is working. 