# Set up your python environment

### What you need

* pyenv -- to manage python versions
* venv - to manage virtual environents (comes with python 3)

### General approach

First, get `pyenv` up and running (which was a pain on OS X Big Sur), and use it to activate the version of python you want to use. Then clone your existing git repository, or if you are starting from scratch, create and empty one on GitHub and clone it. Inside the working folder, set up a local `venv` environment, and `source` it every time you need to work on files in the repository. Use `pip install` to install python packages in this environment, and `pip freeze > requirements.txt` to save the configuration in `requirements.txt`.

### Commands

#### Activate the right python version

```bash
$ python --version  # check the current version
2.7.1  

$ pyenv versions	# what versions are available
* system (set by /Users/dars/.pyenv/version)
  3.8.6

$ cd /to/repository/folder	# go to where you will work

$ pyenv local 3.8.6		# We will work on 3.8.6 whenever we are in this folder

$ python --version
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

```





