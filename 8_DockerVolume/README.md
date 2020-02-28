##  Docker volumes

❖	Create docker volume named "dbvol" -> On the host parent machine -> folder but controlled by Docker -> “/var/lib/docker/volumes”

	$ docker volume create --name dbvol
	$ docker volume ls

❖	Run docker container from wordpress image and mount "dbvol" to /var/lib/mysql

$ docker run -it -v dbvol:/var/lib/Nish wordpress bash

Not needed creates on own

# mkdir /var/lib/Nish

# cd /var/lib/Nish	

# echo “Hello World” >> test.txt

# exit	

•	Even if we stop the container or delete it, volume is permanent
•	Re-running another docker container of wordpress after removing

$ docker run –it wordpress bash

•	Remapping but can have different directory of container

•	Docker inspect [id]

•	BCD!!!! By inspecting, default mounted volume
	Volume: permanent storage and communication
	Until container attached deleted, cannot delete volume 
	/var/lib/docker/volumes/[volumename]/_data/{}
	Container with full permission -> sudo -s

❖	Display all docker volumes.

	$ docker volume ls

❖	Create another docker volume named "testvol"

	$ docker volume create --name testvol
	$ docker volume ls

❖	Remove docker volume "testvol"

	$ docker volume rm testvol
