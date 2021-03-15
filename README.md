# Github / Gitflow and Python CLI Patterns Part 1 `mycli.py`

This exercise will teach you gitflow and common python CLI patterns. You will be able to use these in your work day to day and use them as foundations to build upon when creating CLI tools.
* Parsing arguments
* Reading text from files
* Reading settings from configs

## Recommended Setup: ##
* Linux Desktop or VM
* Sublime Text (or VSCode with equivalent plugins)
    * Syntax checking and linting (SublimeLinter, requires pylint) http://www.sublimelinter.com/en/stable/installation.html
    * GitGutter https://packagecontrol.io/packages/GitGutter
* python 3.7+
    * argparse https://pypi.org/project/argparse/
    * configparser https://pypi.org/project/configparser/
* Personal github account

## Reference materials: ##
* Python PEP8 Style Guide: https://www.python.org/dev/peps/pep-0008/
* Argparse: https://docs.python.org/3/library/argparse.html
* ConfigParser: https://docs.python.org/3/library/configparser.html
* Logging: https://docs.python.org/3/library/logging.html

## Getting started: ##
This is the first part of a set of exercises to create a simple CLI tool that takes arguments, reads a config, reads from a file and logs to a file. It is not supposed to be something useful or real, the desired end result is going to be the experience and learning; not the tool it’s self. This sort of pattern can be easily cherrypicked for code snippets.

First set yourself up a python environment with the above modules. These can be either installed with the systems package manager or with pip under your local user `--user`. Being linux / python there are many ways to achieve the same outcome. The easiest being local user installs of the required python modules.

Example setup on a Fedora machine:
```
[me@mypc]$ sudo dnf install python-pip
[me@mypc]$ pip install argparse --user
[me@mypc]$ pip install configparser --user
```

Fork my `mycli-exercise-1` repo into your own account.

## Exercise 1 Requirements ##
Once this exercise is complete your CLI tool will:
* Take input from a file which you will supply via an argument on the CLI `--file` https://docs.python.org/3/library/argparse.html#type - `type` set to `argparse.FileType()`
* Have a debug flag set via an argument on the CLI `--debug` This will alter the behaviour of the logging. When debug is enabled the script will log to both stdout and to the log file including `DEBUG` level messages. https://docs.python.org/3/library/argparse.html#action - `action` set to `store_true`
    * `DEBUG` level log each line read and how many characters it is.
    * `INFO` level log relevant events like starting reading and done reading.
* Have a configurable log file/path within the config file `mycli.conf`. A sample config `mycli.conf.example` is supplied. Copy the example file to `mycli.conf`. *We never put config files with secrets into git repos.* https://docs.python.org/3/library/configparser.html#quick-start
* Print each line of the file as it is processed in alphabetical order.
* The input file is included in the repo: myfile.txt.

## Exercise 1.1 - Gitflow. ##
Atlassian have a pretty good guide on the Gitflow workflow. https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow

Now that you have forked the `mycli-exercise-1` repo you can clone it to your local machine.

From here we'll create a feature branch from develop to begin adding the --file functionality to the skeleton `mycli.py`. Call it `feature/read_config_file`.

```
[me@mypc]$ git clone git@github.com:tdousset/mycli-exercise-1.git
[me@mypc]$ cd mycli-exercise-1
[me@mypc mycli-exercise-1]$ git checkout develop
[me@mypc mycli-exercise-1]$ git checkout -b feature/read_config_file
```

First thing to keep in mind is defensively programming. Assume files are missing and inputs are bad. For now, just print out the value in the config file for the log file.

### Hint: ###
- Use `os.path.isfile()` https://docs.python.org/3/library/os.path.html to validate the config file is present. But you need the path to the file first.
- You might be able to figure out the absolute path to the config file with the magic variable `__file__` https://docs.python.org/3/library/inspect.html#types-and-members and a combination of `os.path.x` functions.
- Exit the script if there is no config file and print an error message. `sys.exit(1)`.
- To use these modules you will need to import them at the top.
- You will need to `.get()` the `logfile` variable from within the `mycli` section of the config.

Once you have working code that reads the config, submit your branch for review (don't merge yet).