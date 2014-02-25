Install Samba in Debian/Ubuntu
========================

Easy steps to set a Samba server in Debian/Ubuntu.
This is my main setting to share files between a Vagrant managed guest on my Windows host.

## Instructions

### Install Samba

```bash
sudo apt-get -y install samba
```

### Set Samba User

```bash
sudo smbpasswd -a USERNAME
```

It will prompt for a password, type

```bash
PASSWORD
```

### Set Samba config


```bash
sudo vim /etc/samba/smb.conf
```

At the beginning of the config file change this to your PC's WORKGROUP

```bash
[global]                 
   workgroup = WORKGROUP 
```


At the end of the confi append this

```bash
[www]
path = /var/www
available = yes
valid users = vagrant
read only = no
browsable = yes
public = yes
writable = yes
```



### Connect

`Win + R`

`\\192.163.1.102`

Assuming that is your Guest machine's public IP, replace it with your own.




## Why?

Because Virtualization program shared folder don't play that well with Window's horrible file system, so when handling large code bases, say like a typical PHP project, the sync folder logic will make your Guest file system very slow, a typical site could take about 5 seconds to load with this config.
If your host machine is Linux/Unix based you should definitively use sync/shared folder, it's easier to set and easier to use.
