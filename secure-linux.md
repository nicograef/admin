Based on this guide: [First steps to secure your Linux server](https://github.com/netcup-community/community-tutorials/blob/main/community-tutorials/first-steps-to-protect-your-linux-server-against-common-attacks/01-en.md)

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

Before switching:
1. generate new ssh keys via `ssh-keygen`
2. copy public key to `nico@remote:~/.ssh/authorized_keys`
3. make sure this works (might need changes via `chmod` or `chown`)

```bash
sudo cp /etc/ssh/sshd_config /etc/ssh/sshd_config.bak
sudo vim /etc/ssh/sshd_config
```

```diff
- #PubkeyAuthentication yes
+ PubkeyAuthentication yes

- PasswordAuthentication yes
+ PasswordAuthentication no

- PermitRootLogin yes
+ PermitRootLogin no
```

```bash
sudo systemctl restart sshd
```

## use firewall

```bash
sudo apt install ufw -y

sudo ufw default deny  # Close all ports by default, then open only those that are needed
sudo ufw allow ssh  # We open the port for SSH. If you changed the SSH port to something else than 22, replace `ssh` with your port number and /tcp i.e.: sudo ufw allow 2233/tcp
sudo ufw limit ssh  # Adds a rate limit of 6 attempted connections per 30 seconds to this port to prevent brute force attacks. Same as before, change ssh to your port/tcp if you don't use the default; limits can be changed in the ufw config.
sudo ufw enable  # Enable the UFW service
sudo systemctl enable ufw
sudo ufw status  # Check ufw settings afterwards
```
