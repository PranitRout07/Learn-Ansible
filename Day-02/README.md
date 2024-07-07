# SETUP ANSIBLE LAB USING DOCKER

### Step 1

##### Create two ubuntu docker container.
##### Master: 
```
sudo docker -itd --name ansible_master ubuntu /bin/bash
```

##### Slave:
```
sudo docker -itd --name slave ubuntu /bin/bash
```


### Step 2 

##### On master node install ansible,python3,openssh-clint,vim,iputils-ping

```
sudo apt update
sudo apt install -y python-is-python3 ansible openssh-client vim iputils-ping

```

### Step 3

##### On slave node install python3,ssh and vim only .

```
sudo apt update; sudo apt install -y python-is-python3 ssh vim
```

### Step 4 

##### Go to the slave node. Here go to /etc/ssh/sshd_config path to edit sshd_config . Here in the config allow password authentication .Then start the ssh service.
```
service ssh start
```

### Step 5

##### Setup a password on slave node.

```
passwd
```
### Step 6

##### Now go to master node , generate a ssh key.
```
ssh-keygen
```

### Step 7 

##### Now copy id inside the slave node .

```
ssh-copy-id <slave-name>@<ip-address>   (ip address can be found on the host machine using "docker inspect network bridge")
```

### Step 8

##### After the above command executed , then enter the password . Now you can ssh without any trouble .

```
ssh <slave-name>@<ip-address>
```

### Step 9 

##### Now create a file where you can mention the host names(slave machine name) on master node.

```
mkdir -p /etc/ansible
touch /etc/ansible/hosts

```
### Step 10

##### Now mention the host machine IP inside the hosts file

```
[slave]
<ip-address-of-slave>
```

### Step 11

##### Now use this command to ping the slave from master node.

```
ansible -m ping slave (also you can use ansible ping -m all)
```