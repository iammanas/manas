---
author: "Manas"
title: "Installing Linuxbrew in Linux "
date: "2020-02-15"
description: "Installing Linuxbrew in Linux"
tags: [
    "Linux",
]
image: ""
---

---

## Check Git Version
 
Check your git version first by using the following command.

```bash
$ git --version
git version 2.9.5
```

## Manually install Linuxbrew to your preferred location.

Switch to the directory where you want Linuxbrew installed and execute these commands

```bash
git clone https://github.com/Homebrew/brew .linuxbrew/Homebrew
mkdir .linuxbrew/bin
ln -s ../Homebrew/bin/brew .linuxbrew/bin
eval $(.linuxbrew/bin/brew shellenv)
```

These commands are modified from the [Alternative Installation](https://docs.brew.sh/Homebrew-on-Linux#alternative-installation) section of the Homebrew on Linux docs in order to be location-agnostic. I installed to a special /extra/$USER location that has more space than my home directory on the system in question, but $HOME is a perfectly valid choice too.


Now, do which brew and you should see something like this:

```bash 
$ which brew
/manas/home/.linuxbrew/bin/brew
```


*Now some magic thing will happen after following below command*

Use the full path to brew from the last step to determine the correct line to add to your shell rc file. In my case, it is:

```bash
eval $(/manas/home/.linuxbrew/bin/brew shellenv)
```

Now, when I open a new session, I will have the brew command available. That's not the only trick though. We also need to add this line:

```bash
export HOMEBREW_NO_ENV_FILTERING=1
```


This allows Homebrew to see ~/.local/bin/ as a valid place to find git. Otherwise, it will stubbornly insist on using the ancient CentOS version, which will cause things to fail in interesting ways.








