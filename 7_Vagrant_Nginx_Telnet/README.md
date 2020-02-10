## Aim
```
1. Download an Ubuntu box from Vagrant Cloud
2. Launch Ubuntu Machine using Vagrant
3. Install nginx in Ubuntu Box Image.
4. Install Telnet package in same image.
5. Package this image as golden image using vagrant
6. Publish the same image on Vagrant Cloud.
7. Again download the pushed image
8. UP the downloaded golden image using vagrant
9. Host an HTML page in nginx server
10. Access the same HTML page from browser.
```
>

## 1) Downloading a Ubuntu virtual machine using Vagrant

* Create a new directory for Vagrant configuration
```
$ mkdir ubuntubox
$ cd ubuntubox
```
* Check successful installation of Vagrant
```
$ vagrant --version
```
* Initialize Vagrant in current directory using init command that creates the Vagrantfile.
```
$ vagrant init
```
* Make changes in vagrantfile and specify the OS image
```
config.vm.box="ubuntu/xenial64"
```

**Note:** Nginx does not work successfully with ubuntu/trusty64 images.

**Note:** Virtual Box must be opened in background before accessing terminal via Vagrant

## 2) Up the ubuntu machine

* Launch the virtual machine via Vagrant on command line
```
$ vagrant up
```
* Access virtual machine terminal via SSH (Secure Shell)
```
$ vagrant ssh
```

**Note:** To clear the windows CMD, use `cls` command.
