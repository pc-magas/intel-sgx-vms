# Intel SGX Vms
Simple *VIRTUALBOX* vms allowing you to compile a C/C++ project with intel-SGX support (currently tested in simulation mode).


## Variations:

There are 2 variations:

* No GUI: A simple vm with bare minimum tools to share the code between Host and Guest.
* GUI: A minimal Fluxbox GUI with cairo dock and an editor.

In order to develop you must share the code files between guest and host first. Also ensure to install Virtualbox Guest addictions in order to rock & roll especially in GUI for maximum resolution.


## Install Guest Addictions (Tested wiuth virtualbox)

First of all instert the Guest Addictions Iso:
![Insert Guest Addictions](/img/guest_addictions_insert.png)

Then type the following commands:

```
# Optional only if NOT have install via repos
sudo apt-get purge virtualbox-guest-*

sudo mount /dev/sr0 /media/cdrom
cd /media/cdrom
sudo
./VBoxLinuxAddictions.run

sudo reboot
```

## Sharing Files between VM and Guest:

You can share files between host and guest either:

* Using the Guest Addictions anf Virtualbox share (not documented).
* Using nfs (supported in both).


## Share using nfs

First of all create a host-only network adapter and allow networking between host and guest as seen in Virtualbox's [documentation](https://www.virtualbox.org/manual/ch06.html#network_hostonly).

Then **share** via nfs your project's source code.

Than you can mount the nfs to the guest in theese ways (supposing you want to mount the nfs in `/home/user/my_project` folder):

* By typing:
  ```
    mkdir my_project
    sudo mount ^host^:^folder^ /home/user/my_project
  ```
  The `^host^` is the ip of the host maching of the host-only adapter, whilst the `^folder^` is the folder that is mounted the nfs share.

* Or by adding into `/etc/fstab` theese entries for more permanent and productive development:
  ```
  ^host^:^folder^ /home/user/my_project    nfs    defaults 0 0
  ```
