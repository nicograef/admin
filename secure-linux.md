Assuming a new linux machine where logged in via `ssh root@host`

## Update System

```bash
sudo apt update
sudo apt upgrade
sudo apt dist-upgrade
```

## Create normal user

```bash
adduser nico # create new user
usermod -aG sudo nico # add user to sudo group

su - nico # switch to new user
sudo ls -la /root # check if user has sudo priviledges
```

## Switch from Password to Public Key Authentication and disallow root login

```bash
sudo cp /etc/ssh/sshd_config /etc/ssh/sshd_config.bak
sudo vim /etc/ssh/sshd_config
```

```diff
- #PubkeyAuthentication yes
+ PubkeyAuthentication yes
```

```diff
- PasswordAuthentication yes
+ PasswordAuthentication no
```

```diff
- PermitRootLogin yes
+ PermitRootLogin no
```
