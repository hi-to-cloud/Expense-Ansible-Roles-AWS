### Ansible Roles

- follow DRY Principals __> Don't Repeat Yourself
- Role is a proper structure of variables, tasks, templates, handlers, ..etc
- with help of roles we can re use code

### /etc/ansible
![image](./img/ansible-roles.jfif)

### Folder Structure
```
│   ansible.cfg
│   BE.yml
│   DB.yml
│   FE.yml
│   inventory.ini
└───roles
    ├───be
    │   ├───tasks
    │   │       main.yml
    │   ├───templates
    │   │       backend.service.j2
    │   └───vars
    │           main.yml
    │
    ├───db
    │   ├───tasks
    │   │       main.yml
    │   └───vars
    │           main.yml
    │ 
    └───fe
        ├───handlers
        │       main.yml
        ├───tasks
        │       main.yml
        ├───templates
        │       expense.conf.j2
        └───vars
                main.yml
```
### ansible version
```
ansible --version
ansible [core 2.14.14]
  config file = /etc/ansible/ansible.cfg
  configured module search path = ['/root/.ansible/plugins/modules', '/usr/share/ansible/plugins/modules']
  ansible python module location = /usr/lib/python3.9/site-packages/ansible
  ansible collection location = /root/.ansible/collections:/usr/share/ansible/collections
  executable location = /bin/ansible
  python version = 3.9.18 (main, Jan  4 2024, 00:00:00) [GCC 11.4.1 20230605 (Red Hat 11.4.1-2)] (/usr/bin/python3)
  jinja version = 3.1.2
  libyaml = True
```
### Config file preference
```
1. export ANSIBLE_CONFIG=/tmp/ansible.cfg
2. in the current directory Ex: /home/ec2-user/ansible.cfg
3. in the home directory Ex: ~/.ansible.cfg
4. last preference __> /etc/ansible/ansible.cfg
```
```
ansible --version
ansible [core 2.14.14]
  config file = /tmp/ansible.cfg
  configured module search path = ['/root/.ansible/plugins/modules', '/usr/share/ansible/plugins/modules']
  ansible python module location = /usr/lib/python3.9/site-packages/ansible
  ansible collection location = /root/.ansible/collections:/usr/share/ansible/collections
  executable location = /bin/ansible
  python version = 3.9.18 (main, Jan  4 2024, 00:00:00) [GCC 11.4.1 20230605 (Red Hat 11.4.1-2)] (/usr/bin/python3)
  jinja version = 3.1.2
  libyaml = True
```
```
unset ANSIBLE_CONFIG
```
#### no need inventory/username/password
```
ansible-playbook -i inventory -e ansible_user=ec2-user -e ansible_password=DevOps321 db.yaml

#default ansible-config file
ansible-config =  /etc/ansible/ansible.cfg
```
#### vim ansible.cfg
```
[defaults]
inventory = inventory.ini
```
#### vim inventory.ini
```
[db]
db.step-into-iot.cloud
[be]
be.step-into-iot.cloud
[fe]
step-into-iot.cloud

[all:vars]
ansible_user=ec2-user
ansible_password=DevOps321
```
#### run playbooks
```
ansible-playbook DB.yml
ansible-playbook BE.yml
ansible-playbook FE.yml
```