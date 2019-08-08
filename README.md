All these examples are tested on EC Instance created using the AMI for Amazon Linux.

You can install ansible on any of the EC2 Instance created with Amazon Linux AMI using below command

```
sudo amazon-linux-extras install ansible2 
```

Verify ansible version using below.

```
ansible –version
```

You should see output similar to below



Below are some of the basic commands to start with


Test SSH connectivity with the local machine
```
ansible localhost -m ping	
```
create a new file 'inputfile.txt' in the user home directory on local machine
```
ansible localhost -m shell -a "touch inputfile.txt"	
```
list contents of home directory on the local machine
```
ansible localhost -m shell -a "ls -ltr /home/ec2-user"	
```
Install wget on local machine using the shell module
```
ansible localhost -m shell -a "yum install wget" -b	
```
Install wget on local machine using yum module (as root user)
```
ansible localhost -m yum -a "name=wget state=present" -b	
```
Uninstall wget from local machine, using yum module and elevate privileges to root 
ansible localhost -m yum -a "name=wget state=absent" -b	
```




