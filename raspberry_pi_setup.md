# pi setup

1. Install OS.
1. Addssh file to boot partition.
1. Turn on raspberry and connect to eth.
1. Log into raspberry via SSH.
1. Change password via passwd.
1. Set static IP in dhcpcd.conf

```sh
nano /etc/dhcpcd.conf

# Example static IP configuration:
interface eth0
static ip_address=192.168.1.200/24
#static ip6_address=fd51:42f8:caae:d92e::ff/64
static routers=192.168.1.1
static domain_name_servers=192.168.1.1 8.8.8.8 1.1.1.1 8.8.4.4 103.86.96.100 103.86.99.100
```

1. Copy ssh public key to raspberry with:

```sh

```

1. Mount disk with

```sh
sudo lsblk -o UUID,NAME,FSTYPE,SIZE,MOUNTPOINT,LABEL,MODEL
sudo blkid
sudo mkdir /mnt/storage2tb
sudo mount /dev/sda2 /mnt/storage2tb
```

1. Add disk to fstab.

```sh
sudo nano /etc/fstab
UUID=... /mnt/storage2tb ext4 defaults,nofail,x-systemd.device-timeout=1,noatime 0 0
```

1. Install docker. 

```sh
sudo apt-get update && sudo apt-get upgrade 
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
sudo usermod -aG docker $USER
sudo reboot
```

1. Install docker-compose.

```sh
sudo pip3 install docker-compose
```

1. Generate SSH keys.

```sh
ssh-keygen -t ed25519 -C "your_email@example.com"
touch ~/.ssh/config
Host *
  AddKeysToAgent yes
  IdentityFile ~/.ssh/id_ed25519

cat ~/.ssh/id_ed25519.pub

git clone git@github.com:emlagowski/htpc-download-box.git
```


```sh
tree -pufid /mnt/storage2tb | less
```
