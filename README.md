# ssh-notes
SSH notes

- [ssh folder structure](#ssh-folder-structure)
- [config](#config)
  * [ssh-keygen](#ssh-keygen)
- [tools](#tools)
  * [ssh-keygen](#ssh-keygen)
  * [ssh-agent](#ssh-agent)

## ssh folder structure

```
.ssh/
  config
```

## config

OpenSSH per-user configuration file where you can store different SSH options for each remote machine you connect to.

This file is structured as follows:

```
Host hostname1
    SSH_OPTION value
    SSH_OPTION value

Host hostname2
    SSH_OPTION value

Host *
    SSH_OPTION value
```

The Host directive can contain one pattern or a whitespace-separated list of patterns that can contain some specifiers like:

* `*`: zero or more characters
* `?`: just one character
* `!`: negates the pattern (used at the start)

A full list of available ssh options can be found at: `man ssh_config`.

### example


## tools

### ssh-keygen

### ssh-agent
