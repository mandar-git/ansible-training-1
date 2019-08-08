To demo the Ansible roles, clone the git repo into your local machine and run the playbook from the roles-examples directory

```
ansible-playbook roledemo.yml -i inv
```
Ansible Roles use the below directory structure for the playbook to work for tasks, varaibles and files defined as part of the role

└── roles

    └── mongo  (<role-name>)

        ├── templates

        │   ├── files
        
        │   │   └── mongod.repo

        │   ├── tasks

        │   │   └── main.yml

        │   └── vars

        │       ├── main.yml
        
   └── apache 

        ├── templates
        
        │   │   └── apache.conf

        │   ├── files
        
        │   │   └── changed.conf

        │   ├── tasks

        │   │   └── main.yml

        │   └── vars

        │       ├── main.yml
     
           
The playbook output should appear similar to below.  Here , we are using the inv file as inventory file, which specifies the IP address
10.0.1.178 as private IP of the EC2 instance on which the play book will execute tasks and install mongodb and apache

```
[root@ip-10-0-1-226 roles-examples]# ansible-playbook roledemo.yml -i inv

PLAY [all] ***************************************************************************************************************

TASK [mongo : Create mongo directory] ************************************************************************************
ok: [10.0.1.178]

TASK [mongo : configure yum repo] ****************************************************************************************
ok: [10.0.1.178]

TASK [mongo : install mongodb] *******************************************************************************************
ok: [10.0.1.178]

TASK [mongo : start mongod server] ***************************************************************************************
ok: [10.0.1.178]

TASK [mongo : verify mongodb is running] *********************************************************************************
 [WARNING]: Consider using service module rather than running service

changed: [10.0.1.178]

TASK [mongo : display mongod status output] ******************************************************************************
ok: [10.0.1.178] => {
    "msg": [
        "● mongod.service - SYSV: Mongo is a scalable, document-oriented database.",
        "   Loaded: loaded (/etc/rc.d/init.d/mongod; bad; vendor preset: disabled)",
        "   Active: active (running) since Thu 2019-08-08 11:29:21 UTC; 1min 42s ago",
        "     Docs: man:systemd-sysv-generator(8)",
        "   CGroup: /system.slice/mongod.service",
        "           └─3906 /usr/bin/mongod -f /etc/mongod.conf",
        "",
        "Aug 08 11:29:19 ip-10-0-1-178.ap-south-1.compute.internal systemd[1]: Starting SYSV: Mongo is a scalable, document-oriented database....",
        "Aug 08 11:29:19 ip-10-0-1-178.ap-south-1.compute.internal runuser[3902]: pam_unix(runuser:session): session opened for user mongod by (uid=0)",
        "Aug 08 11:29:21 ip-10-0-1-178.ap-south-1.compute.internal mongod[3891]: Starting mongod: [  OK  ]",
        "Aug 08 11:29:21 ip-10-0-1-178.ap-south-1.compute.internal systemd[1]: Started SYSV: Mongo is a scalable, document-oriented database.."
    ]
}

TASK [apache : Ensure httpd package is installed] ************************************************************************
ok: [10.0.1.178]

TASK [apache : Ensure httpd service is enabled and running] **************************************************************
ok: [10.0.1.178]

TASK [apache : Ensure configuration is updated] **************************************************************************
changed: [10.0.1.178]

TASK [apache : Ensure configuration is updated] **************************************************************************
ok: [10.0.1.178]

PLAY RECAP ***************************************************************************************************************
10.0.1.178                 : ok=10   changed=2    unreachable=0    failed=0
```
