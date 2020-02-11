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

## 3) Install Nginx on Ubuntu Box Image

* Update the Linux packages
```
$ sudo apt-get update
```
* Install Nginx on Ubunut
```
$ sudo apt install nginx
```
* See the list of services that can access ports
```
$ sudo ufw app list
```
* Allow port access by disabling the firewall
```
$ sudo ufw enable  
```

* **Note:** Enabling the port access is insecure and must always be disabled before exiting the container.

* Allow Nginx HTTP service to use port 80
```
$ sudo ufw allow 'Nginx HTTP'
```
* Check port status if activated
```
$ sudo ufw status
```
* Install **systemd** package on Linux to use the **systemctl** command.
```
$ sudo apt-get install systemd
$ systemctl status nginx
```
* Get the IP address where the static Nginx website is hosted
```
$ curl -4 icanhazip.com
```

> Verify Nginx installation by opening the browser at `http://server_ip_address`

* Disable the port access to restart firewall
```
$ sudo ufw disable
```

## 4) Install Telnet in the Ubuntu Image
```
$ sudo apt-get install telnet
```

## 5) Package image as golden image

* Exit the virtual machine terminal and return to parent OS command line
```
$ exit
```
* Send the Power Off signal to virtual machine
```
$ vagrant halt
```
* Create a package.box file of the virtual box in current directory.
```
$ vagrant package
```
* Authenticate to Vagrant Cloud via command line.
```
$ vagrant cloud auth login
```

**Note:** `vagrant login` command is deprecated

## 6) Publish image on cloud

* Create the Image repository on [Vagrant Cloud](https://app.vagrantup.com/)
* Create new Vagrant Box -> `[username]/[box name]`
* Publish the package.box file from command line to Vagrant cloud
```
$ vagrant cloud publish [username]/[box name] [version] virtualbox package.box
```

## 7) Download the pushed image

* Create a new directory for the image to be pushed

```
$ mkdir nish
```
* Change directory to the new image
```
$ cd nish
```
* Initialize the vagrant file
```
$ vagrant init
```
* Edit vagrant file with OS name as the one created above in step 6 `[username]/[box name]`

## 8) Up the machine

**Note:** To download own package box, we need to release it first

* Launch the virtual machine via command line using Vagrant
```
$ vagrant up
```

* Access the terminal of the virtual machine
```
$ vagrant ssh
```
