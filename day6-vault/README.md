Examples in this directory demonstrate the use of Ansible Vault to encrypt sensitive data inside files/varaibles referenced in
the Ansible playbooks. All the examples use localhost so there is no need to configure any remote hosts/additional instances to test these
examples, other than the Ansible control machine (on which Ansible is already installed)

You can encrypt a string varible defined in-memory using below command , and then use it inside a vars file reference by a playbook. (the --ask-vault-pass is optional in below command, if it is not mentioned, ansible will prompt for a password by default) 

```
ansible-vault encrypt_string --ask-vault-pass –name ‘ansible-pass’ password
OR 
ansible-vault encrypt_string  –name ‘ansible-pass’ password
```

Below are few ansible commands which opearate on an already created plain/text file

```
ansible-vault create secret.yml      
ansible-vault encrypt secret.yml
ansible-vault view secret.yml 
ansible-vault edit secret.yml 
ansible-vault rekey secret.yml
ansible-vault decrypt secret.yml
```


All of the below commands prompt for a password, which is used to encrypt/decrypt the file contents

```
ansible-vault create <file-name> :  Creates a new file , prompts for a paswword used to encrypt file contents and opens in edit mode , later saves the file as encrypted with the contents updated 
```

```
ansible-vault encrypt <file-name> : Encrypts an already-existing plain/text file 

ansible-vault decrypt <file-name> : Decrypts file which is earlier encrypted using ansible-vault and stores the file as plain-text
```

```
ansible-vault view <file-name>:  Displays the contents of a file encrypted earlier using ansible-vault, prompts for password which was provided when creating/encrypting the file using ansible-vault
```
  
```
ansible-vault edit <file-name>:  Edit the contents of a file encrypted earlier using ansible-vault, prompts for password which was provided when creating/encrypting the file using ansible-vault, and save the file (as encrypted) with changed contents  
```

As a default, all of the above commands, use a default vault id when encrypting the file contents. Below commands can be used to specify a vault-id which is associated with the file which is being encrypted.

```
ansible-vault --vault-id @prompt encrypt file1.txt  // this uses the default vault-id as we have not specified one
ansible-vault --vault-id vault1@prompt encrypt file1.txt   // associates vault1 (vault-id) with file1.txt 
ansible-vault --vault-id vault2@prompt encrypt file2.txt   // associates vault2 (vault-id) with file2.txt   
```

 Multiple files can be encrypted with different vault-ids as seen above. All of these files can be used/referenced  in a single playbook (refer ![multivault.yml](https://github.com/mandar-dindorkar/ansible-training/blob/master/day6-vault/multivault.yml) . You can executing such playbook using below command to specify the vault-id for each file, so that ansible prompts for password for decrypting each file at the time of execuing the playbook 
 
 ```
 ansible-playbook –-vault-id vault1@prompt –-vault-id vault2@prompt playbook.yml
 ```
