Examples in this directory demonstrate the use of Ansible Vault to encrypt sensitive data inside files/varaibles referenced in
the Ansible playbooks. All the examples use localhost so there is no need to configure any remote hosts/additional instances to test these
examples, other than the Ansible control machine (on which Ansible is already installed)

You can encrypt a string varible defined in-memory using below command , and then use it inside a vars file reference by a playbook

```
ansible-vault encrypt_string <--ask-vault-pass> –name ‘ansible-pass’ password
```

Below are few ansible commands which opearate on an already created plain/text file

```
ansible-vault create secret.yml 
ansible-vault view secret.yml 
ansible-vault edit secret.yml 
ansible-vault rekey secret.yml
ansible-vault decrypt secret.yml
```

```
ansible-vault --vault-id @prompt encrypt file1.txt
ansible-vault --vault-id vault1@prompt encrypt file1.txt
ansible-vault --vault-id vault2@prompt encrypt file2.txt
ansible-playbook –-vault-id vault1@prompt –-vault-id vault2@prompt playbook.yml
```
