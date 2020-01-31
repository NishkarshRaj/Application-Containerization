## Networking and Web Hosting using Vagrant

**Aim:** Configure two VM and install Nginx server in both of them. Create index.html file in one VM and host it and ping it via another Virtual Machine. Thence, upload the VM hosting the web server as a new Vagrant Box on the Vagrant Cloud.

## Procedure

1. Launch the first VM (say, Xenial Ubuntu)
```
$ vagrant up
```

2. Enter the shell terminal of the VM
```
$ vagrant ssh
```

3. Install the Nginx server on the virtual machine
```
$ sudo apt-get install nginx
```

4. Exit the shell of the VM and return control to parent CMD
```
$ exit
```

5. Power of the VM
```
$ vagrant halt
```

6. Create a deployable vagrant package of the updated VM
```
$ vagrant package
```

7. Login onto Vagrant Cloud from CMD using your credentials
```
$ vagrant login
```

8. Deploy the Vagrant box in default file **package.box** to vagrant cloud
```
$ vagrant cloud <<username>>/<<Box name>> <<Version number>> <<Hypervisor>> package.box
```

**Example:** `vagrant cloud noicecurse/nginx 1.0 virtualbox package.box`
