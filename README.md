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

#### a simple one

If you want to connect to `my-domain-or-ip` using the user `me` we type

```bash
ssh me@my-domain-or-ip
```

In this case, we can edit our config file as follows:

```
Host my-server
    HostName my-domain-or-ip
    User me
    Port 22
```

And then, you can access your server by typing:

```
ssh my-server
```

#### a bit more complex one

```
Host targaryen
    HostName 192.168.1.10
    User daenerys
    Port 7654
    IdentityFile ~/.ssh/targaryen.key

Host tyrell
    HostName 192.168.10.20

Host martell
    HostName 192.168.10.50

Host *ell
    user oberyn

Host * !martell
    LogLevel INFO

Host *
    User root
    Compression yes
```

In this case, con config of `ssh targaryen` is clear. But if we use `ssh tyrrel`, it will combine the rules of `tyrrel`, `*ell`, `* !martell` and `*`. More info on this [here](https://linuxize.com/post/using-the-ssh-config-file/).

## tools

### ssh-keygen

```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```

> The last field in the ssh public key is a comment. By default it's initialized with the `user@host` value when the key was generated as a reminder. You can choose to edit it, it won't alter the key. This comment doesn't affect any authentication, it's only here to help manage multiple entries.

You can change the passphrase for an existing private key without regenerating the keypair by typing the following command:

```bash
ssh-keygen -p -f ~/.ssh/id_ed25519
```

### ssh-agent

With SSH keys, if someone gains access to your computer, they also gain access to every system that uses that key. To add an extra layer of security, you can add a passphrase to your SSH key. You can use `ssh-agent` to securely save your passphrase so you don't have to reenter it.

```bash
ssh-add ~/.ssh/id_ed25519
```
