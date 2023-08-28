# My Ubuntu(22.04LTS) set up for development

**This document is for Ubuntu set up only.**  

I wrote this documentation for my future Ubuntu set up.  
Every time I reinstall Ubuntu, I had to search for install cammands and install.  
Ofcourse due to dependency issues, order of installations matters and that requires extra time.  
Setting up was a boaring work(most of the time), so I decided to write a set up guide for future me.

I hope this document helps me, and if possible others too.

## 1. Installations

Before installation, update install list.  

```bash
sudo apt get update
```

## 1-1. git(2023.08.28)

When it comes to development, **Git** is essential.  
For me, **Git** is number one priority in PC set up, not only because it is *important*, it's *used to install others*.  

I used to install git with `sudo apt install git`, but in the [git documentation](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git), they suggested using `git-all` instead.  
After reading this([git vs git-all](https://askubuntu.com/questions/796600/difference-between-installing-git-vs-installing-git-all)) post, I dicided to use `git-all`.

```bash
sudo apt-get install git-all
```

## 1-2. build-essential(2023.08.28)

```bash
sudo apt install build-essential
```

## 1-3. pyenv(2023.08.28)

Since *google colab* provides free cloud environment for python, I don't use local python that often.  
But when using local files with big size, or connecting to IP secured servers, local development is necessary.  
Since python version varies, and tend to change quite often(in my sense), I feel comfortable when they're managed with version controls(**pyenv**!!).  

I followed the [pyenv git's installation guide](https://github.com/pyenv/pyenv).

Install pyenv by cloning pyenv git.

```bash
git clone https://github.com/pyenv/pyenv.git ~/.pyenv
cd ~/.pyenv && src/configure && make -C src
```

Add pyenv PATH.  
(Below is for .bash. if you're using other shell, look up for shell specific commands [here](https://github.com/pyenv/pyenv#set-up-your-shell-environment-for-pyenv))

```bash
# for .bashrc
echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bashrc
echo 'command -v pyenv >/dev/null || export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bashrc
echo 'eval "$(pyenv init -)"' >> ~/.bashrc
source ~/.bashrc
# for .profile
echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.profile
echo 'command -v pyenv >/dev/null || export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.profile
echo 'eval "$(pyenv init -)"' >> ~/.profile
source ~/.profile
```

Before installing python from pyenv, **don't forget to install build dependencies**!([pyenv build dependencies](https://github.com/pyenv/pyenv/wiki#suggested-build-environment))

```bash
# pyenv's python build dependencies
sudo apt update; sudo apt install build-essential libssl-dev zlib1g-dev \
libbz2-dev libreadline-dev libsqlite3-dev curl \
libncursesw5-dev xz-utils tk-dev libxml2-dev libxmlsec1-dev libffi-dev liblzma-dev
```

Then, install python.

```bash
# install python(via pyenv)
pyenv install 3.11.5 
```

Replace `3.11.5` with other version names.  
You can view available python versions by `pyenv install --list` command.

And set the global python version as `<version>`.  

```bash
pyenv global <version>
```

For specific projects, you use a specific python version by executing below command **in project directory**.

```bash
python local <version>
```

Alternatively, you can set a python version for current shell session by `python shell <version>`

