# Set up your python environment

### What you need

* pyenv -- to manage python versions
* venv - to manage virtual environents (comes with python 3)

### Strategy

First, get `pyenv` up and running (which was a pain on OS X Big Sur), and use it to activate the version of python you want to use. Then clone your existing git repository, or if you are starting from scratch, create and empty one on GitHub and clone it. Inside the working folder, set up a local `venv` environment, and `source` it every time you need to work on files in the repository. Use `pip install` to install python packages in this environment, and `pip freeze > requirements.txt` to save the configuration in `requirements.txt`.

### Steps

#### Activate the right python version

We will assume `pyenv` is already set up. See instructions below for setting up `pyenv`.

```bash
$ python --version  				# check the current version
2.7.1  

$ pyenv versions						# what versions are available
* system (set by /Users/dars/.pyenv/version)
  3.8.6

$ cd /to/repository/folder	# go to where you will work

$ pyenv local 3.8.6					# Will use 3.8.6 whenever we are in this folder

$ python --version					# default local version is now 3.8.6
3.8.6
```

#### Set up and use a `venv` environment

```bash
$ python --version 		# make sure you have the right version
3.8.6

$ python -m venv my-env		# we are going to call the environment "my-env"

$ source my-env/bin/activate	# activate the new environment

(my-env) $			# environment prompt appears
(my-env) $ pip install numpy		# install packages
(my-env) $ pip freeze > requirements.txt		# save the environment
(my-env) $ pip install -r requirements.txt	# install from requirements.txt

$ deactivate		# will deactivate the active venv environment
$
```



### Setting up pyenv

Set up `pyenv` and install a version of python with the following commands:

```bash
$ brew install pyenv
$ pyenv install 3.8.6
```

And in `~/.zshrc` set the following to initialize `pyenv`:

```bash
eval "$(pyenv init -)"
```

##### OSX installation

Sometimes `$ pyenv install 3.8.6` can run into problems since the compiler does not see the path to `zlib` (and sometimes `bz2`) even if they are installed on the system. To fix this, do the following:

```bash
$ export LDFLAGS="-L/usr/local/opt/bzip2/lib -L/usr/local/opt/zlib/lib"
$ export CPPFLAGS="-I/usr/local/opt/bzip2/include -I/usr/local/opt/zlib/include"
$ brew install zlib 	# (if necessary)
$ brew install bzip2 	# (if necessary)
```

Then run

```bash
$ pyenv install 3.8.6
```

Add the two `export` commands to `~/.zshrc`.





