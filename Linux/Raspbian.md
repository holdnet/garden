# Raspbian

Find your Debian version:  

```
$ lsb_release -d
```

## Install Fish shell

**For Debian 9.0:**  

Keep in mind that the owner of the key may distribute updates, packages and repositories that your system will trust (more information).

```
$ echo 'deb http://download.opensuse.org/repositories/shells:/fish:/release:/3/Debian_9.0/ /' | sudo tee /etc/apt/sources.list.d/shells:fish:release:3.list
$ curl -fsSL https://download.opensuse.org/repositories/shells:fish:release:3/Debian_9.0/Release.key | gpg --dearmor | sudo tee /etc/apt/trusted.gpg.d/shells_fish_release_3.gpg > /dev/null
$ sudo apt update
$ sudo apt install fish
```

**For Debian 10:**  

Keep in mind that the owner of the key may distribute updates, packages and repositories that your system will trust (more information).

```
$ echo 'deb http://download.opensuse.org/repositories/shells:/fish:/release:/3/Debian_10/ /' | sudo tee /etc/apt/sources.list.d/shells:fish:release:3.list
$ curl -fsSL https://download.opensuse.org/repositories/shells:fish:release:3/Debian_10/Release.key | gpg --dearmor | sudo tee /etc/apt/trusted.gpg.d/shells_fish_release_3.gpg > /dev/null
$ sudo apt update
$ sudo apt install fish
```

## Install Build Essentials

```
$ sudo apt install build-essential
```

## Install Docker

```
$ curl -fsSL https://get.docker.com -o get-docker.sh
$ sh get-docker.sh
```
