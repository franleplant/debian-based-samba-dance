Install Samba in Debian/Ubuntu
========================

Easy steps to set a Samba server in Debian/Ubuntu.
This is my main setting to share files between a Vagrant managed guest on my Windows host.

> **{{SOME_NAME}}** indicates a placeholder for real information.

> For example: replace **{{USERNAME}}** for your desired username.

## Instructions

### Install Samba

```bash
sudo apt-get -y install samba
```

### Set Samba User

```bash
sudo smbpasswd -a {{USERNAME}}
```

It will prompt for a password, twice. Type

```bash
{{PASSWORD}}
```

### Set Samba config


```bash
sudo vim /etc/samba/smb.conf
```

At the beginning of the config file change this to your PC's WORKGROUP

```bash
[global]                 
   workgroup = {{WORKGROUP}} 
```


At the end of the config append this

```bash
[www]
path = {{PATH_YOU_WANT_TO_SERVE}}
available = yes
valid users = {{USERNAME}}
read only = no
browsable = yes
public = yes
writable = yes
```

> **{{PATH_YOU_WANT_TO_SERVE}}** for example `/var/www`.


### Connect

Type:
`Win + R`

And inside the `run` box type:
`\\192.163.1.102`

> **IMPORTANT!:** Assuming that is your Guest machine's public IP, replace it with your own.

> If you are using **Vagrant**, look for your `Vagrantfile`, open it and search for this line

> `config.vm.network :private_network, ip: "192.168.33.10"`

> Use that IP


Now, windows will ask for credentials, type **{{USERNAME}}** and **{{PASSWORD}}**

You should have access to your guest files from your host machine now.

Enjoy!

## Why?

Because Virtualization program shared folder don't play that well with Window's horrible file system, so when handling large code bases, say like a typical PHP project, the sync folder logic will make your Guest file system very slow, a typical site could take about 5 seconds to load with this config.
If your host machine is Linux/Unix based you should definitively use sync/shared folder, it's easier to set and easier to use.


## Ref

http://askubuntu.com/questions/19361/cant-access-ubuntus-shared-folders-from-windows-7
