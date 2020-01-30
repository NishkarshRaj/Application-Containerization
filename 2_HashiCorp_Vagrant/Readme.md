## HashiCorp Vagrant Tool

**Aim:** Download and install Vagrant on the local machine. Create two virtual Machines with vagrant and ping them via their IP addresses.

**Commands used:**

 ```
 $ vagrant init
 $ vagrant up
 $ vagrant ssh
 $ vagrant halt
 ```

## Procedure

**Download HashiCorp Vagrant** 
Visit the official Vagrant website to download the software by using this [link](https://www.vagrantup.com/downloads.html)

**Check if Vagrant is successfully installed by using the following command on CMD**
```
$ vagrant --version
```

**Creating a virtual machine using Vagrant**

1. Using command line, create a new directory that will have vagrant configurations:
```
$ mkdir <<directory name>>
```

2. Move to the newly created directory
```
$ cd <<directory name>>
```

3. Initialize Vagrant configurations and create **Vagrantfile** by using the following command
```
$ vagrant init
```

4. Open the Vagrantfile and specify the OS you want to configure and the hardware resources to be allocated
To see the available machines we can import via vagrant from **Vagrant Cloud**, visit this [link](https://app.vagrantup.com/boxes/search)

5. Launch the Virtual machine from the command line on Oracle Virtual Box
```
$ vagrant up
```

6. Enter the Shell Terminal of the up machine from the Parent machine Command line
```
$ vagrant ssh
```

7. Exit the shell of Virtual Machine to return to parent OS command line
```
$ exit
```

8. Send the power off signal to the up VM
```
$ vagrant halt
```

## Ping one VM from another VM or the Parent OS command line

> To check default IP Address of machine, use the following command from VM Shell
```
$ ifconfig
```
The IP of the machine is the **inet address of enp**

> To change the default IP Address, close the machine and make changes in the Vagrant file. Relaunch the machine and fire ifconfig command again
```
Changes to be made in 'Create a Private Network' division
```

> Ping the machine using following command
```
$ ping <<IP Address>>
```
